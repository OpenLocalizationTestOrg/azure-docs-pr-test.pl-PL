---
title: "aaaAMQP 1.0 w operacjach opartych na protokole żądanie odpowiedź usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Lista operacji oparte na żądanie/odpowiedź systemu Microsoft Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: e4f26219c53b0c4172747af683fe511d6366ff2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a>Protokołu AMQP 1.0 w systemie Microsoft Azure Service Bus: operacje na podstawie odpowiedzi żądań

W tym temacie opisano hello listę operacji oparte na żądanie/odpowiedź systemu Microsoft Azure Service Bus. Te informacje opiera się na projekt pracy hello protokołu AMQP 1.0 wersji zarządzania.  
  
Szczegółowy poziom danych przesyłanych w sieci protokołu AMQP 1.0 protokołu przewodnik, co wyjaśnia, jak Usługa Service Bus implementuje i opiera się na powitania specyfikacji technicznej OASIS protokołu AMQP, zobacz hello [protokołu AMQP 1.0 w przewodniku protokołu usługi Azure Service Bus i usługi Event Hubs](service-bus-amqp-protocol-guide.md).  
  
## <a name="concepts"></a>Pojęcia  
  
### <a name="entity-description"></a>Opis jednostki  

Opis jednostki odnosi się tooeither usługi Service Bus [klasy QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [klasy TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription), lub [klasy SubscriptionDescription](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) obiektu.  
  
### <a name="brokered-message"></a>Obsługiwane przez brokera komunikatów.  

Reprezentuje komunikat w usłudze Service Bus, czyli komunikat protokołu AMQP tooan mapowane. Mapowanie Hello jest zdefiniowany w hello [przewodnik protokołu AMQP magistrali usługi](service-bus-amqp-protocol-guide.md).  
  
## <a name="attach-tooentity-management-node"></a>Dołącz tooentity węzła zarządzania  

Wszystkie operacje hello w tym dokumencie opisano wykonaj wzorzec żądanie/odpowiedź, są zakresami tooan jednostki i wymagają dołączanie węzła zarządzania tooan jednostki.  
  
### <a name="create-link-for-sending-requests"></a>Utwórz łącze do wysyłania żądań  

Tworzy węzeł zarządzania toohello łącze do wysyłania żądań.  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a>Utwórz łącze do odbierania odpowiedzi  

Tworzy łącze do odbierania odpowiedzi od węzła zarządzania hello.  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a>Komunikat żądania przeniesienia  

Przesyła komunikat żądania.  
  
```  
requestLink.sendTransfer(  
        Message(  
                properties: {  
                        message-id: <request id>,  
                        reply-to: "<my response link unique address>"  
                },  
                application-properties: {  
                        "operation" -> "<operation>",  
                },  
        )  
```  
  
### <a name="receive-a-response-message"></a>Komunikat odpowiedzi  

Odbiera komunikat odpowiedzi hello z hello odpowiedzi łącza.  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
komunikat odpowiedzi Hello znajduje się w hello następującej postaci:
  
```  
Message(  
properties: {     
        correlation-id: <request id>  
    },  
    application-properties: {  
            "statusCode" -> <status code>,  
            "statusDescription" -> <status description>,  
           },         
)  
  
```  
  
### <a name="service-bus-entity-address"></a>Adres jednostki magistrali usług  

Jednostki usługi Service Bus muszą być kierowane w następujący sposób:  
  
|Typ jednostki|Adres|Przykład|  
|-----------------|-------------|-------------|  
|Kolejki|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|Temat|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|subskrypcja|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a>Operacje dotyczące komunikatów  
  
### <a name="message-renew-lock"></a>Komunikat odnowienia blokady  

Rozszerza blokady hello wiadomości powitania czasu określony w opisie jednostki hello.  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
 treść komunikatu żądania Hello musi składać się z sekcji amqp wartość zawierające mapy z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|Tablica uuid|Tak|Komunikat toorenew tokeny blokady.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — Powodzenie, w przeciwnym razie nie powiodło się.|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
treść komunikatu odpowiedzi Hello musi składać się z sekcji amqp wartość zawierające mapy z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|wygasanie|Tablica sygnatury czasowej|Tak|Komunikat blokady token nowego wygaśnięcia odpowiedniego toohello żądania blokady tokenów.|  
  
### <a name="peek-message"></a>Wgląd do wiadomości  

Dokonuje wiadomości bez blokowania.  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|długa|Tak|Numer sekwencji, z których peek toostart.|  
|`message-count`|int|Tak|Maksymalna liczba toopeek wiadomości.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — ma więcej wiadomości<br /><br /> 0xcc: Brak zawartości — dalszych komunikatów|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
Treść wiadomości powitania odpowiedź musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|z chmury do urządzenia|Lista map|Tak|Lista komunikatów, w których każdy mapy reprezentuje komunikat.|  
  
Mapa Hello reprezentujący wiadomości musi zawierać hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Komunikat|Tablica bajtów|Tak|Komunikat protokołu AMQP 1.0 kodowany w formacie danych przesyłanych w sieci.|  
  
### <a name="schedule-message"></a>Komunikat harmonogramu  

Planuje wiadomości.  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|z chmury do urządzenia|Lista map|Tak|Lista komunikatów, w których każdy mapy reprezentuje komunikat.|  
  
Mapa Hello reprezentujący wiadomości musi zawierać hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Identyfikator komunikatu|Ciąg|Tak|`amqpMessage.Properties.MessageId`jako ciąg|  
|Identyfikator sesji|Ciąg|Tak|`amqpMessage.Properties.GroupId as string`|  
|Klucz partycji|Ciąg|Tak|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|Komunikat|Tablica bajtów|Tak|Komunikat protokołu AMQP 1.0 kodowany w formacie danych przesyłanych w sieci.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — Powodzenie, w przeciwnym razie nie powiodło się.|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
Treść wiadomości powitania odpowiedź musi składać się z **amqp wartość** sekcji zawierającej mapy z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|numerów sekwencji.|Tablica long|Tak|Numer sekwencyjny zaplanowane wiadomości. Numer sekwencji jest używany toocancel.|  
  
### <a name="cancel-scheduled-message"></a>Anulowanie zaplanowanego wiadomości  

Anuluje zaplanowane wiadomości.  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|numerów sekwencji.|Tablica long|Tak|Numery sekwencji toocancel zaplanowane wiadomości.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — Powodzenie, w przeciwnym razie nie powiodło się.|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
Treść wiadomości powitania odpowiedź musi składać się z **amqp wartość** sekcji zawierającej mapy z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|numerów sekwencji.|Tablica long|Tak|Numer sekwencyjny zaplanowane wiadomości. Numer sekwencji jest używany toocancel.|  
  
## <a name="session-operations"></a>Operacje sesji  
  
### <a name="session-renew-lock"></a>Sesja odnawiania blokady  

Rozszerza blokady hello wiadomości powitania czasu określony w opisie jednostki hello.  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Identyfikator sesji|Ciąg|Tak|Identyfikator sesji.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — ma więcej wiadomości<br /><br /> 0xcc: Brak zawartości — dalszych komunikatów|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
Treść wiadomości powitania odpowiedź musi składać się z **amqp wartość** sekcji zawierającej mapy z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|wygaśnięcia|sygnatura czasowa|Tak|Nowe wygaśnięcia.|  
  
### <a name="peek-session-message"></a>Wgląd do wiadomości sesji  

Dokonuje komunikaty sesji bez blokowania.  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|od-— numer sekwencji|długa|Tak|Numer sekwencji, z których peek toostart.|  
|Liczba komunikatów|int|Tak|Maksymalna liczba toopeek wiadomości.|  
|Identyfikator sesji|Ciąg|Tak|Identyfikator sesji.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — ma więcej wiadomości<br /><br /> 0xcc: Brak zawartości — dalszych komunikatów|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
Treść wiadomości powitania odpowiedź musi składać się z **amqp wartość** sekcji zawierającej mapy z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|z chmury do urządzenia|Lista map|Tak|Lista komunikatów, w których każdy mapy reprezentuje komunikat.|  
  
 Mapa Hello reprezentujący wiadomości musi zawierać hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Komunikat|Tablica bajtów|Tak|Komunikat protokołu AMQP 1.0 kodowany w formacie danych przesyłanych w sieci.|  
  
### <a name="set-session-state"></a>Ustaw stan sesji  

Ustawia hello stanu sesji.  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Identyfikator sesji|Ciąg|Tak|Identyfikator sesji.|  
|Stan sesji|Tablica bajtów|Tak|Nieprzezroczysta danych binarnych.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — Powodzenie, w przeciwnym razie nie powiodło się|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
### <a name="get-session-state"></a>Pobierz stan sesji  

Pobiera stan hello sesji.  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Identyfikator sesji|Ciąg|Tak|Identyfikator sesji.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — Powodzenie, w przeciwnym razie nie powiodło się|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
Treść wiadomości powitania odpowiedź musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Stan sesji|Tablica bajtów|Tak|Nieprzezroczysta danych binarnych.|  
  
### <a name="enumerate-sessions"></a>Wyliczenie sesji  

Wylicza sesji na jednostki obsługi komunikatów.  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|ostatnio zaktualizowano czasu|sygnatura czasowa|Tak|Filtr tooinclude sesji tylko zaktualizowane po określonym czasie.|  
|Pomiń|int|Tak|Pomiń liczbę sesji.|  
|Do góry|int|Tak|Maksymalna liczba sesji.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — ma więcej wiadomości<br /><br /> 0xcc: Brak zawartości — dalszych komunikatów|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
Treść wiadomości powitania odpowiedź musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Pomiń|int|Tak|Liczba pominiętych sesji w przypadku kodu stanu 200.|  
|identyfikatory sesji|Tablica ciągów|Tak|Tablica sesji identyfikatory przypadku kodu stanu 200.|  
  
## <a name="rule-operations"></a>Reguły operacji  
  
### <a name="add-rule"></a>Dodaj regułę  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Nazwa reguły|Ciąg|Tak|Nazwa reguły nie tym nazwy subskrypcji i tematu.|  
|Opis reguły|mapy|Tak|Opis reguły określone w następnej sekcji.|  
  
Witaj **opis reguły** Mapa musi zawierać hello następujące wpisy, gdzie **filtrem sql** i **filtru korelacji** wykluczają się wzajemnie:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Filtr programu SQL|mapy|Tak|`sql-filter`, jak określono w następnej sekcji hello.|  
|Filtr korelacji|mapy|Tak|`correlation-filter`, jak określono w następnej sekcji hello.|  
|Akcja SQL reguły|mapy|Tak|`sql-rule-action`, jak określono w następnej sekcji hello.|  
  
Mapa filtrem sql Hello musi zawierać hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|wyrażenie|Ciąg|Tak|Wyrażenie filtru SQL.|  
  
Witaj **filtru korelacji** Mapa musi zawierać co najmniej jeden z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Identyfikator korelacji|Ciąg|Nie||  
|Identyfikator komunikatu|Ciąg|Nie||  
|na|Ciąg|Nie||  
|Odpowiedz do|Ciąg|Nie||  
|Etykiety|Ciąg|Nie||  
|Identyfikator sesji|Ciąg|Nie||  
|Odpowiedz do sesji id|Ciąg|Nie||  
|Typ zawartości|Ciąg|Nie||  
|properties|mapy|Nie|Mapuje tooService magistrali [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties).|  
  
Witaj **sql reguły akcji** Mapa musi zawierać hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|wyrażenie|Ciąg|Tak|Wyrażenie akcji SQL.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — Powodzenie, w przeciwnym razie nie powiodło się|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
### <a name="remove-rule"></a>Usuń regułę  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Nazwa reguły|Ciąg|Tak|Nazwa reguły nie tym nazwy subskrypcji i tematu.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — Powodzenie, w przeciwnym razie nie powiodło się|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
## <a name="deferred-message-operations"></a>Operacje dotyczące komunikatów odroczone  
  
### <a name="receive-by-sequence-number"></a>Odbieranie numerem sekwencji  

Odbiera komunikaty odroczonego numerem sekwencji.  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|numerów sekwencji.|Tablica long|Tak|Numerów sekwencji.|  
|odbiornik rozliczania trybu|ubyte|Tak|**Odbiornik rozliczania** tryb zgodnie z protokołu AMQP 1.0 core.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — Powodzenie, w przeciwnym razie nie powiodło się|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|  
  
Treść wiadomości powitania odpowiedź musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|z chmury do urządzenia|Lista map|Tak|Lista komunikatów, gdzie każdy mapy reprezentuje komunikat.|  
  
Mapa Hello reprezentujący wiadomości musi zawierać hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|token blokady|Identyfikator UUID|Tak|Jeśli token blokady `receiver-settle-mode` 1.|  
|Komunikat|Tablica bajtów|Tak|Komunikat protokołu AMQP 1.0 kodowany w formacie danych przesyłanych w sieci.|  
  
### <a name="update-disposition-status"></a>Aktualizacja stanu dyspozycji  

Aktualizuje stan dyspozycji hello odroczonego wiadomości.  
  
#### <a name="request"></a>Żądanie  

komunikat żądania Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Operacja|Ciąg|Tak|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|uint|Nie|Limit czasu operacji serwera w milisekundach.|  
  
treść komunikatu żądania Hello musi składać się z **wartość amqp** sekcji zawierającej **mapy** z hello następujące wpisy:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|Stan dyspozycji|Ciąg|Tak|ukończone<br /><br /> porzucone<br /><br /> Zawieszone|  
|tokeny blokady|Tablica uuid|Tak|Tooupdate stan dyspozycji komunikat blokady tokenów.|  
|Przyczyna utraconych wiadomości|Ciąg|Nie|Może ustawić, jeśli ustawiono stan dyspozycji za**zawieszone**.|  
|Opis utraconych wiadomości|Ciąg|Nie|Może ustawić, jeśli ustawiono stan dyspozycji za**zawieszone**.|  
|właściwości modyfikować|mapy|Nie|Wykaz usługi Service Bus obsługiwanych przez brokera toomodify właściwości komunikatu.|  
  
#### <a name="response"></a>Odpowiedź  

komunikat odpowiedzi Hello musi zawierać następujące właściwości aplikacji hello:  
  
|Klucz|Typ wartości|Wymagane|Wartość zawartości|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Tak|Kod odpowiedzi HTTP [specyfikacją RFC2616]<br /><br /> 200: OK — Powodzenie, w przeciwnym razie nie powiodło się|  
|StatusDescription|Ciąg|Nie|Opis stanu hello.|

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat protokołu AMQP i usługi Service Bus, odwiedź hello następującego łącza:

* [Omówienie protokołu AMQP magistrali usług]
* [Obsługa protokołu AMQP 1.0 tematów i kolejek usługi Service Bus na partycje]
* [Protokół AMQP w usłudze Service Bus dla systemu Windows Server]

[Omówienie protokołu AMQP magistrali usług]: service-bus-amqp-overview.md
[Obsługa protokołu AMQP 1.0 tematów i kolejek usługi Service Bus na partycje]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Protokół AMQP w usłudze Service Bus dla systemu Windows Server]: https://msdn.microsoft.com/library/dn574799.asp