---
title: "aaaConnect i komunikować się z usługami w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak połączyć tooresolve i komunikować się z usługami w sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="8e4c4-103">Połącz i łączyć się z usługami w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="8e4c4-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="8e4c4-104">W sieci szkieletowej usług Usługa gdzieś działa w klastrze usługi sieć szkieletowa, zazwyczaj są rozproszone na wielu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="8e4c4-105">Można ją przenosić z tooanother w jednym miejscu przez właściciela usługi hello lub automatycznie przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-105">It can be moved from one place tooanother, either by hello service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="8e4c4-106">Usługi nie są statycznie wiązanej tooa określonego komputera lub adres.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-106">Services are not statically tied tooa particular machine or address.</span></span>

<span data-ttu-id="8e4c4-107">Aplikacji usługi Service Fabric zazwyczaj składa się z wielu różnych usług, w którym każda usługa wykonuje zadanie specjalne.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="8e4c4-108">Tych usług może komunikować się z sobą tooform w pełną funkcji, takich jak renderowania różne części aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-108">These services may communicate with each other tooform a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="8e4c4-109">Dostępne są także klienta, które aplikacje łączące tooand łączyć się z usługami.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-109">There are also client applications that connect tooand communicate with services.</span></span> <span data-ttu-id="8e4c4-110">W tym dokumencie omówiono sposób tooset się komunikacji z i od usługi w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-110">This document discusses how tooset up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="8e4c4-111">Ten film Microsoft Virtual Academy omówiono także komunikacji usługi:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="8e4c4-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="8e4c4-112">Przełącz własnego protokołu</span><span class="sxs-lookup"><span data-stu-id="8e4c4-112">Bring your own protocol</span></span>
<span data-ttu-id="8e4c4-113">Sieć szkieletowa usług ułatwia zarządzanie cyklem życia hello usług, ale nie powoduje decyzje na temat działania usługi.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-113">Service Fabric helps manage hello lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="8e4c4-114">W tym komunikacji.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-114">This includes communication.</span></span> <span data-ttu-id="8e4c4-115">Po otwarciu usługi przez usługi Service Fabric, będący tooset możliwości usługi się punkt końcowy dla przychodzących żądań przy użyciu dowolnego stosu protokołu lub komunikacji ma.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-115">When your service is opened by Service Fabric, that's your service's opportunity tooset up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="8e4c4-116">Usługa będzie nasłuchiwać zwykłym **IP:port** adresów przy użyciu dowolnego schematu adresowania, takich jak identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="8e4c4-117">Wiele wystąpień usługi lub replik może udostępniać procesu hosta, w którym to przypadku one będzie konieczne toouse różnych portów albo użyj mechanizm współużytkowania portów, takie jak sterownik jądra hello http.sys w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-117">Multiple service instances or replicas may share a host process, in which case they will either need toouse different ports or use a port-sharing mechanism, such as hello http.sys kernel driver in Windows.</span></span> <span data-ttu-id="8e4c4-118">W obu przypadkach musi być unikatowo adresowane każdego wystąpienia usługi lub repliki w ramach procesu hosta.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![Punkty końcowe usługi][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="8e4c4-120">Odnajdowanie usługi i rozwiązania</span><span class="sxs-lookup"><span data-stu-id="8e4c4-120">Service discovery and resolution</span></span>
<span data-ttu-id="8e4c4-121">W rozproszonym systemie usługi mogą być przenoszone ze tooanother na jednym komputerze wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-121">In a distributed system, services may move from one machine tooanother over time.</span></span> <span data-ttu-id="8e4c4-122">Może to nastąpić z różnych powodów, takich jak zasób równoważenia uaktualnień, pracy w trybie Failover lub skalowalnych w poziomie. Oznacza to, że adresy punktów końcowych usługi zmienić usługi hello przenosi toonodes z różnymi adresami IP, a może otwierać na różnych portów, jeśli usługa hello używa dynamicznie wybranego portu.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out. This means service endpoint addresses change as hello service moves toonodes with different IP addresses, and may open on different ports if hello service uses a dynamically selected port.</span></span>

![Dystrybucja usług programu][7]

<span data-ttu-id="8e4c4-124">Sieć szkieletowa usług zapewnia możliwość odnajdywania i rozpoznawania usługi o nazwie hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-124">Service Fabric provides a discovery and resolution service called hello Naming Service.</span></span> <span data-ttu-id="8e4c4-125">Witaj Naming Service obsługuje wystąpień usługi o nazwie tabeli, która mapuje adresy punktów końcowych toohello, które one nasłuchiwać.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-125">hello Naming Service maintains a table that maps named service instances toohello endpoint addresses they listen on.</span></span> <span data-ttu-id="8e4c4-126">Wszystkie wystąpienia usługi o nazwie w sieci szkieletowej usług mają unikatowe nazwy, reprezentowane jako identyfikatory URI, na przykład `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-126">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="8e4c4-127">nie zmienia nazwę Hello hello usługi okresu istnienia hello hello usługi, jest tylko adresy punktów końcowych hello, które można zmienić podczas przenoszenia usług.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-127">hello name of hello service does not change over hello lifetime of hello service, it's only hello endpoint addresses that can change when services move.</span></span> <span data-ttu-id="8e4c4-128">To jest analogiczne toowebsites, gdy mają stałe adresy URL, ale gdzie adresu IP hello mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-128">This is analogous toowebsites that have constant URLs but where hello IP address may change.</span></span> <span data-ttu-id="8e4c4-129">I podobne tooDNS hello sieci Web, która rozwiązuje adresy tooIP adresów URL witryny sieci Web, usługi Service Fabric ma Rejestrator mapująca adres punktu końcowego tootheir nazwy usługi.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-129">And similar tooDNS on hello web, which resolves website URLs tooIP addresses, Service Fabric has a registrar that maps service names tootheir endpoint address.</span></span>

![Punkty końcowe usługi][2]

<span data-ttu-id="8e4c4-131">Rozpoznawanie i łączenie tooservices obejmuje następujące kroki, uruchom w pętli hello:</span><span class="sxs-lookup"><span data-stu-id="8e4c4-131">Resolving and connecting tooservices involves hello following steps run in a loop:</span></span>

* <span data-ttu-id="8e4c4-132">**Rozwiąż**: hello punktu końcowego Get, który opublikował usługę z hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-132">**Resolve**: Get hello endpoint that a service has published from hello Naming Service.</span></span>
* <span data-ttu-id="8e4c4-133">**Połącz**: Podłączanie usługi toohello niezależnie od protokołu używa w tym punkcie końcowym.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-133">**Connect**: Connect toohello service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="8e4c4-134">**Spróbuj ponownie**: próba połączenia może zakończyć się niepowodzeniem dla dowolnej liczby przyczyn, na przykład jeśli hello usługi została przeniesiona, ponieważ adres punktu końcowego hello ostatni czas hello został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-134">**Retry**: A connection attempt may fail for any number of reasons, for example if hello service has moved since hello last time hello endpoint address was resolved.</span></span> <span data-ttu-id="8e4c4-135">W takim przypadku hello poprzedzających rozwiązanie i połączyć kroki należy toobe ponowione, a ten cykl powtarza się do chwili pomyślnego połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-135">In that case, hello preceding resolve and connect steps need toobe retried, and this cycle is repeated until hello connection succeeds.</span></span>

## <a name="connecting-tooother-services"></a><span data-ttu-id="8e4c4-136">Połączenie usług tooother</span><span class="sxs-lookup"><span data-stu-id="8e4c4-136">Connecting tooother services</span></span>
<span data-ttu-id="8e4c4-137">Łączenie tooeach usług innych wewnątrz klastra zazwyczaj bezpośrednio uzyskać dostęp punkty końcowe hello innych usług ponieważ hello węzłów w klastrze na powitania tej samej sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-137">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="8e4c4-138">toomake jest łatwiejsze tooconnect między usługami, Service Fabric zawiera dodatkowe usługi, które używają hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-138">toomake is easier tooconnect between services, Service Fabric provides additional services that use hello Naming Service.</span></span> <span data-ttu-id="8e4c4-139">Usługa DNS i usługa zwrotnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-139">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="8e4c4-140">Usługa DNS</span><span class="sxs-lookup"><span data-stu-id="8e4c4-140">DNS service</span></span>
<span data-ttu-id="8e4c4-141">Ponieważ wiele usług, zwłaszcza konteneryzowanych usług, może mieć nazwę istniejącego adresu URL, jest w stanie tooresolve je przy użyciu hello standardowy protokół DNS (a nie protokołu Naming Service hello) bardzo wygodny, szczególnie w aplikacji "przyrostu i" scenariusze.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-141">Since many services, especially containerized services, can have an existing URL name, being able tooresolve these using hello standard DNS protocol (rather than hello Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="8e4c4-142">Jest to tak, jakie hello usługa DNS ma.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-142">This is exactly what hello DNS service does.</span></span> <span data-ttu-id="8e4c4-143">Umożliwia możesz toomap nazwy tooa usługi nazwy DNS, a więc rozpoznać adresów IP punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-143">It enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="8e4c4-144">Jako hello przedstawiono na poniższym diagramie, hello usługa DNS, jest uruchomiona w klastrze usługi sieć szkieletowa hello, mapuje nazwy tooservice nazwy DNS, które następnie są rozpoznawane przez hello Naming Service tooreturn hello punktu końcowego adresy tooconnect do.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-144">As shown in hello following diagram, hello DNS service, running in hello Service Fabric cluster, maps DNS names tooservice names which are then resolved by hello Naming Service tooreturn hello endpoint addresses tooconnect to.</span></span> <span data-ttu-id="8e4c4-145">nazwy DNS Hello hello usługi znajduje się na powitania godzina utworzenia.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-145">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![Punkty końcowe usługi][9]

<span data-ttu-id="8e4c4-147">Więcej informacji dotyczących sposobu hello toouse usługi DNS, zobacz [usługa DNS w sieci szkieletowej usług Azure](service-fabric-dnsservice.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-147">For more details on how toouse hello DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="8e4c4-148">Zwrotny serwer proxy usługi</span><span class="sxs-lookup"><span data-stu-id="8e4c4-148">Reverse proxy service</span></span>
<span data-ttu-id="8e4c4-149">Hello zwrotnego serwera proxy dotyczy usługi w klastrze hello, który ujawnia punktów końcowych HTTP, HTTPS w tym.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-149">hello reverse proxy addresses services in hello cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="8e4c4-150">Hello zwrotnego serwera proxy jest znacznie ułatwione wywołaniem innych usług i formatu identyfikatora URI ich metod przez określony i połączenia uchwytów hello rozwiązać, ponów próbę wykonania kroków wymaganych do toocommunicate jedną usługę przy użyciu innego hello nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-150">hello reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles hello resolve, connect, retry steps required for one service toocommunicate with another using hello Naming Serivce.</span></span> <span data-ttu-id="8e4c4-151">Innymi słowy ukrywa on hello usługi nazw użytkownika podczas wywoływania metody innych usług, dokonując to prosty jak wywołanie adresu URL.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-151">In other words, it hides hello Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![Punkty końcowe usługi][10]

<span data-ttu-id="8e4c4-153">Więcej informacji na temat jak toouse hello wstecznego usługi serwera proxy można znaleźć [odwrotny serwer proxy w sieci szkieletowej usług Azure](service-fabric-reverseproxy.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-153">For more details on how toouse hello reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="8e4c4-154">Połączenia z klientami zewnętrznymi</span><span class="sxs-lookup"><span data-stu-id="8e4c4-154">Connections from external clients</span></span>
<span data-ttu-id="8e4c4-155">Łączenie tooeach usług innych wewnątrz klastra zazwyczaj bezpośrednio uzyskać dostęp punkty końcowe hello innych usług ponieważ hello węzłów w klastrze na powitania tej samej sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-155">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="8e4c4-156">W przypadku środowisk jednak klastra może być za modułem równoważenia obciążenia, który przekierowuje ruch przychodzący zewnętrznych za pomocą ograniczonego zestawu portów.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-156">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="8e4c4-157">W takich przypadkach usługi nadal może komunikować się ze sobą i rozwiązać przy użyciu adresów hello Naming Service, ale dodatkowych czynności musi być podjęte tooallow klientów zewnętrznych tooconnect tooservices.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-157">In these cases, services can still communicate with each other and resolve addresses using hello Naming Service, but extra steps must be taken tooallow external clients tooconnect tooservices.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="8e4c4-158">Sieć szkieletowa usług na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="8e4c4-158">Service Fabric in Azure</span></span>
<span data-ttu-id="8e4c4-159">Klastra sieci szkieletowej usług w usłudze Azure znajduje się za usługą równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-159">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="8e4c4-160">Wszystkie ruch zewnętrzny toohello klaster musi przejść przez hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-160">All external traffic toohello cluster must pass through hello load balancer.</span></span> <span data-ttu-id="8e4c4-161">Witaj modułu równoważenia obciążenia będzie automatycznie przesyłał dalej ruch ruchu przychodzącego na losowe tooa danego portu *węzła* mający hello otworzyć tego samego portu.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-161">hello load balancer will automatically forward traffic inbound on a given port tooa random *node* that has hello same port open.</span></span> <span data-ttu-id="8e4c4-162">Hello modułu równoważenia obciążenia Azure tylko zna porty otwarty na powitania *węzłów*, nie może określić dotyczących otwarte porty przez osobę *usług*.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-162">hello Azure Load Balancer only knows about ports open on hello *nodes*, it does not know about ports open by individual *services*.</span></span>

![Azure topologii równoważenia obciążenia i sieci szkieletowej usług][3]

<span data-ttu-id="8e4c4-164">Na przykład w kolejności tooaccept zewnętrznych ruch na porcie **80**, musi być skonfigurowany hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8e4c4-164">For example, in order tooaccept external traffic on port **80**, hello following things must be configured:</span></span>

1. <span data-ttu-id="8e4c4-165">Zapisu to usługa, która nasłuchuje na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-165">Write a service that listens on port 80.</span></span> <span data-ttu-id="8e4c4-166">Skonfiguruj port 80 w pliku ServiceManifest.xml hello usługi i otwórz odbiornik usługi hello, na przykład serwer sieci web hostowania samoobsługowego.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-166">Configure port 80 in hello service's ServiceManifest.xml and open a listener in hello service, for example, a self-hosted web server.</span></span>

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. <span data-ttu-id="8e4c4-167">Tworzenie klastra sieci szkieletowej usług na platformie Azure i określić port **80** jako port punktu końcowego niestandardowych hello typu węzła, który będzie hostem usługi hello.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-167">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for hello node type that will host hello service.</span></span> <span data-ttu-id="8e4c4-168">Jeśli masz więcej niż jeden typ węzła, można skonfigurować *ograniczenia umieszczania* na powitania usługi tooensure uruchomieniu na typ węzła hello otworzyć port punktu końcowego niestandardowych hello.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-168">If you have more than one node type, you can set up a *placement constraint* on hello service tooensure it only runs on hello node type that has hello custom endpoint port opened.</span></span>

    ![Otwarcie portu dla typu węzła][4]
3. <span data-ttu-id="8e4c4-170">Po utworzeniu klastra hello, skonfiguruj hello Azure usługi równoważenia obciążenia w hello klastra grupy zasobów tooforward ruch na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-170">Once hello cluster has been created, configure hello Azure Load Balancer in hello cluster's Resource Group tooforward traffic on port 80.</span></span> <span data-ttu-id="8e4c4-171">Podczas tworzenia klastra za pośrednictwem portalu Azure hello, to jest automatycznie utworzyć dla każdego portu niestandardowego punktu końcowego, który został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-171">When creating a cluster through hello Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Ruch do przodu w hello modułu równoważenia obciążenia Azure][5]
4. <span data-ttu-id="8e4c4-173">Witaj używa modułu równoważenia obciążenia Azure czy toodetermine sondowania lub nie toosend ruchu tooa określonego węzła.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-173">hello Azure Load Balancer uses a probe toodetermine whether or not toosend traffic tooa particular node.</span></span> <span data-ttu-id="8e4c4-174">Hello sondowania okresowo sprawdza punkt końcowy każdego toodetermine węzła czy odpowiada hello węzła.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-174">hello probe periodically checks an endpoint on each node toodetermine whether or not hello node is responding.</span></span> <span data-ttu-id="8e4c4-175">W przypadku niepowodzenia tooreceive odpowiedzi po skonfigurowaną liczbę razy sondowania hello modułu równoważenia obciążenia hello zatrzymuje wysyłania ruchu toothat węzła.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-175">If hello probe fails tooreceive a response after a configured number of times, hello load balancer stops sending traffic toothat node.</span></span> <span data-ttu-id="8e4c4-176">Podczas tworzenia klastra za pośrednictwem portalu Azure hello, badanie automatycznie jest konfigurowane dla poszczególnych portów niestandardowych punktu końcowego, który został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-176">When creating a cluster through hello Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Ruch do przodu w hello modułu równoważenia obciążenia Azure][8]

<span data-ttu-id="8e4c4-178">Jest ważne tooremember, który hello modułu równoważenia obciążenia Azure i badania hello tylko wiedzieć o hello *węzłów*, nie hello *usług* uruchomione w węzłach hello.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-178">It's important tooremember that hello Azure Load Balancer and hello probe only know about hello *nodes*, not hello *services* running on hello nodes.</span></span> <span data-ttu-id="8e4c4-179">Hello modułu równoważenia obciążenia Azure będą zawsze wysyłały toonodes ruchu, który odpowiada toohello sondowania, więc należy uważać tooensure usługi są dostępne w hello węzłów, które są stanie toorespond toohello sondowania.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-179">hello Azure Load Balancer will always send traffic toonodes that respond toohello probe, so care must be taken tooensure services are available on hello nodes that are able toorespond toohello probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="8e4c4-180">Niezawodnej usługi: Opcje komunikacji wbudowanej interfejsu API</span><span class="sxs-lookup"><span data-stu-id="8e4c4-180">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="8e4c4-181">framework niezawodne usługi Hello jest dostarczany z kilku opcji wbudowanych komunikacji.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-181">hello Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="8e4c4-182">Hello decyzja o tym, które jedną będzie najlepsza zależy od hello wybór hello modelu, hello communication framework i hello programowania usług są napisane w języku programowania.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-182">hello decision about which one will work best for you depends on hello choice of hello programming model, hello communication framework, and hello programming language that your services are written in.</span></span>

* <span data-ttu-id="8e4c4-183">**Nie określonego protokołu:** Jeśli nie ma określonego wybór framework komunikacji, ale ma tooget coś do pracy szybko, a następnie jest doskonałym rozwiązaniem hello automatycznie [service remoting](service-fabric-reliable-services-communication-remoting.md), dzięki czemu Wywołanie procedury zdalnej jednoznacznie dla Reliable Services i Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-183">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want tooget something up and running quickly, then hello ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="8e4c4-184">Jest to najprostszy hello i najszybszy sposób tooget wprowadzenie do komunikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-184">This is hello easiest and fastest way tooget started with service communication.</span></span> <span data-ttu-id="8e4c4-185">Service remoting obsługuje rozpoznawanie adresy usługi, połączenia, ponów próbę i obsługa błędów.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-185">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="8e4c4-186">To jest dostępna dla C# i aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-186">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="8e4c4-187">**HTTP**: komunikat niezależny od języka HTTP zapewnia wybór standardowych z narzędziami i serwery HTTP dostępne w wielu językach obsługiwanych przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-187">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="8e4c4-188">Usługi mogą używać żadnych HTTP stosu, w tym [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) dla aplikacji C#.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-188">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="8e4c4-189">Klienci napisane w języku C# można wykorzystać hello `ICommunicationClient` i `ServicePartitionClient` klas, natomiast dla języka Java, użyj hello `CommunicationClient` i `FabricServicePartitionClient` klas, [usługi rozdzielczości, połączeń HTTP i ponów próbę wykonania pętli](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="8e4c4-189">Clients written in C# can leverage hello `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use hello `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="8e4c4-190">**Usługi WCF**: Jeśli istniejący kod, który używa WCF jako platforma sieci komunikacji, a następnie użyć hello `WcfCommunicationListener` powitania po stronie serwera i `WcfCommunicationClient` i `ServicePartitionClient` klasy powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-190">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use hello `WcfCommunicationListener` for hello server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for hello client.</span></span> <span data-ttu-id="8e4c4-191">To jednak jest dostępna tylko dla aplikacji C# w klastrach z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-191">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="8e4c4-192">Aby uzyskać więcej informacji, zobacz ten artykuł [WCF na podstawie wykonania stosu komunikacji hello](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="8e4c4-192">For more details, see this article about [WCF-based implementation of hello communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="8e4c4-193">Przy użyciu protokołów niestandardowych i innych platform komunikacji</span><span class="sxs-lookup"><span data-stu-id="8e4c4-193">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="8e4c4-194">Usługi można użyć protokołu lub framework do komunikacji, czy jest protokołem binarne niestandardowych za pośrednictwem gniazda TCP lub za pośrednictwem przesyłania strumieniowego zdarzenia [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) lub [Centrum IoT Azure](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="8e4c4-194">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="8e4c4-195">Sieć szkieletowa usług zawiera komunikacji interfejsów API stosu komunikacji, można podłączyć wszystkie hello pracy toodiscover i połączyć jest pobieranej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-195">Service Fabric provides communication APIs that you can plug your communication stack into, while all hello work toodiscover and connect is abstracted from you.</span></span> <span data-ttu-id="8e4c4-196">Znajduje się w artykule o hello [model komunikacji niezawodnej usługi](service-fabric-reliable-services-communication.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="8e4c4-196">See this article about hello [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e4c4-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8e4c4-197">Next steps</span></span>
<span data-ttu-id="8e4c4-198">Dowiedz się więcej o hello pojęcia i interfejsami API dostępnymi w hello [model komunikacji niezawodnej usługi](service-fabric-reliable-services-communication.md), następnie szybko rozpocząć pracę z [service remoting](service-fabric-reliable-services-communication-remoting.md) lub jak przejść szczegółowe toolearn toowrite odbiornik komunikacji przy użyciu [interfejsu API sieci Web z hosta samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="8e4c4-198">Learn more about hello concepts and APIs available in hello [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth toolearn how toowrite a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
