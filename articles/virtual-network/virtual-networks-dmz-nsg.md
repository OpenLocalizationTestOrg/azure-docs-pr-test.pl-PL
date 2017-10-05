---
title: "Przykład DMZ Azure — Tworzenie prostego DMZ z grup NSG | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ec29e6b250f927a3a4a94ffdf83d6c7c0e325722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="e958a-103">Przykład 1 — Tworzenie prostego DMZ, za pomocą grup NSG z szablonem usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e958a-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="e958a-104">[Wróć do strony zabezpieczeń granic najlepsze praktyki][HOME]</span><span class="sxs-lookup"><span data-stu-id="e958a-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e958a-105">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e958a-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="e958a-106">Classic — PowerShell</span><span class="sxs-lookup"><span data-stu-id="e958a-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="e958a-107">W tym przykładzie tworzy DMZ pierwotnych z czterech serwerów z systemem Windows i grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="e958a-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="e958a-108">W tym przykładzie przedstawiono sekcjach odpowiedni szablon zapewnienie głębsze zrozumienie każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="e958a-108">This example describes each of the relevant template sections to provide a deeper understanding of each step.</span></span> <span data-ttu-id="e958a-109">Brak sekcji scenariusza ruchu zapewnienie krok po kroku omówiono sposób ruch będzie kontynuowana za pośrednictwem warstw zabezpieczeń w strefie DMZ.</span><span class="sxs-lookup"><span data-stu-id="e958a-109">There is also a Traffic Scenario section to provide an in-depth step-by-step look at how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="e958a-110">Na koniec w odwołaniach sekcja jest kod pełną szablonu i instrukcje dotyczące tworzenia tego środowiska, aby przetestować i wypróbować różne scenariusze.</span><span class="sxs-lookup"><span data-stu-id="e958a-110">Finally, in the references section is the complete template code and instructions to build this environment to test and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="e958a-111">![Przychodzący DMZ z grupy NSG][1]</span><span class="sxs-lookup"><span data-stu-id="e958a-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="e958a-112">Opis elementu środowiska</span><span class="sxs-lookup"><span data-stu-id="e958a-112">Environment description</span></span>
<span data-ttu-id="e958a-113">W tym przykładzie subskrypcja zawiera następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="e958a-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="e958a-114">Pojedyncza grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="e958a-114">A single resource group</span></span>
* <span data-ttu-id="e958a-115">Sieć wirtualną z dwiema podsieciami; "FrontEnd" i "Wewnętrzna"</span><span class="sxs-lookup"><span data-stu-id="e958a-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="e958a-116">Grupy zabezpieczeń sieci jest stosowany do obu podsieci</span><span class="sxs-lookup"><span data-stu-id="e958a-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="e958a-117">Windows Server, który reprezentuje serwer sieci web aplikacji ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="e958a-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="e958a-118">Dwóch systemów windows Server, które reprezentują serwery zaplecza aplikacji ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="e958a-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="e958a-119">Windows server, który reprezentuje serwer DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="e958a-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="e958a-120">Publiczny adres IP skojarzone z serwerem aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="e958a-120">A public IP address associated with the application web server</span></span>

<span data-ttu-id="e958a-121">W sekcji odwołań ma łącza do szablonu usługi Azure Resource Manager, który tworzy środowisko opisane w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="e958a-121">In the references section, there is a link to an Azure Resource Manager template that builds the environment described in this example.</span></span> <span data-ttu-id="e958a-122">Tworzenie maszyn wirtualnych i sieci wirtualnych, mimo że wykonywane przez szablon przykład nie opisano szczegółowo w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="e958a-122">Building the VMs and Virtual Networks, although done by the example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="e958a-123">**Do tworzenia tego środowiska** (szczegółowe informacje znajdują się w sekcji odwołań tego dokumentu);</span><span class="sxs-lookup"><span data-stu-id="e958a-123">**To build this environment** (detailed instructions are in the references section of this document);</span></span>

