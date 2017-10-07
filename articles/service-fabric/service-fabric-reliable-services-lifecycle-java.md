---
title: "aaaOverview życia hello Azure Usługa sieci szkieletowej niezawodnych usług | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello zdarzenia różnych cyklu życia w sieci szkieletowej usług niezawodne usługi"
services: Service-Fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: pakunapa;
ms.openlocfilehash: 6d48c217d12bc5248c2da57b544aac747cecd872
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

* Podczas uruchamiania
  * Usługi są wykonane
  * Mieć możliwość tooconstruct i zwraca zero lub więcej obiektów nasłuchujących
  * Wszystkie zwracane obiekty nasłuchujące są otwarte, zezwolenie na komunikację z usługą hello
  * metodzie runAsync usługi Hello jest wywoływana, umożliwiając hello toodo usługi długotrwałe lub pracy w tle
* Podczas zamykania
  * toorunAsync przekazany token anulowania Hello została anulowana, a odbiorników hello są zamknięte
  * To znaczy po zakończeniu sam obiekt usługi hello jest niszczone

Szczegóły dotyczące hello są dokładne uporządkowanie tych zdarzeń. W szczególności hello kolejność zdarzeń mogą się nieznacznie zmieniać w zależności od tego, czy hello niezawodnej usługi jest Stateless lub Stateful. Ponadto usługi stanowej, zostały toodeal ze scenariuszem głównej wymiany hello. Podczas tej sekwencji hello rolę podstawową jest przeniesione tooanother repliki (lub wróci) bez usługi hello zamykanie. Na koniec mamy toothink o warunkach błędu lub niepowodzenie.

## <a name="stateless-service-startup"></a>Uruchamianie usługi bezstanowej
Witaj cyklem życia usługi bezstanowej jest bardzo prosta. Poniżej przedstawiono kolejność zdarzeń hello:

1. Witaj usługi jest tworzony
2. Następnie w dwie czynności równoległe stanie:
    - `StatelessService.createServiceInstanceListeners()`jest wywoływany i wszystkie zwracane obiekty nasłuchujące (`CommunicationListener.openAsync()` jest wywoływane dla każdego odbiornika)
    - Witaj w metodzie runAsync usługi (`StatelessService.runAsync()`) jest nazywany
3. Jeśli jest obecny, wywoływana jest metoda onOpenAsync tej usługi hello (w szczególności `StatelessService.onOpenAsync()` jest wywoływana. To jest rzadko zastąpienia, ale jest ona dostępna).

Jest toonote ważna jest kolejność nie między toocreate wywołania hello i otwórz hello odbiorników i runAsync. przed rozpoczęciem runAsync odbiorników Hello może zostać otwarty. Podobnie runAsync może się okazać wywoływane przed odbiorników komunikacji hello są otwarte lub nawet zostały wykonane. Jeśli wymagana jest każdej synchronizacji, jest pozostawiany jako implementujący toohello wykonywania. Typowe rozwiązania:

* Czasami odbiorników nie może działać, dopóki niektóre informacje o utworzeniu lub pracy wykonanej. Dla usług bezstanowych, które zwykle można zrobić pracy w Konstruktorze hello usługi podczas hello `createServiceInstanceListeners()` wywołać, lub jako część konstrukcji hello odbiornika hello, sama.
* Czasami hello kodu w runAsync nie chce toostart dopóki odbiorników hello są otwarte. W takim przypadku niezbędne jest dodatkowe koordynacji. Jednym z typowych rozwiązań jest niektórych flagi w odbiorników hello wskazujący, po zakończeniu, który zaznaczono w runAsync przed kontynuowaniem pracy tooactual.

## <a name="stateless-service-shutdown"></a>Zamykanie usługi bezstanowej
Podczas zamykania usługi bezstanowej powitalne tego samego wzorca występuje tylko w odwrotnej:

1. Równoległe
    - Są zamykane wszystkie otwarte odbiorników (`CommunicationListener.closeAsync()` jest wywoływane dla każdego odbiornika)
    - token anulowania Hello przekazano zbyt`runAsync()` zostało anulowane (sprawdzanie token anulowania hello `isCancelled` właściwość zwraca wartość true i wywołuje hello token `throwIfCancellationRequested` metoda zgłasza `CancellationException`)
2. Raz `closeAsync()` uzupełnia w każdym odbiornika i `runAsync()` również zakończeniu hello usługi `StatelessService.onCloseAsync()` metoda jest wywoływana, jeśli jest obecny (ponownie jest rzadko zastąpienie).
3. Po `StatelessService.onCloseAsync()` zakończeniu obiektu usługi hello jest niszczone

## <a name="notes-on-service-lifecycle"></a>Uwagi dotyczące cyklu życia usług
* Zarówno hello `runAsync()` — metoda i hello `createServiceInstanceListeners` wywołania są opcjonalne. Usługa może mieć ich, zarówno lub nie. Na przykład, jeśli usługa hello ma jego pracy w wywołaniach toouser odpowiedzi, jest niepotrzebna dla niego tooimplement `runAsync()`. Wymagane są tylko hello odbiorników komunikacji i ich skojarzonego kodu. Podobnie tworzenie i zwracanie odbiorników komunikacji jest opcjonalne, ponieważ usługa hello może mieć tylko tła pracy toodo i dlatego tylko musi tooimplement`runAsync()`
* Jest on prawidłowy dla toocomplete usługi `runAsync()` pomyślnie i z powrotem od niego. To nie jest uznawane za stanu błędu i stanowić Praca w tle hello kończenia usługi hello. Dla stanowych usług niezawodnej `runAsync()` może zostać wywołana, jeśli usługa hello nastąpiło obniżenie poziomu z podstawowego i podwyższenia poziomu tooprimary Wstecz.
* Jeśli zamknie usługę `runAsync()` przez zgłaszanie nieoczekiwany wyjątek, to jest błąd obiektu usługi hello jest zamknięta i zgłoszony błąd kondycji.
* Gdy nie ma żadnego limitu czasu na zwracanie z tych metod, natychmiast utraty hello możliwości toowrite i z tego powodu nie można ukończyć rzeczywistą pracę. Należy zwrócić możliwie jak najszybciej po otrzymaniu żądania anulowania hello jest zalecane. Jeśli usługa nie odpowiada wywołania toothese interfejsu API w rozsądnym czasie, Service Fabric może wymusić przerwanie usługi. Zwykle to tylko odbywa się podczas uaktualniania aplikacji lub gdy usługa jest usuwana. Tego limitu czasu wynosi 15 minut domyślnie.
* Błędy w hello `onCloseAsync()` doprowadzi do ścieżki `onAbort()` wywoływana, która jest możliwość optymalnych ostatniej szansy hello usługi tooclean w górę i zwolnić wszystkie zasoby, które zostały przejęte one.

> [!NOTE]
> Niezawodne usługi stanowej nie są obsługiwane w języku java jeszcze.
>
>

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooReliable usług](service-fabric-reliable-services-introduction.md)
* [Niezawodne usługi szybki start](service-fabric-reliable-services-quick-start.md)
* [Niezawodne usługi advanced użycia](service-fabric-reliable-services-advanced-usage.md)
