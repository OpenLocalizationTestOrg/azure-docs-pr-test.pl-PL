---
title: "aaaOverview życia hello Azure Usługa sieci szkieletowej niezawodnych usług | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello zdarzenia różnych cyklu życia w sieci szkieletowej usług niezawodne usługi"
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
ms.openlocfilehash: 0d75ed5ee7cda85ac9af6a02e160727277804a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Przegląd cyklu życia niezawodne usługi
> [!div class="op_single_selector"]
> * [C# w systemie Windows](service-fabric-reliable-services-lifecycle.md)
> * [Java w systemie Linux](service-fabric-reliable-services-lifecycle-java.md)
>
>

Rozważania na temat cykli hello niezawodnych usług, podstawy hello życia hello są najważniejsze hello. Ogólnie rzecz biorąc:

- Podczas uruchamiania
  - Usługi są wykonane
  - Mieć możliwość tooconstruct i zwraca zero lub więcej obiektów nasłuchujących
  - Wszystkie zwracane obiekty nasłuchujące są otwarte, zezwolenie na komunikację z usługą hello
  - RunAsync usługi Hello, którego metoda jest wywoływana, dzięki czemu hello usługa toodo długotrwałe lub pracy w tle
- Podczas zamykania
  - tooRunAsync przekazany token anulowania Hello została anulowana, a odbiorników hello są zamknięte
  - To znaczy po zakończeniu sam obiekt usługi hello jest niszczone

Szczegóły dotyczące hello są dokładne uporządkowanie tych zdarzeń. W szczególności hello kolejność zdarzeń mogą się nieznacznie zmieniać w zależności od tego, czy hello niezawodnej usługi jest Stateless lub Stateful. Ponadto usługi stanowej, zostały toodeal ze scenariuszem głównej wymiany hello. Podczas tej sekwencji hello rolę podstawową jest przeniesione tooanother repliki (lub wróci) bez usługi hello zamykanie. Na koniec mamy toothink o warunkach błędu lub niepowodzenie.

## <a name="stateless-service-startup"></a>Uruchamianie usługi bezstanowej
Witaj cyklem życia usługi bezstanowej jest bardzo prosta. Poniżej przedstawiono kolejność zdarzeń hello:

1. Witaj usługi jest tworzony
2. Następnie w dwie czynności równoległe stanie:
    - `StatelessService.CreateServiceInstanceListeners()`jest wywoływany i wszystkie zwracane obiekty nasłuchujące są otwarte. `ICommunicationListener.OpenAsync()`jest wywoływane dla każdego odbiornika
    - Witaj usługi `StatelessService.RunAsync()` metoda jest wywoływana
3. Jeśli jest obecny, hello usługi `StatelessService.OnOpenAsync()` metoda jest wywoływana. Jest to rzadko zastąpienia, ale jest ona dostępna.

Jest toonote ważna jest kolejność nie między toocreate wywołania hello i otwórz hello odbiorników i RunAsync. przed rozpoczęciem RunAsync odbiorników Hello może zostać otwarty. Podobnie RunAsync może się okazać wywoływane przed odbiorników komunikacji hello są otwarte lub nawet zostały wykonane. Jeśli wymagana jest każdej synchronizacji, jest pozostawiany jako implementujący toohello wykonywania. Typowe rozwiązania:

  - Czasami odbiorników nie może działać, dopóki niektóre informacje o utworzeniu lub pracy wykonanej. Dla usług bezstanowych, które pracy zwykle można zrobić w innych lokalizacjach, takich jak: 
    - w Konstruktorze hello usługi
    - Podczas hello `CreateServiceInstanceListeners()` wywołania
    - jako część konstrukcji hello odbiornika hello, sama
  - Czasami hello kodu w RunAsync nie chce toostart dopóki odbiorników hello są otwarte. W takim przypadku niezbędne jest dodatkowe koordynacji. Jednym z typowych rozwiązań jest niektórych flagi w odbiorników hello wskazujący po zakończeniu. Ta flaga jest sprawdzany w RunAsync przed kontynuowaniem pracy tooactual.

## <a name="stateless-service-shutdown"></a>Zamykanie usługi bezstanowej
Podczas zamykania usługi bezstanowej powitalne tego samego wzorca występuje tylko w odwrotnej:

1. Równoległe
    - Są zamykane wszystkie otwarte odbiorników. `ICommunicationListener.CloseAsync()`jest wywoływana na każdym odbiornika.
    - token anulowania Hello przekazano zbyt`RunAsync()` zostało anulowane. Sprawdzanie, czy hello token anulowania na `IsCancellationRequested` właściwość zwraca wartość true i jeśli wywołuje hello token `ThrowIfCancellationRequested` metoda zgłasza `OperationCanceledException`.
2. Raz `CloseAsync()` uzupełnia w każdym odbiornika i `RunAsync()` również zakończeniu hello usługi `StatelessService.OnCloseAsync()` metoda jest wywoływana, jeśli jest obecny. Jest rzadko toooverride `StatelessService.OnCloseAsync()`.
3. Po `StatelessService.OnCloseAsync()` zakończeniu obiektu usługi hello jest niszczone

## <a name="stateful-service-startup"></a>Uruchamianie usługi stanowej
Stanowe usługi mają podobne usługi toostateless wzorzec, kilka zmian. Podczas uruchamiania usługi stanowej, hello kolejność zdarzeń wygląda następująco:

1. Witaj usługi jest tworzony
2. `StatefulServiceBase.OnOpenAsync()`jest wywoływana. To jest zastępowany uncommonly hello usługi.
3. Witaj, następujące elementy wystąpić równolegle
    - `StatefulServiceBase.CreateServiceReplicaListeners()`jest wywoływany 
      - Jeśli usługa hello jest podstawowym wszystkie zwracane obiekty nasłuchujące są otwarte. `ICommunicationListener.OpenAsync()`jest wywoływana na każdym odbiornika.
      - Jeśli usługa hello jest pomocniczego, tylko te odbiorniki oznaczona jako `ListenOnSecondary = true` są otwarte. Odbiorniki otwarte na pomocnicze bazy danych jest mniej typowych.
    - Witaj, jeśli hello usługi jest obecnie podstawowa, usługa hello `StatefulServiceBase.RunAsync()` metoda jest wywoływana
4. Po hello wszystkie repliki odbiornika `OpenAsync()` ukończenia wywołania i `RunAsync()` jest nazywany `StatefulServiceBase.OnChangeRoleAsync()` jest wywoływana. To jest zastępowany uncommonly hello usługi.

Podobnie toostateless usług, nie istnieje żadne koordynację między tymi hello kolejności, w których hello odbiorników są tworzone i otworzyć i gdy jest wywoływana RunAsync. Jeśli potrzebujesz koordynacji rozwiązań hello są znacznie hello tego samego. Istnieje jeden przypadek dodatkowe: powiedzieć, że wywołania hello otrzymywanych odbiorników komunikacji hello wymagają informacje przechowywane w niektórych [niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md). Ponieważ odbiorników komunikacji hello można otworzyć przed hello niezawodnej kolekcje są do odczytu lub zapisu, a przed RunAsync można uruchomić, niektóre dodatkowe koordynacji jest konieczne. Witaj najprostszym i najbardziej typowe rozwiązania dotyczy tooreturn odbiorników komunikacji hello niektórych kod błędu: hello klienta używa tooknow tooretry hello żądania.

## <a name="stateful-service-shutdown"></a>Zamknięcie usługi stanowej
Podobnie usług tooStateless zdarzenia cyklu życia hello podczas zamykania są takie same jak podczas uruchamiania Witaj, lecz wycofane. Gdy trwa zamykanie usługi stanowej, hello miejsce następujące zdarzenia:

1. Równoległe
    - Są zamykane wszystkie otwarte odbiorników. `ICommunicationListener.CloseAsync()`jest wywoływana na każdym odbiornika.
    - token anulowania Hello przekazano zbyt`RunAsync()` zostało anulowane. Sprawdzanie, czy hello token anulowania na `IsCancellationRequested` właściwość zwraca wartość true i jeśli wywołuje hello token `ThrowIfCancellationRequested` metoda zgłasza `OperationCanceledException`.
2. Raz `CloseAsync()` uzupełnia w każdym odbiornika i `RunAsync()` również zakończeniu hello usługi `StatefulServiceBase.OnChangeRoleAsync()` jest wywoływana. (To jest uncommonly zastąpiona w usłudze hello.)
    - Oczekiwanie na RunAsync toocomplete jest konieczne tylko wtedy, jeśli podstawowy został tej repliki usługi.
3. Raz hello `StatefulServiceBase.OnChangeRoleAsync()` metody zakończeniu hello `StatefulServiceBase.OnCloseAsync()` metoda jest wywoływana. Jest to rzadko zastąpienia, ale jest ona dostępna.
3. Po `StatefulServiceBase.OnCloseAsync()` zakończeniu obiektu usługi hello jest niszczone.

## <a name="stateful-service-primary-swaps"></a>Zamienia głównej usługi stanowej
Po uruchomieniu usługi stanowej hello głównej replik tej usługi stanowej może zawierać tylko ich odbiorników komunikacji otworzyć i ich wywołano metodę RunAsync. Pomocniczy są wykonane, ale Zobacz nie kolejne wywołania. Po uruchomieniu usługi stanowej jednak repliki, który jest obecnie hello podstawowej można zmienić. Co to znaczy w kategoriach zdarzenia cyklu życia hello widoczne dla repliki Hello zachowanie hello stanowe repliki widzi zależy od tego, czy jest hello repliki trwa obniżyć poziom jest podwyższany podczas wymiany hello.

### <a name="for-hello-primary-being-demoted"></a>Dla hello jest obniżenie poziomu podstawowego
Sieć szkieletowa usług musi toostop tej repliki, przetwarzanie wiadomości i zakończyć pracę tła, których wykonywanie operacji. W związku z tym kroku wygląda podobnie toowhen hello usługa ta jest zamykany. Jeden różnica polega na tym hello usługi nie jest niszczone lub zamknięte, ponieważ pozostaje pomocniczego. Witaj następujące interfejsy API są nazywane:

1. Równoległe
    - Są zamykane wszystkie otwarte odbiorników. `ICommunicationListener.CloseAsync()`jest wywoływana na każdym odbiornika.
    - token anulowania Hello przekazano zbyt`RunAsync()` zostało anulowane. Sprawdzanie, czy hello token anulowania na `IsCancellationRequested` właściwość zwraca wartość true i jeśli wywołuje hello token `ThrowIfCancellationRequested` metoda zgłasza `OperationCanceledException`.
2. Raz `CloseAsync()` uzupełnia w każdym odbiornika i `RunAsync()` również zakończeniu hello usługi `StatefulServiceBase.OnChangeRoleAsync()` jest wywoływana. To jest zastępowany uncommonly hello usługi.

### <a name="for-hello-secondary-being-promoted"></a>Dla hello dodatkowej, której poziom jest podwyższany
Podobnie sieci szkieletowej usług wymaga tego toostart repliki nasłuchuje wiadomości umieszczonego hello i uruchomić wszystkie zadania w tle, który go dba o. Dzięki temu wygląda ten proces, podobne usługi hello toowhen jest tworzona, z wyjątkiem ta replika hello się już istnieje. Witaj następujące interfejsy API są nazywane:

1. Równoległe
    - `StatefulServiceBase.CreateServiceReplicaListeners()`jest wywoływany i wszystkie zwracane obiekty nasłuchujące są otwarte. `ICommunicationListener.OpenAsync()`jest wywoływana na każdym odbiornika.
    - Witaj usługi `StatefulServiceBase.RunAsync()` metoda jest wywoływana
2. Po hello wszystkie repliki odbiornika `OpenAsync()` ukończenia wywołania i `RunAsync()` została wywołana, `StatefulServiceBase.OnChangeRoleAsync()` jest wywoływana. To jest zastępowany uncommonly hello usługi.

### <a name="common-issues-during-stateful-service-shutdown-and-primary-demotion"></a>Typowe problemy podczas zamykania usługi stanowej i obniżania poziomu podstawowego
Zmiany usługi sieć szkieletowa hello podstawowej usługi stanowej z różnych przyczyn. Witaj najczęściej są [klastra, ponowne równoważenie](service-fabric-cluster-resource-manager-balancing.md) i [uaktualniania aplikacji](service-fabric-application-upgrade.md). Podczas tych czynności (a także podczas zamykania usługi normalnych, jak można zobaczyć, czy usługa hello usunięto), ważne jest, że hello względem usługi hello `CancellationToken`. Usługi, które nie obsługują anulowania prawidłowo może wystąpić pewne problemy. W szczególności tych operacji będzie zajmować dużo czasu, ponieważ oczekuje na powitania toostop usług bezpiecznie sieci szkieletowej usług. Ostatecznie to prowadzić toofailed uaktualnienia tego limitu czasu i wycofać. Token anulowania hello toohonor błąd może również spowodować imbalanced klastrów, ponieważ węzłów uzyskiwanie dostępu, ale nie można rebalanced hello usługi, ponieważ trwa zbyt długo toomove je w innym miejscu. 

Ponieważ hello usługi stanowej, również jest prawdopodobne, że używają hello [niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md). W sieci szkieletowej usług podczas obniżania poziomu głównego, jednym z hello pierwszych rzeczy, które się stanie, jest odebraniu podstawowy stan toohello dostęp do zapisu. Prowadzi to drugi zestaw tooa problemów, które mogą mieć wpływ na hello cyklu życia usług. kolekcje Hello zwracany wyjątków na podstawie czasu hello i czy repliki hello jest przenoszony lub zamykania. Te wyjątki powinny być traktowane jako poprawnie. Wyjątki generowane przez sieć szkieletowa usług można podzielić na stałe [(`FabricException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricexception?view=azure-dotnet) i przejściowych [(`FabricTransientException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabrictransientexception?view=azure-dotnet) kategorii. Stałe wyjątki powinny być rejestrowane i zgłoszony podczas wyjątki przejściowej hello może ponowione opartych na logice niektórych ponów próbę.

Obsługa wyjątków hello, które pochodzą od stosowania hello `ReliableCollections` w połączeniu z zdarzenia cyklu życia usługi jest ważnym elementem przetestowaniu i zweryfikowaniu niezawodnej usługi. Witaj zalecenie jest zawsze toorun usługi Obciążenie podczas wykonywania uaktualnienia i [testowania chaos](service-fabric-controlled-chaos.md) przed wdrożeniem kiedykolwiek tooproduction. Te podstawowe kroki pomoc, sprawdź, czy usługa jest poprawnie zaimplementowana i poprawnie obsługuje zdarzenia cyklu życia.


## <a name="notes-on-service-lifecycle"></a>Uwagi dotyczące cyklu życia usług
  - Zarówno hello `RunAsync()` — metoda i hello `CreateServiceReplicaListeners/CreateServiceInstanceListeners` wywołania są opcjonalne. Usługa może mieć ich, zarówno lub nie. Na przykład, jeśli usługa hello ma jego pracy w wywołaniach toouser odpowiedzi, jest niepotrzebna dla niego tooimplement `RunAsync()`. Wymagane są tylko hello odbiorników komunikacji i ich skojarzonego kodu. Podobnie tworzenie i zwracanie odbiorników komunikacji jest opcjonalne, ponieważ usługa hello może mieć tylko tła pracy toodo i dlatego tylko musi tooimplement`RunAsync()`
  - Jest on prawidłowy dla toocomplete usługi `RunAsync()` pomyślnie i z powrotem od niego. Kończenie pracy nie jest warunek błędu. Kończenie pracy `RunAsync()` wskazuje, czy praca w tle hello hello usługi zostało zakończone. Dla stanowych usług niezawodne `RunAsync()` zostanie ponownie wywołany, jeśli replika hello nastąpiło obniżenie poziomu z głównej tooSecondary i podwyższenia poziomu tooPrimary Wstecz.
  - Jeśli zamknie usługę `RunAsync()` przez zgłaszanie nieoczekiwany wyjątek, powoduje błąd. Obiekt usługi Hello jest zamknięta i zgłoszony błąd kondycji.
  - Gdy nie ma żadnego limitu czasu na zwracanie z tych metod, natychmiast utraty hello możliwości toowrite tooReliable kolekcji i z tego powodu nie można ukończyć rzeczywistą pracę. Należy zwrócić możliwie jak najszybciej po otrzymaniu żądania anulowania hello jest zalecane. Jeśli usługa nie odpowiada wywołania toothese interfejsu API w rozsądnym czasie, Service Fabric może wymusić przerwanie usługi. Zwykle to tylko odbywa się podczas uaktualniania aplikacji lub gdy usługa jest usuwana. Tego limitu czasu wynosi 15 minut domyślnie.
  - Błędy w hello `OnCloseAsync()` doprowadzi do ścieżki `OnAbort()` wywoływana, która jest możliwość optymalnych ostatniej szansy hello usługi tooclean w górę i zwolnić wszystkie zasoby, które zostały przejęte one.

## <a name="next-steps"></a>Następne kroki
- [Wprowadzenie tooReliable usług](service-fabric-reliable-services-introduction.md)
- [Niezawodne usługi szybki start](service-fabric-reliable-services-quick-start.md)
- [Niezawodne usługi advanced użycia](service-fabric-reliable-services-advanced-usage.md)
