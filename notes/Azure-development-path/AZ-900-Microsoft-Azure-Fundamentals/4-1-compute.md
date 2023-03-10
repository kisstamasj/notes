# Examples with Azure CLI

## Create VM, install Nginx webserver, and make it public

### Create VMs

```
az vm create \
  --resource-group learn-9b4767ac-5b7a-4496-960e-9dfa3506898f \
  --name my-vm \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

### Install Nginx in the VM

```
az vm extension set \
  --resource-group learn-9b4767ac-5b7a-4496-960e-9dfa3506898f \
  --vm-name my-vm \
  --name customScript \
  --publisher Microsoft.Azure.Extensions \
  --version 2.1 \
  --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' \
  --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
```

### Get VM IP address
```
IPADDRESS="$(az vm list-ip-addresses \
  --resource-group learn-9b4767ac-5b7a-4496-960e-9dfa3506898f \
  --name my-vm \
  --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
  --output tsv)"
```

### Download the home page
```
curl --connect-timeout 5 http://$IPADDRESS
```
It will time out. :) 

### List the current network security group rules
```
az network nsg list \
  --resource-group learn-9b4767ac-5b7a-4496-960e-9dfa3506898f \
  --query '[].name' \
  --output tsv
```
