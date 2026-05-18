Step 1: Get the existing Resource group name
az group list - details of the existing groups
az group list --query "[0].name" -o tsv // get just the name


Step 2: Create VM
az vm create \                         
  --resource-group <existing_resource_group_name> \
  --name datacenter-vm \
  --image Ubuntu2204 \
  --size Standard_B2s \
  --admin-username azureuser \
  --generate-ssh-keys \
  --storage-sku Standard_LRS \
  --os-disk-size-gb 30

Step 3: Verify VM state
Verify whether the VM is running or not.

az vm get-instance-view \
  --resource-group <your-existing-rg> \
  --name datacenter-vm \
