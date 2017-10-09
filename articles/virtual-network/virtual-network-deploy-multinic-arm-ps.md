---
title: "aaaCreate Maszynę wirtualną z wieloma kartami sieciowymi — programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate maszyny Wirtualnej z wielu kart sieciowych przy użyciu programu PowerShell."
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
ms.openlocfilehash: 507a413510da3ee69aefed324977ee40e442268b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="699ea-103">Utwórz maszynę Wirtualną z wieloma kartami sieciowymi przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="699ea-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="699ea-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="699ea-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="699ea-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="699ea-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="699ea-106">Szablon</span><span class="sxs-lookup"><span data-stu-id="699ea-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="699ea-107">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="699ea-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="699ea-108">Interfejs wiersza polecenia platformy Azure (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="699ea-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="699ea-109">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="699ea-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="699ea-110">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="699ea-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="699ea-111">Witaj następujące kroki Użyj grupy zasobów o nazwie *IaaSStory* hello serwerów sieci WEB oraz grupę zasobów o nazwie *IaaSStory zaplecza* dla serwerów hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="699ea-111">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="699ea-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="699ea-112">Prerequisites</span></span>
<span data-ttu-id="699ea-113">Przed utworzeniem hello serwerów bazy danych, należy toocreate hello *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby hello w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="699ea-113">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="699ea-114">ukończenie tych zasobów, toocreate hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="699ea-114">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="699ea-115">Przejdź za[strony szablonu hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="699ea-115">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="699ea-116">Na stronie szablon hello toohello po prawej **nadrzędnej grupy zasobów**, kliknij przycisk **wdrażanie tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="699ea-116">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="699ea-117">W razie potrzeby zmień wartości parametrów hello, a następnie wykonaj kroki hello w grupie zasobów hello toodeploy portalu Azure w wersji zapoznawczej hello.</span><span class="sxs-lookup"><span data-stu-id="699ea-117">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="699ea-118">Upewnij się, że nazwy konta magazynu są unikatowe.</span><span class="sxs-lookup"><span data-stu-id="699ea-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="699ea-119">Nie może mieć nazwy konta magazynu zduplikowanych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="699ea-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="699ea-120">Tworzenie hello zaplecza maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="699ea-120">Create hello back-end VMs</span></span>
<span data-ttu-id="699ea-121">Hello zaplecza maszyny wirtualne są zależne od utworzenia hello hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="699ea-121">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="699ea-122">**Konto magazynu dla dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="699ea-122">**Storage account for data disks**.</span></span> <span data-ttu-id="699ea-123">W celu poprawy wydajności hello dysków z danymi na serwerach bazy danych hello użyje półprzewodnikowych (SSD) dysku technologii, która wymaga konta magazynu w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="699ea-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="699ea-124">Upewnij się, że hello wdrożyć magazyn w warstwie premium toosupport lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="699ea-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="699ea-125">**Karty sieciowe**.</span><span class="sxs-lookup"><span data-stu-id="699ea-125">**NICs**.</span></span> <span data-ttu-id="699ea-126">Każda maszyna wirtualna będzie mieć dwie karty sieciowe, jeden dla dostępu do bazy danych, a drugi do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="699ea-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="699ea-127">**Zestaw dostępności**.</span><span class="sxs-lookup"><span data-stu-id="699ea-127">**Availability set**.</span></span> <span data-ttu-id="699ea-128">Wszystkie serwery baz danych zostanie dodany zestaw dostępności pojedynczego tooa, tooensure co najmniej jeden z maszyn wirtualnych hello jest uruchomiona podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="699ea-128">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="699ea-129">Krok 1 — Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="699ea-129">Step 1 - Start your script</span></span>
<span data-ttu-id="699ea-130">Możesz pobrać hello używane pełne skrypt programu PowerShell [tutaj](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="699ea-130">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="699ea-131">Wykonaj kroki hello poniżej toochange hello skryptu toowork w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="699ea-131">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="699ea-132">Zmień hello wartości zmiennych hello poniżej oparte na istniejącej grupie zasobów wdrożone powyżej w [wymagania wstępne](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="699ea-132">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="699ea-133">Zmień hello wartości zmiennych hello poniżej na podstawie wartości hello ma toouse wdrożenia wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="699ea-133">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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
3. <span data-ttu-id="699ea-134">Pobrać hello istniejące zasoby potrzebne do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="699ea-134">Retrieve hello existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="699ea-135">Krok 2 — Tworzenie niezbędne zasoby dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="699ea-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="699ea-136">Potrzebujesz toocreate nową grupę zasobów, konto magazynu dla dysków z danymi hello, oraz zbiór dostępności dla wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="699ea-136">You need toocreate a new resource group, a storage account for hello data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="699ea-137">Możesz też konieczne poświadczeń konta administratora lokalnego powitania dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="699ea-137">You alos need hello local administrator account credentials for each VM.</span></span> <span data-ttu-id="699ea-138">wykonanie tych zasobów, toocreate hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="699ea-138">toocreate these resources, execute hello following steps.</span></span>

1. <span data-ttu-id="699ea-139">Utwórz nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="699ea-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="699ea-140">Utwórz nowe konto magazynu premium w grupie zasobów hello utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="699ea-140">Create a new premium storage account in hello resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="699ea-141">Tworzenie nowego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="699ea-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="699ea-142">Pobierz administratora lokalnego hello toobe poświadczenia konta używane dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="699ea-142">Get hello local administrator account credentials toobe used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="699ea-143">Krok 3 — Tworzenie hello karty sieciowe i zaplecza maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="699ea-143">Step 3 - Create hello NICs and back-end VMs</span></span>
<span data-ttu-id="699ea-144">Należy toouse toocreate pętli, jak wiele maszyn wirtualnych, a tworzenie hello niezbędne karty sieciowe i maszyn wirtualnych w pętli hello.</span><span class="sxs-lookup"><span data-stu-id="699ea-144">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="699ea-145">toocreate hello kart sieciowych i maszyn wirtualnych, należy wykonać hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="699ea-145">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="699ea-146">Uruchom `for` hello toorepeat pętli polecenia toocreate Maszynę wirtualną i dwie karty sieciowe, jak tyle razy, na podstawie hello wartości hello `$numberOfVMs` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="699ea-146">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="699ea-147">Utwórz hello używanego przez kartę Sieciową dla dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="699ea-147">Create hello NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="699ea-148">Utwórz hello używanego przez kartę Sieciową dla dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="699ea-148">Create hello NIC used for remote access.</span></span> <span data-ttu-id="699ea-149">Zwróć uwagę, jak ta karta NIC ma tooit grupy NSG skojarzonej.</span><span class="sxs-lookup"><span data-stu-id="699ea-149">Notice how this NIC has an NSG associated tooit.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="699ea-150">Utwórz `vmConfig` obiektu.</span><span class="sxs-lookup"><span data-stu-id="699ea-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="699ea-151">Utwórz dwa dyski danych dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="699ea-151">Create two data disks per VM.</span></span> <span data-ttu-id="699ea-152">Zwróć uwagę, czy hello dysków z danymi w utworzone wcześniej konto magazynu w warstwie premium hello.</span><span class="sxs-lookup"><span data-stu-id="699ea-152">Notice that hello data disks are in hello premium storage account created earlier.</span></span>

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

6. <span data-ttu-id="699ea-153">Skonfiguruj hello systemu operacyjnego i obraz toobe używany dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="699ea-153">Configure hello operating system, and image toobe used for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="699ea-154">Dodaj Witaj dwie karty sieciowe utworzone powyżej toohello `vmConfig` obiektu.</span><span class="sxs-lookup"><span data-stu-id="699ea-154">Add hello two NICs created above toohello `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="699ea-155">Utwórz dysk systemu operacyjnego hello a hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="699ea-155">Create hello OS disk and create hello VM.</span></span> <span data-ttu-id="699ea-156">Powiadomienie hello `}` końcowy hello `for` pętli.</span><span class="sxs-lookup"><span data-stu-id="699ea-156">Notice hello `}` ending hello `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="699ea-157">Krok 4 — uruchamianie skryptu hello</span><span class="sxs-lookup"><span data-stu-id="699ea-157">Step 4 - Run hello script</span></span>
<span data-ttu-id="699ea-158">Pobrane i zmienić hello skryptu na podstawie Twoich potrzeb, runt on skryptu bazy toocreate hello wewnętrznej bazy danych maszyn wirtualnych z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="699ea-158">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="699ea-159">Zapisz skrypt i uruchom go z hello **PowerShell** wiersza polecenia lub **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="699ea-159">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="699ea-160">Witaj początkowej danych wyjściowych, zostanie wyświetlony w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="699ea-160">You will see hello initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="699ea-161">Po kilku minutach wypełniania hello wiersz poświadczenia i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="699ea-161">After a few minutes, fill out hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="699ea-162">Witaj danych wyjściowych poniżej reprezentuje jednej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="699ea-162">hello output below represents a single VM.</span></span> <span data-ttu-id="699ea-163">Cały proces hello powiadomienia trwało toocomplete 8 minut.</span><span class="sxs-lookup"><span data-stu-id="699ea-163">Notice hello entire process took 8 minutes toocomplete.</span></span>

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
