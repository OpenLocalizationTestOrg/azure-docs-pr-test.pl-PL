---
title: "aaaAzure sieci szkieletowej usług odwrotny serwer proxy | Dokumentacja firmy Microsoft"
description: "Użyj usługi sieć szkieletowa zwrotnego serwera proxy dla toomicroservices komunikacji z wewnętrznych i zewnętrznych klastra hello."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="5cb68-103">Zwrotny serwer proxy w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="5cb68-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="5cb68-104">Witaj zwrotnego serwera proxy, wbudowanego w sieci szkieletowej usług Azure adresów mikrousług w klastrze usługi sieć szkieletowa hello, który udostępnia punktów końcowych HTTP.</span><span class="sxs-lookup"><span data-stu-id="5cb68-104">hello reverse proxy that's built into Azure Service Fabric addresses microservices in hello Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="5cb68-105">Model komunikacji Mikrousług</span><span class="sxs-lookup"><span data-stu-id="5cb68-105">Microservices communication model</span></span>
<span data-ttu-id="5cb68-106">Mikrousług w sieci szkieletowej usług zwykle Uruchom w podzestawie maszyny wirtualne w klastrze hello i można przenosić od jednego tooanother maszyny wirtualnej z różnych przyczyn.</span><span class="sxs-lookup"><span data-stu-id="5cb68-106">Microservices in Service Fabric typically run on a subset of virtual machines in hello cluster and can move from one virtual machine tooanother for various reasons.</span></span> <span data-ttu-id="5cb68-107">Tak hello punktów końcowych mikrousług można zmienić dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="5cb68-107">So, hello endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="5cb68-108">Witaj typowy wzorzec toocommunicate toohello mikrousługi znajduje się poniżej hello rozwiązać pętli:</span><span class="sxs-lookup"><span data-stu-id="5cb68-108">hello typical pattern toocommunicate toohello microservice is hello following resolve loop:</span></span>

1. <span data-ttu-id="5cb68-109">Rozwiązania lokalizacji usługi hello początkowo za pośrednictwem usługi nazewnictwa hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-109">Resolve hello service location initially through hello naming service.</span></span>
2. <span data-ttu-id="5cb68-110">Usługa toohello Connect.</span><span class="sxs-lookup"><span data-stu-id="5cb68-110">Connect toohello service.</span></span>
3. <span data-ttu-id="5cb68-111">Określić hello przyczyny błędów połączenia i rozpoznać lokalizacji usługi hello ponownie, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5cb68-111">Determine hello cause of connection failures, and resolve hello service location again when necessary.</span></span>

