---
title: "Maszyna wirtualna (klasyczna) z wieloma kartami sieciowymi — programu Azure PowerShell aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate maszyna wirtualna (klasyczna) z wieloma kartami sieciowymi przy użyciu programu PowerShell."
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
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="2c36b-103">Tworzenie maszyny Wirtualnej (klasyczne) z wieloma kartami sieciowymi przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c36b-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="2c36b-104">Można tworzyć maszyn wirtualnych (VM) na platformie Azure i dołączyć wiele sieci tooeach interfejsów (NIC) z maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2c36b-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="2c36b-105">Wiele kart sieciowych włączać rozdzielenie typów ruchu sieciowego między kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="2c36b-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="2c36b-106">Na przykład jedna karta sieciowa może komunikować się z hello Internet, podczas gdy inny komunikuje się tylko z wewnętrznych zasobów nie podłączone toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="2c36b-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="2c36b-107">Program Hello możliwości tooseparate ruch sieciowy między wieloma kartami jest wymagany dla wielu urządzeń wirtualnych sieci, takich jak dostarczania aplikacji i rozwiązań Optymalizacja sieci WAN.</span><span class="sxs-lookup"><span data-stu-id="2c36b-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c36b-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2c36b-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2c36b-109">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="2c36b-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="2c36b-110">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c36b-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="2c36b-111">Dowiedz się, jak tooperform te czynności przy użyciu hello [modelu wdrażania usługi Resource Manager](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2c36b-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="2c36b-112">Witaj następujące kroki Użyj grupy zasobów o nazwie *IaaSStory* hello serwerów sieci WEB oraz grupę zasobów o nazwie *IaaSStory zaplecza* dla serwerów hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2c36b-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c36b-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2c36b-113">Prerequisites</span></span>

