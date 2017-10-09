---
title: "aaaService Menedżer zasobów klastra sieci szkieletowej — grup aplikacji | Dokumentacja firmy Microsoft"
description: "Omówienie hello funkcji grupy aplikacji hello zasobu klastra sieci szkieletowej programu Service Manager"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a>Wprowadzenie tooApplication grup
Menedżer zasobów klastra usługi sieć szkieletowa zwykle zarządza zasobami klastra przez rozłożenie obciążenia hello (reprezentowane przez [metryki](service-fabric-cluster-resource-manager-metrics.md)) równomiernie w całej hello klastra. Usługa Service Fabric zarządza pojemności hello węzłów hello hello i klastrze hello jako całość przy użyciu [pojemności](service-fabric-cluster-resource-manager-cluster-description.md). Metryki i wydajność pracy wygodne w przypadku wielu obciążeń, ale wzorców, które w znacznym stopniu wykorzystywane różnych wystąpień aplikacji sieci szkieletowej usług czasami przenieść dodatkowe wymagania. Na przykład można:

- Niektóre wydajność hello węzłach klastra hello hello usług w ramach wystąpienia niektórych aplikacji o nazwie rezerwowa
- Ogranicz hello całkowitą liczbę węzłów, które usługi hello w wystąpieniu o nazwie aplikacji są uruchomione na (zamiast rozkładanie je za pośrednictwem hello całego klastra)
- Definiowanie pojemności na powitania aplikacji nazwane wystąpienie toolimit hello liczbę usług lub Suma zużycie zasobów usług hello w nim

toomeet tych wymagań, hello zasobu klastra sieci szkieletowej programu Service Manager obsługuje funkcję grupy aplikacji.

## <a name="limiting-hello-maximum-number-of-nodes"></a>Ograniczanie hello maksymalna liczba węzłów
Witaj najprostszym przypadek użycia pojemności aplikacji jest gdy wystąpienie aplikacji musi toobe ograniczone tooa niektórych maksymalną liczbę węzłów. Zakłada skonsolidowanie obsługi wszystkich usług w ramach danego wystąpienia aplikacji na zestaw liczby maszyn. Konsolidacja jest przydatne, gdy próbujesz toopredict lub cap użycia zasobów fizycznych przez usługi hello w ramach tego wystąpienia nazwanego aplikacji. 

Witaj poniższy obraz przedstawia wystąpienie aplikacji z włączonymi i wyłączonymi maksymalną liczbę węzłów zdefiniowane:

<center>
![Maksymalna liczba węzłów Definiowanie wystąpienia aplikacji][Image1]
</center>

W przykładzie po lewej stronie powitania aplikacji hello nie ma maksymalną liczbę węzłów zdefiniowane, i ma trzy usługi. Witaj Menedżera zasobów klastra ma rozszerzane wszystkie repliki na sześciu dostępne węzły tooachieve hello równowagę w klastrze hello (hello domyślne zachowanie). W przykładzie prawo hello widzimy hello węzłów toothree ograniczone tej samej aplikacji.

Parametr Hello, który kontroluje to zachowanie jest nazywany wartość MaximumNodes. Ten parametr można ustawić podczas tworzenia aplikacji lub aktualizacji dla wystąpienia aplikacji, która została już uruchomiona.

PowerShell

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

C#

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

W ramach hello zestawu węzłów hello Menedżera zasobów klastra nie gwarantuje obiekty, które usługa uzyskać umieszczone razem lub pobrać używane węzły, które.

## <a name="application-metrics-load-and-capacity"></a>Metryki aplikacji, obciążenia i pojemności
Grupy aplikacji pozwalają również metryki toodefine skojarzonych z wystąpienia danej aplikacji o nazwie i wydajności danego wystąpienia aplikacji dla tych metryki. Metryki aplikacji pozwalają tootrack, rezerwy oraz zużycie zasobów hello limit usług hello wewnątrz tego wystąpienia aplikacji.

Dla każdej aplikacji metryki istnieją dwie wartości, które można ustawić:

- **Całkowita liczba aplikacji, zdolność** — to ustawienie reprezentuje hello całkowita pojemność aplikacji hello dla określonej metryki. Hello Menedżera zasobów klastra nie zezwala na powitania tworzenia nowych usług, w ramach tego wystąpienia aplikacji, spowodowałoby tooexceed całkowite obciążenie tej wartości. Na przykład załóżmy, że wystąpienie aplikacji hello pojemności 10 ma już obciążenia pięć. Hello tworzenia usługi z obciążeniem całkowita domyślne 10 będzie niedozwolone.
- **Maksymalna pojemność węzła** — to ustawienie określa maksymalne obciążenie całkowita hello aplikacji hello w jednym węźle. Jeśli obciążenie odbywa się za pośrednictwem tej pojemności, hello Menedżera zasobów klastra przenosi węzłów tooother repliki tak, aby hello obciążenia zmniejsza.


