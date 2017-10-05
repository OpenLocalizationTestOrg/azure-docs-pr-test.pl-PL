---
title: "Tworzenie sieci wirtualnej platformy Azure (klasyczną) z wieloma podsieciami | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć sieć wirtualną (klasyczne) z wieloma podsieciami na platformie Azure."
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
ms.openlocfilehash: 95c2f4fe40590a8d809f634fb5b2c92d07421bb0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="80df3-103">Tworzenie sieci wirtualnej (wdrożenia klasyczne) z wieloma podsieciami</span><span class="sxs-lookup"><span data-stu-id="80df3-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80df3-104">Platforma Azure ma dwa [różne modele wdrażania](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) do tworzenia i pracy z zasobami: Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="80df3-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="80df3-105">Ten artykuł dotyczy klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="80df3-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="80df3-106">Firma Microsoft zaleca utworzenie większości nowych sieci wirtualnych za pomocą [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="80df3-106">Microsoft recommends creating most new virtual networks through the [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="80df3-107">W tym samouczku jak utworzyć podstawowy sieć wirtualna platformy Azure (klasyczną) ma oddzielne podsieci publiczne i prywatne.</span><span class="sxs-lookup"><span data-stu-id="80df3-107">In this tutorial, learn how to create a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="80df3-108">Można utworzyć zasobów platformy Azure, takich jak maszyny wirtualne i usługi w chmurze w podsieci.</span><span class="sxs-lookup"><span data-stu-id="80df3-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="80df3-109">Zasoby utworzone w sieciach wirtualnych (klasyczne) może komunikować się ze sobą oraz z zasobami w innych sieciach, połączony z siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="80df3-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected to a virtual network.</span></span>

<span data-ttu-id="80df3-110">Dowiedz się więcej na temat wszystkich [sieci wirtualnej](virtual-network-manage-network.md) i [podsieci](virtual-network-manage-subnet.md) ustawienia.</span><span class="sxs-lookup"><span data-stu-id="80df3-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="80df3-111">Sieci wirtualne (klasyczne) są natychmiast usuwane przez Azure podczas [subskrypcja została wyłączona](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="80df3-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="80df3-112">Sieci wirtualne (klasyczne) są usuwane niezależnie od tego, czy istnieje zasobów w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="80df3-112">Virtual networks (classic) are deleted regardless of whether resources exist in the virtual network.</span></span> <span data-ttu-id="80df3-113">Jeśli później ponownie włączysz subskrypcji, muszą zostać ponownie utworzone zasoby, które były dostępne w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="80df3-113">If you later re-enable the subscription, resources that existed in the virtual network must be recreated.</span></span>

<span data-ttu-id="80df3-114">Można utworzyć sieci wirtualnej (wdrożenia klasyczne) przy użyciu [portalu Azure](#portal), [Azure interfejsu wiersza polecenia (CLI) 1.0](#azure-cli), lub [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="80df3-114">You can create a virtual network (classic) by using the [Azure portal](#portal), the [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="80df3-115">Portal</span><span class="sxs-lookup"><span data-stu-id="80df3-115">Portal</span></span>

1. <span data-ttu-id="80df3-116">W przeglądarce sieci Web, przejdź do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80df3-116">In an Internet browser, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="80df3-117">Zaloguj się za pomocą programu [konta Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="80df3-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="80df3-118">Jeśli nie masz konta platformy Azure, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="80df3-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="80df3-119">Kliknij przycisk **+ nowy** w portalu.</span><span class="sxs-lookup"><span data-stu-id="80df3-119">Click **+New** in the portal.</span></span>
3. <span data-ttu-id="80df3-120">Wprowadź *sieci wirtualnej* w **wyszukiwania portalu Marketplace** pole w górnej części **nowy** wyświetlonym bloku.</span><span class="sxs-lookup"><span data-stu-id="80df3-120">Enter *Virtual network* in the **Search the Marketplace** box at the top of the **New** blade that appears.</span></span>  <span data-ttu-id="80df3-121">Kliknij przycisk **sieci wirtualnej** po wyświetleniu w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="80df3-121">Click **Virtual network** when it appears in the search results.</span></span>
4. <span data-ttu-id="80df3-122">Wybierz **klasycznego** w **wybierz model wdrożenia** polu **sieci wirtualnej** bloku, zostanie wyświetlone, następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="80df3-122">Select **Classic** in the **Select a deployment model** box in the **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="80df3-123">Wprowadź następujące wartości **Utwórz sieć wirtualną (klasyczne)** bloku, a następnie kliknij przycisk **Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="80df3-123">Enter the following values on the **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="80df3-124">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="80df3-124">Setting</span></span>|<span data-ttu-id="80df3-125">Wartość</span><span class="sxs-lookup"><span data-stu-id="80df3-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="80df3-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="80df3-126">Name</span></span>|<span data-ttu-id="80df3-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="80df3-127">myVnet</span></span>|
    |<span data-ttu-id="80df3-128">Przestrzeń adresowa</span><span class="sxs-lookup"><span data-stu-id="80df3-128">Address space</span></span>|<span data-ttu-id="80df3-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="80df3-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="80df3-130">Nazwa podsieci</span><span class="sxs-lookup"><span data-stu-id="80df3-130">Subnet name</span></span>|<span data-ttu-id="80df3-131">Publiczne</span><span class="sxs-lookup"><span data-stu-id="80df3-131">Public</span></span>|
    |<span data-ttu-id="80df3-132">Zakres adresów podsieci</span><span class="sxs-lookup"><span data-stu-id="80df3-132">Subnet address range</span></span>|<span data-ttu-id="80df3-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="80df3-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="80df3-134">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="80df3-134">Resource group</span></span>|<span data-ttu-id="80df3-135">Pozostaw **Utwórz nowy** zaznaczone, a następnie wprowadź **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="80df3-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="80df3-136">Subskrypcji i lokalizacji</span><span class="sxs-lookup"><span data-stu-id="80df3-136">Subscription and location</span></span>|<span data-ttu-id="80df3-137">Wybierz subskrypcji i lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="80df3-137">Select your subscription and location.</span></span>

    <span data-ttu-id="80df3-138">Jeśli jesteś nowym użytkownikiem usługi Azure, Dowiedz się więcej o [grup zasobów](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subskrypcje](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), i [lokalizacje](https://azure.microsoft.com/regions) (zwaną także *regionów*).</span><span class="sxs-lookup"><span data-stu-id="80df3-138">If you're new to Azure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred to as *regions*).</span></span>
4. <span data-ttu-id="80df3-139">W portalu można utworzyć tylko jedną podsieć, podczas tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="80df3-139">In the portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="80df3-140">W tym samouczku utworzysz drugiej podsieci po utworzeniu sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="80df3-140">In this tutorial, you create a second subnet after you create the virtual network.</span></span> <span data-ttu-id="80df3-141">Później można utworzyć Internet dostępnych zasobów w **publicznego** podsieci.</span><span class="sxs-lookup"><span data-stu-id="80df3-141">You might later create Internet-accessible resources in the **Public** subnet.</span></span> <span data-ttu-id="80df3-142">Można także utworzyć zasoby, które nie są dostępne z Internetu w **prywatnej** podsieci.</span><span class="sxs-lookup"><span data-stu-id="80df3-142">You also might create resources that aren't accessible from the Internet in the **Private** subnet.</span></span> <span data-ttu-id="80df3-143">Aby utworzyć drugą podsieć, wprowadź **myVnet** w **wyszukiwania zasobów** u góry strony.</span><span class="sxs-lookup"><span data-stu-id="80df3-143">To create the second subnet, enter **myVnet** in the **Search resources** box at the top of the page.</span></span> <span data-ttu-id="80df3-144">Kliknij przycisk **myVnet** po wyświetleniu w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="80df3-144">Click **myVnet** when it appears in the search results.</span></span>
5. <span data-ttu-id="80df3-145">Kliknij przycisk **podsieci** (w **ustawienia** sekcji) na **Utwórz sieć wirtualną (klasyczne)** wyświetlonym bloku.</span><span class="sxs-lookup"><span data-stu-id="80df3-145">Click **Subnets** (in the **SETTINGS** section) on the **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="80df3-146">Kliknij przycisk **+ Dodaj** na **myVnet - podsieci** wyświetlonym bloku.</span><span class="sxs-lookup"><span data-stu-id="80df3-146">Click **+Add** on the **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="80df3-147">Wprowadź **prywatnej** dla **nazwa** na **Dodaj podsieć** bloku.</span><span class="sxs-lookup"><span data-stu-id="80df3-147">Enter **Private** for **Name** on the **Add subnet** blade.</span></span> <span data-ttu-id="80df3-148">Wprowadź **10.0.1.0/24** dla **zakres adresów**.</span><span class="sxs-lookup"><span data-stu-id="80df3-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="80df3-149">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="80df3-149">Click **OK**.</span></span>
8. <span data-ttu-id="80df3-150">Na **myVnet - podsieci** bloku, zostanie wyświetlony **publicznego** i **prywatnej** podsieci, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="80df3-150">On the **myVnet - Subnets** blade, you can see the **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="80df3-151">**Opcjonalne**: po zakończeniu tego samouczka warto usunąć zasoby, które zostały utworzone, tak aby nie wiąże się z opłatami użycia:</span><span class="sxs-lookup"><span data-stu-id="80df3-151">**Optional**: When you finish this tutorial, you might want to delete the resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="80df3-152">Kliknij przycisk **omówienie** na **myVnet** bloku.</span><span class="sxs-lookup"><span data-stu-id="80df3-152">Click **Overview** on the **myVnet** blade.</span></span>
    - <span data-ttu-id="80df3-153">Kliknij przycisk **usunąć** ikonę na **myVnet** bloku.</span><span class="sxs-lookup"><span data-stu-id="80df3-153">Click the **Delete** icon on the **myVnet** blade.</span></span>
    - <span data-ttu-id="80df3-154">Aby potwierdzić usunięcie, kliknij przycisk **tak** w **sieci wirtualnej Delete** pole.</span><span class="sxs-lookup"><span data-stu-id="80df3-154">To confirm the deletion, click **Yes** in the **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="80df3-155">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="80df3-155">Azure CLI</span></span>

1. <span data-ttu-id="80df3-156">Możesz albo [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), lub użyj interfejsu wiersza polecenia powłoki chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="80df3-156">You can either [install and configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use the CLI within the Azure Cloud Shell.</span></span> <span data-ttu-id="80df3-157">Usługa Azure Cloud Shell jest bezpłatną powłoką Bash, którą można uruchamiać bezpośrednio w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="80df3-157">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="80df3-158">Ma ona wstępnie zainstalowany interfejs wiersza polecenia platformy Azure skonfigurowany do użycia z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="80df3-158">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="80df3-159">Aby uzyskać pomoc dotyczącą poleceń interfejsu wiersza polecenia, wpisz `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="80df3-159">To get help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="80df3-160">W sesji interfejsu wiersza polecenia należy zalogować się przy użyciu polecenia znajdujący się na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="80df3-160">In a CLI session, log in to Azure with the command that follows.</span></span> <span data-ttu-id="80df3-161">Jeśli klikniesz przycisk **wypróbuj** w polu poniżej, otwiera powłokę chmury.</span><span class="sxs-lookup"><span data-stu-id="80df3-161">If you click **Try it** in the box below, a Cloud Shell opens.</span></span> <span data-ttu-id="80df3-162">Możesz zalogować się do subskrypcji platformy Azure, bez konieczności wprowadzania następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="80df3-162">You can log in to your Azure subscription, without entering the following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="80df3-163">Aby upewnić się, że interfejsu wiersza polecenia jest w trybie zarządzania usługami, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="80df3-163">To ensure the CLI is in Service Management mode, enter the following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="80df3-164">Utwórz sieć wirtualną z prywatnej podsieci:</span><span class="sxs-lookup"><span data-stu-id="80df3-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="80df3-165">Utwórz publiczny podsieci w sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="80df3-165">Create a public subnet within the virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="80df3-166">Przegląd sieci wirtualnej i podsieci:</span><span class="sxs-lookup"><span data-stu-id="80df3-166">Review the virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="80df3-167">**Opcjonalne**: można usunąć zasoby, które zostały utworzone po zakończeniu tego samouczka, dzięki czemu nie wiąże się z opłatami użycia:</span><span class="sxs-lookup"><span data-stu-id="80df3-167">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="80df3-168">Chociaż nie można określić grupę zasobów, aby utworzyć sieć wirtualną (klasyczne) za pomocą interfejsu wiersza polecenia, platforma Azure tworzy sieć wirtualną w grupie zasobów o nazwie *sieci domyślne*.</span><span class="sxs-lookup"><span data-stu-id="80df3-168">Though you can't specify a resource group to create a virtual network (classic) in using the CLI, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="80df3-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="80df3-169">PowerShell</span></span>

1. <span data-ttu-id="80df3-170">Zainstaluj najnowszą wersję programu PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) modułu.</span><span class="sxs-lookup"><span data-stu-id="80df3-170">Install the latest version of the PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="80df3-171">Jeśli jesteś nowym użytkownikiem programu Azure PowerShell, zobacz temat [Azure PowerShell overview (Omówienie programu Azure PowerShell)](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80df3-171">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="80df3-172">Uruchom sesję programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80df3-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="80df3-173">W programie PowerShell zaloguj się do platformy Azure, wprowadzając polecenie `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="80df3-173">In PowerShell, log in to Azure by entering the `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="80df3-174">Zmień ścieżkę i nazwę pliku, zgodnie z potrzebami, następujące, a następnie wyeksportować do istniejącego pliku konfiguracji sieci:</span><span class="sxs-lookup"><span data-stu-id="80df3-174">Change the following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="80df3-175">Aby utworzyć sieć wirtualną przy użyciu publiczne i prywatne podsieci, użyj dowolnego edytora tekstów, aby dodać **VirtualNetworkSite** element znajdujący się w pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="80df3-175">To create a virtual network with public and private subnets, use any text editor to add the **VirtualNetworkSite** element that follows to the network configuration file.</span></span>

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

    <span data-ttu-id="80df3-176">Przejrzyj pełnego [schemat pliku konfiguracji sieci](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="80df3-176">Review the full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="80df3-177">Importowanie pliku konfiguracji sieci:</span><span class="sxs-lookup"><span data-stu-id="80df3-177">Import the network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="80df3-178">Importowanie pliku konfiguracji sieci zmienione może spowodować zmiany w istniejących sieci wirtualnych (klasyczne) w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="80df3-178">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="80df3-179">Upewnij się, tylko dodać poprzedniej sieci wirtualnej i nie zmienić lub usunąć istniejące sieci wirtualnych z subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="80df3-179">Ensure you only add the previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="80df3-180">Przegląd sieci wirtualnej i podsieci:</span><span class="sxs-lookup"><span data-stu-id="80df3-180">Review the virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="80df3-181">**Opcjonalne**: można usunąć zasoby, które zostały utworzone po zakończeniu tego samouczka, dzięki czemu nie wiąże się z opłatami użycia.</span><span class="sxs-lookup"><span data-stu-id="80df3-181">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="80df3-182">Można usunąć sieci wirtualnej, pełną kroki 4 – 6 ponownie, usunięcie tego czasu **VirtualNetworkSite** element dodanej w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="80df3-182">To delete the virtual network, complete steps 4-6 again, this time removing the **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="80df3-183">Chociaż nie można określić grupę zasobów, aby utworzyć sieć wirtualną (klasyczne) przy użyciu programu PowerShell, platforma Azure tworzy sieć wirtualną w grupie zasobów o nazwie *sieci domyślne*.</span><span class="sxs-lookup"><span data-stu-id="80df3-183">Though you can't specify a resource group to create a virtual network (classic) in using PowerShell, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="80df3-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80df3-184">Next steps</span></span>

- <span data-ttu-id="80df3-185">Aby dowiedzieć się więcej o wszystkich ustawieniach podsieci i sieci wirtualnej, zobacz [Zarządzanie sieciami wirtualnymi](virtual-network-manage-network.md) i [Zarządzanie podsieci sieci wirtualnej](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="80df3-185">To learn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="80df3-186">Istnieją różne opcje dotyczące używania sieci wirtualnych i podsieci w środowisku produkcyjnym, aby spełnić różne wymagania.</span><span class="sxs-lookup"><span data-stu-id="80df3-186">You have various options for using virtual networks and subnets in a production environment to meet different requirements.</span></span>
- <span data-ttu-id="80df3-187">Filtrowanie ruchu przychodzącego i wychodzącego podsieci, tworzenie i stosowanie [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md) do podsieci.</span><span class="sxs-lookup"><span data-stu-id="80df3-187">To filter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) to subnets.</span></span>
- <span data-ttu-id="80df3-188">Utwórz [systemu Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) maszyny wirtualnej, a następnie połącz się z istniejącą siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="80df3-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it to an existing virtual network.</span></span>
- <span data-ttu-id="80df3-189">Aby połączyć dwie sieci wirtualne w tej samej lokalizacji platformy Azure, Utwórz [sieci wirtualnej komunikacji równorzędnej](create-peering-different-deployment-models.md) między sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="80df3-189">To connect two virtual networks in the same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between the virtual networks.</span></span> <span data-ttu-id="80df3-190">Elementu równorzędnego sieci wirtualnej (Resource Manager) do sieci wirtualnej (wdrożenia klasyczne), ale nie można utworzyć komunikacji równorzędnej między dwoma sieciami wirtualnymi (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="80df3-190">You can peer a virtual network (Resource Manager) to a virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="80df3-191">Połączyć sieć wirtualną z siecią lokalną przy użyciu [bramy sieci VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) obwodu.</span><span class="sxs-lookup"><span data-stu-id="80df3-191">Connect the virtual network to an on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
