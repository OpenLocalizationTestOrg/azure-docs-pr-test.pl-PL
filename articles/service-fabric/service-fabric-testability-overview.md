---
title: "Omówienie usług analizy aaaFault | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello usługi analiza błędów w sieci szkieletowej usług dla wywołania usterek i uruchamiania scenariuszy testowania usług."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: vturecek
ms.assetid: 1f064276-293a-4989-a513-e0d0b9fdf703
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: deac16ec830aa10d4e488e60691faa9ef2b6cd33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-fault-analysis-service"></a>Wprowadzenie toohello usługi analiza błędów
Hello błędów Analysis Services jest przeznaczony do testowania usług, które są wbudowane w usługi sieć szkieletowa usług Microsoft Azure. Hello błędów usługi Analysis możesz wywołać znaczenie błędów i uruchom ukończenia testowej scenariusze dla aplikacji. Te błędy i scenariuszy wykonywania i sprawdzania poprawności hello wiele stanów i przejść, które usługa może wystąpić w całym cyklu eksploatacji w sposób kontrolowany, bezpieczne i zgodne.

Akcje są błędy poszczególnych hello przeznaczonych dla usługi do testowania go. Projektant usługi można użyć je jako bloków konstrukcyjnych toowrite skomplikowane scenariuszy. Na przykład:

* Uruchom ponownie toosimulate węzła dowolną liczbę sytuacji, w którym ponownego uruchomienia komputera lub maszyny Wirtualnej.
* Przenieś repliki równoważenia obciążenia toosimulate usługi stanowej, trybu failover, lub uaktualniania aplikacji.
* Wywołaj utraty kworum toocreate usługi stanowej sytuacji, gdy nie można kontynuować operacje zapisu dla, ponieważ nie ma wystarczającej liczby replik "kopii zapasowych" i "secondary" tooaccept nowych danych.
* Wywołanie toocreate usługi stanowej sytuacji, w którym całkowicie wyczyszczeniem wszystkich stanów w pamięci poza utraty danych.

Scenariusze są złożonych operacji składa się z co najmniej jednej akcji. Hello błędów Analysis Services zawiera dwa wbudowane pełne scenariusze:

* Scenariusz chaos
* Scenariusz trybu failover

## <a name="testing-as-a-service"></a>Testowanie jako usługa
Hello błędów Analysis Services to usługa systemu sieci szkieletowej usług, która zostanie automatycznie uruchomiony przy użyciu klastra sieci szkieletowej usług. Ta usługa działa jako host hello iniekcji błędów, wykonywania testów scenariusza i analizy kondycji. 

![Błąd analizy usługi][0]

Po zainicjowaniu akcji lub testu scenariusza błędów polecenia są wysyłane toohello błędów Analysis Service toorun hello błędów akcji lub testu scenariusza. Hello błąd analizy usługi jest obiektem stanowym tak, aby można niezawodnie Uruchom scenariuszy i usterek i Zweryfikuj wyniki. Na przykład scenariusza testu długotrwałe może być niezawodnie wykonywane przez hello usługi analizy błędów. I ponieważ testy są wykonywane w klastrze hello, hello usługi można sprawdzić stan hello hello klastra i tooprovide Twojego usług więcej szczegółowych informacji o awarii.

## <a name="testing-distributed-systems"></a>Testowanie systemów rozproszonych
Sieć szkieletowa usług sprawia, że zadania hello zapisywania i aplikacje skalowalne rozproszone znacznie łatwiejsze zarządzanie. Hello usługi analiza błędów sprawia, że testowanie aplikacji rozproszonej podobnie łatwiejsze. Istnieją trzy główne kwestie, które należy rozwiązać podczas badania toobe:

1. Symuluje/generowanie błędów, które mogą wystąpić w rzeczywistych scenariuszach: jeden hello ważne kwestie związane z sieci szkieletowej usług jest możliwość toorecover aplikacje rozproszone z różnych błędów. Jednak tootest, która aplikacja hello jest możliwe toorecover z tych błędów, potrzebujemy mechanizm toosimulate/generowanie tych błędów rzeczywistych w środowisku testowym kontrolowany.
2. toogenerate możliwości Hello skorelowane błędów: podstawowe błędy w systemie hello, takie jak awarie sieci i błędy maszyn są łatwe tooproduce indywidualnie. Generowanie znaczących scenariusze, które mogą wystąpić w rzeczywistych hello wyniku hello interakcji z tych błędów pojedynczych jest nieuproszczony.
3. Ujednolicone i środowisko na różnych poziomach programowanie i wdrożenie: istnieje wiele systemów iniekcji błędów, które mogą wykonywać różnych typów błędów. Jednak środowisko hello we wszystkich tych jest niska, podczas przechodzenia z jednego pola deweloperów, powitalne toorunning takie same testy w środowisku testowym dużych, toousing je dla testów w środowisku produkcyjnym.

Gdy istnieją wiele mechanizmów toosolve tych problemów, system hello sam wymagane gwarancje — wszystkie sposób hello środowiska deweloperskiego jednego pola tootest w klastrów produkcyjnych — Brak. Hello błędów Analysis Service ułatwia deweloperom aplikacji hello skoncentrować się na temat testowania ich logiki biznesowej. Hello błędów Analysis Services zawiera wszystkie funkcje hello potrzebne interakcji hello tootest hello usługi o podstawowym systemie rozproszonej hello.

### <a name="simulatinggenerating-real-world-failure-scenarios"></a>Symuluje generowania scenariuszy awarii rzeczywistych
niezawodność hello tootest systemu rozproszonego przed awariami, potrzebujemy błędów toogenerate mechanizmu. Gdy teoretycznie generowania awarii, jak węzeł w dół prawdopodobnie łatwe, uruchamia, aktywując hello sam zestaw problemów spójności czy usługi sieci szkieletowej, próbuje toosolve. Na przykład jeśli chcemy tooshut wyłączenia węzła, hello wymaganym przepływu pracy jest hello następujące czynności:

1. W kliencie hello wystawiać żądanie zamknięcia węzła.
2. Wyślij żądanie hello toohello prawidłowego węzła.
   
    a. Jeśli nie znaleziono węzła hello, jeżeli nie.
   
    b. Jeśli węzeł hello zostanie znaleziony, powinien on zwrócić tylko jeśli węzeł hello jest zamknięta.

Błąd hello tooverify z punktu widzenia testu, hello testu musi tooknow, że podczas tego błędu jest wywołane, hello błąd wystąpi. Witaj gwarancji, że Usługa Service Fabric realizuje nie zostanie umieszczona w dół dowolnego węzła hello lub już nie działa, jeśli polecenie hello osiągnięto hello węzła. W albo wielkość hello testu powinien być toocorrectly możliwe przyczyny o stanie hello i powiedzie się lub się nie powieść w jego weryfikacji poprawnie. System zaimplementowana poza hello toodo sieci szkieletowej usług sam zestaw błędów można trafień przez wiele sieci, sprzętu i oprogramowania problemy, które mogłyby uniemożliwiać zapewnienie hello poprzedniego gwarancji. Obecność hello problemów hello wspomniano wcześniej, sieci szkieletowej usług ponownie skonfigurować toowork stanu klastra hello wokół hello problemy, a więc hello błędów usługi Analysis będzie nadal mogli toogive hello prawo ustawiony gwarancji.

### <a name="generating-required-events-and-scenarios"></a>Generowanie zdarzeń wymagane i scenariusze
Spójnie symulację awarii rzeczywistych jest trudnych toostart z, nawet silniejsze jest hello możliwości toogenerate skorelowane błędów. Na przykład utraty danych odbywa się w usługa stanowa utrwalonego, gdy wystąpi hello następujące czynności:

1. Tylko do zapisu kworum replik hello są przechwytywane w na replikację. Wszystkie repliki pomocniczej hello opóźniona hello podstawowego.
2. Witaj zapisu kworum ulegnie awarii z powodu replik hello przechodzi w dół (powodu pakietu kodu tooa lub węzeł przechodzi w dół).
3. Witaj zapisu kworum nie przywracane ponieważ hello dane repliki hello są utracone (z powodu uszkodzenia toodisk lub ponownej instalacji systemu komputera).

