---
title: "Mapowanie sieci między dwóch regionach platformy Azure w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Usługa Azure Site Recovery koordynuje replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Więcej informacji na temat trybu failover do platformy Azure lub dodatkowego centrum danych."
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
ms.openlocfilehash: 9d6a806ec533259797080fbfee2c38f918ebd8a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="f9b6b-104">Mapowanie sieci między dwóch regionach platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f9b6b-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="f9b6b-105">W tym artykule opisano sposób mapowania sieci wirtualnych platformy Azure z dwóch regionach platformy Azure ze sobą.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-105">This article describes how to map Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="f9b6b-106">Mapowanie sieci zapewnia, że po utworzeniu maszyny wirtualnej zreplikowanej w docelowym regionie Azure jest tworzona na sieć wirtualną, która jest mapowana na sieć wirtualną dla źródłowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-106">Network mapping ensures that when replicated virtual machine is created in the target Azure region, it is created on the virtual network that is mapped to virtual network of the source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="f9b6b-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f9b6b-107">Prerequisites</span></span>
<span data-ttu-id="f9b6b-108">Przed zamapowaniem sieci upewnij się, utworzono [sieci wirtualnych platformy Azure](../virtual-network/virtual-networks-overview.md) zarówno źródłowych i docelowych regiony platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="f9b6b-109">Mapowanie sieci</span><span class="sxs-lookup"><span data-stu-id="f9b6b-109">Map networks</span></span>

<span data-ttu-id="f9b6b-110">Do innej sieci wirtualnej w innym regionie mapowania sieci wirtualnej platformy Azure, w jednym regionie Azure, przejdź do infrastruktura usługi Site Recovery -> Mapowanie sieci (maszyn wirtualnych platformy Azure) i utworzyć mapowania sieci.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-110">To map an Azure virtual network in one Azure region to another virtual network in another region, go to Site Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="f9b6b-112">W poniższym przykładzie Moja maszyna wirtualna jest uruchomiona w regionie Azja Wschodnia i jest replikowana na Azja południowo-wschodnia.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-112">In the example below my virtual machine is running in East Asia region and is being replicated to Southeast Asia.</span></span>

