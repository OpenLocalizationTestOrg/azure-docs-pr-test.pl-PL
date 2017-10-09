---
title: "aaaDMZ przykład — tworzenie DMZ tooprotect aplikacji z zaporą i grup NSG | Dokumentacja firmy Microsoft"
description: "Tworzenie DMZ z zaporą i grup zabezpieczeń sieci (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="88b4c-103">Przykład 2 — Tworzenie DMZ tooprotect aplikacji z zaporą i grupy NSG</span><span class="sxs-lookup"><span data-stu-id="88b4c-103">Example 2 – Build a DMZ tooprotect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="88b4c-104">[Zwraca toohello strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME]</span><span class="sxs-lookup"><span data-stu-id="88b4c-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="88b4c-105">W tym przykładzie utworzy strefą DMZ z zaporą, windows czterech serwerów i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="88b4c-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="88b4c-106">On również przeprowadzi każdego tooprovide odpowiednich poleceń hello głębsze zrozumienie każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="88b4c-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="88b4c-107">Istnieje również scenariusz ruchu sekcji tooprovide jako szczegółowe krok po kroku, jak ruchu obejmującego hello warstw zabezpieczeń w hello DMZ.</span><span class="sxs-lookup"><span data-stu-id="88b4c-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="88b4c-108">Na koniec w sekcji odwołań hello jest kompletny kod hello i toobuild instrukcji tego środowiska tootest i doświadczenia z różnych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="88b4c-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="88b4c-109">![Przychodzący DMZ NVA i grupy NSG][1]</span><span class="sxs-lookup"><span data-stu-id="88b4c-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="88b4c-110">Opis elementu środowiska</span><span class="sxs-lookup"><span data-stu-id="88b4c-110">Environment Description</span></span>
<span data-ttu-id="88b4c-111">W tym przykładzie jest subskrypcji, która zawiera następujące hello:</span><span class="sxs-lookup"><span data-stu-id="88b4c-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="88b4c-112">Dwie usługi w chmurze: "FrontEnd001" i "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="88b4c-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="88b4c-113">Sieć wirtualna "CorpNetwork", z dwoma podsieciami: "FrontEnd" i "Wewnętrzna"</span><span class="sxs-lookup"><span data-stu-id="88b4c-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="88b4c-114">Jednej grupy zabezpieczeń sieci jest stosowane tooboth podsieci</span><span class="sxs-lookup"><span data-stu-id="88b4c-114">A single Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="88b4c-115">Urządzenie wirtualne sieci, w tym przykładzie zapora NextGen Barracuda, podłączone podsieci frontonu toohello</span><span class="sxs-lookup"><span data-stu-id="88b4c-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected toohello Frontend subnet</span></span>
* <span data-ttu-id="88b4c-116">Windows Server, który reprezentuje serwer sieci web aplikacji ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="88b4c-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="88b4c-117">Dwa okna serwerów, które reprezentują aplikacji z powrotem kończyć serwery ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="88b4c-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="88b4c-118">Windows server, który reprezentuje serwer DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="88b4c-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="88b4c-119">Mimo że w tym przykładzie użyto zapory NextGen Barracuda, wiele hello różnych urządzeń wirtualnych sieci może być używane w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="88b4c-119">Although this example uses a Barracuda NextGen Firewall, many of hello different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="88b4c-120">W sekcji odwołań hello poniżej jest skrypt programu PowerShell, który zostanie skompilowany większość środowiska hello opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="88b4c-120">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="88b4c-121">Maszyny wirtualne hello budynku i sieciami wirtualnymi, chociaż są realizowane przez skrypt hello nie opisano szczegółowo w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="88b4c-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="88b4c-122">toobuild hello środowiska:</span><span class="sxs-lookup"><span data-stu-id="88b4c-122">toobuild hello environment:</span></span>

1. <span data-ttu-id="88b4c-123">Zapisz hello sieci xml pliku konfiguracji zawarte w sekcji odwołań hello (zaktualizowany o nazwy, lokalizacji i scenariusz hello podane toomatch adresów IP)</span><span class="sxs-lookup"><span data-stu-id="88b4c-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="88b4c-124">Zmienne użytkownika hello aktualizacji hello skryptu toomatch hello środowiska hello skryptu jest toobe uruchomienia (subskrypcje, nazwy usługi itp.)</span><span class="sxs-lookup"><span data-stu-id="88b4c-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="88b4c-125">Uruchom skrypt hello w programie PowerShell</span><span class="sxs-lookup"><span data-stu-id="88b4c-125">Execute hello script in PowerShell</span></span>

