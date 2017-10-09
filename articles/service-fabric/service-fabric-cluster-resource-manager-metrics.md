---
title: "za pomocą metryki obciążenia Azure mikrousługi aaaManage | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposób użycia zasobów usługi tooconfigure i użyj metryk w toomanage sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 0d622ea6-a7c7-4bef-886b-06e6b85a97fb
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 592dc749ce30683a1e439a702b7d0dc0a638276f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-resource-consumption-and-load-in-service-fabric-with-metrics"></a>Zarządzanie zużycia zasobów i obciążenia w sieci szkieletowej usług o metryki
*Metryki* zasoby hello Twojej usługi najważniejsze informacje, które są udostępniane przez hello węzłów w klastrze hello. Metryka to wszystko, które mają toomanage w kolejności tooimprove lub monitor wydajności hello usług. Mogą na przykład obserwować tooknow zużycie pamięci, jeśli usługa jest przeciążony. Użyj innego jest toofigure się, czy można przenieść usługę hello innym miejscu, gdzie pamięci jest mniejsza ograniczonego w kolejności tooget lepszą wydajność.

Np. użycia pamięci, dysku i procesora CPU przedstawiono metryki. Te metryki są metryki fizycznych, zasobów, które odpowiadają toophysical zasobów w węźle hello, wymagającym toobe zarządzane. Metryki mogą być również (i często są) logicznej metryki. Metryki logiczne są elementy, takie jak "MyWorkQueueDepth" lub "MessagesToProcess" lub "TotalRecords". Metryki logiczne są zdefiniowane przez aplikację, a pośrednio odpowiada toosome zużycie zasobów fizycznych. Metryki logiczne są często używane, może być twarde toomeasure i raportu zużycia zasobów fizycznych na podstawie-service. złożoność Hello pomiarów i raportowania własne fizycznych metryki jest również, dlaczego Usługa Service Fabric realizuje niektóre domyślne metryki.

## <a name="default-metrics"></a>Domyślne metryki
Załóżmy, że chcesz tooget Rozpoczęto zapisywanie i wdrażania usługi. W tym momencie nie wiadomo, jakie zasoby fizyczne lub logiczne zużywa. To świetnie! Hello zasobu klastra sieci szkieletowej programu Service Manager używa niektóre domyślne metryki, jeśli określono nie innych metryk. Są to:

  - PrimaryCount — liczba replik podstawowych, w węźle hello 
  - ReplicaCount — liczba całkowita stanowe replik w węźle hello
  - Liczba — liczba wszystkich obiektów usługi (bezstanowe i stanowe) w węźle hello

| Metryka | Obciążenia bezstanowe wystąpienia | Stanowe dodatkowej obciążenia | Stanowego obciążenia podstawowego |
| --- | --- | --- | --- |
| PrimaryCount |0 |0 |1 |
| ReplicaCount |0 |1 |1 |
| Licznik |1 |1 |1 |

W przypadku obciążeń podstawowych hello domyślne metryki Podaj zadowalający dystrybucji pracy hello klastra. W hello poniższy przykład Zobacz, co się stanie po możemy utworzyć dwie usługi i polegać na powitania domyślne metryki dla równoważenia. Hello pierwszej usługi jest usługi stanowej trzy partycji i replik docelowy Ustaw rozmiar trzech. Usługa drugi Hello jest usługi bezstanowej z jednej partycji i liczby wystąpień trzy.

Oto, możesz uzyskać:

<center>
![Układ klastra z domyślne metryki][Image1]
</center>

Niektóre toonote rzeczy:
  - Repliki podstawowej dla usługi stanowej hello są rozproszone na kilku węzłów
  - Repliki dla tej samej partycji są w różnych węzłach hello
  - Całkowita liczba Hello kolory podstawowe i pomocnicze bazy danych jest dystrybuowane w hello klastra
  - Całkowita liczba obiektów usługi Hello równomiernie są przydzielane na każdym węźle

