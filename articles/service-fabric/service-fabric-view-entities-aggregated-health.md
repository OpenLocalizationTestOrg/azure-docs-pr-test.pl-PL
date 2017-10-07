---
title: "jednostek aaaHow tooview sieć szkieletowa usług Azure zagregowane kondycji | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooquery, wyświetlać i oceniania kondycji zagregowane jednostki sieci szkieletowej usług Azure, za pomocą zapytań o kondycję i ogólne zapytania."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a>Wyświetl raporty dotyczące kondycji sieci szkieletowej usług
Sieć szkieletowa usług Azure wprowadza [model kondycji](service-fabric-health-introduction.md) z jednostek kondycji, na którym składników systemu i watchdogs można raportu lokalnego warunki, które są monitorowania. Witaj [magazynu kondycji](service-fabric-health-introduction.md#health-store) agreguje wszystkich toodetermine danych kondycji, czy jednostki są w dobrej kondycji.

Witaj klastra jest automatycznie wypełniana wysyłane przez składniki systemu hello raportów o kondycji. Dowiedz się więcej o [tootroubleshoot raportów kondycji systemu używany](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).

Sieć szkieletowa usług zawiera wiele sposobów tooget hello zagregowane kondycji jednostek hello:

* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) lub innych narzędzi wizualizacji
* Zapytań o kondycję (za pośrednictwem programu PowerShell, interfejsu API lub REST)
* Ogólne zapytania to zwracany listę obiektów, które mają kondycji jako jedna z właściwości hello (za pośrednictwem programu PowerShell, interfejsu API lub REST)

