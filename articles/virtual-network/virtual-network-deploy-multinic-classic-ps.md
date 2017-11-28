---
title: "Tworzenie maszyny Wirtualnej (klasyczne) z wieloma kartami sieciowymi — programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć Maszynę wirtualną (klasyczne) z wieloma kartami sieciowymi przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 923d4817d96399fc423b0a89cbf88f8d397f1af0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="954b5-103">Tworzenie maszyny Wirtualnej (klasyczne) z wieloma kartami sieciowymi przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="954b5-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="954b5-104">Można tworzyć maszyn wirtualnych (VM) na platformie Azure i dołączyć wiele interfejsów sieciowych (NIC) do wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="954b5-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="954b5-105">Wiele kart sieciowych włączać rozdzielenie typów ruchu sieciowego między kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="954b5-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="954b5-106">Na przykład jednej karcie Sieciowej może komunikować się z Internetem, podczas gdy inny komunikuje się tylko z wewnętrznych zasobów nie jest połączony z Internetem.</span><span class="sxs-lookup"><span data-stu-id="954b5-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="954b5-107">Do rozdzielania ruchu sieciowego między wiele kart sieciowych jest wymaganych dla wielu urządzeń wirtualnych sieci, takich jak dostarczania aplikacji i rozwiązań Optymalizacja sieci WAN.</span><span class="sxs-lookup"><span data-stu-id="954b5-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="954b5-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="954b5-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="954b5-109">Ten artykuł dotyczy klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="954b5-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="954b5-110">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="954b5-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="954b5-111">Dowiedz się, jak wykonać te czynności przy użyciu [modelu wdrażania usługi Resource Manager](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="954b5-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="954b5-112">Poniższe kroki Użyj grupy zasobów o nazwie *IaaSStory* dla serwerów sieci WEB i grupy zasobów o nazwie *IaaSStory zaplecza* dla serwerów baz danych.</span><span class="sxs-lookup"><span data-stu-id="954b5-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="954b5-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="954b5-113">Prerequisites</span></span>

<span data-ttu-id="954b5-114">Przed utworzeniem serwerów bazy danych, należy utworzyć *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby dotyczące tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="954b5-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="954b5-115">Aby utworzyć tych zasobów, wykonaj kroki, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="954b5-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="954b5-116">Tworzenie sieci wirtualnej, wykonując kroki opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-classic-netcfg-ps.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="954b5-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="954b5-117">Tworzenie maszyn wirtualnych zaplecza</span><span class="sxs-lookup"><span data-stu-id="954b5-117">Create the back-end VMs</span></span>
<span data-ttu-id="954b5-118">Maszyny wirtualne zaplecza są zależne od utworzenie następujących zasobów:</span><span class="sxs-lookup"><span data-stu-id="954b5-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="954b5-119">**Podsieci wewnętrznej bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="954b5-119">**Backend subnet**.</span></span> <span data-ttu-id="954b5-120">Serwery bazy danych będą częścią osobnej podsieci, aby rozdzielenie ruchu.</span><span class="sxs-lookup"><span data-stu-id="954b5-120">The database servers will be part of a separate subnet, to segregate traffic.</span></span> <span data-ttu-id="954b5-121">W poniższym skrypcie oczekuje tej podsieci w sieci wirtualnej o nazwie występują *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="954b5-121">The script below expects this subnet to exist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="954b5-122">**Konto magazynu dla dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="954b5-122">**Storage account for data disks**.</span></span> <span data-ttu-id="954b5-123">W celu poprawy wydajności dysków danych na serwerach bazy danych będzie używać półprzewodnikowych (SSD) dysku technologii, która wymaga konta magazynu w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="954b5-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="954b5-124">Upewnij się, lokalizacja platformy Azure, można wdrożyć na obsługuje usługi premium storage.</span><span class="sxs-lookup"><span data-stu-id="954b5-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="954b5-125">**Zestaw dostępności**.</span><span class="sxs-lookup"><span data-stu-id="954b5-125">**Availability set**.</span></span> <span data-ttu-id="954b5-126">Wszystkie serwery baz danych zostanie dodany do jednej dostępności ustawić, aby upewnić się, że co najmniej jeden z maszynami wirtualnymi i systemem podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="954b5-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="954b5-127">Krok 1 — Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="954b5-127">Step 1 - Start your script</span></span>
<span data-ttu-id="954b5-128">Możesz pobrać pełną skrypt programu PowerShell używane [tutaj](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="954b5-128">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="954b5-129">Wykonaj poniższe kroki, aby zmienić skryptu do pracy w środowisku.</span><span class="sxs-lookup"><span data-stu-id="954b5-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="954b5-130">Zmienianie wartości zmiennych poniżej oparte na istniejącej grupie zasobów wdrożone powyżej w [wymagania wstępne](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="954b5-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="954b5-131">Zmienianie wartości zmiennych poniżej na podstawie wartości, który ma być używany dla danego wdrożenia wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="954b5-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="954b5-132">Krok 2 — Tworzenie niezbędne zasoby dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="954b5-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="954b5-133">Należy utworzyć nową usługę w chmurze i konto magazynu dla dysków z danymi dla wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="954b5-133">You need to create a new cloud service and a storage account for the data disks for all VMs.</span></span> <span data-ttu-id="954b5-134">Należy również określić obrazu, a konto administratora lokalnego dla maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="954b5-134">You also need to specify an image, and a local administrator account for the VMs.</span></span> <span data-ttu-id="954b5-135">Aby utworzyć tych zasobów, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="954b5-135">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="954b5-136">Utwórz nową usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="954b5-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="954b5-137">Utwórz nowe konto magazynu premium.</span><span class="sxs-lookup"><span data-stu-id="954b5-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="954b5-138">Ustaw konto magazynu utworzone powyżej bieżącego konta magazynu dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="954b5-138">Set the storage account created above as the current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="954b5-139">Wybieranie obrazu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="954b5-139">Select an image for the VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="954b5-140">Ustaw poświadczenia konta administratora lokalnego.</span><span class="sxs-lookup"><span data-stu-id="954b5-140">Set the local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="954b5-141">Krok 3 — Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="954b5-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="954b5-142">Należy użyć pętli można utworzyć dowolną liczbę maszyn wirtualnych, jak i utworzyć niezbędne karty sieciowe i maszyn wirtualnych w pętli.</span><span class="sxs-lookup"><span data-stu-id="954b5-142">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="954b5-143">Aby utworzyć karty sieciowe i maszyn wirtualnych, należy wykonać następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="954b5-143">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="954b5-144">Uruchom `for` pętli powtórzeń poleceń, aby utworzyć Maszynę wirtualną i dwie karty sieciowe jako tyle razy, ile to konieczne, na podstawie wartości z `$numberOfVMs` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="954b5-144">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="954b5-145">Utwórz `VMConfig` obiekt określający obrazu, rozmiar i zbiór dostępności dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="954b5-145">Create a `VMConfig` object specifying the image, size, and availability set for the VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="954b5-146">Maszyna wirtualna wyznaczenie jako maszyny Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="954b5-146">Provision the VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="954b5-147">Ustaw domyślny karty Sieciowej i przypisz mu statyczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="954b5-147">Set the default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="954b5-148">Dodawanie drugiej karty Sieciowej dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="954b5-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="954b5-149">Utwórz dyski danych dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="954b5-149">Create to data disks for each VM.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. <span data-ttu-id="954b5-150">Utwórz każdej maszyny Wirtualnej i zakończyć pętli.</span><span class="sxs-lookup"><span data-stu-id="954b5-150">Create each VM, and end the loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="954b5-151">Krok 4 — Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="954b5-151">Step 4 - Run the script</span></span>
<span data-ttu-id="954b5-152">Pobrane i zmienić skryptu na podstawie Twoich potrzeb, runt on skryptu w celu tworzenia wewnętrznej bazy danych maszyn wirtualnych z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="954b5-152">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="954b5-153">Zapisz skrypt i uruchom go z **PowerShell** wiersza polecenia lub **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="954b5-153">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="954b5-154">Zobaczysz początkowej danych wyjściowych, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="954b5-154">You will see the initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="954b5-155">Wprowadź informacje wymagane w wierszu poświadczenia i kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="954b5-155">Fill out the information needed in the credentials prompt and click **OK**.</span></span> <span data-ttu-id="954b5-156">Zwracany jest danych wyjściowych poniżej.</span><span class="sxs-lookup"><span data-stu-id="954b5-156">The output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
