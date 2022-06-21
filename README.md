## bicep_quickstart
https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/quickstart-create-bicep-use-visual-studio-code?tabs=PowerShell

## Install Bicep VSCode Extension
VS Marketplace Link: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-bicep

## Code
```
@minLength(3)
@maxLength(24)
@description('Provide a name for the storage account. Use only lower case letters and numbers. The name must be unique across Azure.')
param storageName string

resource virtualNetwork 'Microsoft.Network/virtualNetworks@2019-11-01' = {
  name: 'examplevnet'
  location: resourceGroup().location
  properties: {
    addressSpace: {
      addressPrefixes: [
        '10.0.0.0/16'
      ]
    }
    subnets: [
      {
        name: 'Subnet-1'
        properties: {
          addressPrefix: '10.0.0.0/24'
        }
      }
      {
        name: 'Subnet-2'
        properties: {
          addressPrefix: '10.0.1.0/24'
        }
      }
    ]
  }
}

resource examplestorage 'Microsoft.Storage/storageAccounts@2021-02-01' = {
  name: storageName
  location: 'eastus'
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
}
```

## Upload main.bicep file into Azure - Not working

## Create Resource Group
```

az group create --name exampleRG --location eastus
```

## Deploy Bicep File
```
az deployment group create --resource-group exampleRG --template-file main.bicep --parameters storageName=uniquename
```

## Delete Resources
```
az group delete --name exampleRG
```
