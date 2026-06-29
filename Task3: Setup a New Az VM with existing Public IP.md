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
  --name pri-vm \
  --location centralus \
  --image Ubuntu2404 \
  --size Standard_B1s \
  --admin-username azureuser \
  --generate-ssh-keys \
  --public-ip-address test-pip \
  --storage-sku Standard_LRS \
  --ssh-key-values ~/.ssh/id_rsa.pub
```
### **Step 3: Create Public IP if not exists**
```bash
az network public-ip create \
  --resource-group <existing_resource_group_name> \
  --name test-pip \
  --location centralus \
  --sku Standard \
  --allocation-method Static
```

### **Step 4: Verify VM state**
Verify whether the VM is running or not.
```bash
az vm show \
  --resource-group <existing_resource_group_name> \
  --name pri-vm \
  --show-details \
  --query "{VM:name, PublicIP:publicIps}" \
  --output table
```
