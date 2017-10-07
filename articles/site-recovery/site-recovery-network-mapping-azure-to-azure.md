---
title: "Mapowanie aaaNetwork między dwóch regionach platformy Azure w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Usługa Azure Site Recovery koordynuje hello replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Więcej informacji na temat trybu failover tooAzure lub dodatkowego centrum danych."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="e12d2-104">Mapowanie sieci między dwóch regionach platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e12d2-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="e12d2-105">W tym artykule opisano sposób toomap Azure sieci wirtualnych dwóch regionów systemu Azure wraz ze sobą.</span><span class="sxs-lookup"><span data-stu-id="e12d2-105">This article describes how toomap Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="e12d2-106">Mapowanie sieci zapewnia, że po utworzeniu maszyny wirtualnej zreplikowanej w celu hello region platformy Azure jest tworzona na powitania sieci wirtualnej jest toovirtual mapowanej sieci hello źródłowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e12d2-106">Network mapping ensures that when replicated virtual machine is created in hello target Azure region, it is created on hello virtual network that is mapped toovirtual network of hello source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="e12d2-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e12d2-107">Prerequisites</span></span>
<span data-ttu-id="e12d2-108">Przed zamapowaniem sieci upewnij się, utworzono [sieci wirtualnych platformy Azure](../virtual-network/virtual-networks-overview.md) zarówno źródłowych i docelowych regiony platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e12d2-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="e12d2-109">Mapowanie sieci</span><span class="sxs-lookup"><span data-stu-id="e12d2-109">Map networks</span></span>

<span data-ttu-id="e12d2-110">toomap sieci wirtualnej platformy Azure w sieci wirtualnej tooanother jeden region platformy Azure w innym regionie, przejdź tooSite infrastruktura Recovery -> Mapowanie sieci (maszyn wirtualnych platformy Azure) i Utwórz mapowania sieci.</span><span class="sxs-lookup"><span data-stu-id="e12d2-110">toomap an Azure virtual network in one Azure region tooanother virtual network in another region, go tooSite Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="e12d2-112">W hello w poniższym przykładzie Moja maszyna wirtualna jest uruchomiona w regionie Azja Wschodnia, a także są replikowane tooSoutheast Azja.</span><span class="sxs-lookup"><span data-stu-id="e12d2-112">In hello example below my virtual machine is running in East Asia region and is being replicated tooSoutheast Asia.</span></span>

