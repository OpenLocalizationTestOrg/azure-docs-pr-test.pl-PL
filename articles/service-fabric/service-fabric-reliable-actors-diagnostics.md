---
title: Diagnostyka aaaActors i monitorowania | Dokumentacja firmy Microsoft
description: "W tym artykule opisano hello diagnostyki i wydajności monitorowania funkcji w środowisku uruchomieniowym usługi sieć szkieletowa Reliable Actors hello, w tym hello zdarzenia i liczniki wydajności emitowane przez nią."
services: service-fabric
documentationcenter: .net
author: abhishekram
manager: timlt
editor: vturecek
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: abhisram
ms.openlocfilehash: 5b266d67875722feef5c5be8861bda6d8132a7d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-actors"></a>Diagnostyka i monitorowanie wydajności struktury Reliable Actors
środowisko uruchomieniowe Reliable Actors Hello emituje [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) zdarzeń i [liczniki wydajności](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Te zapewniają wgląd w działania środowiska uruchomieniowego hello i ułatwić rozwiązywanie problemów i monitorowania wydajności.

## <a name="eventsource-events"></a>Element EventSource zdarzenia
Nazwa dostawcy EventSource Hello hello Reliable Actors w czasie wykonywania jest "Microsoft-ServiceFabric uczestników". Zdarzenia z źródłem tego zdarzenia wyświetlane w hello [zdarzenia diagnostyczne](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) okna, gdy aplikacja aktora hello jest [debugowania w programie Visual Studio](service-fabric-debugging-your-application.md).

Narzędzia i technologie, które pomagają w zbierania i/lub wyświetlanie zdarzeń EventSource przykłady [narzędzia PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [diagnostyki Azure](../cloud-services/cloud-services-dotnet-diagnostics.md), [semantycznego rejestrowania](https://msdn.microsoft.com/library/dn774980.aspx)i hello [ Biblioteka Microsoft TraceEvent](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

### <a name="keywords"></a>Słowa kluczowe
Wszystkie zdarzenia, które należy toohello niezawodnej EventSource złośliwych użytkowników są skojarzone z jedną lub kilka słów kluczowych. Dzięki temu filtrowania zdarzeń, które są zbierane. zdefiniowano powitania po — słowo kluczowe usługi bits.

| bitowe | Opis |
| --- | --- |
| 0x1 |Zestaw ważnych wydarzeń, które Podsumuj operacji hello aparatu plików wykonywalnych hello złośliwych użytkowników sieci szkieletowej. |
| 0x2 |Zestaw zdarzenia, które opisują wywołania metody aktora. Aby uzyskać więcej informacji, zobacz hello [wprowadzające temat podmiotów](service-fabric-reliable-actors-introduction.md). |
| 0x4 |Ustawianie stanu tooactor powiązanych zdarzeń. Aby uzyskać więcej informacji, zobacz temat hello na [Zarządzanie stanem aktora](service-fabric-reliable-actors-state-management.md). |
| 0x8 |Zestaw zdarzeń powiązanych tooturn współbieżności opartej w hello aktora. Aby uzyskać więcej informacji, zobacz temat hello na [współbieżności](service-fabric-reliable-actors-introduction.md#concurrency). |

## <a name="performance-counters"></a>Liczniki wydajności
środowisko uruchomieniowe Reliable Actors Hello definiuje hello następujących kategorii licznika wydajności.

| Kategoria | Opis |
| --- | --- |
| Aktora sieci szkieletowej usług |Liczniki tooAzure określonych podmiotów usługi Service Fabric, np. czas stanu aktora toosave |
| Metoda aktora sieci szkieletowej usług |Liczniki określone toomethods implementowane przez złośliwych użytkowników usługi Service Fabric, np. częstotliwość wywoływana jest metoda aktora |

Każdy z hello powyżej kategorii ma co najmniej jeden licznik.

Witaj [Monitor wydajności systemu Windows](https://technet.microsoft.com/library/cc749249.aspx) aplikacji, która jest dostępna domyślnie w systemie operacyjnym Windows hello mogą być używane dane o liczników wydajności toocollect i widoku. [Diagnostyka Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) jest inną opcją w przypadku zbierania danych licznika wydajności i przekazać go tooAzure tabel.

### <a name="performance-counter-instance-names"></a>Nazwy wystąpień liczników wydajności
Klaster ma dużą liczbę usług aktora lub partycji usługi aktora ma dużą liczbę wystąpień liczników wydajności aktora. Witaj nazwy wystąpień liczników wydajności mogą pomóc w identyfikacji określonych hello [partycji](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors) i metoda aktora (jeśli dotyczy) danego wystąpienia licznika wydajności hello jest skojarzony.

#### <a name="service-fabric-actor-category"></a>Kategoria aktora sieci szkieletowej usług
Dla kategorii hello `Service Fabric Actor`, nazwy wystąpień liczników hello znajdują się w hello następującego formatu:

`ServiceFabricPartitionID_ActorsRuntimeInternalID`

*ServiceFabricPartitionID* jest hello identyfikator partycji usługi sieć szkieletowa hello wystąpienie licznika wydajności jest skojarzony z reprezentację ciągu hello. Identyfikator partycji: Hello jest identyfikatorem GUID i reprezentacji ciągu jest generowany przez hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) metody z specyfikator formatu "D".

*ActorRuntimeInternalID* hello reprezentacja ciągu 64-bitową liczbę całkowitą, generowany przez środowisko uruchomieniowe sieci szkieletowej podmiotów hello użytku wewnętrznego. To jest uwzględniona w wystąpienie licznika wydajności hello nazwy tooensure jego unikatowości i uniknąć konfliktu z innym nazwy wystąpień liczników wydajności. Użytkownicy nie Wypróbuj toointerpret tej części nazwę wystąpienia licznika wydajności hello.

Witaj poniżej przedstawiono przykład nazwę wystąpienia licznika licznika, który należy toohello `Service Fabric Actor` kategorii:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046`

W powyższym przykładzie hello `2740af29-78aa-44bc-a20b-7e60fb783264` jest identyfikator partycji: hello sieci szkieletowej usług, reprezentację ciągu hello i `635650083799324046` za pomocą hello 64-bitowy identyfikator, który jest generowany podczas wewnętrznego hello środowiska wykonawczego.

#### <a name="service-fabric-actor-method-category"></a>Kategoria metoda aktora sieci szkieletowej usług
Dla kategorii hello `Service Fabric Actor Method`, nazwy wystąpień liczników hello znajdują się w hello następującego formatu:

`MethodName_ActorsRuntimeMethodId_ServiceFabricPartitionID_ActorsRuntimeInternalID`

*MethodName* jest hello Nazwa metody aktora hello hello wystąpienie licznika wydajności jest skojarzony. Hello format nazwy metody hello jest określana w oparciu logikę w środowisku uruchomieniowym złośliwych użytkowników sieci szkieletowej hello, który równoważy czytelność hello hello nazwy z ograniczeń hello maksymalna długość nazwy wystąpienia licznika wydajności hello w systemie Windows.

*ActorsRuntimeMethodId* reprezentacja ciąg hello 32-bitową liczbę całkowitą, generowany przez środowisko uruchomieniowe sieci szkieletowej podmiotów hello użytku wewnętrznego. To jest uwzględniona w wystąpienie licznika wydajności hello nazwy tooensure jego unikatowości i uniknąć konfliktu z innym nazwy wystąpień liczników wydajności. Użytkownicy nie Wypróbuj toointerpret tej części nazwę wystąpienia licznika wydajności hello.

*ServiceFabricPartitionID* jest hello identyfikator partycji usługi sieć szkieletowa hello wystąpienie licznika wydajności jest skojarzony z reprezentację ciągu hello. Identyfikator partycji: Hello jest identyfikatorem GUID i reprezentacji ciągu jest generowany przez hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) metody z specyfikator formatu "D".

*ActorRuntimeInternalID* hello reprezentacja ciągu 64-bitową liczbę całkowitą, generowany przez środowisko uruchomieniowe sieci szkieletowej podmiotów hello użytku wewnętrznego. To jest uwzględniona w wystąpienie licznika wydajności hello nazwy tooensure jego unikatowości i uniknąć konfliktu z innym nazwy wystąpień liczników wydajności. Użytkownicy nie Wypróbuj toointerpret tej części nazwę wystąpienia licznika wydajności hello.

Witaj poniżej przedstawiono przykład nazwę wystąpienia licznika licznika, który należy toohello `Service Fabric Actor Method` kategorii:

`ivoicemailboxactor.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486`

W powyższym przykładzie hello `ivoicemailboxactor.leavemessageasync` jest nazwą metody hello, `2` jest hello używać 32-bitowy identyfikator generowane podczas wewnętrzny środowiska uruchomieniowego hello, `89383d32-e57e-4a9b-a6ad-57c6792aa521` reprezentacja ciąg hello identyfikator partycji: hello sieci szkieletowej usług, i `635650083804480486` hello 64-bitowego identyfikatora wygenerowany do użytku wewnętrznego hello runtime.

## <a name="list-of-events-and-performance-counters"></a>Lista zdarzeń i liczników wydajności
### <a name="actor-method-events-and-performance-counters"></a>Aktora metody zdarzenia i liczniki wydajności
Hello środowiska uruchomieniowego Reliable Actors emituje hello następujące zdarzenia związane z zbyt[metody aktora](service-fabric-reliable-actors-introduction.md).

| Nazwa zdarzenia | Identyfikator zdarzenia | Poziom | Słowo kluczowe | Opis |
| --- | --- | --- | --- | --- |
| ActorMethodStart |7 |Pełne |0x2 |Środowisko uruchomieniowe złośliwych użytkowników dotyczy tooinvoke metodę aktora. |
| ActorMethodStop |8 |Pełne |0x2 |Metoda aktora zakończono wykonywanie. To, że zwróciła metodę aktora toohello wywołania asynchronicznego hello środowiska uruchomieniowego i ukończeniu zadania hello zwracany przez metodę aktora hello. |
| ActorMethodThrewException |9 |Ostrzeżenie |0x3 |Wystąpił wyjątek podczas wykonywania metody aktora hello podczas metodę aktora toohello wywołania asynchronicznego hello runtime lub podczas wykonywania zadań hello hello zwracany przez metodę aktora hello. To zdarzenie oznacza jakiegoś awarii w hello aktora kod, który wymaga badania. |

środowisko uruchomieniowe Reliable Actors Hello publikuje hello następujące liczniki wydajności toohello powiązane wykonywanie metody aktora.

| Nazwa kategorii | Nazwa licznika | Opis |
| --- | --- | --- |
| Metoda aktora sieci szkieletowej usług |Wywołania na sekundę |Ile razy wywołaniu metody usługi aktora hello na sekundę |
| Metoda aktora sieci szkieletowej usług |Średnia liczba milisekund dla wywołania |Czas poświęcony na tooexecute hello metody usługi aktora w milisekundach |
| Metoda aktora sieci szkieletowej usług |Wyjątki zgłaszane na sekundę |Ile razy hello metody usługi aktora zwrócił wyjątek na sekundę |

### <a name="concurrency-events-and-performance-counters"></a>Współbieżność zdarzenia i liczniki wydajności
Hello środowiska uruchomieniowego Reliable Actors emituje hello następujące zdarzenia związane z zbyt[współbieżności](service-fabric-reliable-actors-introduction.md#concurrency).

| Nazwa zdarzenia | Identyfikator zdarzenia | Poziom | Słowo kluczowe | Opis |
| --- | --- | --- | --- | --- |
| ActorMethodCallsWaitingForLock |12 |Pełne |0x8 |To zdarzenie jest zapisywane na powitania na początku każdego nowego Włącz w aktora. Zawiera ona hello liczby oczekujących wywołań aktora oczekujących blokady dla aktora hello tooacquire, wymusza współbieżności opartej na Włącz. |

środowisko uruchomieniowe Reliable Actors Hello publikuje powitania po tooconcurrency pokrewne liczniki wydajności.

| Nazwa kategorii | Nazwa licznika | Opis |
| --- | --- | --- |
| Aktora sieci szkieletowej usług |Liczba wywołań aktora czekających na blokadę aktora |Liczba oczekujących wywołań aktora czekających blokady dla aktora hello tooacquire, wymusza współbieżności opartej na włączanie |
| Aktora sieci szkieletowej usług |Średni czas oczekiwania na blokadę (milisekundy) |Czas wykonania (w milisekundach) tooacquire hello na aktora blokady wymusza na podstawie Włącz współbieżności |
| Aktora sieci szkieletowej usług |Średni czas utrzymania blokady aktora (milisekundy) |Czas (w milisekundach), dla których hello jest utrzymywana blokady dla aktora |

### <a name="actor-state-management-events-and-performance-counters"></a>Liczniki wydajności i zdarzeń zarządzania stanu aktora
Hello środowiska uruchomieniowego Reliable Actors emituje hello następujące zdarzenia związane z zbyt[Zarządzanie stanem aktora](service-fabric-reliable-actors-state-management.md).

| Nazwa zdarzenia | Identyfikator zdarzenia | Poziom | Słowo kluczowe | Opis |
| --- | --- | --- | --- | --- |
| ActorSaveStateStart |10 |Pełne |0x4 |Środowisko uruchomieniowe złośliwych użytkowników dotyczy stanu aktora hello toosave. |
| ActorSaveStateStop |11 |Pełne |0x4 |Środowisko uruchomieniowe podmiotów zakończył zapisywanie stanu aktora hello. |

środowisko uruchomieniowe Reliable Actors Hello publikuje powitania po zarządzanie stanem pokrewne tooactor liczników wydajności.

| Nazwa kategorii | Nazwa licznika | Opis |
| --- | --- | --- |
| Aktora sieci szkieletowej usług |Średnia liczba milisekund dla operacji zapisu stanu |Czas poświęcony na toosave stanu aktora w milisekundach |
| Aktora sieci szkieletowej usług |Średni czas operacji ładowania stanu (milisekundy) |Czas poświęcony na tooload stanu aktora w milisekundach |

### <a name="events-related-tooactor-replicas"></a>Zdarzenia pokrewne tooactor repliki
Hello środowiska uruchomieniowego Reliable Actors emituje hello następujące zdarzenia związane z zbyt[replik aktora](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

| Nazwa zdarzenia | Identyfikator zdarzenia | Poziom | Słowo kluczowe | Opis |
| --- | --- | --- | --- | --- |
| ReplicaChangeRoleToPrimary |1 |Informacyjny |0x1 |Repliki aktora zmienić tooPrimary roli. Oznacza to, że hello uczestników dla tej partycji zostanie utworzony wewnątrz tej repliki. |
| ReplicaChangeRoleFromPrimary |2 |Informacyjny |0x1 |Repliki aktora zmienić podstawowy toonon roli. Oznacza to, że hello uczestników dla tej partycji nie można tworzyć wewnątrz tej repliki. Żadne żądania nie są dostarczane tooactors już utworzone w ramach tej repliki. Witaj złośliwych użytkowników zostaną usunięte po ukończeniu wszystkich żądań w toku. |

### <a name="actor-activation-and-deactivation-events-and-performance-counters"></a>Aktora Aktywacja i dezaktywacja zdarzenia i liczniki wydajności
Hello środowiska uruchomieniowego Reliable Actors emituje hello następujące zdarzenia związane z zbyt[aktora Aktywacja i dezaktywacja](service-fabric-reliable-actors-lifecycle.md).

| Nazwa zdarzenia | Identyfikator zdarzenia | Poziom | Słowo kluczowe | Opis |
| --- | --- | --- | --- | --- |
| ActorActivated |5 |Informacyjny |0x1 |Uaktywnieniu aktora. |
| ActorDeactivated |6 |Informacyjny |0x1 |Dezaktywowano aktora. |

środowisko uruchomieniowe Reliable Actors Hello publikuje hello następujące liczniki wydajności powiązane tooactor Aktywacja i dezaktywacja.

| Nazwa kategorii | Nazwa licznika | Opis |
| --- | --- | --- |
| Aktora sieci szkieletowej usług |Średnia liczba milisekund OnActivateAsync |Czas tooexecute metody OnActivateAsync w milisekundach |

### <a name="actor-request-processing-performance-counters"></a>Liczniki wydajności przetwarzania żądania aktora
Gdy klient wywołuje metodę za pośrednictwem obiektu proxy aktora, wynikiem są wysyłane za pośrednictwem usługi aktora toohello sieciowych hello komunikat żądania. Usługa Hello przetwarza komunikat żądania hello i wysyła klientowi wstecz toohello odpowiedzi. środowisko uruchomieniowe Reliable Actors Hello publikuje powitania po przetwarzania żądań powiązanych tooactor liczników wydajności.

| Nazwa kategorii | Nazwa licznika | Opis |
| --- | --- | --- |
| Aktora sieci szkieletowej usług |Liczba oczekujących żądań |Liczba żądań przetwarzanych w usłudze hello |
| Aktora sieci szkieletowej usług |Średnia liczba milisekund dla żądania |Czas trwania (w milisekundach) tooprocess usługi hello żądania |
| Aktora sieci szkieletowej usług |Średni czas deserializacji żądania (milisekundy) |Czas wykonania (w milisekundach) toodeserialize aktora komunikat żądania po odebraniu hello usługi |
| Aktora sieci szkieletowej usług |Średni czas serializacji odpowiedzi (milisekundy) |Wiadomości powitania tooserialize wykonania (w milisekundach) czas odpowiedzi aktora w usług hello przed wysłaniem odpowiedzi powitania klienta toohello |

## <a name="next-steps"></a>Następne kroki
* [Jak używać platformy Service Fabric hello w Reliable Actors](service-fabric-reliable-actors-platform.md)
* [Dokumentację referencyjną aktora interfejsu API](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Przykładowy kod](https://github.com/Azure/servicefabric-samples)
* [Element EventSource dostawców w narzędzia PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
