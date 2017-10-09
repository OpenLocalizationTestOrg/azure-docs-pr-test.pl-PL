---
title: "Wyjątki przekazywania aaaAzure i w jaki sposób tooresolve ich | Dokumentacja firmy Microsoft"
description: "Pobierz listę wyjątków przekaźnika usługi Azure i sugerowanych akcji może zająć toohelp ich rozwiązywania."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5f9dd02c-cce0-43b3-8eb8-744f0c27f38c
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: de417c8e9e43407ef355fd44f6170cf2cdc46d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-exceptions"></a>Wyjątki przekaźnika usługi Azure

W tym artykule wymieniono niektóre wyjątki, które mogą być generowane przez hello interfejsów API przekaźnika usługi Azure. To odwołanie jest toochange podmiotu, dlatego sprawdzanie dostępności aktualizacji.

## <a name="exception-categories"></a>Kategorie wyjątku

Hello przekazywania interfejsów API generowania wyjątków, które mogą można podzielić na następujące kategorie hello. Liście są również wyświetlić sugerowane akcje, czy można wykonać toohelp resolve hello wyjątków.

*   **Błąd kodowania użytkownika**: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [ System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). 

    **Ogólne działanie**: spróbuj kodu hello toofix przed kontynuowaniem.
*   **Błąd instalacji/konfiguracji**: [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). 

    **Ogólne działanie**: Przejrzyj konfigurację. W razie potrzeby zmień hello konfiguracji.
*   **Wyjątki przejściowa**: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [ Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). 

    **Ogólne działanie**: ponów próbę wykonania operacji hello lub powiadomić użytkowników.
*   **Pozostałe wyjątki**: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx). 

    **Ogólne działanie**: toohello określonego typu wyjątku. Zobacz tabelę hello w hello następujących sekcji. 

## <a name="exception-types"></a>Typy wyjątków

Witaj Poniższa tabela zawiera listę typów wyjątków obsługi wiadomości i ich przyczyny. Uwagi dotyczące również sugerowanych akcji może zająć rozwiązanie toohelp hello wyjątków.

