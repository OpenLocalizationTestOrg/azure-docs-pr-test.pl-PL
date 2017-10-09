---
title: "aaaConfigure prywatnych adresów IP dla maszyn wirtualnych (klasyczne) — portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure prywatnych adresów IP maszyn wirtualnych (klasyczne) za pomocą hello portalu Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a><span data-ttu-id="c0de2-103">Konfigurowanie prywatnych adresów IP dla maszyny wirtualnej (klasyczne) przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c0de2-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c0de2-104">W tym artykule omówiono hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c0de2-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="c0de2-105">Możesz również [Zarządzanie statycznego prywatnego adresu IP w modelu wdrażania usługi Resource Manager hello](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c0de2-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="c0de2-106">Poniższe kroki przykładowe Hello oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="c0de2-106">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="c0de2-107">Jeśli kroki hello toorun wyświetlaną w tym dokumencie, należy najpierw utworzyć hello środowisko testowe opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c0de2-107">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="c0de2-108">Jak toospecify statycznych prywatnych adresów IP podczas tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c0de2-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="c0de2-109">toocreate maszyny Wirtualnej o nazwie *DNS01* w hello *frontonu* podsieci sieci wirtualnej o nazwie *TestVNet* z statycznego prywatnego adresu IP z *192.168.1.101*, Wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c0de2-109">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="c0de2-110">W przeglądarce Przejdź toohttp://portal.azure.com i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c0de2-110">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="c0de2-111">Kliknij przycisk **nowy** > **obliczeniowe** > **systemu Windows Server 2012 R2 Datacenter**, zwróć uwagę, że hello **wybierz model wdrożenia** listy już pokazuje **klasycznego**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c0de2-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="c0de2-113">W hello **Utwórz maszynę Wirtualną** bloku, wprowadź nazwę hello hello toobe maszyny Wirtualnej utworzone (*DNS01* w naszym scenariuszu), hello konta administratora lokalnego i hasło.</span><span class="sxs-lookup"><span data-stu-id="c0de2-113">In hello **Create VM** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password.</span></span>
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="c0de2-115">Kliknij przycisk **konfiguracji opcjonalnej** > **sieci** > **sieci wirtualnej**, a następnie kliknij przycisk **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="c0de2-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="c0de2-116">Jeśli **TestVNet** jest niedostępny, upewnij się, że używasz hello *środkowe stany USA* lokalizacji i utworzeniu hello środowisko testowe opisane na początku hello tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="c0de2-116">If **TestVNet** is not available, make sure you are using hello *Central US* location and have created hello test environment described at hello beginning of this article.</span></span>
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="c0de2-118">W hello **sieci** jest upewnij się, że podsieci hello aktualnie zaznaczonego bloku *frontonu*, następnie kliknij przycisk **adresów IP**w obszarze **przypisywania adresów IP** kliknij **statycznych**, a następnie wprowadź *192.168.1.101* dla **adres IP** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c0de2-118">In hello **Network** blade, make sure hello subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="c0de2-120">Kliknij przycisk **OK** w hello **adresów IP** bloku, następnie kliknij przycisk **OK** w hello **sieci** bloku, a następnie kliknij przycisk **OK**w hello **opcjonalne config** bloku.</span><span class="sxs-lookup"><span data-stu-id="c0de2-120">Click **OK** in hello **IP addresses** blade, then click **OK** in hello **Network** blade, and click **OK** in hello **Optional config** blade.</span></span>
7. <span data-ttu-id="c0de2-121">W hello **Utwórz maszynę Wirtualną** bloku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c0de2-121">In hello **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="c0de2-122">Powiadomienie hello kafelka poniżej wyświetlane na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="c0de2-122">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="c0de2-124">Jak tooretrieve statycznych prywatnych adresów IP informacji dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c0de2-124">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="c0de2-125">tooview hello statycznych prywatne informacje o adresie IP dla hello się, że maszyna wirtualna utworzona z powyższych kroków hello wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="c0de2-125">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="c0de2-126">W portalu Azure, Azure hello, kliknij polecenie **PRZEGLĄDAJ wszystko** > **maszyn wirtualnych (klasyczne)** > **DNS01**  >   **Wszystkie ustawienia** > **adresów IP** i zwróć uwagę, hello przypisywania adresów IP i adres IP, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c0de2-126">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice hello IP address assignment and IP address as seen below.</span></span>
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="c0de2-128">Jak tooremove statycznych prywatnych adresów IP z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c0de2-128">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="c0de2-129">tooremove hello statycznego prywatnego adresu IP z powitalne maszyny Wirtualnej utworzone powyżej, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="c0de2-129">tooremove hello static private IP address from hello VM created above, follow hello steps below.</span></span>

1. <span data-ttu-id="c0de2-130">Z hello **adresów IP** bloku przedstawionych powyżej, kliknij przycisk **dynamiczne** toohello po prawej **przypisywania adresów IP**, następnie kliknij przycisk **zapisać**, a następnie Kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="c0de2-130">From hello **IP addresses** blade shown above, click **Dynamic** toohello right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Tworzenie maszyny Wirtualnej w portalu Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="c0de2-132">Jak tooadd statycznego prywatnego adresu IP adresów tooan istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c0de2-132">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="c0de2-133">tooadd statycznego prywatnego adresu IP adres toohello maszyny Wirtualnej utworzonej przy użyciu powyższych kroków hello wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c0de2-133">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="c0de2-134">Z hello **adresów IP** bloku przedstawionych powyżej, kliknij przycisk **statycznych** toohello prawo **przypisywania adresów IP**.</span><span class="sxs-lookup"><span data-stu-id="c0de2-134">From hello **IP addresses** blade shown above, click **Static** toohello right of **IP address assignment**.</span></span>
2. <span data-ttu-id="c0de2-135">Typ *192.168.1.101* dla **adres IP**, następnie kliknij przycisk **zapisać**, a następnie kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="c0de2-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0de2-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c0de2-136">Next steps</span></span>
* <span data-ttu-id="c0de2-137">Dowiedz się więcej o [zastrzeżone publicznego adresu IP](virtual-networks-reserved-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="c0de2-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="c0de2-138">Dowiedz się więcej o [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="c0de2-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="c0de2-139">Zapoznaj się hello [zastrzeżonego adresu IP interfejsów API REST](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0de2-139">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

