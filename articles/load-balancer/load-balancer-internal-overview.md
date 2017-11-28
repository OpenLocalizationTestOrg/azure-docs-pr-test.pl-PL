---
title: "Moduł równoważenia obciążenia aaaInternal omówienie | Dokumentacja firmy Microsoft"
description: "Omówienie dla wewnętrznego modułu równoważenia obciążenia i ich funkcje. Jak działa moduł równoważenia obciążenia dla platformy Azure i możliwe scenariusze tooconfigure wewnętrznych punktów końcowych"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="93697-103">Omówienie usługi równoważenia obciążenia wewnętrznego</span><span class="sxs-lookup"><span data-stu-id="93697-103">Internal load balancer overview</span></span>

<span data-ttu-id="93697-104">W odróżnieniu od hello Internet równoważenia obciążenia hello wewnętrznego modułu równoważenia obciążenia (ILB) określa, że ruch tooresources tylko wewnątrz usługi w chmurze hello lub przy użyciu sieci VPN tooaccess hello infrastruktury platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="93697-104">Unlike hello Internet facing load balancer, hello internal load balancer (ILB) directs traffic only tooresources inside hello cloud service or using VPN tooaccess hello Azure infrastructure.</span></span> <span data-ttu-id="93697-105">Hello infrastruktury ogranicza dostęp toohello ze zrównoważonym obciążeniem wirtualnych adresów IP (VIP) usługi w chmurze lub sieć wirtualną tak, aby nigdy nie będą punktu końcowego Internet tooan bezpośrednio uwidocznione.</span><span class="sxs-lookup"><span data-stu-id="93697-105">hello infrastructure restricts access toohello load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed tooan Internet endpoint.</span></span> <span data-ttu-id="93697-106">To umożliwia wewnętrzny wiersz toorun aplikacje biznesowe (LOB) na platformie Azure i są dostępne z chmury hello lub z zasobami lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="93697-106">This enables internal line of business (LOB) applications toorun in Azure and be accessed from within hello cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="93697-107">Dlaczego może być konieczne wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="93697-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="93697-108">Azure wewnętrzny załadować równoważenia (ILB) zapewnia zrównoważenia obciążenia między maszyn wirtualnych, które znajdują się wewnątrz usługi w chmurze lub sieci wirtualnej z zakresu regionalnego.</span><span class="sxs-lookup"><span data-stu-id="93697-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="93697-109">Informacje o konfiguracji sieci wirtualnych z zakresu regionalnego i użyj hello, zobacz [regionalnych sieci wirtualnych](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) w hello Azure blog.</span><span class="sxs-lookup"><span data-stu-id="93697-109">For information about hello use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure blog.</span></span> <span data-ttu-id="93697-110">Modułu ILB nie można zastosować w istniejących sieciach wirtualnych, które zostały skonfigurowane przy użyciu grupy koligacji.</span><span class="sxs-lookup"><span data-stu-id="93697-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="93697-111">ILB umożliwia hello następujące typy równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="93697-111">ILB enables hello following types of load balancing:</span></span>

