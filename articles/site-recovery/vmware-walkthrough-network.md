---
title: aaaPlan sieci do replikacji tooAzure VMware | Dokumentacja firmy Microsoft
description: "W tym artykule omówiono planowania wymagane podczas replikowania maszyn wirtualnych VMware tooAzure sieci"
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
ms.openlocfilehash: 2b4f385c768cc7f5e98abae0afb8258b00f3724f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-vmware-tooazure-replication"></a><span data-ttu-id="6a9fd-103">Krok 4: Planowanie sieci w przypadku replikacji maszyn wirtualnych VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="6a9fd-103">Step 4: Plan networking for VMware tooAzure replication</span></span>

<span data-ttu-id="6a9fd-104">Ten artykuł zawiera podsumowanie sieci — kwestie podczas replikowania lokalnych maszyn wirtualnych VMware tooAzure przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-104">This article summarizes network planning considerations when replicating on-premises VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="6a9fd-105">Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6a9fd-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connect-tooreplica-vms"></a><span data-ttu-id="6a9fd-106">Połącz tooreplica maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="6a9fd-106">Connect tooreplica VMs</span></span>

<span data-ttu-id="6a9fd-107">Podczas planowania strategii trybu failover i replikacji, na których należy jedno z pytań klucza hello jest sposób tooconnect toohello maszyny Wirtualnej Azure po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-107">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="6a9fd-108">Istnieje kilka opcji do wyboru podczas projektowania strategii sieci dla repliki maszyny wirtualne platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="6a9fd-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="6a9fd-109">**Użyj innego adresu IP**: można wybrać toouse różnych zakresów adresów IP dla hello replikowane sieci maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-109">**Use different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="6a9fd-110">W tym scenariuszu hello maszyny Wirtualnej pobiera nowego adresu IP po pracy awaryjnej i aktualizacji DNS jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-110">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="6a9fd-111">**Zachowaj tego samego adresu IP**: może być toouse hello tego samego zakresu adresów IP jak w witrynie głównej lokalnymi dla hello sieć platformy Azure po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-111">**Retain same IP address**: You might want toouse hello same IP address range as that in your primary on-premises site, for hello Azure network after failover.</span></span> <span data-ttu-id="6a9fd-112">Utrzymywanie hello upraszcza samych adresów IP odzyskiwania hello zmniejszając sieci problemy związane z po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-112">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="6a9fd-113">Jednak Jeśli replikujesz tooAzure należy tooupdate tras z nowej lokalizacji hello adresów IP hello po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-113">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span> 


## <a name="retain-ip-addresses"></a><span data-ttu-id="6a9fd-114">Zachowaj adresów IP</span><span class="sxs-lookup"><span data-stu-id="6a9fd-114">Retain IP addresses</span></span>

<span data-ttu-id="6a9fd-115">Usługa Site Recovery zapewnia adresy IP tooretain stałej możliwości hello przy awarii tooAzure z trybu failover podsieci.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-115">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>

<span data-ttu-id="6a9fd-116">Tryb failover podsieci określonej podsieci jest obecny w lokacji 1 lub 2 lokacji, ale nigdy nie w obu lokacjach jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-116">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="6a9fd-117">W kolejności toomaintain hello przestrzeń adresów IP w przypadku hello trybu failover można programowo Rozmieść hello podsieci hello toomove infrastruktury router z jedną tooanother lokacji.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-117">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="6a9fd-118">Podczas pracy awaryjnej Przenieś podsieci hello z hello skojarzone chronionych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-118">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="6a9fd-119">Główną wadą Hello jest w zdarzeniu hello awarii toomove hello całej podsieci.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-119">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="6a9fd-120">Przykład trybu failover</span><span class="sxs-lookup"><span data-stu-id="6a9fd-120">Failover example</span></span>