<span data-ttu-id="2c36b-114">Przed utworzeniem hello serwerów bazy danych, należy toocreate hello *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby hello w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="2c36b-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="2c36b-115">toocreate tych zasobów, pełny hello kroki, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="2c36b-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="2c36b-116">Tworzenie sieci wirtualnej, wykonując następujące kroki hello hello [utworzyć sieć wirtualną](virtual-networks-create-vnet-classic-netcfg-ps.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2c36b-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="2c36b-117">Tworzenie hello zaplecza maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="2c36b-117">Create hello back-end VMs</span></span>
<span data-ttu-id="2c36b-118">Hello zaplecza maszyny wirtualne są zależne od utworzenia hello hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="2c36b-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="2c36b-119">**Podsieci wewnętrznej bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="2c36b-119">**Backend subnet**.</span></span> <span data-ttu-id="2c36b-120">serwery bazy danych Hello będą częścią osobnej podsieci ruchu toosegregate.</span><span class="sxs-lookup"><span data-stu-id="2c36b-120">hello database servers will be part of a separate subnet, toosegregate traffic.</span></span> <span data-ttu-id="2c36b-121">Poniższy skrypt Hello oczekuje tooexist tej podsieci w sieci wirtualnej o nazwie *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="2c36b-121">hello script below expects this subnet tooexist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="2c36b-122">**Konto magazynu dla dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="2c36b-122">**Storage account for data disks**.</span></span> <span data-ttu-id="2c36b-123">W celu poprawy wydajności hello dysków z danymi na serwerach bazy danych hello użyje półprzewodnikowych (SSD) dysku technologii, która wymaga konta magazynu w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="2c36b-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="2c36b-124">Upewnij się, że hello wdrożyć magazyn w warstwie premium toosupport lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c36b-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="2c36b-125">**Zestaw dostępności**.</span><span class="sxs-lookup"><span data-stu-id="2c36b-125">**Availability set**.</span></span> <span data-ttu-id="2c36b-126">Wszystkie serwery baz danych zostanie dodany zestaw dostępności pojedynczego tooa, tooensure co najmniej jeden z maszyn wirtualnych hello jest uruchomiona podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="2c36b-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="2c36b-127">Krok 1 — Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="2c36b-127">Step 1 - Start your script</span></span>
<span data-ttu-id="2c36b-128">Możesz pobrać hello używane pełne skrypt programu PowerShell [tutaj](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="2c36b-128">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="2c36b-129">Wykonaj kroki hello poniżej toochange hello skryptu toowork w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="2c36b-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="2c36b-130">Zmień hello wartości zmiennych hello poniżej oparte na istniejącej grupie zasobów wdrożone powyżej w [wymagania wstępne](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="2c36b-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="2c36b-131">Zmień hello wartości zmiennych hello poniżej na podstawie wartości hello ma toouse wdrożenia wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2c36b-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="2c36b-132">Krok 2 — Tworzenie niezbędne zasoby dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="2c36b-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="2c36b-133">Należy toocreate konta dla dysków z danymi hello nową usługę w chmurze i magazynu dla wszystkich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2c36b-133">You need toocreate a new cloud service and a storage account for hello data disks for all VMs.</span></span> <span data-ttu-id="2c36b-134">Należy również toospecify obrazu, a konto administratora lokalnego na powitania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2c36b-134">You also need toospecify an image, and a local administrator account for hello VMs.</span></span> <span data-ttu-id="2c36b-135">ukończenie tych zasobów, toocreate hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2c36b-135">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="2c36b-136">Utwórz nową usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2c36b-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="2c36b-137">Utwórz nowe konto magazynu premium.</span><span class="sxs-lookup"><span data-stu-id="2c36b-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="2c36b-138">Ustaw konto magazynu hello utworzone powyżej jako hello bieżącego konta magazynu dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2c36b-138">Set hello storage account created above as hello current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="2c36b-139">Wybierz obraz powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c36b-139">Select an image for hello VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="2c36b-140">Ustaw poświadczenia konta administratora lokalnego hello.</span><span class="sxs-lookup"><span data-stu-id="2c36b-140">Set hello local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="2c36b-141">Krok 3 — Tworzenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="2c36b-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="2c36b-142">Należy toouse toocreate pętli, jak wiele maszyn wirtualnych, a tworzenie hello niezbędne karty sieciowe i maszyn wirtualnych w pętli hello.</span><span class="sxs-lookup"><span data-stu-id="2c36b-142">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="2c36b-143">toocreate hello kart sieciowych i maszyn wirtualnych, należy wykonać hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="2c36b-143">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="2c36b-144">Uruchom `for` hello toorepeat pętli polecenia toocreate Maszynę wirtualną i dwie karty sieciowe, jak tyle razy, na podstawie hello wartości hello `$numberOfVMs` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="2c36b-144">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="2c36b-145">Utwórz `VMConfig` obiektu określenie hello obrazu, rozmiar i zbiór dostępności dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c36b-145">Create a `VMConfig` object specifying hello image, size, and availability set for hello VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="2c36b-146">Zainicjuj obsługę hello maszyny Wirtualnej jako Maszynę wirtualną systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="2c36b-146">Provision hello VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="2c36b-147">Ustaw domyślny hello karty Sieciowej i przypisz mu statyczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="2c36b-147">Set hello default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="2c36b-148">Dodawanie drugiej karty Sieciowej dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c36b-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="2c36b-149">Tworzenie dysków toodata dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c36b-149">Create toodata disks for each VM.</span></span>

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

7. <span data-ttu-id="2c36b-150">Utwórz każdej maszyny Wirtualnej, a koniec hello pętli.</span><span class="sxs-lookup"><span data-stu-id="2c36b-150">Create each VM, and end hello loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="2c36b-151">Krok 4 — uruchamianie skryptu hello</span><span class="sxs-lookup"><span data-stu-id="2c36b-151">Step 4 - Run hello script</span></span>
<span data-ttu-id="2c36b-152">Pobrane i zmienić hello skryptu na podstawie Twoich potrzeb, runt on skryptu bazy toocreate hello wewnętrznej bazy danych maszyn wirtualnych z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="2c36b-152">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="2c36b-153">Zapisz skrypt i uruchom go z hello **PowerShell** wiersza polecenia lub **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="2c36b-153">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="2c36b-154">Zobaczysz hello początkowej danych wyjściowych, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="2c36b-154">You will see hello initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="2c36b-155">Wypełnij informacje hello potrzebne hello poświadczeń monit i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2c36b-155">Fill out hello information needed in hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="2c36b-156">zwracany jest Hello danych wyjściowych poniżej.</span><span class="sxs-lookup"><span data-stu-id="2c36b-156">hello output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