Środowiska PowerShell:

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

C#:

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a>Rezerwacji pojemności
Inne typowe zastosowanie dla grup aplikacji jest tooensure, że zasoby w hello klastra są zastrzeżone dla wystąpienia danej aplikacji. Po utworzeniu wystąpienia aplikacji hello, zawsze jest zarezerwowane miejsce Hello.

Rezerwacji miejsca w klastrze powitania dla aplikacji hello się natychmiast stanie nawet wtedy, gdy:
- wystąpienie aplikacji Hello jest tworzony, ale nie ma jeszcze żadnych usług w niej
- Witaj liczba usług w ramach zmian wystąpienia aplikacji hello zawsze 
- Witaj usługi istnieje, ale nie korzysta z zasobów hello 

Rezerwacji zasobów dla wystąpienia aplikacji wymaga określenia dwóch dodatkowych parametrów: *MinimumNodes* i *NodeReservationCapacity*

- **Wartość MinimumNodes** — definiuje hello minimalna liczba węzłów, które aplikacji hello wystąpienia nie powinna działać.  
- **NodeReservationCapacity** — jest to ustawienie na metrykę dla aplikacji hello. wartość Hello jest hello ilość tego Metryka zastrzeżone dla aplikacji hello w każdym węźle, w przypadku, gdy hello usług w tej aplikacji, uruchom.

Łączenie **MinimumNodes** i **NodeReservationCapacity** gwarancje rezerwacji minimalna obciążenia dla aplikacji hello w ramach klastra hello. W przypadku pozostałych mniej pojemności w hello klastra niż wymagana Rezerwacja całkowita hello, tworzenie aplikacji hello zakończy się niepowodzeniem. 

Oto przykład rezerwacji pojemności:

<center>
![Definiowanie pojemności zastrzeżone wystąpień aplikacji][Image2]
</center>

W przykładzie po lewej stronie powitania aplikacji nie mają żadnych zdefiniowano zdolności produkcyjnych aplikacji. Witaj Menedżera zasobów klastra równoważy wszystko zgodnie z zasadami toonormal.

W przykładzie hello na powitania prawo Załóżmy, że czy Application1 został utworzony z hello następujące ustawienia:

- Wartość MinimumNodes tootwo zestawu
- Metryka zdefiniowana z aplikacji
  - NodeReservationCapacity 20

PowerShell

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

C#

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

Sieć szkieletowa usług rezerw pojemności na dwóch węzłów w Application1 i nie można używać usług z tooconsume Aplikacja2 wydajność nawet jeśli istnieją takie obciążenia jest są używane przez usługi hello wewnątrz Application1 w czasie hello. Pojemność ten zastrzeżony aplikacji jest uznawany za używane i hello pozostająca w tym węźle, a w ramach klastra hello jest za mała.  zastrzeżenie Hello jest odejmowany od hello pozostająca klastra natychmiast, jednak zastrzeżone hello zużycie jest odejmowany od pojemności hello określonego węzła tylko wtedy, gdy co najmniej jedną usługę obiekt znajduje się na nim. Tego zastrzeżenia nowsze umożliwia elastyczność i lepsze wykorzystanie zasobów, ponieważ zasoby są tylko zarezerwowane na węzłach w razie potrzeby.

## <a name="obtaining-hello-application-load-information"></a>Uzyskiwanie informacji o obciążenia aplikacji hello
Dla każdej aplikacji, który posiada zdefiniowane dla co najmniej jedną metrykę zdolność aplikacji można uzyskać hello informacji na temat hello obciążenia agregacji zgłoszone przez repliki z jego usług.

Środowiska PowerShell:

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

C#

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

Witaj ApplicationLoad zapytanie zwraca hello podstawowe informacje o wydajności aplikacji, który został określony dla aplikacji hello. Informacje te obejmują informacje o węzłach minimalna i maksymalna liczba węzłów hello i hello liczba, która obecnie zajmuje aplikacji hello. Zawiera także informacje o każdym Metryka obciążenia aplikacji, w tym:

