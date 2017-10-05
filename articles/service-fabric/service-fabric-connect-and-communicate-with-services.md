---
title: "Połącz i łączyć się z usługami w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązać, łączenie i łączyć się z usługami w sieci szkieletowej usług."
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
ms.openlocfilehash: 3e61ad19df34c6a57da43e26bd2ab9d7ecdbf98e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="3d6ec-103">Połącz i łączyć się z usługami w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="3d6ec-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="3d6ec-104">W sieci szkieletowej usług Usługa gdzieś działa w klastrze usługi sieć szkieletowa, zazwyczaj są rozproszone na wielu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="3d6ec-105">Można można przenosić z jednego miejsca do innego, przez właściciela usługi lub automatycznie przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-105">It can be moved from one place to another, either by the service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="3d6ec-106">Usługi nie są statycznie związane z określonego komputera lub adres.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-106">Services are not statically tied to a particular machine or address.</span></span>

<span data-ttu-id="3d6ec-107">Aplikacji usługi Service Fabric zazwyczaj składa się z wielu różnych usług, w którym każda usługa wykonuje zadanie specjalne.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="3d6ec-108">Te usługi może komunikować się ze sobą do utworzenia pełnej funkcji, takich jak renderowania różne części aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-108">These services may communicate with each other to form a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="3d6ec-109">Dostępne są także aplikacji klienckich, które nawiązać połączenie i łączyć się z usługami.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-109">There are also client applications that connect to and communicate with services.</span></span> <span data-ttu-id="3d6ec-110">Tego dokumentu zawiera omówienie sposobu konfigurowania komunikacji z i od usługi w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-110">This document discusses how to set up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="3d6ec-111">Ten film Microsoft Virtual Academy omówiono także komunikacji usługi:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="3d6ec-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="3d6ec-112">Przełącz własnego protokołu</span><span class="sxs-lookup"><span data-stu-id="3d6ec-112">Bring your own protocol</span></span>
<span data-ttu-id="3d6ec-113">Sieć szkieletowa usług ułatwia zarządzanie cyklem życia usługi, ale nie powoduje decyzje na temat działania usługi.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-113">Service Fabric helps manage the lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="3d6ec-114">W tym komunikacji.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-114">This includes communication.</span></span> <span data-ttu-id="3d6ec-115">Po otwarciu usługi przez sieć szkieletowa usług, który jest możliwość usługi konfigurowania punktu końcowego dla przychodzących żądań przy użyciu dowolnego stosu protokołu lub komunikacji ma.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-115">When your service is opened by Service Fabric, that's your service's opportunity to set up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="3d6ec-116">Usługa będzie nasłuchiwać zwykłym **IP:port** adresów przy użyciu dowolnego schematu adresowania, takich jak identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="3d6ec-117">Wiele wystąpień usługi lub replik może udostępniać procesu hosta, w którym to przypadku albo muszą używać różnych portów lub mechanizm współużytkowania portów, takie jak sterownik http.sys jądra systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-117">Multiple service instances or replicas may share a host process, in which case they will either need to use different ports or use a port-sharing mechanism, such as the http.sys kernel driver in Windows.</span></span> <span data-ttu-id="3d6ec-118">W obu przypadkach musi być unikatowo adresowane każdego wystąpienia usługi lub repliki w ramach procesu hosta.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![Punkty końcowe usługi][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="3d6ec-120">Odnajdowanie usługi i rozwiązania</span><span class="sxs-lookup"><span data-stu-id="3d6ec-120">Service discovery and resolution</span></span>
<span data-ttu-id="3d6ec-121">W rozproszonym systemie usługi może przenieść z jednego komputera na inny wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-121">In a distributed system, services may move from one machine to another over time.</span></span> <span data-ttu-id="3d6ec-122">Może to nastąpić z różnych powodów, takich jak zasób równoważenia uaktualnień, pracy w trybie Failover lub skalowalnych w poziomie.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out.</span></span> <span data-ttu-id="3d6ec-123">Oznacza to, że adresy punktów końcowych usługi zmienić, ponieważ usługa przenosi do węzłów z różnych adresów IP i może otwierać na różnych portów, jeśli usługa używa portu dynamicznego wybrane.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-123">This means service endpoint addresses change as the service moves to nodes with different IP addresses, and may open on different ports if the service uses a dynamically selected port.</span></span>

![Dystrybucja usług programu][7]

<span data-ttu-id="3d6ec-125">Sieć szkieletowa usług udostępnia usługę odnajdywania i rozwiązania o nazwie Naming Service.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-125">Service Fabric provides a discovery and resolution service called the Naming Service.</span></span> <span data-ttu-id="3d6ec-126">Naming Service obsługuje tabelę, która mapuje nazwanych wystąpień usług adresy punktów końcowych, do których one nasłuchiwania.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-126">The Naming Service maintains a table that maps named service instances to the endpoint addresses they listen on.</span></span> <span data-ttu-id="3d6ec-127">Wszystkie wystąpienia usługi o nazwie w sieci szkieletowej usług mają unikatowe nazwy, reprezentowane jako identyfikatory URI, na przykład `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-127">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="3d6ec-128">Nazwa usługi nie zmienia się w okresie istnienia usługi, jest tylko adresy punktów końcowych, które można zmienić podczas przenoszenia usług.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-128">The name of the service does not change over the lifetime of the service, it's only the endpoint addresses that can change when services move.</span></span> <span data-ttu-id="3d6ec-129">To jest analogiczne do witryn sieci Web, gdy mają stałe adresy URL, ale gdzie adresu IP mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-129">This is analogous to websites that have constant URLs but where the IP address may change.</span></span> <span data-ttu-id="3d6ec-130">I podobne w systemie DNS w sieci web, który jest rozpoznawany jako adresy URL witryny sieci Web adresy IP, usługi Service Fabric ma rejestratora, która mapuje nazwy usługi na swój adres punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-130">And similar to DNS on the web, which resolves website URLs to IP addresses, Service Fabric has a registrar that maps service names to their endpoint address.</span></span>

![Punkty końcowe usługi][2]

<span data-ttu-id="3d6ec-132">Rozpoznawanie i łączących się z usługami obejmuje następujące kroki uruchamiania w pętli:</span><span class="sxs-lookup"><span data-stu-id="3d6ec-132">Resolving and connecting to services involves the following steps run in a loop:</span></span>

* <span data-ttu-id="3d6ec-133">**Rozwiąż**: uzyskanie punktu końcowego, który został opublikowany usługą Naming Service.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-133">**Resolve**: Get the endpoint that a service has published from the Naming Service.</span></span>
* <span data-ttu-id="3d6ec-134">**Połącz**: połączyć się z usługą za pośrednictwem niezależnie od protokołu używa w tym punkcie końcowym.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-134">**Connect**: Connect to the service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="3d6ec-135">**Spróbuj ponownie**: próba połączenia może zakończyć się niepowodzeniem dla dowolnej liczby przyczyn, na przykład jeśli usługi zostały przeniesione od czasu ostatniego adres punktu końcowego został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-135">**Retry**: A connection attempt may fail for any number of reasons, for example if the service has moved since the last time the endpoint address was resolved.</span></span> <span data-ttu-id="3d6ec-136">W takim przypadku poprzedni rozwiązania i połączyć kroki potrzebę ponowione, a ten cykl powtarza się do chwili pomyślnego połączenia.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-136">In that case, the preceding resolve and connect steps need to be retried, and this cycle is repeated until the connection succeeds.</span></span>

## <a name="connecting-to-other-services"></a><span data-ttu-id="3d6ec-137">Nawiązywanie połączenia z innymi usługami</span><span class="sxs-lookup"><span data-stu-id="3d6ec-137">Connecting to other services</span></span>
<span data-ttu-id="3d6ec-138">Łączenie ze sobą w klastrze zazwyczaj usług bezpośrednio mają dostęp do punktów końcowych innych usług, ponieważ węzły w klastrze są w tej samej sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-138">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="3d6ec-139">Aby łatwiej łączyć między usługami, Service Fabric zawiera dodatkowe usługi, które korzystają z usługi nazw.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-139">To make is easier to connect between services, Service Fabric provides additional services that use the Naming Service.</span></span> <span data-ttu-id="3d6ec-140">Usługa DNS i usługa zwrotnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-140">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="3d6ec-141">Usługa DNS</span><span class="sxs-lookup"><span data-stu-id="3d6ec-141">DNS service</span></span>
<span data-ttu-id="3d6ec-142">Począwszy od wielu usług zwłaszcza konteneryzowanych usług może mieć nazwę istniejącego adresu URL, możliwość rozwiązać te przy użyciu standardowych DNS protokołu (zamiast protokołu Naming Service) jest bardzo wygodny, szczególnie w scenariuszach "przyrostu i przesunięcia".</span><span class="sxs-lookup"><span data-stu-id="3d6ec-142">Since many services, especially containerized services, can have an existing URL name, being able to resolve these using the standard DNS protocol (rather than the Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="3d6ec-143">Jest to dokładnie, jak działa usługa DNS.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-143">This is exactly what the DNS service does.</span></span> <span data-ttu-id="3d6ec-144">Umożliwia ona mapowania nazw DNS na nazwę usługi i dlatego rozpoznać adresów IP punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-144">It enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="3d6ec-145">Jak pokazano na poniższym diagramie, usługa DNS działa w klastrze usługi sieć szkieletowa mapuje nazwy DNS nazwy usługi, które następnie są rozpoznawane przez usługę nazewnictwa do zwrócenia adresy punktów końcowych, aby nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-145">As shown in the following diagram, the DNS service, running in the Service Fabric cluster, maps DNS names to service names which are then resolved by the Naming Service to return the endpoint addresses to connect to.</span></span> <span data-ttu-id="3d6ec-146">Nazwy DNS dla usługi znajduje się w momencie tworzenia obiektu.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-146">The DNS name for the service is provided at the time of creation.</span></span> 

![Punkty końcowe usługi][9]

<span data-ttu-id="3d6ec-148">Więcej informacji na temat sposobu korzystania z usługi DNS usługi zobacz [usługa DNS w sieci szkieletowej usług Azure](service-fabric-dnsservice.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-148">For more details on how to use the DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="3d6ec-149">Zwrotny serwer proxy usługi</span><span class="sxs-lookup"><span data-stu-id="3d6ec-149">Reverse proxy service</span></span>
<span data-ttu-id="3d6ec-150">Zwrotnego serwera proxy dotyczy usługi w klastrze, który udostępnia punktów końcowych HTTP, łącznie z protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-150">The reverse proxy addresses services in the cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="3d6ec-151">Zwrotny serwer proxy znacząco upraszcza wywoływania innych usług i ich metod przez określony format identyfikatora URI i obsługuje rozpoznania, połączenia, powtórz kroki wymagane do jedną usługę do komunikowania się z inną przy użyciu usługi nazw.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-151">The reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles the resolve, connect, retry steps required for one service to communicate with another using the Naming Serivce.</span></span> <span data-ttu-id="3d6ec-152">Innymi słowy ukrywa on Naming Service od użytkownika podczas wywoływania metody innych usług, dokonując to prosty jak wywołanie adresu URL.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-152">In other words, it hides the Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![Punkty końcowe usługi][10]

<span data-ttu-id="3d6ec-154">Więcej informacji na temat sposobu korzystania z usługi zwrotny serwer proxy można znaleźć [odwrotny serwer proxy w sieci szkieletowej usług Azure](service-fabric-reverseproxy.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-154">For more details on how to use the reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="3d6ec-155">Połączenia z klientami zewnętrznymi</span><span class="sxs-lookup"><span data-stu-id="3d6ec-155">Connections from external clients</span></span>
<span data-ttu-id="3d6ec-156">Łączenie ze sobą w klastrze zazwyczaj usług bezpośrednio mają dostęp do punktów końcowych innych usług, ponieważ węzły w klastrze są w tej samej sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-156">Services connecting to each other inside a cluster generally can directly access the endpoints of other services because the nodes in a cluster are on the same local network.</span></span> <span data-ttu-id="3d6ec-157">W przypadku środowisk jednak klastra może być za modułem równoważenia obciążenia, który przekierowuje ruch przychodzący zewnętrznych za pomocą ograniczonego zestawu portów.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-157">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="3d6ec-158">W takich przypadkach usługi nadal mogą komunikować się ze sobą i rozpoznawania adresów przy użyciu usługi nazw, ale dodatkowe kroki należy zezwolić zewnętrznych klientom na łączenie się z usługami.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-158">In these cases, services can still communicate with each other and resolve addresses using the Naming Service, but extra steps must be taken to allow external clients to connect to services.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="3d6ec-159">Sieć szkieletowa usług na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3d6ec-159">Service Fabric in Azure</span></span>
<span data-ttu-id="3d6ec-160">Klastra sieci szkieletowej usług w usłudze Azure znajduje się za usługą równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-160">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="3d6ec-161">Wszystkie zewnętrznego ruchu do klastra musi przejść przez moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-161">All external traffic to the cluster must pass through the load balancer.</span></span> <span data-ttu-id="3d6ec-162">Moduł równoważenia obciążenia będzie automatycznie przesyłał dalej ruch przychodzący na porcie danego do losowe *węzła* mający ten sam port, Otwórz.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-162">The load balancer will automatically forward traffic inbound on a given port to a random *node* that has the same port open.</span></span> <span data-ttu-id="3d6ec-163">Moduł równoważenia obciążenia Azure tylko zna porty otwarty na *węzłów*, nie może określić dotyczących otwarte porty przez osobę *usług*.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-163">The Azure Load Balancer only knows about ports open on the *nodes*, it does not know about ports open by individual *services*.</span></span>

![Azure topologii równoważenia obciążenia i sieci szkieletowej usług][3]

<span data-ttu-id="3d6ec-165">Na przykład, aby zaakceptować zewnętrznych ruch na porcie **80**, muszą być skonfigurowane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3d6ec-165">For example, in order to accept external traffic on port **80**, the following things must be configured:</span></span>

1. <span data-ttu-id="3d6ec-166">Zapisu to usługa, która nasłuchuje na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-166">Write a service that listens on port 80.</span></span> <span data-ttu-id="3d6ec-167">Skonfiguruj port 80 w pliku ServiceManifest.xml usługi i otwórz odbiornik usługi, na przykład serwer sieci web siebie.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-167">Configure port 80 in the service's ServiceManifest.xml and open a listener in the service, for example, a self-hosted web server.</span></span>

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
2. <span data-ttu-id="3d6ec-168">Tworzenie klastra sieci szkieletowej usług na platformie Azure i określić port **80** jako port punktu końcowego niestandardowych dla typu węzła, który będzie hostem usługi.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-168">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for the node type that will host the service.</span></span> <span data-ttu-id="3d6ec-169">Jeśli masz więcej niż jeden typ węzła, można skonfigurować *ograniczenia umieszczania* na usługę, aby upewnić się, że działa tylko na typ węzła mającego otworzyć port punktu końcowego niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-169">If you have more than one node type, you can set up a *placement constraint* on the service to ensure it only runs on the node type that has the custom endpoint port opened.</span></span>

    ![Otwarcie portu dla typu węzła][4]
3. <span data-ttu-id="3d6ec-171">Po utworzeniu klastra, należy skonfigurować usługę równoważenia obciążenia Azure w grupie zasobów klastra, aby przesyłał dalej ruch na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-171">Once the cluster has been created, configure the Azure Load Balancer in the cluster's Resource Group to forward traffic on port 80.</span></span> <span data-ttu-id="3d6ec-172">Podczas tworzenia klastra za pośrednictwem portalu Azure, to jest automatycznie utworzyć dla każdego portu niestandardowego punktu końcowego, który został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-172">When creating a cluster through the Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Ruch do przodu w usłudze równoważenia obciążenia Azure][5]
4. <span data-ttu-id="3d6ec-174">Moduł równoważenia obciążenia Azure używa badanie w celu określenia, czy przesyłają dane do określonego węzła.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-174">The Azure Load Balancer uses a probe to determine whether or not to send traffic to a particular node.</span></span> <span data-ttu-id="3d6ec-175">Sonda okresowo sprawdza, czy punkt końcowy na każdym węźle, aby określić, czy węzeł odpowiada.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-175">The probe periodically checks an endpoint on each node to determine whether or not the node is responding.</span></span> <span data-ttu-id="3d6ec-176">Jeśli sondy nie można odebrać odpowiedzi od skonfigurowanych wiele razy, usługi równoważenia obciążenia zatrzymuje wysyłania ruchu do tego węzła.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-176">If the probe fails to receive a response after a configured number of times, the load balancer stops sending traffic to that node.</span></span> <span data-ttu-id="3d6ec-177">Podczas tworzenia klastra za pośrednictwem portalu Azure, badanie automatycznie jest konfigurowane dla poszczególnych portów niestandardowych punktu końcowego, który został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-177">When creating a cluster through the Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Ruch do przodu w usłudze równoważenia obciążenia Azure][8]

<span data-ttu-id="3d6ec-179">Należy pamiętać, że moduł równoważenia obciążenia Azure i badania tylko wiedzieć o *węzłów*, a nie *usług* działających w węzłach.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-179">It's important to remember that the Azure Load Balancer and the probe only know about the *nodes*, not the *services* running on the nodes.</span></span> <span data-ttu-id="3d6ec-180">Moduł równoważenia obciążenia Azure będą zawsze wysyłały ruchu do węzłów, które odpowiada sondowania, więc należy uważać, aby upewnić się, że usługi są dostępne w węzłach, które są w stanie odpowiadać na sondę.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-180">The Azure Load Balancer will always send traffic to nodes that respond to the probe, so care must be taken to ensure services are available on the nodes that are able to respond to the probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="3d6ec-181">Niezawodnej usługi: Opcje komunikacji wbudowanej interfejsu API</span><span class="sxs-lookup"><span data-stu-id="3d6ec-181">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="3d6ec-182">Framework niezawodne usługi jest dostarczany z kilku opcji wbudowanych komunikacji.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-182">The Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="3d6ec-183">Decyzja o tym, które jedną będzie najlepsza, zależy od wybór modelu programowania, w ramach komunikacji i język programowania, które usługi są zapisywane w.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-183">The decision about which one will work best for you depends on the choice of the programming model, the communication framework, and the programming language that your services are written in.</span></span>

* <span data-ttu-id="3d6ec-184">**Nie określonego protokołu:** Jeśli nie ma określonego wybór framework komunikacji, ale chcesz coś się szybkie i uruchomienie, a następnie jest doskonałym rozwiązaniem dla Ciebie [service remoting](service-fabric-reliable-services-communication-remoting.md), dzięki czemu Wywołanie procedury zdalnej jednoznacznie dla Reliable Services i Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-184">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want to get something up and running quickly, then the ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="3d6ec-185">Jest to najprostszy i najszybszym sposobem na szybkie wprowadzenie do komunikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-185">This is the easiest and fastest way to get started with service communication.</span></span> <span data-ttu-id="3d6ec-186">Service remoting obsługuje rozpoznawanie adresy usługi, połączenia, ponów próbę i obsługa błędów.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-186">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="3d6ec-187">To jest dostępna dla C# i aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-187">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="3d6ec-188">**HTTP**: komunikat niezależny od języka HTTP zapewnia wybór standardowych z narzędziami i serwery HTTP dostępne w wielu językach obsługiwanych przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-188">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="3d6ec-189">Usługi mogą używać żadnych HTTP stosu, w tym [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) dla aplikacji C#.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-189">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="3d6ec-190">Napisany w języku C# klienci mogą używać `ICommunicationClient` i `ServicePartitionClient` klas, natomiast dla języka Java, użyj `CommunicationClient` i `FabricServicePartitionClient` klas, [usługi rozdzielczości, połączeń HTTP i ponów próbę wykonania pętli](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="3d6ec-190">Clients written in C# can leverage the `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use the `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="3d6ec-191">**Usługi WCF**: Jeśli masz istniejący kod, który używa WCF jako platforma sieci komunikacji, a następnie można użyć `WcfCommunicationListener` po stronie serwera i `WcfCommunicationClient` i `ServicePartitionClient` klasy dla klienta.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-191">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use the `WcfCommunicationListener` for the server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for the client.</span></span> <span data-ttu-id="3d6ec-192">To jednak jest dostępna tylko dla aplikacji C# w klastrach z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-192">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="3d6ec-193">Aby uzyskać więcej informacji, zobacz ten artykuł [WCF na podstawie wykonania stosu komunikacji](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="3d6ec-193">For more details, see this article about [WCF-based implementation of the communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="3d6ec-194">Przy użyciu protokołów niestandardowych i innych platform komunikacji</span><span class="sxs-lookup"><span data-stu-id="3d6ec-194">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="3d6ec-195">Usługi można użyć protokołu lub framework do komunikacji, czy jest protokołem binarne niestandardowych za pośrednictwem gniazda TCP lub za pośrednictwem przesyłania strumieniowego zdarzenia [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) lub [Centrum IoT Azure](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="3d6ec-195">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="3d6ec-196">Sieć szkieletowa usług zapewnia komunikację interfejsów API stosu komunikacji, można podłączyć podczas całą pracę na potrzeby odnajdywania i połączyć jest pobieranej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-196">Service Fabric provides communication APIs that you can plug your communication stack into, while all the work to discover and connect is abstracted from you.</span></span> <span data-ttu-id="3d6ec-197">Znajduje się w artykule [model komunikacji niezawodnej usługi](service-fabric-reliable-services-communication.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="3d6ec-197">See this article about the [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d6ec-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d6ec-198">Next steps</span></span>
<span data-ttu-id="3d6ec-199">Dowiedz się więcej na temat pojęć i interfejsami API dostępnymi w [model komunikacji niezawodnej usługi](service-fabric-reliable-services-communication.md), następnie szybko rozpocząć pracę z [service remoting](service-fabric-reliable-services-communication-remoting.md) lub przejdź szczegółowe informacje na temat zapisu komunikatu przy użyciu odbiornika [interfejsu API sieci Web z hosta samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="3d6ec-199">Learn more about the concepts and APIs available in the [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth to learn how to write a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
