---
title: "ustawienia klastra usługi sieć szkieletowa usług Azure aaaChange | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano ustawienia sieci szkieletowej hello i hello sieci szkieletowej uaktualnienia zasad, które można dostosować."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 7ced36bf-bd3f-474f-a03a-6ebdbc9677e2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: chackdan
ms.openlocfilehash: a8b125f7b4a02547cf4bcf2c936d0c7f1686c1a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-service-fabric-cluster-settings-and-fabric-upgrade-policy"></a>Dostosowywanie ustawień klastra sieci szkieletowej usług i zasady uaktualniania sieci szkieletowej
Ten dokument zawiera informacje dotyczące jak toocustomize hello różnych ustawień sieci szkieletowej i sieci szkieletowej hello zasad uaktualniania klastra sieci szkieletowej usług. Możesz dostosować je w portalu hello lub za pomocą szablonu usługi Azure Resource Manager.

> [!NOTE]
> Nie wszystkie ustawienia mogą być niedostępne za pośrednictwem portalu hello. W przypadku, gdy ustawienie wymienionych poniżej nie jest dostępny za pośrednictwem portalu hello dostosować go za pomocą szablonu usługi Azure Resource Manager.
> 

## <a name="customizing-service-fabric-cluster-settings-using-azure-resource-manager-templates"></a>Dostosowywanie ustawień klastra sieci szkieletowej usług za pomocą szablonów usługi Azure Resource Manager
Poniższe kroki Hello ilustrują sposób tooadd nowe ustawienie *MaxDiskQuotaInMB* toohello *diagnostyki* sekcji.

1. Przejdź toohttps://resources.azure.com
2. Przejdź subskrypcji tooyour rozwijając subskrypcje -> -> grupy zasobów Microsoft.ServiceFabric -> Twoja nazwa klastra
3. Witaj prawym górnym rogu wybierz "Odczytu/zapisu"
4. Wybierz edycji i aktualizacji hello `fabricSettings` elementu JSON i Dodaj nowy element

```
      {
        "name": "Diagnostics",
        "parameters": [
          {
            "name": "MaxDiskQuotaInMB",
            "value": "65536"
          }
        ]
      }
```

## <a name="fabric-settings-that-you-can-customize"></a>Ustawienia sieci szkieletowej, które można dostosować
Poniżej przedstawiono ustawienia sieci szkieletowej hello, które można dostosować:

### <a name="section-name-diagnostics"></a>Nazwa sekcji: Diagnostyka
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| ConsumerInstances |Ciąg |Lista Hello DCA konsumenta wystąpień. |
| ProducerInstances |Ciąg |Lista Hello DCA producent wystąpień. |
| AppEtwTraceDeletionAgeInDays |Int, domyślna to 3 |Liczba dni, po których firma Microsoft usuwanie starych plików ETL zawierający śladów ETW aplikacji. |
| AppDiagnosticStoreAccessRequiresImpersonation |Wartość logiczna, domyślna to true |Określa, czy personifikacja jest wymagana podczas uzyskiwania dostępu do diagnostyki są przechowywane w imieniu aplikacji hello. |
| MaxDiskQuotaInMB |Int, domyślna to 65536 |Przydział dysku w plikach dziennika MB dla systemu Windows Fabric. |
| DiskFullSafetySpaceInMB |Int, domyślny to 1024 |Pozostałe miejsce na dysku w MB tooprotect z użycia przez DCA. |
| ApplicationLogsFormatVersion |Int, domyślna to 0 |Wersja aplikacji rejestruje formatu. Obsługiwane wartości to 0 i 1. Wersja 1 zawiera więcej pól z rekordu zdarzeń ETW hello niż wersja 0. |
| ClusterId |Ciąg |Unikatowy identyfikator Hello hello klastra. To jest generowany po utworzeniu klastra hello. |
| EnableTelemetry |Wartość logiczna, domyślna to true |To będzie tooenable lub wyłączanie telemetrii. |
| EnableCircularTraceSession |Wartość logiczna, wartość domyślna to false |Flaga wskazuje, czy ma być używane sesje cykliczne śledzenia. |

### <a name="section-name-traceetw"></a>Nazwa sekcji: Trace/Etw
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| Poziom |Int, domyślna to 4 |Poziom śledzenia zdarzeń systemu Windows może przyjmować wartości 1, 2, 3, 4. toobe obsługiwany poziom śledzenia hello musi przechowywać 4 |

### <a name="section-name-performancecounterlocalstore"></a>Nazwa sekcji: PerformanceCounterLocalStore
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| IsEnabled |Wartość logiczna, domyślna to true |Flaga wskazuje, czy włączono zbieranie danych licznika wydajności w węźle lokalnym. |
| SamplingIntervalInSeconds |Int, domyślna to 60 |Interwał próbkowania dla liczniki wydajności są zbierane. |
| Liczniki |Ciąg |Rozdzielana przecinkami lista toocollect liczników wydajności. |
| MaxCounterBinaryFileSizeInMB |Int, wartość domyślna to 1 |Maksymalny rozmiar (w MB) dla każdego pliku binarnego licznika wydajności. |
| NewCounterBinaryFileCreationIntervalInMinutes |Int, domyślna to 10 |Maksymalny interwał (w sekundach), po którym zostanie utworzony nowy plik binarny licznika wydajności. |

### <a name="section-name-setup"></a>Nazwa sekcji: Instalatora
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| Zmiennej FabricDataRoot |Ciąg |Katalog główny danych sieci szkieletowej usług. Domyślny dla platformy Azure jest d:\svcfab |
| Lokalizacji FabricLogRoot |Ciąg |Katalog główny usługi sieć szkieletowa dziennika. Jest to rozmieszczenia rz dzienników i danych śledzenia. |
| ServiceRunAsAccountName |Ciąg |Nazwa konta Hello pod które toorun usługi hosta sieci szkieletowej. |
| ServiceStartupType |Ciąg |Typ uruchamiania usługi hosta sieci szkieletowej hello Hello. |
| SkipFirewallConfiguration |Wartość logiczna, wartość domyślna to false |Określa, czy ustawienia zapory należy toobe ustawiony przez hello system, lub nie. Dotyczy to tylko, jeśli używasz zapory systemu windows. Jeśli korzystasz z zapory innej firmy, a następnie należy otworzyć porty hello toouse systemu i aplikacji hello |

### <a name="section-name-transactionalreplicator"></a>Nazwa sekcji: TransactionalReplicator
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| MaxCopyQueueSize |Uint — wartość domyślna to 16384 |Jest to maksymalna wartość hello definiuje hello początkowy rozmiar kolejki hello, co umożliwia utrzymywanie operacji replikacji. Należy pamiętać, że musi być potęgą liczby 2. Jeśli w czasie wykonywania rozwoju kolejki hello toothis rozmiar operacji będzie ograniczony między hello replikatorów podstawowego i pomocniczego. |
| BatchAcknowledgementInterval | Czas w sekundach, domyślnie jest 0,015 | Określ zakres czasu w sekundach. Określa hello ilość czasu, który hello czeka replikatora po otrzymaniu operacji przed odsyła potwierdzenia. Inne operacje otrzymanych w tym czasie będzie miał ich potwierdzeń wysyłane z powrotem w pojedynczym komunikacie -> zmniejszenie ruchu w sieci, ale potencjalnie zmniejszenie przepływności hello hello replikatora. |
| MaxReplicationMessageSize |Uint — wartość domyślna to 52428800 | Maksymalny rozmiar komunikatu operacji replikacji. Domyślną jest 50MB. |
| ReplicatorAddress |ciąg, domyślną jest "localhost:0" | punkt końcowy Hello w postaci ciągu - IP:Port, używany przez hello Replikator sieci szkieletowej systemu Windows tooestablish połączenia z innymi replikami w kolejności toosend/odebrać operacji. |
| InitialPrimaryReplicationQueueSize |Uint — wartość domyślna to 64 | Ta wartość określa hello początkowy rozmiar kolejki hello, co umożliwia utrzymywanie operacji replikacji hello na powitania podstawowego. Należy pamiętać, że musi być potęgą liczby 2.|
| MaxPrimaryReplicationQueueSize |Uint — wartość domyślna to 8192 |Jest to maksymalna liczba operacji, które może znajdować się w kolejce podstawowej replikacji hello hello. Należy pamiętać, że musi być potęgą liczby 2. |
| MaxPrimaryReplicationQueueMemorySize |Uint — wartość domyślna to 0 |Jest to wartość maksymalną hello hello podstawowej replikacji kolejki w bajtach. |
| InitialSecondaryReplicationQueueSize |Uint — wartość domyślna to 64 |Ta wartość określa hello początkowy rozmiar kolejki hello, co umożliwia utrzymywanie pomocniczych operacji replikacji hello na powitania. Należy pamiętać, że musi być potęgą liczby 2. |
| MaxSecondaryReplicationQueueSize |Uint — wartość domyślna to 16384 |Jest to maksymalna liczba operacji, które może znajdować się w kolejce replikacji dodatkowej hello hello. Należy pamiętać, że musi być potęgą liczby 2. |
| MaxSecondaryReplicationQueueMemorySize |Uint — wartość domyślna to 0 |Jest to wartość maksymalną hello hello kolejki dodatkowej replikacji w bajtach. |
| SecondaryClearAcknowledgedOperations |Wartość logiczna, wartość domyślna to false |Wartość logiczna, która kontroluje, czy operacje hello na dodatkowej replikatora hello są czyszczone po uznanych toohello głównej (opróżnionych toohello dysku). Ustawienia tego tooTRUE może spowodować odczyty dodatkowy dysk na powitania nową podstawową podczas Przechwytywanie zapasową replik po przejściu w tryb failover. |
| MaxMetadataSizeInKB |Int, domyślna to 4 |Maksymalny rozmiar hello dziennika strumienia metadanych. |
| MaxRecordSizeInKB |Uint, domyślny to 1024 | Maksymalny rozmiar rekordu dziennika strumienia. |
| CheckpointThresholdInMB |Int, domyślną wartością jest 50 |Punkt kontrolny zostanie rozpoczęte, gdy użycie dziennika hello przekracza tę wartość. |
| MaxAccumulatedBackupLogSizeInMB |Int, domyślnie jest 800 |Maksymalna liczba zebranych elementów rozmiar (w MB) kopii zapasowych dzienników łańcucha danej kopii zapasowej dziennika. Przyrostowej kopii zapasowej żądań zakończy się niepowodzeniem, jeśli hello przyrostowej kopii zapasowej może wygenerować spowodowałoby dzienniki kopii zapasowych hello zebranych od hello odpowiednich pełnej kopii zapasowej toobe większy niż rozmiar tej kopii zapasowej dziennika. W takich przypadkach użytkownika jest wymagane tootake pełnej kopii zapasowej. |
| MaxWriteQueueDepthInKB |Int, domyślna to 0 | Int maksymalnego zapisu głębokość kolejki tego rejestratora core hello można użyć określonych w kilobajtach dziennika hello, który jest skojarzony z tej repliki. Ta wartość jest maksymalną liczbą bajtów, które mogą być oczekujących podczas aktualizacji rejestratora core hello. Może być 0 dla hello podstawowe toocompute rejestratora odpowiednią wartość lub wielokrotnością liczby 4. |
| SharedLogId |Ciąg |Identyfikator dziennika udostępniony. To jest identyfikator guid i powinna być unikatowa dla każdego udostępnionego dziennika. |
| SharedLogPath |Ciąg |Ścieżka dziennika udostępniony toohello. Jeśli ta wartość jest pusta dziennika udostępniony domyślnego hello jest używany. |
| SlowApiMonitoringDuration |Czas w sekundach, domyślna to 300 | Określ czas trwania dla interfejsu api, zanim ostrzeżenie kondycji zdarzenie jest wywoływane.|
| MinLogSizeInMB |Int, domyślna to 0 |Minimalny rozmiar dziennika transakcyjne hello. rozmiar tooa tootruncate poniżej tego ustawienia nie będą dozwolone Hello dziennika. 0 wskazuje, że ten replikatora hello określi hello minimalny rozmiar dziennika zgodnie z ustawieniami tooother. Zwiększenie tej wartości zwiększa możliwości hello podczas częściowej kopii i przyrostowe kopie zapasowe od szanse rekordów dziennika odpowiednich obcięcie jest obniżony. |

