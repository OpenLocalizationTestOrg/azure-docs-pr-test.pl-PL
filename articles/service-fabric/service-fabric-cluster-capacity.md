---
title: "Witaj aaaPlanning pojemności klastra sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Zagadnienia związane z planowaniem pojemności klastra sieci szkieletowej usług. Warstwy elementów NodeType, trwałości i niezawodności"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 4c584f4a-cb1f-400c-b61f-1f797f11c982
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: chackdan
ms.openlocfilehash: 83272ce7fefe698eef755cf66493c2874cc3b120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-capacity-planning-considerations"></a>Zagadnienia związane z planowaniem pojemności klastra sieci szkieletowej usług
Wszystkie wdrożenia produkcyjnego planowania pojemności jest ważnym krokiem. Poniżej przedstawiono niektóre elementy hello ma tooconsider w ramach tego procesu.

* Liczba Hello węzła typy klastra toostart musi się z
* Witaj właściwości każdego typu węzła (rozmiar, podstawową, internetowy, liczba maszyn wirtualnych itd.)
* niezawodność i trwałość właściwości Hello hello klastra

Daj nam krótko Sprawdź każdy z tych elementów.

## <a name="hello-number-of-node-types-your-cluster-needs-toostart-out-with"></a>Liczba Hello węzła typy klastra toostart musi się z
Najpierw należy toofigure jakie klastra hello tworzysz będzie toobe używany dla i planowania jakiego rodzaju aplikacje toodeploy do tego klastra. Jeśli nie masz wyczyść na celu hello hello klastra, możesz najprawdopodobniej nie została jeszcze gotowe proces planowania pojemności hello tooenter.

Ustanów hello rodzaje węzeł klastra musi toostart się z.  Każdy typ węzła jest mapowanych tooa zestawu skalowania maszyn wirtualnych. Każdy typ węzła następnie można skalować w lub w dół niezależnie, mają różne zestawy otwartych portów i może mieć metryki pojemności różnych. Dlatego decyzji hello hello liczby typów węzłów pochodzi zasadniczo dół toohello następujące zagadnienia:

* Aplikacja ma wiele usług i ich zbędna toobe publiczny lub Internetem? Typowe aplikacje zawierają usługi frontonu bramy, który odbiera dane wejściowe z klienta i co najmniej jeden zaplecza usług, które komunikują się z hello usługi frontonu. Dlatego w tym przypadku na końcu mających co najmniej dwa typy węzłów.
* Usługi (wchodzące w skład aplikacji), czy mają potrzeb różnych infrastruktury, takich większa ilość pamięci RAM lub wyższej cykli Procesora? Na przykład załóżmy tej aplikacji hello mają toodeploy zawiera usługi frontonu i zaplecza. Witaj frontonu usługa może działać na mniejsze maszyn wirtualnych (na przykład D2 rozmiarów maszyn wirtualnych), które mają toohello otwarcia portów internetowych.  Witaj usługi zaplecza, jednak jest toorun CPU i potrzeb obliczeń na większych maszyn wirtualnych (o rozmiarów maszyn wirtualnych, takie jak D15 D4, D6,), które nie są internet skierowane.
  
  W tym przykładzie mimo że można zdecydować, tooput hello wszystkich usług na jednym węźle typu, zaleca się umieszczenie ich w klastrze dwa typy węzłów.  Dzięki temu dla każdego węzła typu toohave różne właściwości, takie jak łączność z Internetem lub rozmiar maszyny Wirtualnej. Witaj liczbę maszyn wirtualnych mogą być skalowane niezależnie, jak również.  
* Ponieważ nie można przewidzieć przyszłe hello, przejść z faktów, które znasz i podejmowanie decyzji o hello liczba typy węzłów, które aplikacje muszą toostart z. Można zawsze dodawać i usuwać typy węzłów później. Klaster sieci szkieletowej usług musi mieć co najmniej jeden węzeł typu.

