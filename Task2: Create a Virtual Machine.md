### **Step 1: Get the existing Resource group name**
Details of the existing groups:
```bash
az group list
```
Get just the name: 
```bash
az group list --query "[0].name" -o tsv
```
### **Step 2: Create VM**
```bash
az vm create \                         
  --resource-group <existing_resource_group_name> \
  --name vm-cli \
  --image Ubuntu2404 \
  --size Standard_B2s \
  --admin-username azureuser \
  --generate-ssh-keys \
  --storage-sku Standard_LRS \
  --os-disk-size-gb 30
```

### **Step 3: Verify VM state**
Verify whether the VM is running or not.
```bash
az vm get-instance-view \
  --resource-group <your-existing-rg> \
  --name vm-cli \
```