Dobrym!

Witaj domyślne metryki ponosić działa jako rozpoczęcia. Jednak hello domyślne metryki tylko prowadzi należy do tej pory. Na przykład: co to jest hello prawdopodobieństwo, że partycjonowania hello schemat można pobrać wyników doskonale nawet wykorzystania przez wszystkie partycje? Co to jest stosowany hello hello obciążenia dla danej usługi jest stałe wraz z upływem czasu lub nawet po prostu hello sam między wieloma partycjami teraz?

Można uruchomić z właśnie hello domyślne metryki. Jednak taka zwykle oznacza, że Twoje użycie klastra mniejszą i nierówna bardziej, niż chcesz. Jest to spowodowane hello domyślne metryki nie adaptacyjną i zakładają, że wszystko, co jest równoważne. Na przykład podstawowego, który jest zajęty i który nie jest zarówno współtworzenia "1" toohello PrimaryCount metryki. W najgorszym przypadku hello przy użyciu tylko hello domyślne metryki może również spowodować overscheduled węzłów, co powoduje problemy z wydajnością. Jeśli interesuje Cię uzyskanie hello większości poza klastrem i unikanie problemów z wydajnością, należy toouse niestandardowych metryk i raportowania dynamicznego obciążenia.

## <a name="custom-metrics"></a>Metryki niestandardowe
Metryki są konfigurowane na poszczególnych o nazwie usług wystąpień podczas tworzenia usługi hello.

Niektóre właściwości opisujące go ma wszystkie metryki: nazwę, waga i obciążenia domyślne.

* Nazwa metryki: Nazwa hello hello metryki. Nazwa metryki Hello jest unikatowym identyfikatorem dla metryki hello w ramach klastra hello z punktu widzenia hello Resource Manager.
* Waga: Waga metryki Określa jak ważne ta metryka jest względna toohello innych metryk dla tej usługi.
* Obciążenia domyślne: hello domyślne obciążenia odpowiada inaczej w zależności od tego, czy usługa hello jest bezstanowych i stanowych.
  * W przypadku usług bezstanowych wszystkie metryki ma jedną właściwość o nazwie DefaultLoad
  * Dla stanowych usług można zdefiniować:
    * PrimaryDefaultLoad: pobiera tej usługi hello domyślna ilość ta metryka, w podstawowym
    * SecondaryDefaultLoad: pobiera tej usługi hello domyślna ilość ta metryka, czasie pomocniczego

> [!NOTE]
> Jeśli zdefiniujesz metryki niestandardowe i ma domyślne too_also_ metryki hello, musisz too_explicitly_ Dodaj hello domyślne metryki kopii i zdefiniuj wagi i wartości dla nich. Jest to spowodowane należy zdefiniować relację hello hello domyślne metryki i Twoje metryki niestandardowe. Na przykład może być potrzebne informacje ConnectionCount lub WorkQueueDepth więcej niż podstawowy dystrybucji. Domyślne wagi hello hello PrimaryCount metryka jest wysoki, więc ma tooreduce on tooMedium po dodaniu z innych tooensure metryki one pierwszeństwo.
>

### <a name="defining-metrics-for-your-service---an-example"></a>Definiowanie metryki dla usługi — przykład
Załóżmy, że chcesz hello następującej konfiguracji:

  - Metryka o nazwie "ConnectionCount" raportów usługi
  - Należy także toouse hello domyślne metryki 
  - Przycisk niektórych pomiarów i dowiedzieć się, że zwykle podstawową replikę tej usługi zajmuje 20 jednostek "ConnectionCount"
  - Pomocnicze bazy danych użyj 5 jednostek "ConnectionCount"
  - Wiesz, że "ConnectionCount" jest hello Metryka najważniejszych pod względem wydajności hello tej konkretnej usługi zarządzania
  - Nadal chcesz zrównoważonym replik podstawowych. Równoważenie replik podstawowych zazwyczaj dobrym pomysłem jest bez względu na okoliczności. Pomaga to zapobiec utracie hello niektóre domeny węzła lub fault z wpływające na większości replik podstawowych wraz z jej. 
  - W przeciwnym razie hello domyślne metryki są poprawnie

