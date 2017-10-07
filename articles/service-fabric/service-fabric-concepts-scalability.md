---
title: "aaaScalability usługi sieć szkieletowa usług | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooscale usług sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ed324f23-242f-47b7-af1a-e55c839e7d5d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5af06f8f71ad5dee32ba115b922842684867e654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-in-service-fabric"></a>Skalowanie w sieci szkieletowej usług
Sieć szkieletowa usług Azure umożliwia łatwe toobuild skalowalnych aplikacji przez zarządzanie hello usług, partycji i replik na powitania węzły klastra. Uruchomiony wielu obciążeń hello na tym samym wykorzystanie zasobów maksymalną umożliwia sprzętu, ale również zapewnia elastyczność pod względem sposobu wybranego tooscale obciążeń. 

Skalowanie w sieci szkieletowej usług odbywa się na kilka różnych sposobów:

1. Skalowanie przez tworzenie lub usuwanie wystąpienia usługi bezstanowej
2. Skalowanie przez tworzenia lub usuwania nowych o nazwie usługi
3. Skalowanie przez tworzenia lub usuwania nowych nazwane wystąpienia aplikacji
4. Skalowanie za pomocą usług podzielonym na partycje
5. Skalowanie przez dodawanie i usuwanie węzłów z klastra hello 
6. Skalowanie przy użyciu metryk Menedżera zasobów klastra

## <a name="scaling-by-creating-or-removing-stateless-service-instances"></a>Skalowanie przez tworzenie lub usuwanie wystąpienia usługi bezstanowej
Jeden z hello najprostszy sposób tooscale w sieci szkieletowej usług współpracuje z usług bezstanowych. Podczas tworzenia usługi bezstanowej, możesz uzyskać toodefine szansy `InstanceCount`. `InstanceCount`Określa, ile działających kopii tej usługi kodu są tworzone podczas uruchamiania usługi hello. Załóżmy na przykład, czy 100 węzłów w klastrze hello. Również Załóżmy, że usługa jest tworzony z `InstanceCount` 10. W czasie wykonywania tych 10 uruchomionej kopii hello kod może wszystkie stać się zbyt zajęty (lub może nie być wystarczająco zajęty). Jednym ze sposobów tooscale aby obciążenie jest toochange hello liczba wystąpień. Na przykład niektóre fragment kodu, monitorowania i zarządzania można zmienić liczbę istniejących hello too50 wystąpień lub too5, w zależności od tego, czy obciążenie hello musi tooscale przychodzący lub wychodzący hello na podstawie obciążenia. 

C#:

```csharp
StatelessServiceUpdateDescription updateDescription = new StatelessServiceUpdateDescription(); 
updateDescription.InstanceCount = 50;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

Środowiska PowerShell:

```posh
Update-ServiceFabricService -Stateless -ServiceName $serviceName -InstanceCount 50
```
### <a name="using-dynamic-instance-count"></a>Przy użyciu dynamicznych liczba wystąpień
W szczególności w przypadku usług bezstanowych sieci szkieletowej usług oferuje automatyczny sposób toochange hello l iczba wystąpień. Dzięki temu tooscale usługi hello dynamicznie z hello liczba węzłów, które są dostępne. tooopt sposób Hello do to zachowanie jest liczba wystąpień hello tooset = -1. Wartość InstanceCount = -1 jest tooService instrukcji sieci szkieletowej, stwierdzający "Uruchamianie tej usługi bezstanowej na każdym węźle." W przypadku zmiany hello liczba węzłów, sieci szkieletowej usług automatycznie zmienia hello toomatch liczba wystąpień, sprawdzeniu, czy usługa hello jest uruchomiona na wszystkich węzłach prawidłowe. 

C#:

```csharp
StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
//Set other service properties necessary for creation....
serviceDescription.InstanceCount = -1;
await fc.ServiceManager.CreateServiceAsync(serviceDescription);
```

Środowiska PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName -Stateless -PartitionSchemeSingleton -InstanceCount "-1"
```

