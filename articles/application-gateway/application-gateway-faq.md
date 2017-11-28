---
title: "aaaFrequently zadawane pytania dotyczące usługi Azure Application Gateway | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera odpowiedzi toofrequently zadawane pytania dotyczące bramy aplikacji Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="2e682-103">Często zadawane pytania dotyczące bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="2e682-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="2e682-104">Ogólne</span><span class="sxs-lookup"><span data-stu-id="2e682-104">General</span></span>

<span data-ttu-id="2e682-105">**Q. Co to jest brama aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="2e682-106">Bramy aplikacji Azure jest kontrolera dostarczania aplikacji (ADC) jako usługa, oferty różne obciążenia warstwy 7 równoważenia możliwości dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="2e682-107">Zapewnia wysoką dostępność i skalowalność usługi, która jest w pełni zarządzana przez Azure.</span><span class="sxs-lookup"><span data-stu-id="2e682-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="2e682-108">**Q. Jakie funkcje obsługuje bramy aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="2e682-109">Brama aplikacji w obsługuje SSL Odciążanie i na końcu tooend SSL, Zapora aplikacji sieci Web, koligacji na podstawie plików cookie sesji, adres url na podstawie ścieżki routingu, wielu lokacji hosting i inne.</span><span class="sxs-lookup"><span data-stu-id="2e682-109">Application Gateway supports SSL offloading and end tooend SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="2e682-110">Aby uzyskać pełną listę obsługiwanych funkcji, odwiedź stronę [tooApplication wprowadzenie bramy](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2e682-110">For a full list of supported features, visit [Introduction tooApplication Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="2e682-111">**Q. Jaka jest różnica hello między bramą aplikacji i usługi równoważenia obciążenia Azure?**</span><span class="sxs-lookup"><span data-stu-id="2e682-111">**Q. What is hello difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="2e682-112">Brama aplikacji jest modułem równoważenia obciążenia warstwy 7, co oznacza, że w przypadku ruchu w sieci web tylko (WebSocket-HTTP/HTTPS).</span><span class="sxs-lookup"><span data-stu-id="2e682-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="2e682-113">Obsługuje ona możliwości, takie jak zakończenie protokołu SSL, koligacji na podstawie plików cookie sesji i okrężnego dla ruchu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="2e682-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="2e682-114">Moduł równoważenia obciążenia, załadowanie salda ruchu na poziomie warstwy 4 (TCP/UDP).</span><span class="sxs-lookup"><span data-stu-id="2e682-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="2e682-115">**Q. Jakie protokoły obsługuje bramy aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="2e682-116">Brama aplikacji w obsługuje HTTP, HTTPS i protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="2e682-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="2e682-117">**Q. Jakie zasoby są obsługiwane obecnie częścią puli wewnętrznej bazy danych?**</span><span class="sxs-lookup"><span data-stu-id="2e682-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="2e682-118">Pul zaplecza może składać się z kart sieciowych, zestawy skalowania maszyny wirtualnej, publiczne adresy IP, wewnętrzny adresów IP, w pełni kwalifikowaną nazwę (FQDN) i zapleczy wielodostępne takich jak aplikacje sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2e682-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="2e682-119">Brama aplikacji, elementy członkowskie puli wewnętrznej bazy danych nie są powiązane tooan zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="2e682-119">Application Gateway backend pool members are not tied tooan availability set.</span></span> <span data-ttu-id="2e682-120">Elementami członkowskimi pul zaplecza może być między klastrami i centrami danych, lub poza platformą Azure, jak długo mają połączenia IP.</span><span class="sxs-lookup"><span data-stu-id="2e682-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="2e682-121">**Q. Jakich regionach jest dostępna w hello usługi?**</span><span class="sxs-lookup"><span data-stu-id="2e682-121">**Q. What regions is hello service available in?**</span></span>

<span data-ttu-id="2e682-122">Brama aplikacji jest dostępna we wszystkich regionach Azure globalnego.</span><span class="sxs-lookup"><span data-stu-id="2e682-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="2e682-123">Jest również dostępna w [chińskiej wersji platformy Azure](https://www.azure.cn/) i [Azure dla instytucji rządowych](https://azure.microsoft.com/en-us/overview/clouds/government/)</span><span class="sxs-lookup"><span data-stu-id="2e682-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="2e682-124">**Q. Jest to dedykowane wdrożenia dla mojej subskrypcji lub jest on udostępniony przez klientów?**</span><span class="sxs-lookup"><span data-stu-id="2e682-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="2e682-125">Brama aplikacji jest dedykowany wdrażania w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e682-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="2e682-126">**Q. Jest HTTP -> obsługiwanych przekierowanie protokołu HTTPS**</span><span class="sxs-lookup"><span data-stu-id="2e682-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="2e682-127">Przekierowanie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2e682-127">Redirection is supported.</span></span> <span data-ttu-id="2e682-128">Odwiedź stronę [omówienie przekierowania aplikacji bramy](application-gateway-redirect-overview.md) toolearn więcej.</span><span class="sxs-lookup"><span data-stu-id="2e682-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn more.</span></span>

<span data-ttu-id="2e682-129">**Q. W jakiej kolejności odbiorników przetwarzania?**</span><span class="sxs-lookup"><span data-stu-id="2e682-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="2e682-130">Obiekty nasłuchujące są przetwarzane w kolejności hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="2e682-130">Listeners are processed in hello order they are shown.</span></span> <span data-ttu-id="2e682-131">Dlatego jeśli odbiornik podstawowe pasuje do przychodzącego żądania przetwarza je najpierw.</span><span class="sxs-lookup"><span data-stu-id="2e682-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="2e682-132">Odbiorniki obejmujący wiele lokacji należy skonfigurować przed ruchu tooensure odbiornika podstawowa jest kierowany toohello poprawne zaplecza.</span><span class="sxs-lookup"><span data-stu-id="2e682-132">Multi-site listeners should be configured before a basic listener tooensure traffic is routed toohello correct back-end.</span></span>

<span data-ttu-id="2e682-133">**Q. Gdzie znaleźć adresów IP i DNS bramy aplikacji**</span><span class="sxs-lookup"><span data-stu-id="2e682-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="2e682-134">Korzystając z publicznym adresem IP jako punktu końcowego, te informacje można znaleźć na powitania zasobu publicznego adresu IP lub na stronie Przegląd hello na powitania brama aplikacji w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="2e682-134">When using a public IP address as an endpoint, this information can be found on hello public IP address resource or on hello Overview page for hello Application Gateway in hello portal.</span></span> <span data-ttu-id="2e682-135">Dla adresów IP to można znaleźć na stronie Przegląd hello.</span><span class="sxs-lookup"><span data-stu-id="2e682-135">For internal IP addresses, this can be found on hello Overview page.</span></span>

<span data-ttu-id="2e682-136">**Q. Czy hello adres IP lub DNS zmienia się na okres istnienia hello hello bramy aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-136">**Q. Does hello IP or DNS change over hello lifetime of hello Application Gateway?**</span></span>

<span data-ttu-id="2e682-137">Witaj VIP można zmienić bramy hello jest zatrzymana i uruchomiona przez powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="2e682-137">hello VIP can change if hello gateway is stopped and started by hello customer.</span></span> <span data-ttu-id="2e682-138">nie zmienia DNS skojarzone z bramą aplikacji Hello cyklem hello hello bramy.</span><span class="sxs-lookup"><span data-stu-id="2e682-138">hello DNS associated with Application Gateway does not change over hello lifecycle of hello gateway.</span></span> <span data-ttu-id="2e682-139">Z tego powodu jest zalecane toouse aliasu CNAME, aby wskazywał adresu DNS toohello hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2e682-139">For this reason, it is recommended toouse a CNAME alias and point it toohello DNS address of hello Application Gateway.</span></span>

<span data-ttu-id="2e682-140">**Q. Brama aplikacji w obsługuje statyczny adres IP?**</span><span class="sxs-lookup"><span data-stu-id="2e682-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="2e682-141">Nie, bramy aplikacji nie obsługuje statyczne publiczne adresy IP, ale obsługuje statyczne wewnętrzne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="2e682-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="2e682-142">**Q. Brama aplikacji w obsługuje wiele publicznych adresów IP dla bramy hello?**</span><span class="sxs-lookup"><span data-stu-id="2e682-142">**Q. Does Application Gateway support multiple public IPs on hello gateway?**</span></span>

<span data-ttu-id="2e682-143">Dotyczy tylko jeden publiczny adres IP bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="2e682-144">**Q. Brama aplikacji w obsługuje x przekazywane dla nagłówków?**</span><span class="sxs-lookup"><span data-stu-id="2e682-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="2e682-145">Tak, bramy aplikacji wstawia x przekazywane do, x przekazywane — protokół i nagłówki x przekazywane — port do żądania hello przekazywane toohello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2e682-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into hello request forwarded toohello backend.</span></span> <span data-ttu-id="2e682-146">format Hello x przekazywane do nagłówka jest rozdzielana przecinkami lista IP:Port.</span><span class="sxs-lookup"><span data-stu-id="2e682-146">hello format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="2e682-147">Prawidłowe wartości x przekazywane proto Hello to http lub https.</span><span class="sxs-lookup"><span data-stu-id="2e682-147">hello valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="2e682-148">X-przekazywane — port Określa hello portu, na którym żądania hello na powitania bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-148">X-forwarded-port specifies hello port at which hello request reached at hello Application Gateway.</span></span>

<span data-ttu-id="2e682-149">**Q. Jak długo trwa toodeploy bramę aplikacji? Brama mojej aplikacji nadal działa podczas aktualizowana?**</span><span class="sxs-lookup"><span data-stu-id="2e682-149">**Q. How long does it take toodeploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="2e682-150">Nowe wdrożenia bramy aplikacji może potrwać too20 tooprovision minut.</span><span class="sxs-lookup"><span data-stu-id="2e682-150">New Application Gateway deployments can take up too20 minutes tooprovision.</span></span> <span data-ttu-id="2e682-151">Tooinstance zmiany rozmiaru/liczby nie są zakłócenie i bramy hello pozostaje aktywna w tym czasie.</span><span class="sxs-lookup"><span data-stu-id="2e682-151">Changes tooinstance size/count are not disruptive, and hello gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="2e682-152">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="2e682-152">Configuration</span></span>

<span data-ttu-id="2e682-153">**Q. Brama aplikacji zawsze wdrożonej w sieci wirtualnej?**</span><span class="sxs-lookup"><span data-stu-id="2e682-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="2e682-154">Tak, bramy aplikacji zawsze jest wdrażana w podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2e682-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="2e682-155">Ta podsieć może zawierać tylko bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="2e682-156">**Q. Brama aplikacji można rozmawiać tooinstances poza jego sieci wirtualnej?**</span><span class="sxs-lookup"><span data-stu-id="2e682-156">**Q. Can Application Gateway talk tooinstances outside its virtual network?**</span></span>

<span data-ttu-id="2e682-157">Brama aplikacji można rozmawiać tooinstances poza hello sieci wirtualnej jest tak długo, jak brak połączenia IP.</span><span class="sxs-lookup"><span data-stu-id="2e682-157">Application Gateway can talk tooinstances outside of hello virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="2e682-158">Jeśli planujesz toouse wymaga wewnętrznych adresów IP jako elementy członkowskie puli wewnętrznej bazy danych, a następnie go [sieci Wirtualnej komunikacji równorzędnej](../virtual-network/virtual-network-peering-overview.md) lub [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="2e682-158">If you plan toouse internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="2e682-159">**Q. Można wdrożyć niczego więcej w podsieci bramy aplikacji hello?**</span><span class="sxs-lookup"><span data-stu-id="2e682-159">**Q. Can I deploy anything else in hello Application Gateway subnet?**</span></span>

<span data-ttu-id="2e682-160">Nie, ale można wdrożyć inne bramy aplikacji w podsieci hello.</span><span class="sxs-lookup"><span data-stu-id="2e682-160">No, but you can deploy other application gateways in hello subnet.</span></span>

<span data-ttu-id="2e682-161">**Q. Sieciowe grupy zabezpieczeń są obsługiwane w podsieci bramy aplikacji hello?**</span><span class="sxs-lookup"><span data-stu-id="2e682-161">**Q. Are Network Security Groups supported on hello Application Gateway subnet?**</span></span>

<span data-ttu-id="2e682-162">Sieciowe grupy zabezpieczeń są obsługiwane w podsieci bramy aplikacji hello z hello następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="2e682-162">Network Security Groups are supported on hello Application Gateway subnet with hello following restrictions:</span></span>

* <span data-ttu-id="2e682-163">Wyjątki musi znajdować się w dla ruchu przychodzącego na porty 65503 65534 wewnętrznej bazy danych kondycji toowork poprawnie.</span><span class="sxs-lookup"><span data-stu-id="2e682-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health toowork correctly.</span></span>

* <span data-ttu-id="2e682-164">Wychodzące połączenie z Internetem nie mogą zostać zablokowane.</span><span class="sxs-lookup"><span data-stu-id="2e682-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="2e682-165">Wymagane jest zezwolenie ruch z hello znacznik AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="2e682-165">Traffic from hello AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="2e682-166">**Q. Jakie są limity hello na bramie aplikacji? Można zwiększyć te limity?**</span><span class="sxs-lookup"><span data-stu-id="2e682-166">**Q. What are hello limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="2e682-167">Odwiedź stronę [limitów bramy aplikacji](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limity.</span><span class="sxs-lookup"><span data-stu-id="2e682-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limits.</span></span>

<span data-ttu-id="2e682-168">**Q. Czy można użyć bramy aplikacji wewnętrznych i zewnętrznych ruchu równocześnie?**</span><span class="sxs-lookup"><span data-stu-id="2e682-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="2e682-169">Tak, Application Gateway obsługuje jeden adres IP wewnętrzny i jeden zewnętrznego adresu IP dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="2e682-170">**Q. Czy sieci wirtualnej komunikacji równorzędnej obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="2e682-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="2e682-171">Tak, w sieci wirtualnej komunikacji równorzędnej jest obsługiwany i jest przydatne w przypadku ruchu w innych sieciach wirtualnych równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="2e682-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="2e682-172">**Q. Serwery lokalne tooon można rozmawiać po nawiązaniu przez tunele ExpressRoute lub sieci VPN?**</span><span class="sxs-lookup"><span data-stu-id="2e682-172">**Q. Can I talk tooon-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="2e682-173">Tak, jak długo ruch jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="2e682-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="2e682-174">**Q. Czy można mieć jedną pulę zaplecza obsługujący wiele aplikacji w różnych portów**</span><span class="sxs-lookup"><span data-stu-id="2e682-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="2e682-175">Architektura usługi Micro jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="2e682-175">Micro service architecture is supported.</span></span> <span data-ttu-id="2e682-176">Będzie potrzebny wielu tooprobe skonfigurowane ustawienia http na różnych portów.</span><span class="sxs-lookup"><span data-stu-id="2e682-176">You would need multiple http settings configured tooprobe on different ports.</span></span>

<span data-ttu-id="2e682-177">**Q. Niestandardowe sond obsługują symboli wieloznacznych/regex na odpowiedź na żądanie danych?**</span><span class="sxs-lookup"><span data-stu-id="2e682-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="2e682-178">Niestandardowe sond nie obsługują symboli wieloznacznych i wyrażeń regularnych na dane odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2e682-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="2e682-179">**Q. Jak są przetwarzane reguły**</span><span class="sxs-lookup"><span data-stu-id="2e682-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="2e682-180">Reguły są przetwarzane w kolejności hello są skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="2e682-180">Rules are processed in hello order they are configured.</span></span> <span data-ttu-id="2e682-181">Zaleca się, że obejmujący wiele lokacji skonfigurowanych reguł przed podstawowych reguł tooreduce hello ryzyko, że ruch jest kierowane toohello nieodpowiednie wewnętrznej bazy danych jako hello podstawowe reguły będzie zgodny z ruchu na podstawie reguły obejmujący wiele lokacji toohello poprzedniego portu oceniane.</span><span class="sxs-lookup"><span data-stu-id="2e682-181">It is recommended that multi-site rules are configured before basic rules tooreduce hello chance that traffic is routed toohello inappropriate backend as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="2e682-182">**Q. Jak są przetwarzane reguły**</span><span class="sxs-lookup"><span data-stu-id="2e682-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="2e682-183">Reguły są przetwarzane w kolejności hello, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="2e682-183">Rules are processed in hello order they are created.</span></span> <span data-ttu-id="2e682-184">Zaleca się, że przed podstawowych reguł skonfigurowanych reguł obejmujący wiele lokacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="2e682-185">Konfigurując odbiorników obejmujący wiele lokacji najpierw, ta konfiguracja ogranicza hello prawdopodobieństwo, że ruch jest kierowany toohello nieodpowiednie wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2e682-185">By configuring multi-site listeners first, this configuration reduces hello chance that traffic is routed toohello inappropriate backend.</span></span> <span data-ttu-id="2e682-186">Ten problem routingu mogą występować hello podstawowe reguły spowoduje dopasowanie ruchu na podstawie reguły obejmujący wiele lokacji toohello poprzedniego portu oceniane.</span><span class="sxs-lookup"><span data-stu-id="2e682-186">This routing issue can occur as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="2e682-187">**Q. Co to oznaczającego hello hosta pola niestandardowe sond?**</span><span class="sxs-lookup"><span data-stu-id="2e682-187">**Q. What does hello Host field for custom probes signify?**</span></span>

<span data-ttu-id="2e682-188">Określa hello nazwa toosend hello sondy do hosta.</span><span class="sxs-lookup"><span data-stu-id="2e682-188">Host field specifies hello name toosend hello probe to.</span></span> <span data-ttu-id="2e682-189">Dotyczy tylko wtedy, gdy obejmujący wiele lokacji jest skonfigurowany dla bramy aplikacji, w przeciwnym razie użyj '127.0.0.1'.</span><span class="sxs-lookup"><span data-stu-id="2e682-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="2e682-190">Ta wartość jest inna niż nazwa hosta maszyny Wirtualnej i jest w formacie \<protokołu\>://\<hosta\>:\<portu\>\<ścieżki\>.</span><span class="sxs-lookup"><span data-stu-id="2e682-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="2e682-191">**Q. Czy mogę tooa dostępu bramy aplikacji dozwolonych kilku źródłowych adresów IP?**</span><span class="sxs-lookup"><span data-stu-id="2e682-191">**Q. Can I whitelist Application Gateway access tooa few source IPs?**</span></span>

<span data-ttu-id="2e682-192">W tym scenariuszu można zrobić za pomocą grup NSG podsieci bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="2e682-193">następujące ograniczenia Hello należy umieścić w podsieci hello hello wymienionych według priorytetu:</span><span class="sxs-lookup"><span data-stu-id="2e682-193">hello following restrictions should be put on hello subnet in hello listed order of priority:</span></span>

* <span data-ttu-id="2e682-194">Zezwalaj na ruch przychodzący z zakresu adresów IP/IP źródła.</span><span class="sxs-lookup"><span data-stu-id="2e682-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="2e682-195">Zezwalaj na przychodzące żądania z wszystkich źródeł tooports 65503 65534 dla [zaplecza kondycji komunikacji](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="2e682-195">Allow incoming requests from all sources tooports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="2e682-196">Zezwalaj na przychodzące sondy modułu równoważenia obciążenia Azure (znacznik AzureLoadBalancer) i ruch przychodzący sieci wirtualnych (znacznik VirtualNetwork) na powitania [NSG](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="2e682-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on hello [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="2e682-197">Blokuj wszystkie pozostałe ruch przychodzący z odmowy wszystkie reguły.</span><span class="sxs-lookup"><span data-stu-id="2e682-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="2e682-198">Zezwalaj na ruch wychodzący toohello internet dla wszystkich miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="2e682-198">Allow outbound traffic toohello internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="2e682-199">Wydajność</span><span class="sxs-lookup"><span data-stu-id="2e682-199">Performance</span></span>

<span data-ttu-id="2e682-200">**Q. Jak bramy aplikacji obsługuje wysoką dostępność i skalowalność?**</span><span class="sxs-lookup"><span data-stu-id="2e682-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="2e682-201">Brama aplikacji w obsługuje realizację scenariuszy wysokiej dostępności, jeśli masz co najmniej dwa wystąpienia wdrożone.</span><span class="sxs-lookup"><span data-stu-id="2e682-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="2e682-202">Azure rozdziela te wystąpienia wiele aktualizacji i odporność tooensure domen, że wszystkie wystąpienia nie kończyć się niepowodzeniem na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="2e682-202">Azure distributes these instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="2e682-203">Brama aplikacji w obsługuje skalowalność, dodając hello wiele wystąpień tego samego obciążenia hello tooshare bramy.</span><span class="sxs-lookup"><span data-stu-id="2e682-203">Application Gateway supports scalability by adding multiple instances of hello same gateway tooshare hello load.</span></span>

<span data-ttu-id="2e682-204">**Q. Jak uzyskać scenariusza odzyskiwania po awarii między centrami danych z bramą aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="2e682-205">Klienci mogą użyć Menedżera ruchu toodistribute ruchu między wiele bram aplikacji w różnych centrach danych.</span><span class="sxs-lookup"><span data-stu-id="2e682-205">Customers can use Traffic Manager toodistribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="2e682-206">**Q. Czy automatyczne skalowanie obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="2e682-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="2e682-207">Nie, ale brama aplikacji ma Metryka przepływności, które mogą być używane tooalert należy po osiągnięciu progu.</span><span class="sxs-lookup"><span data-stu-id="2e682-207">No, but Application Gateway has a throughput metric that can be used tooalert you when a threshold is reached.</span></span> <span data-ttu-id="2e682-208">Ręcznie Dodawanie wystąpień lub zmiana rozmiaru nie jest ponownie uruchamiany hello bramy i nie ma wpływu na istniejące ruchu.</span><span class="sxs-lookup"><span data-stu-id="2e682-208">Manually adding instances or changing size does not restart hello gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="2e682-209">**Q. Czy ręczne skalowania w górę/dół Przyczyna Przestój?**</span><span class="sxs-lookup"><span data-stu-id="2e682-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="2e682-210">Nie istnieje bez przestojów, wystąpienia są rozproszone na uaktualnienia domen i domen błędów.</span><span class="sxs-lookup"><span data-stu-id="2e682-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="2e682-211">**Q. Czy można zmienić rozmiar wystąpienia z średnia toolarge bez zakłóceń**</span><span class="sxs-lookup"><span data-stu-id="2e682-211">**Q. Can I change instance size from medium toolarge without disruption?**</span></span>

<span data-ttu-id="2e682-212">Tak, Azure rozdziela wystąpień wiele aktualizacji i odporność tooensure domen, że wszystkie wystąpienia nie kończyć się niepowodzeniem na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="2e682-212">Yes, Azure distributes instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="2e682-213">Aplikacja obsługuje bramy skalowania, dodając wiele wystąpień hello tej samej bramy tooshare hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="2e682-213">Application Gateway supports scaling by adding multiple instances of hello same gateway tooshare hello load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="2e682-214">Konfiguracja protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="2e682-214">SSL Configuration</span></span>

<span data-ttu-id="2e682-215">**Q. Jakie certyfikaty są obsługiwane w bramie aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="2e682-216">Z podpisem własnym certyfikatami, certyfikaty urzędu certyfikacji i certyfikatów — symbol wieloznaczny są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2e682-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="2e682-217">Weryfikacją certyfikaty nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2e682-217">EV certs are not supported.</span></span>

<span data-ttu-id="2e682-218">**Q. Co to są hello bieżącego mechanizmów szyfrowania obsługiwanych przez bramę aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-218">**Q. What are hello current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="2e682-219">Oto Hello hello bieżącego mechanizmów szyfrowania obsługiwanych przez bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-219">hello following are hello current cipher suites supported by application gateway.</span></span> <span data-ttu-id="2e682-220">Odwiedź stronę: [Konfigurowanie SSL wersji zasad i mechanizmów szyfrowania w bramie aplikacji](application-gateway-configure-ssl-policy-powershell.md) toolearn jak toocustomize opcje protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="2e682-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn how toocustomize SSL options.</span></span>

- <span data-ttu-id="2e682-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="2e682-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="2e682-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="2e682-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="2e682-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="2e682-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="2e682-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="2e682-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="2e682-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="2e682-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="2e682-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="2e682-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="2e682-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="2e682-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="2e682-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="2e682-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="2e682-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="2e682-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="2e682-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="2e682-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="2e682-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="2e682-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="2e682-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="2e682-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="2e682-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="2e682-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="2e682-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="2e682-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="2e682-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="2e682-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="2e682-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="2e682-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="2e682-247">**Q. Brama aplikacji w również obsługuje ponownego szyfrowania ruchu toohello wewnętrznej bazy danych?**</span><span class="sxs-lookup"><span data-stu-id="2e682-247">**Q. Does Application Gateway also support re-encryption of traffic toohello backend?**</span></span>

<span data-ttu-id="2e682-248">Tak, Application Gateway obsługuje SSL odciążania i tooend końcowych SSL, który szyfruje ponownie hello ruchu toohello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2e682-248">Yes, Application Gateway supports SSL offload, and end tooend SSL, which re-encrypts hello traffic toohello backend.</span></span>

<span data-ttu-id="2e682-249">**Q. Można skonfigurować wersji protokołu SSL toocontrol zasad SSL?**</span><span class="sxs-lookup"><span data-stu-id="2e682-249">**Q. Can I configure SSL policy toocontrol SSL Protocol versions?**</span></span>

<span data-ttu-id="2e682-250">Tak, można skonfigurować bramy aplikacji toodeny TLS1.0, TLS1.1 i TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="2e682-250">Yes, you can configure Application Gateway toodeny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="2e682-251">Protokół SSL 2.0 i 3.0 już są domyślnie wyłączone i nie są konfigurowalne.</span><span class="sxs-lookup"><span data-stu-id="2e682-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="2e682-252">**Q. Można skonfigurować mechanizmów szyfrowania i kolejność zasad?**</span><span class="sxs-lookup"><span data-stu-id="2e682-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="2e682-253">Tak, [konfiguracji mechanizmów szyfrowania](application-gateway-ssl-policy-overview.md) jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="2e682-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="2e682-254">Podczas definiowania zasad niestandardowych, należy włączyć co najmniej jeden z hello następujące mechanizmy szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="2e682-254">When defining a custom policy, at least one of hello following cipher suites must be enabled.</span></span> <span data-ttu-id="2e682-255">Brama aplikacji w używa SHA256 toofor wewnętrznej bazy danych zarządzania.</span><span class="sxs-lookup"><span data-stu-id="2e682-255">Application gateway uses SHA256 toofor backend management.</span></span>

* <span data-ttu-id="2e682-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="2e682-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="2e682-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="2e682-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="2e682-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="2e682-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="2e682-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="2e682-262">**Q. Jak wiele certyfikatów SSL są obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="2e682-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="2e682-263">Zapasowej too20 SSL certyfikaty są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2e682-263">Up too20 SSL certificates are supported.</span></span>

<span data-ttu-id="2e682-264">**Q. Jak wiele certyfikatów uwierzytelniania w celu ponownego szyfrowania wewnętrznej bazy danych są obsługiwane?**</span><span class="sxs-lookup"><span data-stu-id="2e682-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="2e682-265">Zapasowej too10 certyfikatów uwierzytelniania są obsługiwane z domyślną 5.</span><span class="sxs-lookup"><span data-stu-id="2e682-265">Up too10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="2e682-266">**Q. Czy brama aplikacji można zintegrować z usługą Azure Key Vault natywnie?**</span><span class="sxs-lookup"><span data-stu-id="2e682-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="2e682-267">Nie, nie jest zintegrowany z usługą Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="2e682-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="2e682-268">Konfiguracja zapory (WAF) dla aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="2e682-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="2e682-269">**Q. Witaj SKU zapory aplikacji sieci Web oferuje wszystkie funkcje hello dostępne hello standardowy SKU?**</span><span class="sxs-lookup"><span data-stu-id="2e682-269">**Q. Does hello WAF SKU offer all hello features available with hello Standard SKU?**</span></span>

<span data-ttu-id="2e682-270">Tak, zapory aplikacji sieci Web obsługuje wszystkie funkcje hello hello standardowy SKU.</span><span class="sxs-lookup"><span data-stu-id="2e682-270">Yes, WAF supports all hello features in hello Standard SKU.</span></span>

<span data-ttu-id="2e682-271">**Q. Co to jest hello CRS wersji, która obsługuje bramy aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-271">**Q. What is hello CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="2e682-272">Brama aplikacji w obsługuje znaki CR [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) i CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="2e682-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="2e682-273">**Q. Jak monitorować zapory aplikacji sieci Web?**</span><span class="sxs-lookup"><span data-stu-id="2e682-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="2e682-274">Zapory aplikacji sieci Web jest monitorowany za pośrednictwem rejestrowania diagnostycznego, więcej informacji na temat rejestrowania diagnostycznego można znaleźć w folderze [rejestrowania diagnostyki i metryki bramy aplikacji](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="2e682-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="2e682-275">**Q. Tryb wykrywania blokowania ruchu?**</span><span class="sxs-lookup"><span data-stu-id="2e682-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="2e682-276">Nie, Tryb wykrywania rejestruje tylko ruch, który jest wyzwalana reguła zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2e682-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="2e682-277">**Q. Jak dostosować reguły zapory aplikacji sieci Web?**</span><span class="sxs-lookup"><span data-stu-id="2e682-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="2e682-278">Tak, można dostosowywać, aby uzyskać więcej informacji na jak toocustomize ich odwiedź są reguły zapory aplikacji sieci Web [grup reguł zapory aplikacji sieci Web dostosować i reguł](application-gateway-customize-waf-rules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2e682-278">Yes, WAF rules are customizable, for more information on how toocustomize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="2e682-279">**Q. Jakie reguły są obecnie dostępne?**</span><span class="sxs-lookup"><span data-stu-id="2e682-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="2e682-280">Zapory aplikacji sieci Web obsługuje obecnie CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) i [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), które zapewniają planu bazowego zabezpieczeń przed większość hello 10 pierwszych luk w zabezpieczeniach przez hello Otwórz sieci Web aplikacji zabezpieczeń projektu (OWASP) znaleźć tutaj [OWASP pierwszych 10 luk w zabezpieczeniach](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="2e682-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of hello top 10 vulnerabilities identified by hello Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="2e682-281">Ochrona przed atakami polegającymi na iniekcji SQL</span><span class="sxs-lookup"><span data-stu-id="2e682-281">SQL injection protection</span></span>

* <span data-ttu-id="2e682-282">Ochrona przed atakami z użyciem skryptów wykorzystywanych w obrębie wielu witryn</span><span class="sxs-lookup"><span data-stu-id="2e682-282">Cross site scripting protection</span></span>

* <span data-ttu-id="2e682-283">Częste ataki w ramach sieci Web polegające na iniekcji poleceń, przemycaniu żądań HTTP, rozdzielaniu odpowiedzi HTTP i zdalnym dołączaniu plików</span><span class="sxs-lookup"><span data-stu-id="2e682-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="2e682-284">Ochrona przed naruszeniami protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="2e682-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="2e682-285">Ochrona przed nieprawidłowościami protokołu HTTP, takimi jak brakujące powiązania agenta i użytkownika hosta oraz akceptowanie nagłówków</span><span class="sxs-lookup"><span data-stu-id="2e682-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="2e682-286">Zapobieganie atakom z użyciem robotów, przeszukiwarek i skanerów</span><span class="sxs-lookup"><span data-stu-id="2e682-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="2e682-287">Wykrycie typowych błędów konfiguracji aplikacji (czyli Apache usług IIS, itp.)</span><span class="sxs-lookup"><span data-stu-id="2e682-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="2e682-288">**Q. Czy zapory aplikacji sieci Web obsługuje również zapobiegania DDoS?**</span><span class="sxs-lookup"><span data-stu-id="2e682-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="2e682-289">Nie, zapory aplikacji sieci Web nie ma DDoS zapobiegania.</span><span class="sxs-lookup"><span data-stu-id="2e682-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="2e682-290">Rejestrowanie i Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="2e682-290">Diagnostics and Logging</span></span>

<span data-ttu-id="2e682-291">**Q. Jakie rodzaje dzienniki są dostępne z bramy aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="2e682-292">Istnieją trzy dzienniki dostępne dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="2e682-293">Aby uzyskać więcej informacji na te dzienniki i inne funkcje diagnostyczne, odwiedź stronę [zaplecza kondycji, dzienników diagnostyki i metryki bramy aplikacji](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="2e682-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="2e682-294">**ApplicationGatewayAccessLog** — dziennik dostępu hello zawiera każdego żądania przesłane toohello frontonu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-294">**ApplicationGatewayAccessLog** - hello access log contains each request submitted toohello Application Gateway frontend.</span></span> <span data-ttu-id="2e682-295">dane Hello obejmują wywołującego hello IP, adres URL żądanego, czas oczekiwania na odpowiedź, i wylogowywanie zwracają kod, bajtów. Dziennik dostępu są gromadzone co 300 sekund.</span><span class="sxs-lookup"><span data-stu-id="2e682-295">hello data includes hello caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="2e682-296">Ten dziennik zawiera jeden rekord dla każdego wystąpienia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="2e682-297">**ApplicationGatewayPerformanceLog** — dziennik wydajności hello przechwytuje informacje o wydajności dla poszczególnych wystąpień całkowita liczba żądań podawana, w tym przepływność w bajtach, całkowita liczba żądań obsłużonych, liczba nieudanych żądań, dobrej kondycji i złej kondycji Liczba wystąpień zaplecza.</span><span class="sxs-lookup"><span data-stu-id="2e682-297">**ApplicationGatewayPerformanceLog** - hello performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="2e682-298">**ApplicationGatewayFirewallLog** — dziennik zapory hello zawiera żądań, które są rejestrowane za pomocą wykrywania i zapobiegania tryb bramę aplikacji, który jest skonfigurowany z zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="2e682-298">**ApplicationGatewayFirewallLog** - hello firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="2e682-299">**Q. Jak sprawdzić, czy Moje elementy członkowskie puli zaplecza są w dobrej kondycji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="2e682-300">Można użyć polecenia cmdlet programu PowerShell hello `Get-AzureRmApplicationGatewayBackendHealth` lub Sprawdź kondycję za pośrednictwem portalu hello odwiedzając [diagnostyki bramy aplikacji](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="2e682-300">You can use hello PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through hello portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="2e682-301">**Q. Co to jest hello zasady przechowywania dzienników diagnostycznych hello?**</span><span class="sxs-lookup"><span data-stu-id="2e682-301">**Q. What is hello retention policy on hello diagnostics logs?**</span></span>

<span data-ttu-id="2e682-302">Konto magazynu klientów toohello przepływu dzienniki diagnostyczne i klientów można ustawić zasad przechowywania hello na podstawie swoich preferencji.</span><span class="sxs-lookup"><span data-stu-id="2e682-302">Diagnostic logs flow toohello customers storage account and customers can set hello retention policy based on their preference.</span></span> <span data-ttu-id="2e682-303">Dzienniki diagnostyczne mogą być również wysyłane tooan Centrum zdarzeń lub analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="2e682-303">Diagnostic logs can also be sent tooan Event Hub or Log Analytics.</span></span> <span data-ttu-id="2e682-304">Odwiedź stronę [diagnostyki bramy aplikacji](application-gateway-diagnostics.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="2e682-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="2e682-305">**Q. Jak uzyskać dzienniki inspekcji dla bramy aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="2e682-306">Dzienniki inspekcji są dostępne dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e682-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="2e682-307">W portalu powitania kliknij **dziennik aktywności** w bloku menu hello dziennika inspekcji hello tooaccess Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="2e682-307">In hello portal, click **Activity Log** in hello menu blade of an Application Gateway tooaccess hello audit log.</span></span> 

<span data-ttu-id="2e682-308">**Q. Można ustawić alerty z bramy aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2e682-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="2e682-309">Tak, bramy aplikacji obsługi alertów, alerty są konfigurowane poza metryki.</span><span class="sxs-lookup"><span data-stu-id="2e682-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="2e682-310">Brama aplikacji w aktualnie ma metrykę "przepływności", który może być skonfigurowany tooalert.</span><span class="sxs-lookup"><span data-stu-id="2e682-310">Application Gateway currently has a metric of "throughput", which can be configured tooalert.</span></span> <span data-ttu-id="2e682-311">toolearn więcej informacji na temat alertów, odwiedź stronę [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="2e682-311">toolearn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="2e682-312">**Q. Kondycja wewnętrznej bazy danych zwraca nieznany stan, w poznaniu przyczyny tego stanu?**</span><span class="sxs-lookup"><span data-stu-id="2e682-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="2e682-313">Najczęstszą przyczyną Hello jest toohello dostępu do wewnętrznej bazy danych jest blokowana przez NSG lub niestandardowe DNS.</span><span class="sxs-lookup"><span data-stu-id="2e682-313">hello most common reason is access toohello backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="2e682-314">Odwiedź stronę [zaplecza kondycji, rejestrowanie danych diagnostycznych i metryki bramy aplikacji](application-gateway-diagnostics.md) toolearn więcej.</span><span class="sxs-lookup"><span data-stu-id="2e682-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e682-315">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2e682-315">Next Steps</span></span>

<span data-ttu-id="2e682-316">można znaleźć więcej informacji na temat bramy aplikacji toolearn [tooApplication wprowadzenie bramy](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e682-316">toolearn more about Application Gateway visit [Introduction tooApplication Gateway](application-gateway-introduction.md).</span></span>