* <span data-ttu-id="93697-112">W ramach usługi w chmurze z maszyny wirtualnej zestawu tooa maszyn wirtualnych, które znajdują się w obrębie hello sama usługa w chmurze (zobacz rysunek 1).</span><span class="sxs-lookup"><span data-stu-id="93697-112">Within a cloud service, from virtual machines tooa set of virtual machines that reside within hello same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="93697-113">W ramach sieci wirtualnej, z maszyn wirtualnych w zestawie tooa sieci wirtualnej hello maszyn wirtualnych, które znajdują się w obrębie hello sama usługa w chmurze z hello wirtualnych sieci (patrz rysunek 2).</span><span class="sxs-lookup"><span data-stu-id="93697-113">Within a virtual network, from virtual machines in hello virtual network tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 2).</span></span>
* <span data-ttu-id="93697-114">Dla sieci wirtualnej między lokalizacjami, z zestawu tooa komputerów lokalnych maszyn wirtualnych, które znajdują się w obrębie hello sama usługa w chmurze z hello wirtualnych sieci (patrz rysunek 3).</span><span class="sxs-lookup"><span data-stu-id="93697-114">For a cross-premises virtual network, from on-premises computers tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 3).</span></span>
* <span data-ttu-id="93697-115">Internetowy, wielowarstwowych aplikacji, w których hello zaplecza warstw nie są skierowane do Internetu, ale wymagają równoważenia obciążenia dla ruchu z hello internetowy warstwy.</span><span class="sxs-lookup"><span data-stu-id="93697-115">Internet-facing, multi-tier applications in which hello back-end tiers are not Internet-facing but require load balancing for traffic from hello Internet-facing tier.</span></span>
* <span data-ttu-id="93697-116">Równoważenie obciążenia dla aplikacji biznesowych hostowane na platformie Azure, bez konieczności dodatkowego obciążenia równoważenia sprzętu lub oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="93697-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="93697-117">W tym na serwerach lokalnych w hello zestaw komputerów, których ruch jest obciążenia zrównoważone.</span><span class="sxs-lookup"><span data-stu-id="93697-117">Including on-premises servers in hello set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="93697-118">Aplikacje wielowarstwowe internetowy</span><span class="sxs-lookup"><span data-stu-id="93697-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="93697-119">Warstwa sieci web Hello ma Internet połączonej punktów końcowych dla klientów internetowych i jest częścią zestawu o zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="93697-119">hello web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="93697-120">Moduł równoważenia obciążenia Hello dystrybuuje ruch przychodzący z klientów w sieci web dla TCP port 443 (HTTPS) toohello serwerów sieci web.</span><span class="sxs-lookup"><span data-stu-id="93697-120">hello load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) toohello web servers.</span></span>

<span data-ttu-id="93697-121">serwery bazy danych Hello są za punktem końcowym ILB, której serwery sieci web hello jest używany przez Magazyn.</span><span class="sxs-lookup"><span data-stu-id="93697-121">hello database servers are behind an ILB endpoint which hello web servers use for storage.</span></span> <span data-ttu-id="93697-122">Punkt końcowy, których ruch jest równoważone między serwerami bazy danych hello hello ILB zestawu o zrównoważonym obciążeniu usługi tej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="93697-122">This database service load balanced endpoint, which traffic is load balanced across hello database servers in hello ILB set.</span></span>

<span data-ttu-id="93697-123">powitania po obraz pokazuje hello internetowy aplikację wielowarstwową w hello sama usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="93697-123">hello following image shows hello Internet facing multi-tier application within hello same cloud service.</span></span>