### <a name="section-name-fabricclient"></a>Nazwa sekcji: klienta fabricclient z rolą
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| NodeAddresses |ciąg, domyślna to "" |Kolekcja adresów (parametry połączenia) w różnych węzłach, które mogą być używane toocommunicate z hello hello Naming Service. Początkowo hello klient nawiąże połączenie, wybierając jedną z adresów hello losowo. Jeśli podano więcej niż jeden ciąg połączenia i połączenia kończy się niepowodzeniem z powodu komunikacji lub błąd upływu limitu czasu; Witaj klient przełącza adres następnego hello toouse sekwencyjnie. Witaj nazewnictwa adres usługi ponawiania szczegółowe informacje zawiera sekcja na semantykę ponownych prób. |
| ConnectionInitializationTimeout |Czas w sekundach, domyślna to 2 |Określ zakres czasu w sekundach. Interwał limitu czasu połączenia dla każdego klienta czasu próbuje tooopen bramy toohello połączenia. |
| PartitionLocationCacheLimit |Int, domyślnie jest 100000 |Liczba partycji usługi rozpoznawania w pamięci podręcznej (Ustaw too0 brak limitu). |
| ServiceChangePollInterval |Czas w sekundach, domyślna to 120 |Określ zakres czasu w sekundach. Interwał powitania kolejnym sondowaniem dla usługi zmienia powitania klienta toohello bramy dla wywołania zwrotne powiadomienia zmian zarejestrowanej usługi. |
| KeepAliveIntervalInSeconds |Int, domyślna to 20 |Interwał powitania, które powitania klienta fabricclient z rolą transportu wysyła komunikaty utrzymywania aktywności toohello bramy. 0; keepAlive jest wyłączona. Musi być wartością dodatnią. |
| HealthOperationTimeout |Czas w sekundach, domyślna to 120 |Określ zakres czasu w sekundach. limit czasu Hello wiadomości raportu wysyłane tooHealth Manager. |
| HealthReportSendInterval |Czas w sekundach, wartość domyślna to 30 |Określ zakres czasu w sekundach. Interwał Hello, w których raportowania składnika wysyła kondycji wszystkich raportów tooHealth Manager. |
| HealthReportRetrySendInterval |Czas w sekundach, wartość domyślna to 30 |Określ zakres czasu w sekundach. Interwał powitania, w których składnika raportowania ponownie wysyła kondycji zebraniu raporty tooHealth Manager. |
| RetryBackoffInterval |Czas w sekundach, domyślna to 3 |Określ zakres czasu w sekundach. wycofania interwał powitania przed ponowną próbą wykonania operacji hello. |
| MaxFileSenderThreads |Uint — wartość domyślna to 10 |Witaj maksymalna liczba plików, które są transferowane równolegle. |

### <a name="section-name-common"></a>Nazwa sekcji: wspólnej
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| PerfMonitorInterval |Czas w sekundach, wartość domyślna to 1 |Określ zakres czasu w sekundach. Interwał monitorowania wydajności. Ustawienie too0 lub wartość ujemna powoduje wyłączenie monitorowania. |

### <a name="section-name-healthmanager"></a>Nazwa sekcji: HealthManager
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| EnableApplicationTypeHealthEvaluation |Wartość logiczna, wartość domyślna to false |Klaster zasad oceny kondycji: Włączanie oceny kondycji typu aplikacji. |

### <a name="section-name-fabricnode"></a>Nazwa sekcji: FabricNode
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| StateTraceInterval |Czas w sekundach, domyślna to 300 |Określ zakres czasu w sekundach. Interwał powitania śledzenia stanu węzła w każdym węźle oraz węzły FM/FMM. |

### <a name="section-name-nodedomainids"></a>Nazwa sekcji: NodeDomainIds
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| UpgradeDomainId |ciąg, domyślna to "" |W tym artykule opisano hello domeny uaktualnień, której należy dany węzeł. |
| PropertyGroup |NodeFaultDomainIdCollection |W tym artykule opisano domen błędów hello, której należy dany węzeł. Domena błędów Hello jest zdefiniowany przez identyfikator URI, który opisuje lokalizacji hello hello węzła w hello centrum danych.  Identyfikatory URI domeny błędów są hello sformatować fd: / fd/następuje segment ścieżki identyfikatora URI.|

### <a name="section-name-nodeproperties"></a>Nazwa sekcji: NodeProperties
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| PropertyGroup |NodePropertyCollectionMap |Kolekcja par klucz wartość ciągu dla właściwości węzła. |

### <a name="section-name-nodecapacities"></a>Nazwa sekcji: NodeCapacities
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| PropertyGroup |NodeCapacityCollectionMap |Kolekcja węzła pojemności dla różnych metryk. |

### <a name="section-name-fabricnode"></a>Nazwa sekcji: FabricNode
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| StartApplicationPortRange |Int, domyślna to 0 |Początek portów aplikacji hello zarządza hosting podsystemu. Wymagane, jeśli EndpointFilteringEnabled ma wartość true w hostingu. |
| EndApplicationPortRange |Int, domyślna to 0 |Koniec (nie z wartościami granicznymi) porty aplikacji hello zarządza hosting podsystemu. Wymagane, jeśli EndpointFilteringEnabled ma wartość true w hostingu. |
| ClusterX509StoreName |jest domyślny ciąg "Moje" |Nazwa magazynu certyfikatów X.509, który zawiera certyfikat klastra do zabezpieczania komunikacji wewnątrz klastra. |
| ClusterX509FindType |ciąg, domyślna ma "postać FindByThumbprint" |Wskazuje, jak toosearch dla klastra certyfikatu w magazynie hello określonym przez ClusterX509StoreName obsługiwane wartości: "Postać FindByThumbprint"; "FindBySubjectName" z "FindBySubjectName"; gdy istnieje wiele dopasowań; Hello jedną z wygaśnięciem najdalej hello jest używany. |
| ClusterX509FindValue |ciąg, domyślna to "" |Wartość filtru wyszukiwania używane toolocate certyfikatu klastra. |
| ClusterX509FindValueSecondary |ciąg, domyślna to "" |Wartość filtru wyszukiwania używane toolocate certyfikatu klastra. |
| ServerAuthX509StoreName |jest domyślny ciąg "Moje" |Nazwa magazynu certyfikatu X.509, który zawiera certyfikat serwera dla usługi entrée. |
| ServerAuthX509FindType |ciąg, domyślna ma "postać FindByThumbprint" |Wskazuje, jak toosearch dla certyfikatu serwera w magazynie hello określonym przez wartość obsługiwane ServerAuthX509StoreName: postać FindByThumbprint; FindBySubjectName. |
| ServerAuthX509FindValue |ciąg, domyślna to "" |Wartość filtru wyszukiwania używane toolocate certyfikatu serwera. |
| ServerAuthX509FindValueSecondary |ciąg, domyślna to "" |Wartość filtru wyszukiwania używane toolocate certyfikatu serwera. |
| ClientAuthX509StoreName |jest domyślny ciąg "Moje" |Nazwa hello magazynu certyfikatu X.509, który zawiera certyfikat do roli administratora domyślnego klienta fabricclient z rolą. |
| ClientAuthX509FindType |ciąg, domyślna ma "postać FindByThumbprint" |Wskazuje, jak toosearch dla certyfikatu w magazynie hello określonym przez wartość obsługiwane ClientAuthX509StoreName: postać FindByThumbprint; FindBySubjectName. |
| ClientAuthX509FindValue |ciąg, domyślna to "" | Wartość filtru wyszukiwania używane toolocate certyfikat do roli administratora domyślnego klienta fabricclient z rolą. |
| ClientAuthX509FindValueSecondary |ciąg, domyślna to "" |Wartość filtru wyszukiwania używane toolocate certyfikat do roli administratora domyślnego klienta fabricclient z rolą. |
| UserRoleClientX509StoreName |jest domyślny ciąg "Moje" |Nazwa hello magazynu certyfikatu X.509, który zawiera certyfikat do domyślnej roli użytkownika klienta fabricclient z rolą. |
| UserRoleClientX509FindType |ciąg, domyślna ma "postać FindByThumbprint" |Wskazuje, jak toosearch dla certyfikatu w magazynie hello określonym przez wartość obsługiwane UserRoleClientX509StoreName: postać FindByThumbprint; FindBySubjectName. |
| UserRoleClientX509FindValue |ciąg, domyślna to "" |Wartość filtru wyszukiwania używany certyfikat toolocate dla roli użytkownika domyślnego klienta fabricclient z rolą. |
| UserRoleClientX509FindValueSecondary |ciąg, domyślna to "" |Wartość filtru wyszukiwania używany certyfikat toolocate dla roli użytkownika domyślnego klienta fabricclient z rolą. |

### <a name="section-name-paas"></a>Nazwa sekcji: Paas
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| ClusterId |ciąg, domyślna to "" |X509 certyfikatów Magazyn używany przez sieci szkieletowej dla ochrony konfiguracji. |

### <a name="section-name-fabrichost"></a>Nazwa sekcji: elementu FabricHost
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| StopTimeout |Czas w sekundach, domyślna to 300 |Określ zakres czasu w sekundach. limit czasu Hello w celu aktywacji usługi hostowanej. Dezaktywacja i uaktualniania. |
| StartTimeout |Czas w sekundach, domyślna to 300 |Określ zakres czasu w sekundach. Limit czasu podczas uruchamiania fabricactivationmanager. |
| ActivationRetryBackoffInterval |Czas w sekundach, domyślna to 5 |Określ zakres czasu w sekundach. Interwał wycofywania co w przypadku niepowodzenia aktywacji; na każdej ciągłego aktywacji systemu hello awarii ponowi Aktywacja hello się toohello MaxActivationFailureCount. Interwał ponawiania Hello przy każdej próbie to produkt ciągłe błędu i hello wycofania interwał aktywacji. |
| ActivationMaxRetryInterval |Czas w sekundach, domyślna to 300 |Określ zakres czasu w sekundach. Maksymalna liczba interwału ponawiania prób aktywacji. Przy ponownej próbie co ciągłego awarii hello interwał jest obliczany jako wartość minimalną (ActivationMaxRetryInterval; Ciągłe liczby awarii * ActivationRetryBackoffInterval). |
| ActivationMaxFailureCount |Int, domyślna to 10 |Jest to maksymalna liczba hello, dla którego system będzie ponawiał próby aktywacji nie powiodło się zrezygnuje. |
| EnableServiceFabricAutomaticUpdates |Wartość logiczna, wartość domyślna to false |To automatyczną aktualizację tooenable sieci szkieletowej za pośrednictwem usługi Windows Update. |
| EnableServiceFabricBaseUpgrade |Wartość logiczna, wartość domyślna to false |To jest tooenable aktualizacji dla serwera. |
| EnableRestartManagement |Wartość logiczna, wartość domyślna to false |Jest to tooenable ponownego uruchomienia serwera. |


