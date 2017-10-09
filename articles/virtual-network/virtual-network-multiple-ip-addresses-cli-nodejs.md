---
title: "aaaVM z wielu adresów IP przy użyciu hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooassign wielu adresów IP tooa maszynę wirtualną przy użyciu hello Azure CLI 1.0 | Menedżer zasobów."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a><span data-ttu-id="d737f-103">Przypisz wielu adresów IP maszyn toovirtual przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="d737f-103">Assign multiple IP addresses toovirtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="d737f-104">W tym artykule opisano, jak toocreate maszynę wirtualną (VM) za pośrednictwem hello Azure Resource Manager deployment model przy użyciu hello Azure CLI w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="d737f-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 1.0.</span></span> <span data-ttu-id="d737f-105">Wiele adresów IP nie można przypisać tooresources został utworzony za pomocą hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d737f-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="d737f-106">więcej informacji na temat modeli wdrażania platformy Azure, przeczytaj hello toolearn [zrozumieć modele wdrażania](../resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d737f-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="d737f-107"><a name = "create"></a>Utwórz maszynę Wirtualną z wielu adresów IP</span><span class="sxs-lookup"><span data-stu-id="d737f-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="d737f-108">Można wykonać tego zadania przy użyciu hello Azure CLI 1.0 (w tym artykule) lub hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d737f-108">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="d737f-109">Hello przestrzeganie objaśniono sposób toocreate przykład maszynę Wirtualną za pomocą wielu IP adresów, zgodnie z opisem w scenariuszu hello.</span><span class="sxs-lookup"><span data-stu-id="d737f-109">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="d737f-110">Zmień nazwy zmiennych i typy adresów IP zgodnie z wymaganiami implementacji.</span><span class="sxs-lookup"><span data-stu-id="d737f-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="d737f-111">Instalowanie i konfigurowanie hello Azure CLI 1.0 przez hello następujące kroki w hello [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu i zaloguj się do konta platformy Azure z hello `azure-login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="d737f-111">Install and configure hello Azure CLI 1.0 by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with hello `azure-login` command.</span></span>

2. <span data-ttu-id="d737f-112">Utwórz grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="d737f-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="d737f-113">Utwórz sieć wirtualną:</span><span class="sxs-lookup"><span data-stu-id="d737f-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="d737f-114">Utwórz podsieć w sieci wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="d737f-114">Create a subnet in hello virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="d737f-115">Utwórz konto magazynu dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d737f-115">Create  a storage account for hello VM.</span></span> <span data-ttu-id="d737f-116">Przed uruchomieniem hello następujące polecenia, Zastąp *mojekontomagazynu* o unikatowej nazwie.</span><span class="sxs-lookup"><span data-stu-id="d737f-116">Before running hello following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="d737f-117">Nazwa Hello musi być unikatowa w obrębie platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="d737f-117">hello name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="d737f-118">Utwórz hello konfiguracje adresów IP, karty Sieciowej i przypisz hello IP konfiguracje toohello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="d737f-118">Create hello IP configurations, a NIC, and assign hello IP configurations toohello NIC.</span></span> <span data-ttu-id="d737f-119">Można dodać, usunąć lub zmienić konfigurację hello w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="d737f-119">You can add, remove, or change hello configurations as necessary.</span></span> <span data-ttu-id="d737f-120">w scenariuszu hello opisano Hello następujące konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="d737f-120">hello following configurations are described in hello scenario:</span></span>

    <span data-ttu-id="d737f-121">**Polecenie IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="d737f-121">**IPConfig-1**</span></span>

    <span data-ttu-id="d737f-122">Wprowadź hello poleceń, które należy wykonać toocreate:</span><span class="sxs-lookup"><span data-stu-id="d737f-122">Enter hello commands that follow toocreate:</span></span>

    - <span data-ttu-id="d737f-123">Publiczny zasobu adresu IP za pomocą statycznego publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="d737f-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="d737f-124">Karta sieciowa, przypisywanie hello publicznego adresu IP i statyczne tooit prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d737f-124">A NIC, assigning hello public IP address and a static private IP address tooit.</span></span>
    
    <span data-ttu-id="d737f-125">Zastąp *mypublicdns* o nazwie, która jest unikatowa w hello lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d737f-125">Replace *mypublicdns* with a name that is unique within hello Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="d737f-126">Publiczne adresy IP ma nominalnego opłatą.</span><span class="sxs-lookup"><span data-stu-id="d737f-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="d737f-127">więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony.</span><span class="sxs-lookup"><span data-stu-id="d737f-127">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="d737f-128">Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d737f-128">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="d737f-129">więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d737f-129">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="d737f-130">**Polecenie IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="d737f-130">**IPConfig-2**</span></span>

     <span data-ttu-id="d737f-131">Wprowadź następujące polecenia toocreate hello nowy zasób publiczny adres IP i nową konfigurację adresu IP z statycznego publicznego adresu IP i statycznego prywatnego adresu IP:</span><span class="sxs-lookup"><span data-stu-id="d737f-131">Enter hello following commands toocreate a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="d737f-132">**Polecenie IPConfig 3**</span><span class="sxs-lookup"><span data-stu-id="d737f-132">**IPConfig-3**</span></span>

    <span data-ttu-id="d737f-133">Wprowadź hello następujące polecenia toocreate konfigurację protokołu IP z statycznego prywatnego adresu IP i nie publiczny adres IP:</span><span class="sxs-lookup"><span data-stu-id="d737f-133">Enter hello following commands toocreate an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="d737f-134">Chociaż ten artykuł przypisuje wszystkie tooa konfiguracji IP jednej karty Sieciowej, można przypisać wielu tooany konfiguracji adresu IP karty Sieciowej na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d737f-134">Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations tooany NIC in a VM.</span></span> <span data-ttu-id="d737f-135">toolearn sposób odczytać Maszynę wirtualną z wieloma kartami sieciowymi, toocreate hello Utwórz maszynę Wirtualną z wielu kart sieciowych artykułu.</span><span class="sxs-lookup"><span data-stu-id="d737f-135">toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="d737f-136">Tworzenie maszyny wirtualnej z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="d737f-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="d737f-137">toochange hello v2 tooStandard DS2 rozmiar maszyny Wirtualnej, na przykład po prostu dodaj następujące właściwości hello `--vm-size Standard_DS3_v2` toohello `azure vm create` polecenia w kroku 6.</span><span class="sxs-lookup"><span data-stu-id="d737f-137">toochange hello VM size tooStandard DS2 v2, for example, simply add hello following property `--vm-size Standard_DS3_v2` toohello `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="d737f-138">Wprowadź hello następujące polecenia tooview hello karty Sieciowej i hello skojarzone konfiguracje adresów IP:</span><span class="sxs-lookup"><span data-stu-id="d737f-138">Enter hello following command tooview hello NIC and hello associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="d737f-139">Dodaj hello prywatnego adresu IP dotyczy systemu operacyjnego maszyny Wirtualnej toohello, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="d737f-139">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="d737f-140"><a name="add"></a>Dodaj tooa adresów IP maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d737f-140"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="d737f-141">Możesz dodać dodatkowe prywatnych i publicznych IP adresów tooan istniejących kart interfejsu Sieciowego, wykonując kroki hello, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="d737f-141">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="d737f-142">Przykłady Hello zależą od hello [scenariusza](#Scenario) opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="d737f-142">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="d737f-143">Otwórz okno wiersza polecenia platformy Azure i pełne hello pozostałe kroki opisane w tej sekcji w ramach jednej sesji interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d737f-143">Open Azure CLI and complete hello remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="d737f-144">Jeśli nie masz jeszcze interfejsu wiersza polecenia Azure zainstalowany i skonfigurowany, pełną hello etapami hello [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu i zaloguj się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d737f-144">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="d737f-145">Wykonaj kroki hello w jednym z następujących sekcji, w zależności od wymagań hello:</span><span class="sxs-lookup"><span data-stu-id="d737f-145">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    - <span data-ttu-id="d737f-146">**Dodaj prywatnego adresu IP**</span><span class="sxs-lookup"><span data-stu-id="d737f-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="d737f-147">tooadd prywatnej tooa adresu IP karty Sieciowej, należy utworzyć konfigurację protokołu IP przy użyciu poniższego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="d737f-147">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command below.</span></span> <span data-ttu-id="d737f-148">statyczny adres Hello musi zawierać adres nieużywane hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="d737f-148">hello static address must be an unused address for hello subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="d737f-149">Tworzenie konfiguracji tyle, ile potrzebujesz, przy użyciu nazwy konfiguracji unikatowy i prywatnych adresów IP (w przypadku konfiguracji statycznych adresów IP).</span><span class="sxs-lookup"><span data-stu-id="d737f-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="d737f-150">**Dodaj publiczny adres IP**</span><span class="sxs-lookup"><span data-stu-id="d737f-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="d737f-151">Publiczny adres IP zostanie dodany przez skojarzenie tooeither nową konfigurację adresu IP lub istniejącej konfiguracji adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d737f-151">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="d737f-152">Wykonaj kroki hello w jednym z hello kolejnych sekcjach, ile potrzebujesz.</span><span class="sxs-lookup"><span data-stu-id="d737f-152">Complete hello steps in one of hello sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="d737f-153">Publiczne adresy IP ma nominalnego opłatą.</span><span class="sxs-lookup"><span data-stu-id="d737f-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="d737f-154">więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony.</span><span class="sxs-lookup"><span data-stu-id="d737f-154">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="d737f-155">Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d737f-155">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="d737f-156">więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d737f-156">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="d737f-157">**Skojarz hello zasobów tooa nową konfigurację IP**</span><span class="sxs-lookup"><span data-stu-id="d737f-157">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="d737f-158">Po dodaniu publicznego adresu IP w nowej konfiguracji adresu IP, musisz również dodać prywatnego adresu IP, ponieważ wszystkie konfiguracje adresów IP muszą mieć prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d737f-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="d737f-159">Możesz dodać istniejący zasób publiczny adres IP lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="d737f-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="d737f-160">toocreate nową, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="d737f-160">toocreate a new one, enter hello following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="d737f-161">toocreate nowej konfiguracji IP przy użyciu statycznego prywatnego adresu IP i hello skojarzone *myPublicIP3* publicznego adresu IP adresów zasobów, wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="d737f-161">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="d737f-162">**Skojarz hello zasobów tooan istniejącej konfiguracji IP**</span><span class="sxs-lookup"><span data-stu-id="d737f-162">**Associate hello resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="d737f-163">Zasób publicznego adresu IP może być tylko skojarzone tooan konfiguracji adresów IP, który nie ma jeszcze skojarzone.</span><span class="sxs-lookup"><span data-stu-id="d737f-163">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="d737f-164">Można określić, czy konfiguracja IP ma skojarzone publicznego adresu IP, wprowadzając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="d737f-164">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="d737f-165">Wyszukaj toohello podobne wiersza, który wykonuje 3 IPConfig w hello zwrócone dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d737f-165">Look for a line similar toohello one that follows for IPConfig-3 in hello returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="d737f-166">Ponieważ hello **publicznego adresu IP** kolumny dla *IpConfig 3* jest puste, zasobu bez publicznego adresu IP jest obecnie skojarzone tooit.</span><span class="sxs-lookup"><span data-stu-id="d737f-166">Since hello **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="d737f-167">Można dodać istniejącego publicznego adresu IP adres zasobów tooIpConfig-3, lub wprowadź powitania po toocreate polecenia, co:</span><span class="sxs-lookup"><span data-stu-id="d737f-167">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="d737f-168">Wprowadź następujące polecenie publicznego adresu IP tooassociate hello adresów zasobów toohello istniejącej konfiguracji IP o nazwie hello *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="d737f-168">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="d737f-169">Wyświetlanie hello prywatnych adresów IP i hello publicznego adresu IP adres zasobów przypisanych toohello hello karty Sieciowej, wprowadzając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d737f-169">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="d737f-170">Hello zwrócił dane wyjściowe są podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d737f-170">hello returned output is similar toohello following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="d737f-171">Dodaj hello prywatnych adresów IP systemu operacyjnego maszyny Wirtualnej toohello kart toohello dodane przez instrukcjami hello w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="d737f-171">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="d737f-172">Nie należy dodawać hello publicznego adresu IP adresów toohello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d737f-172">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