## <a name="hello-properties-of-each-node-type"></a>Witaj właściwości każdego typu węzła
Witaj **typu węzła** są widoczne jako równoważne tooroles usług w chmurze. Typy węzłów zdefiniować rozmiary maszyn wirtualnych hello hello liczbę maszyn wirtualnych i ich właściwości. Każdy typ węzła który jest zdefiniowany w klastrze usługi sieć szkieletowa jest skonfigurowany jako zestaw skali oddzielnej maszynie wirtualnej. Zestaw skali maszyny wirtualnej jest zasobem obliczeń platformy Azure, można użyć toodeploy i zarządzanie kolekcją jako zestaw maszyn wirtualnych. Jest określone jako zestaw skali maszyny wirtualnej distinct, każdy typ węzła następnie można skalować w lub w dół niezależnie, mają różne zestawy otwartych portów, a może mieć inną pojemność metryki.

Odczyt [tego dokumentu](service-fabric-cluster-nodetypes.md) jak więcej szczegółów na powitania relacji zestawu skali maszyny toovirtual elementów NodeType, tooRDP do jednego z wystąpień hello otworzyć nowych portów itp.

Klaster może zawierać więcej niż jeden typ węzła, ale typ węzła podstawowego hello (hello w pierwszej kolejności należy zdefiniować w portalu hello) musi mieć co najmniej pięć maszyn wirtualnych dla klastrów używanych w przypadku obciążeń produkcyjnych (lub co najmniej trzech maszyn wirtualnych w klastrach testu). W przypadku tworzenia klastra hello przy użyciu szablonu usługi Resource Manager, następnie wyszukaj **jest podstawowym** atrybutu w definicji typu węzła hello. Typ węzła podstawowego Hello jest typ węzła hello rozmieszczenia usługi sieć szkieletowa usług systemowych.  

### <a name="primary-node-type"></a>Typ węzła podstawowego
W przypadku klastra z wieloma typami węzła należy toochoose jeden z nich toobe podstawowego. Poniżej przedstawiono charakterystyki hello typu węzła podstawowego:

* Witaj **minimalny rozmiar maszyn wirtualnych** dla typu węzła podstawowego hello jest określany przez hello **warstwa trwałości** wybierzesz. Witaj domyślnym warstwa trwałości hello jest brązowa. Szczegółowe informacje o jakie warstwa trwałości hello jest i wartości, które mogą upłynąć hello przewiń w dół.  
* Witaj **minimalną liczbę maszyn wirtualnych** dla typu węzła podstawowego hello jest określany przez hello **warstwa niezawodności** wybierzesz. domyślnym Hello warstwa niezawodności hello jest Silver. Szczegółowe informacje o jakie warstwa niezawodności hello jest i wartości, które mogą upłynąć hello przewiń w dół. 


* Hello usługi sieć szkieletowa usług systemowych (na przykład hello Menedżera klastra usługi lub usługi składnika Image Store) są umieszczane na typ węzła podstawowego hello i niezawodność hello tak i trwałości hello klastra jest określana przez hello warstwy wartość i trwałości warstwa niezawodności wartość dla typu węzła podstawowego hello.

![Zrzut ekranu przedstawiający klastra, która ma dwa typy węzłów ][SystemServices]

### <a name="non-primary-node-type"></a>Typ podstawowy nie węzła
W przypadku klastra z wieloma typami węzła jest jeden typ węzła podstawowego i rest hello z nich są innych niż podstawowe. Poniżej przedstawiono charakterystyki hello typu innego niż podstawowy węzła:

* Hello minimalny rozmiar maszyn wirtualnych dla tego typu węzła jest określany przez warstwę trwałości hello, którą wybierzesz. Witaj domyślnym warstwa trwałości hello jest brązowa. Szczegółowe informacje o jakie warstwa trwałości hello jest i wartości, które mogą upłynąć hello przewiń w dół.  
* może to być jeden Hello minimalną liczbę maszyn wirtualnych dla tego typu węzła. Jednak należy wybrać ten numer na podstawie hello liczby replikami hello aplikacji/usługi ma toorun tego typu węzła. Po wdrożeniu klastra hello można zwiększyć Hello liczbę maszyn wirtualnych w typu węzła.