### <a name="section-name-failovermanager"></a>Nazwa sekcji: FailoverManager
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| UserReplicaRestartWaitDuration |Czas w sekundach, wartość domyślna to 60.0 * 30 |Określ zakres czasu w sekundach. Gdy replika utrwalonego spadnie; Windows Fabric czeka na ten czas trwania dla toocome repliki hello Utwórz kopię zapasową przed utworzeniem nowej repliki zastąpienia (które wymagają kopię hello stanu). |
| QuorumLossWaitDuration |Czas w sekundach, domyślnie jest MaxValue |Określ zakres czasu w sekundach. Jest to maksymalny czas trwania hello którego zezwolimy toobe partycji, w stanie utraciła kworum. Jeśli partycja hello jest nadal w wyniku utraty kworum po tym okresie; partycja Hello jest odzyskała sprawność działania po utrata kworum przez takich hello dół repliki jako utracone. Należy pamiętać, że to potencjalnie ponieść utraty danych. |
| UserStandByReplicaKeepDuration |Czas w sekundach, domyślna to 3600.0 * 24 * 7 |Określ zakres czasu w sekundach. Gdy utrwalonego repliki wrócić z opuszczona; go może już zostały zastąpione. Ten czasomierz Określa, jak długo hello FM zachowa hello rezerwy repliki przed usunięciem. |
| UserMaxStandByReplicaCount |Int, wartość domyślna to 1 |Hello Domyślna maksymalna liczba replik w stanie StandBy, które hello system przechowuje usługi użytkownika. |

### <a name="section-name-namingservice"></a>Nazwa sekcji: NamingService
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| Wartość TargetReplicaSetSize |Int, domyślna to 7 |Witaj liczba zestawów replik dla każdej partycji hello Naming Service magazynu. Zwiększenie liczby hello repliki zestawy zwiększa hello poziomu niezawodności hello informacji w hello magazynu usługi nazewnictwa; zmniejszenie zmiana hello hello informacje zostaną utracone w wyniku awarii węzła; przy koszcie zwiększenie obciążenia sieci szkieletowej systemu Windows i hello ilość czasu zajmuje aktualizacje tooperform toohello nazewnictwa danych.|
|MinReplicaSetSize | Int, domyślna to 3 | Hello minimalnej liczby replikami Naming Service wymagane toowrite do toocomplete aktualizacji. W przypadku replik mniej niż ta aktywny w hello systemu hello niezawodności systemu nie zezwala magazynu usługi nazewnictwa toohello aktualizacji do momentu przywrócenia replik są. Ta wartość nigdy nie powinna być większa niż wartość TargetReplicaSetSize hello. |
|ReplicaRestartWaitDuration | Czas w sekundach, wartość domyślna to (60.0 * 30)| Określ zakres czasu w sekundach. Gdy replika Naming Service spadnie; Ten czasomierz uruchamia.  Po jego wygaśnięciu hello FM rozpocznie tooreplace hello replik, które są w dół (nie jeszcze uważa ich zgubienia). |
|QuorumLossWaitDuration | Czas w sekundach, domyślnie jest MaxValue | Określ zakres czasu w sekundach. Gdy pobiera Naming Service w wyniku utraty kworum; Ten czasomierz uruchamia.  Po jego wygaśnięciu hello FM uwzględni hello dół repliki jako utracone; a próba toorecover kworum. Nie, że może to spowodować utratę danych. |
|StandByReplicaKeepDuration | Czas w sekundach, domyślna to 3600.0 * 2 | Określ zakres czasu w sekundach. Gdy replik Naming Service wrócić z opuszczona; go może już zostały zastąpione.  Ten czasomierz Określa, jak długo hello FM zachowa hello rezerwy repliki przed usunięciem. |
|PlacementConstraints | ciąg, domyślna to "" | Ograniczenia umieszczania dla hello Naming Service. |
|ServiceDescriptionCacheLimit | Int, domyślna to 0 | Witaj maksymalna liczba wpisów, przechowywane w pamięci podręcznej opis usługi LRU hello na hello nazewnictwa usługi magazynu (Ustaw too0 brak limitu). |
|RepairInterval | Czas w sekundach, domyślna to 5 | Określ zakres czasu w sekundach. Interwał, w którym hello rozpocznie nazewnictwa naprawy niespójność między hello urzędu właściciela i nazwy właściciela. |
|MaxNamingServiceHealthReports | Int, domyślna to 10 | Hello maksymalnej liczby operacji powolne przechowywania nazw usługi Raporty złej kondycji w tym samym czasie. Jeśli 0; wszystkie operacje powolne są wysyłane. |
| MaxMessageSize |Int, domyślna to 4*1024*1024 |Witaj maksymalny rozmiar wiadomości do komunikacji z klientem węzła przy użyciu nazw. Łagodzenia skutków ataku DOS; Wartość domyślna to 4MB. |
| MaxFileOperationTimeout |Czas w sekundach, wartość domyślna to 30 |Określ zakres czasu w sekundach. Witaj maksymalny limit czasu dozwolony dla operacji usługi Magazyn plików. Określanie większego limitu czasu żądania zostaną odrzucone. |
| Parametru MaxOperationTimeout |Czas w sekundach, domyślna to 600 |Określ zakres czasu w sekundach. Witaj maksymalny limit czasu dozwolony dla operacji klienta. Określanie większego limitu czasu żądania zostaną odrzucone. |
| MaxClientConnections |Int, domyślna to 1000 |Witaj maksymalną dozwoloną liczbę połączeń klientów na bramę. |
| ServiceNotificationTimeout |Czas w sekundach, wartość domyślna to 30 |Określ zakres czasu w sekundach. limit czasu Hello używane w celu dostarczenia usługi powiadomień toohello klienta. |
| MaxOutstandingNotificationsPerClient |Int, domyślna to 1000 |Maksymalna liczba oczekujących powiadomienia przed rejestracji klienta Hello jest zamknięte przez hello bramy. |
| MaxIndexedEmptyPartitions |Int, domyślna to 1000 |indeksowane Hello maksymalną liczbę puste partycje, które pozostanie w pamięci podręcznej powiadomień hello synchronizowania klientów ponownie nawiązującego połączenie. Wszelkie puste partycje powyżej tego numeru zostaną usunięte z indeksu hello rosnąco wersji wyszukiwania. Ponowne łączenie klientów można nadal zsynchronizować i otrzymywać aktualizacje brakujących partycji pusty; Jednak protokół synchronizacji hello staje się bardziej kosztowne. |
| GatewayServiceDescriptionCacheLimit |Int, domyślna to 0 |Brama nazewnictwa hello Hello maksymalna liczba wpisów, przechowywane w pamięci podręcznej opis usługi LRU hello na (Ustaw too0 brak limitu). |
| Liczba partycji |Int, domyślna to 3 |Witaj liczbę partycji toobe magazynu Naming Service hello utworzony. Każda partycja jest właścicielem klucz jednej partycji, który odpowiada indeksu tooits; klucze partycji tak [0; Liczba partycji) istnieje. Ustaw coraz hello zwiększa partycje Naming Service, skali hello, której hello Naming Service może wykonywać na dzięki skróceniu hello średnia ilość danych przechowywanych przez repliką zapasowy; Koszt zwiększenie użycia zasobów (od momentu PartitionCount * ReplicaSetSize repliki usługi muszą zostać zachowane).|

### <a name="section-name-runas"></a>Nazwa sekcji: Uruchom jako
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| RunAsAccountName |ciąg, domyślna to "" |Wskazuje nazwę konta RunAs hello. Jest to potrzebne tylko dla konta "DomainUser" lub "ManagedServiceAccount" typu. Prawidłowe wartości to "domena\użytkownik" lub "user@domain". |
|RunAsAccountType|ciąg, domyślna to "" |Wskazuje typ konta Uruchom jako hello. Jest to potrzebne dla dowolnego RunAs sekcji prawidłowe wartości to "DomainUser/NetworkService/ManagedServiceAccount/LocalSystem".|
|Hasło|ciąg, domyślna to "" |Wskazuje hasło do konta Uruchom jako hello. Jest to potrzebne tylko dla typu konta "DomainUser". |

### <a name="section-name-runasfabric"></a>Nazwa sekcji: RunAs_Fabric
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| RunAsAccountName |ciąg, domyślna to "" |Wskazuje nazwę konta RunAs hello. Jest to potrzebne tylko dla konta "DomainUser" lub "ManagedServiceAccount" typu. Prawidłowe wartości to "domena\użytkownik" lub "user@domain". |
|RunAsAccountType|ciąg, domyślna to "" |Wskazuje typ konta Uruchom jako hello. Jest to potrzebne dla dowolnego RunAs sekcji prawidłowe wartości to "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|Hasło|ciąg, domyślna to "" |Wskazuje hasło do konta Uruchom jako hello. Jest to potrzebne tylko dla typu konta "DomainUser". |

### <a name="section-name-runashttpgateway"></a>Nazwa sekcji: RunAs_HttpGateway
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| RunAsAccountName |ciąg, domyślna to "" |Wskazuje nazwę konta RunAs hello. Jest to potrzebne tylko dla konta "DomainUser" lub "ManagedServiceAccount" typu. Prawidłowe wartości to "domena\użytkownik" lub "user@domain". |
|RunAsAccountType|ciąg, domyślna to "" |Wskazuje typ konta Uruchom jako hello. Jest to potrzebne dla dowolnego RunAs sekcji prawidłowe wartości to "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|Hasło|ciąg, domyślna to "" |Wskazuje hasło do konta Uruchom jako hello. Jest to potrzebne tylko dla typu konta "DomainUser". |

### <a name="section-name-runasdca"></a>Nazwa sekcji: RunAs_DCA
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| RunAsAccountName |ciąg, domyślna to "" |Wskazuje nazwę konta RunAs hello. Jest to potrzebne tylko dla konta "DomainUser" lub "ManagedServiceAccount" typu. Prawidłowe wartości to "domena\użytkownik" lub "user@domain". |
|RunAsAccountType|ciąg, domyślna to "" |Wskazuje typ konta Uruchom jako hello. Jest to potrzebne dla dowolnego RunAs sekcji prawidłowe wartości to "LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem". |
|Hasło|ciąg, domyślna to "" |Wskazuje hasło do konta Uruchom jako hello. Jest to potrzebne tylko dla typu konta "DomainUser". |

