---
title: "aaaCreate równorzędna sieci wirtualnej platformy Azure - Resource Manager — tej samej subskrypcji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi utworzone za pomocą Menedżera zasobów istnieje w hello sam subskrypcji platformy Azure."
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
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="2337f-103">Tworzenie sieci wirtualnej równorzędna - Resource Manager tej samej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2337f-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="2337f-104">Z tego samouczka dowiesz się toocreate sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi utworzone za pomocą Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="2337f-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="2337f-105">Obie sieci wirtualne istnieją w hello sam subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2337f-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="2337f-106">Witaj komunikacji równorzędnej dwa zasoby umożliwia sieci wirtualnych w różnych sieciach wirtualnych toocommunicate ze sobą z tej samej przepustowości i opóźnień tak, jakby hello zasoby były hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2337f-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="2337f-107">Dowiedz się więcej o [równorzędna sieci wirtualnej](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2337f-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="2337f-108">Witaj toocreate kroki sieci wirtualnej komunikacji równorzędnej są różne, w zależności od tego, czy hello sieci wirtualne są w hello tych samych lub różnych subskrypcji i które [modelu wdrożenia usługi Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sieci wirtualne są tworzone za pomocą.</span><span class="sxs-lookup"><span data-stu-id="2337f-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="2337f-109">Dowiedz się, jak toocreate a wirtualnych sieci równorzędna w innych sytuacjach, klikając hello scenariusza z hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="2337f-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="2337f-110">Model wdrażania platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2337f-110">Azure deployment model</span></span>  | <span data-ttu-id="2337f-111">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2337f-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="2337f-112">Obie usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2337f-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="2337f-113">Różne</span><span class="sxs-lookup"><span data-stu-id="2337f-113">Different</span></span>|
|[<span data-ttu-id="2337f-114">Jeden Resource Manager, co classic</span><span class="sxs-lookup"><span data-stu-id="2337f-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="2337f-115">tym samym</span><span class="sxs-lookup"><span data-stu-id="2337f-115">Same</span></span>|
|[<span data-ttu-id="2337f-116">Jeden Resource Manager, co classic</span><span class="sxs-lookup"><span data-stu-id="2337f-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="2337f-117">Różne</span><span class="sxs-lookup"><span data-stu-id="2337f-117">Different</span></span>|

<span data-ttu-id="2337f-118">Nie można utworzyć sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnej wdrożone za pośrednictwem hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="2337f-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="2337f-119">Element równorzędny sieci wirtualnej można tworzyć tylko między dwiema sieciami wirtualnych, które istnieją w hello sam region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2337f-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="2337f-120">Jeśli potrzebujesz sieci wirtualnych tooconnect zarówno utworzonych za pomocą hello klasycznego modelu wdrażania lub istnieje w różnych regionach platformy Azure, można użyć Azure [bramy sieci VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2337f-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="2337f-121">Można użyć hello [portalu Azure](#portal), hello Azure [interfejsu wiersza polecenia](#cli) (CLI) Azure [PowerShell](#powershell), lub [szablonu usługi Azure Resource Manager](#template) toocreate sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="2337f-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) toocreate a virtual network peering.</span></span> <span data-ttu-id="2337f-122">Kliknij dowolny z hello poprzedniego narzędzia łącza toogo, bezpośrednio toohello kroki tworzenia sieci wirtualnej komunikacji równorzędnej narzędzie wyboru.</span><span class="sxs-lookup"><span data-stu-id="2337f-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="2337f-123"><a name="portal"></a>Utwórz równorzędna - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2337f-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="2337f-124">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2337f-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2337f-125">Zaloguj się przy użyciu konta Hello musi mieć hello toocreate niezbędne uprawnienia sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="2337f-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="2337f-126">Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="2337f-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="2337f-127">Kliknij przycisk **+ nowy**, kliknij przycisk **sieci**, następnie kliknij przycisk **sieci wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="2337f-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="2337f-128">W hello **Utwórz sieć wirtualną** bloku, wprowadź, lub wybierz wartości dla hello następujące ustawienia, a następnie kliknij **Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="2337f-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="2337f-129">**Nazwa**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="2337f-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="2337f-130">**Przestrzeń adresowa**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="2337f-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="2337f-131">**Nazwa podsieci**: *domyślne*</span><span class="sxs-lookup"><span data-stu-id="2337f-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="2337f-132">**Zakres adresów podsieci**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="2337f-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="2337f-133">**Subskrypcja**: Wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="2337f-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="2337f-134">**Grupa zasobów**: Wybierz **Utwórz nowy** , a następnie wprowadź *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="2337f-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="2337f-135">**Lokalizacja**: *wschodnie stany USA*</span><span class="sxs-lookup"><span data-stu-id="2337f-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="2337f-136">Wykonaj kroki od 2 do 3 ponownie określanie hello następujące wartości w kroku 3:</span><span class="sxs-lookup"><span data-stu-id="2337f-136">Complete steps 2-3 again specifying hello following values in step 3:</span></span>
    - <span data-ttu-id="2337f-137">**Nazwa**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="2337f-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="2337f-138">**Przestrzeń adresowa**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="2337f-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="2337f-139">**Nazwa podsieci**: *domyślne*</span><span class="sxs-lookup"><span data-stu-id="2337f-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="2337f-140">**Zakres adresów podsieci**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="2337f-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="2337f-141">**Subskrypcja**: Wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="2337f-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="2337f-142">**Grupa zasobów**: Wybierz **Użyj istniejącego** i wybierz *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="2337f-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="2337f-143">**Lokalizacja**: *wschodnie stany USA*</span><span class="sxs-lookup"><span data-stu-id="2337f-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="2337f-144">W hello **wyszukiwania zasobów** pole u góry hello hello portalu, typ *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="2337f-144">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="2337f-145">Kliknij przycisk **myResourceGroup** po wyświetleniu w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="2337f-145">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="2337f-146">Zostanie wyświetlony blok hello **myresourcegroup** grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="2337f-146">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="2337f-147">Grupa zasobów Hello zawiera Witaj dwie sieci wirtualne utworzone w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="2337f-147">hello resource group contains hello two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="2337f-148">Kliknij przycisk **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="2337f-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="2337f-149">W hello **myVnet1** bloku, który jest wyświetlany, kliknij przycisk **komunikacji równorzędnych** z hello pionowy listy opcji na powitania po lewej stronie powitania bloku.</span><span class="sxs-lookup"><span data-stu-id="2337f-149">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
8. <span data-ttu-id="2337f-150">W hello **myVnet1 - komunikacji równorzędnych** bloku, które wystąpiły, kliknij przycisk **+ Dodaj**</span><span class="sxs-lookup"><span data-stu-id="2337f-150">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="2337f-151">W hello **równorzędna Dodaj** bloku, zostanie wyświetlone, wprowadź, lub wybierz hello następujące opcje, a następnie kliknij **OK**:</span><span class="sxs-lookup"><span data-stu-id="2337f-151">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="2337f-152">**Nazwa**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="2337f-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="2337f-153">**Model wdrażania sieci wirtualnej**: Wybierz **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="2337f-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="2337f-154">**Subskrypcja**: Wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="2337f-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="2337f-155">**Sieć wirtualna**: kliknij **wybierz sieć wirtualną**, następnie kliknij przycisk **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="2337f-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="2337f-156">**Zezwalaj na dostęp do sieci wirtualnej:** upewnij się, że **włączone** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="2337f-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="2337f-157">W tym samouczku są używane żadne inne ustawienia.</span><span class="sxs-lookup"><span data-stu-id="2337f-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="2337f-158">Przeczytaj toolearn dotyczące wszystkich ustawień komunikacji równorzędnej, [Zarządzanie komunikacji równorzędnych sieci wirtualnych](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="2337f-158">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="2337f-159">Po kliknięciu przycisku **OK** w poprzednim kroku hello hello **równorzędna Dodaj** bloku zamyka i zobacz hello **myVnet1 - komunikacji równorzędnych** ponownie blok.</span><span class="sxs-lookup"><span data-stu-id="2337f-159">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="2337f-160">Po kilku sekundach hello równorzędna utworzonego pojawia się w bloku hello.</span><span class="sxs-lookup"><span data-stu-id="2337f-160">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="2337f-161">**Zainicjowane** ma na liście hello **RÓWNORZĘDNA stan** kolumny dla hello **myVnet1ToMyVnet2** równorzędna zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="2337f-161">**Initiated** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="2337f-162">Już połączyć za pomocą Vnet1 tooVnet2, ale teraz musi równorzędnego myVnet2 toomyVnet1.</span><span class="sxs-lookup"><span data-stu-id="2337f-162">You've peered Vnet1 tooVnet2, but now you must peer myVnet2 toomyVnet1.</span></span> <span data-ttu-id="2337f-163">równorzędna Hello należy utworzyć w obu kierunkach tooenable zasobów w toocommunicate sieci wirtualnych hello ze sobą.</span><span class="sxs-lookup"><span data-stu-id="2337f-163">hello peering must be created in both directions tooenable resources in hello virtual networks toocommunicate with each other.</span></span>
11. <span data-ttu-id="2337f-164">Wykonaj kroki 5 – 10 ponownie dla myVnet2.</span><span class="sxs-lookup"><span data-stu-id="2337f-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="2337f-165">Nazwa hello równorzędna *myVnet2ToMyVnet1*.</span><span class="sxs-lookup"><span data-stu-id="2337f-165">Name hello peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="2337f-166">Kilka sekund po kliknięciu przycisku **OK** toocreate hello komunikacji równorzędnej dla MyVnet2, hello **myVnet2ToMyVnet1** równorzędna właśnie utworzony znajduje się **połączony** w hello  **Komunikacja RÓWNORZĘDNA stan** kolumny.</span><span class="sxs-lookup"><span data-stu-id="2337f-166">A few seconds after clicking **OK** toocreate hello peering for MyVnet2, hello **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in hello **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="2337f-167">Wykonaj kroki 5-7 ponownie dla MyVnet1.</span><span class="sxs-lookup"><span data-stu-id="2337f-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="2337f-168">Witaj **RÓWNORZĘDNA stan** dla hello **myVnet1ToVNet2** komunikacji równorzędnej jest teraz również **połączony**.</span><span class="sxs-lookup"><span data-stu-id="2337f-168">hello **PEERING STATUS** for hello **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="2337f-169">równorzędna Hello zostanie pomyślnie nawiązane po **połączony** w hello **RÓWNORZĘDNA stan** kolumny dla obu sieci wirtualnych w komunikacji równorzędnej hello.</span><span class="sxs-lookup"><span data-stu-id="2337f-169">hello peering is successfully established after you see **Connected** in hello **PEERING STATUS** column for both virtual networks in hello peering.</span></span>
14. <span data-ttu-id="2337f-170">**Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.</span><span class="sxs-lookup"><span data-stu-id="2337f-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
15. <span data-ttu-id="2337f-171">**Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello etapami hello [zasoby zostaną usunięte](#delete-portal) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="2337f-171">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="2337f-172">Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP.</span><span class="sxs-lookup"><span data-stu-id="2337f-172">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="2337f-173">Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="2337f-173">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="2337f-174">Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="2337f-174">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="2337f-175">Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="2337f-175">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="2337f-176"><a name="cli"></a>Utwórz równorzędna - wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2337f-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="2337f-177">Witaj następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="2337f-177">hello following script:</span></span>

- <span data-ttu-id="2337f-178">Wymaga hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="2337f-178">Requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2337f-179">Wersja hello toofind, uruchom hello `az --version` polecenia.</span><span class="sxs-lookup"><span data-stu-id="2337f-179">toofind hello version, run hello `az --version` command.</span></span> <span data-ttu-id="2337f-180">Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2337f-180">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="2337f-181">Działanie powłoki Bash.</span><span class="sxs-lookup"><span data-stu-id="2337f-181">Works in a Bash shell.</span></span> <span data-ttu-id="2337f-182">Aby wyświetlić opcje uruchamiania skryptów wiersza polecenia platformy Azure na kliencie systemu Windows, zobacz [działający w systemie Windows hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2337f-182">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="2337f-183">Zamiast instalowania hello interfejsu wiersza polecenia i jego zależności, możesz użyć hello powłoki chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="2337f-183">Instead of installing hello CLI and its dependencies, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="2337f-184">Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2337f-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="2337f-185">Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="2337f-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="2337f-186">Kliknij przycisk hello **wypróbuj** przycisku na powitania skrypt, który pozostaje zgodne z regułami, które wywołuje powłoki chmury, który loguje się użytkownik może zalogować się tooyour konto platformy Azure z.</span><span class="sxs-lookup"><span data-stu-id="2337f-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="2337f-187">tooexecute hello skrypt, kliknij przycisk hello **kopiowania** przycisk i Wklej zawartość hello w chmurze powłoki.</span><span class="sxs-lookup"><span data-stu-id="2337f-187">tooexecute hello script, click hello **Copy** button and paste hello contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="2337f-188">Utwórz grupę zasobów i dwie sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="2337f-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
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

2. <span data-ttu-id="2337f-189">Tworzenie sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnymi hello.</span><span class="sxs-lookup"><span data-stu-id="2337f-189">Create a virtual network peering between hello two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="2337f-190">Po wykonaniu skryptu hello, przejrzyj komunikacji równorzędnych powitania dla każdej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2337f-190">After hello script executes, review hello peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="2337f-191">Poprzednie polecenie hello ponownie uruchomić, zastępując *myVnet1* z *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="2337f-191">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="2337f-192">dane wyjściowe Hello obu polecenia pokazuje **połączony** w hello **PeeringState** kolumny.</span><span class="sxs-lookup"><span data-stu-id="2337f-192">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>

     <span data-ttu-id="2337f-193">Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP.</span><span class="sxs-lookup"><span data-stu-id="2337f-193">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="2337f-194">Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="2337f-194">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="2337f-195">Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="2337f-195">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="2337f-196">Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="2337f-196">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="2337f-197">**Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.</span><span class="sxs-lookup"><span data-stu-id="2337f-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
5. <span data-ttu-id="2337f-198">**Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-cli) w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="2337f-198">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="2337f-199"><a name="powershell"></a>Utwórz równorzędna — PowerShell</span><span class="sxs-lookup"><span data-stu-id="2337f-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="2337f-200">Zainstaluj najnowszą wersję hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułu.</span><span class="sxs-lookup"><span data-stu-id="2337f-200">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="2337f-201">Jeśli jesteś tooAzure nowego środowiska PowerShell, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2337f-201">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="2337f-202">toostart sesję programu PowerShell Przejdź zbyt**Start**, wprowadź **powershell**, a następnie kliknij przycisk **programu PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2337f-202">toostart a PowerShell session, go too**Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="2337f-203">W programie PowerShell Zaloguj tooAzure wprowadzając hello `login-azurermaccount` polecenia.</span><span class="sxs-lookup"><span data-stu-id="2337f-203">In PowerShell, log in tooAzure by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="2337f-204">Zaloguj się przy użyciu konta Hello musi mieć hello toocreate niezbędne uprawnienia sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="2337f-204">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="2337f-205">Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="2337f-205">See hello [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="2337f-206">Utwórz grupę zasobów i dwie sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="2337f-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="2337f-207">skrypt hello tooexecute, następujące hello kopii skryptu, wklej go do programu PowerShell, a następnie naciśnij `Enter` po ostatnim wierszu hello jest wyświetlany na ekranie powitania:</span><span class="sxs-lookup"><span data-stu-id="2337f-207">tooexecute hello script, copy hello following script, paste it into PowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>

    ```powershell
    # Variables for common values used throughout hello script.
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

5. <span data-ttu-id="2337f-208">Tworzenie sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnymi hello.</span><span class="sxs-lookup"><span data-stu-id="2337f-208">Create a virtual network peering between hello two virtual networks.</span></span> <span data-ttu-id="2337f-209">Następujące hello kopii skryptu, Wklej tooPowerShell i naciśnij klawisz `Enter` po ostatnim wierszu hello jest wyświetlany na ekranie powitania:</span><span class="sxs-lookup"><span data-stu-id="2337f-209">Copy hello following script, paste in tooPowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="2337f-210">tooreview hello podsieci sieci wirtualnej hello, kopiowania hello następujące polecenia, Wklej tooPowerShell, a następnie naciśnij `Enter`:</span><span class="sxs-lookup"><span data-stu-id="2337f-210">tooreview hello subnets for hello virtual network, copy hello following command, paste in tooPowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="2337f-211">Poprzednie polecenie hello ponownie uruchomić, zastępując *myVnet1* z *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="2337f-211">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="2337f-212">dane wyjściowe Hello obu polecenia pokazuje **połączony** w hello **PeeringState** kolumny.</span><span class="sxs-lookup"><span data-stu-id="2337f-212">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>
7. <span data-ttu-id="2337f-213">**Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.</span><span class="sxs-lookup"><span data-stu-id="2337f-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
8. <span data-ttu-id="2337f-214">**Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-powershell) w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="2337f-214">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="2337f-215">Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP.</span><span class="sxs-lookup"><span data-stu-id="2337f-215">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="2337f-216">Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="2337f-216">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="2337f-217">Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="2337f-217">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="2337f-218">Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="2337f-218">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="2337f-219"><a name="template"></a>Utwórz równorzędna - szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2337f-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="2337f-220">Odwołanie [tworzenie sieci wirtualnej komunikacji równorzędnej](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2337f-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="2337f-221">Instrukcje znajdują się z szablonem hello wdrażania szablonu hello przy użyciu hello portalu Azure, programu PowerShell lub hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2337f-221">Instructions are provided with hello template for deploying hello template using hello Azure portal, PowerShell, or hello Azure CLI.</span></span> <span data-ttu-id="2337f-222">Dziennik w narzędziu toowhichever, wybierz szablon hello toodeploy przy użyciu konta, które ma hello toocreate niezbędnych uprawnień sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="2337f-222">Log in toowhichever tool you choose toodeploy hello template with using an account that has hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="2337f-223">Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="2337f-223">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="2337f-224">**Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.</span><span class="sxs-lookup"><span data-stu-id="2337f-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
3. <span data-ttu-id="2337f-225">**Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello etapami hello [zasoby zostaną usunięte](#delete) hello sekcji tego artykułu, za pomocą portalu Azure, programu PowerShell lub hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2337f-225">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete) section of this article, using either hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

## <span data-ttu-id="2337f-226"><a name="permissions"></a>Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="2337f-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="2337f-227">konta Hello się, że używasz toocreate sieci wirtualnej komunikacji równorzędnej musi mieć hello ról lub uprawnień.</span><span class="sxs-lookup"><span data-stu-id="2337f-227">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="2337f-228">Na przykład jeśli zostały równorzędna dwie sieci wirtualne o nazwach VNet1 i VNet2, Twoje konto musi zostać przypisane hello następujące minimalne roli lub uprawnienia dla każdej sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="2337f-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="2337f-229">Sieć wirtualna</span><span class="sxs-lookup"><span data-stu-id="2337f-229">Virtual network</span></span>|<span data-ttu-id="2337f-230">Rola</span><span class="sxs-lookup"><span data-stu-id="2337f-230">Role</span></span>|<span data-ttu-id="2337f-231">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="2337f-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="2337f-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="2337f-232">VNet1</span></span>|[<span data-ttu-id="2337f-233">Współautor sieci</span><span class="sxs-lookup"><span data-stu-id="2337f-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="2337f-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="2337f-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="2337f-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="2337f-235">VNet2</span></span>|[<span data-ttu-id="2337f-236">Współautor sieci</span><span class="sxs-lookup"><span data-stu-id="2337f-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="2337f-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="2337f-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="2337f-238">Dowiedz się więcej o [wbudowane role](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) i przypisywanie uprawnień określonych zbyt[role niestandardowe](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (tylko Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="2337f-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="2337f-239"><a name="delete"></a>Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="2337f-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="2337f-240">Po zakończeniu tego samouczka można toodelete hello zasobów, utworzony w samouczek hello w celu uniknięcia opłat użycie.</span><span class="sxs-lookup"><span data-stu-id="2337f-240">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="2337f-241">Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów, które znajdują się w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="2337f-241">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="2337f-242"><a name="delete-portal"></a>Azure portal</span><span class="sxs-lookup"><span data-stu-id="2337f-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="2337f-243">W polu wyszukiwania portalu hello wpisz **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="2337f-243">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="2337f-244">W wynikach wyszukiwania powitania kliknij **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="2337f-244">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="2337f-245">Na powitania **myResourceGroup** bloku, kliknij przycisk hello **usunąć** ikony.</span><span class="sxs-lookup"><span data-stu-id="2337f-245">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="2337f-246">Usuwanie hello tooconfirm, w hello **hello typu nazwa grupy zasobów** wprowadź **myResourceGroup**, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="2337f-246">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="2337f-247"><a name="delete-cli"></a>Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2337f-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="2337f-248">Wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2337f-248">Enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="2337f-249"><a name="delete-powershell"></a>Środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="2337f-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="2337f-250">Wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2337f-250">Enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="2337f-251">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2337f-251">Next steps</span></span>

- <span data-ttu-id="2337f-252">Należy dokładnie zapoznać się z ważne [ograniczenia komunikacji równorzędnej sieci wirtualnej i zachowania](virtual-network-manage-peering.md#requirements-and-constraints) przed utworzeniem sieci wirtualnej komunikacji równorzędnej w środowisku produkcyjnym należy używać.</span><span class="sxs-lookup"><span data-stu-id="2337f-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="2337f-253">Więcej informacji na temat wszystkich [sieci wirtualnej komunikacji równorzędnej ustawienia](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="2337f-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="2337f-254">Dowiedz się, jak za[tworzenie koncentratora i gwiazda topologii sieci](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) z sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="2337f-254">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
