---
title: "Przegląd cyklu życia Azure Usługa sieci szkieletowej niezawodnej usługi | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zdarzeń różnych cyklu życia w sieci szkieletowej usług niezawodne usługi"
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek;
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 16021ca72a2f10070b6409417ff0d88009591331
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Przegląd cyklu życia niezawodne usługi
> [!div class="op_single_selector"]
> * [C# w systemie Windows](service-fabric-reliable-services-lifecycle.md)
> * [Java w systemie Linux](service-fabric-reliable-services-lifecycle-java.md)
>
>

Rozważania na temat cykli niezawodnych usług, podstawowe informacje o cyklu życia są najważniejsze. Ogólnie rzecz biorąc:

- Podczas uruchamiania
  - Usługi są wykonane
  - Mają możliwość utworzenia i zwraca zero lub więcej obiektów nasłuchujących
  - Wszystkie zwracane obiekty nasłuchujące są otwarte, zezwolenie na komunikację z usługą
  - Wywoływana jest metoda RunAsync usługi, dzięki czemu usługa długo działa lub pracy w tle
- Podczas zamykania
  - Token anulowania przekazany do RunAsync została anulowana, a odbiorniki są zamknięte
  - To znaczy po zakończeniu sam obiekt usługi jest niszczone

Brak szczegółów wokół dokładne kolejność tych zdarzeń. W szczególności kolejność zdarzeń mogą się nieznacznie zmieniać w zależności od tego, czy usługa niezawodnej jest Stateless lub Stateful. Ponadto usługi stanowej, zostały radzenia sobie z scenariusz podstawowy wymiany. Podczas tej sekwencji rolę podstawową jest przenoszona do innej repliki (lub wróci) bez zamknięcie usługi. Na koniec mamy Pomyśl o warunkach błędu lub niepowodzenie.

## <a name="stateless-service-startup"></a>Uruchamianie usługi bezstanowej
Cykl życia usługi bezstanowej jest bardzo prosta. Poniżej przedstawiono kolejność zdarzeń:

1. Usługa jest tworzony
2. Następnie w dwie czynności równoległe stanie:
    - `StatelessService.CreateServiceInstanceListeners()`jest wywoływany i wszystkie zwracane obiekty nasłuchujące są otwarte. `ICommunicationListener.OpenAsync()`jest wywoływane dla każdego odbiornika
    - Usługi `StatelessService.RunAsync()` metoda jest wywoływana
3. Jeśli jest obecny, usługi `StatelessService.OnOpenAsync()` metoda jest wywoływana. Jest to rzadko zastąpienia, ale jest ona dostępna.

Należy koniecznie należy pamiętać, że nie kolejność nie między wywołaniami do tworzenia i otwierania odbiorników i RunAsync. Przed rozpoczęciem RunAsync odbiorniki może zostać otwarty. Podobnie RunAsync może się okazać wywoływane przed odbiorników komunikacji są otwarte lub nawet zostały wykonane. Jeśli wymagana jest każdej synchronizacji, jest pozostawiany bez jako wykonywania do implementujący. Typowe rozwiązania:

  - Czasami odbiorników nie może działać, dopóki niektóre informacje o utworzeniu lub pracy wykonanej. Dla usług bezstanowych, które pracy zwykle można zrobić w innych lokalizacjach, takich jak: 
    - w Konstruktorze tej usługi
    - Podczas `CreateServiceInstanceListeners()` wywołania
    - jako część konstrukcji samego odbiornika
  - Czasami kod w RunAsync nie ma się rozpocząć, dopóki odbiorniki są otwarte. W takim przypadku niezbędne jest dodatkowe koordynacji. Jednym z typowych rozwiązań jest niektórych flagi w odbiorników wskazujący po zakończeniu. Ta flaga jest sprawdzany w RunAsync przed kontynuowaniem pracy rzeczywistej.

## <a name="stateless-service-shutdown"></a>Zamykanie usługi bezstanowej
Podczas zamykania usługi bezstanowej, tego samego wzorca jest wykonać tylko w odwrotnej:

1. Równoległe
    - Są zamykane wszystkie otwarte odbiorników. `ICommunicationListener.CloseAsync()`jest wywoływana na każdym odbiornika.
    - Token anulowania przekazany do `RunAsync()` zostało anulowane. Sprawdzanie token anulowania `IsCancellationRequested` właściwość zwraca wartość true i wywołuje tokenu `ThrowIfCancellationRequested` metoda zgłasza `OperationCanceledException`.
2. Raz `CloseAsync()` uzupełnia w każdym odbiornika i `RunAsync()` również zakończeniu usługi `StatelessService.OnCloseAsync()` metoda jest wywoływana, jeśli jest obecny. Jest rzadko do przesłonięcia `StatelessService.OnCloseAsync()`.
3. Po `StatelessService.OnCloseAsync()` zakończeniu obiekt usługi jest niszczone

## <a name="stateful-service-startup"></a>Uruchamianie usługi stanowej
Usługi stanowej mają podobnego wzorca do usług bezstanowych, kilka zmian. Podczas uruchamiania usługi stanowej, kolejność zdarzeń wygląda następująco:

1. Usługa jest tworzony
2. `StatefulServiceBase.OnOpenAsync()`jest wywoływana. To jest zastępowany uncommonly w usłudze.
3. Stanie następujących czynności równoległe
    - `StatefulServiceBase.CreateServiceReplicaListeners()`jest wywoływany 
      - Jeśli usługa jest podstawowym wszystkich odbiorników zwracane są otwarte. `ICommunicationListener.OpenAsync()`jest wywoływana na każdym odbiornika.
      - Jeśli usługa jest pomocniczego, tylko te odbiorniki oznaczona jako `ListenOnSecondary = true` są otwarte. Odbiorniki otwarte na pomocnicze bazy danych jest mniej typowych.
    - Jeśli usługa jest obecnie podstawowym, usługa firmy `StatefulServiceBase.RunAsync()` metoda jest wywoływana
4. Raz wszystkie repliki odbiornika dla `OpenAsync()` ukończenia wywołania i `RunAsync()` jest nazywany `StatefulServiceBase.OnChangeRoleAsync()` jest wywoływana. To jest zastępowany uncommonly w usłudze.

Podobnie do usług bezstanowych, nie zachodzi koordynacja między kolejności, w której odbiorniki są tworzone i otworzyć i gdy jest wywoływana RunAsync. Jeśli potrzebujesz koordynacji rozwiązania są znacznie takie same. Istnieje jeden przypadek dodatkowe: powiedzieć, że wywołania otrzymywanych odbiorników komunikacji wymaga informacje przechowywane w niektórych [niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md). Ponieważ odbiorników komunikacji może otworzyć przed niezawodnej kolekcje są do odczytu lub zapisu, a przed RunAsync można uruchomić, niektóre dodatkowe koordynacji jest konieczne. Rozwiązanie najprostszym i najczęściej jest w przypadku odbiorników komunikacji do zwrócenia kodu błędu używanego przez klienta do ponowić żądanie.

## <a name="stateful-service-shutdown"></a>Zamknięcie usługi stanowej
Podobnie jak usługi bezstanowej zdarzenia cyklu życia podczas zamykania są takie same jak podczas uruchamiania, ale wycofane. Gdy trwa zamykanie usługi stanowej, wykonywane są następujące zdarzenia:

1. Równoległe
    - Są zamykane wszystkie otwarte odbiorników. `ICommunicationListener.CloseAsync()`jest wywoływana na każdym odbiornika.
    - Token anulowania przekazany do `RunAsync()` zostało anulowane. Sprawdzanie token anulowania `IsCancellationRequested` właściwość zwraca wartość true i wywołuje tokenu `ThrowIfCancellationRequested` metoda zgłasza `OperationCanceledException`.
2. Raz `CloseAsync()` uzupełnia w każdym odbiornika i `RunAsync()` również zakończeniu usługi `StatefulServiceBase.OnChangeRoleAsync()` jest wywoływana. (To jest uncommonly zastąpiona w usłudze.)
    - Oczekiwanie na RunAsync ukończyć jest konieczne tylko wtedy, jeśli podstawowy został tej repliki usługi.
3. Raz `StatefulServiceBase.OnChangeRoleAsync()` metody zakończeniu `StatefulServiceBase.OnCloseAsync()` metoda jest wywoływana. Jest to rzadko zastąpienia, ale jest ona dostępna.
3. Po `StatefulServiceBase.OnCloseAsync()` zakończeniu obiekt usługi jest niszczone.

## <a name="stateful-service-primary-swaps"></a>Zamienia głównej usługi stanowej
Uruchomionej usługi stanowej replik podstawowych tej usługi stanowej mają ich odbiorników komunikacji otwarty i ich wywołano metodę RunAsync. Pomocniczy są wykonane, ale Zobacz nie kolejne wywołania. Po uruchomieniu usługi stanowej jednak repliki, który jest obecnie podstawową można zmienić. Co to znaczy w kategoriach zdarzenia cyklu życia, które można wyświetlić repliki Zachowanie, które widzi stanowe repliki zależy od tego, czy jest repliki trwa obniżyć poziom jest podwyższany podczas wymiany.

### <a name="for-the-primary-being-demoted"></a>Dla podstawowego jest obniżenie poziomu
Sieć szkieletowa usług musi tę replikę, aby zatrzymać przetwarzanie komunikatów i zakończyć pracę tła, których wykonywanie operacji. W związku z tym ten krok jest podobny do gdy trwa zamykanie usługi. Jeden różnica polega na czy usługi nie jest niszczone lub zamknięte, ponieważ pozostaje pomocniczego. Następujące interfejsy API są nazywane:

1. Równoległe
    - Są zamykane wszystkie otwarte odbiorników. `ICommunicationListener.CloseAsync()`jest wywoływana na każdym odbiornika.
    - Token anulowania przekazany do `RunAsync()` zostało anulowane. Sprawdzanie token anulowania `IsCancellationRequested` właściwość zwraca wartość true i wywołuje tokenu `ThrowIfCancellationRequested` metoda zgłasza `OperationCanceledException`.
2. Raz `CloseAsync()` uzupełnia w każdym odbiornika i `RunAsync()` również zakończeniu usługi `StatefulServiceBase.OnChangeRoleAsync()` jest wywoływana. To jest zastępowany uncommonly w usłudze.

### <a name="for-the-secondary-being-promoted"></a>Na serwerze pomocniczym, której poziom jest podwyższany
Podobnie sieci szkieletowej usług wymaga tej repliki rozpocząć nasłuchiwania dla wiadomości w sieci i uruchomić wszystkie zadania w tle, który go dba o. W związku z tym ten proces jest podobny do utworzenia usługi, z wyjątkiem tego samego repliki już istnieje. Następujące interfejsy API są nazywane:

1. Równoległe
    - `StatefulServiceBase.CreateServiceReplicaListeners()`jest wywoływany i wszystkie zwracane obiekty nasłuchujące są otwarte. `ICommunicationListener.OpenAsync()`jest wywoływana na każdym odbiornika.
    - Usługi `StatefulServiceBase.RunAsync()` metoda jest wywoływana
2. Raz wszystkie repliki odbiornika dla `OpenAsync()` ukończenia wywołania i `RunAsync()` została wywołana, `StatefulServiceBase.OnChangeRoleAsync()` jest wywoływana. To jest zastępowany uncommonly w usłudze.

### <a name="common-issues-during-stateful-service-shutdown-and-primary-demotion"></a>Typowe problemy podczas zamykania usługi stanowej i obniżania poziomu podstawowego
Sieć szkieletowa usług zmienia podstawowej usługi stanowej z różnych przyczyn. Najbardziej typowe są [klastra, ponowne równoważenie](service-fabric-cluster-resource-manager-balancing.md) i [uaktualniania aplikacji](service-fabric-application-upgrade.md). Podczas tych czynności (a także podczas zamykania normalnego użytkowania, np. zostanie wyświetlony, jeśli usługa została usunięta), należy pamiętać, że usługa przestrzegać `CancellationToken`. Usługi, które nie obsługują anulowania prawidłowo może wystąpić pewne problemy. W szczególności tych operacji będzie zajmować dużo czasu, ponieważ sieć szkieletowa usług czeka na usługi do zatrzymania bezpiecznie. Ostatecznie to prowadzić do uaktualnienia nie powiodło się tego limitu czasu i wycofać. Niepowodzenie uwzględnić token anulowania również może powodować imbalanced klastrów, ponieważ węzły uzyskiwanie dostępu, ale nie można rebalanced usługi, ponieważ trwa zbyt długo, aby przenieść je w innym miejscu. 

Ponieważ usługi stanowej, również jest prawdopodobne, że używają [niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md). W sieci szkieletowej usług podczas obniżania poziomu podstawowego jedną pierwszy co się stanie, jest odebraniu podstawowy stan do zapisu. Prowadzi to do drugiego zestawu problemy, które mogą mieć wpływ na cyklem życia usługi. Kolekcje zwracany wyjątki oparte na czas i czy jest przenoszony repliki lub zamykania. Te wyjątki powinny być traktowane jako poprawnie. Wyjątki generowane przez sieć szkieletowa usług można podzielić na stałe [(`FabricException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricexception?view=azure-dotnet) i przejściowych [(`FabricTransientException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabrictransientexception?view=azure-dotnet) kategorii. Stałe wyjątki powinny być rejestrowane i zgłoszony, gdy przejściowej wyjątki mogą ponowione opartych na logice niektórych ponów próbę.

Obsługa wyjątków, które pochodzą od stosowania `ReliableCollections` w połączeniu z zdarzenia cyklu życia usługi jest ważnym elementem przetestowaniu i zweryfikowaniu niezawodnej usługi. Zalecane jest zawsze przy uruchamianiu usługi Obciążenie podczas wykonywania uaktualnienia i [testowania chaos](service-fabric-controlled-chaos.md) przed wdrożeniem kiedykolwiek do środowiska produkcyjnego. Te podstawowe kroki pomoc, sprawdź, czy usługa jest poprawnie zaimplementowana i poprawnie obsługuje zdarzenia cyklu życia.


## <a name="notes-on-service-lifecycle"></a>Uwagi dotyczące cyklu życia usług
  - Zarówno `RunAsync()` — metoda i `CreateServiceReplicaListeners/CreateServiceInstanceListeners` wywołania są opcjonalne. Usługa może mieć ich, zarówno lub nie. Na przykład, jeśli usługa jest jego pracy w odpowiedź na wywołania użytkownika, jest niepotrzebna go do zaimplementowania `RunAsync()`. Wymagane są tylko odbiorników komunikacji i ich skojarzonego kodu. Podobnie tworzenie i zwracanie odbiorników komunikacji jest opcjonalne, ponieważ usługa może mieć tylko pracy tła i dlatego tylko musi implementować`RunAsync()`
  - Jest on prawidłowy dla usługi, aby ukończyć `RunAsync()` pomyślnie i z powrotem od niego. Kończenie pracy nie jest warunek błędu. Kończenie pracy `RunAsync()` wskazuje, czy praca w tle usługi zostało zakończone. Dla stanowych usług niezawodne `RunAsync()` zostanie ponownie wywołany, jeśli obniżenie poziomu z podstawowego na pomocniczym i następnie podwyższony do podstawowej repliki.
  - Jeśli zamknie usługę `RunAsync()` przez zgłaszanie nieoczekiwany wyjątek, powoduje błąd. Obiekt usługi jest zamknięta i zgłoszony błąd kondycji.
  - Gdy nie ma żadnego limitu czasu na zwracanie z tych metod, natychmiast spowoduje utratę możliwości zapisu do kolekcji niezawodnych i z tego powodu nie można ukończyć rzeczywistą pracę. Zaleca się, czy zwracać możliwie jak najszybciej po otrzymaniu żądania anulowania. Jeśli usługa nie odpowiada na te wywołania interfejsu API w rozsądnym czasie sieci szkieletowej usług wymuszanie może zakończyć korzystanie z usługi. Zwykle to tylko odbywa się podczas uaktualniania aplikacji lub gdy usługa jest usuwana. Tego limitu czasu wynosi 15 minut domyślnie.
  - Błędy w `OnCloseAsync()` doprowadzi do ścieżki `OnAbort()` wywoływana, która jest możliwość optymalnych ostatniej szansy, usługi wyczyścić Konfigurowanie i wszystkie zasoby, które zostały przejęte ich wydania.

## <a name="next-steps"></a>Następne kroki
- [Wprowadzenie do niezawodne usługi](service-fabric-reliable-services-introduction.md)
- [Niezawodne usługi szybki start](service-fabric-reliable-services-quick-start.md)
- [Niezawodne usługi advanced użycia](service-fabric-reliable-services-advanced-usage.md)
