---
title: "Utwórz maszynę Wirtualną z wieloma kartami sieciowymi — 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć Maszynę wirtualną z wieloma kartami sieciowymi przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure."
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
ms.openlocfilehash: b95bcb38664718bf25ec6981c803415790c6da3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="a9328-103">Utwórz maszynę Wirtualną z wieloma kartami sieciowymi przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a9328-103">Create a VM with multiple NICs using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="a9328-104">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a9328-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a9328-105">Ten artykuł dotyczy używania modelu wdrażania usługi Resource Manager zalecanego przez firmę Microsoft w przypadku większości nowych wdrożeń zamiast [klasycznego modelu wdrażania](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a9328-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="a9328-106">Poniższe kroki Użyj grupy zasobów o nazwie *IaaSStory* dla serwerów sieci WEB i grupy zasobów o nazwie *IaaSStory zaplecza* dla serwerów baz danych.</span><span class="sxs-lookup"><span data-stu-id="a9328-106">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span> <span data-ttu-id="a9328-107">Można wykonać tego zadania przy użyciu programu Azure CLI 1.0 (w tym artykule) lub [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a9328-107">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="a9328-108">Wartości "" dla zmiennych w kolejnych krokach tworzenie zasobów przy użyciu ustawień z tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="a9328-108">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span></span> <span data-ttu-id="a9328-109">Zmień wartości, zgodnie z potrzebami, dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="a9328-109">Change the values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9328-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a9328-110">Prerequisites</span></span>
<span data-ttu-id="a9328-111">Przed utworzeniem serwerów bazy danych, należy utworzyć *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby dotyczące tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="a9328-111">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="a9328-112">Aby utworzyć tych zasobów, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a9328-112">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="a9328-113">Przejdź do [strony szablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="a9328-113">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="a9328-114">Na stronie szablonu z prawej strony **grupy zasobów nadrzędnej**, kliknij przycisk **wdrażanie na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="a9328-114">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="a9328-115">W razie potrzeby zmień wartości parametrów, a następnie wykonaj kroki w portalu Azure w wersji zapoznawczej, aby wdrożyć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="a9328-115">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9328-116">Upewnij się, że nazwy konta magazynu są unikatowe.</span><span class="sxs-lookup"><span data-stu-id="a9328-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="a9328-117">Nie może mieć nazwy konta magazynu zduplikowanych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a9328-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="a9328-118">Tworzenie maszyn wirtualnych zaplecza</span><span class="sxs-lookup"><span data-stu-id="a9328-118">Create the back-end VMs</span></span>
<span data-ttu-id="a9328-119">Maszyny wirtualne zaplecza są zależne od utworzenie następujących zasobów:</span><span class="sxs-lookup"><span data-stu-id="a9328-119">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="a9328-120">**Konto magazynu dla dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="a9328-120">**Storage account for data disks**.</span></span> <span data-ttu-id="a9328-121">W celu poprawy wydajności dysków danych na serwerach bazy danych będzie używać półprzewodnikowych (SSD) dysku technologii, która wymaga konta magazynu w warstwie premium.</span><span class="sxs-lookup"><span data-stu-id="a9328-121">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="a9328-122">Upewnij się, lokalizacja platformy Azure, można wdrożyć na obsługuje usługi premium storage.</span><span class="sxs-lookup"><span data-stu-id="a9328-122">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="a9328-123">**Karty sieciowe**.</span><span class="sxs-lookup"><span data-stu-id="a9328-123">**NICs**.</span></span> <span data-ttu-id="a9328-124">Każda maszyna wirtualna będzie mieć dwie karty sieciowe, jeden dla dostępu do bazy danych, a drugi do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="a9328-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="a9328-125">**Zestaw dostępności**.</span><span class="sxs-lookup"><span data-stu-id="a9328-125">**Availability set**.</span></span> <span data-ttu-id="a9328-126">Wszystkie serwery baz danych zostanie dodany do jednej dostępności ustawić, aby upewnić się, że co najmniej jeden z maszynami wirtualnymi i systemem podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="a9328-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="a9328-127">Krok 1 — Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="a9328-127">Step 1 - Start your script</span></span>
<span data-ttu-id="a9328-128">Możesz pobrać skrypt pełna bash używany [tutaj](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="a9328-128">You can download the full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="a9328-129">Wykonaj poniższe kroki, aby zmienić skryptu do pracy w środowisku.</span><span class="sxs-lookup"><span data-stu-id="a9328-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="a9328-130">Zmienianie wartości zmiennych poniżej oparte na istniejącej grupie zasobów wdrożone powyżej w [wymagania wstępne](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="a9328-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="a9328-131">Zmienianie wartości zmiennych poniżej na podstawie wartości, który ma być używany dla danego wdrożenia wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a9328-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

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

3. <span data-ttu-id="a9328-132">Pobierz identyfikator `BackEnd` podsieci, w której zostanie utworzona maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a9328-132">Retrieve the ID for the `BackEnd` subnet where the VMs will be created.</span></span> <span data-ttu-id="a9328-133">Należy to zrobić, ponieważ karty sieciowe do skojarzenia z tym podsieci znajdują się w innej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="a9328-133">You need to do this since the NICs to be associated to this subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="a9328-134">Pierwsze polecenie powyżej używa [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) i [ciągu manipulowania](http://tldp.org/LDP/abs/html/string-manipulation.html) (w szczególności podciąg usunięcie).</span><span class="sxs-lookup"><span data-stu-id="a9328-134">The first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="a9328-135">Pobierz identyfikator `NSG-RemoteAccess` NSG.</span><span class="sxs-lookup"><span data-stu-id="a9328-135">Retrieve the ID for the `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="a9328-136">Należy to zrobić, ponieważ karty sieciowe do skojarzenia z tym NSG znajdują się w innej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="a9328-136">You need to do this since the NICs to be associated to this NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="a9328-137">Krok 2 — Tworzenie niezbędne zasoby dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="a9328-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="a9328-138">Utwórz nową grupę zasobów dla wszystkich zasobów w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="a9328-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="a9328-139">Zwróć uwagę na `$backendRGName` zmiennej dla nazwy grupy zasobów i `$location` dla regionu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a9328-139">Notice the use of the `$backendRGName` variable for the resource group name, and `$location` for the Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="a9328-140">Utwórz konto magazynu premium dysków systemu operacyjnego i danych ma być używany przez Twoje maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a9328-140">Create a premium storage account for the OS and data disks to be used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="a9328-141">Utwórz zbiór dostępności dla maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a9328-141">Create an availability set for the VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-the-nics-and-back-end-vms"></a><span data-ttu-id="a9328-142">Krok 3 — Tworzenie kart sieciowych i zaplecza maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="a9328-142">Step 3 - Create the NICs and back-end VMs</span></span>

1. <span data-ttu-id="a9328-143">Uruchom pętli do utworzenia wielu maszyn wirtualnych, na podstawie `numberOfVMs` zmiennych.</span><span class="sxs-lookup"><span data-stu-id="a9328-143">Start a loop to create multiple VMs, based on the `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="a9328-144">Dla każdej maszyny Wirtualnej Utwórz kartę Sieciową dla dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a9328-144">For each VM, create a NIC for database access.</span></span>

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

3. <span data-ttu-id="a9328-145">Dla każdej maszyny Wirtualnej Utwórz kartę Sieciową dla dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="a9328-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="a9328-146">Powiadomienie `--network-security-group` parametru używanego do kojarzenia kartę Sieciową do grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="a9328-146">Notice the `--network-security-group` parameter, used to associate the NIC to an NSG.</span></span>

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

4. <span data-ttu-id="a9328-147">Tworzenie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9328-147">Create the VM.</span></span>

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

5. <span data-ttu-id="a9328-148">Dla każdej maszyny Wirtualnej, Utwórz dwa dyski danych, a za `done` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a9328-148">For each VM, create two data disks, and end the loop with the `done` command.</span></span>

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

### <a name="step-4---run-the-script"></a><span data-ttu-id="a9328-149">Krok 4 — Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="a9328-149">Step 4 - Run the script</span></span>
<span data-ttu-id="a9328-150">Pobrane i zmienić skryptu na podstawie Twoich potrzeb, należy uruchomić skrypt w celu utworzenia wewnętrznej bazy danych maszyn wirtualnych z wieloma kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="a9328-150">Now that you downloaded and changed the script based on your needs, run the script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="a9328-151">Zapisz skrypt i uruchom go z Twojego **Bash** terminala.</span><span class="sxs-lookup"><span data-stu-id="a9328-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="a9328-152">Zobaczysz początkowej danych wyjściowych, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="a9328-152">You will see the initial output, as shown below.</span></span>
   
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
        info:    Looking up the availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up the network interface "NICDB1-DA"
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
        info:    Looking up the network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up the network interface "NICDB1-RA"
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
        info:    Looking up the VM "DB1"
        info:    Using the VM Size "Standard_DS3"
        info:    The [OS, Data] Disk or image configuration requires storage account
        info:    Looking up the storage account wtestvnetstorageprm
        info:    Looking up the availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up the NIC "NICDB1-DA"
        info:    Looking up the NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="a9328-153">Po kilku minutach zakończy wykonywanie i będzie zobaczyć pozostałą część danych wyjściowych, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="a9328-153">After a few minutes, the execution will end and you will see the rest of the output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB1"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB1"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up the network interface "NICDB2-DA"
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
        info:    Looking up the network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up the network interface "NICDB2-RA"
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
        info:    Looking up the VM "DB2"
        info:    Using the VM Size "Standard_DS3"
        info:    The [OS, Data] Disk or image configuration requires storage account
        info:    Looking up the storage account wtestvnetstorageprm
        info:    Looking up the availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up the NIC "NICDB2-DA"
        info:    Looking up the NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB2"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB2"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