### <a name="section-name-httpgateway"></a>Nazwa sekcji: HttpGateway
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
|IsEnabled|Wartość logiczna, wartość domyślna to false | Włącza/wyłącza hello httpgateway. Httpgateway jest domyślnie wyłączona i tej konfiguracji należy tooenable zestaw toobe go. |
|ActiveListeners |Uint, domyślną wartością jest 50 | Liczba odczytów toopost toohello http serwera kolejki. Kontroluje to hello liczbę jednoczesnych żądań, które mogą być spełnione przez hello HttpGateway. |
|MaxEntityBodySize |Uint — wartość domyślna to 4194304 |  Zapewnia hello maksymalny rozmiar treści hello, których można oczekiwać od żądania http. Wartość domyślna to 4MB. Httpgateway zakończy się niepowodzeniem na żądanie, jeśli ma ona treści rozmiar > tej wartości. Rozmiar minimalny fragmentu odczytu jest 4096 bajtów. Tak, to ma toobe > 4096. |
|HttpGatewayHealthReportSendInterval |Czas w sekundach, wartość domyślna to 30 | Określ zakres czasu w sekundach. Interwał powitania, które hello Http bramy wysyła zgromadzonych tooHealth Raporty kondycji menedżera. |

### <a name="section-name-ktllogger"></a>Nazwa sekcji: KtlLogger
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
|AutomaticMemoryConfiguration |Int, wartość domyślna to 1 | Flaga wskazująca, czy hello pamięci należy dynamicznego i automatycznie skonfigurować ustawienia. Jeśli zero następnie ustawienia konfiguracji pamięci hello są używane bezpośrednio i nie należy zmieniać na podstawie systemu warunków. Jeśli następnie pamięci hello ustawienia zostaną skonfigurowane automatycznie i może ulec zmianie na podstawie systemu warunków. |
|WriteBufferMemoryPoolMinimumInKB |Int, domyślnie jest 8388608 |Liczba Hello KB tooinitially przydzielić dla puli pamięci buforu zapisu hello. Użycie wartości 0 tooindicate brak limitu domyślnego powinny być zgodne z SharedLogSizeInMB poniżej. |
|WriteBufferMemoryPoolMaximumInKB | Int, domyślna to 0 |Liczba Hello KB tooallow hello zapisu buforu pamięci puli toogrow do. Użyj 0 tooindicate brak limitu. |
|MaximumDestagingWriteOutstandingInKB | Int, domyślna to 0 | Liczba Hello KB tooallow hello udostępnionego tooadvance dziennika wcześniejsze hello dziennika dedykowanego. Użyj 0 tooindicate brak limitu.
|SharedLogPath |ciąg, domyślna to "" | Ścieżka i nazwa toolocation tooplace udostępnionego kontenera dziennika. Użyj "" dla przy użyciu ścieżki domyślnej w katalogu głównym danych sieci szkieletowej. |
|SharedLogId |ciąg, domyślna to "" |Unikatowy identyfikator guid dla kontenera dziennika udostępniony. Użyj "" Jeśli przy użyciu ścieżki domyślnej w katalogu głównym danych sieci szkieletowej. |
|SharedLogSizeInMB |Int, domyślnie jest 8192 | Liczba Hello tooallocate MB w kontenerze dziennika udostępniony hello. |

### <a name="section-name-applicationgatewayhttp"></a>Nazwa sekcji: Bramy aplikacji/Http
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
|IsEnabled |Wartość logiczna, wartość domyślna to false | Włącza/wyłącza hello HttpApplicationGateway. HttpApplicationGateway jest domyślnie wyłączona i tej konfiguracji należy tooenable zestaw toobe go. |
|NumberOfParallelOperations | Uint — wartość domyślna to 5000 | Liczba odczytów toopost toohello http serwera kolejki. Kontroluje to hello liczbę jednoczesnych żądań, które mogą być spełnione przez hello HttpGateway. |
|DefaultHttpRequestTimeout |Czas w sekundach. domyślna to 120 |Określ zakres czasu w sekundach.  Zapewnia limit czasu żądania domyślne hello hello żądań http przetwarzanych w hello http bramy aplikacji. |
|ResolveServiceBackoffInterval |Czas w sekundach, domyślna to 5 |Określ zakres czasu w sekundach.  Udostępnia domyślny hello wycofania interwał przed ponowną próbą wykonania operacji usługi rozpoznawania nie powiodło się. |
|BodyChunkSize |Uint — wartość domyślna to 16384 |  Zapewnia rozmiar hello fragmentu hello w bajtach używany tooread hello treści. |
|GatewayAuthCredentialType |ciąg, domyślną jest "None" | Wskazuje typ hello toouse poświadczeń zabezpieczeń na powitania http aplikacji bramy punktu końcowego prawidłowe wartości są "Brak / X 509. |
|GatewayX509CertificateStoreName |jest domyślny ciąg "Moje" | Nazwa magazynu certyfikatu X.509, który zawiera certyfikat dla protokołu http bramy aplikacji. |
|GatewayX509CertificateFindType |ciąg, domyślna ma "postać FindByThumbprint" | Wskazuje, jak toosearch dla certyfikatu w magazynie hello określonym przez wartość obsługiwane GatewayX509CertificateStoreName: postać FindByThumbprint; FindBySubjectName. |
|GatewayX509CertificateFindValue | ciąg, domyślna to "" | Wartość filtru wyszukiwania używany certyfikat bramy aplikacji toolocate hello http. Ten certyfikat jest skonfigurowany w punkcie końcowym https hello i mogą być używane tooverify hello tożsamości aplikacji hello w razie potrzeby przez hello usługi. FindValue jest najpierw wyszukiwane; i który nie istnieje; FindValueSecondary będą wyszukiwane. |
|GatewayX509CertificateFindValueSecondary | ciąg, domyślna to "" |Wartość filtru wyszukiwania używany certyfikat bramy aplikacji toolocate hello http. Ten certyfikat jest skonfigurowany w punkcie końcowym https hello i mogą być używane tooverify hello tożsamości aplikacji hello w razie potrzeby przez hello usługi. FindValue jest najpierw wyszukiwane; i który nie istnieje; FindValueSecondary będą wyszukiwane.|

### <a name="section-name-management"></a>Nazwa sekcji: zarządzania
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| Element ImageStoreConnectionString |SecureString | Toohello ciąg połączenia głównego do magazynu ImageStore. |
| ImageStoreMinimumTransferBPS | Int, domyślny to 1024 |szybkość transferu minimalna Hello między klastrem hello i magazynu ImageStore. Ta wartość jest używane toodetermine hello przekroczenia limitu czasu podczas uzyskiwania dostępu do hello zewnętrznych magazynu ImageStore. Zmień tę wartość, tylko jeśli hello opóźnienie między klastrem hello i magazynu ImageStore jest wysoka tooallow więcej czasu na powitania toodownload klastra z hello zewnętrznych magazynu ImageStore. |
|AzureStorageMaxWorkerThreads | Int, domyślna to 25 | Witaj maksymalną liczbę wątków roboczych równolegle. |
|AzureStorageMaxConnections | Int, domyślna to 5000 | Witaj maksymalną liczbę równoczesnych połączeń tooazure magazynu. |
|AzureStorageOperationTimeout | Czas w sekundach, domyślnie jest 6000 | Określ zakres czasu w sekundach. Limit czasu dla xstore toocomplete operacji. |
|ImageCachingEnabled | Wartość logiczna, domyślna to true | Ta konfiguracja pozwala nam tooenable lub Wyłącz buforowanie. |
|DisableChecksumValidation | Wartość logiczna, wartość domyślna to false | Ta konfiguracja pozwala nam tooenable lub wyłącz Weryfikacja sum kontrolnych podczas inicjowania obsługi aplikacji. |
|DisableServerSideCopy | Wartość logiczna, wartość domyślna to false | Ta konfiguracja Włącza lub wyłącza po stronie serwera kopię pakietu aplikacji na powitania magazynu ImageStore podczas inicjowania obsługi aplikacji. |

### <a name="section-name-healthmanagerclusterhealthpolicy"></a>Nazwa sekcji: HealthManager/ClusterHealthPolicy
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| Elementów ConsiderWarningAsError |Wartość logiczna, wartość domyślna to false |Klaster zasad oceny kondycji: ostrzeżenia są traktowane jako błędy. |
| MaxPercentUnhealthyNodes | Int, domyślna to 0 |Klaster zasad oceny kondycji: dozwolony maksymalny procent węzłów w złej kondycji dla toobe klastra hello dobrej kondycji. |
| MaxPercentUnhealthyApplications | Int, domyślna to 0 |Klaster zasad oceny kondycji: maksymalny procent zła aplikacje dozwolone dla toobe klastra hello dobrej kondycji. |
|Elementów MaxPercentDeltaUnhealthyNodes | Int, domyślna to 10 |Zasady oceny kondycji uaktualnienia klastra: maksymalny procent złej kondycji węzłów różnicowych dozwolony dla toobe klastra hello dobrej kondycji. |
|MaxPercentUpgradeDomainDeltaUnhealthyNodes | Int, domyślną jest 15 |Zasady oceny kondycji uaktualnienia klastra: dozwolony maksymalny procent różnicowych węzłów w złej kondycji w domenie uaktualnienia dla toobe klastra hello dobrej kondycji.|

### <a name="section-name-faultanalysisservice"></a>Nazwa sekcji: FaultAnalysisService
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| Wartość TargetReplicaSetSize |Int, domyślna to 0 |Witaj NOT_PLATFORM_UNIX_START TargetReplicaSetSize dla FaultAnalysisService. |
| MinReplicaSetSize |Int, domyślna to 0 |Witaj MinReplicaSetSize dla FaultAnalysisService. |
| ReplicaRestartWaitDuration |Czas w sekundach, domyślna to 60 minut|Określ zakres czasu w sekundach. Witaj ReplicaRestartWaitDuration dla FaultAnalysisService. |
| QuorumLossWaitDuration | Czas w sekundach, domyślnie jest MaxValue |Określ zakres czasu w sekundach. Witaj QuorumLossWaitDuration dla FaultAnalysisService. |
| StandByReplicaKeepDuration| Czas w sekundach, jest domyślną (60*24*7) minut |Określ zakres czasu w sekundach. Witaj StandByReplicaKeepDuration dla FaultAnalysisService. |
| PlacementConstraints | ciąg, domyślna to ""| Witaj PlacementConstraints dla FaultAnalysisService. |
| StoredActionCleanupIntervalInSeconds | Int, domyślna to 3600 |Jest to, jak często hello magazynu zostaną wyczyszczone.  Tylko akcje w stanie terminali; i że ukończono co najmniej CompletedActionKeepDurationInSeconds temu będzie można usunąć. |
| CompletedActionKeepDurationInSeconds | Int, domyślnie jest 604800 | Jest to około jak długo akcji tookeep, które są w stanie terminala.  Zależy to od również StoredActionCleanupIntervalInSeconds; ponieważ toocleanup pracy hello jest wykonywane tylko w tym interwał. 604800 wynosi 7 dni. |
| StoredChaosEventCleanupIntervalInSeconds | Int, domyślna to 3600 |Jest to, jak często hello magazynu będzie przeprowadzać inspekcję oczyszczania; Jeśli liczba hello zdarzeń jest więcej niż 30000; Oczyszczanie Hello będzie zaczną działać. |

### <a name="section-name-filestoreservice"></a>Nazwa sekcji: FileStoreService
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| NamingOperationTimeout |Czas w sekundach, domyślna to 60 |Określ zakres czasu w sekundach. Witaj limitu czasu dla operacji nazewnictwa. |
| QueryOperationTimeout | Czas w sekundach, domyślna to 60 |Określ zakres czasu w sekundach. Witaj limitu czasu dla operacji zapytania. |
| MaxCopyOperationThreads | Uint — wartość domyślna to 0 | Witaj maksymalną liczbę równoległych plików tej pomocniczej można skopiować z podstawowego. "0" == liczby rdzeni. |
| MaxFileOperationThreads | Uint — wartość domyślna to 100 | Witaj maksymalną liczbę równoległych wątków dozwolonych tooperform FileOperations (skopiowania/przeniesienia) w podstawowym hello. "0" == liczby rdzeni. |
| MaxStoreOperations | Uint — wartość domyślna to 4096 |Witaj maksymalną liczbę operacji transcation magazynu równoległego dozwolone na głównym. "0" == liczby rdzeni. |
| MaxRequestProcessingThreads | Uint — wartość domyślna to 200 |Witaj maksymalną liczbę równoległych wątków dopuszczonych żądań tooprocess w hello podstawowego. "0" == liczby rdzeni. |
| MaxSecondaryFileCopyFailureThreshold | Uint — wartość domyślna to 25| Witaj maksymalnej liczby ponownych prób kopiowania plików na powitania dodatkowej zrezygnuje. |
| AnonymousAccessEnabled | Wartość logiczna, domyślna to true |Włącza/wyłącza toohello dostęp anonimowy, który udostępnia FileStoreService. |
| PrimaryAccountType | ciąg, domyślna to "" |podstawowy Hello AccountType hello główna tooACL hello FileStoreService udziałów. |
| PrimaryAccountUserName | ciąg, domyślna to "" |Witaj kontem podstawowym Username hello główna tooACL hello FileStoreService udziałów. |
| PrimaryAccountUserPassword | SecureString, domyślnym jest pusty |hasło konta podstawowego Hello hello główna tooACL hello FileStoreService udziałów. |
| FileStoreService | PrimaryAccountNTLMPasswordSecret | SecureString, domyślnym jest pusty | Hello hasła użyty jako inicjatora toogenerated same hasła podczas korzystania z uwierzytelniania NTLM. |
| PrimaryAccountNTLMX509StoreLocation | ciąg, domyślną jest "LocalMachine"| Lokalizacja magazynu Hello hello X509 certyfikat używany toogenerate HMAC na powitania PrimaryAccountNTLMPasswordSecret podczas korzystania z uwierzytelniania NTLM. |
| PrimaryAccountNTLMX509StoreName | ciąg, domyślną jest "MY"| Nazwa magazynu Hello hello X509 certyfikat używany toogenerate HMAC na powitania PrimaryAccountNTLMPasswordSecret podczas korzystania z uwierzytelniania NTLM. |
| PrimaryAccountNTLMX509Thumbprint | ciąg, domyślna to ""|Witaj odcisk palca certyfikatu hello X509 użyć toogenerate HMAC hello PrimaryAccountNTLMPasswordSecret podczas korzystania z uwierzytelniania NTLM. |
| SecondaryAccountType | ciąg, domyślna to ""| pomocniczy Hello AccountType hello główna tooACL hello FileStoreService udziałów. |
| SecondaryAccountUserName | ciąg, domyślna to ""| Konto dodatkowej Hello Username hello główna tooACL hello FileStoreService udziałów. |
| SecondaryAccountUserPassword | SecureString, domyślnym jest pusty |hasło konta dodatkowej Hello hello główna tooACL hello FileStoreService udziałów.  |
| SecondaryAccountNTLMPasswordSecret | SecureString, domyślnym jest pusty | Hello hasła użyty jako inicjatora toogenerated same hasła podczas korzystania z uwierzytelniania NTLM. |
| SecondaryAccountNTLMX509StoreLocation | ciąg, domyślną jest "LocalMachine" |Lokalizacja magazynu Hello hello X509 certyfikat używany toogenerate HMAC na powitania SecondaryAccountNTLMPasswordSecret podczas korzystania z uwierzytelniania NTLM. |
| SecondaryAccountNTLMX509StoreName | ciąg, domyślną jest "MY" |Nazwa magazynu Hello hello X509 certyfikat używany toogenerate HMAC na powitania SecondaryAccountNTLMPasswordSecret podczas korzystania z uwierzytelniania NTLM. |
| SecondaryAccountNTLMX509Thumbprint | ciąg, domyślna to ""| Witaj odcisk palca certyfikatu hello X509 użyć toogenerate HMAC hello SecondaryAccountNTLMPasswordSecret podczas korzystania z uwierzytelniania NTLM. |

### <a name="section-name-imagestoreservice"></a>Nazwa sekcji: ImageStoreService
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| Enabled (Włączony) |Wartość logiczna, wartość domyślna to false |Witaj ImageStoreService flagi włączone. |
| Wartość TargetReplicaSetSize | Int, domyślna to 7 |Witaj TargetReplicaSetSize dla ImageStoreService. |
| MinReplicaSetSize | Int, domyślna to 3 |Witaj MinReplicaSetSize dla ImageStoreService. |
| ReplicaRestartWaitDuration | Czas w sekundach, wartość domyślna to 60.0 * 30 | Określ zakres czasu w sekundach. Witaj ReplicaRestartWaitDuration dla ImageStoreService. |
| QuorumLossWaitDuration | Czas w sekundach, domyślnie jest MaxValue | Określ zakres czasu w sekundach. Witaj QuorumLossWaitDuration dla ImageStoreService. |
| StandByReplicaKeepDuration | Czas w sekundach, domyślna to 3600.0 * 2 | Określ zakres czasu w sekundach. Witaj StandByReplicaKeepDuration dla ImageStoreService. |
| PlacementConstraints | ciąg, domyślna to "" | Witaj PlacementConstraints dla ImageStoreService. |
| ClientUploadTimeout | Czas w sekundach, domyślną jest 1800 |Określ zakres czasu w sekundach. Wartość limitu czasu dla operacji przekazywania najwyższego poziomu żądanie usługi tooImage magazynu. |
| ClientCopyTimeout | Czas w sekundach, domyślną jest 1800 | Określ zakres czasu w sekundach. Wartość limitu czasu kopiowania najwyższego poziomu żądanie usługi tooImage magazynu. |
| ClientDownloadTimeout | Czas w sekundach, domyślną jest 1800 | Określ zakres czasu w sekundach. Wartość limitu czasu pobierania najwyższego poziomu żądania usługi magazynu tooImage |
| ClientListTimeout | Czas w sekundach, domyślna to 600 | Określ zakres czasu w sekundach. Wartość limitu czasu dla listy najwyższego poziomu żądanie usługi tooImage magazynu. |
| ClientDefaultTimeout | Czas w sekundach, domyślna to 180 | Określ zakres czasu w sekundach. Wartość limitu czasu dla wszystkich żądań bez przekazywania/z systemem innym niż — pobierania (np. istnieje, Usuń) tooImage usługi magazynu. |

### <a name="section-name-imagestoreclient"></a>Nazwa sekcji: ImageStoreClient
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| ClientUploadTimeout |Czas w sekundach, domyślną jest 1800 | Określ zakres czasu w sekundach. Wartość limitu czasu dla operacji przekazywania najwyższego poziomu żądanie usługi tooImage magazynu. |
| ClientCopyTimeout | Czas w sekundach, domyślną jest 1800 | Określ zakres czasu w sekundach. Wartość limitu czasu kopiowania najwyższego poziomu żądanie usługi tooImage magazynu. |
|ClientDownloadTimeout | Czas w sekundach, domyślną jest 1800 | Określ zakres czasu w sekundach. Wartość limitu czasu pobierania najwyższego poziomu żądanie usługi tooImage magazynu. |
|ClientListTimeout | Czas w sekundach, domyślna to 600 |Określ zakres czasu w sekundach. Wartość limitu czasu dla listy najwyższego poziomu żądanie usługi tooImage magazynu. |
|ClientDefaultTimeout | Czas w sekundach, domyślna to 180 | Określ zakres czasu w sekundach. Wartość limitu czasu dla wszystkich żądań bez przekazywania/z systemem innym niż — pobierania (np. istnieje, Usuń) tooImage usługi magazynu. |

### <a name="section-name-tokenvalidationservice"></a>Nazwa sekcji: TokenValidationService
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| Dostawcy |ciąg, domyślną jest "DSTS" |Rozdzielana przecinkami lista tooenable dostawców weryfikacji tokenu (prawidłowych dostawców usług są: DSTS; AAD). Obecnie tylko jednego dostawcę można włączyć w dowolnej chwili. |

### <a name="section-name-upgradeorchestrationservice"></a>Nazwa sekcji: UpgradeOrchestrationService
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| Wartość TargetReplicaSetSize |Int, domyślna to 0 |Witaj TargetReplicaSetSize dla UpgradeOrchestrationService. |
| MinReplicaSetSize |Int, domyślna to 0 | Witaj MinReplicaSetSize dla UpgradeOrchestrationService.
| ReplicaRestartWaitDuration | Czas w sekundach, domyślna to 60 minut| Określ zakres czasu w sekundach. Witaj ReplicaRestartWaitDuration dla UpgradeOrchestrationService. |
| QuorumLossWaitDuration | Czas w sekundach, domyślnie jest MaxValue | Określ zakres czasu w sekundach. Witaj QuorumLossWaitDuration dla UpgradeOrchestrationService. |
| StandByReplicaKeepDuration | Czas w sekundach, domyślna to 60*24*7 minut | Określ zakres czasu w sekundach. Witaj StandByReplicaKeepDuration dla UpgradeOrchestrationService. |
| PlacementConstraints | ciąg, domyślna to "" | Witaj PlacementConstraints dla UpgradeOrchestrationService. |
| AutoupgradeEnabled | Wartość logiczna, domyślna to true | Automatyczne sondowania i uaktualniania akcji na podstawie pliku stanu docelowego. |
| UpgradeApprovalRequired | Wartość logiczna, wartość domyślna to false | Uaktualnianie kodu toomake ustawienie Wymagaj zgody administratora, przed kontynuowaniem. |

### <a name="section-name-upgradeservice"></a>Nazwa sekcji: UpgradeService
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| PlacementConstraints |ciąg, domyślna to "" |Witaj PlacementConstraints uaktualnienia usługi. |
| Wartość TargetReplicaSetSize | Int, domyślna to 3 | Witaj TargetReplicaSetSize dla UpgradeService. |
| MinReplicaSetSize | Int, domyślna to 2 | Witaj MinReplicaSetSize dla UpgradeService. |
| CoordinatorType | ciąg, domyślną jest "WUTest"| Witaj CoordinatorType dla UpgradeService. |
| BaseUrl | ciąg, domyślna to "" |BaseUrl dla UpgradeService. |
| ClusterId | ciąg, domyślna to "" | ClusterId dla UpgradeService. |
| X509StoreName | jest domyślny ciąg "Moje"| X509StoreName dla UpgradeService. |
| X509StoreLocation | ciąg, domyślna to "" | X509StoreLocation dla UpgradeService. |
| X509FindType | ciąg, domyślna to ""| X509FindType dla UpgradeService. |
| X509FindValue | ciąg, domyślna to "" | X509FindValue dla UpgradeService. |
| X509SecondaryFindValue | ciąg, domyślna to "" | X509SecondaryFindValue dla UpgradeService. |
| OnlyBaseUpgrade | Wartość logiczna, wartość domyślna to false | OnlyBaseUpgrade dla UpgradeService. |
| TestCabFolder | ciąg, domyślna to "" | TestCabFolder dla UpgradeService. |

### <a name="section-name-securityclientaccess"></a>Nazwa sekcji: Zabezpieczeń/ClientAccess
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| CreateName |ciąg, domyślną jest "Admin" |Konfiguracja zabezpieczeń do utworzenia identyfikatora URI nazewnictwa. |
| DeleteName |ciąg, domyślną jest "Admin" |Konfiguracja zabezpieczeń do usunięcia identyfikatora URI nazewnictwa. |
| PropertyWriteBatch |ciąg, domyślną jest "Admin" |Konfiguracja zabezpieczeń dla nazw właściwości operacji zapisu. |
| CreateService |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń do tworzenia usług. |
| CreateServiceFromTemplate |ciąg, domyślną jest "Admin" |Konfiguracja zabezpieczeń do tworzenia usług z szablonu. |
| Funkcji updateservice modułu |ciąg, domyślną jest "Admin" |Konfiguracja zabezpieczeń dla usług aktualizacji. |
| Funkcji DeleteService modułu  |ciąg, domyślną jest "Admin" |Konfiguracja zabezpieczeń do usunięcia usługi. |
| ProvisionApplicationType |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń aprowizacji typu aplikacji. |
| Operacji CreateApplication |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń do tworzenia aplikacji. |
| Funkcji deleteapplication modułu |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń do usunięcia aplikacji. |
| UpgradeApplication |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla uruchamiania lub przerywania uaktualnieniami aplikacji. |
| RollbackApplicationUpgrade |ciąg, domyślną jest "Admin" | Wycofywanie uaktualnienia aplikacji konfiguracji zabezpieczeń. |
| UnprovisionApplicationType |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń do wstrzymania obsługi administracyjnej typu aplikacji. |
| MoveNextUpgradeDomain |ciąg, domyślną jest "Admin" | Wznawianie uaktualniania aplikacji z jawnym domeny uaktualnienia konfiguracji zabezpieczeń. |
| ReportUpgradeHealth |ciąg, domyślną jest "Admin" | Wznawianie uaktualniania aplikacji z hello Bieżący postęp uaktualniania konfiguracji zabezpieczeń. |
| ReportHealth |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla raportowania kondycji. |
| ProvisionFabric |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń MSI i/lub klastra manifestu inicjowania obsługi administracyjnej. |
| UpgradeFabric |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla uruchamiania uaktualnienia klastra. |
| RollbackFabricUpgrade |ciąg, domyślną jest "Admin" | Wycofywanie uaktualnienia klastra konfiguracji zabezpieczeń. |
| UnprovisionFabric |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń MSI i/lub klastra manifestu wstrzymania obsługi administracyjnej. |
| MoveNextFabricUpgradeDomain |ciąg, domyślną jest "Admin" | Wznawianie uaktualniania klastra z jawnie domeny uaktualnienia konfiguracji zabezpieczeń. |
| ReportFabricUpgradeHealth |ciąg, domyślną jest "Admin" | Wznawianie uaktualniania klastra z hello Bieżący postęp uaktualniania konfiguracji zabezpieczeń. |
| StartInfrastructureTask |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla uruchamiania zadań infrastruktury. |
| FinishInfrastructureTask |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń kończenia zadań infrastruktury. |
| ActivateNode |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla aktywacji, a węzeł. |
| DeactivateNode |ciąg, domyślną jest "Admin" | Dezaktywacja węzła konfiguracji zabezpieczeń. |
| DeactivateNodesBatch |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dezaktywowanie wiele węzłów. |
| RemoveNodeDeactivations |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń podczas przywracania dezaktywacji na wielu węzłach. |
| GetNodeDeactivationStatus |ciąg, domyślną jest "Admin" | Sprawdzanie stanu dezaktywacji konfiguracji zabezpieczeń. |
| NodeStateRemoved |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń do raportowania stanu węzła usunięte. |
| RecoverPartition |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń do przywrócenia partycji. |
| RecoverPartitions |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń do przywrócenia partycji. |
| RecoverServicePartitions |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń do przywrócenia partycji usługi. |
| RecoverSystemPartitions |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń do przywrócenia partycji usług systemowych. |
| ReportFault |ciąg, domyślną jest "Admin" | Raportowanie błędów konfiguracji zabezpieczeń. |
| InvokeInfrastructureCommand |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń infrastruktury zadań zarządzania poleceń. |
| Operację FileContent |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla obrazu magazynu klienta transferu plików (toocluster zewnętrznych). |
| FileDownload |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla obrazu magazynu klienta pliku pobierania inicjowania (toocluster zewnętrznych). |
| InternalList |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla obrazu przechowywać operacja listy plików klienta (wewnętrzny). |
| Usuwanie |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla obrazu magazynu operację usuwania klienta. |
| Upload |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla obrazu przechowywać operacja przekazywania klienta. |
| GetStagingLocation |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla obrazu magazynu klienta tymczasowej lokalizacji pobierania. |
| GetStoreLocation |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla obrazu przechowywać Pobieranie lokalizacji magazynu klienta. |
| NodeControl |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla uruchamiania; zatrzymywanie; i ponowne uruchamianie węzłów. |
| CodePackageControl |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń ponownego uruchamiania pakietów kodu. |
| UnreliableTransportControl |ciąg, domyślną jest "Admin" | Zawodne transportu do dodawania i usuwania zachowania. |
| MoveReplicaControl |ciąg, domyślną jest "Admin" | Przenieś repliki. |
| PredeployPackageToNode |ciąg, domyślną jest "Admin" | Przedwdrożeniowe interfejsu api. |
| StartPartitionDataLoss |ciąg, domyślną jest "Admin" | Powoduje utratę danych na partycji. |
| StartPartitionQuorumLoss |ciąg, domyślną jest "Admin" | Powoduje utratę kworum na partycji. |
| StartPartitionRestart |ciąg, domyślną jest "Admin" | Jednocześnie ponownego uruchomienia niektórych lub wszystkich replik hello partycji. |
| CancelTestCommand |ciąg, domyślną jest "Admin" | Anuluje określonych TestCommand — Jeśli w locie. |
| StartChaos |ciąg, domyślną jest "Admin" | Uruchamia Chaos — Jeśli nie jest już uruchomiona. |
| StopChaos |ciąg, domyślną jest "Admin" | Zatrzymuje Chaos — Jeśli została ona uruchomiona. |
| StartNodeTransition |ciąg, domyślną jest "Admin" | Konfiguracja zabezpieczeń dla uruchamiania Przejście węzła. |
| StartClusterConfigurationUpgrade |ciąg, domyślną jest "Admin" | Wywołuje StartClusterConfigurationUpgrade na partycji. |
| GetUpgradesPendingApproval |ciąg, domyślną jest "Admin" | Wywołuje GetUpgradesPendingApproval na partycji. |
| StartApprovedUpgrades |ciąg, domyślną jest "Admin" | Wywołuje StartApprovedUpgrades na partycji. |
| Ping |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń klienta polecenia ping. |
| Zapytanie |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń dla zapytań. |
| NameExists |ciąg, domyślną jest "Admin\|\|Użytkownik" | Sprawdza, czy konfiguracja zabezpieczeń dla identyfikatora URI nazewnictwa istnienia. |
| EnumerateSubnames |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń dla identyfikatora URI nazewnictwa wyliczenia. |
| EnumerateProperties |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń dla nazw właściwości wyliczenia. |
| PropertyReadBatch |ciąg, domyślną jest "Admin\|\|Użytkownik" | Operacje odczytu dla konfiguracji zabezpieczeń dla nazw właściwości. |
| GetServiceDescription |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń dla powiadomień dotyczących usługi long sondowania i odczytywania opisy usług. |
| ResolveService |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń do rozpoznania usług zgodne. |
| ResolveNameOwner |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń rozpoznawania identyfikatora URI nazewnictwa właściciela. |
| ResolvePartition |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń w celu rozwiązania usług systemowych. |
| ServiceNotifications |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń oparty na zdarzeniach usługi powiadomień. |
| PrefixResolveService |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń do rozpoznawania prefiksu usługi opartej na zgodne. |
| GetUpgradeStatus |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń sondowania stanu uaktualniania aplikacji. |
| GetFabricUpgradeStatus |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń sondowania stan uaktualnienia klastra. |
| InvokeInfrastructureQuery |ciąg, domyślną jest "Admin\|\|Użytkownik" | Badania infrastruktury zadań konfiguracji zabezpieczeń. |
| List |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń dla obrazu przechowywać operacja listy pliku klienta. |
| Funkcji resetpartitionload modułu |ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń resetowania obciążenia failoverUnit. |
| Toggleverboseserviceplacementhealthreporting modułu | ciąg, domyślną jest "Admin\|\|Użytkownik" | Konfiguracja zabezpieczeń przełączanie pełne ServicePlacement HealthReporting. |
| GetPartitionDataLossProgress | ciąg, domyślną jest "Admin\|\|Użytkownik" | Pobiera hello postępu wywołanie interfejsu api invoke utraty danych. |
| GetPartitionQuorumLossProgress | ciąg, domyślną jest "Admin\|\|Użytkownik" | Pobiera hello postępu dla wywołania interfejsu api utraty kworum invoke. |
| GetPartitionRestartProgress | ciąg, domyślną jest "Admin\|\|Użytkownik" | Pobiera postępu hello wywołania interfejsu api ponownego uruchamiania partycji. |
| GetChaosReport | ciąg, domyślną jest "Admin\|\|Użytkownik" | Pobiera stan hello milczenia w danym okresie. |
| GetNodeTransitionProgress | ciąg, domyślną jest "Admin\|\|Użytkownik" | Pobieranie postęp w poleceniu Przejście węzła konfiguracji zabezpieczeń. |
| GetClusterConfigurationUpgradeStatus | ciąg, domyślną jest "Admin\|\|Użytkownik" | Wywołuje GetClusterConfigurationUpgradeStatus na partycji. |
| GetClusterConfiguration | ciąg, domyślną jest "Admin\|\|Użytkownik" | Wywołuje GetClusterConfiguration na partycji. |

### <a name="section-name-reconfigurationagent"></a>Nazwa sekcji: ReconfigurationAgent
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| ApplicationUpgradeMaxReplicaCloseDuration | Czas w sekundach, domyślna to 900 |Określ zakres czasu w sekundach. czas Hello, dla których hello system będzie oczekiwał przed zakończeniem hostów usługi, które mają replik, które są nadal w Zamknij. |
| ServiceApiHealthDuration | Czas w sekundach, domyślna to 30 minut | Określ zakres czasu w sekundach. ServiceApiHealthDuration definiuje, jak długo możemy czekać na toorun interfejsu API usługi przed możemy raportu złej kondycji. |
| ServiceReconfigurationApiHealthDuration | Czas w sekundach, wartość domyślna to 30 | Określ zakres czasu w sekundach. ServiceReconfigurationApiHealthDuration definiuje, jak długo hello przed usługę ponownej konfiguracji został zgłoszony jako zła. |
| PeriodicApiSlowTraceInterval | Czas w sekundach, domyślna to 5 minut | Określ zakres czasu w sekundach. PeriodicApiSlowTraceInterval Określa interwał powitania służącym powolne wywołania interfejsu API będzie ponownego wyświetlania hello monitora interfejsu API. |
| NodeDeactivationMaxReplicaCloseDuration | Czas w sekundach, domyślna to 900 | Określ zakres czasu w sekundach. Witaj toowait maksymalny czas, przed zakończeniem hosta usługi, która blokuje dezaktywacji węzła. |
| FabricUpgradeMaxReplicaCloseDuration | Czas w sekundach, domyślna to 900 | Określ zakres czasu w sekundach. RA maksymalny czas trwania Hello czeka przed zakończeniem hosta usługi repliki, który nie jest zamykany. |
| IsDeactivationInfoEnabled | Wartość logiczna, domyślna to true | Określa, czy RA użyje dezaktywacji informacji do wykonywania głównej ponownego wyboru nowych klastrów w tej konfiguracji należy ustawić tootrue w przypadku uaktualniania istniejących klastrów można znaleźć pod adresem hello informacje o wersji dotyczące tooenable to. |

### <a name="section-name-placementandloadbalancing"></a>Nazwa sekcji: PlacementAndLoadBalancing
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| TraceCRMReasons |Wartość logiczna, domyślna to true |Określa, czy tootrace przyczyny CRM wydane przeniesień toohello zdarzenia operacyjne kanału. |
| ValidatePlacementConstraint | Wartość logiczna, domyślna to true | Określa, czy hello wyrażenie PlacementConstraint usługi sprawdzania poprawności po zaktualizowaniu usługi ServiceDescription. |
| PlacementConstraintValidationCacheSize | Int, domyślna to 10 000 | Limity hello rozmiar tabeli hello używany do szybkiego sprawdzania poprawności i buforowanie wyrażeń ograniczeń umieszczania. |
|VerboseHealthReportLimit | Int, domyślna to 20 | Definiuje hello liczba repliki ma toogo unplaced przed ostrzeżenie kondycji został zgłoszony dla niego (jeśli jest włączone raportowanie kondycji pełne). |
|ConstraintViolationHealthReportLimit | Int, domyślną wartością jest 50 | Definiuje hello liczba toobe trwale Niepoprawione przed diagnostyki są wykonywane i raportów o kondycji są emitowane ma ograniczenie naruszania repliki. |
|DetailedConstraintViolationHealthReportLimit | Int, domyślna to 200 | Definiuje hello liczba toobe trwale Niepoprawione przed diagnostyki są wykonywane i raportów o kondycji szczegółowe są emitowane ma ograniczenie naruszania repliki. |
|DetailedVerboseHealthReportLimit | Int, domyślna to 200 | Definiuje hello liczba unplaced repliki ma toobe trwale unplaced przed szczegółowe kondycji, które są emitowane raportów. |
|ConsecutiveDroppedMovementsHealthReportLimit | Int, domyślna to 20 | Definiuje hello liczbę razy wystawiony ResourceBalancer przemieszczania są usuwane przed diagnostyki są wykonywane i są emitowane ostrzeżeń. Ujemna: Nie ostrzeżenia emitowane w tej sytuacji. |
|DetailedNodeListLimit | Int, domyślną jest 15 | Definiuje hello liczbę węzłów tooinclude ograniczenia przed obcięcie w powitalne raporty Unplaced repliki. |
|DetailedPartitionListLimit | Int, domyślną jest 15 | Definiuje hello liczba partycji na diagnostycznych objęcia tooinclude ograniczenia, przed obcięcie w diagnostyce. |
|DetailedDiagnosticsInfoListLimit | Int, domyślną jest 15 | Definiuje hello liczba pozycji diagnostycznych (wraz ze szczegółowymi informacjami) na ograniczenie tooinclude przed obcięcie w diagnostyce.|
|PLBRefreshGap | Czas w sekundach, wartość domyślna to 1 | Określ zakres czasu w sekundach. Definiuje hello minimalna ilość czasu, jaki musi minąć, zanim PLB odświeża stan ponownie. |
|MinPlacementInterval | Czas w sekundach, wartość domyślna to 1 | Określ zakres czasu w sekundach. Określa minimalną ilość czasu, który musi upłynąć przed dwóch kolejnych umieszczania zaokrąglenie hello. |
|MinConstraintCheckInterval | Czas w sekundach, wartość domyślna to 1 | Określ zakres czasu w sekundach. Określa minimalną ilość czasu, jaki musi minąć, zanim dwa kolejne ograniczenia sprawdzania zaokrąglenie hello. |
|MinLoadBalancingInterval | Czas w sekundach, domyślna to 5 | Określ zakres czasu w sekundach. Określa minimalną ilość czasu, który musi upłynąć przed dwóch kolejnych zaokrąglenie równoważenia hello. |
|BalancingDelayAfterNodeDown | Czas w sekundach, domyślna to 120 |Określ zakres czasu w sekundach. Nie uruchamiaj równoważenia działań w tym czasie po węzeł w dół zdarzeń. |
|BalancingDelayAfterNewNode | Czas w sekundach, domyślna to 120 |Określ zakres czasu w sekundach. Nie uruchamiaj równoważenia działań w tym czasie po dodaniu nowego węzła. |
|ConstraintFixPartialDelayAfterNodeDown | Czas w sekundach, domyślna to 120 | Określ zakres czasu w sekundach. W tym czasie po węźle zdarzenie naciśnięcia, czy nie napraw FaultDomain i UpgradeDomain naruszenia ograniczenia. |
|ConstraintFixPartialDelayAfterNewNode | Czas w sekundach, domyślna to 120 | Określ zakres czasu w sekundach. DDo nie napraw FaultDomain i UpgradeDomain naruszenia ograniczeń w tym czasie po dodaniu nowego węzła. |
|GlobalMovementThrottleThreshold | Uint — wartość domyślna to 1000 | Maksymalna liczba przeniesień dozwolone w hello równoważenia fazy w przeszłości hello interwał wskazywanym przez GlobalMovementThrottleCountingInterval. |
|GlobalMovementThrottleThresholdForPlacement | Uint — wartość domyślna to 0 | Maksymalna liczba przeniesień dozwolone w fazie umieszczania w przeszłości hello interwał wskazywanym przez GlobalMovementThrottleCountingInterval.0 oznacza brak limitu.|
|GlobalMovementThrottleThresholdForBalancing | Uint — wartość domyślna to 0 | Maksymalna liczba przeniesień dozwolone w fazie równoważenia w przeszłości hello interwał wskazywanym przez GlobalMovementThrottleCountingInterval. 0 oznacza brak limitu. |
|GlobalMovementThrottleCountingInterval | Czas w sekundach, domyślna to 600 | Określ zakres czasu w sekundach. Wskazuje długość hello hello poza interwał, dla których tootrack na domeny przemieszczania repliki (używane wraz z GlobalMovementThrottleThreshold). Można ustawić too0 tooignore globalnego ograniczania przepustowości całkowicie. |
|MovementPerPartitionThrottleThreshold | Uint, domyślną wartością jest 50 | Bez równoważenia powiązane przepływu zostanie przeprowadzona dla partycji, jeśli liczba hello równoważenia pokrewne przemieszczania replik tej partycji ma osiągnięto lub przekroczono MovementPerFailoverUnitThrottleThreshold w przeszłości hello interwał wskazywanym przez MovementPerPartitionThrottleCountingInterval. |
|MovementPerPartitionThrottleCountingInterval | Czas w sekundach, domyślna to 600 | Określ zakres czasu w sekundach. Wskazuje długość hello hello poza interwał, dla których przemieszczania replik tootrack dla każdej partycji (używane wraz z MovementPerPartitionThrottleThreshold). |
|PlacementSearchTimeout | Czas w sekundach, domyślna to 0,5 | Określ zakres czasu w sekundach. Podczas umieszczania usług. Wyszukiwanie co najwyżej takiej długości przed zwróceniem wyniku. |
|UseMoveCostReports | Wartość logiczna, wartość domyślna to false | Powoduje, że hello LB tooignore hello koszt elementu hello oceniania funkcji; Wynikowa potencjalnie dużej liczby przenosi do lepszego zrównoważonym umieszczania. |
|PreventTransientOvercommit | Wartość logiczna, wartość domyślna to false | Określa powinien PLB natychmiast liczby zasobów, które będą zwalniane przez przenosi hello zainicjowane. Domyślnie; PLB można zainicjować Przenieś i przenieść na powitania overcommit tego samego węzła, który można utworzyć przejściowej. Ustawienie uniemożliwi to tootrue parametru tymi rodzaj overcommits i defragmentacji na żądanie (alias placementWithMove) zostanie wyłączony. |
|InBuildThrottlingEnabled | Wartość logiczna, wartość domyślna to false | Ustal, czy ograniczania wbudowany hello jest włączone. |
|InBuildThrottlingAssociatedMetric | ciąg, domyślna to "" | Witaj skojarzone nazwę metryki dla tego ograniczenia przepustowości. |
|InBuildThrottlingGlobalMaxValue | Int, domyślna to 0 |Witaj maksymalna liczba replik wbudowany dozwolone globalnie. |
|SwapPrimaryThrottlingEnabled | Wartość logiczna, wartość domyślna to false| Ustal, czy ograniczania podstawowy wymiany hello jest włączone. |
|SwapPrimaryThrottlingAssociatedMetric | ciąg, domyślna to ""| Witaj skojarzone nazwę metryki dla tego ograniczenia przepustowości. |
|SwapPrimaryThrottlingGlobalMaxValue | Int, domyślna to 0 | Witaj maksymalna liczba repliki podstawowej wymiany dozwolone globalnie. |
|PlacementConstraintPriority | Int, domyślna to 0 | Określa priorytet hello ograniczenia umieszczania: 0: twarde; 1: nietrwałego; ujemna: Ignoruj. |
|PreferredLocationConstraintPriority | Int, domyślna to 2| Określa priorytet hello ograniczenie lokalizacji preferowanych: 0: twarde; 1: nietrwałego; 2: Optymalizacja; ujemna: Ignoruj |
|CapacityConstraintPriority | Int, domyślna to 0 | Określa priorytet hello ograniczenia pojemności: 0: twarde; 1: nietrwałego; ujemna: Ignoruj. |
|AffinityConstraintPriority | Int, domyślna to 0 | Określa priorytet hello ograniczenia koligacji: 0: twarde; 1: nietrwałego; ujemna: Ignoruj. |
|FaultDomainConstraintPriority | Int, domyślna to 0 | Określa priorytet hello ograniczenia domeny błędów: 0: twarde; 1: nietrwałego; ujemna: Ignoruj. |
|UpgradeDomainConstraintPriority | Int, wartość domyślna to 1| Określa priorytet hello ograniczenia domeny uaktualnień: 0: twarde; 1: nietrwałego; ujemna: Ignoruj. |
|ScaleoutCountConstraintPriority | Int, domyślna to 0 | Określa priorytet hello ograniczenie liczby skalowania w poziomie: 0: twarde; 1: nietrwałego; ujemna: Ignoruj. |
|ApplicationCapacityConstraintPriority | Int, domyślna to 0 | Określa priorytet hello ograniczenia pojemności: 0: twarde; 1: nietrwałego; ujemna: Ignoruj. |
|MoveParentToFixAffinityViolation | Wartość logiczna, wartość domyślna to false | Ustawienie, które określa, czy replik nadrzędny może być przeniesiony toofix koligacji ograniczenia.|
|MoveExistingReplicaForPlacement | Wartość logiczna, domyślna to true |Określa, czy ustawienie toomove istniejącej repliki podczas umieszczania. |
|UseSeparateSecondaryLoad | Wartość logiczna, domyślna to true | Ustawienie, które określa, czy używać różnych dodatkowej obciążenia. |
|PlaceChildWithoutParent | Wartość logiczna, domyślna to true | Ustawienie, które określa, czy podrzędnych usługi repliki można umieścić w przypadku replikacji nie jest uruchomiony. |
|PartiallyPlaceServices | Wartość logiczna, domyślna to true | Określa, czy wszystkie repliki usługi w klastrze zostanie umieszczona "wszystkie lub żadne" podany ograniczone węzłów odpowiednie dla nich.|
|InterruptBalancingForAllFailoverUnitUpdates | Wartość logiczna, wartość domyślna to false | Określa, jeśli dowolny typ aktualizacji jednostki trybu failover powinny szybkiego przerwania lub powolna równoważenia, uruchom. Z określonych równoważenia "false", uruchom zostanie przerwana w przypadku FailoverUnit: jest utworzone/usunąć; Brak replik; zmienić lokalizację repliki podstawowej lub zmiany liczby replik. Równoważenie Uruchom nie zostanie przerwana w innych przypadkach — jeśli FailoverUnit: ma dodatkowe repliki; zmienić wszystkie flagi repliki; zmienić tylko wersję partycji lub innym przypadku. |

