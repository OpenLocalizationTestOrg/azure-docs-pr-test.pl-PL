---
title: "Diagnostyka proxy wstecznego aaaAzure sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor i diagnozowanie przetwarzania żądania na powitania zwrotnego serwera proxy."
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
ms.date: 08/08/2017
ms.author: kavyako
ms.openlocfilehash: 9687b9688dc26ba619cbdfab1b1f49a3035345c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a><span data-ttu-id="b601a-103">Monitorowanie i diagnozowanie przetwarzania żądania na powitania zwrotnego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="b601a-103">Monitor and diagnose request processing at hello reverse proxy</span></span>

<span data-ttu-id="b601a-104">Począwszy od wersji hello 5.7 sieci szkieletowej usług, zdarzeń zwrotnego serwera proxy są dostępne dla kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b601a-104">Starting with hello 5.7 release of Service Fabric, reverse proxy events are available for collection.</span></span> <span data-ttu-id="b601a-105">Witaj zdarzenia są dostępne w dwóch kanałów z tylko zdarzenia błędów pokrewnych błąd przetwarzania toorequest hello zwrotnego serwera proxy i drugi kanał zawierający zdarzenia pełne wpisy dla żądań pomyślnie i niepomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b601a-105">hello events are available in two channels, one with only error events related toorequest processing failure at hello reverse proxy and second channel containing verbose events with entries for both successful and failed requests.</span></span>