Oto kod hello czy piszesz toocreate usługi za pomocą tej konfiguracji metryki:

Kod:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
StatefulServiceLoadMetricDescription connectionMetric = new StatefulServiceLoadMetricDescription();
connectionMetric.Name = "ConnectionCount";
connectionMetric.PrimaryDefaultLoad = 20;
connectionMetric.SecondaryDefaultLoad = 5;
connectionMetric.Weight = ServiceLoadMetricWeight.High;

StatefulServiceLoadMetricDescription primaryCountMetric = new StatefulServiceLoadMetricDescription();
primaryCountMetric.Name = "PrimaryCount";
primaryCountMetric.PrimaryDefaultLoad = 1;
primaryCountMetric.SecondaryDefaultLoad = 0;
primaryCountMetric.Weight = ServiceLoadMetricWeight.Medium;

StatefulServiceLoadMetricDescription replicaCountMetric = new StatefulServiceLoadMetricDescription();
replicaCountMetric.Name = "ReplicaCount";
replicaCountMetric.PrimaryDefaultLoad = 1;
replicaCountMetric.SecondaryDefaultLoad = 1;
replicaCountMetric.Weight = ServiceLoadMetricWeight.Low;

StatefulServiceLoadMetricDescription totalCountMetric = new StatefulServiceLoadMetricDescription();
totalCountMetric.Name = "Count";
totalCountMetric.PrimaryDefaultLoad = 1;
totalCountMetric.SecondaryDefaultLoad = 1;
totalCountMetric.Weight = ServiceLoadMetricWeight.Low;

serviceDescription.Metrics.Add(connectionMetric);
serviceDescription.Metrics.Add(primaryCountMetric);
serviceDescription.Metrics.Add(replicaCountMetric);
serviceDescription.Metrics.Add(totalCountMetric);

await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Środowiska PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ConnectionCount,High,20,5”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

> [!NOTE]
> Witaj powyżej przykłady i hello pozostałej części tego dokumentu opisano zarządzanie metryki na podstawie ciągu o nazwie — usługi. Możliwe jest również możliwe toodefine metryki dla usługi w punkcie usług hello _typu_ poziom. Jest to osiągnąć, określając je w manifestach Twojej usługi. Definiowanie metryki na poziomie typu nie jest zalecane z kilku powodów. pierwsze urząd Hello są nazwy metryki często określonego środowiska. Jeżeli nie istnieje ostateczne kontraktu w miejscu, nie może być się, że tego Metryka hello "Rdzeni" w jednym środowisku nie "MiliCores" lub "Rdzeni" w innych. Jeśli Twoje metryki są zdefiniowane w manifeście należy toocreate nowe manifesty na środowisko. Prowadzi to zwykle tooa mnożenie różnych manifestów tylko drobne różnice, które mogą spowodować trudności toomanagement.  
>
> Metryka obciążenia często są przypisywane na podstawie poszczególnych o nazwie usług wystąpień. Na przykład, załóżmy, że utworzyć jedno wystąpienie powitania dla CustomerA, który plany toouse go obsłużyć rzadziej. Również Załóżmy, że utworzyć inny dla CustomerB mającego większe obciążenie. W takim przypadku będzie prawdopodobnie wskazana będzie domyślna hello tootweak ładuje dla tych usług. Jeśli masz metryki i obciążeń zdefiniowany za pomocą manifestów i chcesz toosupport tego scenariusza, wymaga innej aplikacji i typów usług dla każdego klienta. wartości Hello zdefiniowanych w czasie tworzenia usługi przesłaniają akcje zdefiniowane w manifeście hello, można użyć tego tooset hello określonych wartości domyślnych. Jednak operacją powoduje, że wartości hello zadeklarowany w hello manifestów toonot odpowiada te usługi hello działa z. Może to spowodować tooconfusion. 
>