Tych błędów skorelowane realizowane w świecie rzeczywistym hello, ale nie tak często, jak poszczególne błędy. bardzo ważne jest Hello tootest możliwości dotyczących następujących scenariuszy, zanim wystąpią w środowisku produkcyjnym. Szczególnie ważne jest toosimulate możliwości hello tych scenariuszy z obciążeń produkcyjnych w warunkach kontrolowanych (hello w środku dnia hello z wszystkich inżynierów w talii). To znacznie lepszą niż go być powitania po raz pierwszy w środowisku produkcyjnym o 2:00

### <a name="unified-experience-across-different-environments"></a>Ujednolicone doświadczenie w różnych środowiskach
praktyki Hello tradycyjnie była toocreate trzy różne zestawy środowiska, dla hello środowisko projektowe dla testów i jeden w środowisku produkcyjnym. Hello model był:

1. W środowisku projektowym hello należy utworzyć przejścia stanu zezwala testów jednostkowych poszczególnych metod.
2. W środowisku testowym hello powodują błędy tooallow end-to-end testy, które korzystają z różnych scenariuszy awarii.
3. Zachowaj tooprevent idealnego środowiska produkcyjnego hello wszelkie błędy naturalny z systemem innym niż i tooensure jest bardzo szybko odpowiedź człowieka toofailure.

W sieci szkieletowej usług, za pośrednictwem hello usługi analiza błędów, możemy są proponowania tooturn to wokół i użyj hello takie same metodologii z tooproduction środowiska dewelopera. Istnieją dwa sposoby tooachieve to:

1. błędy tooinduce kontrolowane, użyj hello interfejsów API usługi analiza błędów w środowisku jednego pola wszystkich tooproduction sposób hello klastrów.
2. Witaj toogive klastra pomoru, powoduje automatyczne wywoływanie błędów, użyj hello błędów Analysis Service toogenerate automatyczne błędów. Kontrolowanie hello współczynnik błędów za pomocą konfiguracji umożliwia hello tej samej usługi toobe przetestowane inaczej w różnych środowiskach.

Z sieci szkieletowej usług chociaż skali hello niepowodzeń będą różne w różnych środowiskach hello mechanizmów rzeczywiste hello będą identyczne. Pozwala to znacznie szybsze wdrażanie kodu potoku i hello możliwości tootest hello usług pod obciążeniem rzeczywistych.

## <a name="using-hello-fault-analysis-service"></a>Przy użyciu hello usługi analiza błędów
**C#**

Funkcji usługi analiza błędów znajdują się w przestrzeni nazw System.Fabric hello w hello pakietu Microsoft.ServiceFabric NuGet. toouse hello błędów Analysis Services, cechy pakietu nuget hello jako odwołanie do projektu.

**PowerShell**

toouse programu PowerShell, należy zainstalować program hello zestawu SDK usług sieci szkieletowej. Po hello, który jest zainstalowany zestaw SDK, hello ServiceFabric programu PowerShell moduł jest automatycznie załadowany na potrzeby toouse użytkownik.

## <a name="next-steps"></a>Następne kroki
toocreate naprawdę usług skali chmury jest krytyczne tooensure przed i po wdrożeniu, że usługi może wytrzymać rzeczywistych błędów. Hello dzisiaj świecie usługi hello tooinnovate możliwości szybkiego i Przenieś kod tooproduction szybko jest bardzo ważne. Hello błędów Analysis Service pomaga toodo deweloperów usługi dokładnie który.

Rozpoczęcie testowania aplikacji i usług przy użyciu wbudowanych hello [przetestować scenariusze](service-fabric-testability-scenarios.md), lub tworzenie własnych scenariuszy testowania przy użyciu hello [fault akcje](service-fabric-testability-actions.md) podał hello usługi analizy błędów.

<!--Image references-->
[0]: ./media/service-fabric-testability-overview/faultanalysisservice.png