<span data-ttu-id="6a9fd-121">Oto przykład tooAzure trybu failover.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-121">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="6a9fd-122">Firmy ficticious, banku Woodgrove ma infrastruktury lokalnej hosting aplikacji swoich biznesowych.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-122">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="6a9fd-123">Ich aplikacji dla urządzeń przenośnych znajdują się na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-123">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="6a9fd-124">Łączność między maszynami wirtualnymi banku Woodgrove na serwerach Azure i lokalnymi są udostępniane przez połączenie lokacja lokacja (VPN) między siecią krawędzi lokalne powitania i hello sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-124">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="6a9fd-125">Oznacza to sieci VPN, że hello firmy sieci wirtualnej platformy Azure jest wyświetlany jako rozszerzenie sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-125">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="6a9fd-126">Woodgrove chce toouse usługi Site Recovery tooreplicate lokalnymi obciążeń tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-126">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="6a9fd-127">Woodgrove ma toodeal z aplikacje i konfiguracje, które są zależne od stałe adresy IP, a w związku z tym należy tooretain adresów IP dla swoich aplikacji po tooAzure pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-127">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="6a9fd-128">Woodgrove ma przypisanych adresów IP z zakresu 172.16.1.0/24, zasobów tooits 172.16.2.0/24 działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-128">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="6a9fd-129">Woodgrove toobe stanie tooreplicate adresy jego tooAzure maszyn wirtualnych podczas zachowywania hello IP w tym miejscu jest jakie firma hello wymaga toodo:</span><span class="sxs-lookup"><span data-stu-id="6a9fd-129">For Woodgrove toobe able tooreplicate its VMS tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="6a9fd-130">Tworzenie sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-130">Create an Azure virtual network.</span></span> <span data-ttu-id="6a9fd-131">Należy go rozszerzenie hello lokalnej sieci, dzięki czemu aplikacje mogą bezproblemowo awaryjnie.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-131">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="6a9fd-132">Azure umożliwia możesz tooadd lokacja lokacja łączność w sieci VPN, oprócz toopoint lokacja, łączność toohello sieci wirtualne utworzone na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-132">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="6a9fd-133">Podczas konfigurowania połączenia lokacja lokacja hello, w hello Azure sieci, można kierować ruchu toohello lokalnej lokalizacji (sieci lokalne) tylko wtedy, gdy zakres adresów IP hello różni się od zakresu adresów IP lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-133">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="6a9fd-134">Jest to spowodowane Azure nie obsługuje rozciągnięty podsieci.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-134">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="6a9fd-135">Dlatego masz podsieci 192.168.1.0/24 lokalnymi, nie można dodać 192.168.1.0/24 sieci lokalnej w hello sieć platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-135">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="6a9fd-136">Oczekiwany jest Azure nie może ustalić, czy brak aktywnych maszyn wirtualnych w podsieci hello i podsieci hello jest tworzony tylko odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-136">This is expected because Azure doesn’t know that there are no active VMs in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="6a9fd-137">Program toobe toocorrectly może kierować ruchem sieciowym poza podsieci hello sieć platformy Azure w sieci hello i sieci lokalnej hello nie może powodować konflikt.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-137">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![Przed podsieci trybu failover](./media/site-recovery-network-design/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="6a9fd-139">Przed trybu failover</span><span class="sxs-lookup"><span data-stu-id="6a9fd-139">Before failover</span></span>

1. <span data-ttu-id="6a9fd-140">Utwórz dodatkowe sieci (na przykład odzyskiwania).</span><span class="sxs-lookup"><span data-stu-id="6a9fd-140">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="6a9fd-141">Jest hello sieć w którego przejścia w tryb failover maszyny wirtualne są tworzone.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-141">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="6a9fd-142">tooensure, który hello adresu IP dla maszyny Wirtualnej jest zachowywane po przejściu w tryb failover, hello właściwości maszyny Wirtualnej > **Konfiguruj**, określ hello hello, że maszyna wirtualna ma lokalnego, a następnie kliknij przycisk adres IP tego samego **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-142">tooensure that hello IP address for a VM is retained after a failover, in hello VM properties > **Configure**, specify hello same IP address that hello VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="6a9fd-143">Gdy hello wirtualna przeszła w tryb failover, usługi Azure Site Recovery przypisze hello podane tooit adresów IP.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-143">When hello VM is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>

    ![Właściwości sieci](./media/site-recovery-network-design/network-design8.png)

4. <span data-ttu-id="6a9fd-145">Po wyzwoleniu wyzwalacza i hello maszyny wirtualne są tworzone na platformie Azure z adresem IP hello wymagane trybu failover można połączyć za pomocą sieci toohello [sieci wirtualnej tooVnet połączenia](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="6a9fd-145">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet connection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="6a9fd-146">Ta akcja umożliwia pisanie skryptów.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-146">This action can be scripted.</span></span>
5. <span data-ttu-id="6a9fd-147">Trasy należy zmodyfikować odpowiednio, toobe tooreflect tego 192.168.1.0/24 teraz przeniósł tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-147">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![Po podsieci w tryb failover](./media/site-recovery-network-design/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="6a9fd-149">Po pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="6a9fd-149">After failover</span></span>

<span data-ttu-id="6a9fd-150">Jeśli nie ma sieci platformy Azure, jak pokazano powyżej, można utworzyć połączenie VPN lokacja lokacja między lokacją główną a Azure, po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-150">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failover.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="6a9fd-151">Zmiana adresów IP</span><span class="sxs-lookup"><span data-stu-id="6a9fd-151">Change IP addresses</span></span>

<span data-ttu-id="6a9fd-152">To [wpis w blogu](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) wyjaśniono, jak adresy tooset się hello Azure infrastrukturę sieci, gdy tooretain IP nie jest konieczne po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-152">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="6a9fd-153">Go rozpoczyna się od opisu aplikacji wygląda w sposób tooset się sieci lokalnej i w systemie Azure i zawiera informacje o uruchamianiu przechodzenia w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="6a9fd-153">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="6a9fd-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a9fd-154">Next steps</span></span>

<span data-ttu-id="6a9fd-155">Przejdź do zbyt[krok 5: przygotowanie Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="6a9fd-155">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>
