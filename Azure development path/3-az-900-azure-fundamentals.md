# Azure development path
# AZ-900 Azure Fundamentals

## Azure CLI
### Advantages
- Stable (Text commands don't change and the CLI is in a stable state)
- Structured (CLI commands are structured very logically and all follow the same pattern)
- Cross platform (The CLI works on Windows, Mac and Linux)
- Automation (It is simple to automate the CLI commands for future use)
- Logging (Keep track of who ran what command and when in various ways)
- Install Azure CLI:
  https://learn.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest
  
### Basic Commands


## Azure PowerShell
- PowerShell is pre-installed on windows 
- install Azure modul in PowerShell:
  https://learn.microsoft.com/en-us/powershell/azure/install-az-ps?view=azps-9.4.0&viewFallbackFrom=azps-2.8.0
  
### Basic Commands
- ```az group list``` list resource groups
```
[                
  {
    "id": "/subscriptions/0f39574d-d756-48cf-b622-0e27a6943bd2/resourceGroups/72-6f955b93-accessing-and-using-the-azure-cloud-sh",
    "location": "centralus",
    "managedBy": null,
    "name": "72-6f955b93-accessing-and-using-the-azure-cloud-sh",
    "properties": {
      "provisioningState": "Succeeded"
    },
    "tags": null,
    "type": "Microsoft.Resources/resourceGroups"
  }
]
```

## Cloud Shell
- browser-accessible shell for managing Azure resources

### Featers
- Access from anywhere using web or mobile app. Authenticated and secure
- Choose between Bash (Azure CLI) or PowerShell
- Included tools:
  - Interpretres
  - moduls,
  - Azure tools
- Language support for Node.JS, .NET and Python
- Dedicated storage to persist data between sessions
- A complete file editor