<span data-ttu-id="f9b6b-113">Wybierz sieć źródłowa i docelowa, a następnie kliknij przycisk OK, aby utworzyć mapowanie sieci z Azja Wschodnia, Azja południowo-wschodnia.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-113">Select the source and target network and then click OK to create a network mapping from East Asia to Southeast Asia.</span></span>

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="f9b6b-115">Tak samo postąpić, aby utworzyć mapowanie sieci z Azja południowo-wschodnia, Azja Wschodnia.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-115">Do the same thing to create a network mapping from Southeast Asia to East Asia.</span></span>  
![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="f9b6b-117">Mapowanie sieci, podczas włączania replikacji</span><span class="sxs-lookup"><span data-stu-id="f9b6b-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="f9b6b-118">Jeśli nie zostanie zrobione mapowanie sieci, gdy maszyny wirtualnej w przypadku pierwszego czasu formularza jeden region platformy Azure jest replikowana do innego, można wybrać sieć docelowa w ramach tego samego procesu.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-118">If network mapping is not done when you are replicating a virtual machine for the first time form one Azure region to another, then you can choose target network as part of the same process.</span></span> <span data-ttu-id="f9b6b-119">Usługa Site Recovery tworzy mapowania sieci z regionu źródła na region docelowy i region docelowy do regionu źródła na podstawie tego zaznaczenia.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-119">Site Recovery creates network mappings from source region to target region and from target region to source region based on this selection.</span></span>   

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="f9b6b-121">Domyślnie usługa Site Recovery tworzy sieć w region docelowy, który jest identyczny z siecią źródła i dodając "— Funkcja automatycznego odzyskiwania systemu" jako sufiks nazwy źródłowej sieci.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-121">By default, Site Recovery creates a network in the target region that is identical to the source network and by adding '-asr' as a suffix to the name of the source network.</span></span> <span data-ttu-id="f9b6b-122">Możesz wybrać utworzone sieci, klikając przycisk Dostosuj.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-122">You can choose an already created network by clicking Customize.</span></span>

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="f9b6b-124">Jeśli mapowanie sieci zostało już przeprowadzone, nie można zmienić wirtualnej sieci docelowej podczas włączania replikacji.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-124">If the network mapping is already done, you can't change the target virtual network while enabling replication.</span></span> <span data-ttu-id="f9b6b-125">Aby to zmienić, zmodyfikuj istniejące mapowanie sieci.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-125">To change it, modify existing network mapping.</span></span>  

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mapowanie sieci](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="f9b6b-128">Jeśli zmodyfikujesz mapowanie sieci regionu-1 do 2 regionu, upewnij się, że zmodyfikować mapowania sieci z regionu 2 region-1, jak również.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-128">If you modify a network mapping from region-1 to region-2, make sure you modify the network mapping from region-2 to region-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="f9b6b-129">Wybór podsieci</span><span class="sxs-lookup"><span data-stu-id="f9b6b-129">Subnet selection</span></span>
<span data-ttu-id="f9b6b-130">Podsieci docelowej maszyny wirtualnej jest zaznaczone, na podstawie nazwy podsieci źródłowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-130">Subnet of the target virtual machine is selected based on the name of the subnet of the source virtual machine.</span></span> <span data-ttu-id="f9b6b-131">Jeśli jest dostępny w sieci docelowej podsieci o takiej samej nazwie jak źródłowej maszyny wirtualnej, następnie który jest wybrany dla docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-131">If there is a subnet of the same name as that of the source virtual machine available in the target network, then that is chosen for the target virtual machine.</span></span> <span data-ttu-id="f9b6b-132">Jeśli nie ma żadnych podsieci o takiej samej nazwie w sieci docelowej alfabetycznie pierwszej podsieci jest wybrany jako podsieci docelowej.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-132">If there is no subnet with the same name in the target network, then alphabetically first subnet is chosen as the target subnet.</span></span> <span data-ttu-id="f9b6b-133">Można zmodyfikować tej podsieci, przechodząc do obliczenia i sieć ustawienia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-133">You can modify this subnet by going to Compute and Network settings of the virtual machine.</span></span>

![Modyfikowanie podsieci](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="f9b6b-135">Adres IP</span><span class="sxs-lookup"><span data-stu-id="f9b6b-135">IP address</span></span>

<span data-ttu-id="f9b6b-136">Adres IP dla każdego interfejsu sieci docelowej maszyny wirtualnej jest wybierany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f9b6b-136">IP address for each of the network interface of the target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="f9b6b-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="f9b6b-137">DHCP</span></span>
<span data-ttu-id="f9b6b-138">Jeśli interfejs sieciowy źródłowej maszyny wirtualnej jest używany serwer DHCP, interfejsu sieci docelowej maszyny wirtualnej jest także ustawić jako DHCP.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-138">If the network interface of the source virtual machine is using DHCP, then network interface of the target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="f9b6b-139">Statyczny adres IP</span><span class="sxs-lookup"><span data-stu-id="f9b6b-139">Static IP</span></span>
<span data-ttu-id="f9b6b-140">Jeśli interfejs sieciowy źródłowej maszyny wirtualnej używa statycznego adresu IP, interfejsu sieci docelowej maszyny wirtualnej jest także ustawić do użycia statycznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-140">If the network interface of the source virtual machine is using Static IP, then network interface of the target virtual machine is also set to use Static IP.</span></span> <span data-ttu-id="f9b6b-141">Statyczny adres IP jest wybierany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f9b6b-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="f9b6b-142">Tą samą przestrzenią adresów</span><span class="sxs-lookup"><span data-stu-id="f9b6b-142">Same address space</span></span>

<span data-ttu-id="f9b6b-143">Jeśli podsieć źródłowej i docelowej podsieci z tą samą przestrzenią adresów, docelowy adres IP jest ustawić taki sam jak adres IP interfejsu sieciowego dla źródłowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-143">If the source subnet and the target subnet have the same address space, then target IP is set same as the IP of  the network interface of the source virtual machine.</span></span> <span data-ttu-id="f9b6b-144">Jeśli nie ma tego samego adresu IP, dostępne IP jest ustawiony jako docelowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-144">If same IP is not available, then some other available IP is set as the target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="f9b6b-145">Przestrzeń adresowa różnych</span><span class="sxs-lookup"><span data-stu-id="f9b6b-145">Different address space</span></span>

<span data-ttu-id="f9b6b-146">Jeśli na podsieci źródłowej i docelowej podsieci ma inny adres miejsca, docelowy adres IP jest ustawiony jako dostępny adres IP w podsieci docelowej.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-146">If the source subnet and the target subnet have different address space, then target IP is set as any available IP in the target subnet.</span></span>

<span data-ttu-id="f9b6b-147">Docelowy adres IP dla każdego interfejsu sieciowego można zmodyfikować, przechodząc do ustawień obliczania i sieci maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9b6b-147">You can modify the target IP on each network interface by going to Compute and Network settings of the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9b6b-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9b6b-148">Next steps</span></span>

- <span data-ttu-id="f9b6b-149">Dowiedz się więcej o [wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure networking](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="f9b6b-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
