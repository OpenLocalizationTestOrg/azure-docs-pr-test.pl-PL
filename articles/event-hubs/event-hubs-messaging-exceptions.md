---
title: "Centra zdarzeń aaaAzure wiadomości wyjątki | Dokumentacja firmy Microsoft"
description: "Lista wyjątków i sugerowane rozwiązania do obsługi komunikatów usługi Azure Event hubs."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2c6273de-0106-47e5-b45d-59040e51f2c5
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 9c164e76612c26607219f08407f689aaab4050a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-messaging-exceptions"></a>Wyjątki obsługi komunikatów w usłudze Event Hubs
W tym artykule wymieniono niektóre hello wyjątków generowanych przez hello Azure Service Bus wiadomości interfejsów API, które obejmują usługi Event Hubs. To odwołanie jest toochange podmiotu, dlatego sprawdzanie dostępności aktualizacji.

## <a name="exception-categories"></a>Kategorie wyjątku
Witaj interfejsów API centra zdarzeń generować wyjątki, które można podzielić na następujące kategorie hello, wraz z hello skojarzonych akcji może zająć tootry toofix je.

1. Kodowanie błąd użytkownika: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [ System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). Akcja ogólne: spróbuj kodu hello toofix przed kontynuowaniem.
2. Błąd instalacji/konfiguracji: [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception), [ System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Akcja ogólne: Przejrzyj konfigurację i w razie potrzeby zmień.
3. Wyjątki przejściowej: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](#serverbusyexception), [ Microsoft.Azure.EventHubs.ServerBusyException](#serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). Akcja ogólne: ponów próbę wykonania operacji hello lub powiadomić użytkowników.
4. Pozostałe wyjątki: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](#timeoutexception), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception). Akcja ogólne: toohello określonego typu wyjątku; można znaleźć w tabeli toohello w hello następujących sekcji. 

## <a name="exception-types"></a>Typy wyjątków
Witaj poniższej tabeli wymieniono obsługi typów wyjątków i ich przyczyny i zalecane działanie uwagi, które można wykonać.

| **Typ wyjątku** | **Opis elementu/Przyczyna/przykłady** | **Zalecane działanie** | **Należy zwrócić uwagę na automatyczne/natychmiastowego ponawiania** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Witaj serwer nie odpowiedział toohello żądanej operacji w ramach hello określony czas, który jest kontrolowany przez [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). powitania serwera mogło ukończyć powitalnych żądanej operacji. Może to nastąpić z powodu toonetwork lub innych opóźnienia infrastruktury. |Sprawdź stan systemu hello spójności, a następnie spróbuj ponownie w razie potrzeby.<br /> Zobacz [TimeoutException](#timeoutexception). |Ponów próbę, może pomóc w niektórych przypadkach; Dodaj toocode logiki ponawiania. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Witaj zażądał operacji użytkownika nie jest dozwolone w ramach powitania serwera lub usługi. Zawiera komunikat wyjątku hello, aby uzyskać szczegółowe informacje. Na przykład [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) generuje ten wyjątek, jeśli wiadomość hello została odebrana w [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) tryb. |Sprawdź kod hello i hello dokumentacji. Upewnij się, że hello Żądana operacja jest prawidłowa. |Nie pomoże ponów próbę. |
| [Operationcanceledexception —](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Próba wprowadzone tooinvoke operacji na obiekcie, który już został zamknięty, przerwana lub usunięty. W rzadkich przypadkach transakcja otoczenia hello zostało już usunięte. |Sprawdź kod hello i upewnij się, że nie jest wywoływany operacji na usuniętym obiekcie. |Nie pomoże ponów próbę. |
| [Unauthorizedaccessexception —](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Witaj [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) obiektu nie można uzyskać tokenu, hello token jest nieprawidłowy lub hello token nie zawiera hello oświadczenia wymagane tooperform hello operacji. |Upewnij się, że dostawca tokenów hello jest tworzony z hello poprawne wartości. Sprawdź konfigurację hello hello usługi kontroli dostępu. |Ponów próbę, może pomóc w niektórych przypadkach; Dodaj toocode logiki ponawiania. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [Argumentnullexception —](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Co najmniej jeden metody toohello dostarczone argumenty są nieprawidłowe. Witaj identyfikator URI dostarczony zbyt[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) lub [Utwórz](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) zawiera następującą liczbę segmentów ścieżki. schemat identyfikatora URI Hello dostarczane za[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) lub [Utwórz](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) jest nieprawidłowy. wartość właściwości Hello jest większy niż 32KB. |Sprawdź kod wywołujący hello i upewnij się, że argumenty hello są poprawne. |Nie pomoże ponów próbę. |
| [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) <br /> [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception) |Skojarzone z operacją hello jednostka nie istnieje lub została usunięta. |Upewnij się, że istnieje hello jednostki. |Nie pomoże ponów próbę. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Próba tooreceive wiadomość z liczbą określonej sekwencji. Ta wiadomość nie została znaleziona. |Upewnij się, że wiadomość hello nie zostały jeszcze odebrane. Sprawdź toosee kolejki utraconych wiadomości powitania, jeśli wiadomość hello został deadlettered. |Nie pomoże ponów próbę. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Klient nie jest w stanie tooestablish tooEvent połączenia koncentratora. |Upewnij się, nazwy hosta dostarczone hello jest poprawna i hello host jest dostępny. |Ponów próbę mogą ułatwić, jeśli występują problemy z łącznością sporadyczne. |
| [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) <br /> [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) |Usługa nie jest możliwe tooprocess hello żądania w tej chwili. |Klient może czekać przez czas, a następnie ponów próbę wykonania operacji hello. <br /> Zobacz [ServerBusyException](#serverbusyexception). |Klient może podjąć kolejną próbę po niektórych interwału. Jeśli ponowna próba powoduje różnych wyjątek, sprawdź zachowanie ponów próbę wykonania tego wyjątku. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Token blokady skojarzony z wiadomość hello wygasł lub nie znaleziono hello token blokady. |Usuwanie wiadomości powitania. |Nie pomoże ponów próbę. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Zablokuj skojarzone z tą sesją zostaną utracone. | Przerwij hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) obiektu. |Nie pomoże ponów próbę. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Ogólny wiadomości wyjątek, który może zostać zgłoszony w hello w następujących przypadkach: toocreate podejmowana jest próba [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) za pomocą nazwy lub ścieżki, którego należy typ jednostki różnych tooa (na przykład tematu). Próba wprowadzone toosend wiadomości większych niż 256KB. Serwer Hello lub Usługa napotkała błąd podczas przetwarzania żądania hello. Zobacz hello komunikat wyjątku, aby uzyskać szczegółowe informacje. Zwykle jest to przejściowy wyjątku. |Sprawdź kod hello i upewnij się, że wiadomość hello są używane tylko obiekty możliwe do serializacji lub użyć serializatora niestandardowego. Dokumentacji hello hello obsługiwane typy wartości właściwości hello i tylko Użyj obsługiwane typy. Sprawdź hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) właściwości. Jeśli jest **true**, możesz ponowić próbę operacji hello. |Ponów próbę zachowanie nie jest zdefiniowana i nie może pomóc. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Próba toocreate jednostki o nazwie, która jest już używana przez inną jednostkę w tej przestrzeni nazw usługi. |Usuń hello istniejącej jednostki lub wybierz inną nazwę dla toobe jednostki hello utworzony. |Nie pomoże ponów próbę. |
| [Quotaexceededexception —](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Witaj jednostki do obsługi komunikatów osiągnęła maksymalny dozwolony rozmiar. Może to nastąpić, jeśli hello maksymalną liczbę odbiorników (czyli 5) został już otwarty na poziomie grupy dla użytkownika. |Utwórz miejsca w jednostce hello przez odbieranie wiadomości z jednostki hello lub jego podrzędnej kolejki. <br /> Zobacz [quotaexceededexception —](#quotaexceededexception) |Ponów próbę mogą ułatwić czy wiadomości zostały usunięte w hello czasu. |
|  | | | |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Próba tooaccept, który sesji o identyfikatorze określonej sesji, ale sesja hello jest zablokowany przez innego klienta. |Upewnij się, że sesja hello jest odblokowany przez innych klientów. |Ponów próbę mogą ułatwić Jeżeli hello sesji zostało zwolnione w hello tymczasowe. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Zbyt wiele operacji są częścią hello transakcji. |Ogranicz liczbę hello działań, które są częścią tej transakcji. |Nie pomoże ponów próbę. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Żądanie operacji środowiska uruchomieniowego w jednostce wyłączone. |Aktywuj hello jednostki. |Ponów próbę mogą ułatwić Jeśli hello jednostki został aktywowany w hello tymczasowe. |
| [Microsoft.ServiceBus.Messaging.MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) <br /> [Microsoft.Azure.EventHubs.MessageSizeExceededException](/dotnet/api/microsoft.azure.eventhubs.messagesizeexceededexception) | Ładunek komunikatu przekracza limit hello 256 KB. Należy zauważyć, że ten limit 256 KB hello jest rozmiaru całkowita liczba wiadomości powitania, który może zawierać żadnych czynności .NET i właściwości systemu. |Zmniejsz rozmiar hello ładunku wiadomość hello, a następnie ponów próbę wykonania operacji hello. |Nie pomoże ponów próbę. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Witaj transakcja otoczenia (*Transaction.Current*) jest nieprawidłowy. Może została wykonana lub zostało przerwane. Wyjątek wewnętrzny może zawierać dodatkowe informacje. | |Nie pomoże ponów próbę. |
| [Transactionindoubtexception —](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Nastąpi próba wykonania operacji transakcji, który znajduje się w razie wątpliwości lub transakcji hello toocommit podejmowana jest próba i transakcji hello staje się wątpliwe. |Aplikacja musi obsługiwać tego wyjątku (jako szczególnych przypadkach), jak transakcji hello mogła już zostać zatwierdzone. |- |

## <a name="quotaexceededexception"></a>Quotaexceededexception —
[Quotaexceededexception —](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) wskazuje, że przekroczono limit przydziału dla określonej jednostki.

Może to nastąpić, jeśli hello maksymalną liczbę odbiorników [5] został już otwarty na poziomie grupy dla użytkownika.

### <a name="event-hubs"></a>Usługa Event Hubs
Centra zdarzeń ma limit 20 grup odbiorców, na Centrum zdarzeń. Podczas próby toocreate więcej pojawi się [quotaexceededexception —](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) wskazuje, że użytkownik zainicjował operację trwa dłużej niż limit czasu operacji hello. 

Usługi Event hubs hello limitu czasu jest określony jako część ciągu połączenia hello lub za pośrednictwem [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). komunikat o błędzie Hello, się różnić, ale zawsze zawiera wartość limitu czasu hello hello bieżącej operacji. 

### <a name="common-causes"></a>Typowe przyczyny
Istnieją dwie typowe przyczyny tego błędu: nieprawidłowa konfiguracja lub Błąd przejściowy usługi.

1. **Nieprawidłowa konfiguracja** hello limit czasu operacji może być za mała dla wartości hello warunki operacyjne. Domyślna wartość Limit czasu operacji hello powitania klienta SDK Hello wynosi 60 sekund. Sprawdź, czy toosee, jeśli kod ma wartość hello ustawić toosomething za mały. Zanotuj tego warunku hello hello sieci i użycie Procesora może mieć wpływ na powitania czas dla toocomplete określonej operacji, więc limit czasu operacji hello nie powinien mieć ustawionej bardzo mała wartość tooa.
2. **Błąd przejściowy usługi** hello czasami usługi Event Hubs mogą występować opóźnienia podczas przetwarzania żądań, na przykład w okresach dużego natężenia ruchu sieciowego. W takich przypadkach możesz ponowić operację z opóźnieniem, aż operacja hello zakończy się powodzeniem. Jeśli hello tej samej operacji nadal nie powiedzie się po wielu próbach, odwiedź stronę hello [lokacji stanu usługi Azure](https://azure.microsoft.com/status/) toosee, jeśli występują awarie wszystkie znane usługi.

## <a name="serverbusyexception"></a>ServerBusyException

A [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) lub [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) wskazuje, że serwer jest przeciążony. Istnieją dwa kody błędów odpowiednie dla tego wyjątku.

### <a name="error-code-50002"></a>Kod błędu 50002

Ten błąd może wystąpić z jednej z dwóch przyczyn:

1. obciążenia Hello nie jest równomiernie rozłożona wszystkie partycje na powitania Centrum zdarzeń i jedną partycję trafień hello przepływności lokalnej jednostki ograniczenia.
    
    Rozwiązanie: Zmiana strategii dystrybucji partycji hello lub w trakcie [EventHubClient.Send(eventDataWithOutPartitionKey)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) może pomóc.

2. Witaj centra zdarzeń w przestrzeni nazw nie ma wystarczających jednostek przepływności (można sprawdzić hello **metryki** bloku w bloku przestrzeni nazw usługi Event Hubs w hello [portalu Azure](https://portal.azure.com) tooconfirm). Należy pamiętać, hello portal pokazuje zagregowane (1 minuta) informacje, że firma Microsoft mierzenia przepływności hello w czasie rzeczywistym — tak aby zawierała tylko szacowania.

    Rozwiązanie: Zwiększyć przepustowość hello, jednostki w przestrzeni nazw hello może pomóc. Można to zrobić na powitania portal hello **skali** bloku hello centra zdarzeń w przestrzeni nazw bloku.

### <a name="error-code-50001"></a>Kod błędu 50001

Ten błąd powinny występować rzadko. Występuje, jeśli hello kontener uruchamianie kodu przestrzeni nazw ma za mało procesora CPU — załadować centra zdarzeń w nie więcej niż kilka sekund przed hello zaczyna równoważenia.


## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)
* [Tworzenie centrum zdarzeń](event-hubs-create.md)
* [Event Hubs — często zadawane pytania](event-hubs-faq.md)