![Wewnętrzny usługą równoważenia obciążenia, jednej chmury](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="93697-125">Rysunek 1 — internetowy wielowarstwową aplikację</span><span class="sxs-lookup"><span data-stu-id="93697-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="93697-126">Inny możliwości zastosowania dla aplikacji wielowarstwowych jest gdy hello ILB wdrożony tooa innej usługi w chmurze, niż hello jednej odbierającą usługi hello na powitania ILB.</span><span class="sxs-lookup"><span data-stu-id="93697-126">Another possible use for a multi-tier application is when hello ILB deployed tooa different cloud service than hello one consuming hello service for hello ILB.</span></span>

<span data-ttu-id="93697-127">Chmura punktem końcowym ILB toohello dostęp do usług za pomocą hello będzie mieć tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="93697-127">Cloud services using hello same virtual network will have access toohello ILB endpoint.</span></span> <span data-ttu-id="93697-128">punktem końcowym ILB w hello hello powitania po pokazuje obrazu w innej usługi chmury z wewnętrznej bazy danych hello są serwery frontonu sieci web i przy użyciu tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="93697-128">hello following image shows front-end web servers are in a different cloud service from hello database back-end and using hello ILB endpoint within hello same virtual network.</span></span>

![Wewnętrzny zrównoważenia obciążenia między usługi w chmurze](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="93697-130">Rysunek 2 — serwery frontonu w innej usługi chmury</span><span class="sxs-lookup"><span data-stu-id="93697-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="93697-131">Intranet linii aplikacji biznesowych</span><span class="sxs-lookup"><span data-stu-id="93697-131">Intranet line of business applications</span></span>

<span data-ttu-id="93697-132">Ruch pochodzący od klientów w sieci lokalnej hello Pobierz równoważeniem obciążenia na powitania zestawu serwerów LOB przy użyciu sieci tooAzure połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="93697-132">Traffic from clients on hello on-premises network get load-balanced across hello set of LOB servers using VPN connection tooAzure network.</span></span>

<span data-ttu-id="93697-133">Maszyna klienta Hello będzie mieć dostęp do adresu IP tooan z usługi sieci VPN platformy Azure przy użyciu sieci VPN toosite punktu.</span><span class="sxs-lookup"><span data-stu-id="93697-133">hello client machine will have access tooan IP address from Azure VPN service using point toosite VPN.</span></span> <span data-ttu-id="93697-134">Umożliwia on hello hello użycia aplikacji LOB hostowanej za punktem końcowym ILB hello.</span><span class="sxs-lookup"><span data-stu-id="93697-134">It allows hello use hello LOB application hosted behind hello ILB endpoint.</span></span>

![Wewnętrzne równoważenie, przy użyciu sieci VPN toosite punktu obciążenia](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="93697-136">Rysunek 3 - aplikacji biznesowych przez punkt końcowy hello równoważeniem obciążenia</span><span class="sxs-lookup"><span data-stu-id="93697-136">Figure 3 - LOB applications hosted behind hello LB endpoint</span></span>

<span data-ttu-id="93697-137">Inny scenariusz hello LOB jest toohave witryny toosite VPN toohello sieci wirtualnej którym punktem końcowym ILB hello jest skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="93697-137">Another scenario for hello LOB is toohave a site toosite VPN toohello virtual network where hello ILB endpoint is configured.</span></span> <span data-ttu-id="93697-138">Dzięki temu końcowym ILB toohello toobe kierowany ruch sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="93697-138">This allows on-premises network traffic toobe routed toohello ILB endpoint.</span></span>

![Obciążenia wewnętrznego równoważenia przy użyciu witryny toosite sieci VPN](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="93697-140">Rysunek 4 - ruchu w sieci lokalnej kierowane punktem końcowym ILB toohello</span><span class="sxs-lookup"><span data-stu-id="93697-140">Figure 4 - On-premises network traffic routed toohello ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="93697-141">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="93697-141">Limitations</span></span>

<span data-ttu-id="93697-142">Wewnętrzny moduł równoważenia obciążenia konfiguracje nie obsługują SNAT.</span><span class="sxs-lookup"><span data-stu-id="93697-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="93697-143">W kontekście hello tego dokumentu SNAT odnosi się translatora adresów sieciowych źródła tooport Zamaskowana.</span><span class="sxs-lookup"><span data-stu-id="93697-143">In hello context of this document, SNAT refers tooport masquerading source  network address translation.</span></span>  <span data-ttu-id="93697-144">Dotyczy to tooscenarios których maszyn wirtualnych w puli usługi równoważenia obciążenia wymaga adresu IP frontonu tooreach hello odpowiednich wewnętrzny moduł równoważenia obciążenia firmy.</span><span class="sxs-lookup"><span data-stu-id="93697-144">This applies tooscenarios where a VM in a load balancer pool needs tooreach hello respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="93697-145">W tym scenariuszu nie jest obsługiwana dla wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="93697-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="93697-146">Wystąpią błędy połączenia, gdy przepływ hello jest równoważone toohello maszyny Wirtualnej, które pochodzą hello przepływu.</span><span class="sxs-lookup"><span data-stu-id="93697-146">Connection failures will occur when hello flow is load balanced toohello VM which originated hello flow.</span></span> <span data-ttu-id="93697-147">Należy użyć modułu równoważenia obciążenia styl serwera proxy dla takich scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="93697-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93697-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="93697-148">Next Steps</span></span>

[<span data-ttu-id="93697-149">Pomocy technicznej platformy Azure Resource Manager dla usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="93697-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="93697-150">Przed rozpoczęciem konfigurowania internetowy modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="93697-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="93697-151">Przed rozpoczęciem konfigurowania wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="93697-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

<span data-ttu-id="93697-152">[Configure a Load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="93697-152">[Configure a Load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="93697-153">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="93697-153">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
