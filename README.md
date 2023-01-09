# Create_Manage_Azure-Manage-Disk_Azure-Powershell

## Step 1: Create a resource group in Azure managed disk using powershell:-
    
      #fetching details of previously created resource group az104-03a-rg1
      Get-AzResourceGroup -Name az104-03a-rg1

      #creating variable name location and assigning it location used for az104-03a-rg1
      $location = (Get-AzResourceGroup -Name az104-03a-rg1).Location 
    
      #display value of location variable
      echo $location
      
      #creating variable name rgname and assigning it a value of new rg name
      $rgName = 'az104-03c-rg1'
     
      #displaying variable rgname value
      echo $rgname
     
      #Finally creating a new resource group using 
       New-AzResourceGroup -Name $rgName -Location $location
      
      #Fetching details of newly created resource group
       Get-AzResourceGroup -Name $rgName (verify the resource group name)

## Step 2: To create a newly managed disk:-

       #creating a variable name diskconfig for disk configuration
 
       $diskConfig = New-AzDiskConfig Location $location CreateOption Empty  DiskSizeGB 32 Sku Standard_LRS
   
       #creating another variable diskName to keep value of new disk name
 
       $diskName = 'az104-03c-disk1'

       #creating new disk using variables rgname,diskName and diskConfig
 
       New-AzDisk -ResourceGroupName $rgName -DiskName $diskName -Disk $diskConfig
      
       #fetching details of newly created disk

       Get-AzDisk -ResourceGroupName $rgName -Name $diskName


## Step 3: Configure the managed disk by Azure Powershell:-

       #Increase the size of Azure Managed disk to 64gb, run the below command
        New-AzDiskUpdateConfig -DiskSizeGB 64 | Update-AzDisk -ResourceGroupName $rgName -Diskname $diskName

       #Now verify the changes 
        Get-AzDisk -ResourceGroupName $rgName -Name $diskName
        
       #Verify the SKU as Standard_LRS
        Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku

       #Change the disk performance SKU to Premium_LRS
        New-AzDiskUpdateConfig -Sku Premium_LRS | Update-AzDisk -ResourceGroupName $rgName -DiskName $diskName
        
       #Now Verify the changes again 
        Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku



