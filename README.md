# Cost Effective Data Collection Rules

This template deploys Data Collection Rules for Fortigate logs and workspace transformations in Azure Monitor.

## Deploy to Azure

### Fortigate Standard DCR
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAdvancedThreatAnalytics%2FCost-Effective-Data-Collection-Rules%2Frefs%2Fheads%2Fmain%2Fazuredeploy.json)

### Workspace Transform DCR
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAdvancedThreatAnalytics%2FCost-Effective-Data-Collection-Rules%2Frefs%2Fheads%2Fmain%2FworkspaceTransform.json)

If the button above doesn't work, you can deploy manually:
1. Navigate to Azure Portal > Create a Resource
2. Search for "Template Deployment (Deploy custom template)"
3. Click "Build your own template in the editor"
4. Copy and paste the contents of [workspaceTransform.json](https://raw.githubusercontent.com/AdvancedThreatAnalytics/Cost-Effective-Data-Collection-Rules/refs/heads/main/workspaceTransform.json)
5. Click "Save" and proceed with the deployment

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| workspaceName | string | Name of the Log Analytics workspace (required for both DCRs) |
| facilityName | string | Syslog facility name (local0-local7) - Only for Fortigate DCR |

## Notes

- Location and Resource Group settings are automatically inherited from the deployment context
- Two deployment options available:
  1. Fortigate Standard DCR:
     - Name format: 'CS-Fortigate-Standard-DCR-{current-date}'
     - Configured for Linux systems with facility and NOPRI emergency logs
     - Implements traffic/non-traffic log transformations
  2. Workspace Transform DCR:
     - Fixed name: 'CS-WorkspaceTransformation-Standard-DCR'
     - Tagged with deployment timestamp for tracking
     - Transforms both AAD Non-Interactive User Sign-In Logs and Sign-In Logs
     - Removes specified fields and adds conditional access policy flags
     - Automatically associates with the target workspace as the default transformation rule
- Created by Critical Start Repository

## Workspace Transform Details

The following fields are removed from AAD Sign-in logs to optimize storage:

| Field | Type | Description |
|-------|------|-------------|
| SourceSystem | string | The type of agent the event was collected by |
| OperationName | string | For sign-ins, this value is always Sign-in activity |
| OperationVersion | string | The REST API version that's requested by the client |
| Category | string | Category of the sign-in event |
| DurationMs | long | The duration of the operation in milliseconds |
| ResourceGroup | string | Resource group for the logs |
| Identity | string | The identity from the token that was presented when you made the request |
| Level | string | The severity level of the event |
| Location | string | The region of the resource emitting the event |
| AlternateSignInName | string | Provides the on-premises UPN of the user signing into Azure AD |
| AuthenticationContextClassReferences | string | The authentication contexts of the sign-in |
| AuthenticationProcessingDetails | string | Provides the details associated with authentication processor |
| AuthenticationRequirementPolicies | string | Set of CA policies that apply to this sign-in |
| HomeTenantName | string | The tenant name of the external tenant who homes the entity |
| IsInteractive | bool | Indicates if a sign-in is interactive or not |
| IsTenantRestricted | bool | Indicates if a sign-in is under a tenant restrictions policy |
| IsThroughGlobalSecureAccess | bool | Displays whether or not a user came through Global Secure Access service |
| CreatedDateTime | datetime | Datetime of the sign-in activity |
| FederatedCredentialId | string | Federated Credential Id |
| GlobalSecureAccessIpAddress | string | Global secure IP address that user signed in from |
| ProcessingTimeInMs | string | Request processing time in milliseconds in AD STS |
| OriginalRequestId | string | The request id of the first request in the authentication sequence |
| SessionLifetimePolicies | string | Policies and settings that applied to the sign-in |
| SignInIdentifierType | string | The type of sign-in identifier |
| TokenIssuerName | string | Name of the identity provider |
| TokenProtectionStatusDetails | string | Indicates whether the sign-in token was bound to the device |

These fields are removed to reduce storage costs while maintaining essential security monitoring capabilities.
