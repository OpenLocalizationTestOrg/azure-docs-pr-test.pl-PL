---
title: "aaaAzure przykład DMZ — Tworzenie prostego DMZ z grup NSG | Dokumentacja firmy Microsoft"
description: "Tworzenie DMZ z grup zabezpieczeń sieci (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="f8e12-103">Przykład 1 — Tworzenie prostego DMZ, za pomocą grup NSG z szablonem usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f8e12-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="f8e12-104">[Zwraca toohello strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME]</span><span class="sxs-lookup"><span data-stu-id="f8e12-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8e12-105">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f8e12-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="f8e12-106">Classic — PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8e12-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="f8e12-107">W tym przykładzie tworzy DMZ pierwotnych z czterech serwerów z systemem Windows i grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="f8e12-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="f8e12-108">W tym przykładzie przedstawiono każdy hello odpowiedni szablon sekcje tooprovide głębsze zrozumienie każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="f8e12-108">This example describes each of hello relevant template sections tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="f8e12-109">Istnieje również tooprovide sekcji scenariusza ruchu krok po kroku omówiono sposób obejmującego hello warstw zabezpieczeń w strefie DMZ hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="f8e12-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step look at how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="f8e12-110">Na koniec w sekcji odwołań hello jest pełny szablon hello toobuild kodu i instrukcje tego tootest środowiska i doświadczenia z różnych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="f8e12-110">Finally, in hello references section is hello complete template code and instructions toobuild this environment tootest and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="f8e12-111">![Przychodzący DMZ z grupy NSG][1]</span><span class="sxs-lookup"><span data-stu-id="f8e12-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="f8e12-112">Opis elementu środowiska</span><span class="sxs-lookup"><span data-stu-id="f8e12-112">Environment description</span></span>
<span data-ttu-id="f8e12-113">W tym przykładzie subskrypcja zawiera hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="f8e12-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="f8e12-114">Pojedyncza grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="f8e12-114">A single resource group</span></span>
* <span data-ttu-id="f8e12-115">Sieć wirtualną z dwiema podsieciami; "FrontEnd" i "Wewnętrzna"</span><span class="sxs-lookup"><span data-stu-id="f8e12-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="f8e12-116">Grupy zabezpieczeń sieci jest stosowane tooboth podsieci</span><span class="sxs-lookup"><span data-stu-id="f8e12-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="f8e12-117">Windows Server, który reprezentuje serwer sieci web aplikacji ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="f8e12-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="f8e12-118">Dwóch systemów windows Server, które reprezentują serwery zaplecza aplikacji ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="f8e12-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="f8e12-119">Windows server, który reprezentuje serwer DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="f8e12-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="f8e12-120">Publiczny adres IP skojarzone z serwerem sieci web aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="f8e12-120">A public IP address associated with hello application web server</span></span>

<span data-ttu-id="f8e12-121">W sekcji odwołań hello ma szablonu usługi Azure Resource Manager tooan link, który tworzy środowisko hello opisane w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="f8e12-121">In hello references section, there is a link tooan Azure Resource Manager template that builds hello environment described in this example.</span></span> <span data-ttu-id="f8e12-122">Maszyny wirtualne hello budynku i sieciami wirtualnymi, mimo że wykonywane przez szablon przykład Witaj, nie opisano szczegółowo w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="f8e12-122">Building hello VMs and Virtual Networks, although done by hello example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="f8e12-123">**toobuild to środowisko** (szczegółowe instrukcje znajdują się w sekcji odwołań hello tego dokumentu);</span><span class="sxs-lookup"><span data-stu-id="f8e12-123">**toobuild this environment** (detailed instructions are in hello references section of this document);</span></span>