<span data-ttu-id="5cb68-112">Ten proces obejmuje zwykle zawijania biblioteki klienta komunikacji w pętli ponawiania implementujący hello usługi zasady rozwiązania i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="5cb68-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements hello service resolution and retry policies.</span></span>
<span data-ttu-id="5cb68-113">Aby uzyskać więcej informacji, zobacz [Connect i łączyć się z usługami](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="5cb68-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-hello-reverse-proxy"></a><span data-ttu-id="5cb68-114">Komunikacja za pomocą hello zwrotnego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="5cb68-114">Communicating by using hello reverse proxy</span></span>
<span data-ttu-id="5cb68-115">we wszystkich węzłach klastra hello hello jest uruchamiany Hello zwrotnego serwera proxy w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="5cb68-115">hello reverse proxy in Service Fabric runs on all hello nodes in hello cluster.</span></span> <span data-ttu-id="5cb68-116">Wykonuje proces rozpoznawania całej usługi hello w imieniu klienta, a następnie przesyła dalej żądanie klienta hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-116">It performs hello entire service resolution process on a client's behalf and then forwards hello client request.</span></span> <span data-ttu-id="5cb68-117">Tak uruchomić w klastrze hello klienci mogą używać dowolnego klienta HTTP komunikacji bibliotek tootalk toohello usługi docelowej, przy użyciu zwrotnego serwera proxy hello czy działa lokalnie na hello na tym samym węźle.</span><span class="sxs-lookup"><span data-stu-id="5cb68-117">So, clients that run on hello cluster can use any client-side HTTP communication libraries tootalk toohello target service by using hello reverse proxy that runs locally on hello same node.</span></span>

![Wewnętrznej komunikacji][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a><span data-ttu-id="5cb68-119">Osiągnięcia mikrousług z zewnątrz hello klastra</span><span class="sxs-lookup"><span data-stu-id="5cb68-119">Reaching microservices from outside hello cluster</span></span>
<span data-ttu-id="5cb68-120">Hello domyślny model komunikacji zewnętrznej mikrousług to model opcjonalnych, gdzie każdego nie można uzyskać dostępu do usługi bezpośrednio z klientami zewnętrznymi.</span><span class="sxs-lookup"><span data-stu-id="5cb68-120">hello default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="5cb68-121">[Moduł równoważenia obciążenia Azure](../load-balancer/load-balancer-overview.md), który jest granicę sieci między mikrousług i klientami zewnętrznymi, wykonuje translatora adresów sieciowych i zewnętrzne przekazuje żądania punkty końcowe IP:port toointernal.</span><span class="sxs-lookup"><span data-stu-id="5cb68-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests toointernal IP:port endpoints.</span></span> <span data-ttu-id="5cb68-122">toomake mikrousługi punktu końcowego tooexternal dostępny bezpośrednio klientów, należy najpierw skonfigurować port tooforward tooeach ruchu, który hello usługi używa modułu równoważenia obciążenia w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-122">toomake a microservice's endpoint directly accessible tooexternal clients, you must first configure Load Balancer tooforward traffic tooeach port that hello service uses in hello cluster.</span></span> <span data-ttu-id="5cb68-123">Ponadto większość mikrousług, szczególnie stanowe mikrousług, nie na żywo na wszystkich węzłach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of hello cluster.</span></span> <span data-ttu-id="5cb68-124">Witaj mikrousług można przenosić między węzłami w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="5cb68-124">hello microservices can move between nodes on failover.</span></span> <span data-ttu-id="5cb68-125">W takich przypadkach usługi równoważenia obciążenia skutecznie nie można określić lokalizacji hello węzła docelowego hello toowhich replik hello przekazywała ruchu.</span><span class="sxs-lookup"><span data-stu-id="5cb68-125">In such cases, Load Balancer cannot effectively determine hello location of hello target node of hello replicas toowhich it should forward traffic.</span></span>

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a><span data-ttu-id="5cb68-126">Osiągnięcia mikrousług za pośrednictwem hello zwrotny serwer proxy z poza hello klastra</span><span class="sxs-lookup"><span data-stu-id="5cb68-126">Reaching microservices via hello reverse proxy from outside hello cluster</span></span>
<span data-ttu-id="5cb68-127">Zamiast konfigurować hello port poszczególnych usług w usłudze równoważenia obciążenia, można skonfigurować tylko hello portu hello zwrotnego serwera proxy w usłudze równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="5cb68-127">Instead of configuring hello port of an individual service in Load Balancer, you can configure just hello port of hello reverse proxy in Load Balancer.</span></span> <span data-ttu-id="5cb68-128">Taka konfiguracja pozwala klientom poza klastrem hello reach usługi wewnątrz klastra hello przy użyciu zwrotnego serwera proxy hello bez dodatkowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5cb68-128">This configuration lets clients outside hello cluster reach services inside hello cluster by using hello reverse proxy without additional configuration.</span></span>

![Komunikacji zewnętrznej][0]

> [!WARNING]
> <span data-ttu-id="5cb68-130">Po skonfigurowaniu port proxy odwrotnej hello w usłudze równoważenia obciążenia wszystkie mikrousług hello klastra, które udostępniają punkt końcowy HTTP adresowane z poza hello klastra.</span><span class="sxs-lookup"><span data-stu-id="5cb68-130">When you configure hello reverse proxy's port in Load Balancer, all microservices in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a><span data-ttu-id="5cb68-131">Format identyfikatora URI do adresowania usług przy użyciu zwrotnego serwera proxy hello</span><span class="sxs-lookup"><span data-stu-id="5cb68-131">URI format for addressing services by using hello reverse proxy</span></span>
<span data-ttu-id="5cb68-132">Witaj zwrotnego serwera proxy jest używana powinny zostać przekazane określonych uniform resource identifier (URI) format tooidentify hello partycji toowhich hello przychodzącego żądania obsługi:</span><span class="sxs-lookup"><span data-stu-id="5cb68-132">hello reverse proxy uses a specific uniform resource identifier (URI) format tooidentify hello service partition toowhich hello incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="5cb68-133">**http (s):** hello zwrotny serwer proxy może być skonfigurowany tooaccept HTTP lub ruchu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5cb68-133">**http(s):** hello reverse proxy can be configured tooaccept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="5cb68-134">Przekazywanie protokołu HTTPS, można znaleźć zbyt[uzyskuj Usługa bezpiecznego tooa hello zwrotnego serwera proxy](service-fabric-reverseproxy-configure-secure-communication.md) po toolisten Instalatora zwrotnego serwera proxy w protokole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5cb68-134">For HTTPS forwarding, refer too[Connect tooa secure service with hello reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup toolisten on HTTPS.</span></span>
* <span data-ttu-id="5cb68-135">**Klaster pełną nazwę domeny (FQDN) | wewnętrznym adresem IP:** dla klientów zewnętrznych, można skonfigurować hello zwrotnego serwera proxy, aby był dostępny za pośrednictwem hello klastra domeny, na przykład mycluster.eastus.cloudapp.azure.com. Domyślnie program hello zwrotnego serwera proxy jest uruchamiany na każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="5cb68-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure hello reverse proxy so that it is reachable through hello cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, hello reverse proxy runs on every node.</span></span> <span data-ttu-id="5cb68-136">Dla wewnętrznej ruchu hello zwrotny serwer proxy można połączyć się z hosta lokalnego lub na dowolny węzeł wewnętrzny adres IP, np. 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="5cb68-136">For internal traffic, hello reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="5cb68-137">**Port:** jest to, że jest to port hello, na przykład 19081, który został określony dla zwrotnego serwera proxy hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-137">**Port:** This is hello port, such as 19081, that has been specified for hello reverse proxy.</span></span>
* <span data-ttu-id="5cb68-138">**ServiceInstanceName:** jest hello Pełna nazwa wystąpienia usługi hello wdrożone próbujesz tooreach bez hello "fabric: /" schematu.</span><span class="sxs-lookup"><span data-stu-id="5cb68-138">**ServiceInstanceName:** This is hello fully-qualified name of hello deployed service instance that you are trying tooreach without hello "fabric:/" scheme.</span></span> <span data-ttu-id="5cb68-139">Na przykład tooreach hello *fabric: / myapp/Moja_usługa/* usługi, należy użyć *myapp/Moja_usługa*.</span><span class="sxs-lookup"><span data-stu-id="5cb68-139">For example, tooreach hello *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="5cb68-140">Nazwa wystąpienia usługi Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="5cb68-140">hello service instance name is case-sensitive.</span></span> <span data-ttu-id="5cb68-141">Przy użyciu innej wielkości znaków dla nazwy wystąpienia usługi hello w adresie URL hello powoduje toofail żądań hello z 404 (nie znaleziono).</span><span class="sxs-lookup"><span data-stu-id="5cb68-141">Using a different casing for hello service instance name in hello URL causes hello requests toofail with 404 (Not Found).</span></span>
* <span data-ttu-id="5cb68-142">**Sufiks ścieżki:** to hello rzeczywiste ścieżki adresu URL, takie jak *myapi/wartości/Dodaj/3*, dla hello interesujące tooconnect do usługi.</span><span class="sxs-lookup"><span data-stu-id="5cb68-142">**Suffix path:** This is hello actual URL path, such as *myapi/values/add/3*, for hello service that you want tooconnect to.</span></span>
* <span data-ttu-id="5cb68-143">**PartitionKey:** usługi podzielonym na partycje, jest to klucz obliczanej partycji hello hello partycji, które mają tooreach.</span><span class="sxs-lookup"><span data-stu-id="5cb68-143">**PartitionKey:** For a partitioned service, this is hello computed partition key of hello partition that you want tooreach.</span></span> <span data-ttu-id="5cb68-144">Należy pamiętać, że jest to *nie* hello identyfikator GUID partycji.</span><span class="sxs-lookup"><span data-stu-id="5cb68-144">Note that this is *not* hello partition ID GUID.</span></span> <span data-ttu-id="5cb68-145">Ten parametr nie jest wymagana w przypadku usług korzystających z schemat partycji singleton hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-145">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="5cb68-146">**PartitionKind:** to schemat partycji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-146">**PartitionKind:** This is hello service partition scheme.</span></span> <span data-ttu-id="5cb68-147">Może to być "Int64Range" lub "O nazwie".</span><span class="sxs-lookup"><span data-stu-id="5cb68-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="5cb68-148">Ten parametr nie jest wymagana w przypadku usług korzystających z schemat partycji singleton hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-148">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="5cb68-149">**ListenerName** punkty końcowe hello z usługi hello są formularza hello {"Punkty końcowe": {"Listener1": "Punk końcowy 1", "Listener2": "Punk końcowy 2"...}}.</span><span class="sxs-lookup"><span data-stu-id="5cb68-149">**ListenerName** hello endpoints from hello service are of hello form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="5cb68-150">Gdy usługa hello udostępnia wiele punktów końcowych, identyfikuje punkt końcowy hello tego żądania klienta hello powinny zostać przekazane.</span><span class="sxs-lookup"><span data-stu-id="5cb68-150">When hello service exposes multiple endpoints, this identifies hello endpoint that hello client request should be forwarded to.</span></span> <span data-ttu-id="5cb68-151">Ten można pominąć w przypadku usługi hello tylko jeden odbiornik.</span><span class="sxs-lookup"><span data-stu-id="5cb68-151">This can be omitted if hello service has only one listener.</span></span>
* <span data-ttu-id="5cb68-152">**TargetReplicaSelector** Określa jak powinna być zaznaczona hello docelowej repliki lub wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="5cb68-152">**TargetReplicaSelector** This specifies how hello target replica or instance should be selected.</span></span>
  * <span data-ttu-id="5cb68-153">W przypadku stanowego usługi docelowej hello hello TargetReplicaSelector może być jedną z następujących hello: "PrimaryReplica", "RandomSecondaryReplica" lub "RandomReplica".</span><span class="sxs-lookup"><span data-stu-id="5cb68-153">When hello target service is stateful, hello TargetReplicaSelector can be one of hello following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="5cb68-154">Jeśli ten parametr nie jest określony, hello domyślną jest "PrimaryReplica".</span><span class="sxs-lookup"><span data-stu-id="5cb68-154">When this parameter is not specified, hello default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="5cb68-155">Gdy Usługa docelowa hello jest bezstanowych, zwrotny serwer proxy wybiera losowe wystąpienie hello partycji tooforward hello żądanie usługi.</span><span class="sxs-lookup"><span data-stu-id="5cb68-155">When hello target service is stateless, reverse proxy picks a random instance of hello service partition tooforward hello request to.</span></span>
* <span data-ttu-id="5cb68-156">**Limit czasu:** określa hello przekroczenia limitu czasu dla żądania hello HTTP utworzonych przez usługę toohello zwrotny serwer proxy hello imieniu hello żądania klienta.</span><span class="sxs-lookup"><span data-stu-id="5cb68-156">**Timeout:**  This specifies hello timeout for hello HTTP request created by hello reverse proxy toohello service on behalf of hello client request.</span></span> <span data-ttu-id="5cb68-157">Witaj, wartość domyślna to 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="5cb68-157">hello default value is 60 seconds.</span></span> <span data-ttu-id="5cb68-158">Jest to parametr opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="5cb68-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="5cb68-159">Przykład użycia</span><span class="sxs-lookup"><span data-stu-id="5cb68-159">Example usage</span></span>
<span data-ttu-id="5cb68-160">Na przykład Przyjrzyjmy hello *fabric: / MyApp/Moja_usługa* usługi, która otwiera odbiornik HTTP na powitania następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="5cb68-160">As an example, let's take hello *fabric:/MyApp/MyService* service that opens an HTTP listener on hello following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="5cb68-161">Poniżej przedstawiono zasoby hello hello usługi:</span><span class="sxs-lookup"><span data-stu-id="5cb68-161">Following are hello resources for hello service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="5cb68-162">Jeśli usługa hello używa singleton hello schemat partycjonowania, hello *PartitionKey* i *PartitionKind* parametrów ciągu zapytania nie są wymagane, a usługa hello jest osiągalna przy użyciu bramy hello jako:</span><span class="sxs-lookup"><span data-stu-id="5cb68-162">If hello service uses hello singleton partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters are not required, and hello service can be reached by using hello gateway as:</span></span>

* <span data-ttu-id="5cb68-163">Zewnętrznie:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="5cb68-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="5cb68-164">Wewnętrznie:`http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="5cb68-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="5cb68-165">Jeśli usługa hello używa hello Int64 jednolity schemat partycjonowania, hello *PartitionKey* i *PartitionKind* parametrów ciągu zapytania musi być używane tooreach partycji usługi hello:</span><span class="sxs-lookup"><span data-stu-id="5cb68-165">If hello service uses hello Uniform Int64 partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters must be used tooreach a partition of hello service:</span></span>

* <span data-ttu-id="5cb68-166">Zewnętrznie:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="5cb68-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="5cb68-167">Wewnętrznie:`http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="5cb68-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="5cb68-168">tooreach hello zasobów, które udostępnia usługi hello, po prostu umieść ścieżka zasobu powitania po nazwie usługi hello w adresie URL hello:</span><span class="sxs-lookup"><span data-stu-id="5cb68-168">tooreach hello resources that hello service exposes, simply place hello resource path after hello service name in hello URL:</span></span>

* <span data-ttu-id="5cb68-169">Zewnętrznie:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="5cb68-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="5cb68-170">Wewnętrznie:`http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="5cb68-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="5cb68-171">Hello bramy następnie przekazuje te żądania usługi toohello adresu URL:</span><span class="sxs-lookup"><span data-stu-id="5cb68-171">hello gateway will then forward these requests toohello service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="5cb68-172">Specjalnej obsługi podczas udostępniania portów usług</span><span class="sxs-lookup"><span data-stu-id="5cb68-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="5cb68-173">Bramy aplikacji Azure prób tooresolve usługą adresów ponownie i ponów żądanie hello, gdy nie można nawiązać połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="5cb68-173">Azure Application Gateway attempts tooresolve a service address again and retry hello request when a service cannot be reached.</span></span> <span data-ttu-id="5cb68-174">Jest główną zaletą bramy aplikacji, ponieważ kod klienta nie jest potrzebne tooimplement własnej rozdzielczości usługi rozwiązać pętli.</span><span class="sxs-lookup"><span data-stu-id="5cb68-174">This is a major benefit of Application Gateway because client code does not need tooimplement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="5cb68-175">Ogólnie rzecz biorąc gdy nie można połączyć się z usługą, wystąpienie usługi hello lub repliki został przeniesiony tooa innego węzła w ramach jego normalnej cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="5cb68-175">Generally, when a service cannot be reached, hello service instance or replica has moved tooa different node as part of its normal lifecycle.</span></span> <span data-ttu-id="5cb68-176">W takim przypadku bramy aplikacji może pojawić się sieci połączenia błąd wskazujący, że punkt końcowy, bez otwartego dłużej na powitania pierwotnie rozpoznać adres.</span><span class="sxs-lookup"><span data-stu-id="5cb68-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on hello originally resolved address.</span></span>

<span data-ttu-id="5cb68-177">Jednak repliki lub wystąpień usługi można udostępniać procesu hosta i może również udostępniać port obsługiwanych przez serwer sieci web opartych na pliku http.sys w tym:</span><span class="sxs-lookup"><span data-stu-id="5cb68-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="5cb68-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="5cb68-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="5cb68-179">WebListener platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="5cb68-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="5cb68-180">Katana</span><span class="sxs-lookup"><span data-stu-id="5cb68-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="5cb68-181">W takim przypadku prawdopodobnie tego serwera sieci web hello jest dostępne w hello procesu hosta i odpowiada toorequests, ale hello rozpoznać wystąpienia usługi lub replika nie jest już dostępny na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-181">In this situation, it is likely that hello web server is available in hello host process and responding toorequests, but hello resolved service instance or replica is no longer available on hello host.</span></span> <span data-ttu-id="5cb68-182">W takim przypadku hello bramy z serwera sieci web hello otrzyma odpowiedzi HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="5cb68-182">In this case, hello gateway will receive an HTTP 404 response from hello web server.</span></span> <span data-ttu-id="5cb68-183">W związku z tym HTTP 404 ma dwa różne znaczenie:</span><span class="sxs-lookup"><span data-stu-id="5cb68-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="5cb68-184">Wielkość liter #1: adres usługi hello jest poprawna, ale nie istnieje zasób hello hello żądanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5cb68-184">Case #1: hello service address is correct, but hello resource that hello user requested does not exist.</span></span>
- <span data-ttu-id="5cb68-185">Przypadek #2: adres usługi hello jest nieprawidłowa, i zasobu hello hello żądanego użytkownika może istnieć na inny węzeł.</span><span class="sxs-lookup"><span data-stu-id="5cb68-185">Case #2: hello service address is incorrect, and hello resource that hello user requested might exist on a different node.</span></span>

<span data-ttu-id="5cb68-186">pierwszym przypadku Hello jest normalne 404 protokołu HTTP, która jest uznawana za błąd użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5cb68-186">hello first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="5cb68-187">Jednak w drugim przypadku hello hello użytkownik zażądał z zasobem, który istnieje.</span><span class="sxs-lookup"><span data-stu-id="5cb68-187">However, in hello second case, hello user has requested a resource that does exist.</span></span> <span data-ttu-id="5cb68-188">Brama aplikacji został toolocate, który ponieważ hello samą usługą została przeniesiona.</span><span class="sxs-lookup"><span data-stu-id="5cb68-188">Application Gateway was unable toolocate it because hello service itself has moved.</span></span> <span data-ttu-id="5cb68-189">Aplikacji potrzeb tooresolve hello adres bramy ponownie i ponowić żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-189">Application Gateway needs tooresolve hello address again and retry hello request.</span></span>

<span data-ttu-id="5cb68-190">Brama aplikacji w związku z tym musi toodistinguish sposób, między tymi dwoma przypadkami.</span><span class="sxs-lookup"><span data-stu-id="5cb68-190">Application Gateway thus needs a way toodistinguish between these two cases.</span></span> <span data-ttu-id="5cb68-191">toomake, że różnica, wskazówkę z serwera hello jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="5cb68-191">toomake that distinction, a hint from hello server is required.</span></span>

* <span data-ttu-id="5cb68-192">Domyślnie bramy aplikacji zakłada przypadku #2 i próbuje ponownie Żądanie hello tooresolve i problem.</span><span class="sxs-lookup"><span data-stu-id="5cb68-192">By default, Application Gateway assumes case #2 and attempts tooresolve and issue hello request again.</span></span>
* <span data-ttu-id="5cb68-193">tooApplication przypadku #1 tooindicate bramy, usługa hello powinna zwracać powitania po nagłówka odpowiedzi HTTP:</span><span class="sxs-lookup"><span data-stu-id="5cb68-193">tooindicate case #1 tooApplication Gateway, hello service should return hello following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="5cb68-194">Tego nagłówka odpowiedzi HTTP wskazuje normalnej sytuacji HTTP 404, w których hello żądany zasób nie istnieje, a bramy aplikacji nie będzie próbował adres usługi hello tooresolve ponownie.</span><span class="sxs-lookup"><span data-stu-id="5cb68-194">This HTTP response header indicates a normal HTTP 404 situation in which hello requested resource does not exist, and Application Gateway will not attempt tooresolve hello service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="5cb68-195">Instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="5cb68-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="5cb68-196">Włącz zwrotnego serwera proxy za pośrednictwem portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5cb68-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="5cb68-197">Azure portal udostępnia opcję tooenable zwrotnego serwera proxy podczas tworzenia nowego klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="5cb68-197">Azure portal provides an option tooenable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="5cb68-198">W obszarze **klastra tworzenia sieci szkieletowej usług**, krok 2: konfigurację klastra, konfiguracja typu węzła, zaznacz pole wyboru hello zbyt "Włącz zwrotnego serwera proxy".</span><span class="sxs-lookup"><span data-stu-id="5cb68-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select hello checkbox too"Enable reverse proxy".</span></span>
<span data-ttu-id="5cb68-199">Do konfigurowania bezpiecznej zwrotnego serwera proxy, można określić certyfikat SSL w kroku 3: zbyt zabezpieczeń, konfigurowanie ustawień zabezpieczeń klastra, hello zaznacz pole wyboru "Obejmują certyfikat protokołu SSL dla zwrotnego serwera proxy" i wprowadź szczegóły certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select hello checkbox too"Include a SSL certificate for reverse proxy" and enter hello certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="5cb68-200">Włącz zwrotny serwer proxy przy użyciu szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5cb68-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="5cb68-201">Można użyć hello [szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable hello zwrotnego serwera proxy w sieci szkieletowej usług dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="5cb68-201">You can use hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) tooenable hello reverse proxy in Service Fabric for hello cluster.</span></span>

<span data-ttu-id="5cb68-202">Odwołuje się zbyt[skonfigurować HTTPS zwrotnego serwera Proxy w klastrze bezpiecznego](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) dla usługi Azure Resource Manager szablonu przykłady tooconfigure bezpiecznego zwrotny serwer proxy z certyfikatu i obsługa Przerzucanie certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="5cb68-202">Refer too[Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples tooconfigure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="5cb68-203">Po pierwsze możesz uzyskać szablon hello hello klastra, które mają toodeploy.</span><span class="sxs-lookup"><span data-stu-id="5cb68-203">First, you get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="5cb68-204">Można użyć hello przykładowych szablonów lub utworzyć niestandardowy szablon usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5cb68-204">You can either use hello sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="5cb68-205">Następnie można włączyć hello zwrotny serwer proxy przy użyciu hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5cb68-205">Then, you can enable hello reverse proxy by using hello following steps:</span></span>

1. <span data-ttu-id="5cb68-206">Zdefiniuj port dla zwrotnego serwera proxy hello w hello [sekcji parametrów](../azure-resource-manager/resource-group-authoring-templates.md) hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="5cb68-206">Define a port for hello reverse proxy in hello [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of hello template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="5cb68-207">Określ port powitania dla każdego z obiektów nodetype hello w hello **klastra** [sekcji Typ zasobu](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5cb68-207">Specify hello port for each of hello nodetype objects in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="5cb68-208">Hello port jest identyfikowane przez nazwę parametru hello, reverseProxyEndpointPort.</span><span class="sxs-lookup"><span data-stu-id="5cb68-208">hello port is identified by hello parameter name, reverseProxyEndpointPort.</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. <span data-ttu-id="5cb68-209">tooaddress hello zwrotny serwer proxy z poza hello Azure klastra, skonfigurować zasady modułu równoważenia obciążenia Azure hello hello port, który określono w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="5cb68-209">tooaddress hello reverse proxy from outside hello Azure cluster, set up hello Azure Load Balancer rules for hello port that you specified in step 1.</span></span>

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. <span data-ttu-id="5cb68-210">tooconfigure certyfikatów SSL na porcie powitania dla zwrotnego serwera proxy hello, Dodaj hello certyfikatu toohello ***reverseProxyCertificate*** właściwości w hello **klastra** [sekcji Typ zasobu](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5cb68-210">tooconfigure SSL certificates on hello port for hello reverse proxy, add hello certificate toohello ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a><span data-ttu-id="5cb68-211">Obsługa certyfikatu zwrotny serwer proxy, który różni się od hello klastra certyfikatu</span><span class="sxs-lookup"><span data-stu-id="5cb68-211">Supporting a reverse proxy certificate that's different from hello cluster certificate</span></span>
 <span data-ttu-id="5cb68-212">Jeśli certyfikat zwrotny serwer proxy hello różni się od hello certyfikatu, który zabezpiecza hello klastra, to hello wcześniej określić certyfikat powinien być zainstalowany na maszynie wirtualnej hello i dodany listy kontroli dostępu toohello (ACL), dzięki czemu można sieci szkieletowej usług do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="5cb68-212">If hello reverse proxy certificate is different from hello certificate that secures hello cluster, then hello previously specified certificate should be installed on hello virtual machine and added toohello access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="5cb68-213">Można to zrobić w hello **virtualMachineScaleSets** [sekcji Typ zasobu](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5cb68-213">This can be done in hello **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="5cb68-214">W przypadku instalacji należy dodać osProfile toohello tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="5cb68-214">For installation, add that certificate toohello osProfile.</span></span> <span data-ttu-id="5cb68-215">sekcja rozszerzenia Hello hello szablonu można aktualizować hello certyfikatu w hello listy ACL.</span><span class="sxs-lookup"><span data-stu-id="5cb68-215">hello extension section of hello template can update hello certificate in hello ACL.</span></span>

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> <span data-ttu-id="5cb68-216">Korzystając z certyfikatów, które różnią się od hello klastra certyfikatu tooenable hello zwrotny serwer proxy istniejącego klastra, zainstaluj certyfikat zwrotny serwer proxy hello i zaktualizuj hello listy ACL w klastrze hello, przed włączeniem hello zwrotnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="5cb68-216">When you use certificates that are different from hello cluster certificate tooenable hello reverse proxy on an existing cluster, install hello reverse proxy certificate and update hello ACL on hello cluster before you enable hello reverse proxy.</span></span> <span data-ttu-id="5cb68-217">Zakończenie hello [szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) wdrożenia przy użyciu ustawień hello wymienione wcześniej przed rozpoczęciem wdrażania tooenable hello zwrotny serwer proxy w kroki 1 – 4.</span><span class="sxs-lookup"><span data-stu-id="5cb68-217">Complete hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using hello settings mentioned previously before you start a deployment tooenable hello reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cb68-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5cb68-218">Next steps</span></span>
* <span data-ttu-id="5cb68-219">Zobacz przykład protokołu HTTP do komunikacji między usługami w [przykładowy projekt w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="5cb68-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="5cb68-220">Usługa HTTP toosecure przekazywania z hello zwrotnego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="5cb68-220">Forwarding toosecure HTTP service with hello reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="5cb68-221">Zdalne wywołania procedur z usług zdalnych niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="5cb68-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="5cb68-222">Interfejs API, który używa OWIN w niezawodnej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="5cb68-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="5cb68-223">Komunikacyjny WCF za pomocą niezawodnych usług</span><span class="sxs-lookup"><span data-stu-id="5cb68-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="5cb68-224">Opcje konfiguracji dodatkowych zwrotnego serwera proxy, można znaleźć w części bramy aplikacji/Http [ustawienia klastra dostosować sieci szkieletowej usług](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="5cb68-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
