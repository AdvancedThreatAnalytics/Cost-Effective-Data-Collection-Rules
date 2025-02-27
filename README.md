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

- Location is automatically set based on the selected resource group's location
- Subscription and Resource Group are automatically used from the deployment context
- The DCR name is automatically generated as 'CS-Fortigate-Standard-DCR-{unique-suffix}'
- Make sure to specify a valid Log Analytics workspace Resource ID during deployment
- The workspace details can be found in your Log Analytics workspace's Properties page
- The DCR is configured for Linux systems
- Includes Syslog collection for both local0 and nopri facilities
- Implements KQL transformations for traffic and non-traffic logs
