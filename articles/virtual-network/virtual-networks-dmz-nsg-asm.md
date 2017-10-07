---
title: "aaaAzure przykład DMZ — Tworzenie prostego DMZ z grup NSG | Dokumentacja firmy Microsoft"
description: "Tworzenie DMZ z grup zabezpieczeń sieci (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="10628-103">Przykład 1 — Tworzenie prostego DMZ, za pomocą grup NSG z klasycznego środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="10628-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="10628-104">[Zwraca toohello strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME]</span><span class="sxs-lookup"><span data-stu-id="10628-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="10628-105">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10628-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="10628-106">Classic — PowerShell</span><span class="sxs-lookup"><span data-stu-id="10628-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="10628-107">W tym przykładzie tworzy DMZ pierwotnych z czterech serwerów z systemem Windows i grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="10628-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="10628-108">W tym przykładzie przedstawiono każdy hello odpowiednich PowerShell poleceń tooprovide głębsze zrozumienie każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="10628-108">This example describes each of hello relevant PowerShell commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="10628-109">Istnieje również scenariusz ruchu sekcji tooprovide jako szczegółowe krok po kroku, jak ruchu obejmującego hello warstw zabezpieczeń w hello DMZ.</span><span class="sxs-lookup"><span data-stu-id="10628-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="10628-110">Na koniec w sekcji odwołań hello jest kompletny kod hello i toobuild instrukcji tego środowiska tootest i doświadczenia z różnych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="10628-110">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="10628-111">![Przychodzący DMZ z grupy NSG][1]</span><span class="sxs-lookup"><span data-stu-id="10628-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="10628-112">Opis elementu środowiska</span><span class="sxs-lookup"><span data-stu-id="10628-112">Environment description</span></span>
<span data-ttu-id="10628-113">W tym przykładzie subskrypcja zawiera hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="10628-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="10628-114">Dwie usługi w chmurze: "FrontEnd001" i "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="10628-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="10628-115">Sieć wirtualną "CorpNetwork", z dwoma podsieciami; "FrontEnd" i "Wewnętrzna"</span><span class="sxs-lookup"><span data-stu-id="10628-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="10628-116">Grupy zabezpieczeń sieci jest stosowane tooboth podsieci</span><span class="sxs-lookup"><span data-stu-id="10628-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="10628-117">Windows Server, który reprezentuje serwer sieci web aplikacji ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="10628-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="10628-118">Dwóch systemów windows Server, które reprezentują serwery zaplecza aplikacji ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="10628-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="10628-119">Windows server, który reprezentuje serwer DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="10628-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="10628-120">W sekcji odwołań hello jest skrypt programu PowerShell, która tworzy większość środowiska hello opisane w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="10628-120">In hello references section, there is a PowerShell script that builds most of hello environment described in this example.</span></span> <span data-ttu-id="10628-121">Maszyny wirtualne hello budynku i sieciami wirtualnymi, chociaż są realizowane przez skrypt hello nie opisano szczegółowo w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="10628-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="10628-122">toobuild hello środowiska;</span><span class="sxs-lookup"><span data-stu-id="10628-122">toobuild hello environment;</span></span>

1. <span data-ttu-id="10628-123">Zapisz hello sieci xml pliku konfiguracji zawarte w sekcji odwołań hello (zaktualizowany o nazwy, lokalizacji i scenariusz hello podane toomatch adresów IP)</span><span class="sxs-lookup"><span data-stu-id="10628-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="10628-124">Zmienne użytkownika hello aktualizacji hello skryptu toomatch hello środowiska hello skryptu jest toobe uruchomienia (subskrypcje, nazwy usługi, itp.)</span><span class="sxs-lookup"><span data-stu-id="10628-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="10628-125">Uruchom skrypt hello w programie PowerShell</span><span class="sxs-lookup"><span data-stu-id="10628-125">Execute hello script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="10628-126">region Hello oznaczony w hello skrypt programu PowerShell musi odpowiadać region hello oznaczony w pliku xml konfiguracji sieci hello.</span><span class="sxs-lookup"><span data-stu-id="10628-126">hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>
>
>