## <a name="scaling-by-creating-or-removing-new-named-services"></a>Skalowanie przez tworzenia lub usuwania nowych o nazwie usługi
Wystąpienie usługi o nazwie jest określonego wystąpienia typu usługi (zobacz [cyklu życia aplikacji w sieci szkieletowej usług](service-fabric-application-lifecycle.md)) w ramach niektóre wystąpienia nazwanego aplikacji hello klastra. 

Nowe wystąpienia usługi o nazwie można utworzyć (lub usunięte) jako usługi staną się bardziej lub mniej zajęty. Dzięki temu toobe żądań rozmieszczenie więcej wystąpień usługi, zwykle zwiększając obciążenia istniejących toodecrease usług. Podczas tworzenia usługi, hello zasobu klastra sieci szkieletowej programu Service Manager umieszcza usług hello hello klastra w sposób rozproszonych. dokładne decyzje Hello są regulowane przez hello [metryki](service-fabric-cluster-resource-manager-metrics.md) hello klastra i inne zasady umieszczania. Usługi mogą być tworzone na kilka różnych sposobów, ale hello najczęściej są przez działania administracyjne, takie jak ktoś wywoływania [ `New-ServiceFabricService` ](https://docs.microsoft.com/en-us/powershell/module/servicefabric/new-servicefabricservice?view=azureservicefabricps), lub przez wywołanie kodu [ `CreateServiceAsync` ](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync?view=azure-dotnet). `CreateServiceAsync`Można nawet można wywoływać z wewnątrz innych usług uruchomionych w klastrze hello.

Dynamicznie tworzenie usług mogą być używane w szerokiej gamy scenariuszy i jest wspólnym wzorcem. Rozważmy na przykład usługi stanowej, która reprezentuje określonego przepływu pracy. Połączenia reprezentującą pracy będzie tooshow toothis usługi, a ta usługa jest będzie tooexecute hello kroki toothat przepływu pracy i rejestrowanie postępu. 

Jak można utworzyć tej skali określonej usługi? Hello usługi może być wielodostępne w pewnej formy i akceptować połączeń i zaczną działać poza kroki dla wielu różnych wystąpień hello takie same w całości w przepływie pracy. Który ułatwia kodu hello bardziej złożonej, ponieważ aktualnie tooworry o wiele różnych wystąpień hello tym samym przepływie pracy, wszystko na różnych etapach oraz od innych klientów. Ponadto obsługa wielu przepływów pracy w czasie hello, w tym samym czasie nie rozwiąże problem skali hello. Jest to spowodowane w pewnym momencie tej usługi zużywa zbyt wiele toofit zasobów na określonym komputerze. Wiele usług nie jest skompilowany dla tego wzorca w miejscu pierwszego hello również wystąpić problemy wąskich gardeł związanego z używaniem toosome lub spowolnienie ich kodu. Tego rodzaju problemy spowodować hello usługi nie toowork również w przypadku większych pobiera hello liczbę jednoczesnych przepływów pracy, który go służy do śledzenia.  

Rozwiązanie jest toocreate wystąpienie tej usługi, dla każdego innego wystąpienia przepływu pracy hello ma tootrack. To jest doskonałym wzorca i działa, czy usługa hello jest bezstanowych i stanowych. Dla tego toowork wzorzec jest zwykle innej usługi, która działa jako "Usługa Menedżera obciążenia". zadanie Hello tej usługi jest tooreceive żądań i tooroute tych usług tooother żądań. Menedżer Hello można dynamicznie utworzyć wystąpienia usługi Obciążenie powitania po odebraniu wiadomości powitania, a następnie przekazać na żądania toothose usług. Usługa Menedżera Hello również otrzymać wywołania zwrotne usługi danego przepływu pracy wykonuje swojego zadania. Gdy Menedżer hello odbiera tych wywołań zwrotnych go można usunąć to wystąpienie usługi przepływu pracy hello lub pozostaw Jeśli oczekiwano kolejnych wywołań. 

Zaawansowane wersje tego typu manager można też tworzyć pul usługami hello, którymi zarządza. puli Hello pomaga, upewnij się, że gdy nowe żądanie nie ma toowait dla toospin usługi hello. Zamiast tego hello Menedżera można po prostu wybierz usługi przepływu pracy, który nie jest aktualnie zajęty z puli hello lub losowo trasy. Utrzymywanie puli usług dostępnych przyspiesza nowych żądań obsługi, ponieważ jest mniej prawdopodobne Żądanie hello miał toowait dla nowych toobe usługi przejścia. Tworzenie nowych usług szybki, ale nie jest wolnego lub natychmiastowe. Pula Hello minimalizuje hello ilość czasu, Żądanie hello ma toowait przed są obsługiwane. Często zobaczysz tego wzorca manager i puli, gdy czas reakcji najważniejsze hello. Kolejkowania wiadomości powitania żądania i tworzenia usługi hello w tle hello i _następnie_ przekazaniem go to również popularnych Menedżera wzorzec, tworzenie i usuwanie usług w oparciu o niektórych śledzenie hello ilość pracy usługi obecnie ma oczekujące. 

## <a name="scaling-by-creating-or-removing-new-named-application-instances"></a>Skalowanie przez tworzenia lub usuwania nowych nazwane wystąpienia aplikacji
Tworzenie i usuwanie instancji całej aplikacji jest podobnego wzorca toohello tworzenie i usuwanie usług. Dla tego wzorca jest niektóre usługi Menedżera, która jest wprowadzenie hello decyzji na podstawie żądań hello, które go ma do czynienia i innych usług, wewnątrz klastra hello hello hello informacje, które otrzymuje się z. 

Podczas tworzenia nowego wystąpienia nazwanego aplikacji stosuje się zamiast tworzyć nowe wystąpienia usługi o nazwie w istniejącej aplikacji? Istnieje kilka przykładów:

  * nowe wystąpienie aplikacji Hello jest dla danego klienta, którego kod wymaga toorun w ramach niektórych określonej tożsamości lub ustawienia zabezpieczeń.
    * Sieć szkieletowa usług umożliwia definiowanie toorun pakietów inny kod obszarze określonej tożsamości. W kolejności toolaunch hello tego samego pakietu kodu w różnych tożsamości, aktywacji hello konieczne toooccur w innej aplikacji wystąpień. Rozważmy, gdzie masz istniejący klient obciążeń wdrożonych. Te może być uruchomiony w ramach określonej tożsamości, dzięki czemu może monitorować i kontrolować ich dostęp do zasobów tooother, takie jak zdalne bazy danych lub innych systemów. W takim przypadku po zarejestrowaniu nowego klienta, prawdopodobnie nie ma tooactivate ich kodu w hello samym kontekście (proces miejsca). Gdy użytkownik może utrudnia dla Twojej usługi tooact kod w kontekście hello określonej tożsamości. Zazwyczaj należy więcej zabezpieczeń, izolacji i kod zarządzania tożsamościami. Zamiast używać różnych o nazwie usługi wystąpień poziomu tego samego wystąpienia aplikacji hello i dlatego hello tą samą przestrzenią procesu, można użyć różnych nazwane wystąpienia aplikacji sieci szkieletowej usług. Dzięki temu łatwiejsze toodefine tożsamości różnych kontekstach.
  * nowe wystąpienie aplikacji Hello służy również jako środek konfiguracji
    * Domyślnie wszystkie nazwane wystąpienia usługi typu określonej usługi, w ramach wystąpienia aplikacji hello zostanie uruchomiony w hello tego samego procesu w danym węźle. Co to oznacza to, że podczas każdego wystąpienia usługi można skonfigurować inaczej, jest to skomplikowane. Usługi muszą mieć niektóre token używają toolook się ich konfiguracji w ramach pakietu konfiguracji. Zazwyczaj jest to tylko nazwę hello usługi. To działa prawidłowo, ale jego pozamałżeńskie hello konfiguracji toohello nazwy wystąpień poszczególnych usługi o nazwie hello w ramach danego wystąpienia aplikacji. Może to być mylące i twardych toomanage od konfiguracji jest zwykle artefaktem czasu projektowania, z określonymi wartościami wystąpienie aplikacji. Utworzenie większej liczby usług zawsze powoduje więcej uaktualnień aplikacji toochange hello informacji w ramach pakietów config hello lub toodeploy nowe tak, aby nowe usługi hello można wyszukiwać ich określone informacje. Często jest łatwiejsze toocreate całkiem nowe wystąpienia nazwanego aplikacji. Następnie można tooset parametrów aplikacji hello niezależnie od konfiguracji jest niezbędna dla hello usług. W ten sposób wszystkie usługi hello, które są tworzone w ramach których nazwane wystąpienie aplikacji może dziedziczyć ustawień określonej konfiguracji. Na przykład zamiast pojedynczym pliku konfiguracji z hello ustawień i dostosowań dla każdego klienta, takich jak tajemnice lub na ograniczenia zasobów klienta, zamiast tego trzeba inną aplikację dla poszczególnych klientów przy użyciu tych ustawień przesłonięcia. 
  * Nowa aplikacja Hello służy jako granica uaktualnienia
    * W ramach usługi Service Fabric inną aplikację nazwanego wystąpienia służyć jako granic w celu uaktualnienia. Uaktualnienie jednego wystąpienia nazwanego aplikacji nie ma wpływu hello kod, który jest uruchomione inne wystąpienie nazwane aplikacji. Witaj różnych aplikacji zakończą się z różnymi wersjami hello sam kod na powitania samych węzłów. Może to być czynnikiem, gdy będziesz potrzebować toomake skalowania decyzji, ponieważ można wybrać, czy hello nowego kodu należy stosować hello sam uaktualnia jako inną usługę lub nie. Załóżmy, że wywołanie dociera hello Menedżera usługi, która jest odpowiedzialna za skalowania obciążeń określonego klientów przez tworzenie i usuwanie usług dynamicznie. W takim przypadku wywołania hello jest jednak dla obciążenia związane z _nowe_ klienta. Większość klientów, takich jak są odizolowane od siebie nie tylko ze względów hello zabezpieczeń i konfiguracji wymienionymi wcześniej, ale ponieważ zapewnia większą elastyczność w zakresie określonym wersjami hello oprogramowania i wybierania po ich można uaktualnić. Może także utworzyć nowe wystąpienie aplikacji oraz tworzenie usługi hello po prostu toofurther partycji hello ilość Twojej usługi, które będzie touch żadnych jedno uaktualnienie. Aplikacji osobnych wystąpień zapewniają większy poziom szczegółowości podczas wykonywania uaktualnienia aplikacji, a także włączyć A / B wdrożeń testowych i niebieski/zielony. 
  * istniejące wystąpienie aplikacji Hello jest pełny
    * W sieci szkieletowej usług [aplikacji, zdolność](service-fabric-cluster-resource-manager-application-groups.md) to pojęcie, której można toocontrol hello ilość zasobów dostępnych wystąpień określonej aplikacji. Na przykład może zdecydować, że dana usługa musi toohave innego wystąpienia utworzone w kolejności tooscale. Jednak to wystąpienie aplikacji jest poza pojemność dla niektórych metryki. Jeśli tego konkretnego klienta lub obciążenie może nadal być przyznany więcej zasobów, następnie należy można zwiększyć pojemność istniejących powitania dla tej aplikacji albo utwórz nową aplikację. 

## <a name="scaling-at-hello-partition-level"></a>Skalowanie w poziomie hello partycji
Sieć szkieletowa usług obsługuje partycjonowanie. Partycjonowanie dzieli usługi na kilku sekcji logicznej i fizycznej, z których każdy działa niezależnie. To jest przydatne w przypadku usługi stanowej, ponieważ nikt zestawu replik ma toohandle wszystkie wywołania hello i manipulowania wszystkie stanu hello jednocześnie. Witaj [partycjonowania omówienie](service-fabric-concepts-partitioning.md) zawiera informacje na temat typów hello partycjonowania systemów, które są obsługiwane. Witaj replik każdej partycji są rozkładane między hello węzłów w klastrze, dystrybucji obciążenia tej usługi i zapewnienie, że żadna usługa hello jako całość lub dowolnej partycji ma pojedynczy punkt awarii. 

Należy wziąć pod uwagę usługę korzystającą z ranged schemat partycjonowania niska wartość klucza o wartości 0, wysoka wartość klucza 99 i liczba partycji, 4. W trzech węzłów klastra hello usługi może być rozmieszczona z czterech replik, które współużytkują zasoby hello w każdym węźle, jak pokazano poniżej:

<center>
![Układ partycji z trzech węzłów](./media/service-fabric-concepts-scalability/layout-three-nodes.png)
</center>

Jeśli zwiększysz hello liczba węzłów, sieci szkieletowej usług przeniesie niektórych istniejących replik hello istnieje. Na przykład załóżmy, że hello liczba węzłów zwiększa toofour uzyskać dystrybuowany hello replik. Teraz usługi hello ma teraz replik trzy uruchomione w każdym węźle, każdy należących toodifferent partycji. Umożliwia to lepsze wykorzystanie zasobów, ponieważ hello nowy węzeł nie jest zimnych. Zazwyczaj również zwiększa wydajność, ponieważ każda usługa ma więcej tooit dostępne zasoby.

<center>
![Układ partycji z czterech węzłów](./media/service-fabric-concepts-scalability/layout-four-nodes.png)
</center>

## <a name="scaling-by-using-hello-service-fabric-cluster-resource-manager-and-metrics"></a>Skalowanie za pomocą hello zasobu klastra sieci szkieletowej programu Service Manager i metryki
[Metryki](service-fabric-cluster-resource-manager-metrics.md) są jak usługi express ich tooService zużycia zasobów sieci szkieletowej. Za pomocą metryki daje możliwość tooreorganize hello Menedżera zasobów klastra i zoptymalizować układ hello hello klastra. Na przykład może istnieć wiele zasobów w klastrze hello, ale ich może nie zostać przydzielony toohello usług, które są aktualnie podczas pracy. Przy użyciu metryk umożliwia hello tooreorganize Menedżera zasobów klastra hello tooensure klastra, że usługi mają dostęp toohello dostępnych zasobów. 


## <a name="scaling-by-adding-and-removing-nodes-from-hello-cluster"></a>Skalowanie przez dodawanie i usuwanie węzłów z klastra hello 
Inną opcją w przypadku skalowania z sieci szkieletowej usług jest rozmiarem hello toochange hello klastra. Zmiana rozmiaru hello hello klastra oznacza dodawania lub usuwania węzłów z co najmniej jednego z typów węzłów hello hello klastra. Na przykład rozważmy przykład, gdzie są wszystkie hello węzły w klastrze hello gorących. Oznacza to, czy zasoby klastra hello są prawie wszystkie używane. W takim przypadku dodanie więcej toohello węzłów klastra jest hello najlepsze sposób tooscale. Po hello nowe węzły join hello klastra hello zasobu klastra sieci szkieletowej programu Service Manager przenosi toothem usług, co mniej całkowitego obciążenia na powitania istniejących węzłów. Dla usług bezstanowych z liczbą wystąpień = -1, usługa więcej wystąpień są tworzone automatycznie. Dzięki temu niektórych toomove wywołania z hello istniejących węzłów toohello nowe węzły. 

Dodawanie i usuwanie toohello węzłów klastra można zrealizować przy użyciu modułu programu PowerShell dla usługi sieci szkieletowej Azure Resource Manager hello.

```posh
Add-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName  -NumberOfNodesToAdd 5 
Remove-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName -NumberOfNodesToRemove 5
```

## <a name="putting-it-all-together"></a>Składanie wszystkiego razem
Rozwiąż wszystkie pomysły hello, które firma Microsoft zostały omówione w tym miejscu i komunikują się za pośrednictwem przykład. Należy wziąć pod uwagę hello następujące usługi: próbujesz się toobuild usługi, który działa jako książkę adresową zawierający na toonames i informacje kontaktowe. 

Bezpośrednio na początku masz licznych tooscale powiązane pytania: jak w przypadku wielu użytkowników są toohave będzie? Ile kontaktów zapisze każdego użytkownika? Gdy użytkownik są stałego przy hello z usługi po raz pierwszy jest trudne próby toofigure, to wszystkie limit. Załóżmy, że zostały będzie toogo z jedną usługą statycznych wraz z liczbą określonej partycji. konsekwencje Hello pobrania hello błędne liczby partycji może spowodować problemy skali toohave później. Podobnie nawet jeśli pobranie wszystkich informacji hello hello liczba prawo, nie może być konieczne. Na przykład masz również toodecide hello rozmiar klastra hello na początku zakresie hello liczbę węzłów i ich rozmiary. Toopredict zwykle twardych jego liczby zasobów, usługa będzie tooconsume swojego okresu istnienia. Można też twardych tooknow wcześniejsze czasu hello ruchu wzorzec, który faktycznie widzi hello usługi. Na przykład osób może być dodać i usunąć swoje kontakty tylko po pierwsze rano hello lub może on jest rozłożona równomiernie hello porach dnia hello. Na podstawie tych potrzebne tooscale i dynamicznie. Może być nauczysz toopredict i zacząć tooneed tooscale, ale w obu przypadkach prawdopodobnie będzie zużycie zasobów toochanging tooreact tooneed przez usługę. Może to obejmować zmiana rozmiaru hello hello klastra w kolejności tooprovide więcej zasobów podczas reorganizacja korzystanie z istniejących zasobów nie jest wystarczająca. 

Ale Dlaczego nawet spróbuj toopick schemat jednej partycji wychodzących dla wszystkich użytkowników? Dlaczego należy ograniczyć samodzielnie tooone usługi i jeden klaster statycznych? Witaj rzeczywistych sytuacji jest zazwyczaj bardziej dynamiczne. 

Podczas budowania skali, należy wziąć pod uwagę hello następującego wzorca dynamicznych. Może być konieczne tooadapt on tooyour sytuacji:

1. Zamiast w trakcie toopick schemat partycjonowania dla wszystkich użytkowników na początku, kompilacji "manager service".
2. zadanie Hello usługi Menedżera hello jest toolook klienta informacje o rejestracji usługi. A następnie w zależności od tych informacji usługi Menedżera hello Utwórz wystąpienie użytkownika _rzeczywiste_ skontaktuj się z magazynu usługi _tylko dla tego klienta_. Wymagają one określonej konfiguracji, izolacji lub uaktualnień, można również określić toospin wystąpienia aplikacji dla tego klienta. 

To tworzenie dynamicznych wzorca wiele korzyści:

  - Możesz nie próbujesz liczba partycji poprawne hello tooguess dla wszystkich użytkowników na początku lub utworzyć pojedynczą usługą, która jest nieskończenie skalowalny na jego własnej. 
  - Różni użytkownicy nie mają hello toohave partycji sama liczba, liczba replik, ograniczenia umieszczania, metryki, obciążenia domyślne, nazwy usługi, ustawienia dns lub żadnego hello inne właściwości określone na powitania usługi lub aplikacji. 
  - Możesz uzyskać segmentacji dodatkowe dane. Każdy klient ma swoje własne kopie hello usługi
    - Można konfigurować inaczej i przyznane więcej lub mniej zasobów, przy więcej lub mniej partycji i replik w razie potrzeby, w oparciu o ich oczekiwana Skala każdej usługi klienta.
      - Na przykład powitania klienta uregulowaniu płatności hello warstwy "Złota" — można ich pobrać więcej repliki lub większa liczba partycji i potencjalnie zasobów dedykowanych tootheir usług za pomocą możliwości metryki i aplikacji.
      - Lub Wypowiedz one podane informacje wskazujące hello liczbę kontaktów zachodzi potrzeba został "Mała" — jak tylko kilka partycje lub nawet mogą być wprowadzane w puli usług udostępnionych z innymi klientami.
  - Nie używasz licznych wystąpienie usługi lub replik w czasie oczekiwania dla klientów tooshow w górę
  - Jeśli kiedykolwiek wyjdzie klienta, następnie usuwania ich informacji z usługi jest tak proste, jak ponieważ Menedżer hello usunąć tę usługę lub aplikację, utworzony.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji dotyczących pojęć sieci szkieletowej usług zobacz następujące artykuły hello:

* [Dostępność usług sieci szkieletowej usług](service-fabric-availability-services.md)
* [Partycjonowanie usług sieci szkieletowej usług](service-fabric-concepts-partitioning.md)