Dla przypomnienia: Jeśli chcesz toouse hello domyślne metryki, nie należy tootouch hello metryki kolekcji na wszystkich lub czy jakieś szczególne podczas tworzenia usługi. Hello domyślne metryki uzyskać użyć automatycznie, gdy nie zdefiniowano żadnych innych użytkowników. 

Teraz przejdźmy do każdego z tych ustawień bardziej szczegółowo i omówione hello ma to wpływ na zachowanie.

## <a name="load"></a>Ładowanie
Witaj całego punktu definiowania metryk jest toorepresent niektóre obciążenia. *Obciążenia* jest, jaka część danej metryki jest używany przez niektóre wystąpienia usługi lub replikę z danego węzła. Obciążenia można skonfigurować w dowolnym momencie. Na przykład:

  - Obciążenia można zdefiniować podczas tworzenia usługi. Ta metoda jest wywoływana _obciążenia domyślne_.
  - metryki informacji Hello, w tym domyślnego ładuje usługi można zaktualizowane po utworzeniu hello usługi. Ta metoda jest wywoływana _uaktualnianie usługi_. 
  - Witaj obciążenia dla danej partycji można resetowania toohello domyślne wartości dla tej usługi. Ta metoda jest wywoływana _zresetowania obciążenia partycji_.
  - Obciążenia mogą być zgłaszane na poszczególnych obiektów usługi dynamicznie w czasie wykonywania. Ta metoda jest wywoływana _raportowania obciążenia_. 
  
Wszystkie te strategii znajdują się w hello sama usługa swojego okresu istnienia. 

## <a name="default-load"></a>Domyślne obciążenia
*Domyślne obciążenia* jest znacznie metryki hello zużywa każdego obiektu usługi (bezstanowych wystąpienia lub stanowych repliki) tej usługi. Hello Menedżera zasobów klastra używa tego numeru obciążenia hello hello obiektu usługi, dopóki nie odbierze inne informacje, takie jak raportu dynamicznego obciążenia. W przypadku prostszych usług obciążenie domyślne hello jest definicji statycznych. obciążenia domyślne Hello nigdy nie są aktualizowane i jest używany czas ich istnienia hello hello usługi. Domyślne ładuje Wielkiej działa proste pojemności planowanie scenariuszy, w którym niektórych ilości zasobów dedykowanych toodifferent obciążenia i nie należy zmieniać.

