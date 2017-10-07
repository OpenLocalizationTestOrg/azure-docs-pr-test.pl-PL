---
title: "węzły w puli partii zadań Azure obliczeniowe skali aaaAutomatically | Dokumentacja firmy Microsoft"
description: "Włącz automatyczne skalowanie na toodynamically puli chmury Dostosuj hello liczba węzłów obliczeniowych w puli hello."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6d1e0c5d8e0e56e15a4d3588150f2466a689f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a>Utwórz formułę Skalowanie automatyczne skalowanie węzłów obliczeniowych w puli partii

Partia zadań Azure może automatycznie skalować puli na podstawie parametrów zdefiniowanych przez użytkownika. Automatyczne skalowanie partii dynamicznie dodaje puli tooa węzłów jako wzrost wymagań zadań i usuwa jako zmniejszają węzły obliczeniowe. Automatycznie dostosowując hello liczba węzłów obliczeniowych używanych przez aplikację partii można zapisać zarówno czas i pieniądze. 

Możesz włączyć automatyczne skalowanie węzłów obliczeniowych puli można skojarzyć z nim *formułą automatycznego skalowania* zdefiniowana. Hello usługa partia zadań użyje hello skalowania automatycznego formuły toodetermine hello liczby węzłów obliczeniowych, które są potrzebne tooexecute obciążenie. Obliczeniowe węzły mogą być dedykowanych węzłów lub [węzłów niskiego priorytetu](batch-low-pri-vms.md). Wsadowe odpowiada okresowo zbieranych danych metryki tooservice. Przy użyciu tych danych metryki, partii dopasowuje hello liczba węzłów obliczeniowych w puli hello na podstawie formuły i interwałem można konfigurować.

Można włączyć automatyczne skalowanie, gdy tworzona jest pula lub na istniejącej puli. Można również zmienić istniejącej formuły w puli, która jest skonfigurowana dla Skalowanie automatyczne. Wsadowe umożliwia tooevaluate formuł przed przypisaniem ich automatyczne skalowanie toopools i toomonitor stan hello jest uruchamiana.

W tym artykule omówiono hello różnymi jednostkami wchodzące w skład formułach skalowania automatycznego, w tym zmienne, operatory, operacje i funkcje. Omówiono sposób tooobtain różnych obliczeniowe metryki zasób i zadanie w partii. Możesz użyć tych tooadjust metryki liczba węzłów z puli na podstawie zasobów użycia i zadania stanu. Następnie opisano, jak tooconstruct formuły i Włącz automatyczne skalowanie w puli przy użyciu zarówno hello REST partii i interfejsów API architektury .NET. Na koniec kończymy z kilku przykład formuły.

