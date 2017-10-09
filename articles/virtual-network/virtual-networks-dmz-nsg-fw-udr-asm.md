---
title: "Przykład — aaaDMZ kompilacji DMZ tooProtect sieci z zapory, przez i NSG | Dokumentacja firmy Microsoft"
description: "Tworzenie DMZ za pomocą zapory, zdefiniowane przez użytkownika routingu (przez) i grupy zabezpieczeń sieci (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="d9bf7-103">Przykład 3 — Tworzenie DMZ tooProtect sieci z zapory, przez i grupy NSG</span><span class="sxs-lookup"><span data-stu-id="d9bf7-103">Example 3 – Build a DMZ tooProtect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="d9bf7-104">[Zwraca toohello strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="d9bf7-105">W tym przykładzie utworzy strefą DMZ z zapory, cztery serwery z systemem windows, użytkownik zdefiniowane routingu, przesyłania dalej protokołu IP i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="d9bf7-106">On również przeprowadzi każdego tooprovide odpowiednich poleceń hello głębsze zrozumienie każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="d9bf7-107">Istnieje również scenariusz ruchu sekcji tooprovide jako szczegółowe krok po kroku, jak ruchu obejmującego hello warstw zabezpieczeń w hello DMZ.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="d9bf7-108">Na koniec w sekcji odwołań hello jest kompletny kod hello i toobuild instrukcji tego środowiska tootest i doświadczenia z różnych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="d9bf7-109">![Dwukierunkowe DMZ NVA, NSG i przez][1]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="d9bf7-110">Konfigurowanie środowiska</span><span class="sxs-lookup"><span data-stu-id="d9bf7-110">Environment Setup</span></span>
<span data-ttu-id="d9bf7-111">W tym przykładzie jest subskrypcji, która zawiera następujące hello:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="d9bf7-112">Trzy usługi w chmurze: "SecSvc001", "FrontEnd001" i "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="d9bf7-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="d9bf7-113">"CorpNetwork" przy użyciu trzech podsieci sieci wirtualnej: "SecNet", "Fronton" i "Wewnętrzna"</span><span class="sxs-lookup"><span data-stu-id="d9bf7-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="d9bf7-114">Urządzenie wirtualne sieci, w tym przykładzie zaporą, podłączone podsieci SecNet toohello</span><span class="sxs-lookup"><span data-stu-id="d9bf7-114">A network virtual appliance, in this example a firewall, connected toohello SecNet subnet</span></span>
* <span data-ttu-id="d9bf7-115">Windows Server, który reprezentuje serwer sieci web aplikacji ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="d9bf7-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="d9bf7-116">Dwa okna serwerów, które reprezentują aplikacji z powrotem kończyć serwery ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="d9bf7-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="d9bf7-117">Windows server, który reprezentuje serwer DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="d9bf7-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="d9bf7-118">W sekcji odwołań hello poniżej jest skrypt programu PowerShell, który zostanie skompilowany większość środowiska hello opisane powyżej.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-118">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="d9bf7-119">Maszyny wirtualne hello budynku i sieciami wirtualnymi, chociaż są realizowane przez skrypt hello nie opisano szczegółowo w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-119">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="d9bf7-120">toobuild hello środowiska:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-120">toobuild hello environment:</span></span>

1. <span data-ttu-id="d9bf7-121">Zapisz hello sieci xml pliku konfiguracji zawarte w sekcji odwołań hello (zaktualizowany o nazwy, lokalizacji i scenariusz hello podane toomatch adresów IP)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-121">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="d9bf7-122">Zmienne użytkownika hello aktualizacji hello skryptu toomatch hello środowiska hello skryptu jest toobe uruchomienia (subskrypcje, nazwy usługi itp.)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-122">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="d9bf7-123">Uruchom skrypt hello w programie PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9bf7-123">Execute hello script in PowerShell</span></span>

