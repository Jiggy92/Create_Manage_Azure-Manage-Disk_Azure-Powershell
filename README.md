# Create_Manage_Azure-Manage-Disk_Azure-Powershell

Step 1: Create a resource group an Azure managed disk using powershell:-
    
      # fetching details of previously created resource group az104-03a-rg1
     _ Get-AzResourceGroup -Name az104-03a-rg1_

      # creating variable name location and assigning it location used for az104-03a-rg1
      _$location = (Get-AzResourceGroup -Name az104-03a-rg1).Location_   
    
      # display value of location variable
      _echo $location _
      
      # creating variable name rgname and assigning it a value of new rg name
      _$rgName = 'az104-03c-rg1'_
     
      # displaying variable rgname value
      _echo $rgname_
     
      # Finally creating a new resource group using 
       _New-AzResourceGroup -Name $rgName -Location $location_
      
      # Fetching details of newly created resource group
       _Get-AzResourceGroup -Name $rgName (verify the resource group name)_

Step 2: To create a newly managed disk:-

      ###### creating a variable name diskconfig for disk configuration
 
      _$diskConfig = New-AzDiskConfig Location $location CreateOption Empty  DiskSizeGB 32 Sku Standard_LRS_
   
      ###### creating another variable diskName to keep value of new disk name
 
      _$diskName = 'az104-03c-disk1'_

      #creating new disk using variables rgname,diskName and diskConfig
 
      _New-AzDisk -ResourceGroupName $rgName -DiskName $diskName -Disk $diskConfig_
      
      #fetching details of newly created disk

      _Get-AzDisk -ResourceGroupName $rgName -Name $diskName_


Step 3: Configure the managed disk by Azure Powershell:-

*New-AzDiskUpdateConfig -DiskSizeGB 64 | Update-AzDisk -ResourceGroupName $rgName -Diskname $diskName

*Get-AzDisk -ResourceGroupName $rgName -Name $diskName

*(Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku

*New-AzDiskUpdateConfig -Sku Premium_LRS | Update-AzDisk -ResourceGroupName $rgName -DiskName $diskName

*(Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku



