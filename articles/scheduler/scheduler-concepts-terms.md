---
title: "aaaScheduler pojęcia, warunki i jednostek | Dokumentacja firmy Microsoft"
description: "Pojęcia, terminologia oraz hierarchia jednostek związane z usługą Azure Scheduler, w tym zadania i kolekcje zadań.  Kompleksowy przykład zaplanowanego zadania."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a>Pojęcia i terminologia dotyczące usługi Scheduler oraz hierarchia jednostek
## <a name="scheduler-entity-hierarchy"></a>Hierarchia jednostek w ramach usługi Scheduler
Witaj poniższej tabeli opisano hello głównego widoczne lub zasoby używane przez hello API harmonogramu:

| Zasób | Opis |
| --- | --- |
| **Kolekcja zadań** |Kolekcja zadań zawiera grupy zadań i przechowuje ustawienia, przydziały i limity współużytkowane przez zadań w kolekcji hello. Kolekcja zadań jest tworzona przez właściciela subskrypcji i stanowi grupę zadań utworzoną na podstawie granic użycia lub zastosowania. Jest ograniczone tooone regionu. Umożliwia także przydziały hello Wymuszanie użycia hello tooconstrain wszystkich zadań w tej kolekcji. przydziały Hello obejmują MaxJobs i MaxRecurrence. |
| **Zadanie** |Zadanie definiuje jedną powtarzającą się akcję powiązaną z prostymi lub złożonymi strategiami wykonania. Akcje mogą obejmować żądania HTTP, żądania kolejki magazynu i żądania kolejki magistrali usług lub tematu magistrali usług. |
| **Historia zadania** |Historia zadania zawiera szczegółowe informacje dotyczące wykonywania zadania. Zawiera ona informacje na temat pomyślnych wykonań i niepowodzeń, a także wszelkie szczegóły odpowiedzi. niepowodzeń, a także wszelkie szczegóły odpowiedzi. |

## <a name="scheduler-entity-management"></a>Zarządzanie jednostkami usługi Scheduler
Na wysokim poziomie harmonogram hello i interfejs API zarządzania usługami hello uwidacznia następujące operacje na zasobach hello hello:

| Możliwości | Opis i adres URI |
| --- | --- |
| **Zarządzanie kolekcją zadań** |GET PUT i DELETE Obsługa tworzenia i modyfikowania kolekcji zadań i zadań hello zawartych w niej. Kolekcja zadań jest kontenerem dla zadania oraz mapuje tooquotas i ustawienia udostępnione. Przykłady przydziałów, które zostały opisane w dalszej części artykułu, dotyczą maksymalnej liczby zadań oraz najmniejszego interwału cyklu. <p>PUT i DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p><p>GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p> |
| **Zarządzanie zadaniami** |Obsługa żądań GET, PUT, POST, PATCH i DELETE służących do tworzenia i modyfikowania zadań. Wszystkie zadania muszą należeć tooa kolekcji zadań, która już istnieje, więc nie ma żadnych niejawne tworzenie. <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| **Zarządzanie historią zadania** |Obsługa żądania GET umożliwiającego pobranie historii wykonywania zadania z 60 dni obejmującej m.in. informacje o czasie, który upłynął podczas zadania, oraz o wynikach wykonania zadania. Dodaje obsługę parametru ciągu zapytania służącego do filtrowania na podstawie stanu i statusu. <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a>Typy zadań
Istnieje wiele typów zadań: zadania HTTP (w tym zadania protokołu HTTPS, które obsługują protokół SSL), zadania kolejki magazynu, zadania kolejki magistrali usług i zadania tematu magistrali usług. Zadania HTTP są odpowiednie, jeśli istnieje punkt końcowy danego obciążenia lub usługi. Możesz użyć magazynu kolejki zadań toopost wiadomości toostorage kolejki, dlatego te zadania są idealne rozwiązanie w przypadku obciążeń, które korzystają z magazynu kolejek. Podobnie zadania magistrali usług są odpowiednie dla obciążeń wykorzystujących kolejki i tematy magistrali usług.