## <a name="hello-durability-characteristics-of-hello-cluster"></a>właściwości trwałości Hello hello klastra
Warstwa trwałości Hello jest tooindicate używane toohello systemu hello uprawnienia, których maszyn wirtualnych z hello podstawowej infrastruktury platformy Azure. W polu Typ węzła podstawowego hello to uprawnienie umożliwia toopause usługi sieć szkieletowa dowolnej maszyny Wirtualnej infrastruktury poziomu żądania (takie jak ponowne uruchomienie maszyny Wirtualnej, odtworzenia z obrazu maszyny Wirtualnej lub migracja maszyny Wirtualnej) wpływ hello kworum wymagania dotyczące usługi systemowe hello i stanowych usług. W hello typy węzłów z systemem innym niż podstawowy to uprawnienie umożliwia sieci szkieletowej usług toopause maszyny Wirtualnej infrastruktury poziomu żądań takie jak ponowne uruchomienie maszyny Wirtualnej, odtworzenia z obrazu maszyny Wirtualnej, migracja maszyny Wirtualnej itp., które mają wpływ na powitania kworum wymagania dla stanowych usług uruchomionych w jej.

To uprawnienie jest wyrażona w hello następujące wartości:

* Złota - hello infrastruktury zadań można wstrzymana na okres dwóch godzin na UD. Złoty trwałości można włączyć tylko dla jednostki SKU wirtualna pełne węzła jak D15_V2, G5 itp.
* Srebrny — hello infrastruktury zadania może być wstrzymana na okres 10 minut na każdą UD i jest dostępny na wszystkich standardowych maszyn wirtualnych z pojedynczego rdzenia i powyżej.
* Brązowy - żadnych uprawnień. Jest to domyślna hello. Ten poziom trwałości należy używać tylko dla typów węzłów, które uruchamiane _tylko_ bezstanowe. 

> [!WARNING]
> Uzyskiwanie elementów NodeType systemem trwałości brązowa _żadnych uprawnień_. Oznacza to, że zadania infrastruktury, które mają wpływ na obciążeń bezstanowych nie zostanie zatrzymana ani opóźnione. Istnieje możliwość, że takie zadania nadal może wpłynąć na obciążeń, powodując przestoje lub inne problemy. Rodzaj obciążenia produkcji systemem z co najmniej Silver jest zalecane. 
> 

Otrzymasz poziom trwałości toochoose dla każdego z typów węzłów. Można wybrać jeden typ węzła toohave poziom trwałości złota lub srebrna i hello innych mają brązowa hello tego samego klastra. **Wymagana minimalna liczba węzłów 5 dla dowolnego typu węzła mającego trwałości Gold lub silver**. 

**Korzyści wynikające z używania Silver lub złota poziom trwałości**
 
1. Zmniejsza liczbę hello czynności w ramach operacji skalowania (to znaczy dezaktywacji węzła i Usuń ServiceFabricNodeState jest wywoływana automatycznie)
2. Zmniejsza hello ryzyko utraty danych tooa inicjowane przez klienta, w miejscu i operacji zmiany jednostki SKU maszyny Wirtualnej lub operacji infrastruktury platformy Azure.
     
**Wady używania Silver lub złota poziom trwałości**
 
1. Tooyour wdrożenia zestawu skalowania maszyn wirtualnych i inne powiązane zasoby Azure) mogą być opóźnione, można przekroczyło limit czasu lub mogą zostać zablokowane całkowicie przez problemy w klastrze lub na poziomie infrastruktury hello. 
2. Zwiększa hello liczba [zdarzenia cyklu życia repliki](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle ) (na przykład podstawowego zamiany) powodu tooautomated deactivations węzła podczas operacji infrastruktury platformy Azure.