<span data-ttu-id="10628-127">Po hello skrypt zostanie uruchomiony pomyślnie dodatkowe opcjonalne kroki mogą zostać podjęte, w sekcji odwołań hello są dwa skrypty tooset powitania serwera sieci web i serwerów aplikacji z tooallow aplikacji sieci web proste, testowanie za pomocą tej konfiguracji DMZ.</span><span class="sxs-lookup"><span data-stu-id="10628-127">Once hello script runs successfully additional optional steps may be taken, in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="10628-128">Witaj poniższe sekcje zawierają szczegółowy opis grup zabezpieczeń sieci i ich działania w tym przykładzie przez Instruktaż wierszy kluczy hello skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10628-128">hello following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of hello PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="10628-129">Sieciowe grupy zabezpieczeń (NSG)</span><span class="sxs-lookup"><span data-stu-id="10628-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="10628-130">Na przykład grupy NSG jest wbudowana i następnie ładowane przy użyciu sześciu reguł.</span><span class="sxs-lookup"><span data-stu-id="10628-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="10628-131">Ogólnie rzecz biorąc należy najpierw utworzyć określonych reguł "Zezwalaj" i następnie ostatnio hello bardziej ogólnym reguły "Deny".</span><span class="sxs-lookup"><span data-stu-id="10628-131">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="10628-132">Witaj priorytetem nakazują reguły są sprawdzane jako pierwsze.</span><span class="sxs-lookup"><span data-stu-id="10628-132">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="10628-133">Po znalezieniu tooapply tooa określonej reguły ruchu nie dodatkowe reguły są sprawdzane.</span><span class="sxs-lookup"><span data-stu-id="10628-133">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="10628-134">Reguły NSG można zastosować w hello kierunek ruchu przychodzącego lub wychodzącego (z perspektywy hello hello podsieci).</span><span class="sxs-lookup"><span data-stu-id="10628-134">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="10628-135">Deklaratywnie hello następujące reguły są tworzone dla ruchu przychodzącego:</span><span class="sxs-lookup"><span data-stu-id="10628-135">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="10628-136">Wewnętrzny ruch DNS (port 53) jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="10628-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="10628-137">Ruch protokołu RDP (port 3389) z tooany Internet hello maszyny Wirtualnej jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="10628-137">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="10628-138">Ruch HTTP (port 80) z serwera tooweb internetowej hello (IIS01) jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="10628-138">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="10628-139">Cały ruch (wszystkie porty) z IIS01 tooAppVM1 jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="10628-139">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="10628-140">Cały ruch (wszystkie porty) z hello Internet toohello odmowa całej sieci wirtualnej (obie podsieci)</span><span class="sxs-lookup"><span data-stu-id="10628-140">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="10628-141">Cały ruch (wszystkie porty) z podsieci wewnętrznej bazy danych toohello podsieci frontonu hello jest zabroniony</span><span class="sxs-lookup"><span data-stu-id="10628-141">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="10628-142">Z tych podsieci tooeach powiązane zasady, jeśli żądanie HTTP zostało ruch przychodzący z serwera sieci web toohello Internet hello zarówno 3 reguły (Zezwalaj) i 5 (odmówić go) będą miały zastosowania, ale ponieważ reguła 3 ma wyższy priorytet tylko będą miały zastosowania i reguły 5 nie przybyły do gry.</span><span class="sxs-lookup"><span data-stu-id="10628-142">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="10628-143">W związku z tym żądania HTTP hello mogliby toohello serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="10628-143">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="10628-144">Jeśli ten sam ruch próbował tooreach hello DNS01 serwer, reguła 5 (odmowa) mogą być hello pierwszy tooapply hello ruch w sieci i nie będzie dozwolone toopass toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="10628-144">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="10628-145">Reguła 6 (Odmów) blokuje hello podsieci frontonu z mówić toohello podsieci wewnętrznej bazy danych (z wyjątkiem dozwolonego ruchu w regułach 1 i 4), ten zestaw reguł chroni hello sieci wewnętrznej bazy danych w przypadku, gdy osoba atakująca dokonywania hello aplikacji sieci web na powitania serwera sieci Web, osoba atakująca hello czy ograniczona toohello dostępu do sieci (tylko tooresources udostępniane na serwerze AppVM01 hello) wewnętrznej bazy danych "protected".</span><span class="sxs-lookup"><span data-stu-id="10628-145">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="10628-146">Brak domyślnej regule wychodzącej, która umożliwia ruchu wychodzącego toohello internet.</span><span class="sxs-lookup"><span data-stu-id="10628-146">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="10628-147">Na przykład firma Microsoft zezwala na ruch wychodzący i nie modyfikowanie reguł wychodzących.</span><span class="sxs-lookup"><span data-stu-id="10628-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="10628-148">toolock dół ruchu w obu kierunkach, Routing zdefiniowany przez użytkownika jest wymagany i jest przedstawione w "W przykładzie 3" na powitania [strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME].</span><span class="sxs-lookup"><span data-stu-id="10628-148">toolock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="10628-149">Każda reguła omówiono bardziej szczegółowo w następujący sposób (**Uwaga**: dowolny element w hello następujące listy rozpoczynający się od znaku dolara (na przykład: $NSGName) jest zmienną użytkownika ze skryptu hello hello odwołanie sekcji tego dokumentu):</span><span class="sxs-lookup"><span data-stu-id="10628-149">Each rule is discussed in more detail as follows (**Note**: any item in hello following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="10628-150">Najpierw sieciowej grupy zabezpieczeń muszą zostać skompilowane toohold hello reguł:</span><span class="sxs-lookup"><span data-stu-id="10628-150">First a Network Security Group must be built toohold hello rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="10628-151">Pierwsza reguła Hello w tym przykładzie zezwala na ruch DNS między wszystkich serwerów DNS toohello sieciach wewnętrznych hello podsieci wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="10628-151">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="10628-152">Reguła Hello zawiera niektóre ważne parametry:</span><span class="sxs-lookup"><span data-stu-id="10628-152">hello rule has some important parameters:</span></span>
   
   * <span data-ttu-id="10628-153">"Typ" oznacza, że w kierunku przepływu ruchu obowiązuje tej reguły.</span><span class="sxs-lookup"><span data-stu-id="10628-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="10628-154">Kierunek Hello jest z punktu widzenia hello hello podsieci lub maszyny wirtualnej (w zależności od tego, gdzie jest powiązany ten NSG).</span><span class="sxs-lookup"><span data-stu-id="10628-154">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="10628-155">W związku z tym jeśli typ to "Przychodzącego" i ruchu jest wprowadzanie hello podsieci, powinna zostać zastosowana reguła hello i ruchu wychodzącego hello podsieci nie może niekorzystnie wpływać tej reguły.</span><span class="sxs-lookup"><span data-stu-id="10628-155">Thus if Type is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="10628-156">"Priority" Ustawia kolejność hello, w jakiej są oceniane przepływu ruchu.</span><span class="sxs-lookup"><span data-stu-id="10628-156">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="10628-157">Witaj niższe hello numer hello wyższy hello priorytet.</span><span class="sxs-lookup"><span data-stu-id="10628-157">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="10628-158">Jeśli reguła ma zastosowanie tooa przepływu ruchu, żadne dalsze reguły są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="10628-158">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="10628-159">W związku z tym jeśli reguła o priorytecie 1 zezwala na ruch i reguły o priorytecie 2 nie zezwala na ruch i tootraffic mają zastosowanie zarówno reguły, a następnie hello ruch będzie dozwolony tooflow (ponieważ reguła 1 ma wyższy priorytet trwało efektu i żadne dodatkowe reguły zostały zastosowane).</span><span class="sxs-lookup"><span data-stu-id="10628-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="10628-160">"Akcja" oznacza, że jeśli ruch wpływ ta reguła jest zablokowane lub dozwolone.</span><span class="sxs-lookup"><span data-stu-id="10628-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="10628-161">Ta zasada umożliwia tooflow ruchu protokołu RDP z portem RDP toohello internet hello na dowolnym serwerze na powitania powiązany podsieci.</span><span class="sxs-lookup"><span data-stu-id="10628-161">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> <span data-ttu-id="10628-162">Ta zasada wykorzystuje dwa typy specjalne prefiksy adresów; "VIRTUAL_NETWORK" i "INTERNET".</span><span class="sxs-lookup"><span data-stu-id="10628-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="10628-163">Tagi te są łatwo tooaddress większych kategorii prefiksy adresów.</span><span class="sxs-lookup"><span data-stu-id="10628-163">These tags are an easy way tooaddress a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="10628-164">Ta zasada umożliwia przychodzący serwera sieci web hello toohit internet ruchu.</span><span class="sxs-lookup"><span data-stu-id="10628-164">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="10628-165">Ta zasada nie zmienia hello zachowanie routingu.</span><span class="sxs-lookup"><span data-stu-id="10628-165">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="10628-166">zasada Hello umożliwia tylko ruch kierowany do IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="10628-166">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="10628-167">W związku z tym jeśli ruch z hello Internet miał powitania serwera sieci web jako miejsca docelowego tej reguły spowoduje zezwolenie i zatrzymać dalsze przetwarzanie reguł.</span><span class="sxs-lookup"><span data-stu-id="10628-167">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="10628-168">(W regule hello priorytetem 140 wszystkich innych przychodzącego ruchu internetowego jest zablokowane).</span><span class="sxs-lookup"><span data-stu-id="10628-168">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="10628-169">Jeśli jest tylko przetwarzania ruchu HTTP, ta zasada może być dalsze ograniczeniami tooonly Zezwalaj docelowy Port 80.</span><span class="sxs-lookup"><span data-stu-id="10628-169">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="10628-170">Ta zasada umożliwia toopass ruchu z serwera IIS01 powitania serwera AppVM01 toohello, nowsze reguła blokuje cały ruch tooBackend frontonu.</span><span class="sxs-lookup"><span data-stu-id="10628-170">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="10628-171">tooimprove tej reguły, jeśli znane jest hello portu, który powinien zostać dodane.</span><span class="sxs-lookup"><span data-stu-id="10628-171">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="10628-172">Na przykład, jeśli serwer IIS hello jest naciśnięcie tylko programu SQL Server na AppVM01, zakres portów docelowych hello należy zmienić "*" (Any) too1433 (hello SQL port) dzięki czemu mniejsze przychodzących ataki AppVM01 aplikacji sieci web hello kiedykolwiek zagrożenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="10628-172">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="10628-173">Ta reguła nie zezwala na ruch z hello internet tooany serwerów w sieci hello.</span><span class="sxs-lookup"><span data-stu-id="10628-173">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="10628-174">Przy użyciu reguł hello priorytetem 110 i 120 efekt hello jest tooallow tylko dla ruchu przychodzącego ruchu toohello zapory internetowej i porty protokołu RDP na serwerach i blokuje wszystkie inne elementy.</span><span class="sxs-lookup"><span data-stu-id="10628-174">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="10628-175">Ta reguła jest "awaryjnie" reguły tooblock wszystkie przepływy nieoczekiwany.</span><span class="sxs-lookup"><span data-stu-id="10628-175">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="10628-176">Reguła końcowego Hello nie zezwala na ruch z podsieci wewnętrznej bazy danych toohello podsieci frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="10628-176">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="10628-177">Ponieważ ta reguła jest tylko regułę ruchu przychodzącego, odwrotnej ruch jest dozwolony (od toohello zaplecza hello frontonu).</span><span class="sxs-lookup"><span data-stu-id="10628-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="10628-178">Scenariusze ruchu</span><span class="sxs-lookup"><span data-stu-id="10628-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="10628-179">(*Dozwolone*) Internet tooweb serwera</span><span class="sxs-lookup"><span data-stu-id="10628-179">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="10628-180">Użytkownik internet zażąda strony HTTP z FrontEnd001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)</span><span class="sxs-lookup"><span data-stu-id="10628-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="10628-181">W chmurze usługi przekazuje ruch przez otwarty punkt końcowy na porcie 80 kierunku IIS01 (powitania serwera sieci web)</span><span class="sxs-lookup"><span data-stu-id="10628-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="10628-182">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="10628-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="10628-183">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="10628-183">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="10628-184">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="10628-184">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="10628-185">Zastosować grupy NSG zasady 3 (Internet tooIIS01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="10628-185">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="10628-186">Ruch trafienia wewnętrzny adres IP serwera sieci web hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="10628-186">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="10628-187">IIS01 nasłuchuje ruchu w sieci web, otrzymuje tego żądania i rozpoczyna przetwarzanie żądania hello</span><span class="sxs-lookup"><span data-stu-id="10628-187">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="10628-188">IIS01 hello programu SQL Server na AppVM01 monituje o podanie informacji</span><span class="sxs-lookup"><span data-stu-id="10628-188">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="10628-189">Ponieważ nie ma żadnych reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="10628-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="10628-190">podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="10628-190">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="10628-191">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="10628-191">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="10628-192">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="10628-192">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="10628-193">Grupa NSG zasady 3 (Internet tooFirewall) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="10628-193">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="10628-194">Zastosuj 4 reguły NSG (IIS01 tooAppVM01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="10628-194">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="10628-195">AppVM01 odbiera hello zapytanie SQL i odpowiada</span><span class="sxs-lookup"><span data-stu-id="10628-195">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="10628-196">Ponieważ na powitania podsieci wewnętrznej bazy danych nie ma żadnych reguł dla ruchu wychodzącego, odpowiedź hello jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="10628-196">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="10628-197">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="10628-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="10628-198">Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG</span><span class="sxs-lookup"><span data-stu-id="10628-198">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="10628-199">Reguła systemowa domyślne Hello zezwala na ruch między podsieciami umożliwia ruch więc hello ruch jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="10628-199">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="10628-200">Serwer usług IIS Hello odbiera odpowiedź SQL hello i kończy odpowiedź HTTP hello i przesyła toohello obiektu żądającego</span><span class="sxs-lookup"><span data-stu-id="10628-200">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
13. <span data-ttu-id="10628-201">Ponieważ nie ma żadnych reguł dla ruchu wychodzącego w podsieci frontonu hello hello odpowiedzi jest dozwolone, a hello internet użytkownik otrzymuje hello strona sieci web.</span><span class="sxs-lookup"><span data-stu-id="10628-201">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="10628-202">(*Dozwolone*) toobackend protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="10628-202">(*Allowed*) RDP toobackend</span></span>
1. <span data-ttu-id="10628-203">Administrator serwera w Internecie żądań tooAppVM01 sesji protokołu RDP w przypadku xxxxx hello losowo przypisany numer portu dla protokołu RDP tooAppVM01 BackEnd001.CloudApp.Net:xxxxx (hello przypisany port znajduje się na powitania portalu Azure lub za pomocą programu PowerShell)</span><span class="sxs-lookup"><span data-stu-id="10628-203">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="10628-204">Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="10628-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="10628-205">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="10628-205">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="10628-206">Zastosuj 2 reguły NSG (RDP), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="10628-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="10628-207">Z nie reguł dla ruchu wychodzącego Zastosuj reguły domyślne i zwracany ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="10628-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="10628-208">Włączono sesji protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="10628-208">RDP session is enabled</span></span>
5. <span data-ttu-id="10628-209">AppVM01 monit o podanie hello nazwy użytkownika i hasła</span><span class="sxs-lookup"><span data-stu-id="10628-209">AppVM01 prompts for hello user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="10628-210">(*Dozwolone*) wyszukiwanie nazwy DNS serwera sieci Web na serwerze DNS</span><span class="sxs-lookup"><span data-stu-id="10628-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="10628-211">Serwer, IIS01, musi na www.data.gov strumieniowego źródła danych w sieci Web, ale wymaga tooresolve hello adres.</span><span class="sxs-lookup"><span data-stu-id="10628-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="10628-212">Hello konfiguracji sieci dla listy sieci wirtualnej hello DNS01 (10.0.2.4 podsieci wewnętrznej bazy danych hello) jako podstawowy serwer DNS hello IIS01 wysyła tooDNS01 żądania DNS hello</span><span class="sxs-lookup"><span data-stu-id="10628-212">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="10628-213">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="10628-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="10628-214">Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="10628-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="10628-215">Zastosuj reguły NSG 1 DNS (Domain Name System), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="10628-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="10628-216">Serwer DNS odbiera żądanie hello</span><span class="sxs-lookup"><span data-stu-id="10628-216">DNS server receives hello request</span></span>
6. <span data-ttu-id="10628-217">Serwer DNS nie ma adresu hello w pamięci podręcznej i prosi o główny serwer DNS na powitania internet</span><span class="sxs-lookup"><span data-stu-id="10628-217">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="10628-218">Nie reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="10628-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="10628-219">DNS w Internecie serwer odpowiada, ponieważ ta sesja została zainicjowana wewnętrznie, odpowiedź hello jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="10628-219">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="10628-220">Serwer DNS będzie buforować odpowiedź hello i odpowiada tooIIS01 wstecz toohello żądania początkowego</span><span class="sxs-lookup"><span data-stu-id="10628-220">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="10628-221">Nie reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="10628-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="10628-222">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="10628-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="10628-223">Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG</span><span class="sxs-lookup"><span data-stu-id="10628-223">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="10628-224">Hello domyślna systemu reguła zezwala na ruch między podsieciami umożliwiałyby tego rodzaju ruch, ruch hello jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="10628-224">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="10628-225">IIS01 odbiera odpowiedź hello z DNS01</span><span class="sxs-lookup"><span data-stu-id="10628-225">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="10628-226">(*Dozwolone*) pliku dostępu do serwera sieci Web na AppVM01</span><span class="sxs-lookup"><span data-stu-id="10628-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="10628-227">IIS01 żąda pliku na AppVM01</span><span class="sxs-lookup"><span data-stu-id="10628-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="10628-228">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="10628-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="10628-229">podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="10628-229">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="10628-230">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="10628-230">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="10628-231">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="10628-231">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="10628-232">Grupa NSG zasady 3 (Internet tooIIS01) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="10628-232">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="10628-233">Zastosuj 4 reguły NSG (IIS01 tooAppVM01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="10628-233">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="10628-234">AppVM01 odbiera żądanie hello i wysyła plik (przy założeniu, że autoryzacji dostępu)</span><span class="sxs-lookup"><span data-stu-id="10628-234">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="10628-235">Ponieważ na powitania podsieci wewnętrznej bazy danych nie ma żadnych reguł dla ruchu wychodzącego, odpowiedź hello jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="10628-235">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="10628-236">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="10628-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="10628-237">Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG</span><span class="sxs-lookup"><span data-stu-id="10628-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="10628-238">Reguła systemowa domyślne Hello zezwala na ruch między podsieciami umożliwia ruch więc hello ruch jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="10628-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="10628-239">Serwer usług IIS Hello odbiera hello pliku</span><span class="sxs-lookup"><span data-stu-id="10628-239">hello IIS server receives hello file</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="10628-240">(*Odmowa*) serwera sieci Web toobackend</span><span class="sxs-lookup"><span data-stu-id="10628-240">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="10628-241">Użytkownik internet próbuje tooaccess pliku AppVM01 za pośrednictwem hello BackEnd001.CloudApp.Net usługi</span><span class="sxs-lookup"><span data-stu-id="10628-241">An internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="10628-242">Ponieważ nie ma żadnych punktów końcowych otwarty do udziału plików, tego rodzaju ruch nie przejdzie hello usługi w chmurze i nie dostęp powitania serwera</span><span class="sxs-lookup"><span data-stu-id="10628-242">Since there are no endpoints open for file share, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="10628-243">Jeśli punkty końcowe hello były otwarte jakiegoś powodu, reguły NSG 5 (Internet tooVNet) umożliwia zablokowanie tego ruchu</span><span class="sxs-lookup"><span data-stu-id="10628-243">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="10628-244">(*Odmowa*) wyszukiwanie nazwy DNS w sieci Web na serwerze DNS</span><span class="sxs-lookup"><span data-stu-id="10628-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="10628-245">Użytkownik internet próbuje toolook się wewnętrzny rekord DNS na DNS01 za pośrednictwem hello BackEnd001.CloudApp.Net usługi</span><span class="sxs-lookup"><span data-stu-id="10628-245">An internet user tries toolook up an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="10628-246">Ponieważ nie ma żadnych punktów końcowych otwarte dla serwera DNS, tego rodzaju ruch nie przejdzie hello usługi w chmurze i nie dostęp powitania serwera</span><span class="sxs-lookup"><span data-stu-id="10628-246">Since there are no endpoints open for DNS, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="10628-247">Jeśli punkty końcowe hello były otwarte jakiegoś powodu, reguły NSG 5 (Internet tooVNet) umożliwia zablokowanie tego ruchu (Uwaga: nie ma zastosowania tej reguły 1 (DNS) z dwóch przyczyn, pierwszy adres źródłowy hello jest hello internet, ta zasada ma zastosowanie tylko toohello również lokalnej sieci wirtualnej jako hello źródła Ta reguła jest Reguła zezwalająca, nigdy nie będzie go odmówić ruchu)</span><span class="sxs-lookup"><span data-stu-id="10628-247">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="10628-248">(*Odmowa*) tooSQL dostęp za pośrednictwem zapory w sieci Web</span><span class="sxs-lookup"><span data-stu-id="10628-248">(*Denied*) Web tooSQL access through firewall</span></span>
1. <span data-ttu-id="10628-249">Użytkownik internet żąda danych SQL z FrontEnd001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)</span><span class="sxs-lookup"><span data-stu-id="10628-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="10628-250">Ponieważ nie ma żadnych punktów końcowych otwarte dla bazy danych SQL, tego rodzaju ruch nie przejdzie hello usługi w chmurze i nie dotrzeć hello zapory</span><span class="sxs-lookup"><span data-stu-id="10628-250">Since there are no endpoints open for SQL, this traffic would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="10628-251">Jeśli punkty końcowe zostały otwarte jakiegoś powodu, podsieci frontonu hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="10628-251">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="10628-252">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="10628-252">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="10628-253">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="10628-253">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="10628-254">Zastosować grupy NSG zasady 3 (Internet tooIIS01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="10628-254">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="10628-255">Ruch trafienia wewnętrzny adres IP hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="10628-255">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="10628-256">IIS01 nie nasłuchuje na porcie 1433, więc nie ma odpowiedzi toohello żądania</span><span class="sxs-lookup"><span data-stu-id="10628-256">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="10628-257">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="10628-257">Conclusion</span></span>
<span data-ttu-id="10628-258">W tym przykładzie jest stosunkowo proste i bezpośrednio do przodu sposobem izolowanie podsieci wewnętrznej hello z ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="10628-258">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="10628-259">Więcej przykładów i Przegląd granic zabezpieczeń sieci można znaleźć [tutaj][HOME].</span><span class="sxs-lookup"><span data-stu-id="10628-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="10628-260">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="10628-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="10628-261">Główne config skryptu i sieci</span><span class="sxs-lookup"><span data-stu-id="10628-261">Main script and network config</span></span>
<span data-ttu-id="10628-262">Zapisz hello pełne skryptu w pliku skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10628-262">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="10628-263">Zapisz hello konfigurację sieci w pliku o nazwie "NetworkConf1.xml."</span><span class="sxs-lookup"><span data-stu-id="10628-263">Save hello Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="10628-264">Modyfikuj zmienne zdefiniowane przez użytkownika hello jako hello potrzebne i uruchom skrypt.</span><span class="sxs-lookup"><span data-stu-id="10628-264">Modify hello user-defined variables as needed and run hello script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="10628-265">Pełny skrypt</span><span class="sxs-lookup"><span data-stu-id="10628-265">Full script</span></span>
<span data-ttu-id="10628-266">Ten skrypt zostanie, na podstawie zmiennych zdefiniowanych przez użytkownika hello;</span><span class="sxs-lookup"><span data-stu-id="10628-266">This script will, based on hello user-defined variables;</span></span>

1. <span data-ttu-id="10628-267">Połącz tooan subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="10628-267">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="10628-268">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="10628-268">Create a storage account</span></span>
3. <span data-ttu-id="10628-269">Tworzenie sieci wirtualnej z dwoma podsieciami, zgodnie z definicją w pliku konfiguracji sieci hello</span><span class="sxs-lookup"><span data-stu-id="10628-269">Create a VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="10628-270">Tworzenie maszyn wirtualnych serwera cztery systemu windows</span><span class="sxs-lookup"><span data-stu-id="10628-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="10628-271">Skonfiguruj grupy NSG w tym:</span><span class="sxs-lookup"><span data-stu-id="10628-271">Configure NSG including:</span></span>
   * <span data-ttu-id="10628-272">Utworzenie grupy NSG</span><span class="sxs-lookup"><span data-stu-id="10628-272">Creating an NSG</span></span>
   * <span data-ttu-id="10628-273">Zapełnianie reguły</span><span class="sxs-lookup"><span data-stu-id="10628-273">Populating it with rules</span></span>
   * <span data-ttu-id="10628-274">Powiązanie hello NSG toohello odpowiednie podsieci</span><span class="sxs-lookup"><span data-stu-id="10628-274">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="10628-275">Ten skrypt programu PowerShell powinien zostać uruchomiony lokalnie na się, że połączenie internetowe, komputera lub serwera.</span><span class="sxs-lookup"><span data-stu-id="10628-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10628-276">Uruchomienie tego skryptu można ostrzeżenia lub inne komunikaty informacyjne, które pop w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10628-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="10628-277">Tylko komunikaty o błędach na czerwono są przyczyną problemu.</span><span class="sxs-lookup"><span data-stu-id="10628-277">Only error messages in red are cause for concern.</span></span>
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
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

# User-Defined Global Variables
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
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
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
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
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
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="10628-278">Plik konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="10628-278">Network config file</span></span>
<span data-ttu-id="10628-279">Zapisz ten plik xml z lokalizacji zaktualizowane i dodawać hello łącze toothis pliku toohello $NetworkConfigFile zmiennej hello poprzedzających skryptu.</span><span class="sxs-lookup"><span data-stu-id="10628-279">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello preceding script.</span></span>

```XML
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
```

#### <a name="sample-application-scripts"></a><span data-ttu-id="10628-280">Przykładowe skrypty aplikacji</span><span class="sxs-lookup"><span data-stu-id="10628-280">Sample application scripts</span></span>
<span data-ttu-id="10628-281">Jeśli chcesz tooinstall Przykładowa aplikacja dla tego i innych przykłady DMZ, jeden podano na powitania następującego łącza: [przykładowy skrypt aplikacji][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="10628-281">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="10628-282">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10628-282">Next steps</span></span>
* <span data-ttu-id="10628-283">Aktualizowanie i Zapisz plik XML</span><span class="sxs-lookup"><span data-stu-id="10628-283">Update and save XML file</span></span>
* <span data-ttu-id="10628-284">Uruchom hello — środowiska hello toobuild skryptu PowerShell</span><span class="sxs-lookup"><span data-stu-id="10628-284">Run hello PowerShell script toobuild hello environment</span></span>
* <span data-ttu-id="10628-285">Zainstaluj hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="10628-285">Install hello sample application</span></span>
* <span data-ttu-id="10628-286">Testowanie różnych ruch za pośrednictwem tego DMZ</span><span class="sxs-lookup"><span data-stu-id="10628-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Przychodzący DMZ z grupy NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