1. <span data-ttu-id="f8e12-124">Wdrażanie hello szablon Menedżera zasobów Azure w: [szablonów Szybki Start Azure][Template]</span><span class="sxs-lookup"><span data-stu-id="f8e12-124">Deploy hello Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="f8e12-125">Zainstaluj hello przykładową aplikację w: [przykładowy skrypt aplikacji][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="f8e12-125">Install hello sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="f8e12-126">serwerami zaplecza tooany tooRDP w tym wystąpieniu serwera IIS hello jest używany jako "okno przeskoku".</span><span class="sxs-lookup"><span data-stu-id="f8e12-126">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="f8e12-127">Pierwszy serwer IIS toohello RDP i następnie z serwera hello wewnętrznej toohello RDP serwera IIS.</span><span class="sxs-lookup"><span data-stu-id="f8e12-127">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span> <span data-ttu-id="f8e12-128">Alternatywnie publicznego adresu IP może być skojarzony z każdym serwerem kart interfejsu Sieciowego protokołu RDP łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="f8e12-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="f8e12-129">Witaj poniższe sekcje zawierają szczegółowy opis hello sieciowej grupy zabezpieczeń i jak działa w tym przykładzie przez Instruktaż klucza wierszy hello szablon Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e12-129">hello following sections provide a detailed description of hello Network Security Group and how it functions for this example by walking through key lines of hello Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="f8e12-130">Sieciowe grupy zabezpieczeń (NSG)</span><span class="sxs-lookup"><span data-stu-id="f8e12-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="f8e12-131">Na przykład grupy NSG jest wbudowana i następnie ładowane przy użyciu sześciu reguł.</span><span class="sxs-lookup"><span data-stu-id="f8e12-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="f8e12-132">Ogólnie rzecz biorąc należy najpierw utworzyć określonych reguł "Zezwalaj" i następnie ostatnio hello bardziej ogólnym reguły "Deny".</span><span class="sxs-lookup"><span data-stu-id="f8e12-132">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="f8e12-133">Witaj priorytetem nakazują reguły są sprawdzane jako pierwsze.</span><span class="sxs-lookup"><span data-stu-id="f8e12-133">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="f8e12-134">Po znalezieniu tooapply tooa określonej reguły ruchu nie dodatkowe reguły są sprawdzane.</span><span class="sxs-lookup"><span data-stu-id="f8e12-134">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="f8e12-135">Reguły NSG można zastosować w hello kierunek ruchu przychodzącego lub wychodzącego (z perspektywy hello hello podsieci).</span><span class="sxs-lookup"><span data-stu-id="f8e12-135">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
>
>

<span data-ttu-id="f8e12-136">Deklaratywnie hello następujące reguły są tworzone dla ruchu przychodzącego:</span><span class="sxs-lookup"><span data-stu-id="f8e12-136">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="f8e12-137">Wewnętrzny ruch DNS (port 53) jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="f8e12-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="f8e12-138">Ruch protokołu RDP (port 3389) z tooany Internet hello maszyny Wirtualnej jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="f8e12-138">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="f8e12-139">Ruch HTTP (port 80) z serwera tooweb internetowej hello (IIS01) jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="f8e12-139">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="f8e12-140">Cały ruch (wszystkie porty) z IIS01 tooAppVM1 jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="f8e12-140">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="f8e12-141">Cały ruch (wszystkie porty) z hello Internet toohello odmowa całej sieci wirtualnej (obie podsieci)</span><span class="sxs-lookup"><span data-stu-id="f8e12-141">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="f8e12-142">Cały ruch (wszystkie porty) z podsieci wewnętrznej bazy danych toohello podsieci frontonu hello jest zabroniony</span><span class="sxs-lookup"><span data-stu-id="f8e12-142">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="f8e12-143">Z tych podsieci tooeach powiązane zasady, jeśli żądanie HTTP zostało ruch przychodzący z serwera sieci web toohello Internet hello zarówno 3 reguły (Zezwalaj) i 5 (odmówić go) będą miały zastosowania, ale ponieważ reguła 3 ma wyższy priorytet tylko będą miały zastosowania i reguły 5 nie przybyły do gry.</span><span class="sxs-lookup"><span data-stu-id="f8e12-143">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="f8e12-144">W związku z tym żądania HTTP hello mogliby toohello serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="f8e12-144">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="f8e12-145">Jeśli ten sam ruch próbował tooreach hello DNS01 serwer, reguła 5 (odmowa) mogą być hello pierwszy tooapply hello ruch w sieci i nie będzie dozwolone toopass toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="f8e12-145">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="f8e12-146">Reguła 6 (Odmów) blokuje hello podsieci frontonu z mówić toohello podsieci wewnętrznej bazy danych (z wyjątkiem dozwolonego ruchu w regułach 1 i 4), ten zestaw reguł chroni hello sieci wewnętrznej bazy danych w przypadku, gdy osoba atakująca dokonywania hello aplikacji sieci web na powitania serwera sieci Web, osoba atakująca hello czy ograniczona toohello dostępu do sieci (tylko tooresources udostępniane na serwerze AppVM01 hello) wewnętrznej bazy danych "protected".</span><span class="sxs-lookup"><span data-stu-id="f8e12-146">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="f8e12-147">Brak domyślnej regule wychodzącej, która umożliwia ruchu wychodzącego toohello internet.</span><span class="sxs-lookup"><span data-stu-id="f8e12-147">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="f8e12-148">Na przykład firma Microsoft zezwala na ruch wychodzący i nie modyfikowanie reguł wychodzących.</span><span class="sxs-lookup"><span data-stu-id="f8e12-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="f8e12-149">tooapply tootraffic zasad zabezpieczeń w obu kierunkach, Routing zdefiniowany przez użytkownika jest wymagany i jest przedstawione w "W przykładzie 3" na powitania [strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME].</span><span class="sxs-lookup"><span data-stu-id="f8e12-149">tooapply security policy tootraffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="f8e12-150">Każda reguła omówiono bardziej szczegółowo w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f8e12-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="f8e12-151">Zasób grupy zabezpieczeń sieci musi być skonkretyzowanym toohold hello reguł:</span><span class="sxs-lookup"><span data-stu-id="f8e12-151">A Network Security Group resource must be instantiated toohold hello rules:</span></span>

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. <span data-ttu-id="f8e12-152">Pierwsza reguła Hello w tym przykładzie zezwala na ruch DNS między wszystkich serwerów DNS toohello sieciach wewnętrznych hello podsieci wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f8e12-152">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="f8e12-153">Reguła Hello zawiera niektóre ważne parametry:</span><span class="sxs-lookup"><span data-stu-id="f8e12-153">hello rule has some important parameters:</span></span>
  * <span data-ttu-id="f8e12-154">"destinationAddressPrefix" - reguły można używać specjalnego typu o nazwie "Domyślna Tag" prefiksu adresu, tagi te są dostarczane przez system identyfikatorów, które umożliwia tooaddress łatwy sposób większych kategorii prefiksy adresów.</span><span class="sxs-lookup"><span data-stu-id="f8e12-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way tooaddress a larger category of address prefixes.</span></span> <span data-ttu-id="f8e12-155">Ta zasada domyślna Tag "Internet" hello używa toosignify żadnego adresu poza hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f8e12-155">This rule uses hello Default Tag “Internet” toosignify any address outside of hello VNet.</span></span> <span data-ttu-id="f8e12-156">Inne etykiety prefiks są VirtualNetwork i AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="f8e12-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="f8e12-157">"Direction" oznacza, że w kierunku przepływu ruchu obowiązuje tej reguły.</span><span class="sxs-lookup"><span data-stu-id="f8e12-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="f8e12-158">Kierunek Hello jest z punktu widzenia hello hello podsieci lub maszyny wirtualnej (w zależności od tego, gdzie jest powiązany ten NSG).</span><span class="sxs-lookup"><span data-stu-id="f8e12-158">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="f8e12-159">W związku z tym jeśli "Przychodzącego" jest skierowany i ruchu jest wprowadzanie hello podsieci, powinna zostać zastosowana reguła hello i ruchu wychodzącego hello podsieci nie może niekorzystnie wpływać tej reguły.</span><span class="sxs-lookup"><span data-stu-id="f8e12-159">Thus if Direction is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="f8e12-160">"Priority" Ustawia kolejność hello, w jakiej są oceniane przepływu ruchu.</span><span class="sxs-lookup"><span data-stu-id="f8e12-160">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="f8e12-161">Witaj niższe hello numer hello wyższy hello priorytet.</span><span class="sxs-lookup"><span data-stu-id="f8e12-161">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="f8e12-162">Jeśli reguła ma zastosowanie tooa przepływu ruchu, żadne dalsze reguły są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="f8e12-162">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="f8e12-163">W związku z tym jeśli reguła o priorytecie 1 zezwala na ruch i reguły o priorytecie 2 nie zezwala na ruch i tootraffic mają zastosowanie zarówno reguły, a następnie hello ruch będzie dozwolony tooflow (ponieważ reguła 1 ma wyższy priorytet trwało efektu i żadne dodatkowe reguły zostały zastosowane).</span><span class="sxs-lookup"><span data-stu-id="f8e12-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="f8e12-164">"Access" oznacza, że jeśli wpływ ta reguła jest zablokowane ("Deny") lub dozwolonych ("Zezwalaj").</span><span class="sxs-lookup"><span data-stu-id="f8e12-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. <span data-ttu-id="f8e12-165">Ta zasada umożliwia tooflow ruchu protokołu RDP z portem RDP toohello internet hello na dowolnym serwerze na powitania powiązany podsieci.</span><span class="sxs-lookup"><span data-stu-id="f8e12-165">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. <span data-ttu-id="f8e12-166">Ta zasada umożliwia przychodzący serwera sieci web hello toohit internet ruchu.</span><span class="sxs-lookup"><span data-stu-id="f8e12-166">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="f8e12-167">Ta zasada nie zmienia hello zachowanie routingu.</span><span class="sxs-lookup"><span data-stu-id="f8e12-167">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="f8e12-168">zasada Hello umożliwia tylko ruch kierowany do IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="f8e12-168">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="f8e12-169">W związku z tym jeśli ruch z hello Internet miał powitania serwera sieci web jako miejsca docelowego tej reguły spowoduje zezwolenie i zatrzymać dalsze przetwarzanie reguł.</span><span class="sxs-lookup"><span data-stu-id="f8e12-169">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="f8e12-170">(W regule hello priorytetem 140 wszystkich innych przychodzącego ruchu internetowego jest zablokowane).</span><span class="sxs-lookup"><span data-stu-id="f8e12-170">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="f8e12-171">Jeśli jest tylko przetwarzania ruchu HTTP, ta zasada może być dalsze ograniczeniami tooonly Zezwalaj docelowy Port 80.</span><span class="sxs-lookup"><span data-stu-id="f8e12-171">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. <span data-ttu-id="f8e12-172">Ta zasada umożliwia toopass ruchu z serwera IIS01 powitania serwera AppVM01 toohello, nowsze reguła blokuje cały ruch tooBackend frontonu.</span><span class="sxs-lookup"><span data-stu-id="f8e12-172">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="f8e12-173">tooimprove tej reguły, jeśli znane jest hello portu, który powinien zostać dodane.</span><span class="sxs-lookup"><span data-stu-id="f8e12-173">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="f8e12-174">Na przykład, jeśli serwer IIS hello jest naciśnięcie tylko programu SQL Server na AppVM01, zakres portów docelowych hello należy zmienić "*" (Any) too1433 (hello SQL port) dzięki czemu mniejsze przychodzących ataki AppVM01 aplikacji sieci web hello kiedykolwiek zagrożenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="f8e12-174">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. <span data-ttu-id="f8e12-175">Ta reguła nie zezwala na ruch z hello internet tooany serwerów w sieci hello.</span><span class="sxs-lookup"><span data-stu-id="f8e12-175">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="f8e12-176">Przy użyciu reguł hello priorytetem 110 i 120 efekt hello jest tooallow tylko dla ruchu przychodzącego ruchu toohello zapory internetowej i porty protokołu RDP na serwerach i blokuje wszystkie inne elementy.</span><span class="sxs-lookup"><span data-stu-id="f8e12-176">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="f8e12-177">Ta reguła jest "awaryjnie" reguły tooblock wszystkie przepływy nieoczekiwany.</span><span class="sxs-lookup"><span data-stu-id="f8e12-177">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. <span data-ttu-id="f8e12-178">Reguła końcowego Hello nie zezwala na ruch z podsieci wewnętrznej bazy danych toohello podsieci frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="f8e12-178">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="f8e12-179">Ponieważ ta reguła jest tylko regułę ruchu przychodzącego, odwrotnej ruch jest dozwolony (od toohello zaplecza hello frontonu).</span><span class="sxs-lookup"><span data-stu-id="f8e12-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="f8e12-180">Scenariusze ruchu</span><span class="sxs-lookup"><span data-stu-id="f8e12-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="f8e12-181">(*Dozwolone*) Internet tooweb serwera</span><span class="sxs-lookup"><span data-stu-id="f8e12-181">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="f8e12-182">Użytkownik internet zażąda strony HTTP od hello publicznego adresu IP karty Sieciowej skojarzonych z hello kart IIS01 powitalne</span><span class="sxs-lookup"><span data-stu-id="f8e12-182">An internet user requests an HTTP page from hello public IP address of hello NIC associated with hello IIS01 NIC</span></span>
2. <span data-ttu-id="f8e12-183">Hello publicznego adresu IP przekazuje ruch toohello sieci wirtualnej kierunku IIS01 (powitania serwera sieci web)</span><span class="sxs-lookup"><span data-stu-id="f8e12-183">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="f8e12-184">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="f8e12-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="f8e12-185">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="f8e12-185">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="f8e12-186">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="f8e12-186">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="f8e12-187">Zastosować grupy NSG zasady 3 (Internet tooIIS01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="f8e12-187">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="f8e12-188">Ruch trafienia wewnętrzny adres IP serwera sieci web hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="f8e12-188">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="f8e12-189">IIS01 nasłuchuje ruchu w sieci web, otrzymuje tego żądania i rozpoczyna przetwarzanie żądania hello</span><span class="sxs-lookup"><span data-stu-id="f8e12-189">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="f8e12-190">IIS01 hello programu SQL Server na AppVM01 monituje o podanie informacji</span><span class="sxs-lookup"><span data-stu-id="f8e12-190">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="f8e12-191">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="f8e12-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="f8e12-192">podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="f8e12-192">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="f8e12-193">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="f8e12-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="f8e12-194">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="f8e12-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="f8e12-195">Grupa NSG zasady 3 (Internet tooFirewall) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="f8e12-195">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="f8e12-196">Zastosuj 4 reguły NSG (IIS01 tooAppVM01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="f8e12-196">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="f8e12-197">AppVM01 odbiera hello zapytanie SQL i odpowiada</span><span class="sxs-lookup"><span data-stu-id="f8e12-197">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="f8e12-198">Ponieważ na powitania podsieci wewnętrznej bazy danych nie ma żadnych reguł dla ruchu wychodzącego, odpowiedź hello jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="f8e12-198">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="f8e12-199">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="f8e12-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="f8e12-200">Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG</span><span class="sxs-lookup"><span data-stu-id="f8e12-200">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="f8e12-201">Reguła systemowa domyślne Hello zezwala na ruch między podsieciami umożliwia ruch więc hello ruch jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="f8e12-201">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="f8e12-202">Serwer usług IIS Hello odbiera odpowiedź SQL hello i kończy odpowiedź HTTP hello i przesyła toohello. strona żądająca</span><span class="sxs-lookup"><span data-stu-id="f8e12-202">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requester</span></span>
13. <span data-ttu-id="f8e12-203">Ponieważ nie ma żadnych reguł dla ruchu wychodzącego w podsieci frontonu hello, odpowiedź hello jest dozwolone i hello Internet użytkownik otrzymuje hello strona sieci web.</span><span class="sxs-lookup"><span data-stu-id="f8e12-203">Since there are no outbound rules on hello Frontend subnet, hello response is allowed and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-tooiis-server"></a><span data-ttu-id="f8e12-204">(*Dozwolone*) serwera tooIIS RDP</span><span class="sxs-lookup"><span data-stu-id="f8e12-204">(*Allowed*) RDP tooIIS server</span></span>
1. <span data-ttu-id="f8e12-205">TooIIS01 sesji protokołu RDP na powitania publicznego adresu IP karty Sieciowej skojarzonych z hello IIS01 karty Sieciowej (ten publiczny adres IP znajduje się za pośrednictwem hello portalu lub programu PowerShell) powitalne żąda uprawnień administratora serwera w Internecie</span><span class="sxs-lookup"><span data-stu-id="f8e12-205">A Server Admin on internet requests an RDP session tooIIS01 on hello public IP address of hello NIC associated with hello IIS01 NIC (this public IP address can be found via hello Portal or PowerShell)</span></span>
2. <span data-ttu-id="f8e12-206">Hello publicznego adresu IP przekazuje ruch toohello sieci wirtualnej kierunku IIS01 (powitania serwera sieci web)</span><span class="sxs-lookup"><span data-stu-id="f8e12-206">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="f8e12-207">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="f8e12-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="f8e12-208">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="f8e12-208">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="f8e12-209">Zastosuj 2 reguły NSG (RDP), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="f8e12-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="f8e12-210">Z nie reguł dla ruchu wychodzącego Zastosuj reguły domyślne i zwracany ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="f8e12-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="f8e12-211">Włączono sesji protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="f8e12-211">RDP session is enabled</span></span>
6. <span data-ttu-id="f8e12-212">IIS01 monit o podanie hello nazwy użytkownika i hasła</span><span class="sxs-lookup"><span data-stu-id="f8e12-212">IIS01 prompts for hello user name and password</span></span>

>[!NOTE]
><span data-ttu-id="f8e12-213">serwerami zaplecza tooany tooRDP w tym wystąpieniu serwera IIS hello jest używany jako "okno przeskoku".</span><span class="sxs-lookup"><span data-stu-id="f8e12-213">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="f8e12-214">Pierwszy serwer IIS toohello RDP i następnie z serwera hello wewnętrznej toohello RDP serwera IIS.</span><span class="sxs-lookup"><span data-stu-id="f8e12-214">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="f8e12-215">(*Dozwolone*) wyszukiwanie nazwy DNS serwera sieci Web na serwerze DNS</span><span class="sxs-lookup"><span data-stu-id="f8e12-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="f8e12-216">Serwer, IIS01, musi na www.data.gov strumieniowego źródła danych w sieci Web, ale wymaga tooresolve hello adres.</span><span class="sxs-lookup"><span data-stu-id="f8e12-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="f8e12-217">Hello konfiguracji sieci dla listy sieci wirtualnej hello DNS01 (10.0.2.4 podsieci wewnętrznej bazy danych hello) jako podstawowy serwer DNS hello IIS01 wysyła tooDNS01 żądania DNS hello</span><span class="sxs-lookup"><span data-stu-id="f8e12-217">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="f8e12-218">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="f8e12-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="f8e12-219">Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="f8e12-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="f8e12-220">Zastosuj reguły NSG 1 DNS (Domain Name System), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="f8e12-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="f8e12-221">Serwer DNS odbiera żądanie hello</span><span class="sxs-lookup"><span data-stu-id="f8e12-221">DNS server receives hello request</span></span>
6. <span data-ttu-id="f8e12-222">Serwer DNS nie ma adresu hello w pamięci podręcznej i prosi o główny serwer DNS na powitania internet</span><span class="sxs-lookup"><span data-stu-id="f8e12-222">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="f8e12-223">Nie reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="f8e12-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="f8e12-224">DNS w Internecie serwer odpowiada, ponieważ ta sesja została zainicjowana wewnętrznie, odpowiedź hello jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="f8e12-224">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="f8e12-225">Serwer DNS będzie buforować odpowiedź hello i odpowiada tooIIS01 wstecz toohello żądania początkowego</span><span class="sxs-lookup"><span data-stu-id="f8e12-225">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="f8e12-226">Nie reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="f8e12-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="f8e12-227">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="f8e12-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="f8e12-228">Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG</span><span class="sxs-lookup"><span data-stu-id="f8e12-228">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="f8e12-229">Hello domyślna systemu reguła zezwala na ruch między podsieciami umożliwiałyby tego rodzaju ruch, ruch hello jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="f8e12-229">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="f8e12-230">IIS01 odbiera odpowiedź hello z DNS01</span><span class="sxs-lookup"><span data-stu-id="f8e12-230">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="f8e12-231">(*Dozwolone*) pliku dostępu do serwera sieci Web na AppVM01</span><span class="sxs-lookup"><span data-stu-id="f8e12-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="f8e12-232">IIS01 żąda pliku na AppVM01</span><span class="sxs-lookup"><span data-stu-id="f8e12-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="f8e12-233">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="f8e12-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="f8e12-234">podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="f8e12-234">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="f8e12-235">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="f8e12-235">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="f8e12-236">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="f8e12-236">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="f8e12-237">Grupa NSG zasady 3 (Internet tooIIS01) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="f8e12-237">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="f8e12-238">Zastosuj 4 reguły NSG (IIS01 tooAppVM01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="f8e12-238">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="f8e12-239">AppVM01 odbiera żądanie hello i wysyła plik (przy założeniu, że autoryzacji dostępu)</span><span class="sxs-lookup"><span data-stu-id="f8e12-239">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="f8e12-240">Ponieważ na powitania podsieci wewnętrznej bazy danych nie ma żadnych reguł dla ruchu wychodzącego, odpowiedź hello jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="f8e12-240">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="f8e12-241">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="f8e12-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="f8e12-242">Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG</span><span class="sxs-lookup"><span data-stu-id="f8e12-242">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="f8e12-243">Reguła systemowa domyślne Hello zezwala na ruch między podsieciami umożliwia ruch więc hello ruch jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="f8e12-243">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="f8e12-244">Serwer usług IIS Hello odbiera hello pliku</span><span class="sxs-lookup"><span data-stu-id="f8e12-244">hello IIS server receives hello file</span></span>

#### <a name="denied-rdp-toobackend"></a><span data-ttu-id="f8e12-245">(*Odmowa*) toobackend protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="f8e12-245">(*Denied*) RDP toobackend</span></span>
1. <span data-ttu-id="f8e12-246">Użytkownik internet próbuje tooRDP tooserver AppVM01</span><span class="sxs-lookup"><span data-stu-id="f8e12-246">An internet user tries tooRDP tooserver AppVM01</span></span>
2. <span data-ttu-id="f8e12-247">Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić hello sieci wirtualnej i nie dostęp powitania serwera</span><span class="sxs-lookup"><span data-stu-id="f8e12-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="f8e12-248">Jednak jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, reguły NSG 2 (RDP) umożliwiałyby ten ruch</span><span class="sxs-lookup"><span data-stu-id="f8e12-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="f8e12-249">serwerami zaplecza tooany tooRDP w tym wystąpieniu serwera IIS hello jest używany jako "okno przeskoku".</span><span class="sxs-lookup"><span data-stu-id="f8e12-249">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="f8e12-250">Pierwszy serwer IIS toohello RDP i następnie z serwera hello wewnętrznej toohello RDP serwera IIS.</span><span class="sxs-lookup"><span data-stu-id="f8e12-250">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="f8e12-251">(*Odmowa*) serwera sieci Web toobackend</span><span class="sxs-lookup"><span data-stu-id="f8e12-251">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="f8e12-252">Użytkownik internet próbuje tooaccess pliku na AppVM01</span><span class="sxs-lookup"><span data-stu-id="f8e12-252">An internet user tries tooaccess a file on AppVM01</span></span>
2. <span data-ttu-id="f8e12-253">Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić hello sieci wirtualnej i nie dostęp powitania serwera</span><span class="sxs-lookup"><span data-stu-id="f8e12-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="f8e12-254">Jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, reguły NSG 5 (Internet tooVNet) czy zablokować ruch</span><span class="sxs-lookup"><span data-stu-id="f8e12-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="f8e12-255">(*Odmowa*) wyszukiwanie nazwy DNS w sieci Web na serwerze DNS</span><span class="sxs-lookup"><span data-stu-id="f8e12-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="f8e12-256">Użytkownik internet próbuje toolook się wewnętrzny rekord DNS na DNS01</span><span class="sxs-lookup"><span data-stu-id="f8e12-256">An internet user tries toolook up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="f8e12-257">Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić hello sieci wirtualnej i nie dostęp powitania serwera</span><span class="sxs-lookup"><span data-stu-id="f8e12-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="f8e12-258">Jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, reguły NSG 5 (Internet tooVNet) czy zablokować ruch (Uwaga: Aby reguła 1 (DNS) nie będą miały zastosowania ponieważ hello żądania adresu źródłowego jest hello internet i 1 reguła ma zastosowanie tylko toohello lokalnej sieci wirtualnej jako źródło hello)</span><span class="sxs-lookup"><span data-stu-id="f8e12-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because hello requests source address is hello internet and Rule 1 only applies toohello local VNet as hello source)</span></span>

#### <a name="denied-sql-access-on-hello-web-server"></a><span data-ttu-id="f8e12-259">(*Odmowa*) dostępu SQL na serwerze sieci web hello</span><span class="sxs-lookup"><span data-stu-id="f8e12-259">(*Denied*) SQL access on hello web server</span></span>
1. <span data-ttu-id="f8e12-260">Użytkownik internet żąda danych SQL z IIS01</span><span class="sxs-lookup"><span data-stu-id="f8e12-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="f8e12-261">Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić hello sieci wirtualnej i nie dostęp powitania serwera</span><span class="sxs-lookup"><span data-stu-id="f8e12-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="f8e12-262">Jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, podsieci frontonu hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="f8e12-262">If a Public IP address was enabled for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="f8e12-263">Reguły NSG 1 DNS (Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="f8e12-263">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="f8e12-264">2 reguły NSG (RDP) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="f8e12-264">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="f8e12-265">Zastosować grupy NSG zasady 3 (Internet tooIIS01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="f8e12-265">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="f8e12-266">Ruch trafienia wewnętrzny adres IP hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="f8e12-266">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="f8e12-267">IIS01 nie nasłuchuje na porcie 1433, więc nie ma odpowiedzi toohello żądania</span><span class="sxs-lookup"><span data-stu-id="f8e12-267">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="f8e12-268">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f8e12-268">Conclusion</span></span>
<span data-ttu-id="f8e12-269">W tym przykładzie jest stosunkowo proste i bezpośrednio do przodu sposobem izolowanie podsieci wewnętrznej hello z ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="f8e12-269">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="f8e12-270">Więcej przykładów i Przegląd granic zabezpieczeń sieci można znaleźć [tutaj][HOME].</span><span class="sxs-lookup"><span data-stu-id="f8e12-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="f8e12-271">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="f8e12-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="f8e12-272">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f8e12-272">Azure Resource Manager template</span></span>
<span data-ttu-id="f8e12-273">W tym przykładzie używa wstępnie zdefiniowanych szablonów usługi Azure Resource Manager w repozytorium GitHub obsługiwanego przez firmę Microsoft i otworzyć toohello społeczności.</span><span class="sxs-lookup"><span data-stu-id="f8e12-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="f8e12-274">Tego szablonu można wdrożyć bezpośrednio z witryny GitHub, lub pobrane i zmodyfikować toofit potrzeb.</span><span class="sxs-lookup"><span data-stu-id="f8e12-274">This template can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> 

<span data-ttu-id="f8e12-275">Szablon głównego Hello znajduje się w pliku hello o nazwie "azuredeploy.json."</span><span class="sxs-lookup"><span data-stu-id="f8e12-275">hello main template is in hello file named "azuredeploy.json."</span></span> <span data-ttu-id="f8e12-276">Ten szablon może zostać przesłane za pomocą programu PowerShell lub interfejsu wiersza polecenia (z plikiem skojarzone "azuredeploy.parameters.json" hello) toodeploy tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="f8e12-276">This template can be submitted via PowerShell or CLI (with hello associated "azuredeploy.parameters.json" file) toodeploy this template.</span></span> <span data-ttu-id="f8e12-277">Mogę znaleźć hello najprostszą metodą jest hello toouse przycisku "Wdróż tooAzure" na stronie README.md hello w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8e12-277">I find hello easiest way is toouse hello "Deploy tooAzure" button on hello README.md page at GitHub.</span></span>

<span data-ttu-id="f8e12-278">toodeploy hello szablon, który tworzy w tym przykładzie z serwisu GitHub i hello portalu Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f8e12-278">toodeploy hello template that builds this example from GitHub and hello Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="f8e12-279">W przeglądarce Przejdź toohello [szablonu][Template]</span><span class="sxs-lookup"><span data-stu-id="f8e12-279">From a browser, navigate toohello [Template][Template]</span></span>
2. <span data-ttu-id="f8e12-280">Kliknij przycisk "Wdróż tooAzure" hello (lub toosee przycisk "Wizualizacja" hello graficzną reprezentację tego szablonu)</span><span class="sxs-lookup"><span data-stu-id="f8e12-280">Click hello "Deploy tooAzure" button (or hello "Visualize" button toosee a graphical representation of this template)</span></span>
3. <span data-ttu-id="f8e12-281">Wprowadź w bloku parametrów hello hello konta magazynu, nazwę użytkownika i hasło, a następnie kliknij przycisk **OK**</span><span class="sxs-lookup"><span data-stu-id="f8e12-281">Enter hello Storage Account, User Name, and Password in hello Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="f8e12-282">Utwórz grupę zasobów dla tego wdrożenia (można użyć istniejącego, ale zalecane jest nowy, aby uzyskać najlepsze wyniki)</span><span class="sxs-lookup"><span data-stu-id="f8e12-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="f8e12-283">W razie potrzeby zmień ustawienia subskrypcji i lokalizacji hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f8e12-283">If necessary, change hello Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="f8e12-284">Kliknij przycisk **Przejrzyj postanowienia prawne**, przeczytaj warunki hello i kliknij przycisk **zakupu** tooagree.</span><span class="sxs-lookup"><span data-stu-id="f8e12-284">Click **Review legal terms**, read hello terms, and click **Purchase** tooagree.</span></span>
8. <span data-ttu-id="f8e12-285">Kliknij przycisk **Utwórz** toobegin hello wdrożenia tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="f8e12-285">Click **Create** toobegin hello deployment of this template.</span></span>
9. <span data-ttu-id="f8e12-286">Po hello wdrożenie zakończy się pomyślnie, przejdź toohello utworzone dla tego wdrożenia zasobów hello toosee skonfigurowane wewnątrz grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="f8e12-286">Once hello deployment finishes successfully, navigate toohello Resource Group created for this deployment toosee hello resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="f8e12-287">Ten szablon umożliwia RDP toohello IIS01 serwera tylko (hello Znajdź publicznego adresu IP dla IIS01 na powitania portalu).</span><span class="sxs-lookup"><span data-stu-id="f8e12-287">This template enables RDP toohello IIS01 server only (find hello Public IP for IIS01 on hello Portal).</span></span> <span data-ttu-id="f8e12-288">serwerami zaplecza tooany tooRDP w tym wystąpieniu serwera IIS hello jest używany jako "okno przeskoku".</span><span class="sxs-lookup"><span data-stu-id="f8e12-288">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="f8e12-289">Pierwszy serwer IIS toohello RDP i następnie z serwera hello wewnętrznej toohello RDP serwera IIS.</span><span class="sxs-lookup"><span data-stu-id="f8e12-289">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

<span data-ttu-id="f8e12-290">tooremove tego wdrożenia, Usuń hello grupy zasobów i wszystkie zasoby podrzędne zostaną również usunięte.</span><span class="sxs-lookup"><span data-stu-id="f8e12-290">tooremove this deployment, delete hello Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="f8e12-291">Przykładowe skrypty aplikacji</span><span class="sxs-lookup"><span data-stu-id="f8e12-291">Sample application scripts</span></span>
<span data-ttu-id="f8e12-292">Po pomyślnym uruchomieniu szablonu hello, musisz skonfigurować powitania serwera sieci web i serwera aplikacji tooallow aplikacji sieci web proste, testowanie za pomocą tej konfiguracji DMZ.</span><span class="sxs-lookup"><span data-stu-id="f8e12-292">Once hello template runs successfully, you can set up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span> <span data-ttu-id="f8e12-293">tooinstall przykładowej aplikacji to i inne przykłady DMZ jedną dostarczono na powitania następującego łącza: [przykładowy skrypt aplikacji][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="f8e12-293">tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8e12-294">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f8e12-294">Next steps</span></span>

* <span data-ttu-id="f8e12-295">W tym przykładzie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f8e12-295">Deploy this example</span></span>
* <span data-ttu-id="f8e12-296">Tworzenie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="f8e12-296">Build hello sample application</span></span>
* <span data-ttu-id="f8e12-297">Testowanie różnych ruch za pośrednictwem tego DMZ</span><span class="sxs-lookup"><span data-stu-id="f8e12-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Przychodzący DMZ z grupy NSG"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md