> [!IMPORTANT]
> Podczas tworzenia konta usługi partia zadań można określić hello [konfiguracji konta](batch-api-basics.md#account), która określa, czy pule są przydzielane w ramach subskrypcji usługi partii (hello ustawienie domyślne) lub w ramach subskrypcji użytkownika. Twoje konto jest ograniczone tooa maksymalna liczba rdzeni, które mogą być używane do przetwarzania, utworzeniu konta partii zadań z hello domyślnej usługi partia zadań konfiguracji. Usługa partia zadań Hello skaluje węzły obliczeniowe tylko się limit rdzeni toothat. Z tego powodu hello docelowej liczby węzłów obliczeniowych określony formułą automatycznego skalowania nie może skontaktować się hello usługa partia zadań. Zobacz [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md) informacji na temat przeglądania i zwiększenie przydziały Twojego konta.
>
>Jeśli Twoje konto zostało utworzone z konfiguracją subskrypcji użytkownika hello, Twoje konto udziałów w limit przydziału rdzeni hello hello subskrypcji. Aby uzyskać więcej informacji, zobacz sekcję [Virtual Machines limits (Limity maszyn wirtualnych)](../azure-subscription-service-limits.md#virtual-machines-limits) w artykule [Azure subscription and service limits, quotas, and constraints (Ograniczenia, przydziały i limity usług i subskrypcji platformy Azure)](../azure-subscription-service-limits.md).
>
>

## <a name="automatic-scaling-formulas"></a>Automatyczne skalowanie formuł
Formuła skalowania automatycznego jest wartość ciągu przez Ciebie, która zawiera jedną lub więcej instrukcji. formułą automatycznego skalowania Hello jest przypisany puli tooa [autoScaleFormula] [ rest_autoscaleformula] elementu (REST partii) lub [CloudPool.AutoScaleFormula] [ net_cloudpool_autoscaleformula] Właściwość (partiami platformy .NET). Hello usługa partia zadań używa formuły toodetermine hello docelowej liczby węzłów obliczeniowych w puli hello hello następnym interwale czasowym przetwarzania. Witaj formuły ciąg nie może być dłuższa niż 8 KB, mogą obejmować się too100 instrukcji, które są oddzielone średnikami i może zawierać podziałów wierszy i komentarze.

Można traktować automatycznego skalowania formuł jako skalowania automatycznego partii "język". Instrukcje formuły są wolne sformułowanych wyrażeń zawierających zarówno usługa zdefiniowana zmiennych (zmiennych zdefiniowanych przez usługi partia zadań hello), jak i zmienne zdefiniowane przez użytkownika (zmiennych zdefiniowanych przez użytkownika). Mogą oni wykonywać różne operacje tych wartości za pomocą wbudowanych typów, Operatorzy i funkcje. Na przykład instrukcja może potrwać hello następującej postaci:

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

Formuły zwykle zawierają wiele instrukcji, które wykonują operacje na wartości, które zostały uzyskane w poprzednim instrukcje. Na przykład, najpierw możemy uzyskać wartości `variable1`, następnie przekazać go toopopulate funkcja tooa `variable2`:

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

Dołącz te instrukcje użytkownika skalowania automatycznego tooarrive formuły docelowej liczby węzłów obliczeniowych. Dedykowanych węzłów, jak i węzły niskiego priorytetu mają własnych ustawień obiektu docelowego, dzięki czemu można zdefiniować docelowy dla każdego typu węzła. Formuła automatycznego skalowania może zawierać wartość docelowa dla dedykowanych węzłów i/lub wartość docelowa dla węzłów o niskim priorytecie.

Hello docelowej liczby węzłów może można wyższe, niższe lub hello identyczny hello bieżąca liczba węzłów w puli hello tego typu. Wsadowe ocenia formułą automatycznego skalowania puli w określonych odstępach czasu (zobacz [automatyczne skalowanie interwałów](#automatic-scaling-interval)). Wsadowe dopasowuje hello docelowy liczbę każdego typu węzła w hello puli toohello liczba, która określa formułę automatycznego skalowania w czasie hello oceny.

### <a name="sample-autoscale-formula"></a>Przykładowa formuła skalowania automatycznego

Oto przykład formuły automatycznego skalowania, które mogą być dostosowane toowork dla większości scenariuszy. Witaj zmienne `startingNumberOfVMs` i `maxNumberofVMs` w hello przykład formuły może być dostosowane tooyour potrzeb. W tej formule skaluje dedykowanych węzłów, ale może być zmodyfikowany tooapply tooscale niskiego priorytetu również węzłów. 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

Tą formułą automatycznego skalowania puli hello został początkowo utworzony z jednej maszyny Wirtualnej. Witaj `$PendingTasks` Metryka definiuje hello liczbę zadań, które są uruchomione lub umieszczonych w kolejce. Formuła Hello znalezieniu hello średnią liczbę oczekujących zadań hello ostatnich 180 sekund i ustawia hello `$TargetDedicatedNodes` zmiennej odpowiednio. Formuła Hello gwarantuje, że hello docelowy Liczba dedykowanych węzłów nigdy nie przekracza 25 maszyn wirtualnych. Nowe zadania zostały przesłane, automatycznie zwiększa rozmiar puli hello. Jako zakończenie zadania wolnego jeden po drugim stają się maszyn wirtualnych i formuła Skalowanie automatyczne hello zmniejszana hello puli.

## <a name="variables"></a>Zmienne
Można użyć zarówno **usługa zdefiniowana** i **zdefiniowane przez użytkownika** zmiennych w formułach skalowania automatycznego. zmienne zdefiniowane przez usługę Hello są wbudowane w toohello usługa partia zadań. Niektóre zmienne zdefiniowane usługi są odczytu i zapisu, a niektóre są tylko do odczytu. Zmienne zdefiniowane przez użytkownika są zmiennych zdefiniowanych przez użytkownika. W formule przykład hello pokazana w poprzedniej sekcji hello `$TargetDedicatedNodes` i `$PendingTasks` są zmienne zdefiniowane przez usługę. Zmienne `startingNumberOfVMs` i `maxNumberofVMs` są zmienne zdefiniowane przez użytkownika.

> [!NOTE]
> Zmienne zdefiniowane przez usługi są zawsze poprzedzone znak dolara ($). W przypadku zmiennych zdefiniowanych przez użytkownika dolara hello jest opcjonalna.
>
>

następujące tabele Hello Pokaż zarówno do odczytu / zapisu i zmienne tylko do odczytu, które są zdefiniowane przez hello usługa partia zadań.

Możesz pobrać i ustawić hello wartości tych zmiennych zdefiniowanych przez usługę toomanage hello liczbę węzłów obliczeniowych w puli:

| Zmienne zdefiniowane przez usługę do odczytu / zapisu | Opis |
| --- | --- |
| $TargetDedicatedNodes |Witaj docelowy Liczba dedykowanych obliczeniowe węzłów hello puli. Hello Liczba dedykowanych węzłów jest określony jako element docelowy, ponieważ pula nie zawsze będzie hello żądaną liczbę węzłów. Na przykład jeśli hello docelowy Liczba dedykowanych węzłów jest modyfikowany przez ocenę automatycznego skalowania przed hello puli osiągnęła początkowej docelowy hello, a następnie hello puli nie może skontaktować się docelowy hello. <br /><br /> Pulą konto utworzone z konfiguracją usługi partia zadań hello nie może osiągnąć elementem docelowym, jeśli docelowy hello przekracza przydział węzła lub core konta wsadowego. Puli w ramach konta utworzone za pomocą konfiguracji subskrypcji użytkownika hello nie może osiągnąć elementem docelowym, jeśli docelowy hello przekracza przydział udostępnionego core hello hello subskrypcji.|
| $TargetLowPriorityNodes |numer docelowej Hello o niskim priorytecie obliczeniowe węzłów hello puli. Hello liczba węzłów niskiego priorytetu jest określony jako element docelowy ponieważ puli nie zawsze będzie hello żądaną liczbę węzłów. Na przykład jeśli hello docelowej liczby węzłów niskiego priorytetu jest modyfikowany przez ocenę automatycznego skalowania przed hello puli osiągnęła początkowej docelowy hello, a następnie hello puli nie może skontaktować się hello docelowej. Pulę również może nie będzie elementem docelowym, jeśli docelowy hello przekracza przydział węzła lub core konta wsadowego. <br /><br /> Aby uzyskać więcej informacji na węzłach obliczeniowych niskiego priorytetu, zobacz [niskiego priorytetu maszyn wirtualnych za pomocą partii (wersja zapoznawcza)](batch-low-pri-vms.md). |
| $NodeDeallocationOption |Witaj akcja, która występuje, gdy węzły obliczeniowe są usuwane z puli. Możliwe wartości:<ul><li>**requeue**--natychmiast kończy zadań i umieszczane w kolejce zadań hello, dzięki czemu są one zmienił.<li>**przerwanie**— natychmiast kończy zadań i usuwa je z hello kolejki zadań.<li>**taskcompletion**--oczekuje aktualnie uruchomione zadania toofinish, a następnie usuwa węzła hello hello puli.<li>**retaineddata**--czeka na wszystkich hello zachowane zadania dane lokalne na powitania węzła toobe wyczyszczone przed usunięciem z puli hello hello węzła.</ul> |

Można pobrać wartości hello dostosowania toomake tych zmiennych zdefiniowanych przez usługi, które są oparte na metryki z usługi partia zadań hello:

| Zmienne tylko do odczytu usługa zdefiniowana | Opis |
| --- | --- |
| $CPUPercent |Witaj średnią wartość procentową użycia procesora CPU. |
| $WallClockSeconds |Witaj liczbę sekund, używane. |
| $MemoryBytes |Witaj średnia liczba megabajtów używane. |
| $DiskBytes |Średnia liczba Hello gigabajtów używane na dyski lokalne powitania. |
| $DiskReadBytes |Witaj liczba bajtów odczytanych. |
| $DiskWriteBytes |Witaj liczba zapisanych bajtów. |
| $DiskReadOps |wykonać Hello liczba operacji odczytu dysku. |
| $DiskWriteOps |Liczba Hello zapisu dysku operacji. |
| $NetworkInBytes |Witaj liczba bajtów przychodzących. |
| $NetworkOutBytes |Witaj liczba bajtów wychodzących. |
| $SampleNodeCount |Witaj liczba węzłów obliczeniowych. |
| $ActiveTasks |Witaj liczba zadań, które są gotowe tooexecute, ale nie są jeszcze wykonywany. Licznik Hello $ActiveTasks obejmuje wszystkie zadania, które znajdują się w stanie aktywnym hello i którego zależności zostały spełnione. Wszystkie zadania, które są w stanie aktywnym hello, ale zależności, których nie zostały spełnione są wykluczone z hello $ActiveTasks count.|
| $RunningTasks |Witaj liczba zadań w stanie uruchomienia. |
| $PendingTasks |Suma Hello $ActiveTasks i $RunningTasks. |
| $SucceededTasks |Witaj liczba zadań, które zakończyło się pomyślnie. |
| $FailedTasks |Witaj liczba zadań, których nie powiodła się. |
| $CurrentDedicatedNodes |węzły obliczeniowe Hello bieżąca liczba dedykowanych. |
| $CurrentLowPriorityNodes |Bieżąca liczba niskiego priorytetu Hello obliczeniowe węzły, w tym wszystkie węzły, które zostały opóźnieniem. |
| $PreemptedNodeCount | Hello liczby węzłów w puli hello, które są w stanie opóźnieniem. |

> [!TIP]
> Witaj tylko do odczytu, usługa zdefiniowana zmiennych, które są wyświetlane w poprzedniej tabeli hello są *obiektów* zawierających różne metody tooaccess danych skojarzonych z każdym z nich. Aby uzyskać więcej informacji, zobacz [uzyskać przykładowe dane](#getsampledata) dalszej części tego artykułu.
>
>

## <a name="types"></a>Typy
Te typy są obsługiwane w formule:

* O podwójnej precyzji
* doubleVec
* doubleVecList
* Ciąg
* Sygnatura czasowa — sygnatura czasowa jest złożone struktury, która zawiera następujące elementy członkowskie hello:

  * Roku
  * miesiąc (1-12)
  * dzień (1-31)
  * dzień tygodnia (w formacie hello numeru; na przykład 1, od poniedziałku)
  * Godzina (w formacie liczby 24-godzinnym; na przykład 13 oznacza 13: 00)
  * minut (00 do 59)
  * drugie (00 do 59)
* parametru TimeInterval

  * TimeInterval_Zero
  * TimeInterval_100ns
  * TimeInterval_Microsecond
  * TimeInterval_Millisecond
  * TimeInterval_Second
  * TimeInterval_Minute
  * TimeInterval_Hour
  * TimeInterval_Day
  * TimeInterval_Week
  * TimeInterval_Year

## <a name="operations"></a>Operacje
Te operacje są dozwolone w typach hello, które są wymienione w poprzedniej sekcji hello.

| Operacja | Operatory obsługiwane | Typ wyniku |
| --- | --- | --- |
| Podwójna *operator* podwójne |+, -, *, / |O podwójnej precyzji |
| Podwójna *operator* parametru timeinterval |* |parametru TimeInterval |
| doubleVec *operator* podwójne |+, -, *, / |doubleVec |
| doubleVec *operator* doubleVec |+, -, *, / |doubleVec |
| parametru TimeInterval *operator* podwójne |*, / |parametru TimeInterval |
| parametru TimeInterval *operator* parametru timeinterval |+, - |parametru TimeInterval |
| parametru TimeInterval *operator* sygnatury czasowej |+ |sygnatura czasowa |
| Sygnatura czasowa *operator* parametru timeinterval |+ |sygnatura czasowa |
| Sygnatura czasowa *operator* sygnatury czasowej |- |parametru TimeInterval |
| *operator*podwójne |-, ! |O podwójnej precyzji |
| *operator*parametru timeinterval |- |parametru TimeInterval |
| Podwójna *operator* podwójne |<, <=, ==, >=, >, != |O podwójnej precyzji |
| ciąg *operator* ciągu |<, <=, ==, >=, >, != |O podwójnej precyzji |
| Sygnatura czasowa *operator* sygnatury czasowej |<, <=, ==, >=, >, != |O podwójnej precyzji |
| parametru TimeInterval *operator* parametru timeinterval |<, <=, ==, >=, >, != |O podwójnej precyzji |
| Podwójna *operator* podwójne |&&, &#124;&#124; |O podwójnej precyzji |

Podczas testowania wartość o podwójnej precyzji z trójargumentowy (`double ? statement1 : statement2`), jest różna od zera jest **true**, i zero jest **false**.

## <a name="functions"></a>Funkcje
Te wstępnie zdefiniowane **funkcje** są dostępne dla toouse podczas definiowania automatycznego skalowania formuły.

| Funkcja | Zwracany typ | Opis |
| --- | --- | --- |
| AVG(doubleVecList) |O podwójnej precyzji |Zwraca hello średnią wartość dla wszystkich wartości w hello doubleVecList. |
| Len(doubleVecList) |O podwójnej precyzji |Zwraca hello długość wektora hello, utworzona na podstawie hello doubleVecList. |
| LG(Double) |O podwójnej precyzji |Zwraca dziennik hello podstawie 2 hello dwa razy. |
| LG(doubleVecList) |doubleVec |Zwraca podstawie 2 hello doubleVecList hello component-wise dziennika. Vec(double) muszą być jawnie przekazywane hello parametru. W przeciwnym razie przyjęto hello podwójne lg(double) wersji. |
| ln(Double) |O podwójnej precyzji |Zwraca hello logarytm naturalny z hello dwa razy. |
| ln(doubleVecList) |doubleVec |Zwraca podstawie 2 hello doubleVecList hello component-wise dziennika. Vec(double) muszą być jawnie przekazywane hello parametru. W przeciwnym razie przyjęto hello podwójne lg(double) wersji. |
| log(Double) |O podwójnej precyzji |Zwraca dziennik hello podstawie 10 hello dwa razy. |
| log(doubleVecList) |doubleVec |Zwraca dziennik component-wise hello hello doubleVecList o podstawie 10. Vec(double) muszą być jawnie przekazywane hello jednego parametru dwa razy. W przeciwnym razie przyjęto hello podwójne log(double) wersji. |
| MAX(doubleVecList) |O podwójnej precyzji |Zwraca hello maksymalnej wartości w hello doubleVecList. |
| min(doubleVecList) |O podwójnej precyzji |Zwraca hello minimalnej wartości w hello doubleVecList. |
| norm(doubleVecList) |O podwójnej precyzji |Zwraca hello normy dwóch wektorów hello, utworzona na podstawie hello doubleVecList. |
| percentyl (v doubleVec podwójne p) |O podwójnej precyzji |Zwraca hello percentyl elementu hello wektor v. |
| RAND() |O podwójnej precyzji |Zwraca wartość losowe od 0,0 do 1,0. |
| Range(doubleVecList) |O podwójnej precyzji |Zwraca różnicę hello hello min i max wartości hello doubleVecList. |
| STD(doubleVecList) |O podwójnej precyzji |Zwraca hello przykładowe odchylenie standardowe wartości hello w hello doubleVecList. |
| stop() | |Zatrzymuje obliczania wyrażenia Skalowanie automatyczne hello. |
| sum(doubleVecList) |O podwójnej precyzji |Zwraca hello sumę wszystkich składników hello hello doubleVecList. |
| czas (string, dateTime = "") |sygnatura czasowa |Zwraca bieżący czas sygnaturę czasową hello hello Jeśli żadne parametry są przekazywane lub hello sygnaturę czasową hello ciąg daty i godziny, jeśli został przekazany. Formaty obsługiwanych dateTime są W3C DTF i RFC 1123. |
| Val (v doubleVec i dwa razy) |O podwójnej precyzji |Zwraca wartość hello hello elementu, który znajduje się w lokalizacji i w przypadku wektora v z indeksem początkowej zero. |

Niektóre funkcje hello, które zostały opisane w poprzedniej tabeli hello zaakceptować listy jako argument. rozdzielana przecinkami lista Hello jest dowolną kombinację *podwójne* i *doubleVec*. Na przykład:

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

Witaj *doubleVecList* wartość przekonwertowanego tooa pojedynczego *doubleVec* przed oceny. Na przykład jeśli `v = [1,2,3]`, wywołując `avg(v)` jest równoważne toocalling `avg(1,2,3)`. Wywoływanie `avg(v, 7)` jest równoważne toocalling `avg(1,2,3,7)`.

## <a name="getsampledata"></a>Uzyskaj przykładowe dane
Funkcja automatycznego skalowania formuły działają na metryki danych (przykłady) dostarczonego przez hello usługa partia zadań. Formuła rozwoju lub zmniejszenie rozmiaru puli na podstawie wartości hello, uzyskiwanych od hello usługi. Definicja usługi zmiennych Hello, które zostały opisane wcześniej są obiekty, które zapewniają różne metody tooaccess dane skojarzone z tym obiektem. Na przykład hello poniższy przykład pokazuje hello tooget żądania ostatnich pięciu minut użycia procesora CPU:

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| Metoda | Opis |
| --- | --- |
| GetSample() |Witaj `GetSample()` metoda zwraca wektor próbek danych.<br/><br/>Przykładowe wynosi 30 sekund warto danych metryki. Innymi słowy przykłady są uzyskiwane co 30 sekund. Ale przypadków wymienionych poniżej, opóźnienie między po próbki są zbierane i gdy jest dostępne tooa formuły. Tak nie wszystkie przykłady w danym czasie może być dostępny do szacowania przez formułę.<ul><li>`doubleVec GetSample(double count)`<br/>Określa liczbę hello tooobtain próbki z hello najnowsze przykłady, które zostały zebrane.<br/><br/>`GetSample(1)`Zwraca hello ostatniej próbki dostępne. Dla metryk, takich jak `$CPUPercent`, jednak to nie można używać ponieważ jest niemożliwe tooknow *podczas* próbki hello został zebrany. Może być ostatnie lub z powodu problemów dotyczących systemu, może być znacznie starsza. Najlepiej w takich przypadkach toouse przedział czasu, jak pokazano poniżej.<li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/>Określa przedział czasu zbierania przykładowych danych. Opcjonalnie określa również hello wartość procentowa próbek, które muszą być dostępne w hello żądanej przedziale czasu.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10)`zwróci 20 próbek, gdy wszystkie próbki dla hello ostatnich 10 minut znajdują się w historii CPUPercent hello. Jeśli hello ostatniej minuty historii nie jest dostępna, jednak tylko 18 przykłady będzie zwracany. W takim przypadku:<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`nie powiedzie się, ponieważ tylko 90 procent hello przykłady są dostępne.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)`powiedzie się.<li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/>Określa przedział czasu zbierania danych z godziny rozpoczęcia i godzina zakończenia.<br/><br/>Jak wcześniej wspomniano, istnieje opóźnienie między po próbki są zbierane i gdy jest dostępne tooa formuły. Należy wziąć pod uwagę to opóźnienie używania hello `GetSample` metody. Zobacz `GetSamplePercent` poniżej. |
| GetSamplePeriod() |Zwraca okres hello próbek, które zostały wykonane w zestawie danych historycznych próbki. |
| Funkcji Count() |Zwraca hello łączna liczba próbek w historii metryki hello. |
| HistoryBeginTime() |Zwraca hello sygnaturę czasową hello najstarsze dostępne dane przykładowe hello metryki. |
| GetSamplePercent() |Zwraca hello wartość procentowa próbek, które są dostępne dla danego interwału. Na przykład:<br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/>Ponieważ hello `GetSample` metody zakończy się niepowodzeniem, jeśli hello wartość procentowa próbek, zwracana jest mniejsza niż hello `samplePercent` określony, można użyć hello `GetSamplePercent` toocheck metody pierwszy. Następnie można wykonać akcję alternatywną, jeśli brakuje przykłady są obecne, bez zatrzymania hello automatycznego skalowania oceny. |

### <a name="samples-sample-percentage-and-hello-getsample-method"></a>Przykłady, wartość procentowa próbki i hello *GetSample()* — metoda
Hello podstawowej funkcjonalności formuły skalowania automatycznego jest tooobtain zadania i zasobu metryki danych, a następnie Dostosuj rozmiaru puli na podstawie tych danych. Tak to ważne toohave przejrzysty sposób skalowania automatycznego formuły interakcji z metryki danych (przykłady).

**Przykłady**

Hello usługa partia zadań okresowo przyjmuje przykłady metryki zadań i zasobów i ich dokonuje dostępne tooyour skalowania automatycznego formuły. Te przykłady są rejestrowane co 30 sekund, przez hello usługa partia zadań. Istnieje jednak zwykle opóźnienia między kiedy te przykłady zostały zarejestrowane oraz w przypadku ich stają się dostępne zbyt (i może zostać odczytany przez) formułach skalowania automatycznego. Ponadto powodu toovarious czynników, takich jak sieci lub inne problemy z infrastrukturą, próbki mogą nie zostać zarejestrowane dla określonego interwału.

**Przykładowe wartości procentowej**

Gdy `samplePercent` jest przekazywany toohello `GetSample()` metody lub hello `GetSamplePercent()` metoda jest wywoływana, _procent_ odwołuje się tooa porównanie hello całkowitą możliwą liczbę próbek, które są rejestrowane przez hello usługa partia zadań i Hello liczba próbek, które są dostępne tooyour formuła skalowania automatycznego.

Na przykład Przyjrzyjmy timespan 10 minut. Ponieważ próbki są rejestrowane co 30 sekund w timespan 10 minut, hello maksymalna liczba próbek, które są rejestrowane przez partię będzie 20 próbek (2 na minutę). Jednak powodu toohello związanego z używaniem opóźnienia hello raportowania mechanizmu i inne problemy w systemie Azure, może być tylko 15 przykłady, które są dostępne tooyour skalowania automatycznego formułę do odczytu. Tak na przykład, w tym okresie 10 minut tylko 75% hello łączna liczba próbek, zarejestrowane może być dostępne tooyour formuły.

**Zakresy GetSample() i próbki**

Formułach skalowania automatycznego są będzie toobe powiększania i zmniejszanie z pul &mdash; Dodawanie węzłów i usuwanie węzłów. Ponieważ węzłów koszt pieniądze, ma tooensure, który formułach Użyj inteligentnego metody analizy, który jest oparty na wystarczającą ilość danych. Dlatego zaleca się używać analizy typu analizy trendów w formułach. Ten typ rozwoju i zmniejsza z puli na podstawie zakresu zbieranych próbek.

tak, użyj toodo `GetSample(interval look-back start, interval look-back end)` tooreturn wektor próbek:

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

Gdy hello powyżej wiersza jest oceniane w partii, zwraca zakres próbek jako wektor wartości. Na przykład:

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

Po zostały zebrane wektor hello próbek, można następnie użyć funkcji, takich jak `min()`, `max()`, i `avg()` tooderive istotnych wartości z hello zbierane zakresu.

Aby dodatkowo zwiększyć bezpieczeństwo można wymusić toofail formuły, jeśli mniejsza niż określony procent próbki jest dostępna w określonym czasie. Po wymuszeniu toofail formuły, poinstruuj dalsze toocease partii oceny formuły hello Jeśli hello określona wartość procentowa próbek nie jest dostępny. W takim przypadku rozmiar puli toohello są wprowadzane żadne zmiany. toospecify wymagane odsetek próbek toosucceed oceny hello, określ go jako zbyt hello trzeci parametr`GetSample()`. W tym miejscu określono wymaganie 75 procent próbek:

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

Ponieważ próbki dostępności może wystąpić opóźnienie, ważne jest tooalways określić zakres czasu, czas rozpoczęcia wygląd Wstecz, która jest starsza niż minuta. Trwa około minuty toopropagate próbek za pomocą systemu hello, więc przykłady w zakresie hello `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` mogą nie być dostępne. Ponownie, można użyć parametru procent hello `GetSample()` tooforce wymaganie procent określonej próbki.

> [!IMPORTANT]
> Firma Microsoft **zdecydowanie zaleca się** że **uniknąć jednostki uzależnionej *tylko* na `GetSample(1)` w formułach skalowania automatycznego**. Jest to spowodowane `GetSample(1)` zasadniczo mówi toohello usługa partia zadań, "Mnie hello ostatniej próbki, należy podać nie niezależnie od tego, jak dawno temu pobraniu." Ponieważ jest tylko jeden przykład i mogą być starsze próbki, nie może być przedstawiciel hello większy obraz ostatnie zadanie lub stan zasobów. Jeśli używasz `GetSample(1)`, upewnij się, że jest ona częścią większej instrukcji i nie hello tylko punkt danych zależy od formuły.
>
>

## <a name="metrics"></a>Metryki
Podczas definiowania formuły, można użyć zarówno zasobów, jak i zadanie metryki. Możesz dostosować hello docelowy Liczba dedykowanych węzłów w hello puli na podstawie danych metryki hello uzyskać i oceny. Zobacz hello [zmienne](#variables) sekcji powyżej, aby uzyskać więcej informacji na wszystkie metryki.

<table>
  <tr>
    <th>Metryka</th>
    <th>Opis</th>
  </tr>
  <tr>
    <td><b>Zasób</b></td>
    <td><p>Metryki zasobów są oparte na hello procesora CPU, przepustowości hello, użycie pamięci hello węzłów obliczeniowych i hello liczba węzłów.</p>
        <p> Te zmienne zdefiniowane usługi są przydatne do korekt na podstawie liczby węzłów:</p>
    <p><ul>
            <li>$TargetDedicatedNodes</li>
            <li>$TargetLowPriorityNodes</li>
            <li>$CurrentDedicatedNodes</li>
            <li>$CurrentLowPriorityNodes</li>
            <li>$preemptedNodeCount</li>
            <li>$SampleNodeCount</li>
    </ul></p>
    <p>Te zmienne zdefiniowane usługi są przydatne do korekt na podstawie użycia zasobów węzła:</p>
    <p><ul>
      <li>$CPUPercent</li>
      <li>$WallClockSeconds</li>
      <li>$MemoryBytes</li>
      <li>$DiskBytes</li>
      <li>$DiskReadBytes</li>
      <li>$DiskWriteBytes</li>
      <li>$DiskReadOps</li>
      <li>$DiskWriteOps</li>
      <li>$NetworkInBytes</li>
      <li>$NetworkOutBytes</li></ul></p>
  </tr>
  <tr>
    <td><b>Zadanie podrzędne</b></td>
    <td><p>Metryki zadań opartych na powitania stan zadania, takie jak aktywny, oczekujące i zakończone. Hello następujące zmienne zdefiniowane przez usługi są przydatne, aby wprowadzić zmiany rozmiaru puli, w oparciu metryki zadań:</p>
    <p><ul>
      <li>$ActiveTasks</li>
      <li>$RunningTasks</li>
      <li>$PendingTasks</li>
      <li>$SucceededTasks</li>
            <li>$FailedTasks</li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a>Pisanie formuły skalowania automatycznego
Tworzenie formułą automatycznego skalowania przez tworzenie instrukcji używających hello powyżej składniki następnie łączenie tych instrukcji do ukończenia formuły. W tej sekcji utworzymy skalowania automatycznego przykład formuły, które można wykonywać pewne decyzje skalowania rzeczywistych.

Najpierw zdefiniujmy hello wymagania dotyczące naszej nowej formuły skalowania automatycznego. Formuła Hello następujące czynności:

1. Jeśli użycie procesora CPU jest wysokie, należy zwiększyć liczbę docelowych hello węzłów obliczeniowych dedykowanych w puli.
2. Zmniejszenie liczby docelowy hello węzłów obliczeniowych dedykowanych w puli, gdy użycie Procesora jest niskie.
3. Zawsze ograniczyć hello maksymalna liczba dedykowanych węzłów too400.

tooincrease hello liczba węzłów podczas wysokiego użycia procesora CPU, zdefiniuj hello instrukcji, która wypełnia zmiennej zdefiniowanej przez użytkownika (`$totalDedicatedNodes`) z wartością, która jest 110 procent hello bieżący numer docelowej dedykowanych węzłów, ale tylko wtedy, jeśli hello minimalna średniego użycia procesora CPU Podczas hello ostatnich 10 minut była powyżej 70 procent. W przeciwnym razie użyj wartości hello hello bieżąca liczba dedykowanych węzłów.

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

zbyt*zmniejszyć* hello Liczba dedykowanych węzłów podczas niskie użycie procesora CPU, same hello następnej instrukcji w naszym hello formuły zestawy `$totalDedicatedNodes` zmiennej too90 procent hello bieżący numer docelowej dedykowanych węzłów, jeśli hello średnie użycie procesora CPU w hello ostatnich 60 minut w obszarze było 20 procent. W przeciwnym razie użyj hello bieżącą wartość `$totalDedicatedNodes` który mamy wypełniony w instrukcji hello powyżej.

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

Teraz Ogranicz liczbę docelowych hello obliczeń dedykowanych węzłów tooa maksymalnie 400:

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

Oto hello całej formuły:

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a>Utwórz pulę włączona funkcja automatycznego skalowania z platformą .NET

toocreate pulą o Skalowanie automatyczne włączona w programie .NET, wykonaj następujące kroki:

1. Tworzenie puli hello z [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool).
2. Zestaw hello [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) właściwości zbyt`true`.
3. Zestaw hello [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) właściwości z formułą automatycznego skalowania.
4. (Opcjonalnie) Zestaw hello [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) właściwość (wartość domyślna to 15 minut).
5. Zatwierdź puli hello z [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) lub [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync).

Witaj poniższy fragment kodu tworzy włączona funkcja automatycznego skalowania puli .NET. Witaj formułą automatycznego skalowania puli ustawia hello docelowy liczbę too5 dedykowanych węzłów w poniedziałek i 1 dla każdego dnia, tygodnia hello. Witaj [interwał automatycznego skalowania](#automatic-scaling-interval) jest ustawiony too30 minut. W tym i hello innych wstawki C# w tym artykule `myBatchClient` jest prawidłowo zainicjowany wystąpieniem hello [BatchClient] [ net_batchclient] klasy.

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool(
                    poolId: "mypool",
                    virtualMachineSize: "small", // single-core, 1.75 GB memory, 225 GB disk
                    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));    
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
await pool.CommitAsync();
```

> [!IMPORTANT]
> Podczas tworzenia puli włączone skalowania automatycznego nie należy określać hello _targetDedicatedComputeNodes_ parametr lub hello _targetLowPriorityComputeNodes_ parametru na powitania wywołać zbyt **CreatePool**. Zamiast tego określ hello **AutoScaleEnabled** i **AutoScaleFormula** we właściwościach puli hello. Hello wartości tych właściwości określić numer docelowej hello każdego typu węzła. Ponadto toomanually zmiany rozmiaru puli włączone skalowania automatycznego (na przykład z [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), pierwszy **wyłączyć** automatyczne skalowanie na Witaj puli, a następnie zmienić jego rozmiar.
>
>

Ponadto tooBatch .NET możesz można użyć dowolnego z hello innych [wsadowego zestawów SDK](batch-apis-tools.md#azure-accounts-for-batch-development), [REST partii](https://docs.microsoft.com/rest/api/batchservice/), [poleceń cmdlet programu PowerShell partii](batch-powershell-cmdlets-get-started.md)i hello [CLI partii](batch-cli-get-started.md)tooconfigure Skalowanie automatyczne.


### <a name="automatic-scaling-interval"></a>Interwał automatycznego skalowania
Domyślnie usługa partia zadań hello dopasowuje rozmiaru puli zgodnie z tooits formułą automatycznego skalowania co 15 minut. Interwał ten jest można skonfigurować przy użyciu następujących właściwościach puli hello:

* [CloudPool.AutoScaleEvaluationInterval] [ net_cloudpool_autoscaleevalinterval] (wsadowe .NET)
* [autoScaleEvaluationInterval] [ rest_autoscaleinterval] (interfejsu API REST)

minimalny interwał Hello to pięć minut, a maksymalna hello jest 168 godzin. Jeśli określono interwał poza tym zakresem, hello usługa partia zadań zwrócą błąd nieprawidłowe żądanie (400).

> [!NOTE]
> Skalowanie automatyczne nie jest obecnie zamierzone toorespond toochanges w mniej niż minutę, ale jest raczej przeznaczona tooadjust hello rozmiar puli stopniowo Uruchom obciążenia.
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a>Włącz funkcję skalowania automatycznego na istniejącej puli

Zestaw SDK każdej partii oferuje Skalowanie automatyczne tooenable sposób. Na przykład:

* [BatchClient.PoolOperations.EnableAutoScaleAsync] [ net_enableautoscaleasync] (wsadowe .NET)
* [Włącz automatyczne skalowanie w puli] [ rest_enableautoscale] (interfejsu API REST)

Po włączeniu Skalowanie automatyczne w istniejącej puli, należy pamiętać hello następujące punkty:

* Jeśli automatyczne skalowanie jest obecnie wyłączona w puli hello podczas generowania Skalowanie automatyczne tooenable żądania hello, należy określić formułę prawidłowy automatycznego skalowania w przypadku wysyłania żądania hello. Opcjonalnie można określić interwał oceny skalowania automatycznego. Jeśli nie określisz interwał, jest używany hello wartość domyślna wynosząca 15 minut.
* Jeśli skalowania automatycznego jest aktualnie włączony na powitania puli, można określić formułą automatycznego skalowania i interwał oceny. Należy określić co najmniej jeden z tych właściwości.

  * Jeśli określisz nowy interwał oceny skalowania automatycznego hello istniejący harmonogram oceny został zatrzymany, a nowy harmonogram jest uruchomiona. czas rozpoczęcia Hello nowy harmonogram jest hello czasu, w których hello Skalowanie automatyczne tooenable żądania został wystawiony.
  * Jeśli pominięto interwał albo powitania w skalowania automatycznego formułę lub oceny hello usługa partia zadań nadal toouse hello bieżącą wartość tego ustawienia.

> [!NOTE]
> Jeśli określono wartości dla hello *targetDedicatedComputeNodes* lub *targetLowPriorityComputeNodes* parametry hello **CreatePool** metody podczas tworzenia hello puli w .NET lub parametrów można porównywać pod względem hello w innym języku, a następnie te wartości są ignorowane podczas szacowania hello automatyczne skalowanie formuły.
>
>

Następujący fragment kodu C# używa hello [partiami platformy .NET] [ net_api] Skalowanie automatyczne tooenable biblioteki w istniejącej puli:

```csharp
// Define hello autoscaling formula. This formula sets hello target number of nodes
// too5 on Mondays, and 1 on every other day of hello week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set hello autoscale formula on hello existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a>Aktualizacja formułą automatycznego skalowania

Formuła hello tooupdate na istniejącej włączona funkcja automatycznego skalowania puli, skalowanie automatyczne tooenable operacji hello wywołania ponownie, podając hello nowej formuły. Na przykład, jeśli już włączone Skalowanie automatyczne `myexistingpool` podczas wykonywania następującego kodu platformy .NET hello formułę skalowania automatycznego jest zastępowany zawartość hello `myNewFormula`.

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-hello-autoscale-interval"></a>Interwał automatycznego skalowania hello aktualizacji

tooupdate hello skalowania automatycznego interwał oceny istniejącej włączona funkcja automatycznego skalowania puli, skalowanie automatyczne tooenable operacji hello wywołania ponownie, podając nowy interwał hello. Na przykład tooset hello skalowania automatycznego oceny interwał too60 minut dla puli, która jest już włączona funkcja automatycznego skalowania w .NET:

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a>Ocena formułą automatycznego skalowania

Formuły można obliczyć przed zastosowaniem tooa puli. W ten sposób można przetestować hello toosee formuły, jak jego instrukcje ocenić przed wprowadzeniem hello formuły w środowisku produkcyjnym.

tooevaluate formułą automatycznego skalowania, należy najpierw włączyć funkcję skalowania automatycznego na powitania puli z prawidłową formułę. włączone tootest formuły w puli, która nie ma jeszcze Skalowanie automatyczne, używają hello jednego wiersza formuły `$TargetDedicatedNodes = 0` po pierwszym włączeniu Skalowanie automatyczne. Następnie należy użyć następującej formuły hello tooevaluate ma tootest hello:

* [BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) lub [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)

    Te metody partiami platformy .NET wymagają Identyfikatora hello istniejącej puli i ciąg zawierający tooevaluate formuły hello skalowania automatycznego.

* [Szacowanie formuły skalowania automatycznego](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    W tym żądania interfejsu API REST, określ identyfikator puli hello w hello identyfikator URI, a hello formułą automatycznego skalowania w hello *autoScaleFormula* element hello treści żądania. odpowiedź Hello operacji hello zawiera informacje o błędzie, które mogą być powiązane toohello formuły.

W tym [partiami platformy .NET] [ net_api] fragment kodu, możemy ocenić formułą automatycznego skalowania. Jeśli hello pula nie ma włączone Skalowanie automatyczne, możemy włączyć ją najpierw.

```csharp
// First obtain a reference tooan existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on hello pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula tooenable autoscaling on the
    // pool. This formula is valid, but won't resize hello pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls tooonce every 30 seconds.
    // Because we want tooapply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here tooensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh hello properties of hello pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on hello pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // hello formula tooevaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform hello autoscale formula evaluation. Note that this code does not
    // actually apply hello formula toohello pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print hello results of hello AutoScaleRun.
        // This will display hello values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply hello formula toohello pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output hello message associated with hello error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

Pomyślne obliczanie formuły hello pokazano w poniższym przykładzie tworzy wyniki podobne do:

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a>Uzyskiwanie informacji o uruchomieniu automatycznego skalowania

Oczekiwano tooensure, który wykonuje formułę jako, zalecamy okresowo sprawdzać wyniki hello hello przebiegów Skalowanie automatyczne, wykonywanych w Twojej puli partii. toodo tak, Pobierz (lub Odśwież) toohello odwołanie do puli i sprawdź, czy właściwości hello funkcja automatycznego skalowania jego ostatniego uruchomienia.

W partii .NET hello [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) właściwość ma kilka właściwości, które dostarczają informacji na temat hello najnowsze skalowania automatycznego uruchamiania wykonywane w puli hello:

* [AutoScaleRun.Timestamp](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [AutoScaleRun.Results](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [AutoScaleRun.Error](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

W hello interfejsu API REST, hello [uzyskać informacje o puli](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) żądania zwraca informacje o puli hello, która obejmuje hello najnowsze Skalowanie automatyczne uruchamianie informacji w hello [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) właściwości.

Hello poniższy fragment kodu C# używa hello partiami platformy .NET biblioteki tooprint informacji o ostatnich Skalowanie automatyczne hello uruchamiane na puli _myPool_:

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

Przykładowe dane wyjściowe hello poprzedzających fragment kodu:

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicatedNodes=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a>Przykład formuły skalowania automatycznego
Oto kilka formuły, które zawierają różne sposoby tooadjust hello ilość zasobów obliczeniowych w puli.

### <a name="example-1-time-based-adjustment"></a>Przykład 1: Dopasowania na podstawie czasu
Załóżmy, że rozmiar puli hello tooadjust na podstawie hello dzień tygodnia hello i godzinę. Ten przykład przedstawia, jak tooincrease lub zmniejszenia hello liczby węzłów w hello odpowiednio puli.

Formuła Hello najpierw uzyskuje hello bieżącego czasu. Jeśli dzień (1-5), a w godzinach pracy (too6 8 AM PM), rozmiar puli docelowej hello jest ustawienie too20 węzłów. W przeciwnym razie ustawił too10 węzłów.

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a>Przykład 2: Dostosowywanie opartego na zadaniach
W tym przykładzie hello rozmiar puli jest określany na powitania liczba zadań w kolejce hello podstawie. Zarówno podziały wierszy, jak i komentarze są dozwolone w ciągach formuły.

```csharp
// Get pending tasks for hello past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use hello last sample point,
// otherwise we use hello maximum of last sample point and hello history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM toopending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// hello pool size is capped at 20, if target VM value is more than that, set it
// too20. This value should be adjusted according tooyour use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a>Przykład 3: Uwzględniająca zadań równoległych
W tym przykładzie dopasowuje hello rozmiaru puli na podstawie hello liczby zadań. W tej formule również uwzględnia hello konta [MaxTasksPerComputeNode] [ net_maxtasks] wartość, która została ustawiona na powitania puli. Takie rozwiązanie jest przydatne w sytuacjach, w którym [równoległe wykonywanie zadań](batch-parallel-node-tasks.md) został włączony na pulę.

```csharp
// Determine whether 70 percent of hello samples have been recorded in hello past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set hello number of nodes tooadd tooone-fourth hello number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set too4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt toogrow hello number of compute nodes toomatch hello number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep hello nodes active until hello tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a>Przykład 4: Ustawienie rozmiaru puli początkowej
W przykładzie pokazano C# fragment formułą automatycznego skalowania, która ustawia kodu hello tooa rozmiar puli określoną liczbę węzłów dla początkowego okresu. Następnie można dostosować hello rozmiaru puli na podstawie liczby hello uruchomiona i aktywne zadania po hello początkowy okres czasu upłynął.

Formuła Hello w hello następującego fragmentu kodu:

* Ustawia hello pulę początkowy rozmiar toofour węzłów.
* Nie Dostosuj hello rozmiaru puli na powitania życia puli hello 10 minut.
* Po 10 minutach uzyskuje hello maksymalną wartość hello liczba uruchomiona i aktywne zadania w ramach hello ostatnich 60 minut.
  * Jeśli obie wartości są równe 0 (co oznacza, że żadne zadania zostały uruchomione lub aktywne w hello ostatnich 60 minut), rozmiar puli hello wynosi too0.
  * Jeśli każda wartość jest większa niż zero, są wprowadzane żadne zmiany.

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicatedNodes = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicatedNodes = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicatedNodes) : {1});
    ", now, 4);
```

## <a name="next-steps"></a>Następne kroki
* [Maksymalizowanie użycia zasobów obliczeniowych partii zadań Azure z węzła równoczesnych zadań](batch-parallel-node-tasks.md) zawiera szczegółowe informacje dotyczące sposobu można wykonywać wielu zadań jednocześnie na powitania węzłów obliczeniowych w puli. Ponadto tooautoscaling, ta funkcja może ułatwić czas trwania zadania toolower dla niektórych obciążeń, co pozwala zaoszczędzić pieniądze.
* Dla innego wydajności zestawu wspomagającego upewnij się, że partii zapytań aplikacji hello usługa partia zadań w hello większości optymalny sposób. Zobacz [wydajnie zapytania usługi partia zadań Azure hello](batch-efficient-list-queries.md) toolearn jak toolimit hello ilość danych w przewodowy hello kwerendy stanu hello potencjalnie tysięcy obliczeniowe węzły lub zadania.

[net_api]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch
[net_batchclient]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient
[net_cloudpool_autoscaleformula]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula
[net_cloudpool_autoscaleevalinterval]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval
[net_enableautoscaleasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.enableautoscaleasync
[net_maxtasks]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.maxtaskspercomputenode
[net_poolops_resizepoolasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.resizepoolasync

[rest_api]: https://docs.microsoft.com/rest/api/batchservice/
[rest_autoscaleformula]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_autoscaleinterval]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_enableautoscale]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
