# Fortigate Standard Data Collection Rule

This template deploys a Data Collection Rule for Fortigate standard logs in Azure Monitor.

## Deploy to Azure

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FJohnnyMonteleoneCS%2FCost-Effective-Data-Collection-Rules%2Fmain%2Fazuredeploy.json)

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| workspaceName | string | Name of the Log Analytics workspace (auto-populated from selected resource group) |
| facilityName | string | Syslog facility name (local0-local7) |

## Notes

- Location and Resource Group settings are automatically inherited from the deployment context
- The DCR name is automatically generated as 'CS-Fortigate-Standard-DCR-{current-date}'
- Log Analytics workspace can be selected from a dropdown of available workspaces
- The DCR is configured for Linux systems with two data sources:
  - Primary facility logs (configurable: local0-local7)
  - NOPRI emergency logs
- Implements KQL transformations:
  - Traffic logs → Custom-Fortinet_CL
  - Non-traffic logs → Microsoft-CommonSecurityLog
- Created by Critical Start Repository