> [!NOTE]
> Aby uzyskać więcej informacji dotyczących zarządzania pojemności i definiowanie pojemności dla hello węzłów w klastrze, zobacz [w tym artykule](service-fabric-cluster-resource-manager-cluster-description.md#capacity).
> 

Hello Menedżera zasobów klastra umożliwia toospecify usługi stanowej obciążenia różne domyślne kolory podstawowe i pomocnicze bazy danych. Usługi bezstanowej można określić tylko jedną wartość, która dotyczy tooall wystąpień. Dla stanowych usług obciążenia domyślne hello replik podstawowe i pomocnicze są zwykle różnych, ponieważ repliki są różnego rodzaju pracy w każdej roli. Na przykład kolory podstawowe zwykle służą odczytów i zapisów i obsługę większości obciążeń obliczeniowych hello, gdy nie chcesz pomocnicze bazy danych. Zazwyczaj hello domyślne obciążenia dla repliki podstawowej jest wyższa niż hello domyślne obciążenia dla replik pomocniczych. liczb rzeczywistych Hello powinien zależeć odpowiednie wartości.

## <a name="dynamic-load"></a>Obciążenie dynamicznego
Załóżmy, że działała usługi przez pewien czas. Niektóre monitorowania z zostały zauważyć, że:

1. Niektóre partycje lub wystąpienia danej usługi zużywać więcej zasobów niż inne
2. Niektóre usługi mają obciążenia, która różni się w czasie.

Istnieje wiele rzeczy, które mogły spowodować tego rodzaju wahania obciążenia. Na przykład różnych usług lub partycje są skojarzone z różnych klientów z innymi wymaganiami. Obciążenia można również zmienić, ponieważ hello ilość pracy hello usługi zmienia się w hello porach dnia hello. Niezależnie od przyczyny hello jest zwykle nie jeden numer używanego dla domyślnego. Jest to szczególnie istotne, kiedy ma tooget hello większość wykorzystania hello klastra. Wartość, wybrać domyślne obciążenia jest niewłaściwy niektóre hello czasu. Nieprawidłowe domyślne ładuje spowodować hello Menedżera zasobów klastra za pośrednictwem lub w obszarze alokacji zasobów. W związku z tym masz węzłów, które są powyżej lub poniżej wykorzystywane nawet hello Menedżera zasobów klastra sądzi, że klaster hello jest rozmieszczana. Domyślne obciążenia są nadal dobrej, ponieważ zapewniają niektóre informacje do umieszczenia początkowej, ale nie są one zakończenie wątku dla obciążeń prawdziwe. Przechwytywanie tooaccurately zmiany wymagań dotyczących zasobów, hello Menedżera zasobów klastra umożliwia każdego tooupdate obiektu usługi własną obciążenia w czasie wykonywania. Jest to obciążenie dynamicznego raportowania.

Raporty Obciążenie dynamicznego Zezwalaj tooadjust repliki lub wystąpień ich alokacji/zgłosił obciążenia metryk przez ich istnienia. Repliki usługi lub wystąpienia, który był niskich i bezczynny będzie zazwyczaj raport, aby korzystał z niskim ilości danej metryki. Replika zajęta lub wystąpienie rozpoczną przesyłanie raportów o tym, że używają więcej.

Raportowania obciążenia dla repliki lub wystąpienie pozwala hello tooreorganize Menedżera zasobów klastra hello pojedynczej usługi obiektów hello klastra. Reorganizacja usług hello pomaga, upewnij się, że otrzymują hello zasoby, które wymagają. Zajęty usługi skutecznie Uzyskaj zbyt "odzyskać" zasoby od innych repliki lub wystąpienia, które są aktualnie ten mniej pracy lub niskie.

W ramach niezawodnej usługi hello kodu tooreport obciążenia dynamicznie wygląda następująco:

Kod:

```csharp
this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("CurrentConnectionCount", 1234), new LoadMetric("metric1", 42) });
```

Usługa może raportować na dowolnym metryki hello zdefiniowane w czasie tworzenia. Jeśli usługa raporty obciążenia dla metryki, który nie jest skonfigurowany toouse, sieci szkieletowej usług ignoruje tego raportu. Jeśli istnieją inne metryki zgłoszone w hello sam czas, które są prawidłowe, te raporty są akceptowane. Kod usługi można mierzyć i raportu hello wszystkie metryki wiadomo, jak i operatory można określić hello metryki konfiguracji toouse bez konieczności toochange hello usługi kodu. 

### <a name="updating-a-services-metric-configuration"></a>Trwa aktualizowanie konfiguracji metryki usługi
listy Hello metryki skojarzonych z usługą hello i właściwości hello tych metryk może być aktualizowany dynamicznie, gdy usługa hello jest na żywo. Dzięki temu eksperymenty i elastyczność. Przykłady gdy jest to przydatne są:

  - wyłączanie Metryka z raportem buggy określonej usługi
  - ponowne konfigurowanie hello wagi metryki na podstawie żądanego zachowania
  - Włączanie nowej Metryka tylko wtedy, gdy kod hello został już wdrożony i zweryfikować za pośrednictwem innych mechanizmów
  - Zmiana hello domyślne obciążenia dla usługi na podstawie obserwowanych zachowania i zużycia

Witaj głównego interfejsy API do zmiany konfiguracji metryki są `FabricClient.ServiceManagementClient.UpdateServiceAsync` w języku C# i `Update-ServiceFabricService` w programie PowerShell. Niezależnie od informacje z poniższych interfejsów API zastępuje hello istniejących informacji metryki dla usługi hello natychmiast. 

## <a name="mixing-default-load-values-and-dynamic-load-reports"></a>Mieszanie domyślne wartości obciążenia i raportów obciążenia dynamiczne
Domyślne obciążenia i dynamiczna obciążenia mogą być używane dla hello tę samą usługę. Gdy usługa korzysta zarówno obciążenia domyślne i raportów obciążenia dynamicznego, obciążenia domyślna służy jako szacunkową dopóki wyświetlani dynamicznych raportów. Domyślne obciążenia jest prawidłowa, ponieważ umożliwia hello Menedżera zasobów klastra coś toowork z. obciążenia domyślne Hello umożliwia hello tooplace Menedżera zasobów klastra obiektów usługi hello w lokalizacjach dobrej podczas ich tworzenia. Jeśli podano żadnych informacji obciążenia domyślne, umieszczania usług jest skutecznie losowych. Nadejściu raportów obciążenia później hello początkowej umieszczania losowe często jest nieprawidłowy i hello Menedżera zasobów klastra ma toomove usług.

Teraz pobrać naszych poprzedni przykład i zobacz, co się stanie po dodamy niektóre metryki niestandardowe i raportowania dynamicznego obciążenia. W tym przykładzie używamy "MemoryInMb" jako przykład metryka.

> [!NOTE]
> Pamięć jest jednym z hello systemu metryki sieci szkieletowej usług można [regulują zasobów](service-fabric-resource-governance.md), i raportowania samodzielnie jest zazwyczaj trudne. Nie faktycznie Oczekujemy Cię tooreport na zużycie pamięci; Pamięć jest używana jako toolearning pomocy o możliwości hello hello Menedżera zasobów klastra.
>

Załóżmy zakładają, możemy początkowo utworzony usługi stanowej hello ze hello następujące polecenie:

Środowiska PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("MemoryInMb,High,21,11”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

Dla przypomnienia ta składnia jest ("MetricName, MetricWeight, PrimaryDefaultLoad, SecondaryDefaultLoad").

Zobaczmy, jakie jeden układ możliwe klastra może wyglądać jak:

<center>
![Klaster zrównoważony z domyślnych i niestandardowych metryk][Image2]
</center>

Kilka rzeczy, które są warto zauważyć:

* Każdej repliki pomocniczej w partycji może mieć własne obciążenia
* Ogólne metryki hello Szukaj zrównoważonym. Pamięci, hello proporcje hello maksymalna i minimalna obciążenia jest 1,75 (hello węzła z hello większości obciążenia jest N3, hello jest najmniej N2 i 28/16 = 1,75).

Istnieje kilka kwestii, które nadal potrzebujemy tooexplain:

* Co to ustalić, czy stosunek 1,75 było uzasadnione? Jak hello Menedżera zasobów klastra sprawdzić czy jest wystarczająca, czy istnieje więcej toodo pracy?
* Gdy równoważenia stanie?
* Co oznacza że pamięci zostało ważona "High"?

## <a name="metric-weights"></a>Metryki wagi
Śledzenie hello same metryki w różnych usługach jest ważna. Czy widoku globalnego jest co pozwalają hello zużycie tootrack Menedżera zasobów klastra w klastrze hello równoważenie zużycie na węzłach i upewnij się, że węzły nie przekazywane pojemności. Jednak usługi mogą mieć różne widoki jako toohello znaczenie hello tę samą metrykę. Ponadto w klastrze z wieloma metryki i wiele usług doskonale zrównoważonym rozwiązania może nie istnieć dla wszystkich metryki. Jak hello Menedżera zasobów klastra powinna obsługiwać tych sytuacji?

Metryki wag Zezwalaj hello toodecide Menedżera zasobów klastra, jak toobalance hello klastra po doskonałe odpowiedzi. Metryki wag również umożliwić hello toobalance Menedżera zasobów klastra określonych usług inaczej. Metryki mogą mieć czterech wagi różnych poziomów: Zero, niski, średni i wysoki. Metryka o wadze Zero wspiera nic podczas określania, czy elementy są zrównoważonym lub nie. Jednak jej obciążenia nadal wpływ toocapacity zarządzania. Metryki Zero wagę są nadal przydatne i są często używane jako część zachowanie usługi i monitorowania wydajności. [W tym artykule](service-fabric-diagnostics-event-generation-infra.md) zamieszczono więcej informacji dotyczących użycia hello metryk do monitorowania i diagnostyki usług. 

Witaj rzeczywistego wpływ różne metryki obciążenia w klastrze hello jest tym hello Menedżera zasobów klastra generuje różnych rozwiązań. Wag metryki Poinformuj hello Menedżera zasobów klastra, czy niektóre metryki są ważniejsze od innych użytkowników. Jeśli nie istnieje żadne hello doskonałe rozwiązanie Menedżera zasobów klastra można preferowane rozwiązania, które saldo hello wyższej ważoną metryki lepsze. Jeśli usługa sądzi określonej metryki jest bez znaczenia, może znajdzie ich używania tego metryki imbalanced. Dzięki temu innego tooget usługi nawet dystrybucji niektóre metryki, która jest ważna tooit.

Oto przykład niektórych raportów obciążenia i metrykę, jak różne przeprowadzi wyniki w różnych alokacji w hello klastra. W tym przykładzie przedstawiono, że przełączenie hello względną wagę metryki hello powoduje hello toocreate Menedżera zasobów klastra uzgodnienia różnych usług.

<center>
![Przykład waga metryki i jak wpływa na rozwiązań do równoważenia][Image3]
</center>

W tym przykładzie istnieją cztery różne usługi, wszystkie wartości różnych raportowania dla dwóch różnych metryki MetricA i MetricB. W przypadku jednego wszystkich usług hello zdefiniuj MetricA jest jednym z najważniejszych hello (wagi = wysoki) i MetricB jako nieistotnych (wagi = niski). W związku z tym widzimy się, że ten hello Menedżera zasobów klastra umieszcza hello usługi tak, aby lepiej jest zrównoważonym niż MetricB MetricA. "Lepiej zrównoważonym" oznacza, że MetricA ma mniejszy ma odchylenie standardowe niższe niż MetricB. W drugim przypadku hello możemy wycofać hello wag metryki. W związku z tym hello Menedżera zasobów klastra zamienia usług A i B toocome się z alokacją, gdzie MetricB lepiej jest zrównoważonym niż MetricA.

> [!NOTE]
> Metryki wag określają, jak powinna saldo hello Menedżera zasobów klastra, ale nie podczas równoważenia powinno się zdarzyć. Aby uzyskać więcej informacji na temat funkcji równoważenia, zapoznaj się z [w tym artykule](service-fabric-cluster-resource-manager-balancing.md)
>

### <a name="global-metric-weights"></a>Globalne wag metryki
Załóżmy, że ServiceA definiuje MetricA jako wagi wysokiej i ServiceB ustawia wagi hello MetricA tooLow lub Zero. Co to jest hello wagi rzeczywiste kończy się używany?

Istnieje wiele wagi, śledzonych dla każdego metryki. Waga pierwszy Hello jest hello zdefiniowanych dla metryki powitania po utworzeniu hello usługi. Witaj innych waga jest globalne wagi, która jest obliczana automatycznie. podczas oceniania rozwiązania, Hello Menedżera zasobów klastra używa oba te wagi. Biorąc pod uwagę zarówno wag jest ważne. Dzięki temu hello toobalance Menedżera zasobów klastra każdej usługi tooits zgodnie z właścicielem priorytetów i upewnij się również klastra hello, jako całość jest poprawnie przydzielone.

Co się stanie, jeśli hello Menedżera zasobów klastra nie zależy Ci na zachowaniu saldo zarówno globalne i lokalne? Jest również łatwe tooconstruct rozwiązania, który globalnie równoważy, ale co spowodować równowadze zasobów niska dla poszczególnych usług. Hello poniższy przykład załóżmy przyjrzeć się skonfigurowano tylko hello domyślne metryki usługi i zobacz, co się dzieje, gdy tylko globalne saldo jest uznawany za:

<center>
![Witaj wpływu globalnego rozwiązania tylko][Image4]
</center>

Hello top przykład oparte tylko na globalnego równoważenia w rzeczywistości jest rozmieszczana hello klastra jako całość. Witaj sama liczba kolory podstawowe i hello takie same na wszystkich węzłach jest liczba całkowita replik. Jednak jeśli przyjrzymy się hello rzeczywisty wpływ tej alokacji nie jest tak dobre: hello utraty dowolnego węzła ma wpływ określonego obciążenia nieproporcjonalnie, ponieważ zajmuje całe jego kolory podstawowe. Na przykład jeśli pierwszy węzeł hello nie powiedzie się hello kolory trzy podstawowe dla hello trzech różnych partycji hello koło usługi wszystkie zostałyby utracone. Z drugiej strony hello trójkąt i sześciokąt usług mają ich utratę repliki partycji. Powoduje to nie przerw w działaniu, oprócz posiadania hello toorecover dół repliki.

W przykładzie dolnej hello hello Menedżera zasobów klastra został rozesłany replik hello oparte na obu hello saldo globalnym i dla usługi. Podczas obliczania oceny hello hello rozwiązania daje większość hello wagi toohello globalne rozwiązanie i usług tooindividual części (można konfigurować). Globalne saldo metryka jest obliczany na podstawie hello średnią hello ważonych metryki z każdej usługi. Każda usługa jest rozmieszczana zgodnie z tooits własnych zdefiniowanych metryki wagi. Dzięki temu równoważy hello usług między sobą zgodnie z tootheir własnych potrzeb. W związku z tym jeśli hello pierwszego węzła w tym samym nie powiedzie się niepowodzenie hello jest dystrybuowana do wszystkich partycji wszystkich usług. tooeach wpływ Hello jest hello takie same.

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać więcej informacji na temat konfigurowania usługi [informacje na temat konfigurowania usługi](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Definiowanie metryki defragmentacji jest jednym ze sposobów tooconsolidate obciążenie węzłów zamiast go rozkładanie. toolearn jak tooconfigure defragmentacji, zapoznaj się zbyt[w tym artykule](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
- toofind limit o jak hello Menedżera zasobów klastra zarządza i równoważy obciążenie klastra hello wyewidencjonować hello artykułu na [równoważenia obciążenia](service-fabric-cluster-resource-manager-balancing.md)
- Rozpocznij od początku hello i [uzyskać toohello wprowadzenie zasobu klastra sieci szkieletowej programu Service Manager](service-fabric-cluster-resource-manager-introduction.md)
- Koszt przeniesienia jest jednym ze sposobów sygnalizowania toohello Menedżera zasobów klastra, że niektóre usługi są toomove droższe niż inne. toolearn więcej informacji na temat koszt przeniesienia odwoływać się za[w tym artykule](service-fabric-cluster-resource-manager-movement-cost.md)

[Image1]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-cluster-layout-with-default-metrics.png
[Image2]:./media/service-fabric-cluster-resource-manager-metrics/Service-Fabric-Resource-Manager-Dynamic-Load-Reports.png
[Image3]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-metric-weights-impact.png
[Image4]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-global-vs-local-balancing.png