<span data-ttu-id="88b4c-126">**Uwaga**: region hello oznaczony w hello skrypt programu PowerShell musi odpowiadać region hello oznaczony w pliku xml konfiguracji sieci hello.</span><span class="sxs-lookup"><span data-stu-id="88b4c-126">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="88b4c-127">Po pomyślnym uruchomieniu skryptu hello można podjąć następujące kroki po skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="88b4c-127">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="88b4c-128">Konfigurowanie reguł zapory hello, to jest objęte hello sekcji poniżej: reguł zapory.</span><span class="sxs-lookup"><span data-stu-id="88b4c-128">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="88b4c-129">Opcjonalnie w sekcji odwołań hello są dwa skrypty tooset powitania serwera sieci web i serwerów aplikacji z tooallow aplikacji sieci web proste, testowanie za pomocą tej konfiguracji DMZ.</span><span class="sxs-lookup"><span data-stu-id="88b4c-129">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="88b4c-130">Hello następnej sekcji opisano większość hello skrypty instrukcje względną tooNetwork grup zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="88b4c-130">hello next section explains most of hello scripts statements relative tooNetwork Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="88b4c-131">Sieciowe grupy zabezpieczeń (NSG)</span><span class="sxs-lookup"><span data-stu-id="88b4c-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="88b4c-132">Na przykład grupy NSG jest wbudowana i następnie ładowane przy użyciu sześciu reguł.</span><span class="sxs-lookup"><span data-stu-id="88b4c-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="88b4c-133">Ogólnie rzecz biorąc należy najpierw utworzyć określonych reguł "Zezwalaj" i następnie ostatnio hello bardziej ogólnym reguły "Deny".</span><span class="sxs-lookup"><span data-stu-id="88b4c-133">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="88b4c-134">Witaj priorytetem nakazują reguły są sprawdzane jako pierwsze.</span><span class="sxs-lookup"><span data-stu-id="88b4c-134">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="88b4c-135">Po znalezieniu tooapply tooa określonej reguły ruchu nie dodatkowe reguły są sprawdzane.</span><span class="sxs-lookup"><span data-stu-id="88b4c-135">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="88b4c-136">Reguły NSG można zastosować w hello kierunek ruchu przychodzącego lub wychodzącego (z perspektywy hello hello podsieci).</span><span class="sxs-lookup"><span data-stu-id="88b4c-136">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="88b4c-137">Deklaratywnie hello następujące reguły są tworzone dla ruchu przychodzącego:</span><span class="sxs-lookup"><span data-stu-id="88b4c-137">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="88b4c-138">Wewnętrzny ruch DNS (port 53) jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="88b4c-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="88b4c-139">Ruch protokołu RDP (port 3389) z tooany Internet hello maszyny Wirtualnej jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="88b4c-139">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="88b4c-140">Ruch HTTP (port 80) z hello Internet toohello NVA (zapory) jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="88b4c-140">HTTP traffic (port 80) from hello Internet toohello NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="88b4c-141">Cały ruch (wszystkie porty) z IIS01 tooAppVM1 jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="88b4c-141">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="88b4c-142">Cały ruch (wszystkie porty) z hello Internet toohello odmowa całej sieci wirtualnej (obie podsieci)</span><span class="sxs-lookup"><span data-stu-id="88b4c-142">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="88b4c-143">Cały ruch (wszystkie porty) z podsieci wewnętrznej bazy danych toohello podsieci frontonu hello jest zabroniony</span><span class="sxs-lookup"><span data-stu-id="88b4c-143">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="88b4c-144">Z tych podsieci tooeach powiązane zasady, jeśli żądanie HTTP zostało ruch przychodzący z serwera sieci web toohello Internet hello zarówno 3 reguły (Zezwalaj) i 5 (odmówić go) będą miały zastosowania, ale ponieważ reguła 3 ma wyższy priorytet tylko będą miały zastosowania i reguły 5 nie przybyły do gry.</span><span class="sxs-lookup"><span data-stu-id="88b4c-144">With these rules bound tooeach subnet, if a HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="88b4c-145">W związku z tym żądaniu hello HTTP będzie dozwolone toohello zapory.</span><span class="sxs-lookup"><span data-stu-id="88b4c-145">Thus hello HTTP request would be allowed toohello firewall.</span></span> <span data-ttu-id="88b4c-146">Jeśli ten sam ruch próbował tooreach hello DNS01 serwer, reguła 5 (odmowa) mogą być hello pierwszy tooapply hello ruch w sieci i nie będzie dozwolone toopass toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="88b4c-146">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="88b4c-147">Reguły 6 (Odmów) bloki hello frontonu podsieci z mówić toohello podsieci wewnętrznej bazy danych (z wyjątkiem dozwolonego ruchu w regułach 1 i 4), chroni sieć zaplecze hello, w przypadku, gdy osoba atakująca dokonywania hello aplikacji sieci web na powitania serwera sieci Web, hello musi ograniczony dostęp toohello wewnętrznej bazy danych "protected" sieci (tylko tooresources udostępniane na serwerze AppVM01 hello).</span><span class="sxs-lookup"><span data-stu-id="88b4c-147">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="88b4c-148">Brak domyślnej regule wychodzącej, która umożliwia ruchu wychodzącego toohello internet.</span><span class="sxs-lookup"><span data-stu-id="88b4c-148">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="88b4c-149">Na przykład firma Microsoft zezwala na ruch wychodzący i nie modyfikowanie reguł wychodzących.</span><span class="sxs-lookup"><span data-stu-id="88b4c-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="88b4c-150">toolock dół ruchu w obu kierunkach, Routing zdefiniowany przez użytkownika jest wymagana, jest to przedstawione w przykładzie różnych, który można znaleźć w hello [dokumentu granic zabezpieczeń głównego][HOME].</span><span class="sxs-lookup"><span data-stu-id="88b4c-150">toolock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in hello [main security boundary document][HOME].</span></span>