| **Typ wyjątku** | **Opis** | **Zalecane działanie** | **Należy zwrócić uwagę na automatyczne lub natychmiastowego ponawiania** |
| --- | --- | --- | --- |
| [Limit czasu](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Witaj serwer nie odpowiedział toohello żądanej operacji w ramach hello określony czas, który jest kontrolowany przez [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout). Witaj serwera może mieć ukończone hello żądanej operacji. Może to nastąpić z powodu toonetwork lub innych opóźnienia infrastruktury. |Sprawdź stan systemu hello spójności, a następnie spróbuj ponownie, jeśli jest to konieczne. Zobacz [TimeoutException](#timeoutexception). |Ponów próbę, może pomóc w niektórych przypadkach; Dodaj toocode logiki ponawiania. |
| [Nieprawidłowa operacja](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Witaj zażądał operacji użytkownika nie jest dozwolone w ramach powitania serwera lub usługi. Zawiera komunikat wyjątku hello, aby uzyskać szczegółowe informacje. |Sprawdź kod hello i hello dokumentacji. Upewnij się, że ten hello zażądał operacja jest prawidłowa. |Nie pomoże ponów próbę. |
| [Operacja została anulowana](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Próba wprowadzone tooinvoke operacji na obiekcie, który już został zamknięty, zostało przerwane lub usunięty. W rzadkich przypadkach transakcja otoczenia hello zostało już usunięte. |Sprawdź kod hello i upewnij się, że nie jest wywoływany operacji na usuniętym obiekcie. |Nie pomoże ponów próbę. |
| [Nieautoryzowany dostęp](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Witaj [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) obiektu nie można uzyskać tokenu, hello token jest nieprawidłowy lub hello token nie zawiera hello oświadczenia wymagane tooperform hello operacji. |Upewnij się, że ten dostawca tokenów hello jest tworzony z hello poprawne wartości. Sprawdź konfigurację hello hello usługi kontroli dostępu. |Ponów próbę, może pomóc w niektórych przypadkach; Dodaj toocode logiki ponawiania. |
| [Wyjątek argumentu](https://msdn.microsoft.com/library/system.argumentexception.aspx),<br /> [Argument Null](https://msdn.microsoft.com/library/system.argumentnullexception.aspx),<br />[Argument poza zakresem](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Wystąpił co najmniej jeden z następujących hello:<br />Co najmniej jeden metody toohello dostarczone argumenty są nieprawidłowe.<br /> Witaj identyfikator URI dostarczony zbyt[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) lub [Utwórz](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) zawiera jeden lub więcej segmentów ścieżki.<br />schemat identyfikatora URI Hello dostarczane za[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) lub [Utwórz](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) jest nieprawidłowy. <br />wartość właściwości Hello jest większy niż 32 KB. |Sprawdź kod wywołujący hello i upewnij się, że argumenty hello są poprawne. |Nie pomoże ponów próbę. |
| [Serwer jest zajęty](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Usługa nie jest możliwe tooprocess hello żądania w tej chwili. |powitania klienta może czekać przez czas, a następnie ponów próbę wykonania operacji hello. |powitania klienta może ponowić próbę po upływie określonego czasu. Jeśli wyniki ponownych prób w różnych wyjątek, sprawdź hello zachowanie ponów próbę wykonania tego wyjątku. |
| [Przekroczono przydział](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Witaj jednostki do obsługi komunikatów osiągnęła maksymalny dozwolony rozmiar. |Utwórz miejsca w jednostce hello odbieranie wiadomości z jednostki hello lub jego podkolejki. Zobacz [quotaexceededexception —](#quotaexceededexception). |Ponów próbę mogą ułatwić czy wiadomości zostały usunięte w hello czasu. |
| [Przekroczono rozmiar komunikatu](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Ładunek komunikatu przekracza limit 256 KB hello. Należy zauważyć, że ten limit 256KB hello jest rozmiar całkowitą wiadomości powitania. rozmiar całkowitą wiadomości powitania może zawierać właściwości systemu i wszelkie koszty programu Microsoft .NET. |Zmniejsz rozmiar hello ładunku wiadomość hello, a następnie ponów próbę wykonania operacji hello. |Nie pomoże ponów próbę. |

## <a name="quotaexceededexception"></a>Quotaexceededexception —

[Quotaexceededexception —](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) wskazuje, że przekroczono limit przydziału dla określonej jednostki.

Do przekazywania, ten wyjątek opakowuje hello [System.ServiceModel.QuotaExceededException](https://msdn.microsoft.com/library/system.servicemodel.quotaexceededexception.aspx), co oznacza, że hello maksymalną liczbę odbiorników został przekroczony dla tego punktu końcowego. Jest to wskazane hello **MaximumListenersPerEndpoint** wartość hello komunikat o wyjątku.

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) wskazuje, że użytkownik zainicjował operację trwa dłużej niż limit czasu operacji hello. 

Sprawdź wartość hello hello [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) właściwości. Naciśnięcie tego limitu mogą dodatkowo powodować [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

Do przekazywania może zostać wyświetlony wyjątków przekroczenia limitu czasu, po pierwszym otwarciu połączenia nadawcy przekazywania. Istnieją dwie typowe przyczyny tego wyjątku:

*   Witaj [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) wartość może być za mały (jeśli nawet przez ułamek sekund).
* Odbiornik przekazywania lokalnego nie może odpowiadać (lub mogą wystąpić problemy reguły zapory, które zabrania odbiorników przyjmuje nowe połączenia klientów), a hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) wartość jest mniejsza niż 20 sekund.

Przykład:

```
'System.TimeoutException’: hello operation did not complete within hello allotted timeout of 00:00:10.
hello time allotted toothis operation may have been a portion of a longer timeout.
```

### <a name="common-causes"></a>Typowe przyczyny
Istnieją dwie typowe przyczyny tego błędu:

*   **Nieprawidłowa konfiguracja**
    
    limit czasu operacji Hello może być za mała dla wartości hello warunki operacyjne. Domyślna wartość Limit czasu operacji hello powitania klienta SDK Hello wynosi 60 sekund. Toosee należy sprawdzić, czy hello w kodzie ma wartość toosomething za mały. Należy pamiętać, że Procesora użycia i hello warunku hello sieci może wpływać na czas powitania dla toocomplete operacji. Należy dobrze nie tooset hello operacji wartość limitu czasu tooa bardzo mała.
*   **Błąd przejściowy usługi**

    Czasami hello usługi przekazywania mogą wystąpić opóźnienia podczas przetwarzania żądania. To może się zdarzyć, na przykład w okresach dużego natężenia ruchu sieciowego. W takim przypadku ponów operację z opóźnieniem, aż operacja hello zakończy się powodzeniem. Jeśli hello tej samej operacji toofail po wielu próbach, sprawdź hello [lokacji stanu usługi Azure](https://azure.microsoft.com/status/) toosee, jeśli istnieją znane awarie usługi.

## <a name="next-steps"></a>Następne kroki
* [Przekaźnik Azure — często zadawane pytania](relay-faq.md)
* [Tworzenie przestrzeni nazw przekazywania](relay-create-namespace-portal.md)
* [Rozpoczynanie pracy z przekaźnika usługi Azure i .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Rozpoczynanie pracy z przekaźnika usługi Azure i węzła](relay-hybrid-connections-node-get-started.md)