<span data-ttu-id="b601a-106">Odwołuje się zbyt[zbierania zdarzeń zwrotnego serwera proxy](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable, zbierając zdarzenia z tych kanałów w klastrach sieć szkieletowa usług Azure i lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b601a-106">Refer too[Collect reverse proxy events](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable collecting events from these channels in local and Azure Service Fabric clusters.</span></span>

## <a name="troubleshoot-using-diagnostics-logs"></a><span data-ttu-id="b601a-107">Rozwiązywanie problemów przy użyciu dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="b601a-107">Troubleshoot using diagnostics logs</span></span>
<span data-ttu-id="b601a-108">Oto kilka przykładów w sposób toointerpret hello wspólnej awarii dzienniki co może wystąpić:</span><span class="sxs-lookup"><span data-stu-id="b601a-108">Here are some examples on how toointerpret hello common failure logs that one can encounter:</span></span>

1. <span data-ttu-id="b601a-109">Zwrotny serwer proxy zwraca kod stanu odpowiedzi 504 (limit czasu).</span><span class="sxs-lookup"><span data-stu-id="b601a-109">Reverse proxy returns response status code 504 (Timeout).</span></span>

    <span data-ttu-id="b601a-110">Jedną z przyczyn może być powodu tooreply awaria usługi toohello przed upływem limitu czasu w bazie wiedzy hello żądania.</span><span class="sxs-lookup"><span data-stu-id="b601a-110">One reason could be due toohello service failing tooreply within hello request timeout period.</span></span>
<span data-ttu-id="b601a-111">pierwsze zdarzenie Hello poniżej rejestruje hello szczegóły żądania hello odebraniu hello zwrotnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="b601a-111">hello first event below logs hello details of hello request received at hello reverse proxy.</span></span> <span data-ttu-id="b601a-112">Witaj drugie zdarzenie wskazuje Żądanie hello nie powiodło się podczas przekazywania tooservice, właściwym zbyt "Błąd wewnętrzny = ERROR_WINHTTP_TIMEOUT"</span><span class="sxs-lookup"><span data-stu-id="b601a-112">hello second event indicates that hello request failed while forwarding tooservice, due too"internal error = ERROR_WINHTTP_TIMEOUT"</span></span> 

    <span data-ttu-id="b601a-113">ładunek Hello obejmuje:</span><span class="sxs-lookup"><span data-stu-id="b601a-113">hello payload includes:</span></span>

    *  <span data-ttu-id="b601a-114">**traceId**: ten identyfikator GUID może być używany toocorrelate wszystkie zdarzenia hello odpowiadającego tooa pojedyncze żądanie.</span><span class="sxs-lookup"><span data-stu-id="b601a-114">**traceId**: This GUID can be used toocorrelate all hello events corresponding tooa single request.</span></span> <span data-ttu-id="b601a-115">W hello poniżej dwa zdarzenia, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, co oznacza, że należą one toohello jednym żądaniu.</span><span class="sxs-lookup"><span data-stu-id="b601a-115">In hello below two events, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implying they belong toohello same request.</span></span>
    *  <span data-ttu-id="b601a-116">**Adres_url_żądania**: hello adresu URL (adres URL zwrotnego serwera proxy) toowhich hello żądanie zostało wysłane.</span><span class="sxs-lookup"><span data-stu-id="b601a-116">**requestUrl**: hello URL (Reverse proxy URL) toowhich hello request was sent.</span></span>
    *  <span data-ttu-id="b601a-117">**zlecenie**: Zlecenie HTTP.</span><span class="sxs-lookup"><span data-stu-id="b601a-117">**verb**: HTTP verb.</span></span>
    *  <span data-ttu-id="b601a-118">**remoteAddress**: adres wysyłanie żądania powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="b601a-118">**remoteAddress**: Address of client sending hello request.</span></span>
    *  <span data-ttu-id="b601a-119">**resolvedServiceUrl**: Usługa punktu końcowego adresu URL toowhich hello przychodzące żądanie zostało rozpoznane.</span><span class="sxs-lookup"><span data-stu-id="b601a-119">**resolvedServiceUrl**: Service endpoint URL toowhich hello incoming request was resolved.</span></span> 
    *  <span data-ttu-id="b601a-120">**Szczegóły błędu**: dodatkowe informacje o niepowodzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="b601a-120">**errorDetails**: Additional information about hello failure.</span></span>

    ```
    {
      "Timestamp": "2017-07-20T15:57:59.9871163-07:00",
      "ProviderName": "Microsoft-ServiceFabric",
      "Id": 51477,
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Request url = https://localhost:19081/LocationApp/LocationFEService?zipcode=98052, verb = GET, remote (client) address = ::1, resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052, request processing start time =     15:58:00.074114 (745,608.196 MSec) ",
      "ProcessId": 57696,
      "Level": "Informational",
      "Keywords": "0x1000000000000021",
      "EventName": "ReverseProxy",
      "ActivityID": null,
      "RelatedActivityID": null,
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?zipcode=98052",
        "verb": "GET",
        "remoteAddress": "::1",
        "resolvedServiceUrl": "Https://localhost:8491/LocationApp/?zipcode=98052",
        "requestStartTime": "2017-07-20T15:58:00.0741142-07:00"
      }
    }

    {
      "Timestamp": "2017-07-20T16:00:01.3173605-07:00",
      ...
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request tooservice: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
      ...
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "statusCode": 504,
        "description": "Reverse Proxy Timeout",
        "sendRequestPhase": "FinishSendRequest",
        "errorDetails": "internal error = ERROR_WINHTTP_TIMEOUT"
      }
    }
    ```

2. <span data-ttu-id="b601a-121">Zwrotny serwer proxy zwraca kod stanu odpowiedzi 404 (nie znaleziono).</span><span class="sxs-lookup"><span data-stu-id="b601a-121">Reverse proxy returns response status code 404 (Not Found).</span></span> 
    
    <span data-ttu-id="b601a-122">Oto przykład zdarzenia gdzie zwrotny serwer proxy zwraca 404, ponieważ nie może on hello toofind dopasowania punktu końcowego usługi.</span><span class="sxs-lookup"><span data-stu-id="b601a-122">Here is an example event where reverse proxy returns 404 since it failed toofind hello matching service endpoint.</span></span>
    <span data-ttu-id="b601a-123">wpisy ładunku Hello zainteresowania w tym miejscu są:</span><span class="sxs-lookup"><span data-stu-id="b601a-123">hello payload  entries of interest here are:</span></span>
    *  <span data-ttu-id="b601a-124">**processRequestPhase**: wskazuje fazy hello podczas przetwarzania żądania wystąpił błąd hello, ***TryGetEndpoint*** tj</span><span class="sxs-lookup"><span data-stu-id="b601a-124">**processRequestPhase**: Indicates hello phase during request processing when hello failure occurred, ***TryGetEndpoint*** i.e</span></span> <span data-ttu-id="b601a-125">przy próbie toofetch hello usługi punktu końcowego tooforward do.</span><span class="sxs-lookup"><span data-stu-id="b601a-125">while trying toofetch hello service endpoint tooforward to.</span></span> 
    *  <span data-ttu-id="b601a-126">**Szczegóły błędu**: Wyświetla listę kryteriów wyszukiwania hello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="b601a-126">**errorDetails**: Lists hello endpoint search criteria.</span></span> <span data-ttu-id="b601a-127">Tutaj można zobaczyć, że listenerName hello określony = **FrontEndListener** listy punktów końcowych hello repliki zawiera tylko odbiornik o nazwie hello **OldListener**.</span><span class="sxs-lookup"><span data-stu-id="b601a-127">Here you can see that hello listenerName specified = **FrontEndListener** whereas hello replica endpoint list only contains a listener with hello name **OldListener**.</span></span>
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward tooservice: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
      "ProcessId": 57696,
      "Level": "Warning",
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "c1cca3b7-f85d-4fef-a162-88af23604343",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?ListenerName=NewListener&zipcode=98052",
        ...
        "processRequestPhase": "TryGetEndoint",
        "errorDetails": "SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Https:\/\/localhost:8491\/LocationApp\/\"}}"
      }
    }
    ```
    <span data-ttu-id="b601a-128">Innym przykładem, gdzie zwrotny serwer proxy może zwrócić 404 Nie znaleziono jest: parametr konfiguracji ApplicationGateway\Http **SecureOnlyMode** ustawiono tootrue zwrotny serwer proxy hello nasłuchiwania na **HTTPS**, Jednak wszystkie punkty końcowe repliki hello są niezabezpieczone (nasłuchiwanie HTTP).</span><span class="sxs-lookup"><span data-stu-id="b601a-128">Another example where reverse proxy can return 404 Not Found is: ApplicationGateway\Http configuration parameter **SecureOnlyMode** is set tootrue with hello reverse proxy listening on **HTTPS**, however all of hello replica endpoints are unsecure (listening on HTTP).</span></span>
    <span data-ttu-id="b601a-129">Odtwarzanie zwraca proxy 404, ponieważ nie można odnaleźć punktu końcowego nasłuchiwania na żądanie hello tooforward HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b601a-129">Reverse proxy returns 404 since it cannot find an endpoint listening on HTTPS tooforward hello request.</span></span> <span data-ttu-id="b601a-130">Analizowanie parametrów hello w ładunku zdarzenia hello pomaga toonarrow dół hello problemu:</span><span class="sxs-lookup"><span data-stu-id="b601a-130">Analyzing hello parameters in hello event payload helps toonarrow down hello issue:</span></span>
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. <span data-ttu-id="b601a-131">Zwrotny serwer proxy toohello żądanie kończy się niepowodzeniem z błędem przekroczenia limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="b601a-131">Request toohello reverse proxy fails with a timeout error.</span></span> 
    <span data-ttu-id="b601a-132">dzienniki zdarzeń Hello zawierają zdarzenia z szczegółów żądania hello odebranych (nie jest tutaj widoczny).</span><span class="sxs-lookup"><span data-stu-id="b601a-132">hello event logs contain an event with hello received request details (not shown here).</span></span>
    <span data-ttu-id="b601a-133">następne zdarzenie Hello pokazuje, że usługa hello zwrócił kod stanu 404 i inicjuje zwrotnego serwera proxy, ponownie rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="b601a-133">hello next event shows that hello service responded with a 404 status code and reverse proxy initiates a re-resolve.</span></span> 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request tooservice returned: status code = 404, status description = , Reresolving ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "statusCode": 404,
        "statusDescription": ""
      }
    }
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Re-resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052 ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "requestUrl": "Https://localhost:8491/LocationApp/?zipcode=98052"
      }
    }
    ```
    <span data-ttu-id="b601a-134">Podczas zbierania wszystkich zdarzeń hello, zostanie wyświetlony train zdarzeń przedstawiający co rozwiązanie, a następnie spróbuj do przodu.</span><span class="sxs-lookup"><span data-stu-id="b601a-134">When collecting all hello events, you see a train of events showing every resolve and forward attempt.</span></span>
    <span data-ttu-id="b601a-135">Ostatnie zdarzenie Hello w serii hello pokazuje hello przetwarzania żądania nie powiodła się z limitem czasu, wraz z hello liczbę prób rozpoznania powiodło się.</span><span class="sxs-lookup"><span data-stu-id="b601a-135">hello last event in hello series shows hello request processing has failed with a timeout, along with hello number of successful resolve attempts.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b601a-136">Go zaleca się tookeep hello pełne kanału zbierania zdarzeń domyślnie wyłączona i włącz ją do rozwiązywania problemów na podstawie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="b601a-136">It is recommended tookeep hello  verbose channel event collection disabled by default and enable it for troubleshooting on a need basis.</span></span>

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Error while processing request: number of successful resolve attempts = 12, error = FABRIC_E_TIMEOUT, message = , phase = ResolveServicePartition,  ",
      "EventName": "ReverseProxy",
      ...
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "resolveCount": 12,
        "errorval": -2147017729,
        "errorMessage": "",
        "processRequestPhase": "ResolveServicePartition",
        "errorDetails": ""
      }
    }
    ```
    
    <span data-ttu-id="b601a-137">Jeśli kolekcji jest włączony dla zdarzeń krytyczny błąd tylko, zobaczysz jednego zdarzenia ze szczegółami hello limitu czasu i liczby hello prób rozpoznania.</span><span class="sxs-lookup"><span data-stu-id="b601a-137">If collection is enabled for critical/error events only, you see one event with details about hello timeout and hello number of resolve attempts.</span></span> 
    
    <span data-ttu-id="b601a-138">Gdy usługa hello toosend użytkownika wstecz toohello kod stanu 404, powinien być dołączony przez nagłówek "X-ServiceFabric".</span><span class="sxs-lookup"><span data-stu-id="b601a-138">If hello service intends toosend a 404 status code back toohello user, it should be accompanied by an "X-ServiceFabric" header.</span></span> <span data-ttu-id="b601a-139">Po zmianie tego, zobaczysz zwrotny serwer proxy przekazuje hello stan kodu wstecz toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="b601a-139">After fixing this, you will see that reverse proxy forwards hello status code back toohello client.</span></span>  

4. <span data-ttu-id="b601a-140">Przypadków, gdy hello klient został odłączony hello żądania.</span><span class="sxs-lookup"><span data-stu-id="b601a-140">Cases when hello client has disconnected hello request.</span></span>

    <span data-ttu-id="b601a-141">Hello poniżej zdarzeń jest rejestrowane, gdy zwrotnego serwera proxy jest przekazywanie hello tooclient odpowiedzi, ale rozłączy powitania klienta:</span><span class="sxs-lookup"><span data-stu-id="b601a-141">hello below event is recorded when reverse proxy is forwarding hello response tooclient but hello client disconnects:</span></span>

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable toosend response tooclient: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
      "ProcessId": 57696,
      "Level": "Warning",
      ...
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8",
        "sendResponsePhase": "SendResponseHeaders",
        "errorval": -805306367,
        "winHttpError": "ERROR_SUCCESS"
      }
    }
    ```

