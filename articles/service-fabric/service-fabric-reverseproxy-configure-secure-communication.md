---
title: "Sieć szkieletowa usług Azure odwrotna bezpiecznej komunikacji serwera proxy | Dokumentacja firmy Microsoft"
description: Skonfiguruj zwrotnego serwera proxy, aby komunikacja zabezpieczona na trasie.
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
ms.openlocfilehash: 568f9638c59282bcd7d3fae058a1588a889c22dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-secure-service-with-the-reverse-proxy"></a><span data-ttu-id="c28d9-103">Połączyć z usługą bezpieczny z zwrotnego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="c28d9-103">Connect to a secure service with the reverse proxy</span></span>

<span data-ttu-id="c28d9-104">W tym artykule wyjaśniono, jak można ustanowić bezpiecznego połączenia między zwrotnego serwera proxy i usług, umożliwiając kompleksowe bezpiecznego kanału.</span><span class="sxs-lookup"><span data-stu-id="c28d9-104">This article explains how to establish secure connection between the reverse proxy and services, thus enabling an end to end secure channel.</span></span>

<span data-ttu-id="c28d9-105">Łączenie z usługami bezpiecznego jest obsługiwana tylko wtedy, gdy zwrotnego serwera proxy jest skonfigurowane do nasłuchiwania protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c28d9-105">Connecting to secure services is supported only when reverse proxy is configured to listen on HTTPS.</span></span> <span data-ttu-id="c28d9-106">Pozostałej części dokumentu przyjęto założenie, że jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="c28d9-106">Rest of the document assumes this is the case.</span></span>
<span data-ttu-id="c28d9-107">Zapoznaj się [odwrotny serwer proxy w sieci szkieletowej usług Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) skonfigurować zwrotnego serwera proxy w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="c28d9-107">Refer to [Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) to configure the reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-the-reverse-proxy-and-services"></a><span data-ttu-id="c28d9-108">Ustanawianie bezpiecznego połączenia między zwrotnego serwera proxy i usługami</span><span class="sxs-lookup"><span data-stu-id="c28d9-108">Secure connection establishment between the reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-to-services"></a><span data-ttu-id="c28d9-109">Do usługi uwierzytelniania odwrotnego serwera proxy:</span><span class="sxs-lookup"><span data-stu-id="c28d9-109">Reverse proxy authenticating to services:</span></span>
<span data-ttu-id="c28d9-110">Zwrotny serwer proxy identyfikuje do usług za pomocą swojego certyfikatu określony za pomocą ***reverseProxyCertificate*** właściwości w **klastra** [sekcji Typ zasobu](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c28d9-110">The reverse proxy identifies itself to services using its certificate, specified with ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="c28d9-111">Usługi można zaimplementować logiki, aby zweryfikować certyfikat przedstawiony przez zwrotny serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="c28d9-111">Services can implement the logic to verify the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="c28d9-112">Usługi można określić szczegóły certyfikatu klienta akceptowane jako ustawienia konfiguracji w pakiet konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c28d9-112">The services can specify the accepted client certificate details as configuration settings in the configuration package.</span></span> <span data-ttu-id="c28d9-113">Może to odczytu w czasie wykonywania i używany do sprawdzania poprawności certyfikatu przedstawionego przez zwrotny serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="c28d9-113">This can be read at runtime and used to validate the certificate presented by the reverse proxy.</span></span> <span data-ttu-id="c28d9-114">Zapoznaj się [Zarządzanie parametry aplikacji](service-fabric-manage-multiple-environment-app-configuration.md) Dodaj ustawień konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c28d9-114">Refer to [Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) to add the configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-the-services-identity-via-the-certificate-presented-by-the-service"></a><span data-ttu-id="c28d9-115">Weryfikowanie tożsamości usługi za pośrednictwem certyfikat przedstawiony przez usługę zwrotnego serwera proxy:</span><span class="sxs-lookup"><span data-stu-id="c28d9-115">Reverse proxy verifying the service's identity via the certificate presented by the service:</span></span>
<span data-ttu-id="c28d9-116">Aby przeprowadzić weryfikacji certyfikatu serwera certyfikatów przedstawiony przez usługę, zwrotny serwer proxy obsługuje jedną z następujących opcji: None, ServiceCommonNameAndIssuer i ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="c28d9-116">To perform server certificate validation of the certificates presented by the services, reverse proxy supports one of the following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="c28d9-117">Aby wybrać jedną z tych trzech opcji, należy określić **ApplicationCertificateValidationPolicy** w sekcji parametrów elementu bramy aplikacji/Http w obszarze [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="c28d9-117">To select one of these three options, specify the **ApplicationCertificateValidationPolicy** in the parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

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

<span data-ttu-id="c28d9-118">Zapoznaj się z sekcją dalej, aby uzyskać szczegółowe informacje o dodatkowych konfiguracji dla każdego z tych opcji.</span><span class="sxs-lookup"><span data-stu-id="c28d9-118">Refer to the next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="c28d9-119">Opcje sprawdzania poprawności certyfikatu usługi</span><span class="sxs-lookup"><span data-stu-id="c28d9-119">Service certificate validation options</span></span> 

- <span data-ttu-id="c28d9-120">**Brak**: zwrotny serwer proxy Pomija weryfikację certyfikatu usługi proxy oraz ustanawianie bezpiecznego połączenia.</span><span class="sxs-lookup"><span data-stu-id="c28d9-120">**None**: Reverse proxy skips verification of the proxied service certificate and establishes the secure connection.</span></span> <span data-ttu-id="c28d9-121">Jest to zachowanie domyślne.</span><span class="sxs-lookup"><span data-stu-id="c28d9-121">This is the default behavior.</span></span>
<span data-ttu-id="c28d9-122">Określ **ApplicationCertificateValidationPolicy** z wartością **Brak** w sekcji parametrów elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c28d9-122">Specify the **ApplicationCertificateValidationPolicy** with value **None** in the parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="c28d9-123">**ServiceCommonNameAndIssuer**: zwrotny serwer proxy sprawdza, czy certyfikat przedstawiony przez usługę, na podstawie nazwa pospolita certyfikatu i odcisk palca wystawcy natychmiastowego: Określ **ApplicationCertificateValidationPolicy** z wartością **ServiceCommonNameAndIssuer** w sekcji parametrów elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c28d9-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies the certificate presented by the service based on certificate's common name and immediate issuer's thumbprint: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="c28d9-124">Aby określić listę typowych nazwę usługi i odcisków palca wystawcy, Dodaj **bramy aplikacji/Http/ServiceCommonNameAndIssuer** elementu w obszarze fabricSettings, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c28d9-124">To specify the list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="c28d9-125">W elemencie tablicy parametrów można dodawać wiele par odcisk palca wystawcy i nazwa pospolita certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c28d9-125">Multiple certificate common name and issuer thumbprint pairs can be added in the parameters array element.</span></span> 

<span data-ttu-id="c28d9-126">Jeśli zwrotnego serwera proxy punktu końcowego jest połączenie przedstawia certyfikat, który jest wspólny nazwy i wystawców odcisk palca dopasowuje dowolną z wartości określone w tym miejscu, kanału SSL.</span><span class="sxs-lookup"><span data-stu-id="c28d9-126">If the endpoint reverse proxy is connecting to presents a certificate who's common name and  issuer thumbprint matches any of the values specified here, SSL channel is established.</span></span> <span data-ttu-id="c28d9-127">W przypadku awarii odpowiadające szczegóły certyfikatu zwrotnego serwera proxy nie powiedzie się żądanie klienta z kodem stanu 502 (zły bramy).</span><span class="sxs-lookup"><span data-stu-id="c28d9-127">Upon failure to match the certificate details, reverse proxy fails the client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="c28d9-128">Wiersz stanu HTTP będzie również zawierać frazy "Nieprawidłowy certyfikat SSL."</span><span class="sxs-lookup"><span data-stu-id="c28d9-128">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span> 

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


- <span data-ttu-id="c28d9-129">**ServiceCertificateThumbprints**: zwrotny serwer proxy zweryfikuje oparte na jego odcisk palca certyfikatu usługi proxy.</span><span class="sxs-lookup"><span data-stu-id="c28d9-129">**ServiceCertificateThumbprints**: Reverse proxy will verify the proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="c28d9-130">Użytkownik może przejść tej trasy, gdy usługi są skonfigurowane przy użyciu własnych podpisany certyfikaty: Określ **ApplicationCertificateValidationPolicy** z wartością **ServiceCertificateThumbprints** w sekcja parametrów elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c28d9-130">You can choose to go this route when the services are configured with self signed certificates: Specify the **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in the parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="c28d9-131">Również określić odciski palców z **ServiceCertificateThumbprints** wpis w sekcji parametrów elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c28d9-131">Also specify the thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="c28d9-132">Wiele odciski palców można określić jako listę rozdzielaną przecinkami, w polu wartość, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="c28d9-132">Multiple thumbprints can be specified as a comma-separated list in the value field, as shown below:</span></span>

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

<span data-ttu-id="c28d9-133">Jeśli odcisk palca certyfikatu serwera znajduje się w tej pozycji konfiguracji, zwrotny serwer proxy pomyślnego połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="c28d9-133">If the thumbprint of the server certificate is listed in this config entry, reverse proxy succeeds the SSL connection.</span></span> <span data-ttu-id="c28d9-134">W przeciwnym razie zakończy połączenie i nie powiodło się żądanie klienta z 502 (zły bramy).</span><span class="sxs-lookup"><span data-stu-id="c28d9-134">Otherwise, it terminates the connection and fails the client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="c28d9-135">Wiersz stanu HTTP będzie również zawierać frazy "Nieprawidłowy certyfikat SSL."</span><span class="sxs-lookup"><span data-stu-id="c28d9-135">The HTTP status line will also contain the phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="c28d9-136">Punkt końcowy zaznaczenia logiki podczas usług ekspozycji punktów końcowych, bezpieczne, jak również niezabezpieczona</span><span class="sxs-lookup"><span data-stu-id="c28d9-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="c28d9-137">Sieć szkieletowa usług obsługuje konfigurowanie wiele punktów końcowych dla usługi.</span><span class="sxs-lookup"><span data-stu-id="c28d9-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="c28d9-138">Zobacz [Określanie zasobów w manifeście usługi](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c28d9-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="c28d9-139">Zwrotny serwer proxy wybiera jeden z punktów końcowych do przekazywania żądań na podstawie **ListenerName** parametr zapytania.</span><span class="sxs-lookup"><span data-stu-id="c28d9-139">Reverse proxy selects one of the endpoints to forward the request based on the  **ListenerName** query parameter.</span></span> <span data-ttu-id="c28d9-140">Jeśli nie zostanie określony, ją wybrać dowolnego punktu końcowego z listy punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="c28d9-140">If this is not specified, it can pick any endpoint from the endpoints list.</span></span> <span data-ttu-id="c28d9-141">Teraz, może to być punkt końcowy HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c28d9-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="c28d9-142">Mogą istnieć scenariusze/wymagania miejscu zwrotnego serwera proxy do działania w "tylko tryb bezpieczny", tj</span><span class="sxs-lookup"><span data-stu-id="c28d9-142">There might be scenarios/requirements where you want the reverse proxy to operate in a "secure only mode", i.e</span></span> <span data-ttu-id="c28d9-143">nie chcesz bezpiecznego zwrotnego serwera proxy do przekazywania żądań do punktów końcowych niezabezpieczona.</span><span class="sxs-lookup"><span data-stu-id="c28d9-143">you don't want the secure reverse proxy to forward requests to unsecured endpoints.</span></span> <span data-ttu-id="c28d9-144">Można to osiągnąć, określając **SecureOnlyMode** pozycji konfiguracji z wartością **true** w sekcji parametrów elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c28d9-144">This can be achieved by specifying the **SecureOnlyMode** configuration entry with value **true** in the parameters section of ApplicationGateway/Http element.</span></span>   

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
> <span data-ttu-id="c28d9-145">Podczas działania w **SecureOnlyMode**, jeśli określono klienta **ListenerName** odpowiadającej HTTP(unsecured) punktu końcowego, zwrotnego serwera proxy nie powiodło się żądanie z 404 kod stanu HTTP (nie znaleziono).</span><span class="sxs-lookup"><span data-stu-id="c28d9-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding to an HTTP(unsecured) endpoint, reverse proxy fails the request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-the-reverse-proxy"></a><span data-ttu-id="c28d9-146">Konfigurowanie uwierzytelniania certyfikatu klienta przy użyciu zwrotnego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="c28d9-146">Setting up client certificate authentication through the reverse proxy</span></span>
<span data-ttu-id="c28d9-147">Kończenie żądań SSL odbywa się na zwrotnego serwera proxy i nie zostały utracone wszystkie dane certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="c28d9-147">SSL termination happens at the reverse proxy and all the client certificate data is lost.</span></span> <span data-ttu-id="c28d9-148">Usługi uwierzytelniania certyfikatu klienta, należy ustawić **ForwardClientCertificate** ustawienia w sekcji parametrów elementu bramy aplikacji/Http.</span><span class="sxs-lookup"><span data-stu-id="c28d9-148">For the services to perform client certificate authentication, set the **ForwardClientCertificate** setting in the parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="c28d9-149">Gdy **ForwardClientCertificate** ustawiono **false**, odwrócić serwera proxy nie będą wymagane dla certyfikatu klienta podczas jego uzgadniania protokołu SSL z klientem.</span><span class="sxs-lookup"><span data-stu-id="c28d9-149">When **ForwardClientCertificate** is set to **false**, reverse proxy will not request for the client certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="c28d9-150">Jest to zachowanie domyślne.</span><span class="sxs-lookup"><span data-stu-id="c28d9-150">This is the default behavior.</span></span>

2. <span data-ttu-id="c28d9-151">Gdy **ForwardClientCertificate** ma ustawioną wartość **true**, wstecznego żądania certyfikatu klienta serwera proxy podczas jego uzgadniania protokołu SSL przy użyciu klienta.</span><span class="sxs-lookup"><span data-stu-id="c28d9-151">When **ForwardClientCertificate** is set to **true**, reverse proxy requests for the client's certificate during its SSL handshake with the client.</span></span>
<span data-ttu-id="c28d9-152">Następnie prześle je klienta danych certyfikatu w niestandardowy nagłówek HTTP o nazwie **certyfikat klienta X**.</span><span class="sxs-lookup"><span data-stu-id="c28d9-152">It will then forward the client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="c28d9-153">Wartość nagłówka jest ciągiem formatu PEM kodowanie base64 certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="c28d9-153">The header value is the base64 encoded PEM format string of the client's certificate.</span></span> <span data-ttu-id="c28d9-154">Usługa może powiodło się/Niepowodzenie żądania z kodem stanu odpowiednie po sprawdzeniu danych certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c28d9-154">The service can succeed/fail the request with appropriate status code after inspecting the certificate data.</span></span>
<span data-ttu-id="c28d9-155">Jeśli klient nie przedstawić certyfikat, zwrotny serwer proxy przekazuje pusty nagłówek i zezwolić, w przypadku obsługi.</span><span class="sxs-lookup"><span data-stu-id="c28d9-155">If the client does not present a certificate, reverse proxy forwards an empty header and let the service handle the case.</span></span>

> <span data-ttu-id="c28d9-156">Zwrotny serwer proxy jest tylko usługa przesyłania dalej.</span><span class="sxs-lookup"><span data-stu-id="c28d9-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="c28d9-157">Nie będzie wykonywać żadnych weryfikacji certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="c28d9-157">It will not perform any validation of the client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c28d9-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c28d9-158">Next steps</span></span>
* <span data-ttu-id="c28d9-159">Zapoznaj się [Konfiguruj zwrotnego serwera proxy do nawiązania bezpiecznego usług](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) dla usługi Azure Resource Manager przykłady szablonu, aby skonfigurować zabezpieczenia zwrotny serwer proxy przy użyciu certyfikatu innej usługi opcji weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="c28d9-159">Refer to [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples to configure secure reverse proxy with the different service certificate validation options.</span></span>
* <span data-ttu-id="c28d9-160">Zobacz przykład protokołu HTTP do komunikacji między usługami w [przykładowy projekt w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c28d9-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="c28d9-161">Zdalne wywołania procedur z usług zdalnych niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="c28d9-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="c28d9-162">Interfejs API, który używa OWIN w niezawodnej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="c28d9-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="c28d9-163">Zarządzanie certyfikatami klastra</span><span class="sxs-lookup"><span data-stu-id="c28d9-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
