---
title: Maszyna wirtualna (klasyczna) z wieloma kartami sieciowymi - Azure CLI 1.0 aaaCreate | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate maszyna wirtualna (klasyczna) z wieloma kartami sieciowymi przy użyciu hello Azure interfejsu wiersza polecenia (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="af9b6-103">Tworzenie maszyny Wirtualnej (klasyczne) z wieloma kartami sieciowymi przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="af9b6-103">Create a VM (Classic) with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="af9b6-104">Można tworzyć maszyn wirtualnych (VM) na platformie Azure i dołączyć wiele sieci tooeach interfejsów (NIC) z maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="af9b6-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="af9b6-105">Wiele kart sieciowych włączać rozdzielenie typów ruchu sieciowego między kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="af9b6-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="af9b6-106">Na przykład jedna karta sieciowa może komunikować się z hello Internet, podczas gdy inny komunikuje się tylko z wewnętrznych zasobów nie podłączone toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="af9b6-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="af9b6-107">Program Hello możliwości tooseparate ruch sieciowy między wieloma kartami jest wymagany dla wielu urządzeń wirtualnych sieci, takich jak dostarczania aplikacji i rozwiązań Optymalizacja sieci WAN.</span><span class="sxs-lookup"><span data-stu-id="af9b6-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af9b6-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="af9b6-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="af9b6-109">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="af9b6-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="af9b6-110">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="af9b6-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="af9b6-111">Dowiedz się, jak tooperform te czynności przy użyciu hello [modelu wdrażania usługi Resource Manager](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="af9b6-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="af9b6-112">Witaj następujące kroki Użyj grupy zasobów o nazwie *IaaSStory* hello serwerów sieci WEB oraz grupę zasobów o nazwie *IaaSStory zaplecza* dla serwerów hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="af9b6-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af9b6-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="af9b6-113">Prerequisites</span></span>
<span data-ttu-id="af9b6-114">Przed utworzeniem hello serwerów bazy danych, należy toocreate hello *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby hello w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="af9b6-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="af9b6-115">toocreate tych zasobów, pełny hello kroki, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="af9b6-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="af9b6-116">Tworzenie sieci wirtualnej, wykonując następujące kroki hello hello [utworzyć sieć wirtualną](virtual-networks-create-vnet-classic-cli.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="af9b6-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a><span data-ttu-id="af9b6-117">Wdrażanie zaplecza hello maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="af9b6-117">Deploy hello back-end VMs</span></span>
<span data-ttu-id="af9b6-118">Hello zaplecza maszyny wirtualne są zależne od utworzenia hello hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="af9b6-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="af9b6-119">**Konto magazynu dla dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="af9b6-119">**Storage account for data disks**.</span></span> <span data-ttu-id="af9b6-120">W celu poprawy wydajności hello dysków z danymi na serwerach bazy danych hello użyje półprzewodnikowych (SSD) dysku technologii, która wymaga konta magazynu w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="af9b6-120">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="af9b6-121">Upewnij się, że hello wdrożyć magazyn w warstwie premium toosupport lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="af9b6-121">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="af9b6-122">**Karty sieciowe**.</span><span class="sxs-lookup"><span data-stu-id="af9b6-122">**NICs**.</span></span> <span data-ttu-id="af9b6-123">Każda maszyna wirtualna będzie mieć dwie karty sieciowe, jeden dla dostępu do bazy danych, a drugi do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="af9b6-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="af9b6-124">**Zestaw dostępności**.</span><span class="sxs-lookup"><span data-stu-id="af9b6-124">**Availability set**.</span></span> <span data-ttu-id="af9b6-125">Wszystkie serwery baz danych zostanie dodany zestaw dostępności pojedynczego tooa, tooensure co najmniej jeden z maszyn wirtualnych hello jest uruchomiona podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="af9b6-125">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="af9b6-126">Krok 1 — Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="af9b6-126">Step 1 - Start your script</span></span>
<span data-ttu-id="af9b6-127">Możesz pobrać hello pełna bash skryptu używanego [tutaj](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="af9b6-127">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="af9b6-128">Wykonaj następujące kroki toochange hello skryptu toowork w danym środowisku hello:</span><span class="sxs-lookup"><span data-stu-id="af9b6-128">Complete hello following steps toochange hello script toowork in your environment:</span></span>

1. <span data-ttu-id="af9b6-129">Zmień hello wartości zmiennych hello poniżej oparte na istniejącej grupie zasobów wdrożone powyżej w [wymagania wstępne](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="af9b6-129">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="af9b6-130">Zmień hello wartości zmiennych hello poniżej na podstawie wartości hello ma toouse wdrożenia wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="af9b6-130">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="af9b6-131">Krok 2 — Tworzenie niezbędne zasoby dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="af9b6-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="af9b6-132">Utwórz nową usługę chmury dla wszystkich maszyn wirtualnych wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="af9b6-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="af9b6-133">Użycie hello powiadomienia hello `$backendCSName` zmiennej dla hello Nazwa grupy zasobów, i `$location` dla hello region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="af9b6-133">Notice hello use of hello `$backendCSName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="af9b6-134">Utwórz konto magazynu w warstwie premium dla hello systemu operacyjnego i toobe dysków danych używany przez Twoje maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="af9b6-134">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="af9b6-135">Krok 3 — Tworzenie maszyn wirtualnych z wieloma kartami sieciowymi</span><span class="sxs-lookup"><span data-stu-id="af9b6-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="af9b6-136">Uruchom toocreate pętli wielu maszyn wirtualnych, oparte na powitania `numberOfVMs` zmiennych.</span><span class="sxs-lookup"><span data-stu-id="af9b6-136">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="af9b6-137">Dla każdej maszyny Wirtualnej Określ nazwę hello i adres IP każdego Witaj dwie karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="af9b6-137">For each VM, specify hello name and IP address of each of hello two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="af9b6-138">Utwórz hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af9b6-138">Create hello VM.</span></span> <span data-ttu-id="af9b6-139">Zwróć uwagę, użycie hello hello `--nic-config` parametr zawierający listę wszystkich kart sieciowych podsieci, adresów IP i nazwy.</span><span class="sxs-lookup"><span data-stu-id="af9b6-139">Notice hello usage of hello `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. <span data-ttu-id="af9b6-140">Dla każdej maszyny Wirtualnej należy utworzyć dwa dyski danych.</span><span class="sxs-lookup"><span data-stu-id="af9b6-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="af9b6-141">Krok 4 — uruchamianie skryptu hello</span><span class="sxs-lookup"><span data-stu-id="af9b6-141">Step 4 - Run hello script</span></span>
<span data-ttu-id="af9b6-142">Pobrane i zmienić hello skryptu na podstawie Twoich potrzeb, ponownie uruchom hello skryptu toocreate hello końcowy maszyn wirtualnych bazy danych z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="af9b6-142">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="af9b6-143">Zapisz skrypt i uruchom go z Twojego **Bash** terminala.</span><span class="sxs-lookup"><span data-stu-id="af9b6-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="af9b6-144">Zobaczysz hello początkowej danych wyjściowych, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="af9b6-144">You will see hello initial output, as shown below.</span></span>

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. <span data-ttu-id="af9b6-145">Po kilku minutach zakończy się wykonanie hello i zostanie wyświetlony rest hello hello danych wyjściowych, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="af9b6-145">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
