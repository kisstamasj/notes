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
>Every VM on Azure is associated with at least one network security group. In this case, Azure created an NSG for you called my-vmNSG.

### List the rules
```
az network nsg rule list \
  --resource-group learn-9b4767ac-5b7a-4496-960e-9dfa3506898f \
  --nsg-name my-vmNSG
```

Nice output
```
az network nsg rule list \
  --resource-group learn-9b4767ac-5b7a-4496-960e-9dfa3506898f \
  --nsg-name my-vmNSG \
  --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
  --output table
```
>You see the default rule, default-allow-ssh. This rule allows inbound connections over port 22 (SSH). SSH (Secure Shell) is a protocol that's used on Linux to allow administrators to access the system remotely. The priority of this rule is 1000. Rules are processed in priority order, with lower numbers processed before higher numbers.

### Create the network security rule
```
az network nsg rule create \
  --resource-group learn-9b4767ac-5b7a-4496-960e-9dfa3506898f \
  --nsg-name my-vmNSG \
  --name allow-http \
  --protocol tcp \
  --priority 100 \
  --destination-port-range 80 \
  --access Allow
```
>For learning purposes, here you set the priority to 100. In this case, the priority doesn't matter. You would need to consider the priority if you had overlapping port ranges.

### Check the security rules
```
az network nsg rule list \
  --resource-group learn-9b4767ac-5b7a-4496-960e-9dfa3506898f \
  --nsg-name my-vmNSG \
  --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
  --output table
```

### Access your web server again
```
curl --connect-timeout 5 http://$IPADDRESS
```
