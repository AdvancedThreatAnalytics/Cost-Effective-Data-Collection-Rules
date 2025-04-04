# Fortigate Standard Data Collection Rule

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
| workspaceName | string | Name of the Log Analytics workspace (auto-populated from selected resource group) |
| facilityName | string | Syslog facility name (local0-local7) - Only for Fortigate DCR |

## Notes

- Location and Resource Group settings are automatically inherited from the deployment context
- Two deployment options available:
  1. Fortigate Standard DCR:
     - Name format: 'CS-Fortigate-Standard-DCR-{current-date}'
     - Configured for Linux systems with facility and NOPRI emergency logs
     - Implements traffic/non-traffic log transformations
  2. Workspace Transform DCR:
     - Name format: 'CS-Workspace-Transform-DCR-{current-date}'
     - Implements workspace query log transformations
     - Filters and transforms LAQueryLogs
- Created by Critical Start Repository