### <a name="recommendations-on-when-toouse-silver-or-gold-durability-levels"></a>Zalecenia o tym, kiedy poziom trwałości Silver lub złota toouse

Użyj Silver lub Gold trwałości dla węzła wszystkie typy stateful tego hosta usługi można spodziewać się tooscale w (zmniejszyć liczbę wystąpień maszyny Wirtualnej) często, i wolisz opóźniony operacje wdrażania na rzecz uproszczenia tych operacji skalowania. scenariusze skalowalnego w poziomie Hello (Dodawanie wystąpień maszyn wirtualnych) nie są odtwarzane w wybranym warstwa trwałości hello, tylko skali — w.

### <a name="operational-recommendations-for-hello-node-type-that-you-have-set-toosilver-or-gold-durability-level"></a>Operacyjne zalecenia dotyczące węzła hello wpisz, że ustawiono trwałości toosilver lub złota poziomu.

1. Zachowaj klastra, a aplikacje dobrej kondycji przez cały czas i upewnij się, że aplikacje odpowiadać tooall [usługi zdarzenia cyklu życia repliki](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (np. repliki w kompilacji jest zablokowana) w odpowiednim czasie.
2. Przyjmuje bezpieczniejsze toomake sposobów zmiany jednostki SKU maszyny Wirtualnej (skalowanie w górę/dół): zmiana hello jednostki SKU maszyny Wirtualnej zestawu skalowania maszyn wirtualnych jest z założenia niebezpieczna operacja i dlatego należy unikać Jeśli to możliwe. Oto proces hello możesz wykonać tooavoid typowych problemów.
    - **Dla elementów innych niż podstawowe NodeType:** zalecane jest tworzenie nowego zestawu skalowania maszyn wirtualnych, zmodyfikować hello usługi umieszczania ograniczenia tooinclude hello nowy węzeł zestaw skalowania maszyny wirtualnej typu i następnie zmniejsz hello starego zestawu skalowania maszyn wirtualnych wystąpienie licznika too0 jednym węźle naraz (jest to toomake się upewnić, że usuwania węzłów hello wpływają na niezawodność hello hello klastra).
    - **Dla hello podstawowy typ nodetype:** firma Microsoft zaleca, nie należy zmieniać SKU wirtualna hello typu węzła podstawowego. Jeśli hello przyczyny hello nowe jednostki SKU jest pojemności, firma Microsoft zaleca, dodając więcej wystąpień, lub jeśli to możliwe, Utwórz nowy klaster. Jeśli użytkownik nie mają wyboru, należy modyfikacje toohello modelu ustawić skali maszyny wirtualnej definicji tooreflect hello nowe jednostki SKU. Jeśli klaster ma tylko jeden typ nodetype, następnie upewnij się, że wszystkie aplikacje stanowe odpowiedzi tooall [usługi zdarzenia cyklu życia repliki](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (np. repliki w kompilacji jest zablokowana) w odpowiednim czasie, który repliki usługi odbudować czas trwania jest mniej niż pięć minut (poziom trwałości srebrny). 


> [!WARNING]
> Zmiana hello rozmiar jednostki SKU maszyny Wirtualnej dla zestawy skalowania maszyny Wirtualnej nie działa przynajmniej srebrny trwałości nie jest zalecane. Zmiana rozmiaru jednostki SKU maszyny Wirtualnej jest operacją destrukcyjnego danych w miejscu infrastruktury. Bez co najmniej kilka możliwości toodelay lub monitor ta zmiana jest możliwe, że hello operacji może spowodować dataloss dla stanowych usług lub późniejsze innych unforseen problemy z działaniem, nawet w przypadku obciążeń bezstanowych. 
> 
    
3. Obsługa minimalna liczba pięć węzłów dla dowolnego zestawu skalowania maszyn wirtualnych z MR włączone
4. Usunąć losowe wystąpień maszyn wirtualnych, nie zawsze używać zestawu skalowania maszyn wirtualnych skali w dół funkcji. Usuwanie Hello losowe wystąpienia maszyny Wirtualnej ma nierówności w wystąpieniu maszyny Wirtualnej hello rozmieszczenie UD i FD możliwości. Ta niezgodność może negatywnie wpłynąć na hello systemów możliwości tooproperly Równoważenie obciążenia między hello usługi wystąpień/usługi replik.
6. Przy użyciu automatycznego skalowania, następnie reguły hello tak ustawić skali w (usuwanie wystąpień maszyny Wirtualnej) są wykonywane tylko jeden węzeł naraz. W czasie skalowania więcej niż jedno wystąpienie nie jest bezpieczne.
7. Jeśli skalowania typu węzła podstawowego, nigdy nie należy go skalować więcej niż zezwala na jakie warstwa niezawodności hello w dół.


## <a name="hello-reliability-characteristics-of-hello-cluster"></a>właściwości niezawodności Hello hello klastra
Witaj warstwa niezawodności służy tooset hello liczby replik hello usług systemowych, które mają toorun w tym klastrze hello typu węzła podstawowego. Witaj hello liczby replik, hello bardziej niezawodny hello systemu znajdują się w klastrze.  

Warstwa niezawodności Hello może zająć hello następujące wartości:

* Platynowa — uruchamianie usług systemowych hello wraz z liczbą zestawu replik docelowy 9
* Gold — uruchamianie usług systemowych hello wraz z liczbą zestawu replik docelowy 7
* Silver — Uruchom hello usługi systemowe z docelowa liczba zestawu replik 5 
* Brązowy — uruchamianie usług systemowych hello z liczbą zestaw docelowy repliki 3

> [!NOTE]
> Warstwa niezawodności Hello wybrane określa hello minimalna liczba węzłów, które muszą mieć typu węzła podstawowego. 
> 
> 


### <a name="recommendations-for-hello-reliability-tier"></a>Zalecenia dotyczące warstwy niezawodności hello.

 Zwiększenie lub zmniejszenie rozmiaru hello klastra (suma hello wystąpień maszyn wirtualnych we wszystkich typach węzła), należy zaktualizować niezawodności hello klastra z jedną warstwę tooanother. W ten sposób wyzwala hello klastra uaktualnień wymagane toochange hello systemu usług repliki zestaw count. Poczekaj hello uaktualnianie w toku toocomplete przed wprowadzeniem żadnych innych zmian toohello klastra, takich jak dodawanie węzłów.  Możesz monitorować postęp hello hello uaktualnienia w narzędziu Service Fabric Explorer lub uruchamiając [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

Poniżej przedstawiono zalecenia hello o wyborze hello warstwa niezawodności.

| **Rozmiar klastra** | **Warstwa niezawodności** |
| --- | --- |
| 1 |Nie określaj hello parametr Warstwa niezawodności, hello system oblicza ona |
| 3 |Brązowy |
| 5 lub 6|Srebrny |
| 7 lub 8 |Gold |
| 9 i nowsze |Platynowa |




## <a name="primary-node-type---capacity-guidance"></a>Typ węzła podstawowego — wskazówki dotyczące wydajności

Oto hello wskazówki dotyczące planowania pojemności typu węzła podstawowego hello

1. **Liczba maszyn wirtualnych wystąpień toorun dowolne produkcji obciążenia na platformie Azure:** należy określić minimalny rozmiar typu węzła podstawowego 5. 
2. **Liczba maszyn wirtualnych wystąpień toorun testów obciążenia w Azure** można określić rozmiar typu węzła podstawowego minimalną 1 lub 3. Witaj jednego węzła klastra, jest uruchamiany z specjalnej konfiguracji i dlatego, skalowania poza tego klastra nie jest obsługiwane. Witaj jednego węzła klastra, ma nie niezawodność i dlatego w szablonie usługi Resource Manager, należy określić, że konfiguracja nie tooremove (nie ustawienie hello wartość konfiguracji nie jest wystarczająco dużo). Po skonfigurowaniu hello jeden węzeł klastra, skonfigurować za pomocą portalu, a następnie automatycznie jest poświęcony na obsługę hello konfiguracji. 1 i 3 klastrów nie są obsługiwane do uruchamiania obciążeń produkcyjnych. 
3. **Maszyna wirtualna SKU:** typu węzła podstawowego jest gdzie hello system usługi są uruchomione, więc hello SKU maszyny Wirtualnej, możesz wybrać, musi uwzględniać całkowity szczytowa hello konta obciążenia można zaplanować tooplace do hello klastra. Oto tooillustrate odpowiednio co I oznacza tutaj — traktować hello węzła podstawowego typu jako sieci "płuca", jest to, co zapewnia inteligencji tooyour tlenu, a więc jeśli inteligencji hello nie można uzyskać wystarczającą ilość tlenu, wystąpi treść. 

Ponieważ wymagana pojemność hello klastra zależy od obciążenia planujesz toorun w klastrze hello, firma Microsoft nie może zawierać jakościowe wskazówki dla określonego obciążenia, jednak w tym miejscu jest toohelp szerokie wskazówki hello, możesz rozpocząć pracę

W przypadku obciążeń produkcyjnych 


- Witaj zalecane SKU maszyny Wirtualnej to standardowa D3 lub standardowy D3_V2 lub równoważne z co najmniej 14 GB lokalny dysk SSD.
- Użycie Hello minimalne obsługiwane SKU maszyny Wirtualnej jest standardowe D1 lub standardowy D1_V2 lub równoważne z co najmniej 14 GB lokalny dysk SSD. 
- Częściowe podstawowej jednostki SKU maszyny Wirtualnej, podobnie jak standardowy A0 nie są obsługiwane w przypadku obciążeń produkcyjnych.
- Standardowy SKU A1 nie jest obsługiwana w przypadku obciążeń produkcyjnych ze względu na wydajność.


## <a name="non-primary-node-type---capacity-guidance-for-stateful-workloads"></a>Typ węzła non-Primary — wskazówki dotyczące pojemności dla obciążeń stanowych

Są to wskazówki dla obciążeń stanowych przy użyciu usługi Service fabric [niezawodnej kolekcje lub reliable Actors](service-fabric-choose-framework.md) działającą w typie podstawowym z systemem innym niż węzeł hello.


**Liczba wystąpień maszyn wirtualnych:** dla obciążeń produkcyjnych, które nie jest obiektem stanowym, zalecane jest, uruchom je wraz z liczbą repliki minimalna i docelowa 5. Oznacza to, że w stanie stabilności na końcu repliki (z zestawu replik) w każdej domenie błędów i domeny uaktualnień. pojęcie warstwy niezawodności całego powitania dla typu węzła podstawowego hello jest toospecify sposób tego ustawienia dla usług systemowych. Tak samo hello kwestia dotyczy tooyour również stanowych usług.

Tak w przypadku obciążeń produkcyjnych hello minimalną zalecaną nie - węzła podstawowego typu rozmiar to 5, jeśli używasz obciążeń stanowych w nim.


**Maszyna wirtualna SKU:** jest typ węzła hello którym działają usługi aplikacji, dlatego hello SKU maszyny Wirtualnej wybierz dla niego musi uwzględniać obciążenia szczytowego hello konta należy zaplanować tooplace w każdym węźle. Witaj wymagana pojemność elementu hello nodetype, zależy od obciążenia, które mają toorun hello klastra, dlatego firma Microsoft nie może zawierać jakościowe wskazówki dla określonego obciążenia, jednak w tym miejscu jest toohelp szerokie wskazówki hello, możesz rozpocząć pracę

W przypadku obciążeń produkcyjnych 

- Witaj zalecane SKU maszyny Wirtualnej to standardowa D3 lub standardowy D3_V2 lub równoważne z co najmniej 14 GB lokalny dysk SSD.
- Użycie Hello minimalne obsługiwane SKU maszyny Wirtualnej jest standardowe D1 lub standardowy D1_V2 lub równoważne z co najmniej 14 GB lokalny dysk SSD. 
- Częściowe podstawowej jednostki SKU maszyny Wirtualnej, podobnie jak standardowy A0 nie są obsługiwane w przypadku obciążeń produkcyjnych.
- Standardowy SKU A1 specjalnie nie jest obsługiwana w przypadku obciążeń produkcyjnych ze względu na wydajność.


## <a name="non-primary-node-type---capacity-guidance-for-stateless-workloads"></a>Typ węzła non-Primary — wskazówki dotyczące wydajności w przypadku obciążeń bezstanowych

W tych wskazówkach bezstanowe uruchomionych na powitania nodetype innej niż podstawowa.

**Liczba wystąpień maszyn wirtualnych:** dla obciążeń produkcyjnych, które są bezstanowych, rozmiar czcionki z systemem innym niż podstawowy węzłami hello minimalna obsługiwana jest 2. Dzięki temu można toorun możesz dwa bezstanowych wystąpienia aplikacji, dzięki czemu toosurvive Twojego usługi hello utraty wystąpienia maszyny Wirtualnej. 

> [!NOTE]
> Jeśli klaster jest uruchomiona usługa sieci szkieletowej wersji mniejszej niż 5.6, powodu wada tooa hello środowiska uruchomieniowego (tego problemu w 5.6), skalowania tooless typu węzła innego niż podstawowy, niż 5, powoduje włączenie zła, dopóki wywołania kondycji klastra [ Usuń ServiceFabricNodeState cmd](https://docs.microsoft.com/powershell/servicefabric/vlatest/Remove-ServiceFabricNodeState) nazwą hello odpowiedni węzeł. Odczyt [wykonać klastra sieci szkieletowej usług lub](service-fabric-cluster-scale-up-down.md) więcej szczegółów
> 
>

**Maszyna wirtualna SKU:** jest typ węzła hello którym działają usługi aplikacji, dlatego hello SKU maszyny Wirtualnej wybierz dla niego musi uwzględniać obciążenia szczytowego hello konta należy zaplanować tooplace w każdym węźle. Witaj wymagana pojemność elementu hello nodetype, zależy od obciążenia, które mają toorun hello klastra, dlatego firma Microsoft nie może zawierać jakościowe wskazówki dla określonego obciążenia, jednak w tym miejscu jest toohelp szerokie wskazówki hello, możesz rozpocząć pracę

W przypadku obciążeń produkcyjnych 


- Witaj zalecane SKU maszyny Wirtualnej to standardowa D3 lub standardowy D3_V2 lub równoważnej. 
- Użycie Hello minimalne obsługiwane SKU maszyny Wirtualnej jest standardowe D1 lub standardowy D1_V2 lub równoważnej. 
- Częściowe podstawowej jednostki SKU maszyny Wirtualnej, podobnie jak standardowy A0 nie są obsługiwane w przypadku obciążeń produkcyjnych.
- Standardowy SKU A1 nie jest obsługiwana w przypadku obciążeń produkcyjnych ze względu na wydajność.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Następne kroki
Po zakończeniu planowania pojemności i konfigurowanie klastra, przeczytaj następujące hello:

* [Zabezpieczenia klastra sieci szkieletowej usług](service-fabric-cluster-security.md)
* [Wprowadzenie modelu kondycji sieci szkieletowej usług](service-fabric-health-introduction.md)
* [Relacja elementów NodeType tooVirtual maszyny skali](service-fabric-cluster-nodetypes.md)

<!--Image references-->
[SystemServices]: ./media/service-fabric-cluster-capacity/SystemServices.png
