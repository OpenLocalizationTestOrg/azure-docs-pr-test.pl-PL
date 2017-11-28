---
title: "Utwórz maszynę Wirtualną z wieloma kartami sieciowymi — programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć Maszynę wirtualną z wieloma kartami sieciowymi przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3a11afd8fbd6a5e6b94cf1ebee7ea20665421bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="958f0-103">Utwórz maszynę Wirtualną z wieloma kartami sieciowymi przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="958f0-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="958f0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="958f0-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="958f0-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="958f0-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="958f0-106">Szablon</span><span class="sxs-lookup"><span data-stu-id="958f0-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="958f0-107">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="958f0-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="958f0-108">Interfejs wiersza polecenia platformy Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="958f0-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="958f0-109">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="958f0-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="958f0-110">Ten artykuł dotyczy używania modelu wdrażania usługi Resource Manager zalecanego przez firmę Microsoft w przypadku większości nowych wdrożeń zamiast [klasycznego modelu wdrażania](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="958f0-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="958f0-111">Poniższe kroki Użyj grupy zasobów o nazwie *IaaSStory* dla serwerów sieci WEB i grupy zasobów o nazwie *IaaSStory zaplecza* dla serwerów baz danych.</span><span class="sxs-lookup"><span data-stu-id="958f0-111">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="958f0-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="958f0-112">Prerequisites</span></span>
<span data-ttu-id="958f0-113">Przed utworzeniem serwerów bazy danych, należy utworzyć *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby dotyczące tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="958f0-113">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="958f0-114">Aby utworzyć tych zasobów, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="958f0-114">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="958f0-115">Przejdź do [strony szablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="958f0-115">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="958f0-116">Na stronie szablonu z prawej strony **grupy zasobów nadrzędnej**, kliknij przycisk **wdrażanie na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="958f0-116">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="958f0-117">W razie potrzeby zmień wartości parametrów, a następnie wykonaj kroki w portalu Azure w wersji zapoznawczej, aby wdrożyć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="958f0-117">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="958f0-118">Upewnij się, że nazwy konta magazynu są unikatowe.</span><span class="sxs-lookup"><span data-stu-id="958f0-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="958f0-119">Nie może mieć nazwy konta magazynu zduplikowanych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="958f0-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="958f0-120">Tworzenie maszyn wirtualnych zaplecza</span><span class="sxs-lookup"><span data-stu-id="958f0-120">Create the back-end VMs</span></span>
<span data-ttu-id="958f0-121">Maszyny wirtualne zaplecza są zależne od utworzenie następujących zasobów:</span><span class="sxs-lookup"><span data-stu-id="958f0-121">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="958f0-122">**Konto magazynu dla dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="958f0-122">**Storage account for data disks**.</span></span> <span data-ttu-id="958f0-123">W celu poprawy wydajności dysków danych na serwerach bazy danych będzie używać półprzewodnikowych (SSD) dysku technologii, która wymaga konta magazynu w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="958f0-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="958f0-124">Upewnij się, lokalizacja platformy Azure, można wdrożyć na obsługuje usługi premium storage.</span><span class="sxs-lookup"><span data-stu-id="958f0-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="958f0-125">**Karty sieciowe**.</span><span class="sxs-lookup"><span data-stu-id="958f0-125">**NICs**.</span></span> <span data-ttu-id="958f0-126">Każda maszyna wirtualna będzie mieć dwie karty sieciowe, jeden dla dostępu do bazy danych, a drugi do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="958f0-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="958f0-127">**Zestaw dostępności**.</span><span class="sxs-lookup"><span data-stu-id="958f0-127">**Availability set**.</span></span> <span data-ttu-id="958f0-128">Wszystkie serwery baz danych zostanie dodany do jednej dostępności ustawić, aby upewnić się, że co najmniej jeden z maszynami wirtualnymi i systemem podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="958f0-128">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="958f0-129">Krok 1 — Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="958f0-129">Step 1 - Start your script</span></span>
<span data-ttu-id="958f0-130">Możesz pobrać pełną skrypt programu PowerShell używane [tutaj](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="958f0-130">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="958f0-131">Wykonaj poniższe kroki, aby zmienić skryptu do pracy w środowisku.</span><span class="sxs-lookup"><span data-stu-id="958f0-131">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="958f0-132">Zmienianie wartości zmiennych poniżej oparte na istniejącej grupie zasobów wdrożone powyżej w [wymagania wstępne](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="958f0-132">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="958f0-133">Zmienianie wartości zmiennych poniżej na podstawie wartości, który ma być używany dla danego wdrożenia wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="958f0-133">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. <span data-ttu-id="958f0-134">Pobrać istniejących zasobów niezbędnych do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="958f0-134">Retrieve the existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="958f0-135">Krok 2 — Tworzenie niezbędne zasoby dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="958f0-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="958f0-136">Należy utworzyć nową grupę zasobów, konto magazynu dla dysków z danymi i zbiór dostępności dla wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="958f0-136">You need to create a new resource group, a storage account for the data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="958f0-137">Możesz też konieczne poświadczeń konta administratora lokalnego dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="958f0-137">You alos need the local administrator account credentials for each VM.</span></span> <span data-ttu-id="958f0-138">Aby utworzyć tych zasobów, należy wykonać następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="958f0-138">To create these resources, execute the following steps.</span></span>

1. <span data-ttu-id="958f0-139">Utwórz nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="958f0-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="958f0-140">Utwórz nowe konto magazynu premium w grupie zasobów utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="958f0-140">Create a new premium storage account in the resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="958f0-141">Tworzenie nowego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="958f0-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="958f0-142">Uzyskiwanie poświadczeń konta używanego do każdej maszyny Wirtualnej administratora lokalnego.</span><span class="sxs-lookup"><span data-stu-id="958f0-142">Get the local administrator account credentials to be used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type the name and password for the local administrator account."
    ```

### <a name="step-3---create-the-nics-and-back-end-vms"></a><span data-ttu-id="958f0-143">Krok 3 — Tworzenie kart sieciowych i zaplecza maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="958f0-143">Step 3 - Create the NICs and back-end VMs</span></span>
<span data-ttu-id="958f0-144">Należy użyć pętli można utworzyć dowolną liczbę maszyn wirtualnych, jak i utworzyć niezbędne karty sieciowe i maszyn wirtualnych w pętli.</span><span class="sxs-lookup"><span data-stu-id="958f0-144">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="958f0-145">Aby utworzyć karty sieciowe i maszyn wirtualnych, należy wykonać następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="958f0-145">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="958f0-146">Uruchom `for` pętli powtórzeń poleceń, aby utworzyć Maszynę wirtualną i dwie karty sieciowe jako tyle razy, ile to konieczne, na podstawie wartości z `$numberOfVMs` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="958f0-146">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="958f0-147">Utwórz kartę Sieciową, używane do dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="958f0-147">Create the NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="958f0-148">Tworzenie kart używane dla dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="958f0-148">Create the NIC used for remote access.</span></span> <span data-ttu-id="958f0-149">Zwróć uwagę, jak ta karta NIC ma grupy NSG skojarzonej do niego.</span><span class="sxs-lookup"><span data-stu-id="958f0-149">Notice how this NIC has an NSG associated to it.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="958f0-150">Utwórz `vmConfig` obiektu.</span><span class="sxs-lookup"><span data-stu-id="958f0-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="958f0-151">Utwórz dwa dyski danych dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="958f0-151">Create two data disks per VM.</span></span> <span data-ttu-id="958f0-152">Zwróć uwagę, czy dyski danych w ramach konta magazynu premium utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="958f0-152">Notice that the data disks are in the premium storage account created earlier.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. <span data-ttu-id="958f0-153">Konfigurowanie systemu operacyjnego i obrazu do użycia dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="958f0-153">Configure the operating system, and image to be used for the VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="958f0-154">Dwie karty sieciowe utworzone powyżej, aby dodać `vmConfig` obiektu.</span><span class="sxs-lookup"><span data-stu-id="958f0-154">Add the two NICs created above to the `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="958f0-155">Utwórz dysk systemu operacyjnego i tworzenie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="958f0-155">Create the OS disk and create the VM.</span></span> <span data-ttu-id="958f0-156">Powiadomienie `}` końcowy `for` pętli.</span><span class="sxs-lookup"><span data-stu-id="958f0-156">Notice the `}` ending the `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="958f0-157">Krok 4 — Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="958f0-157">Step 4 - Run the script</span></span>
<span data-ttu-id="958f0-158">Pobrane i zmienić skryptu na podstawie Twoich potrzeb, runt on skryptu w celu tworzenia wewnętrznej bazy danych maszyn wirtualnych z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="958f0-158">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="958f0-159">Zapisz skrypt i uruchom go z **PowerShell** wiersza polecenia lub **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="958f0-159">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="958f0-160">Początkowe dane wyjściowe, zostanie wyświetlony w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="958f0-160">You will see the initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="958f0-161">Po kilku minutach wypełnić wiersz poświadczenia i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="958f0-161">After a few minutes, fill out the credentials prompt and click **OK**.</span></span> <span data-ttu-id="958f0-162">Danych wyjściowych poniżej reprezentuje jednej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="958f0-162">The output below represents a single VM.</span></span> <span data-ttu-id="958f0-163">Powiadomienie cały proces trwało 8 minut.</span><span class="sxs-lookup"><span data-stu-id="958f0-163">Notice the entire process took 8 minutes to complete.</span></span>

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK
