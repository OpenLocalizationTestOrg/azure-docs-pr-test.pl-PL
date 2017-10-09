---
title: "aaaTroubleshoot z raportów o kondycji systemu | Dokumentacja firmy Microsoft"
description: "Opis raportów o kondycji hello wysyłane przez składniki sieci szkieletowej usług Azure i ich użycia dla klastra rozwiązywaniu problemów lub problemów aplikacji."
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
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a>Użyj tootroubleshoot Raporty kondycji systemu
Azure Service Fabric raportu składników fabrycznej hello na wszystkich jednostek w klastrze hello. Witaj [magazynu kondycji](service-fabric-health-introduction.md#health-store) tworzy i usuwa jednostki na podstawie hello systemu raportów. Również organizuje ona je w hierarchii, która przechwytuje interakcje jednostki.

> [!NOTE]
> Pojęcia dotyczące kondycji toounderstand Dowiedz się więcej o [model kondycji sieci szkieletowej usług](service-fabric-health-introduction.md).
> 
> 

Raporty kondycji systemu zapewniają wgląd w klastrze i funkcjonalność aplikacji i flagi błędów za pomocą kondycji. Dla aplikacji i usług systemowych raportów kondycji Sprawdź, czy jednostki są zaimplementowane i są działa prawidłowo z hello perspektywy sieci szkieletowej usług. Raporty Hello nie zawierają żadnych monitorowanie kondycji hello logiki biznesowej usługi hello lub wykrywania zawieszone procesy. Usługi użytkownik może uzupełnić hello dane kondycji z logiką tootheir określonych informacji.

> [!NOTE]
> Watchdogs raportów o kondycji są widoczne tylko *po* składników systemu hello Tworzenie jednostki. Po usunięciu jednostki magazynu kondycji hello automatycznie usuwa wszystkie raporty kondycji skojarzonych z nim. Witaj dotyczy po utworzeniu nowego wystąpienia obiektu hello (na przykład nowe wystąpienie usługi stanowej utrwalonego repliki jest tworzona). Wszystkie raporty skojarzone z wystąpieniem starego hello usunąć i wyczyścić sklepie hello.
> 
> 

Witaj raporty składnik systemu są identyfikowane przez źródło hello, w którym rozpoczyna się od hello "**systemu.**" prefiks. Watchdogs nie można użyć hello sam prefiks dla ich źródła, jak raporty z nieprawidłowe parametry są odrzucane.
Załóżmy przyjrzeć się niektóre systemu raporty toounderstand wywołujących je i jak toocorrect hello możliwe problemy reprezentują.

> [!NOTE]
> Sieć szkieletowa usług nadal tooadd raporty dotyczące warunków odsetek zwiększających wgląd w działania wykonywane w klastrze hello i aplikacji. Może również zostać poprawione istniejących raportów z bardziej szczegółowymi informacjami toohelp hello Rozwiązywanie problemów z szybciej.
> 
> 

## <a name="cluster-system-health-reports"></a>Klaster systemowych raportów kondycji
jednostki kondycji klastra Hello jest tworzony automatycznie w magazynie kondycji hello. Jeśli wszystko działa prawidłowo, nie ma raportu system.

### <a name="neighborhood-loss"></a>Utrata otoczenie
**System.Federation** zgłasza błąd, jeśli wykryje utraty otoczenia. Raport Hello jest w poszczególnych węzłach, a identyfikator węzła hello jest uwzględniony w nazwie właściwości hello. Jeden otoczenie jest zgubiony hello całej sieci szkieletowej usług pierścienia, zwykle można spodziewać się dwa zdarzenia (obie strony raportu przerwę hello). W przypadku utraty więcej klubów ma więcej zdarzeń.

Raport Hello określa limit czasu operacji hello globalnego dzierżawy jako czas hello toolive. Raport Hello jest ponowne wysłanie co pół czas TTL hello tak długo, jak warunek hello pozostaje aktywna. Zdarzenie Hello zostanie automatycznie usunięta po jego wygaśnięciu. Usuń, gdy wygasłe zachowanie gwarantuje, że raport hello są czyszczone z magazynu kondycji hello poprawnie, nawet, jeśli węzeł raportowania hello jest wyłączony.

* **SourceId**: System.Federation
* **Właściwość**: rozpoczyna się od **otoczenie** i zawiera informacje na węzeł
* **Następne kroki**: Sprawdź, dlaczego otoczenie hello jest utracone (na przykład wyboru hello komunikacji między węzłami klastra).

## <a name="node-system-health-reports"></a>Węzeł systemowych raportów kondycji
**System.FM**, który reprezentuje hello usługi Menedżera trybu Failover, jest urzędu hello, który zarządza informacjami o węzłach klastra. Każdy węzeł powinien mieć jeden raport z System.FM przedstawiający jego stanu. jednostek node Hello są usuwane po usunięciu stan węzła hello (zobacz [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>Węzeł w górę lub w dół
System.FM raportów jako OK, gdy węzeł hello dołącza pierścień hello (jest uruchomiona). Zgłasza błąd, gdy węzeł hello odjazdem pierścień hello (działa, albo do uaktualnienia lub po prostu ponieważ nie powiodła się). utworzony przez magazynu kondycji hello hierarchii kondycji Hello podejmuje działania na jednostkach wdrożonej w korelacji z raportów węzłów System.FM. Traktuje hello węzła nadrzędnego wirtualnego wszystkich wdrożonych jednostek. jednostek Hello wdrożone w tym węźle dostępnych za pośrednictwem zapytania, jeśli węzeł hello jest zgłaszana jako się przez System.FM, z hello takie same wystąpienia jako wystąpienie hello skojarzone z jednostek hello. Gdy System.FM zgłasza tego węzła hello jest wyłączony lub ponownego uruchomienia (nowe wystąpienie), magazynu kondycji hello automatycznie oczyszcza hello wdrożone jednostek, które może istnieć tylko na powitania węzeł w dół lub poprzednie wystąpienie hello hello węzła.

* **SourceId**: System.FM
* **Właściwość**: stan
* **Następne kroki**: Jeśli hello węzeł w dół do uaktualnienia, powinna ona przywrócona po został uaktualniony. W takim przypadku stan kondycji hello powinien przełącznika tooOK Wstecz. Jeśli węzeł hello nie wróć lub go nie powiedzie się, hello problem musi więcej dochodzenia.

Witaj poniższy przykład przedstawia hello System.FM zdarzeń o stanie kondycji OK dla węzła:

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
**System.FabricNode** zgłosi ostrzeżenie, gdy zbliża się ważności certyfikatów używanych przez węzeł hello. Występują trzy certyfikaty w każdym węźle: **Certificate_cluster**, **Certificate_server**, i **Certificate_default_client**. Po wygaśnięciu hello jest co najmniej dwa tygodnie, stan kondycji raportów hello jest OK. W przypadku wygaśnięcia hello w ciągu dwóch tygodni, typ raportu hello jest ostrzeżenie. TTL te zdarzenia jest nieskończone, i usuwane, gdy węzeł opuści hello klastra.

* **SourceId**: System.FabricNode
* **Właściwość**: rozpoczyna się od **certyfikatu** i zawiera więcej informacji na temat hello typ certyfikatu
* **Następne kroki**: Aktualizuj certyfikaty, hello, jeśli są one wkrótce wygasną.

### <a name="load-capacity-violation"></a>Naruszenie pojemności obciążenia
Witaj modułu równoważenia obciążenia sieci szkieletowej usług zgłosi ostrzeżenie po wykryciu naruszenie pojemności węzła.

* **SourceId**: System.PLB
* **Właściwość**: rozpoczyna się od **pojemności**
* **Następne kroki**: Sprawdź podany obecna pojemność hello metryki i widoku w węźle hello.

## <a name="application-system-health-reports"></a>Aplikacja systemowych raportów kondycji
**System.CM**, który reprezentuje hello Menedżera klastra usługi, jest urzędu hello, który zarządza informacjami o aplikacji.

### <a name="state"></a>Stan
System.CM raporty jako OK aplikacji hello został utworzony lub zaktualizowany. Informuje magazynu kondycji powitania po usunięciu aplikacji hello, dzięki czemu może zostać usunięty z magazynu.

* **SourceId**: System.CM
* **Właściwość**: stan
* **Następne kroki**: Jeśli aplikacji hello została utworzona lub zaktualizowana, powinny zawierać hello raport o kondycji Menedżera klastra. W przeciwnym razie sprawdź stan hello aplikacji hello wysyłając kwerendy (na przykład Witaj polecenia cmdlet programu PowerShell **Get ServiceFabricApplication - ApplicationName *applicationName***).

Witaj poniższy przykład przedstawia zdarzenia stanu hello na powitania **fabric: / WordCount** aplikacji:

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
**System.FM**, który reprezentuje hello usługi Menedżera trybu Failover, jest urzędu hello, który zarządza informacjami o usługach.

### <a name="state"></a>Stan
System.FM raporty jako OK po utworzeniu hello usługi. Usuwa hello jednostki z magazynu kondycji powitania po usunięciu hello usługi.

* **SourceId**: System.FM
* **Właściwość**: stan

Witaj poniższy przykład przedstawia zdarzenia stanu hello w usłudze hello **fabric: / WordCount/WordCountWebService**:

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
**System.PLB** zgłasza błąd, jeśli wykryje, że aktualizacja toobe usługi, skorelowane z innej usługi tworzy łańcuch koligacji. Raport Hello jest wyczyszczone po pomyślnej aktualizacji.

* **SourceId**: System.PLB
* **Właściwość**: ServiceDescription
* **Następne kroki**: hello wyboru skorelowane opisy usług.

## <a name="partition-system-health-reports"></a>Partycja systemowych raportów kondycji
**System.FM**, który reprezentuje hello usługi Menedżera trybu Failover, jest urzędu hello, który zarządza informacjami o partycji usługi.

### <a name="state"></a>Stan
System.FM raportów, jako OK gdy partycji hello został utworzony i działa prawidłowo. Usuwa hello jednostki z magazynu kondycji powitania po usunięciu hello partycji.

W przypadku partycji hello poniżej hello repliki minimalna liczba, zgłasza błąd. Jeśli hello partycja nie jest mniej hello repliki minimalna liczba, ale jest on poniżej hello docelowa liczba replik, zgłosi ostrzeżenie. W przypadku partycji hello w wyniku utraty kworum, System.FM zgłasza błąd.

Innych ważnych wydarzeń, zawierać ostrzeżenie podczas ponownej konfiguracji hello trwa dłużej, niż oczekiwano i podczas kompilacji hello trwa dłużej, niż oczekiwano. czasy Hello oczekiwano hello kompilacji i ponownej konfiguracji są konfigurowane w oparciu o scenariuszach usługi. Na przykład jeśli usługa ma terabajt stanu, takie jak bazy danych SQL, kompilacji hello trwa dłużej niż usługi z małej ilości stanu.

* **SourceId**: System.FM
* **Właściwość**: stan
* **Następne kroki**: Jeśli stan kondycji hello nie jest OK, jest to możliwe, że niektóre repliki nie zostały utworzone, otwarty lub awansowana tooprimary lub pomocniczej poprawnie. W wielu przypadkach hello główną przyczyną jest to błąd usługi w hello open lub implementacji zmiany roli.

Witaj poniższy przykład przedstawia partycji dobrej kondycji:

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

Witaj poniższy przykład przedstawia kondycję hello partycji, która znajduje się poniżej docelowej liczby replik. Witaj następnym krokiem jest tooget hello partycji opis, który pokazuje, jak skonfigurowano: **MinReplicaSetSize** trzy i **TargetReplicaSetSize** wynosi siedem. Następnie Uzyskaj hello liczby węzłów w klastrze hello: pięć. Dlatego w tym przypadku dwóch replik nie można umieścić, ponieważ liczba replik w docelowym hello jest wyższy niż hello liczby dostępnych węzłów.

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
**System.PLB** zgłosi ostrzeżenie, jeśli wykryje naruszenie ograniczenia repliki i nie można umieścić wszystkich replik partycji. wyświetlone szczegóły raportu Hello których ograniczeń i właściwości zapobiec hello repliki umieszczania.

* **SourceId**: System.PLB
* **Właściwość**: rozpoczyna się od **ReplicaConstraintViolation**

## <a name="replica-system-health-reports"></a>Repliki systemowych raportów kondycji
**System.RA**, reprezentuje składnika agenta rekonfiguracji hello, jest źródłem hello hello stanu repliki.

### <a name="state"></a>Stan
**System.RA** raporty OK po utworzeniu repliki hello.

* **SourceId**: System.RA
* **Właściwość**: stan

Witaj poniższy przykład przedstawia repliki dobrej kondycji:

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
Opis Hello raport o kondycji zawiera czas rozpoczęcia hello (Coordinated Universal Time) podczas wywołania hello interfejsu API.

**System.RA** zgłosi ostrzeżenie, jeśli repliki hello Otwórz trwa dłużej niż okres hello skonfigurowane (domyślne: 30 minut). Jeśli hello interfejsu API ma wpływ na dostępność usługi, raport hello zgłaszany jest znacznie szybciej (można skonfigurować interwał, z domyślną 30 sekund). czas Hello obejmuje czas hello replikatora hello Otwórz i Otwórz usługę hello. kończy Hello tooOK zmiany właściwości hello otwarcia.

* **SourceId**: System.RA
* **Właściwość**: **ReplicaOpenStatus**
* **Następne kroki**: Jeśli stan kondycji hello nie jest OK, sprawdź, dlaczego repliki hello Otwórz trwa dłużej, niż oczekiwano.

### <a name="slow-service-api-call"></a>Wywołanie interfejsu API usługi powolne
**System.RAP** i **System.Replicator** raport ostrzeżenie, jeśli kod wywołania toohello użytkownika usługi trwa dłużej niż hello skonfigurowane. Ostrzeżenie Hello są czyszczone po zakończeniu wywołania hello.

* **SourceId**: System.RAP lub System.Replicator
* **Właściwość**: Nazwa hello hello powolne interfejsu API. Opis Hello zawiera szczegółowe informacje o hello czasu hello interfejsu API został oczekujące.
* **Następne kroki**: Sprawdź, dlaczego wywołania hello trwa dłużej, niż oczekiwano.

Hello poniższy przykład przedstawia partycja utraciła kworum i hello dochodzenia czynności wykonywane toofigure się, dlaczego. Jeden z replik hello ma ostrzegawczy stan kondycji, aby uzyskać jego kondycji. Pokazuje, że operacja usługi hello trwa dłużej, niż oczekiwano zdarzenie zgłaszane przez System.RAP. Po otrzymaniu tych informacji hello następnym krokiem jest toolook na powitania kodu usługi i zbadaj istnieje. Dla tego przypadku hello **RunAsync** implementacji usługi stanowej hello zgłasza nieobsługiwany wyjątek. repliki Hello są odzyskiwanie, więc nie widać żadnych replik w stanie ostrzeżenia hello. Można ponowić próbę pobierania stanu kondycji hello i wyszukaj różnice w identyfikatorze hello repliki. W niektórych przypadkach prób hello pozwalają uzyskać wskazówki.

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

Po uruchomieniu hello błędnej aplikacji w debugerze hello windows zdarzeń diagnostycznych hello Pokaż hello wyjątek z RunAsync:

![Visual Studio 2015 zdarzeń diagnostycznych: niepowodzenie RunAsync w sieci szkieletowej: / HelloWorldStatefulApplication.][1]

Visual Studio 2015 zdarzeń diagnostycznych: niepowodzenie RunAsync w **fabric: / HelloWorldStatefulApplication**.

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>Kolejka replikacji jest pełna
**System.Replicator** zgłosi ostrzeżenie, gdy kolejka replikacji hello jest pełna. Na głównej hello kolejki replikacji zazwyczaj zapełni ponieważ co najmniej jeden replikach pomocniczych operacji tooacknowledge powolne. Na powitania dodatkowej to zazwyczaj miejsce, gdy usługa hello jest powolne tooapply hello operacji. Ostrzeżenie Hello są czyszczone po hello kolejki nie jest już pełna.

* **SourceId**: System.Replicator
* **Właściwość**: **PrimaryReplicationQueueStatus** lub **SecondaryReplicationQueueStatus**w zależności od roli repliki hello

### <a name="slow-naming-operations"></a>Powolne operacje nazewnictwa
**System.NamingService** raportów kondycji na jego repliką podstawową, gdy operacja nazewnictwa trwa dłużej niż dopuszczalne. Przykłady operacji nazewnictwa [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) lub [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync). Więcej metod można znaleźć w obszarze klienta fabricclient z rolą, na przykład w obszarze [usługi metod zarządzania](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) lub [metod zarządzania właściwości](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).

> [!NOTE]
> Hello Naming service jest rozpoznawany jako lokalizacja tooa nazwy usługi w klastrze hello i umożliwia użytkownikom toomanage usługi nazwy i właściwości. Jest to sieć szkieletowa usług na partycje utrwalone usługi. Reprezentuje jedną z partycji hello hello Authority Owner zawierający metadane dotyczące wszystkich nazw usługi Service Fabric i usług. nazwy sieci szkieletowej usług Hello są mapowane toodifferent partycji, o nazwie właściciela partycji, dlatego usługa hello jest rozszerzony. Przeczytaj więcej na temat [Naming service](service-fabric-architecture.md).
> 
> 

Podczas operacji nazewnictwa trwa dłużej, niż oczekiwano, operacja hello oflagowane z raportem ostrzeżenie na powitania *replikę podstawową hello partycji usługi nazw, która służy operacji hello*. Jeśli operacja hello zakończy się pomyślnie, hello ostrzeżenie jest wyczyszczone. Jeśli hello zakończeniu operacji z powodu błędu hello raport o kondycji zawiera szczegółowe informacje o błędzie hello.

* **SourceId**: System.NamingService
* **Właściwość**: rozpoczyna się od prefiksu **Duration_** i identyfikuje hello wolne działanie i nazwę sieci szkieletowej usług hello, w których hello operacji są stosowane. Na przykład jeśli Tworzenie usługi w sieci szkieletowej name: / MyApp/Moja_usługa trwa zbyt długo, właściwość hello jest Duration_AOCreateService.fabric:/MyApp/MyService. AO rola toohello punktów hello nazw partycji dla tej nazwy i operację.
* **Następne kroki**: niepowodzenia hello nazewnictwa operacji wyboru. Każda operacja mogą mieć różnych przyczyn. Na przykład usunąć usługi mogą zostać zatrzymane w węźle, ponieważ host aplikacji hello śledzi awarii w węźle powodu usterki użytkownika tooa hello kodem usługi.

Witaj poniższy przykład przedstawia operację tworzenia usługi. Operacja Hello trwało dłużej niż czas trwania hello skonfigurowane. AO ponawia próbę i wysyła tooNO pracy. NIE ukończono hello ostatniej operacji limitu czasu. W takim przypadku hello tej samej repliki jest kluczem podstawowym hello AO i żadnych ról.

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
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
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
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>DeployedApplication systemowych raportów kondycji
**System.Hosting** urzędu hello na wdrożonym jednostek.

### <a name="activation"></a>aktywacji
System.Hosting raportów, jako OK gdy aplikacji został pomyślnie uaktywniony na powitania węzła. W przeciwnym razie go zgłasza błąd.

* **SourceId**: System.Hosting
* **Właściwość**: aktywacji wersji wdrożenia hello
* **Następne kroki**: Jeśli aplikacja hello jest zła, sprawdź, dlaczego hello aktywacja nie powiodła się.

Witaj poniższy przykład przedstawia pomyślnej aktywacji:

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Do pobrania
**System.Hosting** zgłasza błąd, jeśli pobieranie pakietu aplikacji hello nie powiedzie się.

* **SourceId**: System.Hosting
* **Właściwość**:  **pobrać:*RolloutVersion***
* **Następne kroki**: Sprawdź, dlaczego hello pobieranie nie powiodło się w węźle hello.

## <a name="deployedservicepackage-system-health-reports"></a>DeployedServicePackage systemowych raportów kondycji
**System.Hosting** urzędu hello na wdrożonym jednostek.

### <a name="service-package-activation"></a>Aktywowanie pakietu usługi
Jako OK System.Hosting raporty, jeśli aktywowanie pakietu usługi hello w węźle hello zakończy się pomyślnie. W przeciwnym razie go zgłasza błąd.

* **SourceId**: System.Hosting
* **Właściwość**: aktywacji
* **Następne kroki**: Sprawdź, dlaczego hello aktywacja nie powiodła się.

### <a name="code-package-activation"></a>Aktywowanie pakietu kodu
**System.Hosting** raporty jako OK dla każdego pakietu kodu, jeśli aktywacja hello zakończy się pomyślnie. W przypadku niepowodzenia aktywacji hello zgłosi ostrzeżenie zgodnie z konfiguracją. Jeśli **elementu CodePackage** nie powiedzie się tooactivate lub kończy się z powodu błędu większy niż skonfigurowany hello **CodePackageHealthErrorThreshold**, hosting zgłasza błąd. Jeśli pakiet usługi zawiera wiele pakietów kodu, aktywacji raport jest generowany dla każdego z nich.

* **SourceId**: System.Hosting
* **Właściwość**: prefiks hello używa **CodePackageActivation** i zawiera nazwę hello hello pakietu kodu i punktu wejścia hello jako  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint*** (na przykład **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>Rejestracja typu usługi
**System.Hosting** zgłasza jako OK, jeśli typ usługi hello został pomyślnie zarejestrowany. Zgłasza błąd, jeśli hello rejestracja nie została wykonana w czasie (zgodnie z konfiguracją przy użyciu **ServiceTypeRegistrationTimeout**). Jeśli środowisko uruchomieniowe hello są zamknięte, typ usługi hello jest zarejestrowany z węzła hello i hostingu zgłosi ostrzeżenie.

* **SourceId**: System.Hosting
* **Właściwość**: prefiks hello używa **ServiceTypeRegistration** i zawiera nazwę typu usługi hello (na przykład **ServiceTypeRegistration:FileStoreServiceType**)

Witaj poniższy przykład przedstawia pakietu dobrej kondycji wdrożonej usługi:

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Do pobrania
**System.Hosting** zgłasza błąd, jeśli pobieranie pakietu hello usługi nie powiedzie się.

* **SourceId**: System.Hosting
* **Właściwość**:  **pobrać:*RolloutVersion***
* **Następne kroki**: Sprawdź, dlaczego hello pobieranie nie powiodło się w węźle hello.

### <a name="upgrade-validation"></a>Weryfikacja uaktualnienia
**System.Hosting** zgłasza błąd w przypadku niepowodzenia weryfikacji podczas uaktualniania hello lub hello uaktualnienie nie powiedzie się w węźle hello.

* **SourceId**: System.Hosting
* **Właściwość**: prefiks hello używa **FabricUpgradeValidation** i zawiera hello uaktualniania wersji
* **Opis elementu**: Napotkano błąd toohello punktów

## <a name="next-steps"></a>Następne kroki
[Wyświetl raporty dotyczące kondycji sieci szkieletowej usług](service-fabric-view-entities-aggregated-health.md)

[Jak tooreport i zaznacz pole wyboru usługi kondycji](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Monitorowanie i diagnozowania usług lokalnie](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Uaktualnianie aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md)