<span data-ttu-id="88b4c-151">reguły NSG powyżej Hello omówione są bardzo podobne reguły NSG toohello w [przykład 1 — Tworzenie prostego DMZ z grup NSG][Example1].</span><span class="sxs-lookup"><span data-stu-id="88b4c-151">hello above discussed NSG rules are very similar toohello NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="88b4c-152">Zapoznaj się z tematem hello NSG opis w tym dokumencie, aby uzyskać szczegółowy widok każdej reguły NSG i jego atrybuty.</span><span class="sxs-lookup"><span data-stu-id="88b4c-152">Please review hello NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="88b4c-153">Reguły zapory</span><span class="sxs-lookup"><span data-stu-id="88b4c-153">Firewall Rules</span></span>
<span data-ttu-id="88b4c-154">Klienta zarządzania należy toobe zainstalowany w zaporze hello toomanage komputera, a następnie utwórz wymagane konfiguracje hello.</span><span class="sxs-lookup"><span data-stu-id="88b4c-154">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="88b4c-155">Zobacz hello dostawcy dokumentacji zapory (lub inne NVA) w sposób toomanage hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="88b4c-155">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="88b4c-156">Hello pozostałej części tej sekcji opisano konfigurację hello hello zapory, za pośrednictwem powitania klienta zarządzania dostawców (tj. hello portalu Azure lub programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="88b4c-156">hello remainder of this section will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="88b4c-157">Instrukcje dotyczące pobierania klienta i łączenia toohello Barracuda używana w tym przykładzie można znaleźć tutaj: [Barracuda NG administratora](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="88b4c-157">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="88b4c-158">W zaporze hello przekazywania zasady należy toobe utworzony.</span><span class="sxs-lookup"><span data-stu-id="88b4c-158">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="88b4c-159">Ponieważ w tym przykładzie tylko trasy toohello przychodzącego ruchu zaporę, a następnie toohello serwera sieci web, przekazywanie tylko jedną regułę NAT jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="88b4c-159">Since this example only routes internet traffic in-bound toohello firewall and then toohello web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="88b4c-160">Na powitania zapory NextGen Barracuda używane w tym hello przykład reguły byłoby NAT docelowy reguły toopass ("NAT czasu letniego") tego ruchu.</span><span class="sxs-lookup"><span data-stu-id="88b4c-160">On hello Barracuda NextGen Firewall used in this example hello rule would be a Destination NAT rule (“Dst NAT”) toopass this traffic.</span></span>

<span data-ttu-id="88b4c-161">toocreate hello następujących reguł (lub sprawdź istniejących reguł domyślnych), zaczynając od pulpitu nawigacyjnego klienta Barracuda NG Admin hello, przejdź na kartę Konfiguracja toohello w hello konfigurację operacyjną sekcji kliknij pozycję zestaw reguł.</span><span class="sxs-lookup"><span data-stu-id="88b4c-161">toocreate hello following rule (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="88b4c-162">Wywołuje siatkę, "Main reguły" wyświetli hello istniejących active i zdezaktywowane reguły zapory hello.</span><span class="sxs-lookup"><span data-stu-id="88b4c-162">A grid called, “Main Rules” will show hello existing active and deactivated rules on hello firewall.</span></span> <span data-ttu-id="88b4c-163">W hello prawego górnego rogu tej siatki jest mały, zielony "+", kliknij ten toocreate nową regułę (Uwaga: Zapora może być "zablokowana" zmian, jeśli przycisk oznaczony jako "Lock" i są toocreate lub Edytuj reguły, kliknij ten przycisk zbyt "odblokować" hello zestaw reguł i Zezwól na edytowanie).</span><span class="sxs-lookup"><span data-stu-id="88b4c-163">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello ruleset and allow editing).</span></span> <span data-ttu-id="88b4c-164">Jeśli chcesz, aby tooedit istniejącą regułę, wybierz tej reguły, kliknij prawym przyciskiem myszy i wybierz edytowanie reguły.</span><span class="sxs-lookup"><span data-stu-id="88b4c-164">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="88b4c-165">Utwórz nową regułę i podaj nazwę, na przykład "WebTraffic".</span><span class="sxs-lookup"><span data-stu-id="88b4c-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="88b4c-166">Ikona reguł NAT docelowego Hello wygląda następująco: ![docelowym translacji adresów Sieciowych ikony][2]</span><span class="sxs-lookup"><span data-stu-id="88b4c-166">hello Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="88b4c-167">Reguła Hello, sam będzie wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="88b4c-167">hello rule itself would look something like this:</span></span>

<span data-ttu-id="88b4c-168">![Reguły zapory][3]</span><span class="sxs-lookup"><span data-stu-id="88b4c-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="88b4c-169">W tym miejscu dowolnego adresu dla ruchu przychodzącego, że trafień hello zapory w trakcie tooreach HTTP (port 80 i 443 dla protokołu HTTPS) będą wysyłane hello interfejsu "DHCP1 lokalny adres IP" i przekierowanego toohello serwera sieci Web z hello 10.0.1.5 adres IP zapory.</span><span class="sxs-lookup"><span data-stu-id="88b4c-169">Here any inbound address that hits hello Firewall trying tooreach HTTP (port 80 or 443 for HTTPS) will be sent out hello Firewall’s “DHCP1 Local IP” interface and redirected toohello Web Server with hello IP Address of 10.0.1.5.</span></span> <span data-ttu-id="88b4c-170">Ponieważ przychodzącym hello ruch na porcie 80 i serwer sieci web toohello będzie na porcie 80 zostało niezbędne nie zmiany portu.</span><span class="sxs-lookup"><span data-stu-id="88b4c-170">Since hello traffic is coming in on port 80 and going toohello web server on port 80 no port change was needed.</span></span> <span data-ttu-id="88b4c-171">Jednak powitalne listy docelowej mogło być 10.0.1.5:8080 jeśli nasłuch serwera sieci Web na porcie 8080 w związku z tym tłumaczenia hello przychodzący port 80 hello zapory tooinbound portu 8080 na powitania serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="88b4c-171">However, hello Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating hello inbound port 80 on hello firewall tooinbound port 8080 on hello web server.</span></span>

<span data-ttu-id="88b4c-172">Metodę połączenia powinien również być oznaczony, dla hello docelowy reguły z hello Internet, "Dynamiczne SNAT" jest najbardziej odpowiednia.</span><span class="sxs-lookup"><span data-stu-id="88b4c-172">A Connection Method should also be signified, for hello Destination Rule from hello Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="88b4c-173">Mimo że tylko jedna reguła została utworzona ważne jest jej priorytet została poprawnie ustawiona.</span><span class="sxs-lookup"><span data-stu-id="88b4c-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="88b4c-174">Jeśli w siatce hello wszystkich reguł zapory hello nowe znajdzie się na dole hello (poniżej reguła "BLOCKALL" hello) nigdy nie będą wchodzić w grę.</span><span class="sxs-lookup"><span data-stu-id="88b4c-174">If in hello grid of all rules on hello firewall this new rule is on hello bottom (below hello "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="88b4c-175">Upewnij się, że hello nowo utworzona reguła dla ruchu w sieci web jest powyżej hello BLOCKALL reguły.</span><span class="sxs-lookup"><span data-stu-id="88b4c-175">Ensure hello newly created rule for web traffic is above hello BLOCKALL rule.</span></span>

<span data-ttu-id="88b4c-176">Po utworzeniu reguły hello musi być przypisany toohello zapory, a następnie aktywowany, jeśli nie zostanie to zrobione reguły hello zmiana nie zacznie obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="88b4c-176">Once hello rule is created, it must be pushed toohello firewall and then activated, if this is not done hello rule change will not take effect.</span></span> <span data-ttu-id="88b4c-177">Hello procesu wypychania i aktywacji jest opisany w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="88b4c-177">hello push and activation process is described in hello next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="88b4c-178">Reguły aktywacji</span><span class="sxs-lookup"><span data-stu-id="88b4c-178">Rule Activation</span></span>
<span data-ttu-id="88b4c-179">Z hello ruleset zmodyfikowane tooadd tej reguły, hello ruleset musi być przekazywane toohello zapory i aktywowane.</span><span class="sxs-lookup"><span data-stu-id="88b4c-179">With hello ruleset modified tooadd this rule, hello ruleset must be uploaded toohello firewall and activated.</span></span>

<span data-ttu-id="88b4c-180">![Aktywacja reguły zapory][4]</span><span class="sxs-lookup"><span data-stu-id="88b4c-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="88b4c-181">W prawym górnym narożniku hello powitania klienta zarządzania są klastra przycisków.</span><span class="sxs-lookup"><span data-stu-id="88b4c-181">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="88b4c-182">Kliknij przycisk hello "Wyślij zmiany" przycisk toosend hello zmodyfikowane zasady toohello zapory, a następnie kliknij przycisk "Uaktywnij" hello.</span><span class="sxs-lookup"><span data-stu-id="88b4c-182">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="88b4c-183">Z aktywacji hello zestaw reguł zapory hello tej kompilacji w środowisku przykładzie zostanie zakończona.</span><span class="sxs-lookup"><span data-stu-id="88b4c-183">With hello activation of hello firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="88b4c-184">Opcjonalnie hello post kompilacji w hello odwołuje się do sekcji można uruchamiać skryptów tooadd aplikacji toothis środowiska tootest hello poniżej scenariusze ruchu.</span><span class="sxs-lookup"><span data-stu-id="88b4c-184">Optionally, hello post build scripts in hello References section can be run tooadd an application toothis environment tootest hello below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88b4c-185">Jest krytyczne toorealize, że nie nastąpi trafienie powitania serwera sieci web bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="88b4c-185">It is critical toorealize that you will not hit hello web server directly.</span></span> <span data-ttu-id="88b4c-186">Gdy przeglądarka żąda strony HTTP z FrontEnd001.CloudApp.Net, przekazuje (port 80) punktu końcowego HTTP hello Zapora toohello ruchu nie hello serwer sieci web.</span><span class="sxs-lookup"><span data-stu-id="88b4c-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, hello HTTP endpoint (port 80) passes this traffic toohello firewall not hello web server.</span></span> <span data-ttu-id="88b4c-187">Witaj zapory, a następnie, zgodnie z toohello reguły utworzone powyżej translatory adresów sieciowych, które żądają toohello serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="88b4c-187">hello firewall then, according toohello rule created above, NATs that request toohello Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="88b4c-188">Scenariusze ruchu</span><span class="sxs-lookup"><span data-stu-id="88b4c-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-tooweb-server-through-firewall"></a><span data-ttu-id="88b4c-189">(Dozwolone) TooWeb Web Server przez zaporę</span><span class="sxs-lookup"><span data-stu-id="88b4c-189">(Allowed) Web tooWeb Server through Firewall</span></span>
1. <span data-ttu-id="88b4c-190">Strony internetowe użytkownika żądania HTTP z FrontEnd001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)</span><span class="sxs-lookup"><span data-stu-id="88b4c-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="88b4c-191">Chmury usługi przekazuje ruch przez otwarty punkt końcowy na interfejsie lokalnym toofirewall port 80 na 10.0.1.4:80</span><span class="sxs-lookup"><span data-stu-id="88b4c-191">Cloud service passes traffic through open endpoint on port 80 toofirewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="88b4c-192">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="88b4c-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88b4c-193">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="88b4c-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="88b4c-194">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="88b4c-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="88b4c-195">Zastosować grupy NSG zasady 3 (Internet tooFirewall), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="88b4c-195">NSG Rule 3 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="88b4c-196">Ruch trafienia wewnętrzny adres IP zapory hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="88b4c-196">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="88b4c-197">Reguła zapory przekazywania Zobacz to jest ruch na porcie 80, go przekierowuje serwera sieci web toohello IIS01</span><span class="sxs-lookup"><span data-stu-id="88b4c-197">Firewall forwarding rule see this is port 80 traffic, redirects it toohello web server IIS01</span></span>
6. <span data-ttu-id="88b4c-198">IIS01 nasłuchuje ruchu w sieci web, otrzymuje tego żądania i rozpoczyna przetwarzanie żądania hello</span><span class="sxs-lookup"><span data-stu-id="88b4c-198">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
7. <span data-ttu-id="88b4c-199">IIS01 hello programu SQL Server na AppVM01 monituje o podanie informacji</span><span class="sxs-lookup"><span data-stu-id="88b4c-199">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="88b4c-200">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="88b4c-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="88b4c-201">podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="88b4c-201">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88b4c-202">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="88b4c-202">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="88b4c-203">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="88b4c-203">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="88b4c-204">Grupa NSG zasady 3 (Internet tooFirewall) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="88b4c-204">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="88b4c-205">Zastosuj 4 reguły NSG (IIS01 tooAppVM01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="88b4c-205">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="88b4c-206">AppVM01 odbiera hello zapytanie SQL i odpowiada</span><span class="sxs-lookup"><span data-stu-id="88b4c-206">AppVM01 receives hello SQL Query and responds</span></span>
11. <span data-ttu-id="88b4c-207">Ponieważ ma żadnych reguł wychodzących na powitania odpowiedź hello podsieci wewnętrznej bazy danych jest dozwolone</span><span class="sxs-lookup"><span data-stu-id="88b4c-207">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
12. <span data-ttu-id="88b4c-208">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="88b4c-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="88b4c-209">Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG</span><span class="sxs-lookup"><span data-stu-id="88b4c-209">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="88b4c-210">Reguła systemowa domyślne Hello zezwala na ruch między podsieciami umożliwia ruch więc hello ruch jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="88b4c-210">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
13. <span data-ttu-id="88b4c-211">Serwer usług IIS Hello odbiera odpowiedź SQL hello i kończy odpowiedź HTTP hello i przesyła toohello obiektu żądającego</span><span class="sxs-lookup"><span data-stu-id="88b4c-211">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
14. <span data-ttu-id="88b4c-212">Ponieważ jest to sesji translatora adresów Sieciowych z zapory hello, miejsce docelowe odpowiedzi hello (początkowo) dotyczy hello zapory</span><span class="sxs-lookup"><span data-stu-id="88b4c-212">Since this is a NAT session from hello firewall, hello response destination (initially) is for hello Firewall</span></span>
15. <span data-ttu-id="88b4c-213">zapory Hello odbiera odpowiedź hello z powitania serwera sieci Web i przekazuje wstecz toohello użytkowników Internetu</span><span class="sxs-lookup"><span data-stu-id="88b4c-213">hello firewall receives hello response from hello Web Server and forwards back toohello Internet User</span></span>
16. <span data-ttu-id="88b4c-214">Ponieważ ma żadnych reguł wychodzących na powitania odpowiedź hello podsieci frontonu jest dozwolona, i hello Internet użytkownik otrzymuje hello strona sieci web.</span><span class="sxs-lookup"><span data-stu-id="88b4c-214">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="88b4c-215">(Dozwolone) TooBackend protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="88b4c-215">(Allowed) RDP tooBackend</span></span>
1. <span data-ttu-id="88b4c-216">Administrator serwera w Internecie żądań tooAppVM01 sesji protokołu RDP w przypadku xxxxx hello losowo przypisany numer portu dla protokołu RDP tooAppVM01 BackEnd001.CloudApp.Net:xxxxx (hello przypisany port znajduje się na powitania portalu Azure lub za pomocą programu PowerShell)</span><span class="sxs-lookup"><span data-stu-id="88b4c-216">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="88b4c-217">Ponieważ hello zapory tylko nasłuchuje na powitania FrontEnd001.CloudApp.Net adres nie uczestniczy z tego przepływu ruchu</span><span class="sxs-lookup"><span data-stu-id="88b4c-217">Since hello Firewall is only listening on hello FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="88b4c-218">Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="88b4c-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88b4c-219">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="88b4c-219">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="88b4c-220">Zastosuj 2 reguły NSG (RDP), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="88b4c-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="88b4c-221">Z nie reguł dla ruchu wychodzącego Zastosuj reguły domyślne i zwracany ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="88b4c-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="88b4c-222">Włączono sesji protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="88b4c-222">RDP session is enabled</span></span>
6. <span data-ttu-id="88b4c-223">AppVM01 wyświetli monit o hasło nazwy użytkownika</span><span class="sxs-lookup"><span data-stu-id="88b4c-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="88b4c-224">(Dozwolone) Wyszukiwania DNS serwera sieci Web na serwerze DNS</span><span class="sxs-lookup"><span data-stu-id="88b4c-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="88b4c-225">Serwer, IIS01, musi na www.data.gov strumieniowego źródła danych w sieci Web, ale wymaga tooresolve hello adres.</span><span class="sxs-lookup"><span data-stu-id="88b4c-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="88b4c-226">Hello konfiguracji sieci dla listy sieci wirtualnej hello DNS01 (10.0.2.4 podsieci wewnętrznej bazy danych hello) jako podstawowy serwer DNS hello IIS01 wysyła tooDNS01 żądania DNS hello</span><span class="sxs-lookup"><span data-stu-id="88b4c-226">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="88b4c-227">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="88b4c-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="88b4c-228">Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="88b4c-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88b4c-229">Zastosuj reguły NSG 1 DNS (Domain Name System), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="88b4c-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="88b4c-230">Serwer DNS odbiera żądanie hello</span><span class="sxs-lookup"><span data-stu-id="88b4c-230">DNS server receives hello request</span></span>
6. <span data-ttu-id="88b4c-231">Serwer DNS nie ma adresu hello w pamięci podręcznej i prosi o główny serwer DNS na powitania internet</span><span class="sxs-lookup"><span data-stu-id="88b4c-231">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="88b4c-232">Nie reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="88b4c-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="88b4c-233">DNS w Internecie serwer odpowiada, ponieważ ta sesja została zainicjowana wewnętrznie, odpowiedź hello jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="88b4c-233">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="88b4c-234">Serwer DNS będzie buforować odpowiedź hello i odpowiada tooIIS01 wstecz toohello żądania początkowego</span><span class="sxs-lookup"><span data-stu-id="88b4c-234">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="88b4c-235">Nie reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="88b4c-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="88b4c-236">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="88b4c-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="88b4c-237">Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG</span><span class="sxs-lookup"><span data-stu-id="88b4c-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="88b4c-238">Hello domyślna systemu reguła zezwala na ruch między podsieciami umożliwiałyby tego rodzaju ruch, ruch hello jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="88b4c-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="88b4c-239">IIS01 odbiera odpowiedź hello z DNS01</span><span class="sxs-lookup"><span data-stu-id="88b4c-239">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="88b4c-240">(Dozwolone) Plik dostępu do serwera sieci Web na AppVM01</span><span class="sxs-lookup"><span data-stu-id="88b4c-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="88b4c-241">IIS01 żąda pliku na AppVM01</span><span class="sxs-lookup"><span data-stu-id="88b4c-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="88b4c-242">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="88b4c-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="88b4c-243">podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="88b4c-243">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88b4c-244">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="88b4c-244">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="88b4c-245">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="88b4c-245">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="88b4c-246">Grupa NSG zasady 3 (Internet tooFirewall) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="88b4c-246">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="88b4c-247">Zastosuj 4 reguły NSG (IIS01 tooAppVM01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="88b4c-247">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="88b4c-248">AppVM01 odbiera żądanie hello i wysyła plik (przy założeniu, że autoryzacji dostępu)</span><span class="sxs-lookup"><span data-stu-id="88b4c-248">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="88b4c-249">Ponieważ ma żadnych reguł wychodzących na powitania odpowiedź hello podsieci wewnętrznej bazy danych jest dozwolone</span><span class="sxs-lookup"><span data-stu-id="88b4c-249">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
6. <span data-ttu-id="88b4c-250">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="88b4c-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88b4c-251">Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG</span><span class="sxs-lookup"><span data-stu-id="88b4c-251">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="88b4c-252">Reguła systemowa domyślne Hello zezwala na ruch między podsieciami umożliwia ruch więc hello ruch jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="88b4c-252">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="88b4c-253">Serwer usług IIS Hello odbiera hello pliku</span><span class="sxs-lookup"><span data-stu-id="88b4c-253">hello IIS server receives hello file</span></span>

#### <a name="denied-web-direct-tooweb-server"></a><span data-ttu-id="88b4c-254">(Odmowa) Bezpośrednie tooWeb sieci Web serwera</span><span class="sxs-lookup"><span data-stu-id="88b4c-254">(Denied) Web direct tooWeb Server</span></span>
<span data-ttu-id="88b4c-255">Ponieważ powitania serwera sieci Web, IIS01 i hello zapory są w hello mają tej samej usługi w chmurze hello sam publiczny adres IP połączonej.</span><span class="sxs-lookup"><span data-stu-id="88b4c-255">Since hello Web Server, IIS01, and hello Firewall are in hello same Cloud Service they share hello same public facing IP address.</span></span> <span data-ttu-id="88b4c-256">W związku z tym cały ruch HTTP będą kierowane toohello zapory.</span><span class="sxs-lookup"><span data-stu-id="88b4c-256">Thus any HTTP traffic would be directed toohello firewall.</span></span> <span data-ttu-id="88b4c-257">Podczas żądania hello czy można pomyślnie obsłużył operację, go nie można przejść bezpośrednio toohello serwera sieci Web, jest przekazywany, zgodnie z założeniami, za pośrednictwem hello najpierw zapory.</span><span class="sxs-lookup"><span data-stu-id="88b4c-257">While hello request would be successfully served, it cannot go directly toohello Web Server, it passed, as designed, through hello Firewall first.</span></span> <span data-ttu-id="88b4c-258">Zobacz hello pierwszego scenariusza, w tej sekcji hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="88b4c-258">See hello first Scenario in this section for hello traffic flow.</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="88b4c-259">(Odmowa) TooBackend sieci Web serwera</span><span class="sxs-lookup"><span data-stu-id="88b4c-259">(Denied) Web tooBackend Server</span></span>
1. <span data-ttu-id="88b4c-260">Internet użytkownik spróbuje tooaccess pliku AppVM01 za pośrednictwem hello BackEnd001.CloudApp.Net usługi</span><span class="sxs-lookup"><span data-stu-id="88b4c-260">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="88b4c-261">Ponieważ nie ma żadnych punktów końcowych otwarty do udziału plików, to nie przejdzie hello usługi w chmurze i nie osiągnięcia powitania serwera</span><span class="sxs-lookup"><span data-stu-id="88b4c-261">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="88b4c-262">Jeśli punkty końcowe hello były otwarte jakiegoś powodu, reguły NSG 5 (Internet tooVNet) umożliwia zablokowanie tego ruchu</span><span class="sxs-lookup"><span data-stu-id="88b4c-262">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="88b4c-263">(Odmowa) Wyszukiwania DNS w sieci Web na serwerze DNS</span><span class="sxs-lookup"><span data-stu-id="88b4c-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="88b4c-264">Internet użytkownik spróbuje toolookup wewnętrzny rekord DNS na DNS01 za pośrednictwem hello BackEnd001.CloudApp.Net usługi</span><span class="sxs-lookup"><span data-stu-id="88b4c-264">Internet user tries toolookup an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="88b4c-265">Ponieważ nie ma żadnych punktów końcowych otwarte dla serwera DNS, to nie przejdzie hello usługi w chmurze i nie osiągnięcia powitania serwera</span><span class="sxs-lookup"><span data-stu-id="88b4c-265">Since there are no endpoints open for DNS, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="88b4c-266">Jeśli punkty końcowe hello były otwarte jakiegoś powodu, reguły NSG 5 (Internet tooVNet) umożliwia zablokowanie tego ruchu (Uwaga: nie ma zastosowania tej reguły 1 (DNS) z dwóch przyczyn, pierwszy adres źródłowy hello jest hello internet, ta zasada ma zastosowanie tylko toohello również lokalnej sieci wirtualnej jako hello źródła jest to Reguła zezwalająca, nigdy nie będzie go odmówić ruchu)</span><span class="sxs-lookup"><span data-stu-id="88b4c-266">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="88b4c-267">(Odmowa) Dostęp w sieci Web tooSQL przez zaporę</span><span class="sxs-lookup"><span data-stu-id="88b4c-267">(Denied) Web tooSQL access through Firewall</span></span>
1. <span data-ttu-id="88b4c-268">Internet użytkownik żąda danych SQL z FrontEnd001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)</span><span class="sxs-lookup"><span data-stu-id="88b4c-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="88b4c-269">Ponieważ nie ma żadnych punktów końcowych otwarte dla bazy danych SQL, to nie przejdzie hello usługi w chmurze i nie osiągnąć hello zapory</span><span class="sxs-lookup"><span data-stu-id="88b4c-269">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="88b4c-270">Jeśli punkty końcowe zostały otwarte jakiegoś powodu, podsieci frontonu hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="88b4c-270">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88b4c-271">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="88b4c-271">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="88b4c-272">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="88b4c-272">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="88b4c-273">2 reguły NSG (Internet tooFirewall) mają zastosowanie, ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="88b4c-273">NSG Rule 2 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="88b4c-274">Ruch trafienia wewnętrzny adres IP zapory hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="88b4c-274">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="88b4c-275">Zapora nie ma przekazywanie reguł dla bazy danych SQL i porzucania hello ruchu</span><span class="sxs-lookup"><span data-stu-id="88b4c-275">Firewall has no forwarding rules for SQL and drops hello traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="88b4c-276">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="88b4c-276">Conclusion</span></span>
<span data-ttu-id="88b4c-277">Jest to stosunkowo proste do przodu sposób ochrony aplikacji za pomocą zapory i izolowanie podsieci wewnętrznej hello z ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="88b4c-277">This is a relatively straight forward way of protecting your application with a firewall and isolating hello back end subnet from inbound traffic.</span></span>

<span data-ttu-id="88b4c-278">Więcej przykładów i Przegląd granic zabezpieczeń sieci można znaleźć [tutaj][HOME].</span><span class="sxs-lookup"><span data-stu-id="88b4c-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="88b4c-279">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="88b4c-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="88b4c-280">Skrypt głównego i konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="88b4c-280">Main Script and Network Config</span></span>
<span data-ttu-id="88b4c-281">Zapisz hello pełne skryptu w pliku skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88b4c-281">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="88b4c-282">Zapisz hello konfigurację sieci w pliku o nazwie "NetworkConf2.xml".</span><span class="sxs-lookup"><span data-stu-id="88b4c-282">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="88b4c-283">Modyfikuj zmienne zdefiniowane przez użytkownika hello, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="88b4c-283">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="88b4c-284">Uruchom skrypt hello, a następnie postępuj zgodnie z powyższych instrukcji instalacji reguły zapory hello.</span><span class="sxs-lookup"><span data-stu-id="88b4c-284">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="88b4c-285">Pełna skryptu</span><span class="sxs-lookup"><span data-stu-id="88b4c-285">Full Script</span></span>
<span data-ttu-id="88b4c-286">Ten skrypt zostanie, na podstawie hello zmiennych zdefiniowanych przez użytkownika:</span><span class="sxs-lookup"><span data-stu-id="88b4c-286">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="88b4c-287">Połącz tooan subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="88b4c-287">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="88b4c-288">Utwórz nowe konto magazynu</span><span class="sxs-lookup"><span data-stu-id="88b4c-288">Create a new storage account</span></span>
3. <span data-ttu-id="88b4c-289">Utwórz nową sieć wirtualną z dwoma podsieciami, zgodnie z definicją w pliku konfiguracji sieci hello</span><span class="sxs-lookup"><span data-stu-id="88b4c-289">Create a new VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="88b4c-290">Tworzenie maszyn wirtualnych serwera 4 windows</span><span class="sxs-lookup"><span data-stu-id="88b4c-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="88b4c-291">Skonfiguruj grupy NSG w tym:</span><span class="sxs-lookup"><span data-stu-id="88b4c-291">Configure NSG including:</span></span>
   * <span data-ttu-id="88b4c-292">Tworzenie grupy NSG</span><span class="sxs-lookup"><span data-stu-id="88b4c-292">Creating a NSG</span></span>
   * <span data-ttu-id="88b4c-293">Zapełnianie reguły</span><span class="sxs-lookup"><span data-stu-id="88b4c-293">Populating it with rules</span></span>
   * <span data-ttu-id="88b4c-294">Powiązanie hello NSG toohello odpowiednie podsieci</span><span class="sxs-lookup"><span data-stu-id="88b4c-294">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="88b4c-295">Ten skrypt programu PowerShell powinien zostać uruchomiony lokalnie na się, że połączenie internetowe, komputera lub serwera.</span><span class="sxs-lookup"><span data-stu-id="88b4c-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88b4c-296">Uruchomienie tego skryptu można ostrzeżenia lub inne komunikaty informacyjne, które pop w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88b4c-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="88b4c-297">Tylko komunikaty o błędach na czerwono są przyczyną problemu.</span><span class="sxs-lookup"><span data-stu-id="88b4c-297">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
       - Three Servers on hello BackEnd Subnet
       - Network Security Groups tooallow/deny traffic patterns as declared

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Security requirements are different for each use case and can be addressed in a
      myriad of ways. Please be sure that any sensitive data or applications are behind
      hello appropriate layer(s) of protection. This script serves as an example of some
      of hello techniques that can be used, but should not be used for all scenarios. You
      are responsible tooassess your security needs and hello appropriate protections
      needed, and then effectively implement those protections.

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       myFirewall - 10.0.1.4
       IIS01      - 10.0.1.5

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
            -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
            -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
            -Protocol *

        # Assign hello NSG toohello Subnets
            Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="88b4c-298">Plik konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="88b4c-298">Network Config File</span></span>
<span data-ttu-id="88b4c-299">Zapisz ten plik xml z lokalizacji zaktualizowane i Dodaj hello łącze toothis pliku toohello $NetworkConfigFile zmiennej w skrypcie hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="88b4c-299">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a><span data-ttu-id="88b4c-300">Przykładowe skrypty aplikacji</span><span class="sxs-lookup"><span data-stu-id="88b4c-300">Sample Application Scripts</span></span>
<span data-ttu-id="88b4c-301">Jeśli chcesz tooinstall Przykładowa aplikacja dla tego i innych przykłady DMZ, jeden podano na powitania następującego łącza: [przykładowy skrypt aplikacji][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="88b4c-301">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Przychodzący DMZ z grupy NSG"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Ikona NAT docelowego"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Reguły zapory"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Aktywacja reguły zapory"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
