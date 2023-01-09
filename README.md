# Create_Manage_Azure-Manage-Disk_Azure-Powershell

Step 1: Create a resource group an Azure managed disk using powershell:-

-Get-AzResourceGroup -Name az104-03a-rg1

-$location = (Get-AzResourceGroup -Name az104-03a-rg1).Location

-echo $location (save the location)

*Create new resource group name*:-
  $rgName = 'az104-03c-rg1'
  echo $rgname (save the location)

**New-AzResourceGroup -Name $rgName -Location $location
**Get-AzResourceGroup -Name $rgName (verify the resource group name)

1) To create a newly managed disk:-

 #creating a variable name diskconfig for disk configuration
   $diskConfig = New-AzDiskConfig Location $location CreateOption Empty  DiskSizeGB 32 Sku Standard_LRS
 #creating another variable diskName to keep value of new disk nam
  *$diskName = 'az104-03c-disk1'*

**New-AzDisk `
 -ResourceGroupName $rgName `
 -DiskName $diskName `
 -Disk $diskConfig

- Get-AzDisk -ResourceGroupName $rgName -Name $diskName


Step 2: Configure the managed disk by Azure Powershell:-

*New-AzDiskUpdateConfig -DiskSizeGB 64 | Update-AzDisk -ResourceGroupName $rgName -Diskname $diskName

*Get-AzDisk -ResourceGroupName $rgName -Name $diskName

*(Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku

*New-AzDiskUpdateConfig -Sku Premium_LRS | Update-AzDisk -ResourceGroupName $rgName -DiskName $diskName

*(Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku



