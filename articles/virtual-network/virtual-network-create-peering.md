---
title: "Tworzenie sieci wirtualnej platformy Azure komunikację równorzędną - Resource Manager — tej samej subskrypcji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć sieć wirtualną komunikacji równorzędnej między sieciami wirtualnymi utworzone za pomocą Menedżera zasobów, które istnieją w tej samej subskrypcji platformy Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: a32a6b33e04c603325ab3612f61e5852682eac7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="1d909-103">Tworzenie sieci wirtualnej równorzędna - Resource Manager tej samej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1d909-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="1d909-104">Z tego samouczka dowiesz się, można utworzyć sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi utworzone za pomocą Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="1d909-104">In this tutorial, you learn to create a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="1d909-105">Istnieją obie sieci wirtualne w tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1d909-105">Both virtual networks exist in the same subscription.</span></span> <span data-ttu-id="1d909-106">Komunikacja równorzędna dwa zasoby umożliwia sieci wirtualnych w różnych sieciach wirtualnych do komunikowania się ze sobą przy tym samym przepustowości i opóźnień, tak jakby były zasoby w tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1d909-106">Peering two virtual networks enables resources in different virtual networks to communicate with each other with the same bandwidth and latency as though the resources were in the same virtual network.</span></span> <span data-ttu-id="1d909-107">Dowiedz się więcej o [równorzędna sieci wirtualnej](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d909-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="1d909-108">Kroki tworzenia sieci wirtualnej komunikacji równorzędnej są różne, w zależności od tego, czy sieci wirtualne są w tym samym lub różnych subskrypcji i które [modelu wdrożenia usługi Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sieci wirtualne są tworzone za pomocą.</span><span class="sxs-lookup"><span data-stu-id="1d909-108">The steps to create a virtual network peering are different, depending on whether the virtual networks are in the same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the virtual networks are created through.</span></span> <span data-ttu-id="1d909-109">Dowiedz się, jak utworzyć sieć wirtualną równorzędna w innych sytuacjach, klikając w scenariuszu z następującej tabeli:</span><span class="sxs-lookup"><span data-stu-id="1d909-109">Learn how to create a virtual network peering in other scenarios by clicking the scenario from the following table:</span></span>

|<span data-ttu-id="1d909-110">Model wdrażania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1d909-110">Azure deployment model</span></span>  | <span data-ttu-id="1d909-111">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1d909-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="1d909-112">Obie usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d909-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="1d909-113">Różne</span><span class="sxs-lookup"><span data-stu-id="1d909-113">Different</span></span>|
|[<span data-ttu-id="1d909-114">Jeden Resource Manager, co classic</span><span class="sxs-lookup"><span data-stu-id="1d909-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="1d909-115">tym samym</span><span class="sxs-lookup"><span data-stu-id="1d909-115">Same</span></span>|
|[<span data-ttu-id="1d909-116">Jeden Resource Manager, co classic</span><span class="sxs-lookup"><span data-stu-id="1d909-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="1d909-117">Różne</span><span class="sxs-lookup"><span data-stu-id="1d909-117">Different</span></span>|

<span data-ttu-id="1d909-118">Nie można utworzyć sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnej wdrożone za pośrednictwem klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="1d909-118">A virtual network peering cannot be created between two virtual networks deployed through the classic deployment model.</span></span> <span data-ttu-id="1d909-119">Tylko można utworzyć sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnymi, znajdujące się w tym samym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="1d909-119">A virtual network peering can only be created between two virtual networks that exist in the same Azure region.</span></span> <span data-ttu-id="1d909-120">Jeśli musisz połączyć sieci wirtualnych obu utworzonych przy użyciu klasycznego modelu wdrażania lub istnieje w różnych regionach platformy Azure, możesz użyć Azure [bramy sieci VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) do łączenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1d909-120">If you need to connect virtual networks that were both created through the classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) to connect the virtual networks.</span></span> 

<span data-ttu-id="1d909-121">Można użyć [portalu Azure](#portal), Azure [interfejsu wiersza polecenia](#cli) (CLI) Azure [PowerShell](#powershell), lub [szablonu usługi Azure Resource Manager](#template)można utworzyć sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="1d909-121">You can use the [Azure portal](#portal), the Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) to create a virtual network peering.</span></span> <span data-ttu-id="1d909-122">Kliknij dowolny z poprzedniej łączy narzędzia, aby przejść bezpośrednio do kroki tworzenia sieci wirtualnej komunikacji równorzędnej narzędzie wyboru.</span><span class="sxs-lookup"><span data-stu-id="1d909-122">Click any of the previous tool links to go directly to the steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="1d909-123"><a name="portal"></a>Utwórz równorzędna - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1d909-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="1d909-124">Zaloguj się do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1d909-124">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1d909-125">Konto logowania przy użyciu musi mieć uprawnienia do tworzenia sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="1d909-125">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="1d909-126">Zobacz [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="1d909-126">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="1d909-127">Kliknij przycisk **+ nowy**, kliknij przycisk **sieci**, następnie kliknij przycisk **sieci wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="1d909-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="1d909-128">W **Utwórz sieć wirtualną** bloku, wprowadź, lub wybierz wartości poniższych ustawień, a następnie kliknij przycisk **Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="1d909-128">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="1d909-129">**Nazwa**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="1d909-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="1d909-130">**Przestrzeń adresowa**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="1d909-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="1d909-131">**Nazwa podsieci**: *domyślne*</span><span class="sxs-lookup"><span data-stu-id="1d909-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="1d909-132">**Zakres adresów podsieci**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="1d909-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="1d909-133">**Subskrypcja**: Wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="1d909-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="1d909-134">**Grupa zasobów**: Wybierz **Utwórz nowy** , a następnie wprowadź *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="1d909-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="1d909-135">**Lokalizacja**: *wschodnie stany USA*</span><span class="sxs-lookup"><span data-stu-id="1d909-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="1d909-136">Wykonaj kroki 2 – 3 ponownie określanie następujące wartości w kroku 3:</span><span class="sxs-lookup"><span data-stu-id="1d909-136">Complete steps 2-3 again specifying the following values in step 3:</span></span>
    - <span data-ttu-id="1d909-137">**Nazwa**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="1d909-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="1d909-138">**Przestrzeń adresowa**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="1d909-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="1d909-139">**Nazwa podsieci**: *domyślne*</span><span class="sxs-lookup"><span data-stu-id="1d909-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="1d909-140">**Zakres adresów podsieci**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="1d909-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="1d909-141">**Subskrypcja**: Wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="1d909-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="1d909-142">**Grupa zasobów**: Wybierz **Użyj istniejącego** i wybierz *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="1d909-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="1d909-143">**Lokalizacja**: *wschodnie stany USA*</span><span class="sxs-lookup"><span data-stu-id="1d909-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="1d909-144">W **wyszukiwania zasobów** pole w górnej części portalu typu *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="1d909-144">In the **Search resources** box at the top of the portal, type *myResourceGroup*.</span></span> <span data-ttu-id="1d909-145">Kliknij przycisk **myResourceGroup** po wyświetleniu w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1d909-145">Click **myResourceGroup** when it appears in the search results.</span></span> <span data-ttu-id="1d909-146">Zostanie wyświetlony blok **myresourcegroup** grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="1d909-146">A blade appears for the **myresourcegroup** resource group.</span></span> <span data-ttu-id="1d909-147">Grupa zasobów zawiera dwie sieci wirtualne utworzone w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="1d909-147">The resource group contains the two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="1d909-148">Kliknij przycisk **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="1d909-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="1d909-149">W **myVnet1** bloku, który jest wyświetlany, kliknij przycisk **komunikacji równorzędnych** z pionowy listy opcji w lewej części bloku.</span><span class="sxs-lookup"><span data-stu-id="1d909-149">In the **myVnet1** blade that appears, click **Peerings** from the vertical list of options on the left side of the blade.</span></span>
8. <span data-ttu-id="1d909-150">W **myVnet1 - komunikacji równorzędnych** bloku, które wystąpiły, kliknij przycisk **+ Dodaj**</span><span class="sxs-lookup"><span data-stu-id="1d909-150">In the **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="1d909-151">W **równorzędna Dodaj** bloku, zostanie wyświetlone, wprowadź, lub wybierz poniższe opcje, a następnie kliknij **OK**:</span><span class="sxs-lookup"><span data-stu-id="1d909-151">In the **Add peering** blade that appears, enter, or select the following options, then click **OK**:</span></span>
     - <span data-ttu-id="1d909-152">**Nazwa**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="1d909-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="1d909-153">**Model wdrażania sieci wirtualnej**: Wybierz **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="1d909-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="1d909-154">**Subskrypcja**: Wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="1d909-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="1d909-155">**Sieć wirtualna**: kliknij **wybierz sieć wirtualną**, następnie kliknij przycisk **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="1d909-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="1d909-156">**Zezwalaj na dostęp do sieci wirtualnej:** upewnij się, że **włączone** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="1d909-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="1d909-157">W tym samouczku są używane żadne inne ustawienia.</span><span class="sxs-lookup"><span data-stu-id="1d909-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="1d909-158">Aby dowiedzieć się więcej na temat wszystkich ustawień komunikacji równorzędnej, przeczytaj [Zarządzanie komunikacji równorzędnych sieci wirtualnych](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="1d909-158">To learn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="1d909-159">Po kliknięciu przycisku **OK** w poprzednim kroku, **równorzędna Dodaj** zamyka bloku, aby zobaczyć **myVnet1 - komunikacji równorzędnych** ponownie blok.</span><span class="sxs-lookup"><span data-stu-id="1d909-159">After clicking **OK** in the previous step, the **Add peering** blade closes and you see the **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="1d909-160">Po kilku sekundach komunikacji równorzędnej, utworzony zostanie wyświetlony w bloku.</span><span class="sxs-lookup"><span data-stu-id="1d909-160">After a few seconds, the peering you created appears in the blade.</span></span> <span data-ttu-id="1d909-161">**Zainicjowano** znajduje się w **RÓWNORZĘDNA stan** kolumny dla **myVnet1ToMyVnet2** równorzędna zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="1d909-161">**Initiated** is listed in the **PEERING STATUS** column for the **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="1d909-162">Już połączyć za pomocą Vnet1 do Vnet2, ale teraz musi równorzędnego myVnet2 do myVnet1.</span><span class="sxs-lookup"><span data-stu-id="1d909-162">You've peered Vnet1 to Vnet2, but now you must peer myVnet2 to myVnet1.</span></span> <span data-ttu-id="1d909-163">Komunikację równorzędną muszą być tworzone w obu kierunkach, aby włączyć zasobów w sieci wirtualne do komunikowania się ze sobą.</span><span class="sxs-lookup"><span data-stu-id="1d909-163">The peering must be created in both directions to enable resources in the virtual networks to communicate with each other.</span></span>
11. <span data-ttu-id="1d909-164">Wykonaj kroki 5 – 10 ponownie dla myVnet2.</span><span class="sxs-lookup"><span data-stu-id="1d909-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="1d909-165">Nazwa komunikację równorzędną *myVnet2ToMyVnet1*.</span><span class="sxs-lookup"><span data-stu-id="1d909-165">Name the peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="1d909-166">Kilka sekund po kliknięciu przycisku **OK** utworzyć komunikacji równorzędnej dla MyVnet2, **myVnet2ToMyVnet1** równorzędna właśnie utworzony znajduje się **połączony** w  **Komunikacja RÓWNORZĘDNA stan** kolumny.</span><span class="sxs-lookup"><span data-stu-id="1d909-166">A few seconds after clicking **OK** to create the peering for MyVnet2, the **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in the **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="1d909-167">Wykonaj kroki 5-7 ponownie dla MyVnet1.</span><span class="sxs-lookup"><span data-stu-id="1d909-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="1d909-168">**RÓWNORZĘDNA stan** dla **myVnet1ToVNet2** komunikacji równorzędnej jest teraz również **połączony**.</span><span class="sxs-lookup"><span data-stu-id="1d909-168">The **PEERING STATUS** for the **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="1d909-169">Komunikację równorzędną zostanie pomyślnie nawiązane po **połączony** w **RÓWNORZĘDNA stan** kolumny dla obu sieci wirtualnych w komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="1d909-169">The peering is successfully established after you see **Connected** in the **PEERING STATUS** column for both virtual networks in the peering.</span></span>
14. <span data-ttu-id="1d909-170">**Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć się z jednej maszyny wirtualnej do drugiej strony, aby sprawdzić łączność.</span><span class="sxs-lookup"><span data-stu-id="1d909-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
15. <span data-ttu-id="1d909-171">**Opcjonalne**: Aby usunąć zasoby, które możesz utworzyć w tym samouczku, wykonaj kroki [zasoby zostaną usunięte](#delete-portal) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="1d909-171">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="1d909-172">Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej mogą teraz komunikować się ze sobą za pośrednictwem ich adresy IP.</span><span class="sxs-lookup"><span data-stu-id="1d909-172">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="1d909-173">Jeśli używasz domyślnego rozwiązania Azure nazwy sieci wirtualnych, zasobów w sieci wirtualne nie będą mogli rozpoznawania nazw w sieciach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1d909-173">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="1d909-174">Rozpoznawanie nazw między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="1d909-174">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="1d909-175">Dowiedz się, jak skonfigurować [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="1d909-175">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="1d909-176"><a name="cli"></a>Utwórz równorzędna - wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1d909-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="1d909-177">Poniższy skrypt:</span><span class="sxs-lookup"><span data-stu-id="1d909-177">The following script:</span></span>

- <span data-ttu-id="1d909-178">Wymaga wiersza polecenia platformy Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1d909-178">Requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1d909-179">Aby znaleźć wersję, uruchom `az --version` polecenia.</span><span class="sxs-lookup"><span data-stu-id="1d909-179">To find the version, run the `az --version` command.</span></span> <span data-ttu-id="1d909-180">Jeśli konieczne będzie uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d909-180">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="1d909-181">Działanie powłoki Bash.</span><span class="sxs-lookup"><span data-stu-id="1d909-181">Works in a Bash shell.</span></span> <span data-ttu-id="1d909-182">Aby wyświetlić opcje uruchamiania skryptów wiersza polecenia platformy Azure na kliencie systemu Windows, zobacz [działający w systemie Windows Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d909-182">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="1d909-183">Zamiast instalowania interfejsu wiersza polecenia i jego zależności, można użyć powłoki chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="1d909-183">Instead of installing the CLI and its dependencies, you can use the Azure Cloud Shell.</span></span> <span data-ttu-id="1d909-184">Usługa Azure Cloud Shell jest bezpłatną powłoką Bash, którą można uruchamiać bezpośrednio w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1d909-184">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="1d909-185">Ma ona wstępnie zainstalowany interfejs wiersza polecenia platformy Azure skonfigurowany do użycia z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="1d909-185">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="1d909-186">Kliknij przycisk **wypróbuj** przycisk w skrypcie, który następujące, które wywołuje powłoka chmury, która rejestruje możesz zalogować się do konta platformy Azure z.</span><span class="sxs-lookup"><span data-stu-id="1d909-186">Click the **Try it** button in the script that follows, which invokes a Cloud Shell that logs you can log in to your Azure account with.</span></span> <span data-ttu-id="1d909-187">Aby wykonać skrypt, kliknij przycisk **kopiowania** przycisk i Wklej zawartość w chmurze powłoki.</span><span class="sxs-lookup"><span data-stu-id="1d909-187">To execute the script, click the **Copy** button and paste the contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="1d909-188">Utwórz grupę zasobów i dwie sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="1d909-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout the script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. <span data-ttu-id="1d909-189">Tworzenie sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="1d909-189">Create a virtual network peering between the two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get the id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get the id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 to VNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="1d909-190">Po wykonaniu skryptu, przejrzyj komunikacji równorzędnych dla każdej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1d909-190">After the script executes, review the peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="1d909-191">Poprzednie polecenie ponownie uruchomić, zastępując *myVnet1* z *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="1d909-191">Run the previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="1d909-192">Zarówno dane wyjściowe polecenia pokazuje **połączony** w **PeeringState** kolumny.</span><span class="sxs-lookup"><span data-stu-id="1d909-192">The output of both commands shows **Connected** in the **PeeringState** column.</span></span>

     <span data-ttu-id="1d909-193">Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej mogą teraz komunikować się ze sobą za pośrednictwem ich adresy IP.</span><span class="sxs-lookup"><span data-stu-id="1d909-193">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="1d909-194">Jeśli używasz domyślnego rozwiązania Azure nazwy sieci wirtualnych, zasobów w sieci wirtualne nie będą mogli rozpoznawania nazw w sieciach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1d909-194">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="1d909-195">Rozpoznawanie nazw między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="1d909-195">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="1d909-196">Dowiedz się, jak skonfigurować [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="1d909-196">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="1d909-197">**Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć się z jednej maszyny wirtualnej do drugiej strony, aby sprawdzić łączność.</span><span class="sxs-lookup"><span data-stu-id="1d909-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
5. <span data-ttu-id="1d909-198">**Opcjonalne**: Aby usunąć zasoby, które możesz utworzyć w tym samouczku, wykonaj kroki [zasoby zostaną usunięte](#delete-cli) w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="1d909-198">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="1d909-199"><a name="powershell"></a>Utwórz równorzędna — PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d909-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="1d909-200">Zainstaluj najnowszą wersję modułu [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d909-200">Install the latest version of the PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="1d909-201">Jeśli jesteś nowym użytkownikiem programu Azure PowerShell, zobacz temat [Azure PowerShell overview (Omówienie programu Azure PowerShell)](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d909-201">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="1d909-202">Aby rozpocząć sesję programu PowerShell, przejdź do pozycji **Start**, wprowadź ciąg **powershell**, a następnie kliknij pozycję **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1d909-202">To start a PowerShell session, go to **Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="1d909-203">W programie PowerShell zaloguj się do platformy Azure, wprowadzając polecenie `login-azurermaccount`.</span><span class="sxs-lookup"><span data-stu-id="1d909-203">In PowerShell, log in to Azure by entering the `login-azurermaccount` command.</span></span> <span data-ttu-id="1d909-204">Konto logowania przy użyciu musi mieć uprawnienia do tworzenia sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="1d909-204">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="1d909-205">Zobacz [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="1d909-205">See the [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="1d909-206">Utwórz grupę zasobów i dwie sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="1d909-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="1d909-207">Można wykonać skryptu, skopiuj poniższy skrypt, wklej go do programu PowerShell, a następnie naciśnij klawisz `Enter` po ostatnim wierszu są wyświetlane na ekranie:</span><span class="sxs-lookup"><span data-stu-id="1d909-207">To execute the script, copy the following script, paste it into PowerShell, and then press `Enter` after the last line appears on the screen:</span></span>

    ```powershell
    # Variables for common values used throughout the script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. <span data-ttu-id="1d909-208">Tworzenie sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="1d909-208">Create a virtual network peering between the two virtual networks.</span></span> <span data-ttu-id="1d909-209">Skopiuj poniższy skrypt, Wklej do środowiska PowerShell i naciśnij klawisz `Enter` po ostatnim wierszu są wyświetlane na ekranie:</span><span class="sxs-lookup"><span data-stu-id="1d909-209">Copy the following script, paste in to PowerShell, and then press `Enter` after the last line appears on the screen:</span></span>
    ```powershell
    # Peer VNet1 to VNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 to VNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="1d909-210">Aby przejrzeć podsieci sieci wirtualnej, skopiuj poniższe polecenie, Wklej do środowiska PowerShell i naciśnij klawisz `Enter`:</span><span class="sxs-lookup"><span data-stu-id="1d909-210">To review the subnets for the virtual network, copy the following command, paste in to PowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="1d909-211">Poprzednie polecenie ponownie uruchomić, zastępując *myVnet1* z *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="1d909-211">Run the previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="1d909-212">Zarówno dane wyjściowe polecenia pokazuje **połączony** w **PeeringState** kolumny.</span><span class="sxs-lookup"><span data-stu-id="1d909-212">The output of both commands shows **Connected** in the **PeeringState** column.</span></span>
7. <span data-ttu-id="1d909-213">**Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć się z jednej maszyny wirtualnej do drugiej strony, aby sprawdzić łączność.</span><span class="sxs-lookup"><span data-stu-id="1d909-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
8. <span data-ttu-id="1d909-214">**Opcjonalne**: Aby usunąć zasoby, które możesz utworzyć w tym samouczku, wykonaj kroki [zasoby zostaną usunięte](#delete-powershell) w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="1d909-214">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="1d909-215">Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej mogą teraz komunikować się ze sobą za pośrednictwem ich adresy IP.</span><span class="sxs-lookup"><span data-stu-id="1d909-215">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="1d909-216">Jeśli używasz domyślnego rozwiązania Azure nazwy sieci wirtualnych, zasobów w sieci wirtualne nie będą mogli rozpoznawania nazw w sieciach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1d909-216">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="1d909-217">Rozpoznawanie nazw między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="1d909-217">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="1d909-218">Dowiedz się, jak skonfigurować [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="1d909-218">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="1d909-219"><a name="template"></a>Utwórz równorzędna - szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d909-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="1d909-220">Odwołanie [tworzenie sieci wirtualnej komunikacji równorzędnej](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d909-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="1d909-221">Szablon jest dostarczany wraz z instrukcjami wdrażania przy użyciu witryny Azure Portal, programu PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d909-221">Instructions are provided with the template for deploying the template using the Azure portal, PowerShell, or the Azure CLI.</span></span> <span data-ttu-id="1d909-222">Logowanie w zależności od tego narzędzia, możesz wybrać opcję wdrożyć szablon przy użyciu konta, które ma odpowiednie uprawnienia do tworzenia sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="1d909-222">Log in to whichever tool you choose to deploy the template with using an account that has the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="1d909-223">Zobacz [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="1d909-223">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="1d909-224">**Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć się z jednej maszyny wirtualnej do drugiej strony, aby sprawdzić łączność.</span><span class="sxs-lookup"><span data-stu-id="1d909-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
3. <span data-ttu-id="1d909-225">**Opcjonalne**: Aby usunąć zasoby, które możesz utworzyć w tym samouczku, wykonaj kroki [zasoby zostaną usunięte](#delete) sekcji tego artykułu, przy użyciu portalu Azure, programu PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d909-225">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete) section of this article, using either the Azure portal, PowerShell, or the Azure CLI.</span></span>

## <span data-ttu-id="1d909-226"><a name="permissions"></a>Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="1d909-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="1d909-227">Konta, które służy do tworzenia sieci wirtualnej komunikacji równorzędnej musi mieć ról lub uprawnień.</span><span class="sxs-lookup"><span data-stu-id="1d909-227">The accounts you use to create a virtual network peering must have the necessary role or permissions.</span></span> <span data-ttu-id="1d909-228">Na przykład jeśli zostały równorzędna dwie sieci wirtualne o nazwach VNet1 i VNet2, Twoje konto musi zostać przypisane następujące minimalne roli lub uprawnienia dla każdej sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="1d909-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned the following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="1d909-229">Sieć wirtualna</span><span class="sxs-lookup"><span data-stu-id="1d909-229">Virtual network</span></span>|<span data-ttu-id="1d909-230">Rola</span><span class="sxs-lookup"><span data-stu-id="1d909-230">Role</span></span>|<span data-ttu-id="1d909-231">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="1d909-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="1d909-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="1d909-232">VNet1</span></span>|[<span data-ttu-id="1d909-233">Współautor sieci</span><span class="sxs-lookup"><span data-stu-id="1d909-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="1d909-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="1d909-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="1d909-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="1d909-235">VNet2</span></span>|[<span data-ttu-id="1d909-236">Współautor sieci</span><span class="sxs-lookup"><span data-stu-id="1d909-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="1d909-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="1d909-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="1d909-238">Dowiedz się więcej o [wbudowane role](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) i przypisywanie określonych uprawnień do [role niestandardowe](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (tylko Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="1d909-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions to [custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="1d909-239"><a name="delete"></a>Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="1d909-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="1d909-240">Po zakończeniu tego samouczka można usunąć utworzony w samouczka w celu uniknięcia opłat użycie zasobów.</span><span class="sxs-lookup"><span data-stu-id="1d909-240">When you've finished this tutorial, you might want to delete the resources you created in the tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="1d909-241">Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów, które znajdują się w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="1d909-241">Deleting a resource group also deletes all resources that are in the resource group.</span></span>

### <span data-ttu-id="1d909-242"><a name="delete-portal"></a>Azure portal</span><span class="sxs-lookup"><span data-stu-id="1d909-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="1d909-243">W polu wyszukiwania portalu wprowadź **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="1d909-243">In the portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="1d909-244">W wynikach wyszukiwania kliknij **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="1d909-244">In the search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="1d909-245">Na **myResourceGroup** bloku, kliknij przycisk **usunąć** ikony.</span><span class="sxs-lookup"><span data-stu-id="1d909-245">On the **myResourceGroup** blade, click the **Delete** icon.</span></span>
3. <span data-ttu-id="1d909-246">Aby potwierdzić decyzję, w **typu nazwa grupy zasobów** wprowadź **myResourceGroup**, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="1d909-246">To confirm the deletion, in the **TYPE THE RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="1d909-247"><a name="delete-cli"></a>Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1d909-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="1d909-248">Wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1d909-248">Enter the following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="1d909-249"><a name="delete-powershell"></a>Środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d909-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="1d909-250">Wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1d909-250">Enter the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="1d909-251">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d909-251">Next steps</span></span>

- <span data-ttu-id="1d909-252">Należy dokładnie zapoznać się z ważne [ograniczenia komunikacji równorzędnej sieci wirtualnej i zachowania](virtual-network-manage-peering.md#requirements-and-constraints) przed utworzeniem sieci wirtualnej komunikacji równorzędnej w środowisku produkcyjnym należy używać.</span><span class="sxs-lookup"><span data-stu-id="1d909-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="1d909-253">Więcej informacji na temat wszystkich [sieci wirtualnej komunikacji równorzędnej ustawienia](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="1d909-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="1d909-254">Dowiedz się, jak [tworzenie koncentratora i gwiazda topologii sieci](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) z sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="1d909-254">Learn how to [create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
