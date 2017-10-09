---
title: "aaaCreate Maszynę wirtualną z wieloma kartami sieciowymi — 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate maszyny Wirtualnej z wielu kart sieciowych przy użyciu hello Azure CLI w wersji 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 07c660b632bcdc004365a6f910ecf8a5c13cbc6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="2ba43-103">Utwórz maszynę Wirtualną z wieloma kartami sieciowymi przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="2ba43-103">Create a VM with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="2ba43-104">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2ba43-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="2ba43-105">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2ba43-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="2ba43-106">Witaj następujące kroki Użyj grupy zasobów o nazwie *IaaSStory* hello serwerów sieci WEB oraz grupę zasobów o nazwie *IaaSStory zaplecza* dla serwerów hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2ba43-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span> <span data-ttu-id="2ba43-107">Można wykonać tego zadania przy użyciu hello Azure CLI 1.0 (w tym artykule) lub hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2ba43-107">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="2ba43-108">Witaj wartości "" hello zmiennych w hello czynności, które wykonują Utwórz zasoby przy użyciu ustawień z hello scenariusza.</span><span class="sxs-lookup"><span data-stu-id="2ba43-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="2ba43-109">Zmień wartości hello, zgodnie z potrzebami, dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="2ba43-109">Change hello values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ba43-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2ba43-110">Prerequisites</span></span>
<span data-ttu-id="2ba43-111">Przed utworzeniem hello serwerów bazy danych, należy toocreate hello *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby hello w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="2ba43-111">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="2ba43-112">ukończenie tych zasobów, toocreate hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2ba43-112">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="2ba43-113">Przejdź za[strony szablonu hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="2ba43-113">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="2ba43-114">Na stronie szablon hello toohello po prawej **nadrzędnej grupy zasobów**, kliknij przycisk **wdrażanie tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="2ba43-114">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="2ba43-115">W razie potrzeby zmień wartości parametrów hello, a następnie wykonaj kroki hello w grupie zasobów hello toodeploy portalu Azure w wersji zapoznawczej hello.</span><span class="sxs-lookup"><span data-stu-id="2ba43-115">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ba43-116">Upewnij się, że nazwy konta magazynu są unikatowe.</span><span class="sxs-lookup"><span data-stu-id="2ba43-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="2ba43-117">Nie może mieć nazwy konta magazynu zduplikowanych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba43-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="2ba43-118">Tworzenie hello zaplecza maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="2ba43-118">Create hello back-end VMs</span></span>
<span data-ttu-id="2ba43-119">Hello zaplecza maszyny wirtualne są zależne od utworzenia hello hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="2ba43-119">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="2ba43-120">**Konto magazynu dla dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="2ba43-120">**Storage account for data disks**.</span></span> <span data-ttu-id="2ba43-121">W celu poprawy wydajności hello dysków z danymi na serwerach bazy danych hello użyje półprzewodnikowych (SSD) dysku technologii, która wymaga konta magazynu w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="2ba43-121">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="2ba43-122">Upewnij się, że hello wdrożyć magazyn w warstwie premium toosupport lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba43-122">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="2ba43-123">**Karty sieciowe**.</span><span class="sxs-lookup"><span data-stu-id="2ba43-123">**NICs**.</span></span> <span data-ttu-id="2ba43-124">Każda maszyna wirtualna będzie mieć dwie karty sieciowe, jeden dla dostępu do bazy danych, a drugi do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="2ba43-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="2ba43-125">**Zestaw dostępności**.</span><span class="sxs-lookup"><span data-stu-id="2ba43-125">**Availability set**.</span></span> <span data-ttu-id="2ba43-126">Wszystkie serwery baz danych zostanie dodany zestaw dostępności pojedynczego tooa, tooensure co najmniej jeden z maszyn wirtualnych hello jest uruchomiona podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="2ba43-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="2ba43-127">Krok 1 — Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="2ba43-127">Step 1 - Start your script</span></span>
<span data-ttu-id="2ba43-128">Możesz pobrać hello pełna bash skryptu używanego [tutaj](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="2ba43-128">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="2ba43-129">Wykonaj kroki hello poniżej toochange hello skryptu toowork w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="2ba43-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="2ba43-130">Zmień hello wartości zmiennych hello poniżej oparte na istniejącej grupie zasobów wdrożone powyżej w [wymagania wstępne](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="2ba43-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="2ba43-131">Zmień hello wartości zmiennych hello poniżej na podstawie wartości hello ma toouse wdrożenia wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2ba43-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendRGName="IaaSStory-Backend"
    prmStorageAccountName="wtestvnetstorageprm"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    publisher="Canonical"
    offer="UbuntuServer"
    sku="14.04.2-LTS"
    version="latest"
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskName="datadisk"
    nicNamePrefix="NICDB"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

3. <span data-ttu-id="2ba43-132">Pobierz identyfikator hello hello `BackEnd` podsieci, w której zostanie utworzona hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2ba43-132">Retrieve hello ID for hello `BackEnd` subnet where hello VMs will be created.</span></span> <span data-ttu-id="2ba43-133">Toodo to konieczne, ponieważ hello kart sieciowych skojarzonych toobe toothis podsieci znajdują się w innej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="2ba43-133">You need toodo this since hello NICs toobe associated toothis subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="2ba43-134">Witaj pierwsze polecenie powyżej używa [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) i [ciągu manipulowania](http://tldp.org/LDP/abs/html/string-manipulation.html) (w szczególności podciąg usunięcie).</span><span class="sxs-lookup"><span data-stu-id="2ba43-134">hello first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="2ba43-135">Pobierz identyfikator hello hello `NSG-RemoteAccess` NSG.</span><span class="sxs-lookup"><span data-stu-id="2ba43-135">Retrieve hello ID for hello `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="2ba43-136">Toodo to konieczne, ponieważ hello toobe kart sieciowych skojarzonych toothis NSG znajdują się w innej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="2ba43-136">You need toodo this since hello NICs toobe associated toothis NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="2ba43-137">Krok 2 — Tworzenie niezbędne zasoby dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="2ba43-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="2ba43-138">Utwórz nową grupę zasobów dla wszystkich zasobów w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2ba43-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="2ba43-139">Użycie hello powiadomienia hello `$backendRGName` zmiennej dla hello Nazwa grupy zasobów, i `$location` dla hello region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba43-139">Notice hello use of hello `$backendRGName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="2ba43-140">Utwórz konto magazynu w warstwie premium dla hello systemu operacyjnego i toobe dysków danych używany przez Twoje maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2ba43-140">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="2ba43-141">Utwórz zbiór dostępności dla hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2ba43-141">Create an availability set for hello VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="2ba43-142">Krok 3 — Tworzenie hello karty sieciowe i zaplecza maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="2ba43-142">Step 3 - Create hello NICs and back-end VMs</span></span>

1. <span data-ttu-id="2ba43-143">Uruchom toocreate pętli wielu maszyn wirtualnych, oparte na powitania `numberOfVMs` zmiennych.</span><span class="sxs-lookup"><span data-stu-id="2ba43-143">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="2ba43-144">Dla każdej maszyny Wirtualnej Utwórz kartę Sieciową dla dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2ba43-144">For each VM, create a NIC for database access.</span></span>

    ```azurecli
    nic1Name=$nicNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x
    azure network nic create --name $nic1Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress1 \
        --subnet-id $subnetId
    ```

3. <span data-ttu-id="2ba43-145">Dla każdej maszyny Wirtualnej Utwórz kartę Sieciową dla dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="2ba43-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="2ba43-146">Powiadomienie hello `--network-security-group` parametru tooassociate używane hello kart tooan NSG.</span><span class="sxs-lookup"><span data-stu-id="2ba43-146">Notice hello `--network-security-group` parameter, used tooassociate hello NIC tooan NSG.</span></span>

    ```azurecli
    nic2Name=$nicNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    azure network nic create --name $nic2Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress2 \
        --subnet-id $subnetId $vnetName \
        --network-security-group-id $nsgId
    ```

4. <span data-ttu-id="2ba43-147">Utwórz hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2ba43-147">Create hello VM.</span></span>

    ```azurecli
    azure vm create --resource-group $backendRGName \
        --name $vmNamePrefix$suffixNumber \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --availset-name $avSetName \
        --nic-names $nic1Name,$nic2Name \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName$suffixNumber.vhd \
        --admin-username $username \
        --admin-password $password
    ```

5. <span data-ttu-id="2ba43-148">Dla każdej maszyny Wirtualnej, należy utworzyć z hello dwóch dysków i koniec hello pętli `done` polecenia.</span><span class="sxs-lookup"><span data-stu-id="2ba43-148">For each VM, create two data disks, and end hello loop with hello `done` command.</span></span>

    ```azurecli
    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-1.vhd \
        --size-in-gb $diskSize \
        --lun 0

    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \        
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-2.vhd \
        --size-in-gb $diskSize \
        --lun 1
        done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="2ba43-149">Krok 4 — uruchamianie skryptu hello</span><span class="sxs-lookup"><span data-stu-id="2ba43-149">Step 4 - Run hello script</span></span>
<span data-ttu-id="2ba43-150">Pobrane i zmienić hello skryptu na podstawie Twoich potrzeb, ponownie uruchom hello skryptu toocreate hello końcowy maszyn wirtualnych bazy danych z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="2ba43-150">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="2ba43-151">Zapisz skrypt i uruchom go z Twojego **Bash** terminala.</span><span class="sxs-lookup"><span data-stu-id="2ba43-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="2ba43-152">Zobaczysz hello początkowej danych wyjściowych, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="2ba43-152">You will see hello initial output, as shown below.</span></span>
   
        info:    Executing command group create
        info:    Getting resource group IaaSStory-Backend
        info:    Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command availset create
        info:    Looking up hello availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up hello network interface "NICDB1-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-DA
        data:    Name                            : NICDB1-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up hello network interface "NICDB1-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-RA
        data:    Name                            : NICDB1-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.54
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB1"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB1-DA"
        info:    Looking up hello NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="2ba43-153">Po kilku minutach zakończy się wykonanie hello i zostanie wyświetlony rest hello hello danych wyjściowych, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="2ba43-153">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up hello network interface "NICDB2-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-DA
        data:    Name                            : NICDB2-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.5
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up hello network interface "NICDB2-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-RA
        data:    Name                            : NICDB2-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.55
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB2"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB2-DA"
        info:    Looking up hello NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