1. <span data-ttu-id="e958a-124">Wdrażanie szablonu Azure Resource Manager w: [szablonów Szybki Start Azure][Template]</span><span class="sxs-lookup"><span data-stu-id="e958a-124">Deploy the Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="e958a-125">Instalowanie przykładowej aplikacji w: [przykładowy skrypt aplikacji][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="e958a-125">Install the sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="e958a-126">Dla protokołu RDP do serwerów zaplecza w tym wystąpieniu na serwerze usług IIS jest używana jako "okno przeskoku".</span><span class="sxs-lookup"><span data-stu-id="e958a-126">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="e958a-127">Pierwszy RDP do serwera IIS, a następnie z RDP serwera usług IIS do serwera zaplecza.</span><span class="sxs-lookup"><span data-stu-id="e958a-127">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span> <span data-ttu-id="e958a-128">Alternatywnie publicznego adresu IP może być skojarzony z każdym serwerem kart interfejsu Sieciowego protokołu RDP łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="e958a-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="e958a-129">Poniższe sekcje zawierają szczegółowy opis grupy zabezpieczeń sieci i jak działa w tym przykładzie przez Instruktaż klucza wierszy szablon Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="e958a-129">The following sections provide a detailed description of the Network Security Group and how it functions for this example by walking through key lines of the Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="e958a-130">Sieciowe grupy zabezpieczeń (NSG)</span><span class="sxs-lookup"><span data-stu-id="e958a-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="e958a-131">Na przykład grupy NSG jest wbudowana i następnie ładowane przy użyciu sześciu reguł.</span><span class="sxs-lookup"><span data-stu-id="e958a-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="e958a-132">Ogólnie rzecz biorąc należy najpierw utworzyć określonych reguł "Zezwalaj", a następnie ostatni bardziej ogólnym reguły "Deny".</span><span class="sxs-lookup"><span data-stu-id="e958a-132">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="e958a-133">Określają priorytetem, do których zasady są oceniane pierwszej.</span><span class="sxs-lookup"><span data-stu-id="e958a-133">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="e958a-134">Po znalezieniu ruchu do zastosowania do określonej reguły nie dalsze reguły są sprawdzane.</span><span class="sxs-lookup"><span data-stu-id="e958a-134">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="e958a-135">Reguły NSG można zastosować w jednym kierunku ruchu przychodzącego lub wychodzącego (z punktu widzenia podsieci).</span><span class="sxs-lookup"><span data-stu-id="e958a-135">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
>
>

<span data-ttu-id="e958a-136">Deklaratywnie są tworzone następujące reguły dla ruchu przychodzącego:</span><span class="sxs-lookup"><span data-stu-id="e958a-136">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="e958a-137">Wewnętrzny ruch DNS (port 53) jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="e958a-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="e958a-138">Ruch RDP (port 3389) z Internetu do żadnej maszyny Wirtualnej jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="e958a-138">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="e958a-139">Ruch HTTP (port 80) z Internetu do serwera sieci web (IIS01) jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="e958a-139">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="e958a-140">Cały ruch (wszystkie porty) z IIS01 do AppVM1 jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="e958a-140">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="e958a-141">Cały ruch (wszystkie porty) z Internetu do całej sieci wirtualnej (obie podsieci) jest zabroniony.</span><span class="sxs-lookup"><span data-stu-id="e958a-141">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="e958a-142">Odmowa cały ruch (wszystkie porty) z podsieci frontonu do podsieci wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="e958a-142">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="e958a-143">Przy użyciu tych reguł powiązany z każdej podsieci, jeśli żądanie HTTP zostało przychodzące z Internetu do serwera sieci web, obie zasady 3 (Zezwalaj) i 5 (odmówić go) będą miały zastosowania, ale ponieważ reguła 3 ma wyższy priorytet tylko będą miały zastosowania i reguły 5 nie przybyły do gry.</span><span class="sxs-lookup"><span data-stu-id="e958a-143">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="e958a-144">W związku z tym żądania HTTP będą dozwolone na serwerze sieci web.</span><span class="sxs-lookup"><span data-stu-id="e958a-144">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="e958a-145">Jeśli ten sam ruch próbował uzyskać dostęp do serwera DNS01, reguły 5 (odmowa) będzie pierwszy do zastosowania, a ruch będzie niedozwolone do przekazania na serwer.</span><span class="sxs-lookup"><span data-stu-id="e958a-145">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="e958a-146">Reguła 6 (Odmów) blokuje podsieci frontonu z rozmowie z podsieci wewnętrznej bazy danych (z wyjątkiem dozwolonego ruchu w regułach 1 i 4), ten zestaw reguł chroni sieć zaplecze w przypadku dokonywania atakująca aplikacja sieci web frontonu, osoba atakująca może mieć ograniczony dostęp do sieci wewnętrznej bazy danych "chronionej" (tylko dla zasobów udostępniane na serwerze AppVM01).</span><span class="sxs-lookup"><span data-stu-id="e958a-146">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="e958a-147">Brak domyślnej regule wychodzącej, która umożliwia ruchu wychodzącego do Internetu.</span><span class="sxs-lookup"><span data-stu-id="e958a-147">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="e958a-148">Na przykład firma Microsoft zezwala na ruch wychodzący i nie modyfikowanie reguł wychodzących.</span><span class="sxs-lookup"><span data-stu-id="e958a-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="e958a-149">Aby zastosować zasady zabezpieczeń do ruchu wychodzącego w obu kierunkach, zdefiniowane routingu użytkownika jest wymagana i jest przedstawione w "W przykładzie 3" na [strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME].</span><span class="sxs-lookup"><span data-stu-id="e958a-149">To apply security policy to traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="e958a-150">Każda reguła omówiono bardziej szczegółowo w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e958a-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="e958a-151">Do przechowywania reguł, można utworzyć wystąpienia zasobu sieciowej grupy zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="e958a-151">A Network Security Group resource must be instantiated to hold the rules:</span></span>

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

2. <span data-ttu-id="e958a-152">Pierwsza reguła w tym przykładzie zezwala na ruch DNS od wszystkich sieci wewnętrznej na serwerze DNS w podsieci wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e958a-152">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="e958a-153">Reguła ma pewne ważne parametry:</span><span class="sxs-lookup"><span data-stu-id="e958a-153">The rule has some important parameters:</span></span>
  * <span data-ttu-id="e958a-154">"destinationAddressPrefix" - reguły można używać specjalnego typu o nazwie "Domyślna Tag" prefiksu adresu, tagi te są dostarczane przez system identyfikatorów, które umożliwiają łatwe większych kategorię prefiksy adresów.</span><span class="sxs-lookup"><span data-stu-id="e958a-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way to address a larger category of address prefixes.</span></span> <span data-ttu-id="e958a-155">Ta zasada taga domyślna "Internet" oznaczającego dowolny adres poza siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e958a-155">This rule uses the Default Tag “Internet” to signify any address outside of the VNet.</span></span> <span data-ttu-id="e958a-156">Inne etykiety prefiks są VirtualNetwork i AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="e958a-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="e958a-157">"Direction" oznacza, że w kierunku przepływu ruchu obowiązuje tej reguły.</span><span class="sxs-lookup"><span data-stu-id="e958a-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="e958a-158">Kierunek jest z punktu widzenia podsieci lub maszyny wirtualnej (w zależności od tego, gdzie jest powiązany ten NSG).</span><span class="sxs-lookup"><span data-stu-id="e958a-158">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="e958a-159">W związku z tym jeśli kierunek jest "Przychodzącego" i ruchu jest wprowadzanie podsieci, reguła powinna zostać zastosowana i ruchu wychodzącego do podsieci nie może mieć wpływ na przez tę regułę.</span><span class="sxs-lookup"><span data-stu-id="e958a-159">Thus if Direction is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="e958a-160">"Priority" Ustawia kolejność, w jakiej są oceniane przepływu ruchu.</span><span class="sxs-lookup"><span data-stu-id="e958a-160">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="e958a-161">Im mniejsza liczba wyższy priorytet.</span><span class="sxs-lookup"><span data-stu-id="e958a-161">The lower the number the higher the priority.</span></span> <span data-ttu-id="e958a-162">Jeśli reguła ma zastosowanie do określonego ruchu, żadne dalsze reguły są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="e958a-162">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="e958a-163">W związku z tym jeśli reguła o priorytecie 1 zezwala na ruch i reguły o priorytecie 2 nie zezwala na ruch i obie zasady są stosowane do ruchu, a następnie ruch będzie dozwolony przepływ (ponieważ reguła 1 ma wyższy priorytet trwało efektu i żadne dodatkowe reguły zostały zastosowane).</span><span class="sxs-lookup"><span data-stu-id="e958a-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="e958a-164">"Access" oznacza, że jeśli wpływ ta reguła jest zablokowane ("Deny") lub dozwolonych ("Zezwalaj").</span><span class="sxs-lookup"><span data-stu-id="e958a-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

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

3. <span data-ttu-id="e958a-165">Ta reguła zezwala na ruch RDP mogą przepływać z Internetu z portem RDP na dowolnym serwerze podsieci powiązania.</span><span class="sxs-lookup"><span data-stu-id="e958a-165">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> 

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

4. <span data-ttu-id="e958a-166">Ta zasada umożliwia ruch przychodzący z Internetu trafienie serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="e958a-166">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="e958a-167">Ta zasada nie powoduje zmiany zachowania routingu.</span><span class="sxs-lookup"><span data-stu-id="e958a-167">This rule does not change the routing behavior.</span></span> <span data-ttu-id="e958a-168">Ta reguła zezwala tylko ruch kierowany do IIS01 do przekazania.</span><span class="sxs-lookup"><span data-stu-id="e958a-168">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="e958a-169">W związku z tym jeśli ruch z Internetu miał serwera sieci web jako miejsca docelowego tej reguły spowoduje zezwolenie i zatrzymać dalsze przetwarzanie reguł.</span><span class="sxs-lookup"><span data-stu-id="e958a-169">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="e958a-170">(W regule priorytetem 140 wszystkich innych przychodzącego ruchu internetowego jest zablokowana).</span><span class="sxs-lookup"><span data-stu-id="e958a-170">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="e958a-171">Tylko w przypadku przetwarzania ruchu HTTP, ta zasada można dodatkowo ograniczony umożliwiają tylko docelowy Port 80.</span><span class="sxs-lookup"><span data-stu-id="e958a-171">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet to [variables('VM01Name')]",
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

5. <span data-ttu-id="e958a-172">Ta zasada umożliwia ruch z serwera IIS01 na serwerze AppVM01 nowsze bloków reguł innych frontonu dla ruchu wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e958a-172">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="e958a-173">Aby poprawić tej reguły, jeśli znane jest port, który ma zostać dodany.</span><span class="sxs-lookup"><span data-stu-id="e958a-173">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="e958a-174">Na przykład, jeśli serwer usług IIS jest naciśnięcie tylko programu SQL Server na AppVM01, zakres portów docelowych należy zmienić "*" (Any) 1433 (SQL port), dzięki czemu mniejsze przychodzących ataki AppVM01 aplikacji sieci web kiedykolwiek zagrożenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="e958a-174">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] to [variables('VM02Name')]",
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

6. <span data-ttu-id="e958a-175">Ta reguła nie zezwala na ruch z Internetu do serwerów w sieci.</span><span class="sxs-lookup"><span data-stu-id="e958a-175">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="e958a-176">Z regułami priorytetem 110 i 120 efekt jest umożliwienie tylko internet ruchu przychodzącego zapory i porty protokołu RDP na serwerach i bloków, wszystkie inne elementy.</span><span class="sxs-lookup"><span data-stu-id="e958a-176">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="e958a-177">Ta reguła jest regułą "awaryjnego" Aby zablokować wszystkie przepływy nieoczekiwany.</span><span class="sxs-lookup"><span data-stu-id="e958a-177">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate the [variables('VNetName')] VNet from the Internet",
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

7. <span data-ttu-id="e958a-178">Reguła końcowego nie zezwala na ruch z podsieci frontonu do podsieci wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e958a-178">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="e958a-179">Ponieważ ta reguła jest tylko regułę ruchu przychodzącego, odwrotnej ruch jest dozwolony (z wewnętrznej bazy danych do serwera sieci Web).</span><span class="sxs-lookup"><span data-stu-id="e958a-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate the [variables('Subnet1Name')] subnet from the [variables('Subnet2Name')] subnet",
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

## <a name="traffic-scenarios"></a><span data-ttu-id="e958a-180">Scenariusze ruchu</span><span class="sxs-lookup"><span data-stu-id="e958a-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="e958a-181">(*Dozwolone*) Internetu do serwera sieci web</span><span class="sxs-lookup"><span data-stu-id="e958a-181">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="e958a-182">Użytkownik internet zażąda strony HTTP od publicznego adresu IP karty Sieciowej, skojarzonych z IIS01 kart interfejsu Sieciowego</span><span class="sxs-lookup"><span data-stu-id="e958a-182">An internet user requests an HTTP page from the public IP address of the NIC associated with the IIS01 NIC</span></span>
2. <span data-ttu-id="e958a-183">Publiczny adres IP przekazuje ruch do sieci wirtualnej kierunku IIS01 (serwer sieci web)</span><span class="sxs-lookup"><span data-stu-id="e958a-183">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="e958a-184">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="e958a-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e958a-185">Reguły NSG 1 DNS (Domain Name System) nie są spełnione, przejść do następnej reguły</span><span class="sxs-lookup"><span data-stu-id="e958a-185">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="e958a-186">2 reguły NSG (RDP) nie są spełnione, przejść do następnej reguły</span><span class="sxs-lookup"><span data-stu-id="e958a-186">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="e958a-187">Zastosować grupy NSG zasady 3 (Internet w celu IIS01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="e958a-187">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="e958a-188">Ruch trafienia wewnętrzny adres IP serwera sieci web IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="e958a-188">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="e958a-189">IIS01 nasłuchuje ruchu w sieci web, otrzymuje tego żądania i rozpoczyna przetwarzanie żądania</span><span class="sxs-lookup"><span data-stu-id="e958a-189">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="e958a-190">IIS01 żąda od serwera SQL na AppVM01 informacji</span><span class="sxs-lookup"><span data-stu-id="e958a-190">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="e958a-191">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="e958a-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="e958a-192">Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="e958a-192">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e958a-193">Reguły NSG 1 DNS (Domain Name System) nie są spełnione, przejść do następnej reguły</span><span class="sxs-lookup"><span data-stu-id="e958a-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="e958a-194">2 reguły NSG (RDP) nie są spełnione, przejść do następnej reguły</span><span class="sxs-lookup"><span data-stu-id="e958a-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="e958a-195">Grupy NSG zasady 3 (Internet do zapory) nie są spełnione, przejść do następnej reguły</span><span class="sxs-lookup"><span data-stu-id="e958a-195">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="e958a-196">4 reguły NSG zastosować (IIS01 do AppVM01), ruch jest dozwolony, Zatrzymaj przetwarzania zasad</span><span class="sxs-lookup"><span data-stu-id="e958a-196">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="e958a-197">AppVM01 odbiera zapytanie SQL i odpowiada</span><span class="sxs-lookup"><span data-stu-id="e958a-197">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="e958a-198">Ponieważ nie ma żadnych reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, odpowiedzi jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="e958a-198">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="e958a-199">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="e958a-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e958a-200">Nie zasady grupy NSG, która ma zastosowanie do przychodzącego ruchu w podsieci wewnętrznej bazy danych do podsieci frontonu, aby żadna grupa NSG zasady stosowane</span><span class="sxs-lookup"><span data-stu-id="e958a-200">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="e958a-201">Domyślna reguła system zezwala na ruch między podsieciami pozwala tego rodzaju ruch, ruch jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="e958a-201">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="e958a-202">Serwer usług IIS otrzyma odpowiedź SQL i kończy odpowiedź HTTP i przesyła do osoby żądającej</span><span class="sxs-lookup"><span data-stu-id="e958a-202">The IIS server receives the SQL response and completes the HTTP response and sends to the requester</span></span>
13. <span data-ttu-id="e958a-203">Ponieważ nie ma żadnych reguł dla ruchu wychodzącego w podsieci frontonu, odpowiedź jest dozwolone i użytkownik Internet otrzymuje żądanej strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="e958a-203">Since there are no outbound rules on the Frontend subnet, the response is allowed and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-iis-server"></a><span data-ttu-id="e958a-204">(*Dozwolone*) RDP do serwera IIS</span><span class="sxs-lookup"><span data-stu-id="e958a-204">(*Allowed*) RDP to IIS server</span></span>
1. <span data-ttu-id="e958a-205">Administrator serwera w Internecie żądań sesji protokołu RDP do IIS01 na publiczny adres IP karty sieciowej, skojarzonych z kart IIS01 (ten publiczny adres IP znajduje się za pośrednictwem portalu lub programu PowerShell)</span><span class="sxs-lookup"><span data-stu-id="e958a-205">A Server Admin on internet requests an RDP session to IIS01 on the public IP address of the NIC associated with the IIS01 NIC (this public IP address can be found via the Portal or PowerShell)</span></span>
2. <span data-ttu-id="e958a-206">Publiczny adres IP przekazuje ruch do sieci wirtualnej kierunku IIS01 (serwer sieci web)</span><span class="sxs-lookup"><span data-stu-id="e958a-206">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="e958a-207">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="e958a-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e958a-208">Reguły NSG 1 DNS (Domain Name System) nie są spełnione, przejść do następnej reguły</span><span class="sxs-lookup"><span data-stu-id="e958a-208">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="e958a-209">Zastosuj 2 reguły NSG (RDP), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="e958a-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="e958a-210">Z nie reguł dla ruchu wychodzącego Zastosuj reguły domyślne i zwracany ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="e958a-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="e958a-211">Włączono sesji protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="e958a-211">RDP session is enabled</span></span>
6. <span data-ttu-id="e958a-212">IIS01 monit o podanie nazwy użytkownika i hasła</span><span class="sxs-lookup"><span data-stu-id="e958a-212">IIS01 prompts for the user name and password</span></span>

>[!NOTE]
><span data-ttu-id="e958a-213">Dla protokołu RDP do serwerów zaplecza w tym wystąpieniu na serwerze usług IIS jest używana jako "okno przeskoku".</span><span class="sxs-lookup"><span data-stu-id="e958a-213">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="e958a-214">Pierwszy RDP do serwera IIS, a następnie z RDP serwera usług IIS do serwera zaplecza.</span><span class="sxs-lookup"><span data-stu-id="e958a-214">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="e958a-215">(*Dozwolone*) wyszukiwanie nazwy DNS serwera sieci Web na serwerze DNS</span><span class="sxs-lookup"><span data-stu-id="e958a-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="e958a-216">Sieci Web serwera, IIS01, musi na www.data.gov strumieniowego źródła danych, ale musi rozpoznać adresu.</span><span class="sxs-lookup"><span data-stu-id="e958a-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="e958a-217">Konfigurację sieci dla listy sieci wirtualnej DNS01 (10.0.2.4 podsieci wewnętrznej bazy danych) jako podstawowy serwer DNS, IIS01 wysyła żądanie DNS DNS01</span><span class="sxs-lookup"><span data-stu-id="e958a-217">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="e958a-218">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="e958a-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="e958a-219">Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="e958a-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="e958a-220">Zastosuj reguły NSG 1 DNS (Domain Name System), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="e958a-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="e958a-221">Serwer DNS odbiera żądanie</span><span class="sxs-lookup"><span data-stu-id="e958a-221">DNS server receives the request</span></span>
6. <span data-ttu-id="e958a-222">Serwer DNS nie ma adresu w pamięci podręcznej i prosi o główny serwer DNS w Internecie</span><span class="sxs-lookup"><span data-stu-id="e958a-222">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="e958a-223">Nie reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="e958a-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="e958a-224">DNS w Internecie serwer odpowiada, ponieważ ta sesja została zainicjowana wewnętrznie, odpowiedź jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="e958a-224">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="e958a-225">Serwer DNS będzie buforować odpowiedź i odpowiada na żądania początkowego do IIS01</span><span class="sxs-lookup"><span data-stu-id="e958a-225">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="e958a-226">Nie reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="e958a-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="e958a-227">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="e958a-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e958a-228">Nie zasady grupy NSG, która ma zastosowanie do przychodzącego ruchu w podsieci wewnętrznej bazy danych do podsieci frontonu, aby żadna grupa NSG zasady stosowane</span><span class="sxs-lookup"><span data-stu-id="e958a-228">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="e958a-229">Domyślna reguła system zezwala na ruch między podsieciami pozwala tego rodzaju ruch, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="e958a-229">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="e958a-230">IIS01 odbiera odpowiedź z DNS01</span><span class="sxs-lookup"><span data-stu-id="e958a-230">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="e958a-231">(*Dozwolone*) pliku dostępu do serwera sieci Web na AppVM01</span><span class="sxs-lookup"><span data-stu-id="e958a-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="e958a-232">IIS01 żąda pliku na AppVM01</span><span class="sxs-lookup"><span data-stu-id="e958a-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="e958a-233">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="e958a-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="e958a-234">Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="e958a-234">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e958a-235">Reguły NSG 1 DNS (Domain Name System) nie są spełnione, przejść do następnej reguły</span><span class="sxs-lookup"><span data-stu-id="e958a-235">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="e958a-236">2 reguły NSG (RDP) nie są spełnione, przejść do następnej reguły</span><span class="sxs-lookup"><span data-stu-id="e958a-236">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="e958a-237">Grupa NSG zasady 3 (Internet w celu IIS01) nie są spełnione, przejść do następnej reguły</span><span class="sxs-lookup"><span data-stu-id="e958a-237">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="e958a-238">4 reguły NSG zastosować (IIS01 do AppVM01), ruch jest dozwolony, Zatrzymaj przetwarzania zasad</span><span class="sxs-lookup"><span data-stu-id="e958a-238">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="e958a-239">AppVM01 odbiera żądanie i odpowiada plik (przy założeniu, że autoryzacji dostępu)</span><span class="sxs-lookup"><span data-stu-id="e958a-239">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="e958a-240">Ponieważ nie ma żadnych reguł dla ruchu wychodzącego w podsieci wewnętrznej bazy danych, odpowiedzi jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="e958a-240">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="e958a-241">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="e958a-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e958a-242">Nie zasady grupy NSG, która ma zastosowanie do przychodzącego ruchu w podsieci wewnętrznej bazy danych do podsieci frontonu, aby żadna grupa NSG zasady stosowane</span><span class="sxs-lookup"><span data-stu-id="e958a-242">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="e958a-243">Domyślna reguła system zezwala na ruch między podsieciami pozwala tego rodzaju ruch, ruch jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="e958a-243">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="e958a-244">Serwer usług IIS odbiera plik</span><span class="sxs-lookup"><span data-stu-id="e958a-244">The IIS server receives the file</span></span>

#### <a name="denied-rdp-to-backend"></a><span data-ttu-id="e958a-245">(*Odmowa*) RDP do wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="e958a-245">(*Denied*) RDP to backend</span></span>
1. <span data-ttu-id="e958a-246">Użytkownik internet próbuje RDP do serwera AppVM01</span><span class="sxs-lookup"><span data-stu-id="e958a-246">An internet user tries to RDP to server AppVM01</span></span>
2. <span data-ttu-id="e958a-247">Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić sieci wirtualnej, a nie dociera do serwera</span><span class="sxs-lookup"><span data-stu-id="e958a-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="e958a-248">Jednak jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, reguły NSG 2 (RDP) umożliwiałyby ten ruch</span><span class="sxs-lookup"><span data-stu-id="e958a-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="e958a-249">Dla protokołu RDP do serwerów zaplecza w tym wystąpieniu na serwerze usług IIS jest używana jako "okno przeskoku".</span><span class="sxs-lookup"><span data-stu-id="e958a-249">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="e958a-250">Pierwszy RDP do serwera IIS, a następnie z RDP serwera usług IIS do serwera zaplecza.</span><span class="sxs-lookup"><span data-stu-id="e958a-250">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="e958a-251">(*Odmowa*) do serwera wewnętrznej bazy danych w sieci Web</span><span class="sxs-lookup"><span data-stu-id="e958a-251">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="e958a-252">Użytkownik internet próbuje uzyskać dostęp do pliku na AppVM01</span><span class="sxs-lookup"><span data-stu-id="e958a-252">An internet user tries to access a file on AppVM01</span></span>
2. <span data-ttu-id="e958a-253">Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić sieci wirtualnej, a nie dociera do serwera</span><span class="sxs-lookup"><span data-stu-id="e958a-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="e958a-254">Jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, reguły NSG 5 (Internet do sieci wirtualnej) czy zablokować ruch</span><span class="sxs-lookup"><span data-stu-id="e958a-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="e958a-255">(*Odmowa*) wyszukiwanie nazwy DNS w sieci Web na serwerze DNS</span><span class="sxs-lookup"><span data-stu-id="e958a-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="e958a-256">Internet próby odszukania wewnętrzny rekord DNS na DNS01</span><span class="sxs-lookup"><span data-stu-id="e958a-256">An internet user tries to look up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="e958a-257">Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić sieci wirtualnej, a nie dociera do serwera</span><span class="sxs-lookup"><span data-stu-id="e958a-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="e958a-258">Jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, reguły NSG 5 (Internet do sieci wirtualnej) czy zablokować ruch (Uwaga: Aby reguła 1 (DNS) nie ma zastosowania, ponieważ adres źródłowy żądania jest internet i 1 reguła ma zastosowanie tylko do lokalnej sieci wirtualnej jako źródło)</span><span class="sxs-lookup"><span data-stu-id="e958a-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because the requests source address is the internet and Rule 1 only applies to the local VNet as the source)</span></span>

#### <a name="denied-sql-access-on-the-web-server"></a><span data-ttu-id="e958a-259">(*Odmowa*) dostęp SQL na serwerze sieci web</span><span class="sxs-lookup"><span data-stu-id="e958a-259">(*Denied*) SQL access on the web server</span></span>
1. <span data-ttu-id="e958a-260">Użytkownik internet żąda danych SQL z IIS01</span><span class="sxs-lookup"><span data-stu-id="e958a-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="e958a-261">Ponieważ nie ma żadnych publiczne adresy IP skojarzone z tym serwerami kart interfejsu Sieciowego, tego rodzaju ruch nigdy nie wprowadzić sieci wirtualnej, a nie dociera do serwera</span><span class="sxs-lookup"><span data-stu-id="e958a-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="e958a-262">Jeśli do publicznego adresu IP zostały włączone dla jakiegoś powodu, podsieci frontonu rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="e958a-262">If a Public IP address was enabled for some reason, the Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e958a-263">Reguły NSG 1 DNS (Domain Name System) nie są spełnione, przejść do następnej reguły</span><span class="sxs-lookup"><span data-stu-id="e958a-263">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="e958a-264">2 reguły NSG (RDP) nie są spełnione, przejść do następnej reguły</span><span class="sxs-lookup"><span data-stu-id="e958a-264">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="e958a-265">Zastosować grupy NSG zasady 3 (Internet w celu IIS01), ruch jest dozwolony, stop reguły przetwarzania</span><span class="sxs-lookup"><span data-stu-id="e958a-265">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="e958a-266">Wewnętrzny adres IP IIS01 trafienia ruchu (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="e958a-266">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="e958a-267">IIS01 nie nasłuchuje na porcie 1433, więc nie ma odpowiedzi na żądanie</span><span class="sxs-lookup"><span data-stu-id="e958a-267">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="e958a-268">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e958a-268">Conclusion</span></span>
<span data-ttu-id="e958a-269">W tym przykładzie jest stosunkowo proste i bezpośrednio do przodu sposobem izolowanie podsieci wewnętrznej z ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="e958a-269">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="e958a-270">Więcej przykładów i Przegląd granic zabezpieczeń sieci można znaleźć [tutaj][HOME].</span><span class="sxs-lookup"><span data-stu-id="e958a-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="e958a-271">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="e958a-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="e958a-272">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e958a-272">Azure Resource Manager template</span></span>
<span data-ttu-id="e958a-273">W tym przykładzie używa wstępnie zdefiniowanych szablonów usługi Azure Resource Manager w repozytorium GitHub obsługiwanego przez firmę Microsoft i dla społeczności.</span><span class="sxs-lookup"><span data-stu-id="e958a-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="e958a-274">Tego szablonu można wdrożyć bezpośrednio z witryny GitHub, lub pobrać i zmodyfikować odpowiednio do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="e958a-274">This template can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> 

<span data-ttu-id="e958a-275">Główny szablon znajduje się w pliku o nazwie "azuredeploy.json."</span><span class="sxs-lookup"><span data-stu-id="e958a-275">The main template is in the file named "azuredeploy.json."</span></span> <span data-ttu-id="e958a-276">Ten szablon może zostać przesłane za pomocą programu PowerShell lub interfejsu wiersza polecenia (przy użyciu pliku skojarzone "azuredeploy.parameters.json") do wdrożenia tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="e958a-276">This template can be submitted via PowerShell or CLI (with the associated "azuredeploy.parameters.json" file) to deploy this template.</span></span> <span data-ttu-id="e958a-277">Odnalezienie Najprostszym sposobem jest użycie przycisku "Wdrożenia do platformy Azure" na stronie README.md w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="e958a-277">I find the easiest way is to use the "Deploy to Azure" button on the README.md page at GitHub.</span></span>

<span data-ttu-id="e958a-278">Aby wdrożyć szablon, który tworzy w tym przykładzie z serwisu GitHub i portalu Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e958a-278">To deploy the template that builds this example from GitHub and the Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="e958a-279">W przeglądarce przejdź do [szablonu][Template]</span><span class="sxs-lookup"><span data-stu-id="e958a-279">From a browser, navigate to the [Template][Template]</span></span>
2. <span data-ttu-id="e958a-280">Kliknij przycisk "Wdrożenia do platformy Azure" (lub przycisk "Wizualizacja", aby wyświetlić graficzną reprezentację tego szablonu)</span><span class="sxs-lookup"><span data-stu-id="e958a-280">Click the "Deploy to Azure" button (or the "Visualize" button to see a graphical representation of this template)</span></span>
3. <span data-ttu-id="e958a-281">Wprowadź konto magazynu, nazwę użytkownika i hasło w bloku parametrów, a następnie kliknij przycisk **OK**</span><span class="sxs-lookup"><span data-stu-id="e958a-281">Enter the Storage Account, User Name, and Password in the Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="e958a-282">Utwórz grupę zasobów dla tego wdrożenia (można użyć istniejącego, ale zalecane jest nowy, aby uzyskać najlepsze wyniki)</span><span class="sxs-lookup"><span data-stu-id="e958a-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="e958a-283">W razie potrzeby zmień ustawienia subskrypcji i lokalizacji sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e958a-283">If necessary, change the Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="e958a-284">Kliknij przycisk **Przejrzyj postanowienia prawne**, przeczytaj warunki i kliknij przycisk **zakupu** do wyrażenia zgody.</span><span class="sxs-lookup"><span data-stu-id="e958a-284">Click **Review legal terms**, read the terms, and click **Purchase** to agree.</span></span>
8. <span data-ttu-id="e958a-285">Kliknij przycisk **Utwórz** aby rozpocząć wdrażanie tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="e958a-285">Click **Create** to begin the deployment of this template.</span></span>
9. <span data-ttu-id="e958a-286">Po pomyślnym wdrożeniu, przejdź do grupy zasobów utworzonej dla tego wdrożenia do wyświetlania zasobów, skonfigurowane w.</span><span class="sxs-lookup"><span data-stu-id="e958a-286">Once the deployment finishes successfully, navigate to the Resource Group created for this deployment to see the resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="e958a-287">Ten szablon umożliwia RDP tylko serwera IIS01 (Znajdź publicznego adresu IP dla IIS01 w portalu).</span><span class="sxs-lookup"><span data-stu-id="e958a-287">This template enables RDP to the IIS01 server only (find the Public IP for IIS01 on the Portal).</span></span> <span data-ttu-id="e958a-288">Dla protokołu RDP do serwerów zaplecza w tym wystąpieniu na serwerze usług IIS jest używana jako "okno przeskoku".</span><span class="sxs-lookup"><span data-stu-id="e958a-288">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="e958a-289">Pierwszy RDP do serwera IIS, a następnie z RDP serwera usług IIS do serwera zaplecza.</span><span class="sxs-lookup"><span data-stu-id="e958a-289">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

<span data-ttu-id="e958a-290">Aby usunąć to wdrożenie, Usuń grupę zasobów i wszystkie zasoby podrzędne zostaną również usunięte.</span><span class="sxs-lookup"><span data-stu-id="e958a-290">To remove this deployment, delete the Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="e958a-291">Przykładowe skrypty aplikacji</span><span class="sxs-lookup"><span data-stu-id="e958a-291">Sample application scripts</span></span>
<span data-ttu-id="e958a-292">Po pomyślnym uruchomieniu szablon, można skonfigurować serwer sieci web i serwerów aplikacji z prostą aplikację sieci web umożliwia testowanie za pomocą tej konfiguracji DMZ.</span><span class="sxs-lookup"><span data-stu-id="e958a-292">Once the template runs successfully, you can set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span> <span data-ttu-id="e958a-293">Aby zainstalować przykładową aplikację dla tego i innych przykłady DMZ, jeden podano przy użyciu następującego łącza: [przykładowy skrypt aplikacji][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="e958a-293">To install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="e958a-294">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e958a-294">Next steps</span></span>

* <span data-ttu-id="e958a-295">W tym przykładzie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="e958a-295">Deploy this example</span></span>
* <span data-ttu-id="e958a-296">Tworzenie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="e958a-296">Build the sample application</span></span>
* <span data-ttu-id="e958a-297">Testowanie różnych ruch za pośrednictwem tego DMZ</span><span class="sxs-lookup"><span data-stu-id="e958a-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
<span data-ttu-id="e958a-298">[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Przychodzący DMZ z grupy NSG"</span><span class="sxs-lookup"><span data-stu-id="e958a-298">[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Inbound DMZ with NSG"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md