### <a name="section-name-security"></a>Nazwa sekcji: zabezpieczeń
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| ClusterProtectionLevel |Brak lub EncryptAndSign |Brak (ustawienie domyślne) w przypadku klastrów niezabezpieczona EncryptAndSign dla bezpiecznych klastrów. |

### <a name="section-name-hosting"></a>Nazwa sekcji: hostingu
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| ServiceTypeRegistrationTimeout |Czas w sekundach, domyślna to 300 |Maksymalny dozwolony czas realizacji toobe ServiceType hello zarejestrowany w sieci szkieletowej |
| ServiceTypeDisableFailureThreshold |Liczby całkowitej, domyślna to 1 |Jest to próg hello hello liczby awarii po FailoverManager (FM) poinformowany toodisable typ usługi hello na tym węźle i spróbuj inny węzeł do umieszczania. |
| ActivationRetryBackoffInterval |Czas w sekundach, domyślna to 5 |Interwał wycofywania na co w przypadku niepowodzenia aktywacji; W przypadku każdego błędu ciągłe ponownych prób systemu hello hello Aktywacja się toohello MaxActivationFailureCount. Interwał ponawiania Hello przy każdej próbie to produkt ciągłe błędu i hello wycofania interwał aktywacji. |
| ActivationMaxRetryInterval |Czas w sekundach, domyślna to 300 |W przypadku każdego błędu ciągłe ponownych prób systemu hello hello Aktywacja się tooActivationMaxFailureCount. ActivationMaxRetryInterval określa czas oczekiwania, przed ponowną próbą wykonania po co w przypadku niepowodzenia aktywacji |
| ActivationMaxFailureCount |Liczby całkowitej, domyślna to 10 |Liczba ponownych prób system nie powiodła się Aktywacja zrezygnuje |

### <a name="section-name-failovermanager"></a>Nazwa sekcji: FailoverManager
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| PeriodicLoadPersistInterval |Czas w sekundach, domyślna to 10 |Określa, jak często hello FM sprawdzaj nowe raporty obciążenia |

### <a name="section-name-federation"></a>Nazwa sekcji: federacyjnego
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| LeaseDuration |Czas w sekundach, wartość domyślna to 30 |Czas trwania dzierżawy ważny między węzłem a jego sąsiadów. |
| LeaseDurationAcrossFaultDomain |Czas w sekundach, wartość domyślna to 30 |Czas trwania dzierżawy ważny między węzłem a jego sąsiadów domen błędów. |

### <a name="section-name-clustermanager"></a>Nazwa sekcji: ClusterManager
| **Parametr** | **Dozwolone wartości** | **Wskazówki lub krótki opis** |
| --- | --- | --- |
| UpgradeStatusPollInterval |Czas w sekundach, domyślna to 60 |częstotliwość Hello sondowanie stanu uaktualniania aplikacji. Ta wartość określa szybkość hello aktualizacji dla każde wywołanie GetApplicationUpgradeProgress |
| UpgradeHealthCheckInterval |Czas w sekundach, domyślna to 60 |częstotliwość Hello stanu kondycji sprawdza podczas uaktualniania monitorowanej aplikacji |
| FabricUpgradeStatusPollInterval |Czas w sekundach, domyślna to 60 |częstotliwość Hello sondowanie stan uaktualnienia sieci szkieletowej. Ta wartość określa szybkość hello aktualizacji dla każde wywołanie GetFabricUpgradeProgress |
| FabricUpgradeHealthCheckInterval |Czas w sekundach, domyślna to 60 |częstotliwość Hello sprawdzenie stanu kondycji podczas uaktualniania monitorowanych sieci szkieletowej |
|InfrastructureTaskProcessingInterval | Czas w sekundach, domyślna to 10 |Określ zakres czasu w sekundach. Interwał przetwarzania Hello używane przez komputer stanu infrastruktury zadań przetwarzania hello. |
|Wartość TargetReplicaSetSize |Int, domyślna to 7 |Witaj TargetReplicaSetSize dla ClusterManager. |
|MinReplicaSetSize |Int, domyślna to 3 |Witaj MinReplicaSetSize dla ClusterManager. |
|ReplicaRestartWaitDuration |Czas w sekundach, wartość domyślna to (60.0 * 30)|Określ zakres czasu w sekundach. Witaj ReplicaRestartWaitDuration dla ClusterManager. |
|QuorumLossWaitDuration |Czas w sekundach, domyślnie jest MaxValue | Określ zakres czasu w sekundach. Witaj QuorumLossWaitDuration dla ClusterManager. |
|StandByReplicaKeepDuration | Czas w sekundach, domyślnie jest (3600.0 * 2)|Określ zakres czasu w sekundach. Witaj StandByReplicaKeepDuration dla ClusterManager. |
|PlacementConstraints | ciąg, domyślna to "" |Witaj PlacementConstraints dla ClusterManager. |
|SkipRollbackUpdateDefaultService | Wartość logiczna, wartość domyślna to false |Hello CM pominie cofanie usług domyślnych zaktualizowany podczas wycofywania uaktualniania aplikacji. |
|EnableDefaultServicesUpgrade | Wartość logiczna, wartość domyślna to false |Włącz uaktualnianie usług domyślnych podczas uaktualniania aplikacji. Opisów domyślnej usługi zostaną zastąpione po uaktualnieniu. |
|InfrastructureTaskHealthCheckWaitDuration |Czas w sekundach, domyślna to 0| Określ zakres czasu w sekundach. ilość Hello toowait czas przed rozpoczęciem kontroli kondycji po przetwarzania końcowego zadanie infrastruktury. |
|InfrastructureTaskHealthCheckStableDuration | Czas w sekundach, domyślna to 0| Określ zakres czasu w sekundach. Witaj ilość czasu tooobserve kolejnych przekazany kondycji sprawdza przed przetwarzania końcowego infrastruktury zadań zakończy się pomyślnie. Przywróci ten czasomierz obserwowania sprawdzenie kondycji nie powiodło się. |
|InfrastructureTaskHealthCheckRetryTimeout | Czas w sekundach, domyślna to 60 |Określ zakres czasu w sekundach. Witaj ilość czasu toospend ponawianie próby kontroli kondycji nie powiodło się podczas przetwarzania końcowego zadanie infrastruktury. Sprawdzenie kondycji przekazany obserwowania spowoduje zresetowanie tego czasomierza. |
|ImageBuilderTimeoutBuffer |Czas w sekundach, domyślna to 3 |Określ zakres czasu w sekundach. Witaj ilość czasu tooallow dla składnika Image Builder określonego limitu czasu błędy tooreturn toohello klienta. Jeśli bufor jest zbyt mały; Następnie klient hello upłynie limit czasu, zanim serwer hello i pobiera błąd ogólny limit czasu. |
|MinOperationTimeout | Czas w sekundach, domyślna to 60 |Określ zakres czasu w sekundach. Witaj minimalna globalnego limitu czasu dla operacji na ClusterManager wewnętrznie przetwarzania. |
|Parametru MaxOperationTimeout |Czas w sekundach, domyślnie jest MaxValue | Określ zakres czasu w sekundach. Witaj maksymalną globalnego limitu czasu dla operacji na ClusterManager wewnętrznie przetwarzania. |
|MaxTimeoutRetryBuffer | Czas w sekundach, domyślna to 600 |Określ zakres czasu w sekundach. limit czasu operacji maksymalną Hello wewnętrznie ponawianie próby ukończenia tootimeouts po <Original Timeout>  +  <MaxTimeoutRetryBuffer>. Dodatkowe limitu czasu jest dodawany w przyrostach MinOperationTimeout. |
|MaxCommunicationTimeout |Czas w sekundach, domyślna to 600 |Określ zakres czasu w sekundach. Witaj maksymalny limit czasu dla wewnętrznej komunikacji między ClusterManager i innych usługach system (tj. Usługa nazewnictwa; Menedżer trybu failover i itp.). Tego limitu czasu powinna być krótsza od parametru MaxOperationTimeout globalnych, (ponieważ może istnieć wiele komunikacji między składnikami systemu dla każdej operacji klienta). |
|MaxDataMigrationTimeout |Czas w sekundach, domyślna to 600 |Określ zakres czasu w sekundach. Witaj maksymalny limit czasu dla operacji odzyskiwania migracji danych po przeprowadzeniu uaktualnienia sieci szkieletowej. |
|MaxOperationRetryDelay |Czas w sekundach, domyślna to 5| Określ zakres czasu w sekundach. Witaj Maksymalne opóźnienie dla wewnętrznego ponownych prób, gdy wystąpią błędy. |
|ReplicaSetCheckTimeoutRollbackOverride |Czas w sekundach, domyślnie jest 1200 | Określ zakres czasu w sekundach. Jeśli wartości ReplicaSetCheckTimeout ustawiono toohello maksymalną wartość DWORD; następnie zostanie zastąpiona wartością hello tej konfiguracji na potrzeby hello wycofywania. wartość Hello służąca do przeniesienia nigdy nie zostanie zastąpiona. |
|ImageBuilderJobQueueThrottle |Int, domyślna to 10 |Wątek ograniczania liczby dla składnika Image Builder kolejki zadań serwera proxy na żądania aplikacji. |

## <a name="next-steps"></a>Następne kroki
Przeczytaj następujące artykuły, aby uzyskać więcej informacji na temat zarządzania klastrem:

[Dodawanie, przerzucane, Usuń certyfikaty z klastrem Azure](service-fabric-cluster-security-update-certs-azure.md) 

