---
title: Plan sieci dla VMware do platformy Azure replikacji | Dokumentacja firmy Microsoft
description: W tym artykule opisano planowanie wymagane sieci podczas replikowania maszyn wirtualnych VMware do platformy Azure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5578a0b4-0352-41c3-9cce-56beb17a4d97
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f164ac68ba6ec650bb3996b4aa870e1b98533a23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="step-4-plan-networking-for-vmware-to-azure-replication"></a><span data-ttu-id="dbaa8-103">Krok 4: Planowanie sieci dla VMware do platformy Azure replikacji</span><span class="sxs-lookup"><span data-stu-id="dbaa8-103">Step 4: Plan networking for VMware to Azure replication</span></span>

<span data-ttu-id="dbaa8-104">W tym artykule przedstawiono zagadnienia związane z planowaniem podczas replikowania lokalnych maszyn wirtualnych VMware do platformy Azure przy użyciu sieci [usługi Azure Site Recovery](site-recovery-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-104">This article summarizes network planning considerations when replicating on-premises VMware VMs to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="dbaa8-105">Wszelkie komentarze umieszczaj pod tym artykułem lub zadawaj pytania na [Forum usług Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="dbaa8-105">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connect-to-replica-vms"></a><span data-ttu-id="dbaa8-106">Połącz się z repliką maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="dbaa8-106">Connect to replica VMs</span></span>

<span data-ttu-id="dbaa8-107">Podczas planowania strategii trybu failover i replikacji, na których, jedno z pytań klucza jest sposób nawiązywania połączenia z maszyną wirtualną Azure po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-107">When planning your replication and failover strategy, one of the key questions is how to connect to the Azure VM after failover.</span></span> <span data-ttu-id="dbaa8-108">Istnieje kilka opcji do wyboru podczas projektowania strategii sieci dla repliki maszyny wirtualne platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="dbaa8-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="dbaa8-109">**Użyj innego adresu IP**: można określić, aby użyć różnych zakresów adresów IP dla sieci maszyny Wirtualnej Azure zreplikowane.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-109">**Use different IP address**: You can select to use a different IP address range for the replicated Azure VM network.</span></span> <span data-ttu-id="dbaa8-110">W tym scenariuszu maszyny Wirtualnej pobiera nowego adresu IP po w tryb failover i aktualizowania DNS jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-110">In this scenario the VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="dbaa8-111">**Zachowaj tego samego adresu IP**: może chcesz użyć tego samego zakresu adresów IP jak w witrynie głównej lokalnymi dla sieci platformy Azure po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-111">**Retain same IP address**: You might want to use the same IP address range as that in your primary on-premises site, for the Azure network after failover.</span></span> <span data-ttu-id="dbaa8-112">Utrzymywanie tego samego adresu IP adresów upraszcza odzyskiwanie dzięki zmniejszeniu problemów dotyczących sieci po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-112">Keeping the same IP addresses simplifies the recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="dbaa8-113">Jednak jeśli przeprowadzasz replikację do platformy Azure, należy zaktualizować tras z nowej lokalizacji adresy IP po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-113">However, when you're replicating to Azure, you will need to update routes with the new location of the IP addresses after failover.</span></span> 


## <a name="retain-ip-addresses"></a><span data-ttu-id="dbaa8-114">Zachowaj adresów IP</span><span class="sxs-lookup"><span data-stu-id="dbaa8-114">Retain IP addresses</span></span>

<span data-ttu-id="dbaa8-115">Usługa Site Recovery zapewnia adresy możliwości, aby zachować stałego adresu IP podczas przechodzenie w tryb failover na platformie Azure, z trybu failover podsieci.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-115">Site Recovery provides the capability to retain fixed IP addresses when failing over to Azure, with a subnet failover.</span></span>

<span data-ttu-id="dbaa8-116">Tryb failover podsieci określonej podsieci jest obecny w lokacji 1 lub 2 lokacji, ale nigdy nie w obu lokacjach jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-116">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="dbaa8-117">Aby zachować przestrzeń adresów IP w przypadku trybu failover, można programowo Rozmieść infrastruktury router przenieść podsieci z jednej lokacji.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-117">In order to maintain the IP address space in the event of a failover, you programmatically arrange for the router infrastructure to move the subnets from one site to another.</span></span> <span data-ttu-id="dbaa8-118">Podczas pracy w trybie failover podsieci są przenoszone wraz z skojarzone chronionych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-118">During failover, the subnets move with the associated protected VMs.</span></span> <span data-ttu-id="dbaa8-119">Główną wadą jest, że w przypadku awarii, należy przenieść całej podsieci.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-119">The main drawback is that in the event of a failure, you have to move the whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="dbaa8-120">Przykład trybu failover</span><span class="sxs-lookup"><span data-stu-id="dbaa8-120">Failover example</span></span>

<span data-ttu-id="dbaa8-121">Oto przykład dla trybu failover na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-121">Let's look at an example for failover to Azure.</span></span>

- <span data-ttu-id="dbaa8-122">Firmy ficticious, banku Woodgrove ma infrastruktury lokalnej hosting aplikacji swoich biznesowych.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-122">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="dbaa8-123">Ich aplikacji dla urządzeń przenośnych znajdują się na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-123">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="dbaa8-124">Łączność między maszynami wirtualnymi banku Woodgrove na serwerach Azure i lokalnymi są udostępniane przez połączenie lokacja lokacja (VPN) między siecią lokalną krawędzi i sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-124">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between the on-premises edge network and the Azure virtual network.</span></span>
- <span data-ttu-id="dbaa8-125">Tej sieci VPN oznacza, że sieci wirtualnej firmy w usłudze Azure jest wyświetlany jako rozszerzenie sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-125">This VPN means that the company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="dbaa8-126">Woodgrove chce Użyj usługi Site Recovery, aby replikować obciążenia lokalnego do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-126">Woodgrove wants to use Site Recovery to replicate on-premises workloads to Azure.</span></span>
 - <span data-ttu-id="dbaa8-127">Woodgrove ma radzenia sobie z aplikacje i konfiguracje, które są zależne od stałe adresy IP, a w związku z tym konieczne zachowanie adresów IP dla swoich aplikacji po w tryb failover na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-127">Woodgrove has to deal with applications and configurations which depend on hard-coded IP addresses, and thus need to retain IP addresses for their applications after failover to Azure.</span></span>
 - <span data-ttu-id="dbaa8-128">Woodgrove ma przypisanych adresów IP z zakresu 172.16.1.0/24, 172.16.2.0/24 do jej zasobów, które działają na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-128">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 to its resources running in Azure.</span></span>


<span data-ttu-id="dbaa8-129">Dla Woodgrove można było do replikowania jego maszyn wirtualnych na platformie Azure przy zachowaniu adresy IP, tutaj firmy, co firma musi wykonać:</span><span class="sxs-lookup"><span data-stu-id="dbaa8-129">For Woodgrove to be able to replicate its VMS to Azure while retaining the IP addresses, here's what the company needs to do:</span></span>

1. <span data-ttu-id="dbaa8-130">Tworzenie sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-130">Create an Azure virtual network.</span></span> <span data-ttu-id="dbaa8-131">Rozszerzenie sieci lokalnej, należy tak, aby aplikacje działają w trybie Failover bezproblemowo.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-131">It should be an extension of the on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="dbaa8-132">Azure umożliwia dodanie połączenie sieci VPN typu lokacja lokacja, oprócz połączenie punkt lokacja sieci wirtualnych utworzonych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-132">Azure allows you to add site-to-site VPN connectivity, in addition to point-to-site connectivity to the virtual networks created in Azure.</span></span>
3. <span data-ttu-id="dbaa8-133">Podczas konfigurowania połączenia lokacja lokacja, w sieci platformy Azure może kierować ruchem do lokalizacji lokalnego (sieci lokalne) tylko wtedy, gdy zakres adresów IP jest inny niż zakres adresów lokalnych.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-133">When setting up the site-to-site connection, in the Azure network, you can route traffic to the on-premises location (local-network) only if the IP address range is different from the on-premises IP address range.</span></span>
    - <span data-ttu-id="dbaa8-134">Jest to spowodowane Azure nie obsługuje rozciągnięty podsieci.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-134">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="dbaa8-135">Jeśli masz podsieci 192.168.1.0/24 lokalnymi, nie można dodać 192.168.1.0/24 sieci lokalnej w sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-135">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in the Azure network.</span></span>
    - <span data-ttu-id="dbaa8-136">Oczekiwany jest Azure nie może ustalić, czy brak aktywnych maszyn wirtualnych w podsieci i że podsieć jest tworzony tylko odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-136">This is expected because Azure doesn’t know that there are no active VMs in the subnet, and that the subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="dbaa8-137">Aby można było poprawnie kierować ruchem sieciowym spoza sieci platformy Azure podsieci w sieci i sieci lokalnej nie może powodować konflikt.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-137">To be able to correctly route network traffic out of an Azure network the subnets in the network and the local-network mustn't conflict.</span></span>

![Przed podsieci trybu failover](./media/site-recovery-network-design/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="dbaa8-139">Przed trybu failover</span><span class="sxs-lookup"><span data-stu-id="dbaa8-139">Before failover</span></span>

1. <span data-ttu-id="dbaa8-140">Utwórz dodatkowe sieci (na przykład odzyskiwania).</span><span class="sxs-lookup"><span data-stu-id="dbaa8-140">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="dbaa8-141">To jest sieć w którego przejścia w tryb failover maszyny wirtualne są tworzone.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-141">This is the network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="dbaa8-142">Aby upewnić się, że adres IP dla maszyny Wirtualnej jest zachowywany po przejściu w tryb failover, we właściwościach maszyny Wirtualnej > **Konfiguruj**, należy określić ten sam adres IP, że maszyna wirtualna ma lokalnego i kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-142">To ensure that the IP address for a VM is retained after a failover, in the VM properties > **Configure**, specify the same IP address that the VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="dbaa8-143">Gdy maszyna wirtualna przeszła w tryb failover, usługi Azure Site Recovery przypisze podanego adresu IP do niego.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-143">When the VM is failed over, Azure Site Recovery will assign the provided IP address to it.</span></span>

    ![Właściwości sieci](./media/site-recovery-network-design/network-design8.png)

4. <span data-ttu-id="dbaa8-145">Po wyzwoleniu wyzwalacza i maszyn wirtualnych są tworzone na platformie Azure przy użyciu wymaganych adresu IP trybu failover możesz nawiązać połączenie przy użyciu sieci [sieci wirtualnej do sieci wirtualnej połączenia](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="dbaa8-145">After failover is trigger is triggered, and the VMs are created in Azure with the required IP address, you can connect to the network using a [Vnet to Vnet connection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="dbaa8-146">Ta akcja umożliwia pisanie skryptów.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-146">This action can be scripted.</span></span>
5. <span data-ttu-id="dbaa8-147">Trasy należy odpowiednio można zmodyfikować, aby odzwierciedlał tego 192.168.1.0/24 teraz zostały przeniesione do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-147">Routes need to be appropriately modified, to reflect that 192.168.1.0/24 has now moved to Azure.</span></span>

    ![Po podsieci w tryb failover](./media/site-recovery-network-design/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="dbaa8-149">Po pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="dbaa8-149">After failover</span></span>

<span data-ttu-id="dbaa8-150">Jeśli nie ma sieci platformy Azure, jak pokazano powyżej, można utworzyć połączenie VPN lokacja lokacja między lokacją główną a Azure, po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-150">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failover.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="dbaa8-151">Zmiana adresów IP</span><span class="sxs-lookup"><span data-stu-id="dbaa8-151">Change IP addresses</span></span>

<span data-ttu-id="dbaa8-152">To [wpis w blogu](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) wyjaśniono, jak skonfigurować infrastrukturę sieci Azure, gdy nie trzeba zachować adresy IP po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-152">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how to set up the Azure networking infrastructure when you don't need to retain IP addresses after failover.</span></span> <span data-ttu-id="dbaa8-153">Go rozpoczyna się od opisu aplikacji wygląda jak skonfigurować sieci lokalnej na platformie Azure i zawiera informacje o uruchamianiu przechodzenia w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="dbaa8-153">It starts with an application description, looks at how to set up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="dbaa8-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dbaa8-154">Next steps</span></span>

<span data-ttu-id="dbaa8-155">Przejdź do [krok 5: przygotowanie Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="dbaa8-155">Go to [Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>