<span data-ttu-id="e12d2-113">Wybierz sieć źródłowa i docelowa hello, a następnie kliknij przycisk OK toocreate mapowanie sieci tooSoutheast Azja Wschodnia, Azja.</span><span class="sxs-lookup"><span data-stu-id="e12d2-113">Select hello source and target network and then click OK toocreate a network mapping from East Asia tooSoutheast Asia.</span></span>

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="e12d2-115">Witaj sam element toocreate mapowanie sieci tooEast Azja południowo-wschodnia, Azja.</span><span class="sxs-lookup"><span data-stu-id="e12d2-115">Do hello same thing toocreate a network mapping from Southeast Asia tooEast Asia.</span></span>  
![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="e12d2-117">Mapowanie sieci, podczas włączania replikacji</span><span class="sxs-lookup"><span data-stu-id="e12d2-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="e12d2-118">Jeśli nie zostanie zrobione mapowanie sieci, podczas replikowania maszyny wirtualnej do hello pierwszego czasu formularza jeden region platformy Azure tooanother, możesz zdecydować, Sieć docelowa hello w ramach tego samego procesu.</span><span class="sxs-lookup"><span data-stu-id="e12d2-118">If network mapping is not done when you are replicating a virtual machine for hello first time form one Azure region tooanother, then you can choose target network as part of hello same process.</span></span> <span data-ttu-id="e12d2-119">Usługa Site Recovery tworzy mapowania sieci z tootarget regionu źródłowego i docelowego regionu toosource na podstawie tego zaznaczenia.</span><span class="sxs-lookup"><span data-stu-id="e12d2-119">Site Recovery creates network mappings from source region tootarget region and from target region toosource region based on this selection.</span></span>   

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="e12d2-121">Domyślnie usługi Site Recovery tworzy sieć w regionie docelowym hello, który jest identyczne toohello źródłowej sieci i dodając "— Funkcja automatycznego odzyskiwania systemu" jako nazwę toohello sufiks hello źródła sieci.</span><span class="sxs-lookup"><span data-stu-id="e12d2-121">By default, Site Recovery creates a network in hello target region that is identical toohello source network and by adding '-asr' as a suffix toohello name of hello source network.</span></span> <span data-ttu-id="e12d2-122">Możesz wybrać utworzone sieci, klikając przycisk Dostosuj.</span><span class="sxs-lookup"><span data-stu-id="e12d2-122">You can choose an already created network by clicking Customize.</span></span>

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="e12d2-124">Jeśli mapowanie sieci hello zostało już przeprowadzone, nie można zmienić sieci wirtualnej hello docelowego podczas włączania replikacji.</span><span class="sxs-lookup"><span data-stu-id="e12d2-124">If hello network mapping is already done, you can't change hello target virtual network while enabling replication.</span></span> <span data-ttu-id="e12d2-125">toochange, zmodyfikuj istniejące mapowanie sieci.</span><span class="sxs-lookup"><span data-stu-id="e12d2-125">toochange it, modify existing network mapping.</span></span>  

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="e12d2-128">Jeśli zmodyfikujesz mapowanie sieci z regionu 1 tooregion-2, upewnij się, że zmodyfikować mapowania sieci powitania od regionu 2 tooregion-1 również.</span><span class="sxs-lookup"><span data-stu-id="e12d2-128">If you modify a network mapping from region-1 tooregion-2, make sure you modify hello network mapping from region-2 tooregion-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="e12d2-129">Wybór podsieci</span><span class="sxs-lookup"><span data-stu-id="e12d2-129">Subnet selection</span></span>
<span data-ttu-id="e12d2-130">Podsieci hello docelowej maszyny wirtualnej jest zaznaczone, na podstawie nazwy hello podsieci hello hello źródłowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e12d2-130">Subnet of hello target virtual machine is selected based on hello name of hello subnet of hello source virtual machine.</span></span> <span data-ttu-id="e12d2-131">Jeśli podsieć hello takie same nazwy co hello źródłowej maszyny wirtualnej dostępne w sieci docelowej hello, który jest wybrany dla hello docelowej maszyny wirtualnej, a następnie.</span><span class="sxs-lookup"><span data-stu-id="e12d2-131">If there is a subnet of hello same name as that of hello source virtual machine available in hello target network, then that is chosen for hello target virtual machine.</span></span> <span data-ttu-id="e12d2-132">Jeśli podsieć o hello sam nazw w sieci docelowej hello, następnie alfabetycznie pierwszej podsieci jest wybrana jako hello docelowej podsieci.</span><span class="sxs-lookup"><span data-stu-id="e12d2-132">If there is no subnet with hello same name in hello target network, then alphabetically first subnet is chosen as hello target subnet.</span></span> <span data-ttu-id="e12d2-133">Można zmodyfikować tej podsieci, przechodząc tooCompute i ustawień sieci maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="e12d2-133">You can modify this subnet by going tooCompute and Network settings of hello virtual machine.</span></span>

![Modyfikowanie podsieci](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="e12d2-135">Adres IP</span><span class="sxs-lookup"><span data-stu-id="e12d2-135">IP address</span></span>

<span data-ttu-id="e12d2-136">Adres IP dla każdego interfejsu sieci hello hello docelowej maszyny wirtualnej jest wybierany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e12d2-136">IP address for each of hello network interface of hello target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="e12d2-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="e12d2-137">DHCP</span></span>
<span data-ttu-id="e12d2-138">Jeśli interfejs sieciowy hello hello źródłowej maszyny wirtualnej jest używany serwer DHCP, interfejs sieciowy hello docelowej maszyny wirtualnej jest również ustawić jako DHCP.</span><span class="sxs-lookup"><span data-stu-id="e12d2-138">If hello network interface of hello source virtual machine is using DHCP, then network interface of hello target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="e12d2-139">Statyczny adres IP</span><span class="sxs-lookup"><span data-stu-id="e12d2-139">Static IP</span></span>
<span data-ttu-id="e12d2-140">Interfejs sieciowy hello hello źródłowej maszyny wirtualnej używa statycznego adresu IP, następnie interfejsu sieci docelowej maszyny wirtualnej hello jest również ustawić toouse statycznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="e12d2-140">If hello network interface of hello source virtual machine is using Static IP, then network interface of hello target virtual machine is also set toouse Static IP.</span></span> <span data-ttu-id="e12d2-141">Statyczny adres IP jest wybierany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e12d2-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="e12d2-142">Tą samą przestrzenią adresów</span><span class="sxs-lookup"><span data-stu-id="e12d2-142">Same address space</span></span>

<span data-ttu-id="e12d2-143">Jeśli podsieć źródła hello i hello docelowej podsieci hello sam przestrzeni adresów, docelowy adres IP jest ustawić taki sam jak hello IP interfejsu sieci hello hello źródłowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e12d2-143">If hello source subnet and hello target subnet have hello same address space, then target IP is set same as hello IP of  hello network interface of hello source virtual machine.</span></span> <span data-ttu-id="e12d2-144">Jeśli nie ma tego samego adresu IP, dostępne IP jest ustawiony jako hello docelowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="e12d2-144">If same IP is not available, then some other available IP is set as hello target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="e12d2-145">Przestrzeń adresowa różnych</span><span class="sxs-lookup"><span data-stu-id="e12d2-145">Different address space</span></span>

<span data-ttu-id="e12d2-146">Jeśli podsieć źródła hello i hello docelowej podsieci ma inny adres miejsca, docelowy adres IP jest ustawiony jako dostępny adres IP w podsieci docelowej hello.</span><span class="sxs-lookup"><span data-stu-id="e12d2-146">If hello source subnet and hello target subnet have different address space, then target IP is set as any available IP in hello target subnet.</span></span>

<span data-ttu-id="e12d2-147">Można zmodyfikować hello docelowy adres IP dla każdego interfejsu sieciowego, przechodząc tooCompute i ustawień sieci maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="e12d2-147">You can modify hello target IP on each network interface by going tooCompute and Network settings of hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e12d2-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e12d2-148">Next steps</span></span>

- <span data-ttu-id="e12d2-149">Dowiedz się więcej o [wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure networking](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="e12d2-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