* Nazwa metryki: Nazwa metryki hello.
* Reservationcapacity: Pojemności klastra w klastrze hello zarezerwowane dla tej aplikacji.
* Obciążenia aplikacji: Całkowita liczba obciążenia replik podrzędnych tej aplikacji.
* Pojemność aplikacji: Maksymalna dopuszczalna wartość obciążenia aplikacji.

## <a name="removing-application-capacity"></a>Usuwanie aplikacji, zdolność
Po ustawieniu parametrów aplikacji, zdolność powitania dla aplikacji, można je usunąć za pomocą poleceń cmdlet interfejsów API aplikacji aktualizacji lub programu PowerShell. Na przykład:

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

To polecenie usuwa wszystkie parametry zarządzania wydajności aplikacji z wystąpienia aplikacji hello. W tym MinimumNodes, wartość MaximumNodes i metryki aplikacji hello, jeśli istnieje. Witaj hello polecenie powoduje natychmiastowe. Po wykonaniu tego polecenia, hello Menedżera zasobów klastra używa hello domyślne zachowanie związanych z zarządzaniem aplikacjami. Parametry pojemność aplikacji można określić ponownie za pomocą `Update-ServiceFabricApplication` / `System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.

### <a name="restrictions-on-application-capacity"></a>Ograniczenia dotyczące wydajności aplikacji
Istnieje kilka ograniczeń w parametrach wydajność aplikacji, które muszą zostać zachowane. Jeśli występują błędy sprawdzania poprawności żadne zmiany nie została wykonana.

- Wszystkie parametry liczba całkowita musi być liczby nieujemnej.
- Wartość MinimumNodes nigdy nie może być większa niż wartość MaximumNodes.
- Jeśli zdefiniowano wydajności dla metryki obciążenia, są one musi wykonać następujące czynności:
  - Węzeł rezerwacji pojemność nie może być większa niż maksymalna pojemność węzła. Nie można na przykład ograniczyć hello pojemność hello metryki "CPU" hello węzła tootwo jednostki i spróbuj tooreserve trzy jednostki w każdym węźle.
  - Jeśli określono wartość MaximumNodes, następnie produktu hello MaximumNodes i maksymalna pojemność węzła nie może być większa niż całkowita pojemność aplikacji. Na przykład załóżmy, że hello maksymalna pojemność węzła metryki obciążenia, ustawione tooeight "CPU". Również Załóżmy, że ustawisz hello too10 maksymalna liczba węzłów. W takim przypadku całkowita pojemność aplikacji musi być większa niż 80 dla ta metryka obciążenia.

ograniczenia dotyczące Hello są wymuszane, zarówno podczas tworzenia aplikacji i aktualizacji.

## <a name="how-not-toouse-application-capacity"></a>W jaki sposób toouse wydajności aplikacji
- Nie próbuj grupy aplikacji hello toouse funkcji tooa aplikacji hello tooconstrain _określonych_ podzbioru węzłów. Innymi słowy, można określić, że aplikacja hello działa na maksymalnie pięć węzłów, ale nie których określonych pięć węzłów w klastrze hello. Ograniczający toospecific aplikacji węzłów można osiągnąć za pomocą ograniczenia umieszczania usług.
- Nie próbuj tooensure pojemność aplikacji hello toouse czy dwie usługi z tej samej aplikacji są umieszczane na powitania hello samych węzłów. Zamiast tego użyj [koligacji](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) lub [ograniczenia umieszczania](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).

## <a name="next-steps"></a>Następne kroki
- Aby uzyskać więcej informacji na temat konfigurowania usługi [Dowiedz się więcej o konfigurowaniu usługi](service-fabric-cluster-resource-manager-configure-services.md)
- toofind limit o jak hello Menedżera zasobów klastra zarządza i równoważy obciążenie klastra hello wyewidencjonować hello artykułu na [równoważenia obciążenia](service-fabric-cluster-resource-manager-balancing.md)
- Rozpocznij od początku hello i [uzyskać toohello wprowadzenie zasobu klastra sieci szkieletowej programu Service Manager](service-fabric-cluster-resource-manager-introduction.md)
- Aby uzyskać więcej informacji na temat działania metryki ogólnie rzecz biorąc, przeczytaj na [metryki obciążenia sieci szkieletowej usług](service-fabric-cluster-resource-manager-metrics.md)
- Witaj Menedżera zasobów klastra ma wiele opcji opisujące hello klastra. toofind się więcej na ich temat, zapoznaj się w tym artykule na [opisujące klastra sieci szkieletowej usług](service-fabric-cluster-resource-manager-cluster-description.md)

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