## <a name="hello-job-entity-in-detail"></a>Jednostka "zadania" Hello szczegółowo
Ogólna struktura zaplanowanego zadania obejmuje kilka elementów:

* Witaj tooperform akcji po hello zadania czasomierza  
* Witaj (opcjonalnie) czas toorun hello zadania  
* (Opcjonalnie) Kiedy i jak często zadanie hello toorepeat  
* (Opcjonalnie) Toofire akcji, jeśli akcji głównej hello nie powiedzie się.  

Wewnętrznie zaplanowane zadanie zawiera także dane dostarczane przez system, takie jak następnym zaplanowanym terminie wykonywania hello.

Witaj następującego kodu zapewnia kompleksowy przykład zaplanowanego zadania. Szczegóły można znaleźć w kolejnych sekcjach.

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

Jak pokazano w hello próbki zaplanowane zadanie powyżej, definicji zadania ma kilka części:

* Czas rozpoczęcia (“startTime”)  
* Akcja („action”), w tym akcja w przypadku błędu („errorAction”)
* Cykl („recurrence”)  
* Stan („state”)  
* Status („status”)  
* Zasady ponawiania („retryPolicy”)  

Przeanalizujmy szczegółowo każdy z nich:

## <a name="starttime"></a>startTime
Witaj "wartość startTime" jest czas rozpoczęcia hello i umożliwia toospecify wywołującego hello przesunięcie umieszczonego hello w strefie czasowej [formacie ISO 8601](http://en.wikipedia.org/wiki/ISO_8601).

## <a name="action-and-erroraction"></a>action i errorAction
Hello: akcja jest wywoływana przy każdym wystąpieniu Akcja hello i opisuje typ wywołania usługi. Akcja Hello jest, co ma zostać wykonany hello podany harmonogram. Usługa Scheduler obsługuje akcje HTTP, akcje kolejki magazynu oraz akcje tematu i kolejki magistrali usług.

Akcja Hello w powyższym przykładzie hello jest akcji HTTP. Poniżej znajduje się przykład akcji kolejki magazynu:

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

Poniżej znajduje się przykład akcji tematu magistrali usług:

  "action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Możliwe opcje to netMessaging i AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Wybrany komunikat", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }

Poniżej znajduje się przykład akcji kolejki magistrali usług:

  "action": { "serviceBusQueueMessage": { "queueName": "q1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Możliwe opcje to netMessaging i AMQP "authentication": {  
        "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Wybrany komunikat",  
      "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }

Witaj "errorAction" jest hello błąd obsługi, hello Akcja wywoływana, gdy hello głównej akcji kończy się niepowodzeniem. Możesz użyć tej zmiennej toocall punktu końcowego obsługi błędów lub wysłać powiadomienia użytkownika. Może to służyć do osiągnięcia dodatkowej punktu końcowego w przypadku hello tego hello podstawowy jest niedostępny (np. w przypadku hello awarii w lokacji hello punktu końcowego) lub może służyć do powiadamiania błąd obsługi punktu końcowego. Podobnie jak akcji głównej hello hello akcji błędu może być proste i złożone logiki oparte na inne akcje. jak toocreate tokenu sygnatury dostępu Współdzielonego, można znaleźć zbyt toolearn[tworzenia i używania sygnaturę dostępu współdzielonego](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="recurrence"></a>recurrence
Na cykl składa się kilka elementów:

* Częstotliwość (frequency): minuta, godzina, dzień, tydzień, miesiąc lub rok  
* : Interwał na powitania podana częstotliwość cyklu hello  
* Harmonogram wyznaczonych: Określ minuty, godziny, dni tygodnia, miesięcy i monthdays hello cyklu  
* Liczba (count): liczba wystąpień  
* Czas zakończenia: żadne zadania będą wykonywane po hello określony czas zakończenia  

Zadanie określa się jako cykliczne, jeśli jego definicja JSON zawiera obiekt cykliczny. Jeśli jest określony zarówno liczby, jak i endTime jest honorowane hello ukończenia regułę, która zostanie wykonane jako pierwsze.

## <a name="state"></a>state
Stan Hello zadania hello jest jednym z cztery wartości: włączone, wyłączone, zakończone lub wystąpił błąd. Możesz też ZAZNACZYĆ lub poprawki zadania, tak jak tooupdate ich toohello włączenie lub wyłączenie stanu. W przypadku zadania została wykonana lub wystąpił błąd, który jest stan końcowy, który nie można zaktualizować (ale nadal można usunąć zadania hello). Przykład właściwość state hello jest następujący:

        "state": "disabled", // enabled, disabled, completed, or faulted
Zadania ukończone oraz zadania z błędami są usuwane po upływie 60 dni.

## <a name="status"></a>status
Po rozpoczęciu zadania harmonogramu, zostaną zwrócone informacje o bieżący stan zadania hello hello. Ten obiekt nie jest można ustawić przez użytkownika hello — jest on ustawiony przez hello system. Jednak jest ona objęta hello obiektu zadania (a nie oddzielnych zasobu połączonego), aby jeden łatwo uzyskać hello stanu zadania.

Stan zadania zawiera czas hello hello poprzednie wykonanie (jeśli istnieje), hello czasu hello kolejne zaplanowane wykonanie (dla zadania w toku), a liczba wykonań hello hello zadania.

## <a name="retrypolicy"></a>retryPolicy
W przypadku niepowodzenia zadania harmonogramu jest możliwe toospecify toodetermine zasady ponawiania, czy i jak akcji hello próba zostanie ponowiona. Jest to określane za pomocą hello **retryType** obiektu — ustawiono zbyt**Brak** Jeśli nie zasady ponawiania zgodnie z powyższym. Ustaw zbyt**stałej** przypadku zasady ponawiania.

tooset zasady ponawiania, można określić dodatkowe ustawienia w dwóch: interwał ponawiania prób (**retryInterval**) i hello liczby ponownych prób (**retryCount**).

Interwał ponawiania Hello, określony za pomocą hello **retryInterval** obiektu, jest hello interwał między ponownymi próbami. Jego wartość domyślna to 30 sekund. Minimalna wartość, jaką można skonfigurować, wynosi 15 sekund, a wartość maksymalna — 18 miesięcy. W przypadku zadań z bezpłatnej kolekcji zadań minimalna wartość możliwa do skonfigurowania to 1 godzina.  Jest on zdefiniowany w formacie ISO 8601 hello. Podobnie, określona jest wartość hello hello liczby ponownych prób z hello **retryCount** obiekt; jest hello liczbę razy, zostanie podjęta ponowna próba. Wartość domyślna to 4, a wartość maksymalna jest 20\. Zarówno **retryInterval** i **retryCount** są opcjonalne. Są podane wartości domyślne, jeśli **retryType** ustawiono zbyt**stałej** i nie określono żadnych wartości jawnie.

## <a name="see-also"></a>Zobacz też
 [Co to jest Scheduler?](scheduler-intro.md)

 [Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure](scheduler-get-started-portal.md)

 [Plany i rozliczenia w usłudze Azure Scheduler](scheduler-plans-billing.md)

 [Jak planuje toobuild złożone i zaawansowane cyklu z Harmonogram systemu Azure](scheduler-advanced-complexity.md)

 [Dokumentacja interfejsu API REST usługi Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler](scheduler-powershell-reference.md)

 [Wysoka dostępność i niezawodność usługi Azure Scheduler](scheduler-high-availability-reliability.md)

 [Limity, wartości domyślne i kody błędów usługi Azure Scheduler](scheduler-limits-defaults-errors.md)

 [Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler](scheduler-outbound-authentication.md)

