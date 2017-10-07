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
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a>Monitorowanie i diagnozowanie przetwarzania żądania na powitania zwrotnego serwera proxy

Począwszy od wersji hello 5.7 sieci szkieletowej usług, zdarzeń zwrotnego serwera proxy są dostępne dla kolekcji. Witaj zdarzenia są dostępne w dwóch kanałów z tylko zdarzenia błędów pokrewnych błąd przetwarzania toorequest hello zwrotnego serwera proxy i drugi kanał zawierający zdarzenia pełne wpisy dla żądań pomyślnie i niepomyślnie.

Odwołuje się zbyt[zbierania zdarzeń zwrotnego serwera proxy](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable, zbierając zdarzenia z tych kanałów w klastrach sieć szkieletowa usług Azure i lokalnego.

## <a name="troubleshoot-using-diagnostics-logs"></a>Rozwiązywanie problemów przy użyciu dzienników diagnostycznych
Oto kilka przykładów w sposób toointerpret hello wspólnej awarii dzienniki co może wystąpić:

1. Zwrotny serwer proxy zwraca kod stanu odpowiedzi 504 (limit czasu).

    Jedną z przyczyn może być powodu tooreply awaria usługi toohello przed upływem limitu czasu w bazie wiedzy hello żądania.
pierwsze zdarzenie Hello poniżej rejestruje hello szczegóły żądania hello odebraniu hello zwrotnego serwera proxy. Witaj drugie zdarzenie wskazuje Żądanie hello nie powiodło się podczas przekazywania tooservice, właściwym zbyt "Błąd wewnętrzny = ERROR_WINHTTP_TIMEOUT" 

    ładunek Hello obejmuje:

    *  **traceId**: ten identyfikator GUID może być używany toocorrelate wszystkie zdarzenia hello odpowiadającego tooa pojedyncze żądanie. W hello poniżej dwa zdarzenia, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, co oznacza, że należą one toohello jednym żądaniu.
    *  **Adres_url_żądania**: hello adresu URL (adres URL zwrotnego serwera proxy) toowhich hello żądanie zostało wysłane.
    *  **zlecenie**: Zlecenie HTTP.
    *  **remoteAddress**: adres wysyłanie żądania powitania klienta.
    *  **resolvedServiceUrl**: Usługa punktu końcowego adresu URL toowhich hello przychodzące żądanie zostało rozpoznane. 
    *  **Szczegóły błędu**: dodatkowe informacje o niepowodzeniu hello.

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

2. Zwrotny serwer proxy zwraca kod stanu odpowiedzi 404 (nie znaleziono). 
    
    Oto przykład zdarzenia gdzie zwrotny serwer proxy zwraca 404, ponieważ nie może on hello toofind dopasowania punktu końcowego usługi.
    wpisy ładunku Hello zainteresowania w tym miejscu są:
    *  **processRequestPhase**: wskazuje fazy hello podczas przetwarzania żądania wystąpił błąd hello, ***TryGetEndpoint*** tj przy próbie toofetch hello usługi punktu końcowego tooforward do. 
    *  **Szczegóły błędu**: Wyświetla listę kryteriów wyszukiwania hello punktu końcowego. Tutaj można zobaczyć, że listenerName hello określony = **FrontEndListener** listy punktów końcowych hello repliki zawiera tylko odbiornik o nazwie hello **OldListener**.
    
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
    Innym przykładem, gdzie zwrotny serwer proxy może zwrócić 404 Nie znaleziono jest: parametr konfiguracji ApplicationGateway\Http **SecureOnlyMode** ustawiono tootrue zwrotny serwer proxy hello nasłuchiwania na **HTTPS**, Jednak wszystkie punkty końcowe repliki hello są niezabezpieczone (nasłuchiwanie HTTP).
    Odtwarzanie zwraca proxy 404, ponieważ nie można odnaleźć punktu końcowego nasłuchiwania na żądanie hello tooforward HTTPS. Analizowanie parametrów hello w ładunku zdarzenia hello pomaga toonarrow dół hello problemu:
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. Zwrotny serwer proxy toohello żądanie kończy się niepowodzeniem z błędem przekroczenia limitu czasu. 
    dzienniki zdarzeń Hello zawierają zdarzenia z szczegółów żądania hello odebranych (nie jest tutaj widoczny).
    następne zdarzenie Hello pokazuje, że usługa hello zwrócił kod stanu 404 i inicjuje zwrotnego serwera proxy, ponownie rozwiązanie. 

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
    Podczas zbierania wszystkich zdarzeń hello, zostanie wyświetlony train zdarzeń przedstawiający co rozwiązanie, a następnie spróbuj do przodu.
    Ostatnie zdarzenie Hello w serii hello pokazuje hello przetwarzania żądania nie powiodła się z limitem czasu, wraz z hello liczbę prób rozpoznania powiodło się.
    
    > [!NOTE]
    > Go zaleca się tookeep hello pełne kanału zbierania zdarzeń domyślnie wyłączona i włącz ją do rozwiązywania problemów na podstawie potrzeby.

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
    
    Jeśli kolekcji jest włączony dla zdarzeń krytyczny błąd tylko, zobaczysz jednego zdarzenia ze szczegółami hello limitu czasu i liczby hello prób rozpoznania. 
    
    Gdy usługa hello toosend użytkownika wstecz toohello kod stanu 404, powinien być dołączony przez nagłówek "X-ServiceFabric". Po zmianie tego, zobaczysz zwrotny serwer proxy przekazuje hello stan kodu wstecz toohello klienta.  

4. Przypadków, gdy hello klient został odłączony hello żądania.

    Hello poniżej zdarzeń jest rejestrowane, gdy zwrotnego serwera proxy jest przekazywanie hello tooclient odpowiedzi, ale rozłączy powitania klienta:

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
> Zdarzenia pokrewne toowebsocket żądania przetwarzania nie jest aktualnie zalogowany. Zostanie ona dodana w hello następnej wersji.

## <a name="next-steps"></a>Następne kroki
* [Agregacja zdarzeń i kolekcji przy użyciu systemu Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) umożliwiający zbieranie danych dziennika w klastrach platformy Azure.
* tooview zdarzenia platformy Service Fabric w programie Visual Studio, zobacz [monitorowanie i diagnozowanie lokalnie](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).
* Odwołuje się zbyt[Konfigurowanie usług toosecure tooconnect zwrotnego serwera proxy](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) dla usługi Azure Resource Manager szablonu przykłady tooconfigure bezpiecznego zwrotny serwer proxy przy użyciu opcji weryfikacji certyfikatu hello w innej usługi.
* Odczyt [sieci szkieletowej usług odwrotny serwer proxy](service-fabric-reverseproxy.md) toolearn więcej.
