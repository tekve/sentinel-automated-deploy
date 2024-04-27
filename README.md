# Microsoft Sentinel All-in-One

## Try it now!

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Ftekveoy%2Fsentinel-automated-deploy%2Fmain%2Fazuredeploy.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2Ftekveoy%2Fsentinel-automated-deploy%2Fmain%2FcreateUiDefinition.json" target="_blank">
    <img src="https://aka.ms/deploytoazurebutton""/>
</a>


The azuredeploy.json contains the following steps:

1. Parameters of the deployment prompted via "createUiDefinition.json"
   
2. Create a resource group
   - Resource group name
   - Location
  
3. Create a new log analytics workspace
   - Resource group name
   - location
   - LAW name
   - pricing tier
   - daily quota
   - data retention
   - immediatePurgeDataOn30Days
   - capacity reservation (for commitment tier pricing)
  
4. Settings (entity diagnostics, ueba, diagnostic settings)
   - Workspace name
   - enable ueba
   - identity providers (to be synced with ueba)
   - enable diagnostics
  
5. Data Connectors (enable data connectors)
   - enableDataConnectors (bool)
   - aadStreams (which entra id logs to enable, default is Sign in logs and Audit logs)
   - Workspace name
   - subscription id
   - tenant id
   - location
  
6. Enable solutions and alerts
   - EnableSolutions1P (List of solutions to install, reference is below)
   - EnableSolutionsEssentials
   - EnableSolutionsTraining
   - Workspace name
   - Severity levels (of analytical rules to activate in the solutions)
   - enableAlerts (bool)
   - location
  
  This step calls a script located in this repository called "Create-NewSolutionAndRulesFromList.ps1".

*Moving on to the anatomy of the important script that handles enabling of solutions and analytical rules*

**Create-NewSolutionAndRulesFromList.ps1**

Command line: 

./Create-NewSolutionAndRulesFromList.ps1 
    -Workspace <workspaceName>            # Workspace name
    -ResourceGroup <resourceGroupName>    # Resource group name
    -Solutions <solutions>                # List of solutions
    -SeveritiesToInclude <severities>     # Severities of analytic rules to activate
    -Region <location>                    # Location of the resource group

# Script to deploy analytic rules


### References

To specify a solution to install use the format or list of following objects for multiple solutions:
"
{
    "label": "Microsoft Entra ID",
    "description": "The Microsoft Entra ID solution for Microsoft Sentinel enables you to ingest Entra ID Audit,Sign-in,Provisioning,Risk EveRisky User/Service Principal logs using Diagnostic Settings into Microsoft Sentinel.",
    "value": "Microsoft Entra ID"
}
"