toodemonstrate korzystać z tych opcji, umożliwia używanie lokalnego klastra z pięciu węzłów i hello [sieci szkieletowej: / WordCount aplikacji](http://aka.ms/servicefabric-wordcountapp). Hello **fabric: / WordCount** aplikacji zawiera dwie domyślne usługi, usługi stanowej typu `WordCountServiceType`i usługi bezstanowej typu `WordCountWebServiceType`. Po zmianie hello `ApplicationManifest.xml` toorequire siedmiu docelowej repliki usługi stanowej hello i jedną partycję. Ponieważ istnieje tylko pięć węzłów w klastrze hello, hello składników systemu raport ostrzeżenie na hello partycji usługi, ponieważ jest on poniżej hello docelowa liczba.

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a>Kondycji w narzędziu Service Fabric Explorer
Service Fabric Explorer zawiera czytelny hello klastra. Obraz powitania poniżej można stwierdzić, że:

* Aplikacja Hello **sieci szkieletowej: / WordCount** jest czerwony (w wyniku błędu), ponieważ ma ona zdarzenie błędu zgłoszony przez **MyWatchdog** dla właściwości hello **dostępności**.
* Jedna z jego usług **fabric: / WordCount/usługi WordCountService** jest żółty (w ostrzeżenie). Usługa Hello jest skonfigurowana z replikami siedem i hello klastra ma pięć węzłów, więc nie może zostać umieszczona repicas dwa. Wprawdzie nie pokazano poniżej, partycji usługi hello jest żółty, ze względu na raport dotyczący systemu z `System.FM` informacją, że `Partition is below target replica or instance count`. Wyzwalacze żółty partycji Hello hello żółty usługi.
* z powodu aplikacji hello red klastra Hello jest czerwony.

Ocena Hello korzysta z domyślnych zasad z manifestu klastra hello i manifest aplikacji. Są ścisłe zasady i nieodpowiednie jakiekolwiek niepowodzenie.

Widok Eksploratora usługi sieć szkieletowa hello klastra:

![Widok klastra hello z Eksploratora usługi sieć szkieletowa.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> Przeczytaj więcej na temat [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

## <a name="health-queries"></a>Zapytań o kondycję
Usługa sieci szkieletowej udostępnia zapytań o kondycję dla każdej z obsługiwanych hello [typów jednostek](service-fabric-health-introduction.md#health-entities-and-hierarchy). Są one dostępne za pośrednictwem hello interfejsu API, przy użyciu metody na [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), poleceń cmdlet programu PowerShell i REST. Te zapytania zwraca pełną kondycję informacje dotyczące jednostki hello: hello zagregowane stan kondycji, zdarzenia kondycji jednostki stanów kondycji podrzędnych (jeśli jest to wymagane), zła ocen (jeśli jednostki hello nie jest w dobrej kondycji) i statystyki kondycji elementy podrzędne (gdy ma zastosowanie).

> [!NOTE]
> Jednostki kondycji jest zwracany, gdy pełni znajduje się w magazynie kondycji hello. Hello jednostki musi być aktywne (nie usunięto) i ma raportu system. Jej podmioty nadrzędnego w łańcuchu hierarchii hello musi mieć również raporty systemu. Jeśli te warunki nie są spełnione, kondycji hello kwerendy powrotu [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) z [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` który pokazuje, dlaczego nie są zwracane jednostki hello.
>
>

zapytań o kondycję Hello musi upłynąć w hello identyfikator jednostki, który jest zależny od typu jednostki hello. zapytania Hello zaakceptować kondycji opcjonalne parametry zasad. Jeśli nie określono żadnych zasad dotyczących kondycji, hello [zasady dotyczące kondycji](service-fabric-health-introduction.md#health-policies) z manifestu klastra lub aplikacji hello są używane do oceny. Jeśli hello manifestów nie zawiera definicji dla zasad dotyczących kondycji, zasady dotyczące kondycji domyślne hello są używane do oceny. zasady dotyczące kondycji domyślne Hello nieodpowiednie zakończą się niepowodzeniem. zapytania Hello również Zaakceptuj filtry dla zwracania tylko częściowe elementów podrzędnych lub zdarzenia — Witaj te, które przestrzegać hello określonych filtrów. Inny filtr zezwala, z wyłączeniem hello statystyki elementów podrzędnych.

> [!NOTE]
> filtrów danych wyjściowych Hello są stosowane na powitania po stronie serwera, więc zmniejsza rozmiar odpowiedzi wiadomości powitania. Zaleca się, że używasz filtrów danych wyjściowych hello toolimit hello danych zwrócił, zamiast zastosować filtry na powitania po stronie klienta.
>
>

Prawidłowość jednostki zawiera:

* stan kondycji Hello zagregowane hello jednostki. Obliczone przez hello magazynu kondycji na podstawie raportów o kondycji jednostki, stanów kondycji podrzędnych (jeśli jest to wymagane) i zasad dotyczących kondycji. Przeczytaj więcej na temat [oceny kondycji jednostki](service-fabric-health-introduction.md#health-evaluation).  
* zdarzenia kondycji Hello na powitania jednostki.
* Kolekcja Hello stanów kondycji wszystkich elementów podrzędnych dla hello jednostek, które mogą mieć elementów podrzędnych. stany kondycji Hello zawierają identyfikatory jednostek i hello zagregowane kondycji. pełną kondycję tooget dziecka, wywołanie dla typów jednostek podrzędnych hello hello zapytania kondycji i podaj identyfikator podrzędnych hello.
* Hello ocen zła raport toohello tego punktu, który wyzwalane hello stanu jednostki hello, jeżeli hello jednostki jest nieprawidłowa. Obliczanie Hello są cykliczne zawierające hello dzieci kondycji oceny, które wywołały bieżącego stanu kondycji. Na przykład programu alarmowego zgłosił błąd przed repliki. Kondycja aplikacji Hello pokazuje ocenę zła powodu usługi w złej kondycji tooan; Usługa Hello jest zła powodu tooa partycji w błąd; partycja Hello jest zła powodu repliki tooa błąd; Replika Hello jest nieprawidłowy, ponieważ raport o kondycji błąd programu alarmowego toohello.
* Witaj statystyki kondycji dla wszystkich typów elementów podrzędnych hello jednostek, które mają elementy podrzędne. Na przykład stan klastra jest wyświetlana liczba całkowita hello aplikacji, usług, partycji i replik i wdrażane jednostek w klastrze hello. Kondycja usługi pokazuje hello łączna liczba partycji i replik w obszarze hello określonej usługi.

## <a name="get-cluster-health"></a>Pobierz stan klastra
Zwraca hello kondycji jednostki klastra hello i zawiera hello stanów kondycji aplikacji i węzły (dzieci hello klastra). Dane wejściowe:

* [Opcjonalnie] hello zasad dotyczących kondycji klastra używane tooevaluate hello węzły i hello zdarzenia klastra.
* Mapowanie zasady kondycji aplikacji hello [opcjonalnie], z zasad dotyczących kondycji hello używane zasady manifestu aplikacji hello toooverride.
* [Opcjonalnie] Filtry dla zdarzeń, węzły i aplikacje, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy). Wszystkie zdarzenia, węzły i aplikacji są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.
* [Opcjonalnie] Filtr tooexclude statystyki kondycji.
* [Opcjonalnie] Filtrować tooinclude fabric: / statystyki kondycji systemu w hello statystyki kondycji. Dotyczy tylko gdy hello statystyki kondycji nie są wyłączone. Domyślnie statystyki kondycji hello zawierają tylko statystyki dla użytkownika aplikacji i nie hello aplikacji systemowej.

### <a name="api"></a>Interfejs API
tooget klastra kondycji, należy utworzyć `FabricClient` i wywołanie hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) metody na jego **HealthManager**.

Witaj następujące wywołanie pobiera stan klastra hello:

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

Witaj poniższy kod pobiera stan klastra hello za pomocą zasad niestandardowych klastra kondycji i filtrów dla węzłów i aplikacji. Określa, że statystyki kondycji hello obejmuje hello sieci szkieletowej: / statystyk systemu. Tworzy [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), który zawiera informacje wejściowe hello.

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Stan klastra hello tooget polecenia cmdlet Hello jest [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth). Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.

Witaj stan klastra hello jest pięć węzłów, aplikacji systemowej hello i sieci szkieletowej: / WordCount skonfigurowane zgodnie z opisem.

Hello następujące polecenie cmdlet pobiera stan klastra za pomocą domyślnych zasad kondycji. Witaj zagregowane kondycji jest w stanie ostrzegawczym, ponieważ hello fabric: / aplikacja WordCount jest ostrzeżenie. Należy zwrócić uwagę, jak hello zła oceny zawierają szczegółowe informacje dotyczące hello warunki, które wyzwalane kondycji hello agregowane.

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

Witaj następujące polecenia cmdlet programu PowerShell pobiera kondycji hello hello klastra za pomocą zasad niestandardowych aplikacji. Filtruje wyniki tooget tylko aplikacji i węzły w błąd lub ostrzeżenie. W związku z tym żadnych węzłów są zwracane, ponieważ są one wszystkich dobrej kondycji. Tylko hello fabric: / WordCount aplikacji szanuje filtru aplikacji hello. Ponieważ zasady niestandardowe hello określa tooconsider ostrzeżenia jako błędy sieci szkieletowej hello: / WordCount aplikacji, aplikacji hello jest oceniany, tak jak błąd, i dlatego jest hello klastra.

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a>REST
Możesz uzyskać kondycji klastra z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.

## <a name="get-node-health"></a>Pobierz węzeł kondycji
Zwraca hello kondycji jednostek node i zawiera zdarzenia kondycji hello zgłoszone w węźle hello. Dane wejściowe:

* Nazwa węzła hello [wymagane], która identyfikuje hello węzła.
* Ustawienia zasad kondycji klastra [opcjonalnie] hello używane tooevaluate kondycji.
* [Opcjonalnie] Filtry dla zdarzeń, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy). Wszystkie zdarzenia są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.

### <a name="api"></a>Interfejs API
Tworzenie tooget węzła kondycji za pomocą interfejsu API, hello `FabricClient` i hello wywołania [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) metody na jego HealthManager.

Witaj poniższy kod pobiera kondycji węzła hello nazwę określonego węzła hello:

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

Witaj poniższy kod umożliwia pobranie kondycji węzła hello hello określić nazwy węzła i przekazuje filtr zdarzeń i niestandardowych zasad za pośrednictwem [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Witaj polecenia cmdlet tooget hello węzła kondycja jest [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth). Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.
Hello następujące polecenie cmdlet pobiera hello węzła kondycji za pomocą domyślnych zasad kondycji:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Witaj następujące polecenie cmdlet pobiera hello kondycję wszystkich węzłów w klastrze hello:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a>REST
Możesz uzyskać kondycji węzła z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.

## <a name="get-application-health"></a>Pobierz kondycji aplikacji
Zwraca hello kondycję obiektu aplikacji. Zawiera ona hello stanów kondycji aplikacji hello wdrożony i usługa dzieci. Dane wejściowe:

* [Wymagane] hello Nazwa aplikacji (URI) określający aplikacji hello.
* Zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.
* [Opcjonalnie] Filtry dla zdarzeń, usług i wdrożone aplikacje, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy). Zdarzeń, usług i wdrożone aplikacje są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.
* [Opcjonalnie] Filtrowanie statystyki kondycji hello tooexclude. Jeśli nie zostanie określony, statystyki kondycji hello obejmują hello ok, ostrzeżenie i liczby błędów dla wszystkich aplikacji elementów podrzędnych: usług, partycji, repliki, wdrożonych aplikacji i wdrożonych pakietów usługi.

### <a name="api"></a>Interfejs API
tooget kondycji aplikacji, Utwórz `FabricClient` i wywołanie hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) metody na jego HealthManager.

Witaj poniższy kod pobiera kondycji aplikacji hello nazwy określonej aplikacji hello (URI):

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

Witaj poniższy kod pobiera kondycji aplikacji hello nazwy określonej aplikacji hello (URI), z filtrami i niestandardowych zasad określona za pomocą [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Kondycja aplikacji hello tooget polecenia cmdlet Hello jest [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps). Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.

Witaj następujące polecenie cmdlet zwraca hello kondycję hello **fabric: / WordCount** aplikacji:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

Witaj, po przekazuje polecenia cmdlet programu PowerShell w ramach zasad niestandardowych. Filtruje także elementów podrzędnych i zdarzeń.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a>REST
Możesz uzyskać kondycji aplikacji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.

## <a name="get-service-health"></a>Pobierz usługi kondycji
Zwraca hello kondycji jednostki usługi. Zawiera ona stanów kondycji hello partycji. Dane wejściowe:

* [Wymagane] hello nazwa usługi (URI) określający hello usługi.
* Zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.
* [Opcjonalnie] Filtry dla zdarzeń i partycje, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy). Wszystkie zdarzenia i partycji są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.
* [Opcjonalnie] Filtr tooexclude statystyki kondycji. Jeśli nie zostanie określony, ok hello hello Pokaż statystyki kondycji, ostrzeżenia i błędu liczba dla wszystkich partycji i replik hello usługi.

### <a name="api"></a>Interfejs API
Kondycja usługi tooget za pośrednictwem hello interfejsu API, Utwórz `FabricClient` i wywołanie hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) metody na jego HealthManager.

Witaj poniższy przykład pobiera hello kondycji usługi o nazwie określonej usługi (URI):

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

Witaj poniższy kod pobiera hello usługi kondycji dla nazwy usługi określony hello (URI), filtrów i zasad niestandardowych za pomocą [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Kondycja usługi hello tooget polecenia cmdlet Hello jest [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth). Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.

Hello następujące polecenie cmdlet pobiera hello usługi kondycji za pomocą domyślnych zasad kondycji:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a>REST
Można pobrać usługi kondycji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.

## <a name="get-partition-health"></a>Pobierz kondycji partycji
Zwraca hello kondycji jednostki partycji. Zawiera ona stanów kondycji hello repliki. Dane wejściowe:

* [Wymagane] hello partycji identyfikator (GUID), który identyfikuje hello partycji.
* Zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.
* [Opcjonalnie] Filtry dla zdarzeń i replik, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy). Wszystkie zdarzenia i repliki są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.
* [Opcjonalnie] Filtr tooexclude statystyki kondycji. Jeśli nie zostanie określony, statystyki kondycji hello pokazują, jak wiele repliki są w ok, ostrzeżenia i błędu stanów.

### <a name="api"></a>Interfejs API
Utwórz tooget partycji kondycji za pomocą interfejsu API, hello `FabricClient` i wywołanie hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) metody na jego HealthManager. Utwórz następujące parametry opcjonalne toospecify, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a>PowerShell
Witaj polecenia cmdlet tooget hello partycji kondycja jest [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth). Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.

Hello następujące polecenie cmdlet pobiera hello kondycji dla wszystkich partycji hello **fabric: / WordCount/usługi WordCountService** usługi i odfiltrowuje repliki stanów kondycji:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Możesz uzyskać kondycji partycji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.

## <a name="get-replica-health"></a>Pobierz kondycji repliki
Zwraca kondycji hello repliki usługi stanowej lub wystąpienia usługi bezstanowej. Dane wejściowe:

* [Wymagane] hello identyfikator partycji: Identyfikatora (GUID) i repliki identyfikujący hello repliki.
* Parametry zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.
* [Opcjonalnie] Filtry dla zdarzeń, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy). Wszystkie zdarzenia są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.

### <a name="api"></a>Interfejs API
Utwórz tooget hello repliki kondycji za pomocą interfejsu API, hello `FabricClient` i wywołanie hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) metody na jego HealthManager. Zaawansowane parametry, użyj toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a>PowerShell
Witaj polecenia cmdlet tooget hello repliki kondycja jest [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth). Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.

Witaj następujące polecenie cmdlet pobiera hello kondycję hello repliki podstawowej dla wszystkich partycji usługi hello:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Możesz uzyskać kondycji repliki z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.

## <a name="get-deployed-application-health"></a>Pobierz kondycji wdrożonej aplikacji
Zwraca hello kondycji aplikacji wdrożone w ramach jednostki węzła. Zawiera ona stanów kondycji pakietu usługi hello wdrożone. Dane wejściowe:

* Nazwa aplikacji hello [wymagane] (URI) i nazwa węzła (ciąg) identyfikujących hello wdrożonych aplikacji.
* Zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.
* [Opcjonalnie] Filtry dla zdarzeń i wdrożone pakiety usługi określające zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy). Wszystkie zdarzenia i wdrożone pakiety usługi są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.
* [Opcjonalnie] Filtr tooexclude statystyki kondycji. Jeśli nie zostanie określony, statystyki kondycji hello zawierają hello liczbę pakietów wdrożonej usługi w ok, ostrzeżenia i błędu stanów kondycji.

### <a name="api"></a>Interfejs API
Utwórz tooget hello kondycji aplikacji wdrożonych na węźle, za pośrednictwem interfejsu API, hello `FabricClient` i wywołanie hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) metody na jego HealthManager. Parametry opcjonalne toospecify, użyj [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a>PowerShell
Witaj kondycji aplikacji hello wdrożone tooget polecenia cmdlet jest [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps). Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet. Uruchom toofind się, gdy aplikacja jest wdrażana, [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) i przyjrzeć hello wdrożonych aplikacji elementów podrzędnych.

Hello następujące polecenie cmdlet pobiera hello kondycję hello **fabric: / WordCount** aplikacji wdrożonych na **to węzeł _Node_2**.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Możesz uzyskać kondycji wdrożonej aplikacji z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.

## <a name="get-deployed-service-package-health"></a>Pobierz kondycji pakietu wdrożonej usługi
Zwraca hello kondycji jednostki pakietu wdrożonej usługi. Dane wejściowe:

* Nazwa aplikacji hello [wymagane] (URI), nazwę węzła (ciąg) i nazwa manifestu usługi (ciąg) identyfikujących hello wdrożony pakiet usługi.
* Zasady kondycji aplikacji hello [opcjonalnie] używane zasady manifestu aplikacji hello toooverride.
* [Opcjonalnie] Filtry dla zdarzeń, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello (na przykład tylko błędy lub ostrzeżenia i błędy). Wszystkie zdarzenia są używane tooevaluate hello jednostki zagregowane kondycji, niezależnie od filtru hello.

### <a name="api"></a>Interfejs API
Utwórz tooget hello kondycji pakietu wdrożonej usługi za pośrednictwem hello interfejsu API, `FabricClient` i wywołanie hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) metody na jego HealthManager. Parametry opcjonalne toospecify, użyj [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a>PowerShell
Witaj polecenia cmdlet tooget hello wdrożone usługi pakietu kondycja jest [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth). Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet. Uruchom toosee, w którym aplikacja jest wdrażana, [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) i przyjrzyj się hello wdrożone aplikacje. toosee, które pakiety usługi są w aplikacji, poszukać w hello wdrożone usługi pakietu dzieci w hello [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) danych wyjściowych.

Witaj następujące polecenie cmdlet pobiera hello kondycję hello **WordCountServicePkg** pakiet usługi hello **sieci szkieletowej: / WordCount** aplikacji wdrożonych na **to węzeł _Node_2**. Jednostka Hello ma **System.Hosting** raporty dla pomyślnej aktywacji w pakiecie usługi i punktu wejścia i pomyślną rejestrację typu usługi.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Możesz uzyskać wdrożonej usługi kondycji pakietu z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) zawierającej zasady dotyczące kondycji opisanego w treści hello.

## <a name="health-chunk-queries"></a>Fragmentu zapytań o kondycję
Witaj kondycji fragmentu zapytania mogą zwracać elementy podrzędne (rekursywnie), wielopoziomowe klastra na filtry. Obsługuje ona filtrów zaawansowanych, zezwalających na dużą elastyczność w wyborze dzieci hello toobe zwracane. filtry Hello określić elementy podrzędne Unikatowy identyfikator hello lub przez inne grupy identyfikatorów i/lub stanów kondycji. Domyślnie bez żadnych elementów podrzędnych zostaną uzupełnione, w przeciwieństwie toohealth poleceń, które zawsze zawierają elementy podrzędne pierwszego stopnia.

Witaj [zapytań o kondycję](service-fabric-view-entities-aggregated-health.md#health-queries) zwracane elementy podrzędne tylko pierwszy poziom hello określone jednostki na wymagane filtrów. tooget hello podrzędnych elementów podrzędnych hello, należy wywołać kondycji dodatkowe interfejsy API dla każdej jednostki zainteresowań. Podobnie kondycję hello tooget konkretnych obiektów, należy wywołać kondycji jednego interfejsu API dla każdego żądanego obiektu. Witaj fragmentu zapytania zaawansowane filtrowanie pozwala toorequest wielu elementy w jednym zapytaniu, minimalizując rozmiaru wiadomości powitania i hello liczbę komunikatów.

wartość Hello hello fragmentu zapytania jest, że możesz też uzyskać stan kondycji kolejnych jednostek klastra (potencjalnie wszystkich klastra jednostek zaczynając od wymaganego głównego) w jednym wywołaniu. Można wyrazić zapytania kondycji złożonych takich jak:

* Zwracany aplikacji tylko w błąd, a w przypadku aplikacji obejmują wszystkie usługi w ostrzeżenia lub błędu. W przypadku zwróconych usług zawiera wszystkie partycje.
* Zwróć tylko hello kondycji cztery aplikacje, określonych przez ich nazwy.
* Zwróć tylko hello kondycję aplikacji typu żądanej aplikacji.
* Zwraca wszystkie wdrożone jednostek w węźle. Zwraca wszystkie aplikacje, wszystkich aplikacji wdrożonych na powitania określony węzeł i wszystkie pakiety service hello wdrożone w tym węźle.
* Zwróć wszystkie repliki na błąd. Zwraca wszystkich aplikacji, usług, partycji i replik tylko z błędami.
* Zwróć wszystkie aplikacje. Dla określonej usługi należy wprowadzić wszystkie partycje.

Obecnie hello kondycji fragmentu zapytania jest widoczne tylko dla obiektu klastra hello. Zwraca fragmentu kondycji klastra, który zawiera:

* klaster Hello agregowana stan kondycji.
* Hello kondycji stanu fragmentu listy węzłów, które przestrzegać filtry.
* Hello kondycji stanu fragmentu lista aplikacji, których przestrzeganie filtry. Każdego fragmentu stan kondycji aplikacji znajduje się lista fragmentu ze wszystkich usług, których przestrzeganie filtry i listy fragmentu z wszystkich wdrożonych aplikacji, które przestrzegać hello filtrów. Wartość taka sama dla dzieci hello usług i wdrożone aplikacje. Dzięki temu wszystkie jednostki w klastrze hello może być potencjalnie zwracany żądanie w hierarchiczny sposób.

### <a name="cluster-health-chunk-query"></a>Klaster kondycji fragmentu zapytania
Zwraca hello kondycji jednostki klastra hello i zawiera fragmenty stan kondycji hierarchiczna hello wymagane elementy podrzędne. Dane wejściowe:

* [Opcjonalnie] hello zasad dotyczących kondycji klastra używane tooevaluate hello węzły i hello zdarzenia klastra.
* Mapowanie zasady kondycji aplikacji hello [opcjonalnie], z zasad dotyczących kondycji hello używane zasady manifestu aplikacji hello toooverride.
* [Opcjonalnie] Filtry dla węzłów i aplikacje, które określają zapisy, które są interesujące i powinny być zwrócone w wyniku hello. filtry Hello są tooan określonej jednostki/grupy jednostek lub tooall odpowiednich jednostek na tym poziomie. Witaj lista filtrów może zawierać jeden filtr ogólne i/lub filtrów dla określonych identyfikatorów toofine ziarna jednostek zwróconych przez zapytanie hello. W przypadku braku hello elementy podrzędne nie są zwracane domyślnie.
  Przeczytaj więcej na temat filtrów hello w [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) i [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter). rekursywnie może filtrów aplikacji Hello określ filtry zaawansowane podrzędnych.

Wynik fragmentu Hello zawiera elementy podrzędne hello przestrzegać hello filtrów.

Obecnie hello fragmentu zapytania nie zwraca zła ocen lub zdarzeń jednostki. Dodatkowe informacje można uzyskać za pomocą hello istniejące zapytanie kondycji klastra.

### <a name="api"></a>Interfejs API
Stan klastra tooget bryłkach, Utwórz `FabricClient` i wywołanie hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) metody na jego **HealthManager**. Można przekazać [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe zasady dotyczące kondycji i filtry zaawansowane.

Witaj poniższy kod pobiera fragmentu kondycji klastra z filtry zaawansowane.

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Stan klastra hello tooget polecenia cmdlet Hello jest [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk). Najpierw połącz toohello klastra przy użyciu hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet.

Witaj poniższy kod pobiera węzły tylko wtedy, gdy są one błąd z wyjątkiem określonego węzła zawsze ma zostać zwrócony.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

Witaj następujące polecenie cmdlet pobiera fragmentu klastra z filtrami aplikacji.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

Witaj następujące polecenie cmdlet zwraca wszystkie wdrożone jednostki w węźle.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a>REST
Możesz uzyskać fragment kondycji klastra z [żądania GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) lub [żądania POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) zawierającej zasady dotyczące kondycji i opisane w treści hello filtry zaawansowane.

## <a name="general-queries"></a>Ogólne zapytań
Ogólne kwerendy zwracają listę jednostki sieci szkieletowej usług określonego typu. Są one dostępne za pośrednictwem hello interfejsu API (za pomocą metod hello na **FabricClient.QueryManager**), polecenia cmdlet programu PowerShell i REST. Te zapytania agregować podzapytania z wielu składników. Jeden z nich jest hello [magazynu kondycji](service-fabric-health-introduction.md#health-store), który wypełnia hello zagregowane stan kondycji dla każdego wyniku zapytania.  

> [!NOTE]
> Ogólne zapytania zwracać hello zagregowane stanu kondycji jednostki hello i nie zawierają danych sformatowanego kondycji. Jeśli jednostka nie jest w dobrej kondycji, można odpowiednio zareagować z tooget zapytania kondycji wszystkich jego kondycji informacji, w tym zdarzenia, stanów kondycji podrzędnych i oceny złej kondycji.
>
>

Jeśli ogólne kwerend zwraca nieznany kondycja jednostki, istnieje możliwość tego magazynu kondycji hello nie ma pełnych danych o hello jednostki. Istnieje również możliwość, że sklep kondycji toohello podzapytania nie powiodło się (na przykład wystąpił błąd komunikacji lub magazynu kondycji hello został ograniczony). Wykonaj przy użyciu zapytania kondycji hello jednostki. Jeśli podzapytanie hello napotkała przejściowe błędy, takie jak problemy z siecią, to zapytanie kolejnych może się powieść. Go może także zapewniają więcej szczegółowych informacji z magazynu kondycji hello o Dlaczego hello jednostki nie jest widoczne.

Witaj zapytania, które zawierają **HealthState** dla jednostki to:

* Listy węzłów: zwraca hello listy węzłów w klastrze hello (stronicowanej).
  * Interfejs API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)
  * Środowiska PowerShell: Get-ServiceFabricNode
* Lista aplikacji: hello zwraca listę aplikacji w klastrze hello (stronicowanej).
  * Interfejs API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)
  * Środowiska PowerShell: Get-ServiceFabricApplication
* Lista usług: hello zwraca listę usług w aplikacji (stronicowanej).
  * Interfejs API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)
  * Środowiska PowerShell: Get-ServiceFabricService
* Lista partycji: zwraca listę hello partycji w usłudze (stronicowanej).
  * Interfejs API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)
  * Środowiska PowerShell: Get-ServiceFabricPartition
* Listy replik: zwraca hello listę replik w partycji (stronicowanej).
  * Interfejs API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)
  * Środowiska PowerShell: Get-ServiceFabricReplica
* Wdrożone listy aplikacji: hello zwraca listę wdrożonych aplikacji w węźle.
  * Interfejs API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)
  * Środowiska PowerShell: Get-ServiceFabricDeployedApplication
* Wdrożone usługi listy pakietów: hello zwraca listę pakietów usług we wdrożonej aplikacji.
  * Interfejs API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)
  * Środowiska PowerShell: Get-ServiceFabricDeployedApplication

> [!NOTE]
> Niektóre z zapytań hello zwracać wyników stronicowania. Witaj zwrotu z tych kwerend znajduje się lista pochodzące z [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1). Jeśli wyniki hello nie pasują do wiadomości, jest zwracana tylko stronę i ContinuationToken śledzi gdzie wyliczenie zatrzymana. Nadal hello toocall sam zapytań i przekaż token kontynuacji hello z hello poprzednich zapytań tooget dalej wyników.
>
>

### <a name="examples"></a>Przykłady
Witaj poniższy kod pobiera złej kondycji aplikacji hello w klastrze hello:

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

Witaj następujące polecenie cmdlet pobiera szczegóły aplikacji hello hello sieci szkieletowej: / WordCount aplikacji. Należy zauważyć, że stan kondycji jest ostrzeżenie.

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

Witaj następujące polecenie cmdlet pobiera hello usług o stanie kondycji błędu:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a>Uaktualnienia klastra i aplikacji
Podczas uaktualniania monitorowanych hello klastra i aplikacji sieci szkieletowej usług sprawdza tooensure kondycji wszystkich pozostaje dobrej kondycji. Jeśli jednostka jest nieprawidłowy, ponieważ oceniane przy użyciu zasad dotyczących kondycji skonfigurowanego, uaktualnienie hello ma zastosowanie zasad dla konkretnych uaktualnienia toodetermine hello następnej akcji. uaktualnienie Hello może być wstrzymana tooallow interakcji z użytkownikiem (na przykład poprawki błędów lub zmiany zasad) lub go może automatycznie przywrócić poprzedniej wersji dobrej toohello.

Podczas *klastra* uaktualnienia, możesz uzyskać stan uaktualnienia klastra hello. Stan uaktualnienia Hello obejmuje oceny złej kondycji, które toowhat punkt jest zła hello klastra. Jeśli uaktualnienie hello jest przywracana powodu toohealth problemy, stan uaktualnienia hello pamięta hello ostatniego przyczyny złej kondycji. Te informacje mogą pomóc Administratorzy zbadać, co poszło źle po uaktualnieniu hello wycofana lub zatrzymana.

Podobnie podczas *aplikacji* uaktualnienia, wszelkie nieprawidłowości oceny są zawarte w stan uaktualnienia aplikacji hello.

Hello poniżej przedstawia stan uaktualnienia aplikacji hello zmodyfikowane sieci szkieletowej: / WordCount aplikacji. Programu alarmowego zgłosił błąd na jednym z jego repliki. uaktualnienie Hello wykonuje procedurę wycofywania, ponieważ hello kontroli kondycji nie są przestrzegane.

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

Dowiedz się więcej o hello [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md).

## <a name="use-health-evaluations-tootroubleshoot"></a>Użyj tootroubleshoot oceny kondycji
Zawsze, gdy występuje problem z klastra hello lub aplikacji, obejrzyj toopinpoint kondycji klastra lub aplikacji hello co to jest nieprawidłowy. Zła ocen Hello zawierają szczegółowe informacje o jakie wyzwalanych hello bieżący stan złej kondycji. Jeśli zajdzie potrzeba, użytkownik może przejść do podrzędne o złej kondycji jednostek tooidentify hello główną przyczynę.

Rozważmy na przykład aplikacji nieprawidłowy, ponieważ raport o błędach na jednym z jego repliki. Hello następujące polecenia cmdlet programu Powershell pokazuje hello ocen złej kondycji:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

Można przyjrzeć się tooget repliki hello więcej informacji:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> Hello zła ocen Pokaż hello pierwszy przyczyny jednostka hello jest oceniane toocurrent stan kondycji. Może istnieć wiele zdarzeń wyzwalających ten stan, ale są one nie zostać zawarte w hello oceny. tooget więcej informacji, przechodzenie do toofigure jednostek kondycji hello limit wszystkich raportów zła hello hello klastra.
>
>

## <a name="next-steps"></a>Następne kroki
[Użyj tootroubleshoot Raporty kondycji systemu](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Dodawanie niestandardowych raportów kondycji sieci szkieletowej usług](service-fabric-report-health.md)

[Jak tooreport i zaznacz pole wyboru usługi kondycji](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Monitorowanie i diagnozowania usług lokalnie](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Uaktualnianie aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md)