> [!NOTE]
> <span data-ttu-id="b601a-142">Zdarzenia pokrewne toowebsocket żądania przetwarzania nie jest aktualnie zalogowany.</span><span class="sxs-lookup"><span data-stu-id="b601a-142">Events related toowebsocket request processing are not currently logged.</span></span> <span data-ttu-id="b601a-143">Zostanie ona dodana w hello następnej wersji.</span><span class="sxs-lookup"><span data-stu-id="b601a-143">This will be added in hello next release.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b601a-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b601a-144">Next steps</span></span>
* <span data-ttu-id="b601a-145">[Agregacja zdarzeń i kolekcji przy użyciu systemu Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) umożliwiający zbieranie danych dziennika w klastrach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b601a-145">[Event aggregation and collection using Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) for enabling log collection in Azure clusters.</span></span>
* <span data-ttu-id="b601a-146">tooview zdarzenia platformy Service Fabric w programie Visual Studio, zobacz [monitorowanie i diagnozowanie lokalnie](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="b601a-146">tooview Service Fabric events in Visual Studio, see [Monitor and diagnose locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>
* <span data-ttu-id="b601a-147">Odwołuje się zbyt[Konfigurowanie usług toosecure tooconnect zwrotnego serwera proxy](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) dla usługi Azure Resource Manager szablonu przykłady tooconfigure bezpiecznego zwrotny serwer proxy przy użyciu opcji weryfikacji certyfikatu hello w innej usługi.</span><span class="sxs-lookup"><span data-stu-id="b601a-147">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="b601a-148">Odczyt [sieci szkieletowej usług odwrotny serwer proxy](service-fabric-reverseproxy.md) toolearn więcej.</span><span class="sxs-lookup"><span data-stu-id="b601a-148">Read [Service Fabric reverse proxy](service-fabric-reverseproxy.md) toolearn more.</span></span>
