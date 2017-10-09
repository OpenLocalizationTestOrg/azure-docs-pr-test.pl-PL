---
title: "aaaAzure sieci szkieletowej usług wstecznego bezpiecznej komunikacji serwera proxy | Dokumentacja firmy Microsoft"
description: Konfigurowanie komunikacji zabezpieczonej end-to-end tooenable zwrotnego serwera proxy.
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a><span data-ttu-id="c0407-103">Usługa bezpiecznego tooa Uzyskuj dostęp do hello zwrotnego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="c0407-103">Connect tooa secure service with hello reverse proxy</span></span>

<span data-ttu-id="c0407-104">W tym artykule opisano, jak tooestablish bezpiecznego połączenia między hello zwrotnego serwera proxy i usług, umożliwiając w ten sposób zakończenia tooend bezpiecznego kanału.</span><span class="sxs-lookup"><span data-stu-id="c0407-104">This article explains how tooestablish secure connection between hello reverse proxy and services, thus enabling an end tooend secure channel.</span></span>

<span data-ttu-id="c0407-105">Połączenie usług toosecure jest obsługiwana tylko wtedy, gdy zwrotnego serwera proxy skonfigurowanego toolisten HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c0407-105">Connecting toosecure services is supported only when reverse proxy is configured toolisten on HTTPS.</span></span> <span data-ttu-id="c0407-106">Pozostałej części dokumentu hello przyjęto założenie, że w przypadku hello.</span><span class="sxs-lookup"><span data-stu-id="c0407-106">Rest of hello document assumes this is hello case.</span></span>
<span data-ttu-id="c0407-107">Odwołuje się zbyt[odwrotny serwer proxy w sieci szkieletowej usług Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello zwrotnego serwera proxy w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="c0407-107">Refer too[Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a><span data-ttu-id="c0407-108">Ustanawianie bezpiecznego połączenia między hello zwrotnego serwera proxy i usługami</span><span class="sxs-lookup"><span data-stu-id="c0407-108">Secure connection establishment between hello reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-tooservices"></a><span data-ttu-id="c0407-109">Odwrotny serwer proxy uwierzytelniania tooservices:</span><span class="sxs-lookup"><span data-stu-id="c0407-109">Reverse proxy authenticating tooservices:</span></span>
<span data-ttu-id="c0407-110">Hello zwrotny serwer proxy identyfikowany przy użyciu jego certyfikat określony tooservices ***reverseProxyCertificate*** właściwości w hello **klastra** [sekcji Typ zasobu](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c0407-110">hello reverse proxy identifies itself tooservices using its certificate, specified with ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="c0407-111">Usługi można zaimplementować hello logiki tooverify hello certyfikat przedstawiony przez zwrotny serwer proxy hello.</span><span class="sxs-lookup"><span data-stu-id="c0407-111">Services can implement hello logic tooverify hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="c0407-112">Hello usługi można określić ustawienia konfiguracji w pakiecie konfiguracji hello szczegóły certyfikatu klienta hello akceptowane.</span><span class="sxs-lookup"><span data-stu-id="c0407-112">hello services can specify hello accepted client certificate details as configuration settings in hello configuration package.</span></span> <span data-ttu-id="c0407-113">Mogą być odczytywane w czasie wykonywania, a używane toovalidate hello certyfikat przedstawiony przez zwrotny serwer proxy hello.</span><span class="sxs-lookup"><span data-stu-id="c0407-113">This can be read at runtime and used toovalidate hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="c0407-114">Odwołuje się zbyt[Zarządzanie parametry aplikacji](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello konfiguracji ustawień.</span><span class="sxs-lookup"><span data-stu-id="c0407-114">Refer too[Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a><span data-ttu-id="c0407-115">Odwrotny serwer proxy weryfikowania tożsamości usługi hello za pośrednictwem hello certyfikat przedstawiony przez usługę hello:</span><span class="sxs-lookup"><span data-stu-id="c0407-115">Reverse proxy verifying hello service's identity via hello certificate presented by hello service:</span></span>
<span data-ttu-id="c0407-116">tooperform weryfikacji certyfikatu serwera certyfikatów hello przedstawianych przez usługi hello, zwrotny serwer proxy obsługuje jeden hello następujące opcje: None, ServiceCommonNameAndIssuer i ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="c0407-116">tooperform server certificate validation of hello certificates presented by hello services, reverse proxy supports one of hello following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="c0407-117">tooselect jedną z tych trzech opcji Określ hello **ApplicationCertificateValidationPolicy** w sekcji parametrów hello elementu bramy aplikacji/Http w obszarze [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="c0407-117">tooselect one of these three options, specify hello **ApplicationCertificateValidationPolicy** in hello parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="c0407-118">Aby uzyskać szczegółowe informacje o dodatkowych konfiguracji dla każdego z tych opcji można znaleźć toohello następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c0407-118">Refer toohello next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="c0407-119">Opcje sprawdzania poprawności certyfikatu usługi</span><span class="sxs-lookup"><span data-stu-id="c0407-119">Service certificate validation options</span></span> 

- <span data-ttu-id="c0407-120">**Brak**: zwrotny serwer proxy Pomija weryfikację certyfikatu usługi proxy hello i ustanawia hello bezpiecznego połączenia.</span><span class="sxs-lookup"><span data-stu-id="c0407-120">**None**: Reverse proxy skips verification of hello proxied service certificate and establishes hello secure connection.</span></span> <span data-ttu-id="c0407-121">Jest to zachowanie domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="c0407-121">This is hello default behavior.</span></span>
<span data-ttu-id="c0407-122">Określ hello **ApplicationCertificateValidationPolicy** z wartością **Brak** w sekcji parametrów hello elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c0407-122">Specify hello **ApplicationCertificateValidationPolicy** with value **None** in hello parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="c0407-123">**ServiceCommonNameAndIssuer**: zwrotny serwer proxy sprawdza hello certyfikat przedstawiony przez usługę hello na podstawie nazwa pospolita certyfikatu i odcisk palca wystawcy natychmiastowego: Określ hello **ApplicationCertificateValidationPolicy**  z wartością **ServiceCommonNameAndIssuer** w sekcji parametrów hello elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c0407-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies hello certificate presented by hello service based on certificate's common name and immediate issuer's thumbprint: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in hello parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="c0407-124">Dodawanie listy hello toospecify wspólnej nazwy usługi oraz odciski palców wystawcy, **bramy aplikacji/Http/ServiceCommonNameAndIssuer** elementu w obszarze fabricSettings, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c0407-124">toospecify hello list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="c0407-125">W elemencie tablicy parametrów hello można dodawać wiele par odcisk palca wystawcy i nazwa pospolita certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c0407-125">Multiple certificate common name and issuer thumbprint pairs can be added in hello parameters array element.</span></span> 

<span data-ttu-id="c0407-126">Jeśli zwrotnego serwera proxy punktu końcowego hello jest połączenie toopresents certyfikatu, który jest wspólny nazwy i wystawców odcisk palca zgodny z dowolnym hello wartości określone w tym miejscu, kanału SSL.</span><span class="sxs-lookup"><span data-stu-id="c0407-126">If hello endpoint reverse proxy is connecting toopresents a certificate who's common name and  issuer thumbprint matches any of hello values specified here, SSL channel is established.</span></span> <span data-ttu-id="c0407-127">Po awarii toomatch hello szczegóły certyfikatu zwrotnego serwera proxy nie powiedzie się żądanie powitania klienta z kodem stanu 502 (zły bramy).</span><span class="sxs-lookup"><span data-stu-id="c0407-127">Upon failure toomatch hello certificate details, reverse proxy fails hello client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="c0407-128">Witaj wiersza stanu HTTP będzie również zawierać hello frazy "Nieprawidłowy certyfikat SSL."</span><span class="sxs-lookup"><span data-stu-id="c0407-128">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span> 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- <span data-ttu-id="c0407-129">**ServiceCertificateThumbprints**: zwrotny serwer proxy zweryfikuje hello serwerem proxy usługi certyfikatu opartego na jego odcisk palca.</span><span class="sxs-lookup"><span data-stu-id="c0407-129">**ServiceCertificateThumbprints**: Reverse proxy will verify hello proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="c0407-130">Można wybrać toogo tej trasy podczas hello usługi są skonfigurowane przy użyciu certyfikatów z podpisem własnym: Określ hello **ApplicationCertificateValidationPolicy** z wartością **ServiceCertificateThumbprints**w sekcji parametrów hello elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c0407-130">You can choose toogo this route when hello services are configured with self signed certificates: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in hello parameters section of ApplicationGateway/Http element.</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="c0407-131">Również określić odciski palców hello z **ServiceCertificateThumbprints** wpis w sekcji parametrów elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c0407-131">Also specify hello thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="c0407-132">Można określić wiele odciski palców jako listę rozdzielaną przecinkami, w polu wartość hello, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="c0407-132">Multiple thumbprints can be specified as a comma-separated list in hello value field, as shown below:</span></span>

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

<span data-ttu-id="c0407-133">Jeśli hello odcisk palca certyfikatu serwera hello jest wyświetlana na tej pozycji konfiguracji, zwrotny serwer proxy zakończy się pomyślnie hello połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="c0407-133">If hello thumbprint of hello server certificate is listed in this config entry, reverse proxy succeeds hello SSL connection.</span></span> <span data-ttu-id="c0407-134">W przeciwnym razie zostaje zakończone hello połączenia i kończy się niepowodzeniem hello żądanie klienta z 502 (zły bramy).</span><span class="sxs-lookup"><span data-stu-id="c0407-134">Otherwise, it terminates hello connection and fails hello client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="c0407-135">Witaj wiersza stanu HTTP będzie również zawierać hello frazy "Nieprawidłowy certyfikat SSL."</span><span class="sxs-lookup"><span data-stu-id="c0407-135">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="c0407-136">Punkt końcowy zaznaczenia logiki podczas usług ekspozycji punktów końcowych, bezpieczne, jak również niezabezpieczona</span><span class="sxs-lookup"><span data-stu-id="c0407-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="c0407-137">Sieć szkieletowa usług obsługuje konfigurowanie wiele punktów końcowych dla usługi.</span><span class="sxs-lookup"><span data-stu-id="c0407-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="c0407-138">Zobacz [Określanie zasobów w manifeście usługi](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c0407-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="c0407-139">Zwrotny serwer proxy wybierze jeden z hello punkty końcowe tooforward hello żądania oparte na powitania **ListenerName** parametr zapytania.</span><span class="sxs-lookup"><span data-stu-id="c0407-139">Reverse proxy selects one of hello endpoints tooforward hello request based on hello  **ListenerName** query parameter.</span></span> <span data-ttu-id="c0407-140">Jeśli nie zostanie określony, ją wybrać dowolnego punktu końcowego z listy punktów końcowych hello.</span><span class="sxs-lookup"><span data-stu-id="c0407-140">If this is not specified, it can pick any endpoint from hello endpoints list.</span></span> <span data-ttu-id="c0407-141">Teraz, może to być punkt końcowy HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c0407-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="c0407-142">Mogą istnieć scenariusze/wymagania miejscu hello toooperate zwrotnego serwera proxy w "tylko tryb bezpieczny", tj</span><span class="sxs-lookup"><span data-stu-id="c0407-142">There might be scenarios/requirements where you want hello reverse proxy toooperate in a "secure only mode", i.e</span></span> <span data-ttu-id="c0407-143">nie ma punktów końcowych hello bezpiecznego zwrotnego serwera proxy tooforward żądań toounsecured.</span><span class="sxs-lookup"><span data-stu-id="c0407-143">you don't want hello secure reverse proxy tooforward requests toounsecured endpoints.</span></span> <span data-ttu-id="c0407-144">Można to osiągnąć, określając hello **SecureOnlyMode** pozycji konfiguracji z wartością **true** w sekcji parametrów hello elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c0407-144">This can be achieved by specifying hello **SecureOnlyMode** configuration entry with value **true** in hello parameters section of ApplicationGateway/Http element.</span></span>   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> <span data-ttu-id="c0407-145">Podczas działania w **SecureOnlyMode**, jeśli określono klienta **ListenerName** odpowiadającego punktu końcowego HTTP(unsecured) tooan, zwrotnego serwera proxy nie powiedzie się Żądanie hello 404 kod stanu HTTP (nie znaleziono).</span><span class="sxs-lookup"><span data-stu-id="c0407-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding tooan HTTP(unsecured) endpoint, reverse proxy fails hello request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a><span data-ttu-id="c0407-146">Konfigurowanie uwierzytelniania certyfikatu klienta za pośrednictwem hello zwrotnego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="c0407-146">Setting up client certificate authentication through hello reverse proxy</span></span>
<span data-ttu-id="c0407-147">Kończenie żądań SSL odbywa się na powitania zwrotnego serwera proxy i wszystkie powitania klienta certyfikatu dane zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="c0407-147">SSL termination happens at hello reverse proxy and all hello client certificate data is lost.</span></span> <span data-ttu-id="c0407-148">Uwierzytelnianie certyfikatu hello usług tooperform klienta, ustaw hello **ForwardClientCertificate** ustawienia w sekcji parametrów hello elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c0407-148">For hello services tooperform client certificate authentication, set hello **ForwardClientCertificate** setting in hello parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="c0407-149">Gdy **ForwardClientCertificate** ustawiono zbyt**false**, odwrócić serwera proxy nie będą wymagane dla certyfikatu klienta hello podczas jego uzgadniania protokołu SSL z powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="c0407-149">When **ForwardClientCertificate** is set too**false**, reverse proxy will not request for hello client certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="c0407-150">Jest to zachowanie domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="c0407-150">This is hello default behavior.</span></span>

2. <span data-ttu-id="c0407-151">Gdy **ForwardClientCertificate** ustawiono zbyt**true**, żądań serwera proxy dla certyfikatu klienta hello wstecznego podczas jego uzgadniania protokołu SSL z powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="c0407-151">When **ForwardClientCertificate** is set too**true**, reverse proxy requests for hello client's certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="c0407-152">Następnie prześle je powitania klienta danych certyfikatu w niestandardowy nagłówek HTTP o nazwie **certyfikat klienta X**.</span><span class="sxs-lookup"><span data-stu-id="c0407-152">It will then forward hello client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="c0407-153">wartość nagłówka Hello jest ciąg formatu PEM hello kodowanie base64 certyfikatu powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="c0407-153">hello header value is hello base64 encoded PEM format string of hello client's certificate.</span></span> <span data-ttu-id="c0407-154">usługi Hello można powiodło się/niepowodzenie hello żądania z kodem stanu odpowiednie po sprawdzeniu danych certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="c0407-154">hello service can succeed/fail hello request with appropriate status code after inspecting hello certificate data.</span></span>
<span data-ttu-id="c0407-155">Jeżeli powitania klienta nie przedstawić certyfikat, zwrotny serwer proxy przekazuje pusty nagłówek i powiadom hello usługi dojścia hello case.</span><span class="sxs-lookup"><span data-stu-id="c0407-155">If hello client does not present a certificate, reverse proxy forwards an empty header and let hello service handle hello case.</span></span>

> <span data-ttu-id="c0407-156">Zwrotny serwer proxy jest tylko usługa przesyłania dalej.</span><span class="sxs-lookup"><span data-stu-id="c0407-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="c0407-157">Nie będzie wykonywać żadnych weryfikacji certyfikatu powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="c0407-157">It will not perform any validation of hello client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c0407-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c0407-158">Next steps</span></span>
* <span data-ttu-id="c0407-159">Odwołuje się zbyt[Konfigurowanie usług toosecure tooconnect zwrotnego serwera proxy](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) dla usługi Azure Resource Manager szablonu przykłady tooconfigure bezpiecznego zwrotny serwer proxy przy użyciu opcji weryfikacji certyfikatu hello w innej usługi.</span><span class="sxs-lookup"><span data-stu-id="c0407-159">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="c0407-160">Zobacz przykład protokołu HTTP do komunikacji między usługami w [przykładowy projekt w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c0407-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="c0407-161">Zdalne wywołania procedur z usług zdalnych niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="c0407-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="c0407-162">Interfejs API, który używa OWIN w niezawodnej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="c0407-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="c0407-163">Zarządzanie certyfikatami klastra</span><span class="sxs-lookup"><span data-stu-id="c0407-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
