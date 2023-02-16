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
- ```az group list``` list resource groups
- ```az storage acount list``` list the storage account
- ```az vm list``` list virtual machines
- create virtual machine:
```
az vm create  `
>> --name LabVM `
>> --resource-group 72-3087af2d-accessing-and-using-the-azure-cloud-sh `
>> --image UbuntuLTS `
>> --admin-username azureuser `
>> --generate-ssh-keys
``` 
> The ssh key is stored in a ephemeral storage, so we have to save to a permanent storage location.

## Azure PowerShell
- PowerShell is pre-installed on windows 
- install Azure modul in PowerShell:
  https://learn.microsoft.com/en-us/powershell/azure/install-az-ps?view=azps-9.4.0&viewFallbackFrom=azps-2.8.0
  
 ### Basic commands
 - ```Get-AzResourceGroup``` list resource groups
 - ```Get-AzStorageAccount``` list the storage account
 - ```Get-AzVM``` list virtual machines
 - ```Get-AzResource | ft``` get all the resources with format
 - ```Remove-AzVM -Name LabVM -ResourceGroupName 72-3087af2d-accessing-and-using-the-azure-cloud-sh``` remove virtual machine

## Cloud Shell
Browser-accessible shell for managing Azure resources

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

## Azure Mobile App
- available on Android and iOS also

### Features
- The main aim of the app is to give you quick information on the go.
  - Alerts
  - Recently used resources
  - The health of your system
  - favourite resources
  - etc.
- Quick diagnose and potentially fix any issues
- It uses the Azure Resource Manager (ARM)
  - Azure CLI

## Azure Resource Group (ARM) templates
- Describe Resource usage
  - What are you updating, deleting, creating
- Common Syntax
  - Defined language for all ARM templates, making it easier to formalize and learn
- Idempotent
  - Every ARM template can be applied multiple times, and the result is always the same
- Written in JSON
- It can contain variables: ```{provided-unique-name}```

> Azure ARM Templates: https://learn.microsoft.com/en-us/samples/browse/?expanded=azure&products=azure-resource-manager

![image](https://user-images.githubusercontent.com/48266482/219310785-bc7e0087-781c-4e57-bab3-9de77b83d9b7.png)

### Benefits
- Idempotent
  - Run the same templates once, twice, or as many times as you like. It will have the same outcome
- Source Control
  - Keep track of all changes to the ARM templates
- Reuse
  - Use a combination of multiple partial ARM templates to achive glory - or at least complatex templates
- Declarative
  - Specify what you want, not how it is done
- No Human Errors
  - Automation means humans don't repeat the same mistakes

## Azure Advisor
The Advisor will provide recommendation to improve availability of resources, save costs on services increase reliability and a whole lot more.

> **Example**: 
> I have 10 virtual machines, where 2 of them are only used infrequently the Advisor will tell me to 
> turn off those 2 virtual machines, or at least make them a smaller size.

Security is also a large part of the recommandations given by the advisor.

> **Example**: You should have more then 1 assigned owner to your subscription.
> **Example**: FTPS should be required in your Functions app.
> **Example**: You should enable Azure Defender for DNS




