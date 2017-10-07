---
title: "Wyjątki obsługi komunikatów usługi Service Bus aaaAzure | Dokumentacja firmy Microsoft"
description: "Lista wyjątki obsługi komunikatów usługi Service Bus i wyświetlić sugerowane akcje."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3d8526fe-6e47-4119-9f3e-c56d916a98f9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: sethm
ms.openlocfilehash: 0a206b7bbc808c1190044c1dfd6ffd47b9d454fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-exceptions"></a>Wyjątki obsługi komunikatów w usłudze Service Bus
W tym artykule wymieniono niektóre wyjątki generowane przez hello Microsoft Azure Service Bus interfejsów API do obsługi komunikatów. To odwołanie jest toochange podmiotu, dlatego sprawdzanie dostępności aktualizacji.

## <a name="exception-categories"></a>Kategorie wyjątku
Witaj interfejsów API obsługi komunikatów generowania wyjątków, które można podzielić na następujące kategorie hello, wraz z hello skojarzonych akcji może zająć tootry toofix je. Należy pamiętać, że hello znaczenie i przyczyny wyjątek może się różnić w zależności od typu hello jednostki obsługi komunikatów (kolejki/tematy lub Event Hubs):

1. Błąd kodowania użytkownika ([System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx)). Akcja ogólne: spróbuj kodu hello toofix przed kontynuowaniem.
2. Błąd instalacji/konfiguracji ([Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Akcja ogólne: Przejrzyj konfigurację i w razie potrzeby zmień.
3. Wyjątki przejściowy ([Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)). Akcja ogólne: ponów próbę wykonania operacji hello lub powiadomić użytkowników.
4. Pozostałe wyjątki ([System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception)). Akcja ogólne: toohello określonego typu wyjątku; można znaleźć w tabeli toohello w hello następujących sekcji. 

## <a name="exception-types"></a>Typy wyjątków
Witaj poniższej tabeli wymieniono obsługi typów wyjątków i ich przyczyny i zalecane działanie uwagi, które można wykonać.

| **Typ wyjątku** | **Opis elementu/Przyczyna/przykłady** | **Zalecane działanie** | **Należy zwrócić uwagę na automatyczne/natychmiastowego ponawiania** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Witaj serwer nie odpowiedział toohello żądanej operacji w ramach hello określony czas, który jest kontrolowany przez [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). powitania serwera mogło ukończyć powitalnych żądanej operacji. Może to nastąpić z powodu toonetwork lub innych opóźnienia infrastruktury. |Sprawdź stan systemu hello spójności, a następnie spróbuj ponownie w razie potrzeby. Zobacz [wyjątków przekroczenia limitu czasu](#timeoutexception). |Ponów próbę, może pomóc w niektórych przypadkach; Dodaj toocode logiki ponawiania. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Witaj zażądał operacji użytkownika nie jest dozwolone w ramach powitania serwera lub usługi. Zawiera komunikat wyjątku hello, aby uzyskać szczegółowe informacje. Na przykład [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) wygeneruje ten wyjątek, jeśli wiadomość hello została odebrana w [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) tryb. |Sprawdź kod hello i hello dokumentacji. Upewnij się, że hello Żądana operacja jest prawidłowa. |Nie pomoże ponów próbę. |
| [Operationcanceledexception —](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Próba wprowadzone tooinvoke operacji na obiekcie, który już został zamknięty, przerwana lub usunięty. W rzadkich przypadkach transakcja otoczenia hello zostało już usunięte. |Sprawdź kod hello i upewnij się, że nie jest wywoływany operacji na usuniętym obiekcie. |Nie pomoże ponów próbę. |
| [Unauthorizedaccessexception —](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Witaj [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) obiektu nie można uzyskać tokenu, hello token jest nieprawidłowy lub hello token nie zawiera hello oświadczenia wymagane tooperform hello operacji. |Upewnij się, że dostawca tokenów hello jest tworzony z hello poprawne wartości. Sprawdź konfigurację hello hello usługi kontroli dostępu. |Ponów próbę, może pomóc w niektórych przypadkach; Dodaj toocode logiki ponawiania. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [Argumentnullexception —](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Co najmniej jeden metody toohello dostarczone argumenty są nieprawidłowe.<br /> Witaj identyfikator URI dostarczony zbyt[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) lub [Utwórz](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) zawiera następującą liczbę segmentów ścieżki.<br /> schemat identyfikatora URI Hello dostarczane za[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) lub [Utwórz](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) jest nieprawidłowy. <br />wartość właściwości Hello jest większy niż 32KB. |Sprawdź kod wywołujący hello i upewnij się, że argumenty hello są poprawne. |Nie pomoże ponów próbę. |
| [MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) |Skojarzone z operacją hello jednostka nie istnieje lub została usunięta. |Upewnij się, że istnieje hello jednostki. |Nie pomoże ponów próbę. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Próba tooreceive wiadomość z liczbą określonej sekwencji. Ta wiadomość nie została znaleziona. |Upewnij się, że wiadomość hello nie zostały jeszcze odebrane. Sprawdź toosee kolejki utraconych wiadomości powitania, jeśli wiadomość hello został deadlettered. |Nie pomoże ponów próbę. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Klient nie jest w stanie tooestablish tooService połączenia magistrali. |Upewnij się, nazwy hosta dostarczone hello jest poprawna i hello host jest dostępny. |Ponów próbę mogą ułatwić, jeśli występują problemy z łącznością sporadyczne. |
| [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Usługa nie jest możliwe tooprocess hello żądania w tej chwili. |Klient może czekać przez czas, a następnie ponów próbę wykonania operacji hello. |Klient może podjąć kolejną próbę po niektórych interwału. Jeśli ponowna próba powoduje różnych wyjątek, sprawdź zachowanie ponów próbę wykonania tego wyjątku. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Token blokady skojarzony z wiadomość hello wygasł lub nie znaleziono hello token blokady. |Usuwanie wiadomości powitania. |Nie pomoże ponów próbę. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Zablokuj skojarzone z tą sesją zostaną utracone. |Przerwij hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) obiektu. |Nie pomoże ponów próbę. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Ogólny wiadomości wyjątek, który może zostać zgłoszony w hello w następujących przypadkach:<br /> Toocreate podejmowana jest próba [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) za pomocą nazwy lub ścieżki, którego należy typ jednostki różnych tooa (na przykład tematu).<br />  Próba wprowadzone toosend wiadomości większych niż 256KB. Serwer Hello lub Usługa napotkała błąd podczas przetwarzania żądania hello. Zobacz hello komunikat wyjątku, aby uzyskać szczegółowe informacje. Zwykle jest to przejściowy wyjątku. |Sprawdź kod hello i upewnij się, że wiadomość hello są używane tylko obiekty możliwe do serializacji lub użyć serializatora niestandardowego. Dokumentacji hello hello obsługiwane typy wartości właściwości hello i tylko Użyj obsługiwane typy. Sprawdź hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) właściwości. Jeśli jest **true**, możesz ponowić próbę operacji hello. |Ponów próbę zachowanie nie jest zdefiniowana i nie może pomóc. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Próba toocreate jednostki o nazwie, która jest już używana przez inną jednostkę w tej przestrzeni nazw usługi. |Usuń hello istniejącej jednostki lub wybierz inną nazwę dla toobe jednostki hello utworzony. |Nie pomoże ponów próbę. |
| [Quotaexceededexception —](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Witaj jednostki do obsługi komunikatów osiągnęła maksymalny dopuszczalny rozmiar lub przekroczono maksymalną liczbę połączeń tooa nazw hello. |Utwórz miejsca w jednostce hello przez odbieranie wiadomości z jednostki hello lub jego podrzędnej kolejki. Zobacz [quotaexceededexception —](#quotaexceededexception). |Ponów próbę mogą ułatwić czy wiadomości zostały usunięte w hello czasu. |
| [RuleActionException](/dotnet/api/microsoft.servicebus.messaging.ruleactionexception) |Usługi Service Bus zwraca ten wyjątek, jeśli próba toocreate akcji nieprawidłową zasadę. Usługa Service Bus dołącza ten komunikat o wyjątku tooa deadlettered, jeśli wystąpi błąd podczas przetwarzania hello Akcja reguły dla tej wiadomości. |Sprawdź Akcja reguły hello pod kątem poprawności. |Nie pomoże ponów próbę. |
| [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) |Usługi Service Bus zwraca ten wyjątek, jeśli próba toocreate nieprawidłowy filtr. Usługa Service Bus dołącza ten komunikat o wyjątku tooa deadlettered, jeśli wystąpił błąd podczas przetwarzania hello filtru dla tego komunikatu. |Filtr hello sprawdzania pod kątem poprawności. |Nie pomoże ponów próbę. |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Próba tooaccept, który sesji o identyfikatorze określonej sesji, ale sesja hello jest zablokowany przez innego klienta. |Upewnij się, że sesja hello jest odblokowany przez innych klientów. |Ponów próbę mogą ułatwić Jeżeli hello sesji zostało zwolnione w hello tymczasowe. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Zbyt wiele operacji są częścią hello transakcji. |Ogranicz liczbę hello działań, które są częścią tej transakcji. |Nie pomoże ponów próbę. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Żądanie operacji środowiska uruchomieniowego w jednostce wyłączone. |Aktywuj hello jednostki. |Ponów próbę mogą ułatwić Jeśli hello jednostki został aktywowany w hello tymczasowe. |
| [NoMatchingSubscriptionException](/dotnet/api/microsoft.servicebus.messaging.nomatchingsubscriptionexception) |Usługa Service Bus zwraca tego wyjątku w przypadku wysłania temat tooa komunikat, który ma wstępnie Filtrowanie włączone i żadna hello filtrów nie zgadza się. |Upewnij się, że co najmniej jeden filtr jest zgodna. |Nie pomoże ponów próbę. |
| [MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Ładunek komunikatu przekracza limit 256 KB hello. Należy zauważyć, że ten limit 256 KB hello jest rozmiaru całkowita liczba wiadomości powitania, który może zawierać żadnych czynności .NET i właściwości systemu. |Zmniejsz rozmiar hello ładunku wiadomość hello, a następnie ponów próbę wykonania operacji hello. |Nie pomoże ponów próbę. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Witaj transakcja otoczenia (*Transaction.Current*) jest nieprawidłowy. Może została wykonana lub zostało przerwane. Wyjątek wewnętrzny może zawierać dodatkowe informacje. | |Nie pomoże ponów próbę. |
| [Transactionindoubtexception —](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Nastąpi próba wykonania operacji transakcji, który znajduje się w razie wątpliwości lub transakcji hello toocommit podejmowana jest próba i transakcji hello staje się wątpliwe. |Aplikacja musi obsługiwać tego wyjątku (jako szczególnych przypadkach), jak transakcji hello mogła już zostać zatwierdzone. |- |

## <a name="quotaexceededexception"></a>Quotaexceededexception —
[Quotaexceededexception —](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) wskazuje, że przekroczono limit przydziału dla określonej jednostki.

### <a name="queues-and-topics"></a>Kolejki i tematy
W przypadku kolejek i tematów często jest hello rozmiar kolejki hello. Właściwość wiadomości powitania błędu będzie zawierać dodatkowe szczegóły, jak hello poniższy przykład:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException
Message: hello maximum entity size has been reached or exceeded for Topic: ‘xxx-xxx-xxx’. 
    Size of entity in bytes:1073742326, Max entity size in bytes:
1073741824..TrackingId:xxxxxxxxxxxxxxxxxxxxxxxxxx, TimeStamp:3/15/2013 7:50:18 AM
```

wiadomości powitania informacją, że ten temat hello przekracza limit rozmiaru, w tym wielkości 1 GB (hello domyślnego limitu rozmiaru). 

### <a name="namespaces"></a>Przestrzenie nazw

W przypadku przestrzeni nazw [quotaexceededexception —](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) może oznaczać, że aplikacji przekroczył maksymalną liczbę połączeń tooa nazw hello. Na przykład:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException: ConnectionsQuotaExceeded for namespace xxx.
<tracking-id-guid>_G12 ---> 
System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: 
ConnectionsQuotaExceeded for namespace xxx.
```

#### <a name="common-causes"></a>Typowe przyczyny
Istnieją dwie typowe przyczyny tego błędu: hello kolejki utraconych wiadomości i niedziałającej odbiorcy wiadomości.

1. **Kolejki utraconych wiadomości** czytnik kończy się niepowodzeniem toocomplete komunikaty i wiadomości powitania są zwracane toohello kolejki/tematu, po wygaśnięciu hello blokady. Może się to zdarzyć, jeśli czytnik hello napotkał wyjątek, który uniemożliwia wywołanie [BrokeredMessage.Complete](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.complete.aspx). Po komunikat został odczytany 10 razy, przenosi kolejki utraconych wiadomości toohello domyślnie. To zachowanie jest kontrolowany przez hello [QueueDescription.MaxDeliveryCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.maxdeliverycount.aspx) właściwości i ma wartość domyślną równą 10. Jak komunikaty Ustawianie kolejki utraconych wiadomości powitania, zajmują miejsce.
   
    problem hello tooresolve, hello odczytu i pełne komunikaty z kolejki utraconych wiadomości powitania, jako użytkownik będzie z innych kolejki. Witaj [QueueClient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.aspx) klasa nawet zawiera [FormatDeadLetterPath](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.formatdeadletterpath.aspx) metody toohelp format hello kolejki utraconych wiadomości ścieżki.
2. **Odbiornik zatrzymana** odbiornik została zatrzymana, odbierania wiadomości z kolejki lub subskrypcji. Witaj tooidentify sposób jest toolook na powitania [QueueDescription.MessageCountDetails](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.messagecountdetails.aspx) właściwość, która przedstawia podział pełne hello wiadomości powitania. Jeśli hello [ActiveMessageCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagecountdetails.activemessagecount.aspx) właściwości jest duża lub rosnącym, a następnie wiadomości powitania nie jest odczytywana tak szybko, jak jest zapisywana.

### <a name="event-hubs"></a>Usługa Event Hubs
Centra zdarzeń ma limit 20 grup odbiorców, na Centrum zdarzeń. Podczas próby toocreate więcej pojawi się [quotaexceededexception —](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) wskazuje, że użytkownik zainicjował operację trwa dłużej niż limit czasu operacji hello. 

Należy sprawdzić wartość hello hello [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) właściwość jako naciśnięcie tego limitu może również spowodować [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

### <a name="queues-and-topics"></a>Kolejki i tematy
Dla kolejek i tematów, limit czasu hello jest określony w hello [MessagingFactorySettings.OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout) właściwość, jako część ciągu połączenia hello, lub za pośrednictwem [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). komunikat o błędzie Hello, się różnić, ale zawsze zawiera wartość limitu czasu hello hello bieżącej operacji. 

### <a name="event-hubs"></a>Usługa Event Hubs
Usługi Event hubs hello limitu czasu jest określony jako część ciągu połączenia hello lub za pośrednictwem [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). komunikat o błędzie Hello, się różnić, ale zawsze zawiera wartość limitu czasu hello hello bieżącej operacji. 

### <a name="common-causes"></a>Typowe przyczyny
Istnieją dwie typowe przyczyny tego błędu: nieprawidłowa konfiguracja lub Błąd przejściowy usługi.

1. **Nieprawidłowa konfiguracja** hello limit czasu operacji może być za mała dla wartości hello warunki operacyjne. Domyślna wartość Limit czasu operacji hello powitania klienta SDK Hello wynosi 60 sekund. Sprawdź, czy toosee, jeśli kod ma wartość hello ustawić toosomething za mały. Zanotuj tego warunku hello hello sieci i użycie Procesora może mieć wpływ na powitania czas dla toocomplete określonej operacji, więc limit czasu operacji hello nie powinien mieć ustawionej bardzo mała wartość tooa.
2. **Błąd przejściowy usługi** hello czasami usługi Service Bus mogą występować opóźnienia podczas przetwarzania żądań, na przykład w okresach dużego natężenia ruchu sieciowego. W takich przypadkach możesz ponowić operację z opóźnieniem, aż operacja hello zakończy się powodzeniem. Jeśli hello tej samej operacji nadal nie powiedzie się po wielu próbach, odwiedź stronę hello [lokacji stanu usługi Azure](https://azure.microsoft.com/status/) toosee, jeśli występują awarie wszystkie znane usługi.

## <a name="next-steps"></a>Następne kroki

Aby hello pełną dokumentację interfejsu API usługi Service Bus .NET, zobacz hello [dokumentacja interfejsu API platformy .NET Azure](/dotnet/api/overview/azure/servicebus).

więcej informacji na temat toolearn [usługi Service Bus](https://azure.microsoft.com/services/service-bus/), zobacz następujące tematy hello.

* [Omówienie obsługi komunikatów w usłudze Service Bus](service-bus-messaging-overview.md)
* [Podstawy usługi Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Architektura usługi Service Bus](service-bus-architecture.md)

