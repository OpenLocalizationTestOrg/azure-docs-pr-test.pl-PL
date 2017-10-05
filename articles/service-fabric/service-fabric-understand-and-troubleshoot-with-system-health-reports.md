---
title: "Rozwiązywanie problemów z raportów o kondycji systemu | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano raportów kondycji wysyłane przez składniki sieci szkieletowej usług Azure i ich użycia dla klastra rozwiązywaniu problemów lub problemów aplikacji."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: 54e20146b2f1e0ca6153b66319be70c6f7c2fb59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-system-health-reports-to-troubleshoot"></a>Używanie raportów kondycji systemu do rozwiązywania problemów
Azure Service Fabric składniki raport poza pole na wszystkich jednostek w klastrze. [Magazynu kondycji](service-fabric-health-introduction.md#health-store) tworzy i usuwa jednostki na podstawie raportów systemu. Również organizuje ona je w hierarchii, która przechwytuje interakcje jednostki.

> [!NOTE]
> Aby zapoznać się z kondycją pojęcia, Dowiedz się więcej na [model kondycji sieci szkieletowej usług](service-fabric-health-introduction.md).
> 
> 

Raporty kondycji systemu zapewniają wgląd w klastrze i funkcjonalność aplikacji i flagi błędów za pomocą kondycji. Dla aplikacji i usług systemowych raportów kondycji Sprawdź, czy jednostki są zaimplementowane i są działa prawidłowo z punktu widzenia sieci szkieletowej usług. Raporty nie zawierają żadnych monitorowanie kondycji logiki biznesowej usługi lub wykrywania zawieszone procesy. Usługi użytkownik może uzupełnić dane kondycji z użyciem informacji specyficznych ich logiki.

> [!NOTE]
> Watchdogs raportów o kondycji są widoczne tylko *po* składników systemu Tworzenie jednostki. Po usunięciu jednostki magazynu kondycji automatycznie usuwa wszystkie raporty kondycji skojarzonych z nim. To samo dotyczy po utworzeniu nowego wystąpienia obiektu (na przykład nowe wystąpienie usługi stanowej utrwalonego repliki jest tworzona). Wszystkie raporty skojarzone z wystąpieniem stare usunąć i wyczyścić ze sklepu.
> 
> 

Składnik systemu raporty są identyfikowane przez źródło, w którym rozpoczyna się od "**systemu.**" prefiks. Watchdogs nie można użyć tego samego prefiksu dla ich źródła, jak raporty z nieprawidłowe parametry są odrzucane.
Oto niektóre raporty systemu, aby zrozumieć wywołujących je i jak skorygować możliwe problemy, które reprezentują.

> [!NOTE]
> Sieć szkieletowa usług w dalszym ciągu Dodaj raporty warunków odsetek zwiększających wgląd w działania wykonywane w klastrze i aplikacji. Istniejące raporty mogą być również dołączane więcej szczegółów, aby ułatwić rozwiązanie problemu szybciej.
> 
> 

## <a name="cluster-system-health-reports"></a>Klaster systemowych raportów kondycji
Jednostki kondycji klastra jest tworzony automatycznie w magazynie kondycji. Jeśli wszystko działa prawidłowo, nie ma raportu system.

### <a name="neighborhood-loss"></a>Utrata otoczenie
**System.Federation** zgłasza błąd, jeśli wykryje utraty otoczenia. Raport jest w poszczególnych węzłach, a identyfikator węzła jest uwzględniony w nazwie właściwości. Jeden otoczenie jest zgubiony w kręgu całej sieci szkieletowej usług, zwykle można spodziewać się dwa zdarzenia (obie strony raportu gap). W przypadku utraty więcej klubów ma więcej zdarzeń.

Raport określa limit czasu globalnego dzierżawy jako czas wygaśnięcia. Raport jest ponowne wysłanie co pół czas TTL, jak długo warunek pozostaje aktywna. Zdarzenie zostanie automatycznie usunięta po jego wygaśnięciu. Usuń, gdy wygasłe zachowanie gwarantuje, że raportu są czyszczone z magazynu kondycji poprawnie, nawet, jeśli węzeł raportowania jest wyłączony.

* **SourceId**: System.Federation
* **Właściwość**: rozpoczyna się od **otoczenie** i zawiera informacje na węzeł
* **Następne kroki**: Sprawdź, dlaczego otoczenie zostaną utracone (na przykład sprawdzić komunikację między węzłami klastra).

## <a name="node-system-health-reports"></a>Węzeł systemowych raportów kondycji
**System.FM**, który reprezentuje usługę Menedżer trybu Failover jest urzędu, który zarządza informacjami o węzłach klastra. Każdy węzeł powinien mieć jeden raport z System.FM przedstawiający jego stanu. Jednostek node są usuwane po usunięciu stanu węzła (zobacz [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>Węzeł w górę lub w dół
System.FM raportów jako OK, gdy węzeł dołączy pierścień (jest uruchomiona). Zgłasza błąd, gdy węzeł odjazdem pierścienia (działa, albo do uaktualnienia lub po prostu ponieważ nie powiodła się). Hierarchia kondycji utworzony przez magazynu kondycji podejmuje działania na jednostkach wdrożonej w korelacji z System.FM węzła Raporty. Traktuje węzła nadrzędnego wirtualnego wszystkich wdrożonych jednostek. Jednostek wdrożonych w tym węźle dostępnych za pośrednictwem zapytania, jeśli węzeł został zgłoszony jako czas przez System.FM z tego samego wystąpienia jako wystąpienie skojarzone z jednostkami. Gdy System.FM zgłasza, że węzeł nie działa lub ponownego uruchomienia (nowe wystąpienie), magazynu kondycji automatycznie oczyszcza wdrożonej jednostek, które może istnieć tylko na dół węzła lub poprzednie wystąpienie węzła.

* **SourceId**: System.FM
* **Właściwość**: stan
* **Następne kroki**: Jeśli węzeł nie działa w przypadku uaktualnienia, powinna ona przywrócona po został uaktualniony. W takim przypadku stan kondycji powinna przejdź do OK. Jeśli węzeł nie wróć lub go nie powiedzie się, problem wymaga więcej dochodzenia.

W poniższym przykładzie przedstawiono System.FM zdarzenia o stanie kondycji OK dla węzła w:

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a>Wygaśnięcie certyfikatu
**System.FabricNode** zgłosi ostrzeżenie, gdy zbliża się ważności certyfikatów używanych przez węzeł. Występują trzy certyfikaty w każdym węźle: **Certificate_cluster**, **Certificate_server**, i **Certificate_default_client**. Jeśli czas wygaśnięcia jest co najmniej dwa tygodnie, stan kondycji raportu jest OK. Jeśli czas wygaśnięcia jest w ciągu dwóch tygodni, jego typ jest ostrzeżenie. TTL te zdarzenia jest nieskończone, i usuwane, gdy węzeł opuści klastra.

* **SourceId**: System.FabricNode
* **Właściwość**: rozpoczyna się od **certyfikatu** i zawiera więcej informacji na temat typ certyfikatu
* **Następne kroki**: zaktualizować certyfikaty, jeśli są one wkrótce wygasną.

### <a name="load-capacity-violation"></a>Naruszenie pojemności obciążenia
Usługa równoważenia obciążenia sieci szkieletowej zgłosi ostrzeżenie po wykryciu naruszenie pojemności węzła.

* **SourceId**: System.PLB
* **Właściwość**: rozpoczyna się od **pojemności**
* **Następne kroki**: Sprawdź podane metryki i wyświetlić w węźle pojemność bieżąca.

## <a name="application-system-health-reports"></a>Aplikacja systemowych raportów kondycji
**System.CM**, który reprezentuje usługę Menedżer klastra jest urzędu, który zarządza informacjami o aplikacji.

### <a name="state"></a>Stan
System.CM raportów, jako OK gdy aplikacji została utworzona lub zaktualizowana. Informuje magazynu kondycji po usunięciu aplikacji, dzięki czemu może zostać usunięty z magazynu.

* **SourceId**: System.CM
* **Właściwość**: stan
* **Następne kroki**: Jeśli aplikacja została utworzona lub aktualizowane, powinny zawierać raport o kondycji Menedżera klastra. W przeciwnym razie sprawdź stan aplikacji, wysyłając zapytanie (na przykład polecenia cmdlet programu PowerShell **Get ServiceFabricApplication - ApplicationName *applicationName***).

W poniższym przykładzie przedstawiono zdarzenia stanu na **fabric: / WordCount** aplikacji:

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a>Usługa systemowych raportów kondycji
**System.FM**, który reprezentuje usługę Menedżer trybu Failover jest urzędu, który zarządza informacjami o usługach.

### <a name="state"></a>Stan
System.FM raporty jako OK po utworzeniu usługi. Usuwa obiekt z magazynu kondycji po usunięciu usługi.

* **SourceId**: System.FM
* **Właściwość**: stan

W poniższym przykładzie przedstawiono zdarzenia stanu usługi **fabric: / WordCount/WordCountWebService**:

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a>Błąd korelacji usługi
**System.PLB** zgłasza błąd, jeśli wykryje, czy uaktualnianie usługi mają zostać skorelowane z inną usługą tworzy łańcuch koligacji. Raport jest wyczyszczone po pomyślnej aktualizacji.

* **SourceId**: System.PLB
* **Właściwość**: ServiceDescription
* **Następne kroki**: Sprawdź opisy skorelowane usług.

## <a name="partition-system-health-reports"></a>Partycja systemowych raportów kondycji
**System.FM**, reprezentuje usługą Failover Manager service jest urzędu, który zarządza informacjami o partycji usługi.

### <a name="state"></a>Stan
System.FM raportów, jako OK, gdy partycja został utworzony i działa prawidłowo. Usuwa obiekt z magazynu kondycji po usunięciu partycji.

W przypadku partycji mniej niż liczba minimalna repliki, zgłasza błąd. Jeśli partycja nie jest mniej niż liczba minimalna repliki, ale jest mniejsza od liczby replik docelowej, zgłosi ostrzeżenie. W przypadku partycji w wyniku utraty kworum, System.FM zgłasza błąd.

Innych ważnych wydarzeń, zawierać ostrzeżenie podczas ponownej konfiguracji trwa dłużej, niż oczekiwano, a jeśli Kompilacja trwa dłużej, niż oczekiwano. Przewidywany czas dla kompilacji i ponownej konfiguracji są konfigurowane na podstawie scenariuszy usługi. Na przykład jeśli usługa ma terabajt stanu, takie jak bazy danych SQL, Kompilacja trwa dłużej niż usługi z małej ilości stanu.

* **SourceId**: System.FM
* **Właściwość**: stan
* **Następne kroki**: Jeśli kondycja nie jest OK, istnieje możliwość, że niektóre repliki nie zostały utworzone, otwarte lub poziom jest podwyższany do podstawowej lub pomocniczej poprawnie. W wielu przypadkach główną przyczyną jest to błąd usługi w implementacji open lub zmiany roli.

W poniższym przykładzie przedstawiono partycji dobrej kondycji:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Poniższy przykład przedstawia kondycję partycji, która znajduje się poniżej docelowej liczby replik. Następnym krokiem jest, aby uzyskać opis partycji, który przedstawia sposób skonfigurowania: **MinReplicaSetSize** trzy i **TargetReplicaSetSize** wynosi siedem. Następnie Pobierz liczbę węzłów w klastrze: pięć. Dlatego w tym przypadku dwóch replik nie można umieścić, ponieważ docelowy liczba replik jest wyższa niż liczba dostępnych węzłów.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
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
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a>Naruszenie ograniczenia repliki
**System.PLB** zgłosi ostrzeżenie, jeśli wykryje naruszenie ograniczenia repliki i nie można umieścić wszystkich replik partycji. Szczegóły raportu Pokaż których ograniczeń i właściwości zapobiec umieszczania repliki.

* **SourceId**: System.PLB
* **Właściwość**: rozpoczyna się od **ReplicaConstraintViolation**

## <a name="replica-system-health-reports"></a>Repliki systemowych raportów kondycji
**System.RA**, reprezentuje składnika agenta rekonfiguracji, jest serwerem autorytatywnym dla stanu repliki.

### <a name="state"></a>Stan
**System.RA** raporty OK po utworzeniu repliki.

* **SourceId**: System.RA
* **Właściwość**: stan

W poniższym przykładzie przedstawiono repliki dobrej kondycji:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a>Otwórz stanu repliki
Opis tego raportu o kondycji zawiera czas rozpoczęcia (Coordinated Universal Time), gdy wywołano wywołanie interfejsu API.

**System.RA** zgłosi ostrzeżenie, jeśli replika Otwórz trwa dłużej niż skonfigurowanego okresu (domyślne: 30 minut). Jeśli interfejs API ma wpływ na dostępność usługi, raport, zgłaszany jest znacznie szybciej (można skonfigurować interwał, z domyślną 30 sekund). Czas obejmuje czas poświęcony na Otwórz replikatora i Otwórz usługę. Po zakończeniu Otwórz właściwość zmienia się na OK.

* **SourceId**: System.RA
* **Właściwość**: **ReplicaOpenStatus**
* **Następne kroki**: Jeśli stan kondycji nie jest OK, sprawdź, dlaczego Otwórz repliki trwa dłużej, niż oczekiwano.

### <a name="slow-service-api-call"></a>Wywołanie interfejsu API usługi powolne
**System.RAP** i **System.Replicator** raportować ostrzeżenie w przypadku wywołania do kodu użytkownika usługi trwa dłużej niż w skonfigurowanym czasie. To ostrzeżenie zostanie wyczyszczona po zakończeniu wywołania.

* **SourceId**: System.RAP lub System.Replicator
* **Właściwość**: Nazwa powolne interfejsu API. Opis zawiera więcej informacji na temat interfejsu API został oczekujące czas.
* **Następne kroki**: Sprawdź, dlaczego wywołanie trwa dłużej, niż oczekiwano.

Poniższy przykład przedstawia partycji w wyniku utraty kworum i kroki dochodzenia gotowe, aby dowiedzieć się, dlaczego. Jednej z replik ma ostrzegawczy stan kondycji, aby uzyskać jego kondycji. Przedstawia on, że operacja usługi trwa dłużej, niż oczekiwano zdarzenie zgłaszane przez System.RAP. Po otrzymaniu tych informacji, następnym krokiem jest przyjrzeć się kodu usługi i badanie istnieje. Dla tego przypadku **RunAsync** implementacji usługi stanowej zgłasza nieobsługiwany wyjątek. Repliki są odzyskiwanie, więc nie widać żadnych replik w stanie ostrzeżenia. Możesz ponowić próbę pobierania stanu kondycji i wyszukaj różnice w identyfikatorze repliki. W niektórych przypadkach ponowne próby pozwoli uzyskać wskazówki.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

Po uruchomieniu błędnej aplikacji w debugerze okna zdarzeń diagnostycznych Pokaż wyjątek z RunAsync:

![Visual Studio 2015 zdarzeń diagnostycznych: niepowodzenie RunAsync w sieci szkieletowej: / HelloWorldStatefulApplication.][1]

Visual Studio 2015 zdarzeń diagnostycznych: niepowodzenie RunAsync w **fabric: / HelloWorldStatefulApplication**.

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>Kolejka replikacji jest pełna
**System.Replicator** zgłosi ostrzeżenie, gdy kolejka replikacji jest pełna. Na serwerze podstawowym kolejki replikacji zazwyczaj zapełni, ponieważ co najmniej jeden replikach pomocniczych są przetwarzane wolno potwierdzić operacji. Na serwerze pomocniczym zwykle dzieje się tak, gdy usługa jest powolne zastosować operacji. To ostrzeżenie zostanie wyczyszczona po kolejki nie jest już pełna.

* **SourceId**: System.Replicator
* **Właściwość**: **PrimaryReplicationQueueStatus** lub **SecondaryReplicationQueueStatus**w zależności od roli repliki

### <a name="slow-naming-operations"></a>Powolne operacje nazewnictwa
**System.NamingService** raportów kondycji na jego repliką podstawową, gdy operacja nazewnictwa trwa dłużej niż dopuszczalne. Przykłady operacji nazewnictwa [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) lub [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync). Więcej metod można znaleźć w obszarze klienta fabricclient z rolą, na przykład w obszarze [usługi metod zarządzania](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) lub [metod zarządzania właściwości](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).

> [!NOTE]
> Usługa nazewnictwa rozpoznawania nazw usługi do lokalizacji w klastrze i umożliwia użytkownikom zarządzanie nazwy usługi i właściwości. Jest to sieć szkieletowa usług na partycje utrwalone usługi. Reprezentuje jedną z partycji Authority Owner zawierający metadane dotyczące wszystkich nazw usługi Service Fabric i usług. Nazwy sieci szkieletowej usług są mapowane do różnych partycji o nazwie właściciela partycji, dlatego usługa jest rozszerzalny. Przeczytaj więcej na temat [Naming service](service-fabric-architecture.md).
> 
> 

Podczas operacji nazewnictwa trwa dłużej, niż oczekiwano, operacja oflagowane z raportem ostrzeżenie na *repliki podstawowej partycji usługi nazewnictwa, która służy operacji*. Jeśli operacja zakończy się pomyślnie, ostrzeżenie jest wyczyszczone. Po zakończeniu operacji z powodu błędu, raport o kondycji zawiera szczegóły dotyczące błędu.

* **SourceId**: System.NamingService
* **Właściwość**: rozpoczyna się od prefiksu **Duration_** i identyfikuje wolne działanie i nazwa sieci szkieletowej usług, dla którego jest stosowana operacji. Na przykład jeśli Tworzenie usługi w sieci szkieletowej name: / MyApp/Moja_usługa trwa zbyt długo, ta właściwość jest Duration_AOCreateService.fabric:/MyApp/MyService. AO wskazuje rolą partycji nazewnictwa dla tej nazwy i operację.
* **Następne kroki**: Sprawdź, dlaczego nazewnictwa kończy się niepowodzeniem. Każda operacja mogą mieć różnych przyczyn. Na przykład usunąć usługi mogą zostać zatrzymane w węźle, ponieważ host aplikacji przechowuje awarii w węźle z powodu błędu użytkownika w kodzie usługi.

Poniższy przykład przedstawia tworzenie operacji usługi. Operacja trwało dłużej niż skonfigurowany czas trwania. AO ponawia próbę i wysyła pracy na nie. NIE ukończono z limitem czasu ostatniej operacji. W takim przypadku samej repliki jest kluczem podstawowym AO i żadnych ról.

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>DeployedApplication systemowych raportów kondycji
**System.Hosting** urzędu na wdrożonym jednostek.

### <a name="activation"></a>aktywacji
System.Hosting raportów, jako OK gdy aplikacji został pomyślnie uaktywniony na węźle. W przeciwnym razie go zgłasza błąd.

* **SourceId**: System.Hosting
* **Właściwość**: aktywacji, łącznie z wersją wdrożenia
* **Następne kroki**: Jeśli aplikacja jest zła, zbadać, dlaczego aktywacja nie powiodła się.

W poniższym przykładzie przedstawiono pomyślnej aktywacji:

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Do pobrania
**System.Hosting** zgłasza błąd, jeśli pobieranie pakietu aplikacji nie powiedzie się.

* **SourceId**: System.Hosting
* **Właściwość**:  **pobrać:*RolloutVersion***
* **Następne kroki**: Sprawdź, dlaczego pobieranie nie powiodło się w węźle.

## <a name="deployedservicepackage-system-health-reports"></a>DeployedServicePackage systemowych raportów kondycji
**System.Hosting** urzędu na wdrożonym jednostek.

### <a name="service-package-activation"></a>Aktywowanie pakietu usługi
System.Hosting raporty jako OK, jeżeli usługa aktywacji pakietu w węźle zakończy się pomyślnie. W przeciwnym razie go zgłasza błąd.

* **SourceId**: System.Hosting
* **Właściwość**: aktywacji
* **Następne kroki**: Sprawdź, dlaczego aktywacja nie powiodła się.

### <a name="code-package-activation"></a>Aktywowanie pakietu kodu
**System.Hosting** raporty jako OK dla każdego pakietu kodu, jeśli aktywacja zakończy się pomyślnie. W przypadku niepowodzenia aktywacji zgłosi ostrzeżenie zgodnie z konfiguracją. Jeśli **elementu CodePackage** nie może aktywować lub kończy się z powodu błędu większy niż skonfigurowany **CodePackageHealthErrorThreshold**, hosting zgłasza błąd. Jeśli pakiet usługi zawiera wiele pakietów kodu, aktywacji raport jest generowany dla każdego z nich.

* **SourceId**: System.Hosting
* **Właściwość**: używa prefiksu **CodePackageActivation** i zawiera nazwę pakietu kodu i punktu wejścia jako  **CodePackageActivation:*CodePackageName* :*SetupEntryPoint/EntryPoint*** (na przykład **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>Rejestracja typu usługi
**System.Hosting** zgłasza jako OK, jeśli typ usługi został pomyślnie zarejestrowany. Zgłasza błąd, jeśli rejestracja nie została wykonana w czasie (zgodnie z konfiguracją przy użyciu **ServiceTypeRegistrationTimeout**). Jeśli środowisko uruchomieniowe jest zamknięty, typ usługi jest zarejestrowany z węzła i hostingu zgłosi ostrzeżenie.

* **SourceId**: System.Hosting
* **Właściwość**: używa prefiksu **ServiceTypeRegistration** i zawiera nazwę typu usługi (na przykład **ServiceTypeRegistration:FileStoreServiceType**)

W poniższym przykładzie przedstawiono pakietu wdrożonej usługi w dobrej kondycji:

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Do pobrania
**System.Hosting** zgłasza błąd, jeśli pobieranie pakietu usługi nie powiedzie się.

* **SourceId**: System.Hosting
* **Właściwość**:  **pobrać:*RolloutVersion***
* **Następne kroki**: Sprawdź, dlaczego pobieranie nie powiodło się w węźle.

### <a name="upgrade-validation"></a>Weryfikacja uaktualnienia
**System.Hosting** zgłasza błąd w przypadku niepowodzenia weryfikacji podczas uaktualniania lub Jeśli uaktualnienie nie powiedzie się w węźle.

* **SourceId**: System.Hosting
* **Właściwość**: używa prefiksu **FabricUpgradeValidation** i zawiera uaktualniania wersji
* **Opis elementu**: wskazuje wystąpił błąd

## <a name="next-steps"></a>Następne kroki
[Wyświetl raporty dotyczące kondycji sieci szkieletowej usług](service-fabric-view-entities-aggregated-health.md)

[Jak zgłosić i Sprawdź kondycję usług](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Monitorowanie i diagnozowania usług lokalnie](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Uaktualnianie aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md)