<span data-ttu-id="d9bf7-124">**Uwaga**: region hello oznaczony w hello skrypt programu PowerShell musi odpowiadać region hello oznaczony w pliku xml konfiguracji sieci hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-124">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="d9bf7-125">Po pomyślnym uruchomieniu skryptu hello można podjąć następujące kroki po skryptu hello:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-125">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="d9bf7-126">Konfigurowanie reguł zapory hello, to jest objęte hello sekcji poniżej: opis reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-126">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="d9bf7-127">Opcjonalnie w sekcji odwołań hello są dwa skrypty tooset powitania serwera sieci web i serwerów aplikacji z tooallow aplikacji sieci web proste, testowanie za pomocą tej konfiguracji DMZ.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-127">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="d9bf7-128">Po pomyślnym uruchomieniu skryptu hello hello reguły zapory, należy ukończyć toobe, ten temat znajdują się w sekcji hello: reguł zapory.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-128">Once hello script runs successfully hello firewall rules will need toobe completed, this is covered in hello section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="d9bf7-129">Zdefiniowane przez użytkownika routingu (przez)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="d9bf7-130">Domyślnie program hello następujące trasy systemowe są zdefiniowane jako:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-130">By default, hello following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="d9bf7-131">Witaj VNETLocal jest zawsze prefiksy adresów hello zdefiniowane z hello sieci wirtualnej dla tej sieci określonych (ie go ulegnie zmianie z tooVNet sieci wirtualnej, w zależności od tego, jak zdefiniowano każdej określonej sieci wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-131">hello VNETLocal is always hello defined address prefix(es) of hello VNet for that specific network (ie it will change from VNet tooVNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="d9bf7-132">trasy systemowe pozostałych Hello są statyczne i domyślne jako powyżej.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-132">hello remaining system routes are static and default as above.</span></span>

<span data-ttu-id="d9bf7-133">Podobnie jak w przypadku priorytet trasy są przetwarzane przy użyciu metody najdłuższym prefiksu dopasowania (LPM) Wybierane hello, w związku z tym hello specyficzny trasy w tabeli hello powinna zostać zastosowana tooa podany adres docelowy.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-133">As for priority, routes are processed via hello Longest Prefix Match (LPM) method, thus hello most specific route in hello table would apply tooa given destination address.</span></span>

<span data-ttu-id="d9bf7-134">W związku z tym ruchu (na przykład serwer toohello DNS01, 10.0.2.4) przeznaczone na powitania w sieci lokalnej (10.0.0.0/16) zostanie przekierowane na docelowym tooits sieci wirtualnej hello powodu toohello 10.0.0.0/16 trasy.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-134">Therefore, traffic (for example toohello DNS01 server, 10.0.2.4) intended for hello local network (10.0.0.0/16) would be routed across hello VNet tooits destination due toohello 10.0.0.0/16 route.</span></span> <span data-ttu-id="d9bf7-135">Innymi słowy 10.0.2.4, trasy 10.0.0.0/16 hello jest najbardziej określoną trasę hello, mimo że hello 10.0.0.0/8 i 0.0.0.0/0 również można zastosować, ale ponieważ są one szerszym nie wpływają one na ten ruch.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-135">In other words, for 10.0.2.4, hello 10.0.0.0/16 route is hello most specific route, even though hello 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="d9bf7-136">W związku z tym too10.0.2.4 ruchu hello musi następnego przeskoku hello lokalnej sieci wirtualnej i po prostu trasy toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-136">Thus hello traffic too10.0.2.4 would have a next hop of hello local VNet and simply route toohello destination.</span></span>

<span data-ttu-id="d9bf7-137">Jeśli ruch jest przeznaczona do 10.1.1.1, na przykład, hello 10.0.0.0/16 trasy nie zastosować, ale hello 10.0.0.0/8 byłoby hello specyficzny i będzie ruch hello pomijane ("czarna holed"), ponieważ hello następnego przeskoku jest Null.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-137">If traffic was intended for 10.1.1.1 for example, hello 10.0.0.0/16 route wouldn’t apply, but hello 10.0.0.0/8 would be hello most specific, and this hello traffic would be dropped (“black holed”) since hello next hop is Null.</span></span> 

<span data-ttu-id="d9bf7-138">Jeśli hello docelowy nie miał zastosowania tooany prefiksy Null hello lub hello VNETLocal prefiksy, a następnie należy wykonać hello najmniej określonej trasy, 0.0.0.0/0 oraz być kierowane toohello Internet jako hello następnego przeskoku i w związku z tym limit krawędzi internet platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-138">If hello destination didn’t apply tooany of hello Null prefixes or hello VNETLocal prefixes, then it would follow hello least specific route, 0.0.0.0/0 and be routed out toohello Internet as hello next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="d9bf7-139">Jeśli istnieją dwie identyczne prefiksów w tabeli tras hello, hello Oto hello według priorytetu na podstawie atrybutu "source" tras hello:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-139">If there are two identical prefixes in hello route table, hello following is hello order of preference based on hello routes “source” attribute:</span></span>

1. <span data-ttu-id="d9bf7-140">"VirtualAppliance" = tabeli dodane ręcznie toohello trasy zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="d9bf7-140">"VirtualAppliance" = A User Defined Route manually added toohello table</span></span>
2. <span data-ttu-id="d9bf7-141">"Właściwość VPNGateway" = dynamiczny trasy protokołu BGP (gdy jest używany z sieci hybrydowe), dodane przez protokół dynamicznej sieci, te trasy może ulec zmianie jako protokół dynamicznej hello automatycznie uwzględnia zmiany w połączyć za pomocą sieci</span><span class="sxs-lookup"><span data-stu-id="d9bf7-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as hello dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="d9bf7-142">"Default" = hello tras systemowych, hello lokalnej sieci wirtualnej i hello statyczne, jak pokazano w powyższej tabeli tras hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-142">“Default” = hello System Routes, hello local VNet and hello static entries as shown in hello route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="d9bf7-143">Użytkownika zdefiniowane routingu przez mogą teraz używać z bramy sieci VPN i ExpressRoute tooforce wychodzący i przychodzący między lokalizacjami ruchu toobe routingiem tooa sieci urządzenie wirtualne (NVA).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways tooforce outbound and inbound cross-premises traffic toobe routed tooa network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-hello-local-routes"></a><span data-ttu-id="d9bf7-144">Tworzenie hello tras lokalnych</span><span class="sxs-lookup"><span data-stu-id="d9bf7-144">Creating hello local routes</span></span>
<span data-ttu-id="d9bf7-145">W tym przykładzie są potrzebne dwie tabele routingu, jeden dla każdej podsieci hello frontonu i wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-145">In this example, two routing tables are needed, one each for hello Frontend and Backend subnets.</span></span> <span data-ttu-id="d9bf7-146">Każda tabela tras statycznych, które są odpowiednie dla podanej podsieci hello jest załadowana.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-146">Each table is loaded with static routes appropriate for hello given subnet.</span></span> <span data-ttu-id="d9bf7-147">W celu hello w tym przykładzie każda tabela zawiera trzy tras:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-147">For hello purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="d9bf7-148">Ruchu w podsieci lokalnej z następnego przeskoku zdefiniowane tooallow podsieci lokalnej ruchu toobypass hello zapory</span><span class="sxs-lookup"><span data-stu-id="d9bf7-148">Local subnet traffic with no Next Hop defined tooallow local subnet traffic toobypass hello firewall</span></span>
2. <span data-ttu-id="d9bf7-149">Ruchu w sieci wirtualnej z przeskoku dalej zdefiniowany jako zapory, przesłania hello domyślna reguła, która umożliwia bezpośrednio lokalnego tooroute ruchu w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d9bf7-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides hello default rule that allows local VNet traffic tooroute directly</span></span>
3. <span data-ttu-id="d9bf7-150">Wszystkie pozostałe ruchu (0/0) z następnego przeskoku zdefiniowany jako hello zapory</span><span class="sxs-lookup"><span data-stu-id="d9bf7-150">All remaining traffic (0/0) with a Next Hop defined as hello firewall</span></span>

<span data-ttu-id="d9bf7-151">Po utworzeniu tabele routingu hello są one powiązane tootheir podsieci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-151">Once hello routing tables are created they are bound tootheir subnets.</span></span> <span data-ttu-id="d9bf7-152">Na frontonie hello podsieci tabeli routingu po utworzeniu i powiązane podsieci toohello powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-152">For hello Frontend subnet routing table, once created and bound toohello subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="d9bf7-153">W tym przykładzie polecenia tabeli tras hello toobuild używane są następujące hello Dodaj trasy zdefiniowane przez użytkownika, a następnie powiązać podsieci tooa tabeli tras hello (Uwaga; wszystkie elementy poniżej rozpoczynający się od znaku dolara (np.: $BESubnet) są zmiennych zdefiniowanych przez użytkownika ze skryptu hello w Witaj odwołanie sekcji tego dokumentu):</span><span class="sxs-lookup"><span data-stu-id="d9bf7-153">For this example, hello following commands are used toobuild hello route table, add a user defined route, and then bind hello route table tooa subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="d9bf7-154">Można utworzyć pierwszy hello podstawowej tabeli routingu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-154">First hello base routing table must be created.</span></span> <span data-ttu-id="d9bf7-155">Ta Wstawka kodu pokazano tworzenie hello tabeli hello hello podsieci wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-155">This snippet shows hello creation of hello table for hello Backend subnet.</span></span> <span data-ttu-id="d9bf7-156">W skrypcie hello tworzona jest również odpowiedniego tabeli hello podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-156">In hello script, a corresponding table is also created for hello Frontend subnet.</span></span>
   
     <span data-ttu-id="d9bf7-157">Nowe AzureRouteTable-Name $BERouteTableName "</span><span class="sxs-lookup"><span data-stu-id="d9bf7-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="d9bf7-158">Po utworzeniu tabeli tras hello można dodać trasy zdefiniowane przez określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-158">Once hello route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="d9bf7-159">W tym przedstawiono cały ruch (0.0.0.0/0), zostaną przesłane za pośrednictwem hello urządzenie wirtualne (używane toopass hello adres IP przypisany, gdy urządzenie wirtualne hello został utworzony we wcześniejszej części skryptu hello jest zmienną $VMIP [0]).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-159">In this snipped, all traffic (0.0.0.0/0) will be routed through hello virtual appliance (a variable, $VMIP[0], is used toopass in hello IP address assigned when hello virtual appliance was created earlier in hello script).</span></span> <span data-ttu-id="d9bf7-160">W skrypcie hello tworzona jest również odpowiednią regułę hello tabeli frontonu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-160">In hello script, a corresponding rule is also created in hello Frontend table.</span></span>
   
     <span data-ttu-id="d9bf7-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="d9bf7-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="d9bf7-162">Witaj powyżej wejście dla trasy spowoduje zastąpienie hello domyślną trasę "0.0.0.0/0", ale reguła 10.0.0.0/16 domyślnej hello nadal istniejące, które umożliwiałyby ruch w ramach tooroute sieci wirtualnej hello bezpośrednio toohello docelowego i toohello urządzenie wirtualne sieci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-162">hello above route entry will override hello default "0.0.0.0/0" route, but hello default 10.0.0.0/16 rule still existing which would allow traffic within hello VNet tooroute directly toohello destination and not toohello Network Virtual Appliance.</span></span> <span data-ttu-id="d9bf7-163">toocorrect, należy dodać tę regułę wykonaj hello zachowanie.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-163">toocorrect this behavior hello follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="d9bf7-164">W tym momencie jest toobe wyborów dokonanych.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-164">At this point there is a choice toobe made.</span></span> <span data-ttu-id="d9bf7-165">Z hello powyżej na dwa sposoby cały ruch będzie przekierowywać toohello zapory w celu oceny, nawet ruch w ramach pojedynczej podsieci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-165">With hello above two routes all traffic will route toohello firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="d9bf7-166">Może to konieczne, jednak tooallow ruchu w podsieci tooroute lokalnie bez udziału hello zapory, trzeci, bardzo określonej reguły mogą zostać dodane.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-166">This may be desired, however tooallow traffic within a subnet tooroute locally without involvement from hello firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="d9bf7-167">Ta trasa stanów, które dowolnego adresu destine dla podsieci lokalne powitania można po prostu kierować bezpośrednio (Typ następnego przeskoku = VNETLocal).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-167">This route states that any address destine for hello local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="d9bf7-168">Na koniec z tabeli routingu hello tworzone i wypełniane przy użyciu trasy zdefiniowane przez użytkownika, tabela hello teraz musi być powiązane tooa podsieci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-168">Finally, with hello routing table created and populated with a user defined routes, hello table must now be bound tooa subnet.</span></span> <span data-ttu-id="d9bf7-169">W skrypcie hello tabeli tras frontonu hello jest także powiązane toohello podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-169">In hello script, hello front end route table is also bound toohello Frontend subnet.</span></span> <span data-ttu-id="d9bf7-170">W tym miejscu to skrypt powiązanie hello hello podsieci wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-170">Here is hello binding script for hello back end subnet.</span></span>
   
     <span data-ttu-id="d9bf7-171">Zestaw AzureSubnetRouteTable - VirtualNetworkName $VNetName "</span><span class="sxs-lookup"><span data-stu-id="d9bf7-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="d9bf7-172">Przesyłanie dalej IP</span><span class="sxs-lookup"><span data-stu-id="d9bf7-172">IP Forwarding</span></span>
<span data-ttu-id="d9bf7-173">TooUDR funkcji Pomocnik jest przekazywanie adresów IP.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-173">A companion feature tooUDR, is IP Forwarding.</span></span> <span data-ttu-id="d9bf7-174">To jest ustawienie na urządzenie wirtualne, umożliwiającą ruch tooreceive nie specjalnie kierowane toohello urządzenia i następnie przesyła ten ruch tooits ostatecznym miejscem przeznaczenia.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-174">This is a setting on a Virtual Appliance that allows it tooreceive traffic not specifically addressed toohello appliance and then forward that traffic tooits ultimate destination.</span></span>

<span data-ttu-id="d9bf7-175">Na przykład jeśli ruch z AppVM01 sprawia, że serwer DNS01 toohello żądania przez może kierować Zapora toohello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-175">As an example, if traffic from AppVM01 makes a request toohello DNS01 server, UDR would route this toohello firewall.</span></span> <span data-ttu-id="d9bf7-176">Z przesyłania dalej protokołu IP włączone hello ruchu dla miejsca docelowego DNS01 hello (10.0.2.4) zostanie zaakceptowane przez urządzenia hello (10.0.0.4) i przesyłane dalej ostatecznym miejscem przeznaczenia tooits (10.0.2.4).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-176">With IP Forwarding enabled, hello traffic for hello DNS01 destination (10.0.2.4) will be accepted by hello appliance (10.0.0.4) and then forwarded tooits ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="d9bf7-177">Bez przesyłania dalej protokołu IP włączone na powitania zapory ruch może nie zostać zaakceptowane przez hello urządzenia nawet hello tabeli tras ma zapory hello jako hello następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-177">Without IP Forwarding enabled on hello Firewall, traffic would not be accepted by hello appliance even though hello route table has hello firewall as hello next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d9bf7-178">Jest krytyczne tooremember tooenable przesyłania dalej protokołu IP w połączeniu z routingiem zdefiniowane użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-178">It’s critical tooremember tooenable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="d9bf7-179">Konfigurowanie przekazywania adresów IP jest jednego polecenia i może odbywać się w czasie tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="d9bf7-180">Dla hello przepływu fragment kodu hello ten przykład jest końcowej hello hello skryptu i zgrupowana za pomocą polecenia przez hello:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-180">For hello flow of this example hello code snippet is towards hello end of hello script and grouped with hello UDR commands:</span></span>

1. <span data-ttu-id="d9bf7-181">Wywołania hello wystąpienia maszyny Wirtualnej, które jest urządzenia wirtualnego, w takim przypadku hello zapory i włączenia funkcji przesyłania dalej IP (Uwaga; dowolny element w czerwonym rozpoczynający się od znaku dolara (np.: $VMName[0]) jest zmienną zdefiniowanych przez użytkownika ze skryptu hello hello odwołanie sekcji tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-181">Call hello VM instance that is your virtual appliance, hello firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="d9bf7-182">Witaj zero w nawiasach [0], reprezentuje hello pierwsza maszyna wirtualna w tablicy hello maszyn wirtualnych, dla hello przykładowy skrypt toowork bez żadnych modyfikacji, powitalne pierwsza maszyna wirtualna (VM 0) musi być hello zapory):</span><span class="sxs-lookup"><span data-stu-id="d9bf7-182">hello zero in brackets, [0], represents hello first VM in hello array of VMs, for hello example script toowork without modification, hello first VM (VM 0) must be hello firewall):</span></span>
   
     <span data-ttu-id="d9bf7-183">Get-AzureVM-Name $VMName [0] - ServiceName $ServiceName [0] | \`</span><span class="sxs-lookup"><span data-stu-id="d9bf7-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="d9bf7-184">Sieciowe grupy zabezpieczeń (NSG)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="d9bf7-185">W tym przykładzie grupa NSG jest wbudowana i następnie ładowane przy użyciu jednej reguły.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="d9bf7-186">Ta grupa jest następnie powiązany tylko toohello frontonu i zaplecza podsieci (nie hello SecNet).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-186">This group is then bound only toohello Frontend and Backend subnets (not hello SecNet).</span></span> <span data-ttu-id="d9bf7-187">Deklaratywnie budowanego hello następujące reguły:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-187">Declaratively hello following rule is being built:</span></span>

1. <span data-ttu-id="d9bf7-188">Cały ruch (wszystkie porty) z hello Internet toohello odmowa całej sieci wirtualnej (wszystkie podsieci)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-188">Any traffic (all ports) from hello Internet toohello entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="d9bf7-189">Mimo że grupy NSG są używane w tym przykładzie, jego głównym celem jest jako dodatkowej warstwy obrony przed ręcznej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="d9bf7-190">Chcemy tooblock wszystkie przychodzący ruch z hello internet tooeither hello frontonu, lub podsieci wewnętrznej bazy danych, ruch powinny przepływać tylko za pośrednictwem zapory toohello podsieci SecNet hello (i następnie jeśli odpowiednią na toohello frontonu lub wewnętrznej bazy danych podsieci).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-190">We want tooblock all inbound traffic from hello internet tooeither hello Frontend or Backend subnets, traffic should only flow through hello SecNet subnet toohello firewall (and then if appropriate on toohello Frontend or Backend subnets).</span></span> <span data-ttu-id="d9bf7-191">Plus przy użyciu reguł przez hello w miejscu, dowolnego ruchu, który przekształcić go hello podsieci frontonu lub wewnętrznej bazy danych spowoduje przekierowanie limit toohello zapory (Dziękujemy tooUDR).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-191">Plus, with hello UDR rules in place, any traffic that did make it into hello Frontend or Backend subnets would be directed out toohello firewall (thanks tooUDR).</span></span> <span data-ttu-id="d9bf7-192">Zapora Hello będzie traktować jako asymetrycznego przepływu i spowoduje pominięcie hello ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-192">hello firewall would see this as an asymmetric flow and would drop hello outbound traffic.</span></span> <span data-ttu-id="d9bf7-193">W związku z tym istnieją trzy warstwy zabezpieczeń Ochrona powitalnych frontonu i wewnętrznej bazy danych podsieci; 1) nie Otwórz punkty końcowe na powitania FrontEnd001 i usługi w chmurze BackEnd001, 2) grupy NSG zezwalających na ruch z Internetu, 3) hello Zapora porzucenie asymetrycznego ruchu hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-193">Thus there are three layers of security protecting hello Frontend and Backend subnets; 1) no open endpoints on hello FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from hello Internet, 3) hello firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="d9bf7-194">Jeden punkt interesujące dotyczące hello sieciowej grupy zabezpieczeń w tym przykładzie jest, że zawiera on tylko jedną regułę, pokazano poniżej, czyli toodeny internet ruchu toohello całej sieci wirtualnej, która obejmuje hello zabezpieczeń podsieci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-194">One interesting point regarding hello Network Security Group in this example is that it contains only one rule, shown below, which is toodeny internet traffic toohello entire virtual network which would include hello Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="d9bf7-195">Jednak ponieważ hello grupa NSG jest tylko powiązana toohello frontonu i wewnętrznej bazy danych podsieci, reguła hello nie jest przetwarzana ruchu przychodzącego toohello zabezpieczeń podsieci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-195">However, since hello NSG is only bound toohello Frontend and Backend subnets, hello rule isn’t processed on traffic inbound toohello Security subnet.</span></span> <span data-ttu-id="d9bf7-196">W związku z tym mimo że reguły NSG hello jest wyświetlany komunikat nie adres internetowy ruch tooany na powitania sieci wirtualnej, ponieważ powitalne NSG nigdy nie został powiązany podsieci zabezpieczeń toohello ruch będzie przepływać toohello zabezpieczeń podsieci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-196">As a result, even though hello NSG rule says no Internet traffic tooany address on hello VNet, because hello NSG was never bound toohello Security subnet, traffic will flow toohello Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="d9bf7-197">Reguły zapory</span><span class="sxs-lookup"><span data-stu-id="d9bf7-197">Firewall Rules</span></span>
<span data-ttu-id="d9bf7-198">W zaporze hello przekazywania zasady należy toobe utworzony.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-198">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="d9bf7-199">Ponieważ Zapora hello jest blokowanie lub funkcji przekazywania wszystkich przychodzące, wychodzące, sieć wirtualną wewnątrz ruchu wiele reguł zapory są wymagane.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-199">Since hello firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="d9bf7-200">Ponadto cały ruch przychodzący nastąpi trafienie hello usługi zabezpieczeń publicznego adresu IP (różne porty), toobe przetworzony przez zaporę Windows hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-200">Also, all inbound traffic will hit hello Security Service public IP address (on different ports), toobe processed by hello firewall.</span></span> <span data-ttu-id="d9bf7-201">Najlepszym rozwiązaniem jest toodiagram hello logicznej przepływów przed rozpoczęciem konfigurowania później hello podsieci i przeróbek tooavoid reguł zapory.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-201">A best practice is toodiagram hello logical flows before setting up hello subnets and firewall rules tooavoid rework later.</span></span> <span data-ttu-id="d9bf7-202">Witaj poniższej ilustracji jest widok logiczny hello reguły zapory w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-202">hello following figure is a logical view of hello firewall rules for this example:</span></span>

<span data-ttu-id="d9bf7-203">![Widok logiczny hello reguły zapory][2]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-203">![Logical View of hello Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="d9bf7-204">Oparte na powitania używanych przez urządzenie wirtualne sieci, porty zarządzania hello będą się różnić.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-204">Based on hello Network Virtual Appliance used, hello management ports will vary.</span></span> <span data-ttu-id="d9bf7-205">W tym przykładzie, który odwołuje się do zapory NextGen Barracuda, który używa portów 22, 801 i 807.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="d9bf7-206">Przejrzyj hello urządzenia dostawcy dokumentacji toofind hello porty używane do zarządzania hello urządzenie używane.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-206">Please consult hello appliance vendor documentation toofind hello exact ports used for management of hello device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="d9bf7-207">Opis reguły logiczne</span><span class="sxs-lookup"><span data-stu-id="d9bf7-207">Logical Rule Description</span></span>
<span data-ttu-id="d9bf7-208">W hello logicznej powyższym diagramie hello zabezpieczeń podsieci nie jest wyświetlane, ponieważ zapory hello hello tylko zasobów tej podsieci, a ten diagram jest wyświetlany hello reguły zapory i sposób ich logicznie akceptować lub odrzucać przepływów ruchu sieciowego i nie hello routingiem ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-208">In hello logical diagram above, hello security subnet is not shown since hello firewall is hello only resource on that subnet, and this diagram is showing hello firewall rules and how they logically allow or deny traffic flows and not hello actual routed path.</span></span> <span data-ttu-id="d9bf7-209">Ponadto zewnętrzne porty hello wybrany na potrzeby hello na ruch RDP są wyższe ranged portów (8014 — 8026) i zostały wybrane toosomewhat są wyrównane z hello ostatni dwa oktety hello lokalny adres IP dla czytelności łatwiejsze (np. adres serwera lokalnego 10.0.1.4 jest skojarzony z portu zewnętrznego 8014), jednak można użyć żadnych wyższej niekolidujących portów.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-209">Also, hello external ports selected for hello RDP traffic are higher ranged ports (8014 – 8026) and were selected toosomewhat align with hello last two octets of hello local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="d9bf7-210">Na przykład potrzebujemy 7 typów reguł, te typy reguł są opisane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="d9bf7-211">Reguły zewnętrzne (dla ruchu przychodzącego):</span><span class="sxs-lookup"><span data-stu-id="d9bf7-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="d9bf7-212">Zarządzanie reguła: Ta zasada przekierowania aplikacji umożliwia ruch toopass toohello zarządzania porty urządzenie wirtualne hello sieci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-212">Firewall Management Rule: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance.</span></span>
  2. <span data-ttu-id="d9bf7-213">Zasady protokołu RDP (na każdym serwerze z systemem windows): następujące cztery reguły (po jednym dla każdego serwera) umożliwi Zarządzanie hello poszczególnych serwerów za pomocą protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of hello individual servers via RDP.</span></span> <span data-ttu-id="d9bf7-214">Może to być również połączone w jedną regułę w zależności od możliwości hello hello urządzenie wirtualne sieci używane.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-214">This could also be bundled into one rule depending on hello capabilities of hello Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="d9bf7-215">Reguły ruchu aplikacji: Istnieją dwie reguły ruchu aplikacji hello najpierw dla ruchu w sieci web frontonu hello i hello drugi transmisji hello zaplecza (np warstwa sieci web serwera toodata).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-215">Application Traffic Rules: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="d9bf7-216">Konfiguracja Hello tych zasad będzie zależeć od architektury sieci hello (w którym są umieszczane serwerów) oraz ruch (które ruchu hello kierunek przepływu i które porty są używane).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-216">hello configuration of these rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="d9bf7-217">Pierwsza reguła Hello umożliwi serwera aplikacji hello tooreach ruch rzeczywisty aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-217">hello first rule will allow hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="d9bf7-218">Hello inne zasady Zezwalaj na zabezpieczenia, zarządzanie, itp., reguły aplikacji są co Zezwalaj zewnętrznych tooaccess użytkowników lub usług aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-218">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="d9bf7-219">Na przykład jest jednym serwerze sieci web na porcie 80, w związku z tym regułę zapory jednej aplikacji przekieruje ruch przychodzący toohello IP zewnętrznego, toohello serwerów wewnętrzny adres IP sieci web.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span> <span data-ttu-id="d9bf7-220">Witaj przekierowanie ruchu sesji ma NAT może być toohello wewnętrznego serwera.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-220">hello redirected traffic session would be NAT’d toohello internal server.</span></span>
     * <span data-ttu-id="d9bf7-221">Hello jest drugą regułę ruchu aplikacji hello wewnętrzna reguła tooallow powitania serwera sieci Web tootalk toohello AppVM01 serwera (ale nie AppVM02) za pomocą dowolnego portu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-221">hello second Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="d9bf7-222">Wewnętrzne zasady (dla ruchu w sieci wirtualnej wewnątrz)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="d9bf7-223">TooInternet wychodzących reguł: Ta reguła będzie zezwalać na ruch z dowolnej sieci toopass toohello wybrane sieci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-223">Outbound tooInternet Rule: This rule will allow traffic from any network toopass toohello selected networks.</span></span> <span data-ttu-id="d9bf7-224">Ta reguła jest zwykle domyślna reguła już na powitania zapory, ale w stanie wyłączenia.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-224">This rule is usually a default rule already on hello firewall, but in a disabled state.</span></span> <span data-ttu-id="d9bf7-225">Ta reguła powinna być włączona w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="d9bf7-226">Reguła DNS: Ta zasada umożliwia tylko DNS (port 53) ruchu toopass toohello serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-226">DNS Rule: This rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="d9bf7-227">Dla tego środowiska, większość ruchu z toohello frontonu hello wewnętrznej bazy danych jest zablokowany ta zasada umożliwia DNS w szczególności z żadnych podsieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-227">For this environment most traffic from hello Frontend toohello Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="d9bf7-228">Podsieci tooSubnet reguły: Ta reguła jest tooallow dowolnego serwera na powitania wstecz kończyć podsieci tooconnect tooany serwera na powitania podsieci frontonu (ale nie hello odwrotnej).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-228">Subnet tooSubnet Rule: This rule is tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet (but not hello reverse).</span></span>
* <span data-ttu-id="d9bf7-229">Reguła awaryjnego (dla ruchu, który nie spełnia żadnego z hello powyżej):</span><span class="sxs-lookup"><span data-stu-id="d9bf7-229">Fail-safe Rule (for traffic that doesn’t meet any of hello above):</span></span>
  1. <span data-ttu-id="d9bf7-230">Odmów wszystkie reguły ruchu: To zawsze powinna być hello reguły końcowego (w zakresie priorytet), a jako takie Jeśli przepływa ruch nie toomatch żadnego hello poprzedzających reguł, które zostaną usunięte przez tę regułę.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-230">Deny All Traffic Rule: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="d9bf7-231">Jest to domyślna reguła i zwykle jest aktywna, żadnych modyfikacji nie są zwykle wymagane.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="d9bf7-232">Na powitania drugą regułę ruchu aplikacji każdy port jest dozwolony dla łatwy w tym przykładzie, hello rzeczywistym scenariuszu najbardziej określonych zakresów port i adres powinien być używany tooreduce hello ataku tej reguły.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-232">On hello second application traffic rule, any port is allowed for easy of this example, in a real scenario hello most specific port and address ranges should be used tooreduce hello attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="d9bf7-233">Po utworzeniu wszystkich hello powyżej reguły, ważne jest tooreview hello priorytetu ruchu tooensure każdej reguły, które ma być dozwolony lub zabroniony zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-233">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="d9bf7-234">W tym przykładzie są reguły hello w kolejności priorytetu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-234">For this example, hello rules are in priority order.</span></span> <span data-ttu-id="d9bf7-235">Jest łatwy toobe zablokowane zapory hello powodu uporządkowane toomis reguły.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-235">It's easy toobe locked out of hello firewall due toomis-ordered rules.</span></span> <span data-ttu-id="d9bf7-236">Co najmniej upewnij się, że hello zarządzania samą zaporę hello jest zawsze hello bezwzględną najwyższy priorytet reguły.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-236">At a minimum, ensure hello management for hello firewall itself is always hello absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="d9bf7-237">Reguły wymagań wstępnych</span><span class="sxs-lookup"><span data-stu-id="d9bf7-237">Rule Prerequisites</span></span>
<span data-ttu-id="d9bf7-238">Jeden wymagań wstępnych dla zapory hello uruchomionej maszyny wirtualnej hello są publiczne punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-238">One prerequisite for hello Virtual Machine running hello firewall are public endpoints.</span></span> <span data-ttu-id="d9bf7-239">Dla ruchu tooprocess zapory hello hello odpowiednie publiczne punkty końcowe musi być otwarty.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-239">For hello firewall tooprocess traffic hello appropriate public endpoints must be open.</span></span> <span data-ttu-id="d9bf7-240">Istnieją trzy typy ruchu w tym przykładzie; 1) zarządzania ruchu toocontrol hello zapory i reguły zapory, serwerów windows hello toocontrol ruch RDP 2) i ruchu 3) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-240">There are three types of traffic in this example; 1) Management traffic toocontrol hello firewall and firewall rules, 2) RDP traffic toocontrol hello windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="d9bf7-241">Są trzy kolumny hello typów ruchu w górnym hello połowy widok logiczny reguł zapory hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-241">These are hello three columns of traffic types in hello upper half of logical view of hello firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9bf7-242">W tym miejscu klucza takeway jest tooremember który **wszystkie** ruchu rozpocznie się przez zaporę Windows hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-242">A key takeway here is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="d9bf7-243">Tak pulpitu tooremote toohello IIS01 serwera, nawet jeśli komputer jest w hello Front End chmury usługi i podsieci frontonu hello, tooaccess tego serwera, potrzebne będą tooRDP toohello zapory na porcie 8014, a następnie wewnętrznie Pozwól hello zapory tooroute hello RDP żądania toohello IIS01 portem RDP.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-243">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="d9bf7-244">Witaj portalu Azure "Połącz" przycisku nie będzie działać, ponieważ nie istnieje żadne bezpośrednie tooIIS01 ścieżkę protokołu RDP (o ile hello portalu można zobaczyć).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-244">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="d9bf7-245">Oznacza to, że wszystkie połączenia z hello internet będzie toohello usługi zabezpieczeń i Port, np. secscv001.cloudapp.net:xxxx (odwołanie hello powyżej diagram mapowania hello portu zewnętrznego i wewnętrznym adresem IP i Port).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-245">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference hello above diagram for hello mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="d9bf7-246">Punkt końcowy można otworzyć w momencie hello tworzenia maszyny Wirtualnej lub po kompilacji jest przeprowadzane w hello przykładowy skrypt i przedstawionym poniżej na następujący fragment kodu (Uwaga; dowolnego elementu, począwszy od znak dolara (np.: $VMName[$i]) jest zmienną zdefiniowanych przez użytkownika ze skryptu hello w hello referen CE sekcji tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-246">An endpoint can be opened either at hello time of VM creation or post build as is done in hello example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="d9bf7-247">Witaj "$i" w nawiasach [$i] reprezentuje hello tablicy liczbę określonej maszyny Wirtualnej w tablicy maszyn wirtualnych):</span><span class="sxs-lookup"><span data-stu-id="d9bf7-247">hello “$i” in brackets, [$i], represents hello array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="d9bf7-248">Mimo że nie wyraźnie przedstawiony tutaj powodu toohello użycie zmiennych, ale punkty końcowe są **tylko** otwarte na powitania zabezpieczeń usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-248">Although not clearly shown here due toohello use of variables, but endpoints are **only** opened on hello Security Cloud Service.</span></span> <span data-ttu-id="d9bf7-249">Jest to tooensure obsługi cały ruch przychodzący (kierowane, translatora adresów Sieciowych porzucone) przez zaporę Windows hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-249">This is tooensure that all inbound traffic is handled (routed, NAT'd, dropped) by hello firewall.</span></span>

<span data-ttu-id="d9bf7-250">Klienta zarządzania należy toobe zainstalowany w zaporze hello toomanage komputera, a następnie utwórz wymagane konfiguracje hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-250">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="d9bf7-251">Zobacz hello dostawcy dokumentacji zapory (lub inne NVA) w sposób toomanage hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-251">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="d9bf7-252">Hello pozostałej części tej sekcji i hello następnej sekcji, tworzenie reguł zapory, opisano konfigurację hello hello zapory, za pośrednictwem powitania klienta zarządzania dostawców (tj. hello portalu Azure lub programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-252">hello remainder of this section and hello next section, Firewall Rules Creation, will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="d9bf7-253">Instrukcje dotyczące pobierania klienta i łączenia toohello Barracuda używana w tym przykładzie można znaleźć tutaj: [Barracuda NG administratora](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-253">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="d9bf7-254">Po zalogowaniu się na powitania zapory, ale przed utworzeniem reguły zapory, istnieją dwie klasy obiektu wymagań wstępnych, które ułatwia tworzenie reguł hello; Obiekty sieci i usługi.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-254">Once logged onto hello firewall but before creating firewall rules, there are two prerequisite object classes that can make creating hello rules easier; Network & Service objects.</span></span>

<span data-ttu-id="d9bf7-255">W tym przykładzie trzy obiekty nazwanej sieci powinien być zdefiniowany (jeden dla podsieci Frontend hello i hello podsieci wewnętrznej bazy danych, również obiekt sieci hello adres IP serwera DNS hello).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-255">For this example, three named network objects should be defined (one for hello Frontend subnet and hello Backend subnet, also a network object for hello IP address of hello DNS server).</span></span> <span data-ttu-id="d9bf7-256">toocreate nazwanej sieci; począwszy od pulpitu nawigacyjnego klienta Barracuda NG Admin hello, przejdź na kartę Konfiguracja toohello, w hello sekcji konfiguracji operacyjnych kliknij zestaw reguł, kliknij przycisk "Sieci" w menu obiekty zapory hello, a następnie kliknij przycisk Nowa, w menu Edycja sieci hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-256">toocreate a named network; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Networks” under hello Firewall Objects menu, then click New in hello Edit Networks menu.</span></span> <span data-ttu-id="d9bf7-257">Hello sieci można teraz można utworzyć obiektu, dodając nazwy hello i prefiksu hello:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-257">hello network object can now be created, by adding hello name and hello prefix:</span></span>

<span data-ttu-id="d9bf7-258">![Utwórz obiekt sieci frontonu][3]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="d9bf7-259">Spowoduje to utworzenie nazwanej sieci dla podsieci FrontEnd hello, należy utworzyć obiekt podobny hello również podsieci wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-259">This will create a named network for hello FrontEnd subnet, a similar object should be created for hello BackEnd subnet as well.</span></span> <span data-ttu-id="d9bf7-260">Teraz hello podsieci można łatwiej odwoływać się do nazwy w regułach zapory hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-260">Now hello subnets can be more easily referenced by name in hello firewall rules.</span></span>

<span data-ttu-id="d9bf7-261">Dla hello obiektu serwera DNS:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-261">For hello DNS Server Object:</span></span>

<span data-ttu-id="d9bf7-262">![Utwórz obiekt serwera DNS][4]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="d9bf7-263">Ten jedno odwołanie adres IP zostanie wykorzystana w regule DNS w dalszej części dokumentu hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-263">This single IP address reference will be utilized in a DNS rule later in hello document.</span></span>

<span data-ttu-id="d9bf7-264">drugi obiekty wymagań wstępnych Hello są obiektami usługi.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-264">hello second prerequisite objects are Services objects.</span></span> <span data-ttu-id="d9bf7-265">Te będą stanowiły hello portów połączeń protokołu RDP dla każdego serwera.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-265">These will represent hello RDP connection ports for each server.</span></span> <span data-ttu-id="d9bf7-266">Ponieważ hello istniejący obiekt usługi protokołu RDP jest powiązane toohello domyślnym portem RDP, 3389, nowych usług mogą być tworzone tooallow ruchu z portów zewnętrznych hello (8014 8026).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-266">Since hello existing RDP service object is bound toohello default RDP port, 3389, new Services can be created tooallow traffic from hello external ports (8014-8026).</span></span> <span data-ttu-id="d9bf7-267">Hello nowych portów można również dodać toohello istniejącej usługi protokołu RDP, ale w celu ułatwienia demonstracyjnych, można utworzyć regułę dla każdego serwera.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-267">hello new ports could also be added toohello existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="d9bf7-268">toocreate nowej reguły protokołu RDP dla serwera; począwszy od hello Barracuda NG administratora klient pulpitu nawigacyjnego, przejdź na kartę Konfiguracja toohello, w hello konfigurację operacyjną kliknij zestaw reguł, sekcji, a następnie kliknij przycisk "Usługi" w obszarze hello menu obiekty zapory, przewiń w dół listę hello usług i wybierz hello Usługa "RDP".</span><span class="sxs-lookup"><span data-stu-id="d9bf7-268">toocreate a new RDP rule for a server; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Services” under hello Firewall Objects menu, scroll down hello list of services and select hello “RDP” service.</span></span> <span data-ttu-id="d9bf7-269">Kliknij prawym przyciskiem myszy i wybierz Kopiuj, a następnie kliknij prawym przyciskiem myszy i wybierz Wklej.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="d9bf7-270">Teraz jest obiektem usługi RDP Copy1, które mogą być edytowane.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="d9bf7-271">Kliknij prawym przyciskiem myszy RDP Copy1 i wybrać edycji, hello Edytuj obiekt usługi oknie wyskakującym zostanie w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-271">Right-click RDP-Copy1 and select Edit, hello Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="d9bf7-272">![Kopiowanie reguły domyślnej protokołu RDP][5]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="d9bf7-273">wartości Hello następnie może być edytowany toorepresent hello usługi protokołu RDP dla określonego serwera.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-273">hello values can then be edited toorepresent hello RDP service for a specific server.</span></span> <span data-ttu-id="d9bf7-274">W przypadku hello AppVM01 powyżej domyślnej reguły protokołu RDP powinien być zmodyfikowane tooreflect nową nazwę usługi, opis, i portu zewnętrznego RDP używane w hello diagram rysunek 8 (Uwaga: hello portów nie zostaną zmienione hello RDP domyślną 3389 portu zewnętrznego toohello używany dla tego określonego serwera w przypadku hello portu zewnętrznego AppVM01 hello jest 8025) hello zmodyfikowane usługi przedstawiono poniżej:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-274">For AppVM01 hello above default RDP rule should be modified tooreflect a new Service Name, Description, and external RDP Port used in hello Figure 8 diagram (Note: hello ports are changed from hello RDP default of 3389 toohello external port being used for this specific server, in hello case of AppVM01 hello external Port is 8025) hello modified service is shown below:</span></span>

<span data-ttu-id="d9bf7-275">![Reguła AppVM01][6]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="d9bf7-276">Ten proces musi być powtarzane toocreate usługi protokołu RDP dla hello pozostałych serwerów; AppVM02 DNS01 i IIS01.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-276">This process must be repeated toocreate RDP Services for hello remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="d9bf7-277">Tworzenie Hello tych usług będzie tworzenia reguły hello prostszy i bardziej oczywistymi w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-277">hello creation of these Services will make hello Rule creation simpler and more obvious in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="d9bf7-278">Usługa protokołu RDP dla hello zapory nie jest wymagana dwóch powodów; 1) pierwsze zapory hello maszyny Wirtualnej jest obrazem opartymi na systemie Linux SSH będzie używany port 22 dla maszyny Wirtualnej zarządzania zamiast protokołu RDP, a port 22 2) i dwa porty zarządzania są dozwolone w hello pierwszej reguły zarządzania opisane poniżej tooallow zarządzania łączności.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-278">An RDP service for hello Firewall is not needed for two reasons; 1) first hello firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in hello first management rule described below tooallow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="d9bf7-279">Tworzenie reguły zapory</span><span class="sxs-lookup"><span data-stu-id="d9bf7-279">Firewall Rules Creation</span></span>
<span data-ttu-id="d9bf7-280">Istnieją trzy typy reguł zapory, w tym przykładzie, wszystkie mają różne ikony:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="d9bf7-281">Reguła przekierowania aplikacji Hello: ![przekierowania ikona aplikacji][7]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-281">hello Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="d9bf7-282">Reguła NAT docelowego Hello: ![docelowym translacji adresów Sieciowych ikony][8]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-282">hello Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="d9bf7-283">Reguła przebiegu Hello: ![Przekaż ikonę][9]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-283">hello Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="d9bf7-284">Więcej informacji na temat tych zasad można znaleźć w witrynie sieci web Barracuda hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-284">More information on these rules can be found at hello Barracuda web site.</span></span>

<span data-ttu-id="d9bf7-285">toocreate hello następujące zasady (lub sprawdź istniejących reguł domyślnych), zaczynając od pulpitu nawigacyjnego klienta Barracuda NG Admin hello, przejdź na kartę Konfiguracja toohello w hello konfigurację operacyjną sekcji kliknij pozycję zestaw reguł.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-285">toocreate hello following rules (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="d9bf7-286">Wywołuje siatkę, "Main reguły" wyświetli hello istniejących reguł active i zdezaktywowane tej zapory.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-286">A grid called, “Main Rules” will show hello existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="d9bf7-287">W hello prawego górnego rogu tej siatki jest mały, zielony "+", kliknij ten toocreate nową regułę (Uwaga: Zapora może być "zablokowana" zmian, jeśli przycisk oznaczony jako "Lock" i są toocreate lub Edytuj reguły, kliknij ten przycisk, zbyt "Odblokuj" hello se reguły t i Zezwól na edytowanie).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-287">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello rule set and allow editing).</span></span> <span data-ttu-id="d9bf7-288">Jeśli chcesz, aby tooedit istniejącą regułę, wybierz tej reguły, kliknij prawym przyciskiem myszy i wybierz edytowanie reguły.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-288">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="d9bf7-289">Gdy reguły są tworzone i/lub zmodyfikowane, musi być przypisany toohello zapory, a następnie aktywowany, jeśli nie zostanie to zrobione reguły hello zmiany nie zostaną wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-289">Once your rules are created and/or modified, they must be pushed toohello firewall and then activated, if this is not done hello rule changes will not take effect.</span></span> <span data-ttu-id="d9bf7-290">opisano sposób wypychania i aktywacji Hello poniżej hello szczegóły reguły opisy.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-290">hello push and activation process is described below hello details rule descriptions.</span></span>

<span data-ttu-id="d9bf7-291">Szczegóły Hello każdej reguły wymagane toocomplete w tym przykładzie są opisane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-291">hello specifics of each rule required toocomplete this example are described as follows:</span></span>

* <span data-ttu-id="d9bf7-292">**Zarządzanie reguły zapory**: ten przekierowania aplikacji reguła zezwala na ruch portów zarządzania toohello toopass hello sieci urządzenie wirtualne, w tym przykładzie zapory NextGen Barracuda.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-292">**Firewall Management Rule**: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="d9bf7-293">porty zarządzania Hello są 801, 807 i opcjonalnie 22.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-293">hello management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="d9bf7-294">Witaj zewnętrznych i wewnętrznych portów są hello takie same (tzn. bez translacji port).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-294">hello external and internal ports are hello same (i.e. no port translation).</span></span> <span data-ttu-id="d9bf7-295">Reguły i ustawienia dostępu do danych, reguła domyślna i domyślnie włączona (w wersji zapory NextGen Barracuda 6.1).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="d9bf7-296">![Reguły zapory zarządzania][10]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="d9bf7-297">Hello przestrzeni adresowej źródła w tej regule jest dowolne, jeśli hello zakresów adresów IP zarządzania są znane, zmniejszając ten zakres będzie również zmniejszyć porty zarządzania powierzchni toohello atak powitania.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-297">hello source address space in this rule is Any, if hello management IP address ranges are known, reducing this scope would also reduce hello attack surface toohello management ports.</span></span>
> 
> 

* <span data-ttu-id="d9bf7-298">**Zasady protokołu RDP**: reguł NAT przeznaczenia tych umożliwi Zarządzanie hello poszczególnych serwerów za pomocą protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-298">**RDP Rules**:  These Destination NAT rules will allow management of hello individual servers via RDP.</span></span>
  <span data-ttu-id="d9bf7-299">Istnieją cztery toocreate wymagane pola krytyczne tej reguły:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-299">There are four critical fields needed toocreate this rule:</span></span>
  
  1. <span data-ttu-id="d9bf7-300">Źródło — tooallow protokołu RDP z dowolnego miejsca, odwołanie hello "Dowolne" jest używany w polu źródła hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-300">Source – tooallow RDP from anywhere, hello reference “Any” is used in hello Source field.</span></span>
  2. <span data-ttu-id="d9bf7-301">Usługi — używają powitalne odpowiedniego obiektu usługi utworzony wcześniej, w tym przypadku "AppVM01 RDP", zewnętrzne porty hello przekierowania toohello serwerów lokalny adres IP i tooport 3386 (hello domyślny port protokołu RDP).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-301">Service – use hello appropriate Service Object created earlier, in this case “AppVM01 RDP”, hello external ports redirect toohello servers local IP address and tooport 3386 (hello default RDP port).</span></span> <span data-ttu-id="d9bf7-302">Ta reguła określonych ma tooAppVM01 dostępu RDP.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-302">This specific rule is for RDP access tooAppVM01.</span></span>
  3. <span data-ttu-id="d9bf7-303">Miejsce docelowe — powinno być hello *portów lokalnych na zaporze hello*, "DCHP 1 lokalny adres IP" lub eth0 używania statycznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-303">Destination – should be hello *local port on hello firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="d9bf7-304">numer porządkowy Hello (eth0, eth1 itp.) może się różnić, jeśli urządzenia sieciowe ma wiele interfejsów lokalnych.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-304">hello ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="d9bf7-305">Jest to hello port zapory hello wysyła z (może to być hello takie same jak hello odbieranie portu), pole listy docelowej hello jest hello rzeczywistego przeznaczenia routingiem.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-305">This is hello port hello firewall is sending out from (may be hello same as hello receiving port), hello actual routed destination is in hello Target List field.</span></span>
  4. <span data-ttu-id="d9bf7-306">Przekierowanie — w tej sekcji opisano urządzenie wirtualne hello gdzie tooultimately przekierować ruch.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-306">Redirection – this section tells hello virtual appliance where tooultimately redirect this traffic.</span></span> <span data-ttu-id="d9bf7-307">Najprostsza przekierowania Hello jest tooplace hello IP i Port (opcjonalnie) w polu listy docelowej hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-307">hello simplest redirection is tooplace hello IP and Port (optional) in hello Target List field.</span></span> <span data-ttu-id="d9bf7-308">Jeśli nie jest używane hello port docelowy na żądanie przychodzące hello będzie używany (ie nie tłumaczenie), jeśli port jest wybrany hello port będzie również NAT oraz hello IP zajmie się.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-308">If no port is used hello destination port on hello inbound request will be used (ie no translation), if a port is designated hello port will also be NAT’d along with hello IP address.</span></span>
     
     <span data-ttu-id="d9bf7-309">![Reguły zapory protokołu RDP][11]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="d9bf7-310">Łącznie cztery reguły protokołu RDP, należy utworzyć toobe:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-310">A total of four RDP rules will need toobe created:</span></span> 
     
     | <span data-ttu-id="d9bf7-311">Nazwa reguły</span><span class="sxs-lookup"><span data-stu-id="d9bf7-311">Rule Name</span></span> | <span data-ttu-id="d9bf7-312">Serwer</span><span class="sxs-lookup"><span data-stu-id="d9bf7-312">Server</span></span> | <span data-ttu-id="d9bf7-313">Usługa</span><span class="sxs-lookup"><span data-stu-id="d9bf7-313">Service</span></span> | <span data-ttu-id="d9bf7-314">Listy docelowej</span><span class="sxs-lookup"><span data-stu-id="d9bf7-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="d9bf7-315">RDP-IIS01</span><span class="sxs-lookup"><span data-stu-id="d9bf7-315">RDP-to-IIS01</span></span> |<span data-ttu-id="d9bf7-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="d9bf7-316">IIS01</span></span> |<span data-ttu-id="d9bf7-317">IIS01 PROTOKOŁU RDP</span><span class="sxs-lookup"><span data-stu-id="d9bf7-317">IIS01 RDP</span></span> |<span data-ttu-id="d9bf7-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="d9bf7-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="d9bf7-319">RDP-DNS01</span><span class="sxs-lookup"><span data-stu-id="d9bf7-319">RDP-to-DNS01</span></span> |<span data-ttu-id="d9bf7-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="d9bf7-320">DNS01</span></span> |<span data-ttu-id="d9bf7-321">DNS01 PROTOKOŁU RDP</span><span class="sxs-lookup"><span data-stu-id="d9bf7-321">DNS01 RDP</span></span> |<span data-ttu-id="d9bf7-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="d9bf7-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="d9bf7-323">RDP-AppVM01</span><span class="sxs-lookup"><span data-stu-id="d9bf7-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="d9bf7-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="d9bf7-324">AppVM01</span></span> |<span data-ttu-id="d9bf7-325">AppVM01 protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="d9bf7-325">AppVM01 RDP</span></span> |<span data-ttu-id="d9bf7-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="d9bf7-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="d9bf7-327">RDP-AppVM02</span><span class="sxs-lookup"><span data-stu-id="d9bf7-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="d9bf7-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="d9bf7-328">AppVM02</span></span> |<span data-ttu-id="d9bf7-329">AppVm02 protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="d9bf7-329">AppVm02 RDP</span></span> |<span data-ttu-id="d9bf7-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="d9bf7-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="d9bf7-331">Zawęzić zakres hello hello źródła i pola usługi zmniejsza możliwości ataku hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-331">Narrowing down hello scope of hello Source and Service fields will reduce hello attack surface.</span></span> <span data-ttu-id="d9bf7-332">zakres Hello najbardziej ograniczone, który umożliwi funkcji powinny być używane.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-332">hello most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="d9bf7-333">**Reguły ruchu aplikacji**: istnieją dwie reguły ruchu aplikacji hello najpierw dla ruchu w sieci web frontonu hello i hello drugi transmisji hello zaplecza (np warstwa sieci web serwera toodata).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-333">**Application Traffic Rules**: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="d9bf7-334">Te reguły będzie zależeć od architektury sieci hello (w którym są umieszczane serwerów) oraz ruch (które ruchu hello kierunek przepływu i które porty są używane).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-334">These rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="d9bf7-335">Najpierw omówiona jest hello frontonu reguły dla ruchu w sieci web:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-335">First discussed is hello front end rule for web traffic:</span></span>
  
    <span data-ttu-id="d9bf7-336">![Reguła zapory w sieci Web][12]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="d9bf7-337">Ta reguła NAT docelowym zezwala serwerowi aplikacji hello tooreach hello rzeczywistej aplikacji ruchu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-337">This Destination NAT rule allows hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="d9bf7-338">Hello inne zasady Zezwalaj na zabezpieczenia, zarządzanie, itp., reguły aplikacji są co Zezwalaj zewnętrznych tooaccess użytkowników lub usług aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-338">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="d9bf7-339">Na przykład jest jednym serwerze sieci web na porcie 80, w związku z tym hello pojedynczą aplikacji regułę zapory przekieruje ruch przychodzący toohello IP zewnętrznego, toohello serwerów wewnętrzny adres IP sieci web.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-339">For this example, there is a single web server on port 80, thus hello single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span>
  
    <span data-ttu-id="d9bf7-340">**Uwaga**: czy istnieje nie portu przypisane w polu listy docelowej hello, w związku z tym hello przychodzący port 80 (lub 443 dla wybranej usługi hello) będzie używany w przekierowania hello powitania serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-340">**Note**: that there is no port assigned in hello Target List field, thus hello inbound port 80 (or 443 for hello Service selected) will be used in hello redirection of hello web server.</span></span> <span data-ttu-id="d9bf7-341">Jeśli serwer sieci web hello nasłuchuje na innym porcie, na przykład portu 8080, pole listy docelowej hello może być tooallow too10.0.1.4:8080 Zaktualizowano również przekierowania portu hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-341">If hello web server is listening on a different port, for example port 8080, hello Target List field could be updated too10.0.1.4:8080 tooallow for hello Port redirection as well.</span></span>
  
    <span data-ttu-id="d9bf7-342">Hello jest dalej reguły ruchu aplikacji hello wewnętrzna reguła tooallow powitania serwera sieci Web tootalk toohello AppVM01 serwera (ale nie AppVM02) za pośrednictwem usługi:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-342">hello next Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="d9bf7-343">![Reguły zapory AppVM01][13]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="d9bf7-344">Ta zasada przebiegu umożliwia dowolnego serwera IIS na powitania serwera sieci Web podsieci tooreach hello AppVM01 (adres IP 10.0.2.5) na dowolnym porcie przy użyciu protokołu danych tooaccess wymagane przez aplikację sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-344">This Pass rule allows any IIS server on hello Frontend subnet tooreach hello AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol tooaccess data needed by hello web application.</span></span>
  
    <span data-ttu-id="d9bf7-345">W tym zrzucie ekranu "\<jawne dest\>" jest używany w toosignify pola docelowego hello 10.0.2.5 jako miejsce docelowe hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-345">In this screen shot an "\<explicit-dest\>" is used in hello Destination field toosignify 10.0.2.5 as hello destination.</span></span> <span data-ttu-id="d9bf7-346">Może to być albo jawne pokazany lub a o nazwie obiektu Network (jak to zostało zrobione wymagań wstępnych hello powitania serwera DNS).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-346">This could be either explicit as shown or a named Network Object (as was done in hello prerequisites for hello DNS server).</span></span> <span data-ttu-id="d9bf7-347">Jest to się administrator toohello zapory hello zostanie użyta metoda toowhich.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-347">This is up toohello administrator of hello firewall as toowhich method will be used.</span></span> <span data-ttu-id="d9bf7-348">Kliknij dwukrotnie hello pierwszy pusty wiersz pod tooadd 10.0.2.5 jako Explict Desitnation \<jawne dest\> , a następnie wprowadź adres hello w oknie wyskakującym hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-348">tooadd 10.0.2.5 as an Explict Desitnation, double-click on hello first blank row under \<explicit-dest\> and enter hello address in hello window that pops up.</span></span>
  
    <span data-ttu-id="d9bf7-349">Z tą regułą przekazać odłączenia translatora adresów Sieciowych jest niezbędne, ponieważ jest to wewnętrzny ruchu, hello metodę połączenia można ustawić za "Nie SNAT".</span><span class="sxs-lookup"><span data-stu-id="d9bf7-349">With this Pass Rule, no NAT is needed since this is internal traffic, so hello Connection Method can be set too"No SNAT".</span></span>
  
    <span data-ttu-id="d9bf7-350">**Uwaga**: hello sieć źródłową w tej regule jest dowolnego zasobu w podsieci frontonu hello, jeśli będą istnieć tylko jedna lub znanych określoną liczbę serwerów sieci web, obiekt sieci, zasoby mogą być tworzone toobe dokładniej toothose dokładne adresów IP zamiast Witaj całej podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-350">**Note**: hello Source network in this rule is any resource on hello FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created toobe more specific toothose exact IP addresses instead of hello entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="d9bf7-351">Ta zasada używa usługi hello toomake "Wszystkie" hello toosetup łatwiejsze przykładowej aplikacji i użyć, to będzie również umożliwiać ICMPv4 (ping) w jednej reguły.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-351">This rule uses hello service “Any” toomake hello sample application easier toosetup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="d9bf7-352">Jednak to nie jest zalecanym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="d9bf7-353">Witaj portów i protokołów ("usługi") powinna być zwężającym toohello minimalne możliwe, że umożliwia aplikacji operacji tooreduce hello ataku tej granicy.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-353">hello ports and protocols (“Services”) should be narrowed toohello minimum possible that allows application operation tooreduce hello attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="d9bf7-354">Mimo że ta zasada zawiera odwołania do jawnego dest używany, spójnego podejścia powinny być używane w konfiguracji zapory hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout hello firewall configuration.</span></span> <span data-ttu-id="d9bf7-355">Zaleca się, że hello o nazwie obiektu sieci używanego w łatwiejsze czytelności i obsługi.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-355">It is recommended that hello named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="d9bf7-356">jawne dest Hello jest używany tutaj tooshow tylko alternatywnych reference — metoda i zwykle nie jest zalecane (szczególnie w przypadku złożonych konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-356">hello explicit-dest is used here only tooshow an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="d9bf7-357">**TooInternet wychodzące reguły**: przekazać ta reguła będzie zezwalać na ruch z dowolnego źródła sieci toopass toohello wybrane miejsce docelowe sieci.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-357">**Outbound tooInternet Rule**: This Pass rule will allow traffic from any Source network toopass toohello selected Destination networks.</span></span> <span data-ttu-id="d9bf7-358">Ta reguła jest domyślna reguła zwykle już hello Barracuda NextGen zapory, ale jest w stanie wyłączenia.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-358">This rule is a default rule usually already on hello Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="d9bf7-359">Kliknięcie prawym przyciskiem myszy tę regułę można uzyskać dostęp hello uaktywnić reguły polecenia.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-359">Right-clicking on this rule can access hello Activate Rule command.</span></span> <span data-ttu-id="d9bf7-360">Reguła Hello pokazane został zmodyfikowany tooadd hello dwie podsieci lokalne utworzonych jako odwołania w sekcji wymagań wstępnych hello tego dokumentu toohello źródła atrybutu tej reguły.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-360">hello rule shown here has been modified tooadd hello two local subnets that were created as references in hello prerequisite section of this document toohello Source attribute of this rule.</span></span>
  
    <span data-ttu-id="d9bf7-361">![Reguła ruchu wychodzącego][14]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="d9bf7-362">**Reguła DNS**: przekazać ta reguła zezwala tylko DNS (port 53) ruchu toopass toohello serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="d9bf7-363">Dla tego środowiska, większość ruchu z toohello frontonu hello wewnętrznej bazy danych jest zablokowany ta zasada umożliwia w szczególności DNS.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-363">For this environment most traffic from hello FrontEnd toohello BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="d9bf7-364">![Reguły zapory DNS][15]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="d9bf7-365">**Uwaga**: na tym ekranie jest dołączony zrzut hello metodę połączenia.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-365">**Note**: In this screen shot hello Connection Method is included.</span></span> <span data-ttu-id="d9bf7-366">Ponieważ ta reguła dotyczy ruchu adres IP wewnętrznego adresu IP toointernal, NATing nie jest wymagane, to hello metodę połączenia jest ustawiany za "Nie SNAT" dla tej reguły przebiegu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-366">Because this rule is for internal IP toointernal IP address traffic, no NATing is required, this hello Connection Method is set too“No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="d9bf7-367">**Podsieci tooSubnet reguły**: przekazania tej reguły jest domyślna reguła, która została uaktywniona i modyfikacji tooallow dowolnego serwera na powitania wstecz kończyć podsieci tooconnect tooany serwera na hello podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-367">**Subnet tooSubnet Rule**: This Pass rule is a default rule that has been activated and modified tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet.</span></span> <span data-ttu-id="d9bf7-368">Ta reguła jest ruchu wszystkie wewnętrznej, hello metodę połączenia można ustawić tooNo SNAT.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-368">This rule is all internal traffic so hello Connection Method can be set tooNo SNAT.</span></span>
  
    <span data-ttu-id="d9bf7-369">![Reguła sieci wirtualnej wewnątrz zapory][16]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="d9bf7-370">**Uwaga**: hello dwukierunkowe wyboru nie jest zaznaczone (ani nie jest zaznaczone w większości reguł), to ma znaczenie dla tej reguły, ponieważ ułatwia to reguły "w jedną stronę", można zainicjować połączenia z toohello sieć frontonu hello wewnętrzna podsieć, jednak nie hello odwrotnie.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-370">**Note**: hello Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from hello back end subnet toohello front end network, but not hello reverse.</span></span> <span data-ttu-id="d9bf7-371">Jeśli pole wyboru zostało zaznaczone, ta zasada umożliwiłyby ruch dwukierunkowy, który z naszych diagram logiczny nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="d9bf7-372">**Odmów wszystkie reguły ruchu**: to zawsze powinna być hello reguły końcowego (w zakresie priorytet), i w związku Jeśli przepływa ruch toomatch kończy się niepowodzeniem żadnego hello poprzedzających reguły go zostanie usunięte przez tę regułę.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-372">**Deny All Traffic Rule**: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="d9bf7-373">Jest to domyślna reguła i zwykle jest aktywna, żadnych modyfikacji nie są zwykle wymagane.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="d9bf7-374">![Zapora regułę Odmów][17]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9bf7-375">Po utworzeniu wszystkich hello powyżej reguły, ważne jest tooreview hello priorytetu ruchu tooensure każdej reguły, które ma być dozwolony lub zabroniony zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-375">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="d9bf7-376">W tym przykładzie hello reguły są w kolejności hello powinien pojawią się one w hello siatki Main przesyłania reguły w powitania klienta zarządzania Barracuda.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-376">For this example, hello rules are in hello order they should appear in hello Main Grid of forwarding rules in hello Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="d9bf7-377">Reguły aktywacji</span><span class="sxs-lookup"><span data-stu-id="d9bf7-377">Rule Activation</span></span>
<span data-ttu-id="d9bf7-378">Specyfikacja toohello ruleset zmodyfikowane hello diagramu logiki hello, hello ruleset musi być przekazany toohello zapory, a następnie aktywowany.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-378">With hello ruleset modified toohello specification of hello logic diagram, hello ruleset must be uploaded toohello firewall and then activated.</span></span>

<span data-ttu-id="d9bf7-379">![Aktywacja reguły zapory][18]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="d9bf7-380">W prawym górnym narożniku hello powitania klienta zarządzania są klastra przycisków.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-380">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="d9bf7-381">Kliknij przycisk hello "Wyślij zmiany" przycisk toosend hello zmodyfikowane zasady toohello zapory, a następnie kliknij przycisk "Uaktywnij" hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-381">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="d9bf7-382">Z aktywacji hello zestaw reguł zapory hello tej kompilacji w środowisku przykładzie zostanie zakończona.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-382">With hello activation of hello firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="d9bf7-383">Scenariusze ruchu</span><span class="sxs-lookup"><span data-stu-id="d9bf7-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d9bf7-384">Takeway klucza jest tooremember który **wszystkie** ruchu rozpocznie się przez zaporę Windows hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-384">A key takeway is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="d9bf7-385">Tak pulpitu tooremote toohello IIS01 serwera, nawet jeśli komputer jest w hello Front End chmury usługi i podsieci frontonu hello, tooaccess tego serwera, potrzebne będą tooRDP toohello zapory na porcie 8014, a następnie wewnętrznie Pozwól hello zapory tooroute hello RDP żądania toohello IIS01 portem RDP.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-385">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="d9bf7-386">Witaj portalu Azure "Połącz" przycisku nie będzie działać, ponieważ nie istnieje żadne bezpośrednie tooIIS01 ścieżkę protokołu RDP (o ile hello portalu można zobaczyć).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-386">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="d9bf7-387">Oznacza to, że wszystkie połączenia z hello internet będzie toohello usługi zabezpieczeń i Port, np. secscv001.cloudapp.net:xxxx.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-387">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="d9bf7-388">W tych sytuacjach hello następujące reguły zapory powinny być stosowane:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-388">For these scenarios, hello following firewall rules should be in place:</span></span>

1. <span data-ttu-id="d9bf7-389">Zarządzanie zaporą</span><span class="sxs-lookup"><span data-stu-id="d9bf7-389">Firewall Management</span></span>
2. <span data-ttu-id="d9bf7-390">TooIIS01 protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="d9bf7-390">RDP tooIIS01</span></span>
3. <span data-ttu-id="d9bf7-391">TooDNS01 protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="d9bf7-391">RDP tooDNS01</span></span>
4. <span data-ttu-id="d9bf7-392">TooAppVM01 protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="d9bf7-392">RDP tooAppVM01</span></span>
5. <span data-ttu-id="d9bf7-393">TooAppVM02 protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="d9bf7-393">RDP tooAppVM02</span></span>
6. <span data-ttu-id="d9bf7-394">Toohello ruchu aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="d9bf7-394">App Traffic toohello Web</span></span>
7. <span data-ttu-id="d9bf7-395">TooAppVM01 ruchu aplikacji</span><span class="sxs-lookup"><span data-stu-id="d9bf7-395">App Traffic tooAppVM01</span></span>
8. <span data-ttu-id="d9bf7-396">Wychodzące toohello Internet</span><span class="sxs-lookup"><span data-stu-id="d9bf7-396">Outbound toohello Internet</span></span>
9. <span data-ttu-id="d9bf7-397">TooDNS01 frontonu</span><span class="sxs-lookup"><span data-stu-id="d9bf7-397">Frontend tooDNS01</span></span>
10. <span data-ttu-id="d9bf7-398">Wewnątrz podsieci ruchu (tylko koniec toofront wewnętrzna)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-398">Intra-Subnet Traffic (back end toofront end only)</span></span>
11. <span data-ttu-id="d9bf7-399">Odmów wszystkich</span><span class="sxs-lookup"><span data-stu-id="d9bf7-399">Deny All</span></span>

<span data-ttu-id="d9bf7-400">zestaw reguł zapory rzeczywiste hello najprawdopodobniej będzie miał wiele innych reguł w toothese dodanie, reguły hello na dowolnym danym zapory będą także mieć różne numery niż hello te wymienione w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-400">hello actual firewall ruleset will most likely have many other rules in addition toothese, hello rules on any given firewall will also have different priority numbers than hello ones listed here.</span></span> <span data-ttu-id="d9bf7-401">Tej listy i skojarzone z nimi numery są istotność tooprovide między tylko te reguły 11 i hello względny priorytet jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-401">This list and associated numbers are tooprovide relevance between just these eleven rules and hello relative priority amongst them.</span></span> <span data-ttu-id="d9bf7-402">Innymi słowy; zaporę rzeczywiste hello hello "RDP tooIIS01" może być numer reguły 5, ale tak długo, jak jest poniżej reguły "Zarządzanie zaporą" hello lub nowszym regułę "RDP tooDNS01" hello, którą będzie ona zgodna z zamiarem hello tej listy.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-402">In other words; on hello actual firewall, hello “RDP tooIIS01” may be rule number 5, but as long as it’s below hello “Firewall Management” rule and above hello “RDP tooDNS01” rule it would align with hello intention of this list.</span></span> <span data-ttu-id="d9bf7-403">Lista Hello także pomoże w hello poniżej scenariusze umożliwiające skrócenia; np. "Reguła Zapory 9 (DNS)".</span><span class="sxs-lookup"><span data-stu-id="d9bf7-403">hello list will also aid in hello below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="d9bf7-404">Jednak hello cztery reguły protokołu RDP będzie zbiorczo skrót, "tekst hello reguły protokołu RDP" gdy scenariusz ruchu hello jest tooRDP niepowiązanych.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-404">Also for brevity, hello four RDP rules will be collectively called, “hello RDP rules” when hello traffic scenario is unrelated tooRDP.</span></span>

<span data-ttu-id="d9bf7-405">Odwołaj również, czy grupy zabezpieczeń sieci w miejscu dla ruchu przychodzącego internet na powitania serwera sieci Web i podsieci wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-405">Also recall that Network Security Groups are in-place for inbound internet traffic on hello Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="d9bf7-406">(Dozwolone) Internet tooWeb serwera</span><span class="sxs-lookup"><span data-stu-id="d9bf7-406">(Allowed) Internet tooWeb Server</span></span>
1. <span data-ttu-id="d9bf7-407">Strony internetowe użytkownika żądania HTTP z SecSvc001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="d9bf7-408">Chmury usługi przekazuje ruch przez otwarty punkt końcowy interfejsu toofirewall port 80 na 10.0.0.4:80</span><span class="sxs-lookup"><span data-stu-id="d9bf7-408">Cloud service passes traffic through open endpoint on port 80 toofirewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="d9bf7-409">Nie NSG przypisane tooSecurity podsieci, więc reguły NSG systemu zezwalają na ruch toofirewall</span><span class="sxs-lookup"><span data-stu-id="d9bf7-409">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="d9bf7-410">Ruch trafienia wewnętrzny adres IP zapory hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-410">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="d9bf7-411">Zapora rozpoczyna przetwarzanie reguł:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="d9bf7-412">PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-412">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="d9bf7-413">Reguły Zapory 2-5 (zasad protokołu RDP) nie zastosować, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="d9bf7-414">PD zasady 6 (aplikacji: sieci Web) zastosować, ruch jest dozwolony, zapory NAT go too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it too10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="d9bf7-415">podsieci frontonu Hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-415">hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="d9bf7-416">1 reguły NSG (Zablokuj Internet) nie ma zastosowania (ruch został NAT czy przez zaporę Windows hello, w związku z tym adresu źródłowego hello jest teraz hello zaporą, który znajduje się w podsieci zabezpieczeń hello i widoczne dla podsieci Frontend hello NSG toobe "lokalnie" ruchu, w związku z tym jest dozwolone), przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Frontend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="d9bf7-417">Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG</span><span class="sxs-lookup"><span data-stu-id="d9bf7-417">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="d9bf7-418">IIS01 nasłuchuje ruchu w sieci web, otrzymuje tego żądania i rozpoczyna przetwarzanie żądania hello</span><span class="sxs-lookup"><span data-stu-id="d9bf7-418">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
8. <span data-ttu-id="d9bf7-419">IIS01 prób tooinitiates tooAppVM01 sesji FTP w podsieci wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="d9bf7-419">IIS01 attempts tooinitiates an FTP session tooAppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="d9bf7-420">Witaj przez trasy podsieci frontonu sprawia, że hello zapory hello następnego skoku</span><span class="sxs-lookup"><span data-stu-id="d9bf7-420">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
10. <span data-ttu-id="d9bf7-421">Nie reguł dla ruchu wychodzącego w podsieci frontonu, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="d9bf7-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="d9bf7-422">Zapora rozpoczyna przetwarzanie reguł:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="d9bf7-423">PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-423">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="d9bf7-424">Nie można stosować reguły Zapory 2-5 (zasad protokołu RDP), przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="d9bf7-425">PD zasady 6 (aplikacji: sieci Web) nie są spełnione, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-425">FW Rule 6 (App: Web) doesn’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="d9bf7-426">PD zasady 7 (aplikacji: wewnętrznej bazy danych) jest stosowana, ruch jest dozwolony, zapora przekazuje ruch too10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic too10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="d9bf7-427">podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-427">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="d9bf7-428">Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-428">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="d9bf7-429">Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG</span><span class="sxs-lookup"><span data-stu-id="d9bf7-429">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="d9bf7-430">AppVM01 odbiera żądanie hello i inicjuje hello sesji i odpowiada</span><span class="sxs-lookup"><span data-stu-id="d9bf7-430">AppVM01 receives hello request and initiates hello session and responds</span></span>
14. <span data-ttu-id="d9bf7-431">trasy przez Hello podsieci wewnętrznej bazy danych powoduje, że hello zapory hello następnego skoku</span><span class="sxs-lookup"><span data-stu-id="d9bf7-431">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
15. <span data-ttu-id="d9bf7-432">Ponieważ ma nie wychodzące reguły NSG na powitania odpowiedź hello podsieci wewnętrznej bazy danych jest dozwolone</span><span class="sxs-lookup"><span data-stu-id="d9bf7-432">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
16. <span data-ttu-id="d9bf7-433">Ponieważ to zwraca ruchu na zapory hello ustanowienie sesji przekazuje hello odpowiedzi serwera sieci web wstecz toohello (IIS01)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-433">Because this is returning traffic on an established session hello firewall passes hello response back toohello web server (IIS01)</span></span>
17. <span data-ttu-id="d9bf7-434">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="d9bf7-435">Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-435">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="d9bf7-436">Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG</span><span class="sxs-lookup"><span data-stu-id="d9bf7-436">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="d9bf7-437">powitania serwera IIS otrzyma odpowiedź hello, zakończeniu transakcji hello z AppVM01 i następnie kończy tworzenie hello odpowiedzi HTTP, odpowiedź HTTP zostanie wysłany toohello obiektu żądającego</span><span class="sxs-lookup"><span data-stu-id="d9bf7-437">hello IIS server receives hello response, completes hello transaction with AppVM01, and then completes building hello HTTP response, this HTTP response is sent toohello requestor</span></span>
19. <span data-ttu-id="d9bf7-438">Ponieważ ma nie wychodzące reguły NSG na powitania odpowiedź hello podsieci frontonu jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="d9bf7-438">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
20. <span data-ttu-id="d9bf7-439">Witaj zapory hello trafień odpowiedzi HTTP, a ponieważ jest to tooan odpowiedzi hello ustanowić sesji translatora adresów Sieciowych jest akceptowany przez zaporę Windows hello</span><span class="sxs-lookup"><span data-stu-id="d9bf7-439">hello HTTP response hits hello firewall, and because this is hello response tooan established NAT session is accepted by hello firewall</span></span>
21. <span data-ttu-id="d9bf7-440">Witaj zapory, a następnie przekierowuje hello toohello wstecz odpowiedzi użytkownika Internet</span><span class="sxs-lookup"><span data-stu-id="d9bf7-440">hello firewall then redirects hello response back toohello Internet User</span></span>
22. <span data-ttu-id="d9bf7-441">Ponieważ nie ma żadnych reguł NSG dla ruchu wychodzącego ani przeskoków przez podsieci frontonu hello odpowiedź hello jest dozwolone, a hello Internet użytkownik otrzymuje hello strona sieci web.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-441">Since there are no outbound NSG rules or UDR hops on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-internet-rdp-toobackend"></a><span data-ttu-id="d9bf7-442">(Dozwolone) TooBackend protokołu RDP z Internetu</span><span class="sxs-lookup"><span data-stu-id="d9bf7-442">(Allowed) Internet RDP tooBackend</span></span>
1. <span data-ttu-id="d9bf7-443">Administrator serwera w Internecie żądań tooAppVM01 sesji protokołu RDP za pośrednictwem SecSvc001.CloudApp.Net:8025, gdzie 8025 jest numer portu przypisany użytkownik hello reguły zapory "RDP tooAppVM01" hello</span><span class="sxs-lookup"><span data-stu-id="d9bf7-443">Server Admin on internet requests RDP session tooAppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is hello user assigned port number for hello “RDP tooAppVM01” firewall rule</span></span>
2. <span data-ttu-id="d9bf7-444">usługi w chmurze Hello przekazuje ruch za pośrednictwem punktu końcowego Otwórz hello interfejsu toofirewall 8025 portu na 10.0.0.4:8025</span><span class="sxs-lookup"><span data-stu-id="d9bf7-444">hello cloud service passes traffic through hello open endpoint on port 8025 toofirewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="d9bf7-445">Nie NSG przypisane tooSecurity podsieci, więc reguły NSG systemu zezwalają na ruch toofirewall</span><span class="sxs-lookup"><span data-stu-id="d9bf7-445">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="d9bf7-446">Zapora rozpoczyna przetwarzanie reguł:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="d9bf7-447">PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-447">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="d9bf7-448">2 reguły Zapory (RDP IIS) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-448">FW Rule 2 (RDP IIS) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="d9bf7-449">PD zasady 3 (RDP DNS01) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-449">FW Rule 3 (RDP DNS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="d9bf7-450">Zastosować PD zasady 4 (RDP AppVM01), ruch jest dozwolony, zapory NAT go too10.0.2.5:3386 (portem RDP na AppVM01)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it too10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="d9bf7-451">podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-451">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="d9bf7-452">1 reguły NSG (Zablokuj Internet) nie ma zastosowania (ruch został NAT czy przez zaporę Windows hello, w związku z tym adresu źródłowego hello jest teraz hello zaporą, który znajduje się w podsieci zabezpieczeń hello i widoczne dla podsieci wewnętrznej bazy danych hello NSG toobe "lokalnie" ruchu, w związku z tym jest dozwolone), przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Backend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="d9bf7-453">Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG</span><span class="sxs-lookup"><span data-stu-id="d9bf7-453">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="d9bf7-454">AppVM01 nasłuchuje ruchu protokołu RDP i odpowiada</span><span class="sxs-lookup"><span data-stu-id="d9bf7-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="d9bf7-455">Z wychodzących reguł NSG Zastosuj reguły domyślne, a zwracany ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="d9bf7-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="d9bf7-456">PRZEZ kieruje ruch wychodzący toohello zapory jako hello następnego skoku</span><span class="sxs-lookup"><span data-stu-id="d9bf7-456">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
9. <span data-ttu-id="d9bf7-457">Ponieważ to zwraca ruchu na zapory hello ustanowienie sesji przekazuje hello odpowiedzi wstecz toohello internet użytkownika</span><span class="sxs-lookup"><span data-stu-id="d9bf7-457">Because this is returning traffic on an established session hello firewall passes hello response back toohello internet user</span></span>
10. <span data-ttu-id="d9bf7-458">Włączono sesji protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="d9bf7-458">RDP session is enabled</span></span>
11. <span data-ttu-id="d9bf7-459">AppVM01 wyświetli monit o hasło nazwy użytkownika</span><span class="sxs-lookup"><span data-stu-id="d9bf7-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="d9bf7-460">(Dozwolone) Wyszukiwania DNS serwera sieci Web na serwerze DNS</span><span class="sxs-lookup"><span data-stu-id="d9bf7-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="d9bf7-461">Serwer, IIS01, musi na www.data.gov strumieniowego źródła danych w sieci Web, ale wymaga tooresolve hello adres.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="d9bf7-462">Hello konfiguracji sieci dla listy sieci wirtualnej hello DNS01 (10.0.2.4 podsieci wewnętrznej bazy danych hello) jako podstawowy serwer DNS hello IIS01 wysyła tooDNS01 żądania DNS hello</span><span class="sxs-lookup"><span data-stu-id="d9bf7-462">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="d9bf7-463">PRZEZ kieruje ruch wychodzący toohello zapory jako hello następnego skoku</span><span class="sxs-lookup"><span data-stu-id="d9bf7-463">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
4. <span data-ttu-id="d9bf7-464">Brak wychodzących reguł NSG są powiązane toohello podsieci frontonu, ruch jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-464">No outbound NSG rules are bound toohello Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="d9bf7-465">Zapora rozpoczyna przetwarzanie reguł:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="d9bf7-466">PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-466">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="d9bf7-467">Nie można stosować reguły Zapory 2-5 (zasad protokołu RDP), przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="d9bf7-468">Nie można stosować PD zasady 6 i 7 (zasady aplikacji), przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-468">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="d9bf7-469">8 reguły Zapory (tooInternet) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-469">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="d9bf7-470">Zastosuj reguły Zapory 9 DNS (Domain Name System), ruch jest dozwolony, zapora przekazuje ruch too10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic too10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="d9bf7-471">podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-471">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="d9bf7-472">Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-472">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="d9bf7-473">Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG</span><span class="sxs-lookup"><span data-stu-id="d9bf7-473">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="d9bf7-474">Serwer DNS odbiera żądanie hello</span><span class="sxs-lookup"><span data-stu-id="d9bf7-474">DNS server receives hello request</span></span>
8. <span data-ttu-id="d9bf7-475">Serwer DNS nie ma adresu hello w pamięci podręcznej i prosi o główny serwer DNS na powitania internet</span><span class="sxs-lookup"><span data-stu-id="d9bf7-475">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
9. <span data-ttu-id="d9bf7-476">PRZEZ kieruje ruch wychodzący toohello zapory jako hello następnego skoku</span><span class="sxs-lookup"><span data-stu-id="d9bf7-476">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
10. <span data-ttu-id="d9bf7-477">Nie wychodzące reguły NSG podsieci wewnętrznej bazy danych, ruch jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="d9bf7-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="d9bf7-478">Zapora rozpoczyna przetwarzanie reguł:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="d9bf7-479">PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-479">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="d9bf7-480">Nie można stosować reguły Zapory 2-5 (zasad protokołu RDP), przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="d9bf7-481">Nie można stosować PD zasady 6 i 7 (zasady aplikacji), przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-481">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="d9bf7-482">Zastosuj 8 reguły Zapory (tooInternet), ruch jest dozwolony, sesja jest SNAT limit tooroot DNS serwera na powitania Internet</span><span class="sxs-lookup"><span data-stu-id="d9bf7-482">FW Rule 8 (tooInternet) does apply, traffic is allowed, session is SNAT out tooroot DNS server on hello Internet</span></span>
12. <span data-ttu-id="d9bf7-483">Serwer DNS w Internecie odpowiada, ponieważ w tej sesji zostało zainicjowane w zaporze hello, odpowiedź hello jest akceptowany przez zaporę Windows hello</span><span class="sxs-lookup"><span data-stu-id="d9bf7-483">Internet DNS server responds, since this session was initiated from hello firewall, hello response is accepted by hello firewall</span></span>
13. <span data-ttu-id="d9bf7-484">Jak jest to ustanowienie sesji, zapory hello przekazuje toohello odpowiedzi hello inicjowania serwera, DNS01</span><span class="sxs-lookup"><span data-stu-id="d9bf7-484">As this is an established session, hello firewall forwards hello response toohello initiating server, DNS01</span></span>
14. <span data-ttu-id="d9bf7-485">podsieci wewnętrznej bazy danych Hello rozpoczyna przetwarzanie przychodzącej reguły:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-485">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="d9bf7-486">Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-486">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="d9bf7-487">Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG</span><span class="sxs-lookup"><span data-stu-id="d9bf7-487">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="d9bf7-488">Hello serwer DNS odbiera i buforuje odpowiedź hello i następnie odpowiada tooIIS01 wstecz toohello żądania początkowego</span><span class="sxs-lookup"><span data-stu-id="d9bf7-488">hello DNS server receives and caches hello response, and then responds toohello initial request back tooIIS01</span></span>
16. <span data-ttu-id="d9bf7-489">trasy przez Hello podsieci wewnętrznej bazy danych powoduje, że hello zapory hello następnego skoku</span><span class="sxs-lookup"><span data-stu-id="d9bf7-489">hello UDR route on backend subnet makes hello firewall hello next hop</span></span>
17. <span data-ttu-id="d9bf7-490">Wychodzące NSG nie istnieją żadne reguły podsieci wewnętrznej bazy danych hello ruch jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-490">No outbound NSG rules exist on hello Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="d9bf7-491">Jest to ustanowienie sesji na zaporze hello, odpowiedź hello jest przesyłany dalej przez serwer IIS wstecz toohello zapory hello</span><span class="sxs-lookup"><span data-stu-id="d9bf7-491">This is an established session on hello firewall, hello response is forwarded by hello firewall back toohello IIS server</span></span>
19. <span data-ttu-id="d9bf7-492">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="d9bf7-493">Nie zasady grupy NSG, stosowanym tooInbound ruchu z podsieci frontonu hello wewnętrznej bazy danych podsieci toohello, więc żaden hello reguły NSG</span><span class="sxs-lookup"><span data-stu-id="d9bf7-493">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="d9bf7-494">Hello domyślna systemu reguła zezwala na ruch między podsieciami umożliwiałyby tego rodzaju ruch, ruch hello jest dozwolony</span><span class="sxs-lookup"><span data-stu-id="d9bf7-494">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
20. <span data-ttu-id="d9bf7-495">IIS01 odbiera odpowiedź hello z DNS01</span><span class="sxs-lookup"><span data-stu-id="d9bf7-495">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-backend-server-toofrontend-server"></a><span data-ttu-id="d9bf7-496">(Dozwolone) TooFrontend serwera wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="d9bf7-496">(Allowed) Backend server tooFrontend server</span></span>
1. <span data-ttu-id="d9bf7-497">Administrator zalogowany tooAppVM02 za pomocą protokołu RDP zażąda pliku bezpośrednio z serwerem IIS01 hello za pomocą Eksploratora plików systemu windows</span><span class="sxs-lookup"><span data-stu-id="d9bf7-497">An administrator logged on tooAppVM02 via RDP requests a file directly from hello IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="d9bf7-498">trasy przez Hello podsieci wewnętrznej bazy danych powoduje, że hello zapory hello następnego skoku</span><span class="sxs-lookup"><span data-stu-id="d9bf7-498">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
3. <span data-ttu-id="d9bf7-499">Ponieważ ma nie wychodzące reguły NSG na powitania odpowiedź hello podsieci wewnętrznej bazy danych jest dozwolone</span><span class="sxs-lookup"><span data-stu-id="d9bf7-499">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
4. <span data-ttu-id="d9bf7-500">Zapora rozpoczyna przetwarzanie reguł:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="d9bf7-501">PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-501">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="d9bf7-502">Nie można stosować reguły Zapory 2-5 (zasad protokołu RDP), przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="d9bf7-503">Nie można stosować PD zasady 6 i 7 (zasady aplikacji), przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-503">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="d9bf7-504">8 reguły Zapory (tooInternet) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-504">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="d9bf7-505">9 reguły Zapory (DNS, Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-505">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="d9bf7-506">Zastosuj 10 reguły Zapory (Intra-podsieć), ruch jest dozwolony, zapora przekazuje ruch too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic too10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="d9bf7-507">Podsieci frontonu rozpoczyna przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="d9bf7-508">Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-508">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="d9bf7-509">Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG</span><span class="sxs-lookup"><span data-stu-id="d9bf7-509">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="d9bf7-510">Zakładając, że odpowiednie uwierzytelniania i autoryzacji, IIS01 akceptuje Żądanie hello i odpowiada</span><span class="sxs-lookup"><span data-stu-id="d9bf7-510">Assuming proper authentication and authorization, IIS01 accepts hello request and responds</span></span>
7. <span data-ttu-id="d9bf7-511">Witaj przez trasy podsieci frontonu sprawia, że hello zapory hello następnego skoku</span><span class="sxs-lookup"><span data-stu-id="d9bf7-511">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
8. <span data-ttu-id="d9bf7-512">Ponieważ ma nie wychodzące reguły NSG na powitania odpowiedź hello podsieci frontonu jest dozwolona</span><span class="sxs-lookup"><span data-stu-id="d9bf7-512">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
9. <span data-ttu-id="d9bf7-513">Jak jest to istniejącej sesji na zaporze hello ta odpowiedź jest dozwolone i zapory hello zwraca hello tooAppVM02 odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d9bf7-513">As this is an existing session on hello firewall this response is allowed and hello firewall returns hello response tooAppVM02</span></span>
10. <span data-ttu-id="d9bf7-514">Podsieci wewnętrznej bazy danych rozpoczyna się przetwarzanie przychodzących reguł:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="d9bf7-515">Grupa NSG reguła 1 (Zablokuj Internet) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-515">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="d9bf7-516">Reguły NSG domyślne zezwolić na ruch toosubnet podsieci, ruch jest dozwolony, Zatrzymaj przetwarzanie reguł NSG</span><span class="sxs-lookup"><span data-stu-id="d9bf7-516">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="d9bf7-517">AppVM02 odbiera odpowiedź hello</span><span class="sxs-lookup"><span data-stu-id="d9bf7-517">AppVM02 receives hello response</span></span>

#### <a name="denied-internet-direct-tooweb-server"></a><span data-ttu-id="d9bf7-518">(Odmowa) Bezpośrednie tooWeb internetowego serwera</span><span class="sxs-lookup"><span data-stu-id="d9bf7-518">(Denied) Internet direct tooWeb Server</span></span>
1. <span data-ttu-id="d9bf7-519">Internet użytkownik spróbuje tooaccess powitania serwera sieci web, IIS01, za pośrednictwem hello FrontEnd001.CloudApp.Net usługi</span><span class="sxs-lookup"><span data-stu-id="d9bf7-519">Internet user tries tooaccess hello web server, IIS01, through hello FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="d9bf7-520">Ponieważ nie ma żadnych punktów końcowych otwarte dla ruchu HTTP, to nie będzie przekazywać hello usługi w chmurze i nie osiągnięcia powitania serwera</span><span class="sxs-lookup"><span data-stu-id="d9bf7-520">Since there are no endpoints open for HTTP traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="d9bf7-521">Jeśli punkty końcowe hello były otwarte jakiegoś powodu, hello NSG (Zablokuj Internet) w podsieci frontonu hello uniemożliwiają ten ruch</span><span class="sxs-lookup"><span data-stu-id="d9bf7-521">If hello endpoints were open for some reason, hello NSG (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="d9bf7-522">Na koniec trasy przez podsieci frontonu hello wyśle cały ruch wychodzący z zapory toohello IIS01 jako hello następnego przeskoku i zapory hello będzie traktować jako asymetrycznego ruchu i upuść odpowiedzi wychodzących hello związku z tym istnieją przynajmniej trzy warstwy niezależne sposobem ochrony między hello internet i IIS01 za pośrednictwem jego uniemożliwia nieautoryzowanym niewłaściwego dostępu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-522">Finally, hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toobackend-server"></a><span data-ttu-id="d9bf7-523">(Odmowa) Internet tooBackend serwera</span><span class="sxs-lookup"><span data-stu-id="d9bf7-523">(Denied) Internet tooBackend Server</span></span>
1. <span data-ttu-id="d9bf7-524">Internet użytkownik spróbuje tooaccess pliku AppVM01 za pośrednictwem hello BackEnd001.CloudApp.Net usługi</span><span class="sxs-lookup"><span data-stu-id="d9bf7-524">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="d9bf7-525">Ponieważ nie ma żadnych punktów końcowych otwarty do udziału plików, to nie przejdzie hello usługi w chmurze i nie osiągnięcia powitania serwera</span><span class="sxs-lookup"><span data-stu-id="d9bf7-525">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="d9bf7-526">Jeśli punkty końcowe hello były otwarte jakiegoś powodu, hello NSG (Zablokuj Internet) umożliwia zablokowanie tego ruchu</span><span class="sxs-lookup"><span data-stu-id="d9bf7-526">If hello endpoints were open for some reason, hello NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="d9bf7-527">Na koniec trasy przez hello wyśle cały ruch wychodzący z zapory toohello AppVM01 jako hello następnego przeskoku i zapory hello będzie traktować jako asymetrycznego ruchu i upuść odpowiedzi wychodzących hello związku z tym są co najmniej trzy warstwy niezależne obrony między Witaj internet i AppVM01 za pośrednictwem jego uniemożliwia nieautoryzowanym niewłaściwego dostępu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-527">Finally, hello UDR route would send any outbound traffic from AppVM01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-toobackend-server"></a><span data-ttu-id="d9bf7-528">(Odmowa) TooBackend serwera frontonu serwera</span><span class="sxs-lookup"><span data-stu-id="d9bf7-528">(Denied) Frontend server tooBackend Server</span></span>
1. <span data-ttu-id="d9bf7-529">Przykładowa IIS01 zostało naruszone i działa złośliwego kodu w trakcie serwerów podsieci wewnętrznej bazy danych hello tooscan.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-529">Assume IIS01 was compromised and is running malicious code trying tooscan hello Backend subnet servers.</span></span>
2. <span data-ttu-id="d9bf7-530">trasy przez podsieci frontonu Hello czy Wyślij cały ruch wychodzący z zapory toohello IIS01 jako hello następnego przeskoku.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-530">hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop.</span></span> <span data-ttu-id="d9bf7-531">Nie jest to coś, który może być modyfikowany przez hello naruszenia zabezpieczeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-531">This is not something that can be altered by hello compromised VM.</span></span>
3. <span data-ttu-id="d9bf7-532">zapory Hello może przetwarzać ruchu hello, jeśli Żądanie hello zostało tooAppVM01 lub toohello serwera DNS podczas wyszukiwania DNS, które potencjalnie być dozwolony ruch przez zaporę Windows hello (powodu tooFW zasady 7 i 9).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-532">hello firewall would process hello traffic, if hello request was tooAppVM01, or toohello DNS server for DNS lookups that traffic could potentially be allowed by hello firewall (due tooFW Rules 7 and 9).</span></span> <span data-ttu-id="d9bf7-533">Wszelki inny ruch zostałby zablokowany przez PD zasady 11 (Odmów wszystko).</span><span class="sxs-lookup"><span data-stu-id="d9bf7-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="d9bf7-534">Jeśli zaawansowane wykrywanie zagrożeń włączono zaporę hello (nieuwzględnionego w tym dokumencie, zobacz hello dokumentacji dostawcy dla urządzenia określoną sieć zaawansowane funkcje zagrożenia), nawet ruch będzie dozwolony przez hello podstawowe zasady przekazywania omówione w tym dokumencie można zapobiegać Jeśli ruch hello zawarte podpisów znanych lub wzorce, które Flaga regułę advanced threat.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-534">If advanced threat detection was enabled on hello firewall (which is not covered in this document, see hello vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by hello basic forwarding rules discussed in this document could be prevented if hello traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="d9bf7-535">(Odmowa) Wyszukiwania DNS w Internecie na serwerze DNS</span><span class="sxs-lookup"><span data-stu-id="d9bf7-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="d9bf7-536">Internet użytkownik spróbuje toolookup wewnętrzny rekord DNS na DNS01 za pośrednictwem usługi BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="d9bf7-536">Internet user tries toolookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="d9bf7-537">Ponieważ nie ma żadnych punktów końcowych otwarte dla ruchu DNS, to nie przejdzie za pośrednictwem hello usługi w chmurze i nie osiągnięcia powitania serwera</span><span class="sxs-lookup"><span data-stu-id="d9bf7-537">Since there are no endpoints open for DNS traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="d9bf7-538">Jeśli punkty końcowe hello były otwarte jakiegoś powodu, reguły NSG hello (Zablokuj Internet) w podsieci frontonu hello uniemożliwiają ten ruch</span><span class="sxs-lookup"><span data-stu-id="d9bf7-538">If hello endpoints were open for some reason, hello NSG rule (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="d9bf7-539">Na koniec tras przez podsieci wewnętrznej bazy danych hello wyśle cały ruch wychodzący z zapory toohello DNS01 jako hello następnego przeskoku i zapory hello będzie traktować jako asymetrycznego ruchu i upuść odpowiedzi wychodzących hello związku z tym istnieją przynajmniej trzy warstwy niezależne sposobem ochrony między hello internet i DNS01 za pośrednictwem jego uniemożliwia nieautoryzowanym niewłaściwego dostępu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-539">Finally, hello Backend subnet UDR route would send any outbound traffic from DNS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toosql-access-through-firewall"></a><span data-ttu-id="d9bf7-540">(Odmowa) Dostęp do tooSQL Internetu przez zaporę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-540">(Denied) Internet tooSQL access through Firewall</span></span>
1. <span data-ttu-id="d9bf7-541">Internet użytkownik żąda danych SQL z SecSvc001.CloudApp.Net (Internet ukierunkowane usługa w chmurze)</span><span class="sxs-lookup"><span data-stu-id="d9bf7-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="d9bf7-542">Ponieważ nie ma żadnych punktów końcowych otwarte dla bazy danych SQL, to nie przejdzie hello usługi w chmurze i nie osiągnąć hello zapory</span><span class="sxs-lookup"><span data-stu-id="d9bf7-542">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="d9bf7-543">Jeśli punkty końcowe SQL były otwarte jakiegoś powodu, zapory hello może rozpocząć przetwarzania zasad:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-543">If SQL endpoints were open for some reason, hello firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="d9bf7-544">PD reguła 1 (PD Mgmt) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-544">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="d9bf7-545">Reguły Zapory 2-5 (zasad protokołu RDP) nie zastosować, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="d9bf7-546">Nie można stosować PD zasady 6 i 7 (zasady aplikacji), przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-546">FW Rule 6 & 7 (Application Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="d9bf7-547">8 reguły Zapory (tooInternet) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-547">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="d9bf7-548">9 reguły Zapory (DNS, Domain Name System) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-548">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="d9bf7-549">10 reguły Zapory (Intra-podsieci) nie ma zastosowania, przenieść toonext regułę</span><span class="sxs-lookup"><span data-stu-id="d9bf7-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move toonext rule</span></span>
   7. <span data-ttu-id="d9bf7-550">Zastosować PD zasady 11 (Odmów wszystko), ruch jest przetwarzania zasad zablokowane, stop</span><span class="sxs-lookup"><span data-stu-id="d9bf7-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="d9bf7-551">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="d9bf7-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="d9bf7-552">Skrypt głównego i konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="d9bf7-552">Main Script and Network Config</span></span>
<span data-ttu-id="d9bf7-553">Zapisz hello pełne skryptu w pliku skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-553">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="d9bf7-554">Zapisz hello konfigurację sieci w pliku o nazwie "NetworkConf2.xml".</span><span class="sxs-lookup"><span data-stu-id="d9bf7-554">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="d9bf7-555">Modyfikuj zmienne zdefiniowane przez użytkownika hello, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-555">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="d9bf7-556">Uruchom skrypt hello, a następnie postępuj zgodnie z powyższych instrukcji instalacji reguły zapory hello.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-556">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="d9bf7-557">Pełna skryptu</span><span class="sxs-lookup"><span data-stu-id="d9bf7-557">Full Script</span></span>
<span data-ttu-id="d9bf7-558">Ten skrypt zostanie, na podstawie hello zmiennych zdefiniowanych przez użytkownika:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-558">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="d9bf7-559">Połącz tooan subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d9bf7-559">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="d9bf7-560">Utwórz nowe konto magazynu</span><span class="sxs-lookup"><span data-stu-id="d9bf7-560">Create a new storage account</span></span>
3. <span data-ttu-id="d9bf7-561">Utwórz nową sieć wirtualną i trzy podsieci zgodnie z definicją w pliku konfiguracji sieci hello</span><span class="sxs-lookup"><span data-stu-id="d9bf7-561">Create a new VNet and three subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="d9bf7-562">Tworzenie maszyn wirtualnych pięć; zapory 1 i 4 systemu windows server maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="d9bf7-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="d9bf7-563">Skonfiguruj przez w tym:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="d9bf7-564">Utworzenie dwóch nowych tabel tras</span><span class="sxs-lookup"><span data-stu-id="d9bf7-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="d9bf7-565">Dodawanie tras toohello tabel</span><span class="sxs-lookup"><span data-stu-id="d9bf7-565">Add routes toohello tables</span></span>
   3. <span data-ttu-id="d9bf7-566">Powiąż podsieci tooappropriate tabel</span><span class="sxs-lookup"><span data-stu-id="d9bf7-566">Bind tables tooappropriate subnets</span></span>
6. <span data-ttu-id="d9bf7-567">Włączanie funkcji przesyłania dalej IP na powitania NVA</span><span class="sxs-lookup"><span data-stu-id="d9bf7-567">Enable IP Forwarding on hello NVA</span></span>
7. <span data-ttu-id="d9bf7-568">Skonfiguruj grupy NSG w tym:</span><span class="sxs-lookup"><span data-stu-id="d9bf7-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="d9bf7-569">Tworzenie grupy NSG</span><span class="sxs-lookup"><span data-stu-id="d9bf7-569">Creating a NSG</span></span>
   2. <span data-ttu-id="d9bf7-570">Dodanie reguły</span><span class="sxs-lookup"><span data-stu-id="d9bf7-570">Adding a rule</span></span>
   3. <span data-ttu-id="d9bf7-571">Powiązanie hello NSG toohello odpowiednie podsieci</span><span class="sxs-lookup"><span data-stu-id="d9bf7-571">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="d9bf7-572">Ten skrypt programu PowerShell powinien zostać uruchomiony lokalnie na się, że połączenie internetowe, komputera lub serwera.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9bf7-573">Uruchomienie tego skryptu można ostrzeżenia lub inne komunikaty informacyjne, które pop w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="d9bf7-574">Tylko komunikaty o błędach na czerwono są przyczyną problemu.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-574">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

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
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

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

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

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
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
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
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
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


#### <a name="network-config-file"></a><span data-ttu-id="d9bf7-575">Plik konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="d9bf7-575">Network Config File</span></span>
<span data-ttu-id="d9bf7-576">Zapisz ten plik xml z lokalizacji zaktualizowane i Dodaj hello łącze toothis pliku toohello $NetworkConfigFile zmiennej w skrypcie hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="d9bf7-576">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
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

#### <a name="sample-application-scripts"></a><span data-ttu-id="d9bf7-577">Przykładowe skrypty aplikacji</span><span class="sxs-lookup"><span data-stu-id="d9bf7-577">Sample Application Scripts</span></span>
<span data-ttu-id="d9bf7-578">Jeśli chcesz tooinstall Przykładowa aplikacja dla tego i innych przykłady DMZ, jeden podano na powitania następującego łącza: [przykładowy skrypt aplikacji][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="d9bf7-578">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Dwukierunkowe DMZ NVA, NSG i przez"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Widok logiczny hello reguły zapory"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Utwórz obiekt sieci frontonu"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Utwórz obiekt serwera DNS"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Kopiowanie reguły domyślnej protokołu RDP"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Reguła AppVM01"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Ikona przekierowania aplikacji"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Ikona NAT docelowego"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Ikona — dostęp próbny"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Reguły zapory zarządzania"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Reguły zapory protokołu RDP"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Reguła zapory w sieci Web"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Reguły zapory AppVM01"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Reguła ruchu wychodzącego"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Reguły zapory DNS"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Reguła sieci wirtualnej wewnątrz zapory"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Zapora regułę Odmów"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Aktywacja reguły zapory"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
