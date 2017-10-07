---
title: "aaaCreate sieci wirtualnej platformy Azure (klasyczną) z wieloma podsieciami | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnej (wdrożenia klasyczne) z wieloma podsieciami na platformie Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="b8be3-103">Tworzenie sieci wirtualnej (wdrożenia klasyczne) z wieloma podsieciami</span><span class="sxs-lookup"><span data-stu-id="b8be3-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8be3-104">Platforma Azure ma dwa [różne modele wdrażania](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) do tworzenia i pracy z zasobami: Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="b8be3-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="b8be3-105">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="b8be3-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="b8be3-106">Firma Microsoft zaleca utworzenie większości nowych sieci wirtualnych za pomocą hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="b8be3-106">Microsoft recommends creating most new virtual networks through hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="b8be3-107">W tym samouczku Dowiedz się, jak toocreate Podstawowa sieć wirtualna platformy Azure (klasyczne) ma oddzielne podsieci publiczne i prywatne.</span><span class="sxs-lookup"><span data-stu-id="b8be3-107">In this tutorial, learn how toocreate a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="b8be3-108">Można utworzyć zasobów platformy Azure, takich jak maszyny wirtualne i usługi w chmurze w podsieci.</span><span class="sxs-lookup"><span data-stu-id="b8be3-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="b8be3-109">Zasoby utworzone w sieciach wirtualnych (klasyczne) może komunikować się ze sobą oraz z zasobami w sieci wirtualnej podłączonej tooa innych sieci.</span><span class="sxs-lookup"><span data-stu-id="b8be3-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="b8be3-110">Dowiedz się więcej na temat wszystkich [sieci wirtualnej](virtual-network-manage-network.md) i [podsieci](virtual-network-manage-subnet.md) ustawienia.</span><span class="sxs-lookup"><span data-stu-id="b8be3-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="b8be3-111">Sieci wirtualne (klasyczne) są natychmiast usuwane przez Azure podczas [subskrypcja została wyłączona](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="b8be3-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="b8be3-112">Sieci wirtualne (klasyczne) są usuwane niezależnie od tego, czy istnieje zasobów w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="b8be3-112">Virtual networks (classic) are deleted regardless of whether resources exist in hello virtual network.</span></span> <span data-ttu-id="b8be3-113">Jeśli później ponownie włączysz hello subskrypcji, zasobów, które były dostępne w sieci wirtualnej hello muszą zostać ponownie utworzone.</span><span class="sxs-lookup"><span data-stu-id="b8be3-113">If you later re-enable hello subscription, resources that existed in hello virtual network must be recreated.</span></span>

<span data-ttu-id="b8be3-114">Sieć wirtualna (klasyczna) można utworzyć za pomocą hello [portalu Azure](#portal), hello [Azure interfejsu wiersza polecenia (CLI) 1.0](#azure-cli), lub [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="b8be3-114">You can create a virtual network (classic) by using hello [Azure portal](#portal), hello [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="b8be3-115">Portal</span><span class="sxs-lookup"><span data-stu-id="b8be3-115">Portal</span></span>

1. <span data-ttu-id="b8be3-116">W przeglądarce sieci Web, przejdź do pozycji toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8be3-116">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b8be3-117">Zaloguj się za pomocą programu [konta Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="b8be3-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="b8be3-118">Jeśli nie masz konta platformy Azure, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="b8be3-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="b8be3-119">Kliknij przycisk **+ nowy** w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="b8be3-119">Click **+New** in hello portal.</span></span>
3. <span data-ttu-id="b8be3-120">Wprowadź *sieci wirtualnej* w hello **hello wyszukiwania portalu Marketplace** u góry hello hello **nowy** wyświetlonym bloku.</span><span class="sxs-lookup"><span data-stu-id="b8be3-120">Enter *Virtual network* in hello **Search hello Marketplace** box at hello top of hello **New** blade that appears.</span></span>  <span data-ttu-id="b8be3-121">Kliknij przycisk **sieci wirtualnej** po wyświetleniu w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="b8be3-121">Click **Virtual network** when it appears in hello search results.</span></span>
4. <span data-ttu-id="b8be3-122">Wybierz **klasycznego** w hello **wybierz model wdrożenia** polu w hello **sieci wirtualnej** bloku, zostanie wyświetlone, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b8be3-122">Select **Classic** in hello **Select a deployment model** box in hello **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="b8be3-123">Wprowadź następujące wartości na powitania hello **Utwórz sieć wirtualną (klasyczne)** bloku, a następnie kliknij przycisk **Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="b8be3-123">Enter hello following values on hello **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="b8be3-124">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="b8be3-124">Setting</span></span>|<span data-ttu-id="b8be3-125">Wartość</span><span class="sxs-lookup"><span data-stu-id="b8be3-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="b8be3-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b8be3-126">Name</span></span>|<span data-ttu-id="b8be3-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="b8be3-127">myVnet</span></span>|
    |<span data-ttu-id="b8be3-128">Przestrzeń adresowa</span><span class="sxs-lookup"><span data-stu-id="b8be3-128">Address space</span></span>|<span data-ttu-id="b8be3-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b8be3-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="b8be3-130">Nazwa podsieci</span><span class="sxs-lookup"><span data-stu-id="b8be3-130">Subnet name</span></span>|<span data-ttu-id="b8be3-131">Publiczne</span><span class="sxs-lookup"><span data-stu-id="b8be3-131">Public</span></span>|
    |<span data-ttu-id="b8be3-132">Zakres adresów podsieci</span><span class="sxs-lookup"><span data-stu-id="b8be3-132">Subnet address range</span></span>|<span data-ttu-id="b8be3-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="b8be3-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="b8be3-134">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="b8be3-134">Resource group</span></span>|<span data-ttu-id="b8be3-135">Pozostaw **Utwórz nowy** zaznaczone, a następnie wprowadź **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="b8be3-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="b8be3-136">Subskrypcji i lokalizacji</span><span class="sxs-lookup"><span data-stu-id="b8be3-136">Subscription and location</span></span>|<span data-ttu-id="b8be3-137">Wybierz subskrypcji i lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="b8be3-137">Select your subscription and location.</span></span>

    <span data-ttu-id="b8be3-138">Jeśli nowy tooAzure, Dowiedz się więcej o [grup zasobów](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subskrypcje](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), i [lokalizacje](https://azure.microsoft.com/regions) (nazywana także tooas *regionów*).</span><span class="sxs-lookup"><span data-stu-id="b8be3-138">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="b8be3-139">W portalu hello można utworzyć tylko jedną podsieć, podczas tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b8be3-139">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="b8be3-140">W tym samouczku utworzysz drugiej podsieci po utworzeniu sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="b8be3-140">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="b8be3-141">Później można utworzyć zasoby internetowe dostępny w hello **publicznego** podsieci.</span><span class="sxs-lookup"><span data-stu-id="b8be3-141">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="b8be3-142">Można także utworzyć zasoby, które nie są dostępne z hello Internet w hello **prywatnej** podsieci.</span><span class="sxs-lookup"><span data-stu-id="b8be3-142">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="b8be3-143">toocreate hello drugiej podsieci, wprowadź **myVnet** w hello **wyszukiwania zasobów** pole u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="b8be3-143">toocreate hello second subnet, enter **myVnet** in hello **Search resources** box at hello top of hello page.</span></span> <span data-ttu-id="b8be3-144">Kliknij przycisk **myVnet** po wyświetleniu w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="b8be3-144">Click **myVnet** when it appears in hello search results.</span></span>
5. <span data-ttu-id="b8be3-145">Kliknij przycisk **podsieci** (w hello **ustawienia** sekcji) na powitania **Utwórz sieć wirtualną (klasyczne)** wyświetlonym bloku.</span><span class="sxs-lookup"><span data-stu-id="b8be3-145">Click **Subnets** (in hello **SETTINGS** section) on hello **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="b8be3-146">Kliknij przycisk **+ Dodaj** na powitania **myVnet - podsieci** wyświetlonym bloku.</span><span class="sxs-lookup"><span data-stu-id="b8be3-146">Click **+Add** on hello **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="b8be3-147">Wprowadź **prywatnej** dla **nazwa** na powitania **Dodaj podsieć** bloku.</span><span class="sxs-lookup"><span data-stu-id="b8be3-147">Enter **Private** for **Name** on hello **Add subnet** blade.</span></span> <span data-ttu-id="b8be3-148">Wprowadź **10.0.1.0/24** dla **zakres adresów**.</span><span class="sxs-lookup"><span data-stu-id="b8be3-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="b8be3-149">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8be3-149">Click **OK**.</span></span>
8. <span data-ttu-id="b8be3-150">Na powitania **myVnet - podsieci** bloku widać hello **publicznego** i **prywatnej** podsieci, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="b8be3-150">On hello **myVnet - Subnets** blade, you can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="b8be3-151">**Opcjonalne**: po zakończeniu tego samouczka, może być toodelete hello zasoby, które zostały utworzone, tak aby nie wiąże się z opłatami użycia:</span><span class="sxs-lookup"><span data-stu-id="b8be3-151">**Optional**: When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="b8be3-152">Kliknij przycisk **omówienie** na powitania **myVnet** bloku.</span><span class="sxs-lookup"><span data-stu-id="b8be3-152">Click **Overview** on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="b8be3-153">Kliknij przycisk hello **usunąć** ikonę na powitania **myVnet** bloku.</span><span class="sxs-lookup"><span data-stu-id="b8be3-153">Click hello **Delete** icon on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="b8be3-154">Usuwanie hello tooconfirm, kliknij przycisk **tak** w hello **sieci wirtualnej Usuń** pole.</span><span class="sxs-lookup"><span data-stu-id="b8be3-154">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="b8be3-155">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b8be3-155">Azure CLI</span></span>

1. <span data-ttu-id="b8be3-156">Możesz albo [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), lub użyj hello interfejsu wiersza polecenia w hello powłoki chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="b8be3-156">You can either [install and configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use hello CLI within hello Azure Cloud Shell.</span></span> <span data-ttu-id="b8be3-157">Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b8be3-157">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="b8be3-158">Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="b8be3-158">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="b8be3-159">tooget pomocy dla poleceń interfejsu wiersza polecenia, wpisz `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="b8be3-159">tooget help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="b8be3-160">Zaloguj się za tooAzure przy użyciu polecenia hello znajdujący się w sesji interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b8be3-160">In a CLI session, log in tooAzure with hello command that follows.</span></span> <span data-ttu-id="b8be3-161">Jeśli klikniesz przycisk **wypróbuj** w poniższym polu hello, otwiera powłokę chmury.</span><span class="sxs-lookup"><span data-stu-id="b8be3-161">If you click **Try it** in hello box below, a Cloud Shell opens.</span></span> <span data-ttu-id="b8be3-162">Możesz zalogować się w tooyour subskrypcji platformy Azure, bez konieczności wprowadzania hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b8be3-162">You can log in tooyour Azure subscription, without entering hello following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="b8be3-163">powitalne tooensure interfejsu wiersza polecenia jest w trybie zarządzania usługami, wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b8be3-163">tooensure hello CLI is in Service Management mode, enter hello following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="b8be3-164">Utwórz sieć wirtualną z prywatnej podsieci:</span><span class="sxs-lookup"><span data-stu-id="b8be3-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="b8be3-165">Utwórz publiczny podsieci w sieci wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="b8be3-165">Create a public subnet within hello virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="b8be3-166">Przejrzyj hello sieci wirtualnej i podsieci:</span><span class="sxs-lookup"><span data-stu-id="b8be3-166">Review hello virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="b8be3-167">**Opcjonalne**: może być toodelete hello zasoby, które zostały utworzone po zakończeniu tego samouczka, dzięki czemu nie wiąże się z opłatami użycia:</span><span class="sxs-lookup"><span data-stu-id="b8be3-167">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="b8be3-168">Chociaż nie można określić toocreate grupy zasobów sieci wirtualnej (wdrożenia klasyczne) za pomocą interfejsu wiersza polecenia hello, platforma Azure tworzy hello sieci wirtualnej w grupie zasobów o nazwie *sieci domyślne*.</span><span class="sxs-lookup"><span data-stu-id="b8be3-168">Though you can't specify a resource group toocreate a virtual network (classic) in using hello CLI, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="b8be3-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8be3-169">PowerShell</span></span>

1. <span data-ttu-id="b8be3-170">Zainstaluj najnowszą wersję hello PowerShell hello [Azure](https://www.powershellgallery.com/packages/Azure) modułu.</span><span class="sxs-lookup"><span data-stu-id="b8be3-170">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="b8be3-171">Jeśli jesteś tooAzure nowego środowiska PowerShell, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b8be3-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="b8be3-172">Uruchom sesję programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8be3-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="b8be3-173">W programie PowerShell Zaloguj tooAzure wprowadzając hello `Add-AzureAccount` polecenia.</span><span class="sxs-lookup"><span data-stu-id="b8be3-173">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="b8be3-174">Zmień poniżej hello ścieżkę i nazwę pliku, zgodnie z potrzebami, a następnie wyeksportować do istniejącego pliku konfiguracji sieci:</span><span class="sxs-lookup"><span data-stu-id="b8be3-174">Change hello following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="b8be3-175">toocreate sieci wirtualnej z podsieciami publiczne i prywatne, użyj dowolnej hello tooadd Edytor tekstu **VirtualNetworkSite** elementem pliku konfiguracji sieci toohello.</span><span class="sxs-lookup"><span data-stu-id="b8be3-175">toocreate a virtual network with public and private subnets, use any text editor tooadd hello **VirtualNetworkSite** element that follows toohello network configuration file.</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    <span data-ttu-id="b8be3-176">Przejrzyj hello pełne [schemat pliku konfiguracji sieci](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8be3-176">Review hello full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="b8be3-177">Importowanie pliku konfiguracji sieci hello:</span><span class="sxs-lookup"><span data-stu-id="b8be3-177">Import hello network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="b8be3-178">Importowanie pliku konfiguracji sieci zmienione może spowodować zmiany tooexisting sieciami wirtualnymi (klasyczne) w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8be3-178">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="b8be3-179">Upewnij się, tylko dodać hello poprzedniej sieci wirtualnej i nie zmienić lub usunąć istniejące sieci wirtualnych z subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b8be3-179">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="b8be3-180">Przejrzyj hello sieci wirtualnej i podsieci:</span><span class="sxs-lookup"><span data-stu-id="b8be3-180">Review hello virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="b8be3-181">**Opcjonalne**: może być toodelete hello zasoby, które zostały utworzone po zakończeniu tego samouczka, dzięki czemu nie wiąże się z opłatami użycia.</span><span class="sxs-lookup"><span data-stu-id="b8be3-181">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="b8be3-182">toodelete hello sieci wirtualnej, pełną kroki 4 – 6 ponownie, ten czas hello usuwania **VirtualNetworkSite** element dodanej w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="b8be3-182">toodelete hello virtual network, complete steps 4-6 again, this time removing hello **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="b8be3-183">Chociaż nie można określić toocreate grupy zasobów sieci wirtualnej (wdrożenia klasyczne) przy użyciu programu PowerShell, platforma Azure tworzy hello sieci wirtualnej w grupie zasobów o nazwie *sieci domyślne*.</span><span class="sxs-lookup"><span data-stu-id="b8be3-183">Though you can't specify a resource group toocreate a virtual network (classic) in using PowerShell, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="b8be3-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8be3-184">Next steps</span></span>

- <span data-ttu-id="b8be3-185">Zobacz toolearn o wszystkich sieci wirtualnej i ustawienia podsieci [Zarządzanie sieciami wirtualnymi](virtual-network-manage-network.md) i [Zarządzanie podsieci sieci wirtualnej](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="b8be3-185">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="b8be3-186">Istnieją różne opcje dotyczące korzystania z sieci wirtualnych i podsieci w środowisku produkcyjnym wymagania różnych toomeet środowiska.</span><span class="sxs-lookup"><span data-stu-id="b8be3-186">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="b8be3-187">toofilter dla ruchu przychodzącego i wychodzącego ruchu w podsieci, tworzenie i stosowanie [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md) toosubnets.</span><span class="sxs-lookup"><span data-stu-id="b8be3-187">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="b8be3-188">Utwórz [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) maszyny wirtualnej, a następnie podłącz je tooan istniejącej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b8be3-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="b8be3-189">tooconnect dwie sieci wirtualne w tej samej lokalizacji platformy Azure Witaj, Utwórz [sieci wirtualnej komunikacji równorzędnej](create-peering-different-deployment-models.md) między sieciami wirtualnymi hello.</span><span class="sxs-lookup"><span data-stu-id="b8be3-189">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between hello virtual networks.</span></span> <span data-ttu-id="b8be3-190">Można elementu równorzędnego sieci wirtualnej tooa sieci wirtualnej (Resource Manager) (klasyczne), ale nie można utworzyć komunikacji równorzędnej między dwiema sieciami wirtualnymi (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="b8be3-190">You can peer a virtual network (Resource Manager) tooa virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="b8be3-191">Połączyć sieć lokalną tooan hello w sieci wirtualnej przy użyciu [bramy sieci VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) obwodu.</span><span class="sxs-lookup"><span data-stu-id="b8be3-191">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
