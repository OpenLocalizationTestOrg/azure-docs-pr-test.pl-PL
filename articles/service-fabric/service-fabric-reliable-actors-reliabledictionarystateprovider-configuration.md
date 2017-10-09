---
title: "Ustawienia ReliableDictionaryActorStateProvider aaaChange w Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Informacje na temat konfigurowania stanowe uczestnikami typu ReliableDictionaryActorStateProvider sieć szkieletowa usług Azure."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: 79b48ffa-2474-4f1c-a857-3471f9590ded
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 44c85a41c90a17669ba874401d7921c94e7be9ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--reliabledictionaryactorstateprovider"></a>Konfigurowanie Reliable Actors — ReliableDictionaryActorStateProvider
Domyślna konfiguracja hello ReliableDictionaryActorStateProvider można modyfikować, zmieniając pliku settings.xml hello wygenerowanych w głównym pakietu Visual Studio hello hello folderze konfiguracji dla określonego aktora hello.

środowisko uruchomieniowe usługi sieć szkieletowa usług Azure Hello szuka nazwy sekcji wstępnie zdefiniowanych w pliku settings.xml hello i wykorzystuje wartości konfiguracji hello podczas tworzenia hello podstawowych składników środowiska wykonawczego.

> [!NOTE]
> Czy **nie** usunięcia lub zmodyfikowania nazwy sekcji hello hello następujące konfiguracje w pliku settings.xml hello wygenerowanego w hello rozwiązania Visual Studio.
> 
> 

Istnieją ustawienia globalne, które mają wpływ na konfigurację hello ReliableDictionaryActorStateProvider.

## <a name="global-configuration"></a>Konfigurację globalną
konfigurację globalną Hello jest określona w manifeście klastra hello hello klastra w obszarze hello KtlLogger sekcji. Umożliwia konfiguracji hello udostępnionych dziennika lokalizacji i rozmiaru oraz hello globalne limity pamięci używane przez hello rejestratora. Należy pamiętać, wszystkich usług, które używają ReliableDictionaryActorStateProvider i niezawodne usługi stanowej wpływać na zmiany w manifeście klastra hello.

manifest klastra Hello jest pojedynczy plik XML, który przechowuje ustawienia i konfiguracje zastosować tooall węzły i usług w klastrze hello. Plik Hello jest zwykle nazywany ClusterManifest.xml. Widać hello manifestu klastra dla klastra przy użyciu polecenia programu powershell Get-ServiceFabricClusterManifest hello.

### <a name="configuration-names"></a>Nazwy konfiguracji
| Nazwa | Jednostka | Wartość domyślna | Uwagi |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Kilobajtów |8388608 |Minimalna liczba tooallocate KB w trybie jądra dla rejestratora hello zapisu puli bufora pamięci. Tej puli pamięci jest używana do buforowania informacji o stanie przed zapisaniem toodisk. |
| WriteBufferMemoryPoolMaximumInKB |Kilobajtów |Bez ograniczeń |Maksymalny rozmiar toowhich hello rejestratora zapisu buforu pamięci puli mogą rosnąć. |
| SharedLogId |IDENTYFIKATOR GUID |"" |Określa unikatowy toouse identyfikatora GUID do identyfikacji hello domyślny udostępniony plik dziennika używanych przez wszystkie usługi niezawodnego we wszystkich węzłach w klastrze hello, które nie określają hello SharedLogId ich określonej konfiguracji usługi. Jeśli określono SharedLogId, to SharedLogPath należy również określić. |
| SharedLogPath |W pełni kwalifikowana nazwa |"" |Określa pełną ścieżkę hello którym hello udostępniony plik dziennika dla wszystkich usług niezawodnej we wszystkich węzłach w klastrze hello, które nie określają hello SharedLogPath ich określonej konfiguracji usługi. Jednak jeśli SharedLogPath jest określona, to SharedLogId należy również określić. |
| SharedLogSizeInMB |Megabajtów |8192 |Określa liczbę hello MB miejsca na dysku toostatically przydzielić hello dziennika udostępniony. wartość Hello musi być 2048 lub większy. |

### <a name="sample-cluster-manifest-section"></a>Sekcja manifestu klastra próbki
```xml
   <Section Name="KtlLogger">
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
     <Parameter Name="SharedLogSizeInMB" Value="16383"/>
   </Section>
```

### <a name="remarks"></a>Uwagi
Rejestrator Hello ma globalnej puli pamięci przydzielonej z pamięci jądra niestronicowana usługi niezawodnego tooall dostępne w węźle do buforowania danych o stanie przed zapisaniem toohello dziennika dedykowanego skojarzone z repliki usługi niezawodnego hello. rozmiar puli Hello jest kontrolowana przez ustawienia WriteBufferMemoryPoolMaximumInKB i hello WriteBufferMemoryPoolMinimumInKB. WriteBufferMemoryPoolMinimumInKB określa zarówno hello początkowy rozmiar tej puli pamięci i może zmniejszyć hello najniższy rozmiar toowhich hello puli pamięci. WriteBufferMemoryPoolMaximumInKB jest może przekroczyć hello najwyższy rozmiar toowhich hello puli pamięci. Każda replika niezawodnej usługi, która jest otwarta może zwiększyć rozmiar hello hello puli pamięci o kwotę systemu ustalić się tooWriteBufferMemoryPoolMaximumInKB. Jeśli istnieje więcej zapotrzebowanie na pamięć z hello puli pamięci niż jest dostępne, żądania dotyczące pamięci zostanie opóźnione aż do pamięci. W związku z tym jeśli puli pamięci buforu zapisu hello jest zbyt mały dla konkretnej konfiguracji następnie to spowodować obniżenie wydajności.

Ustawienia SharedLogId i SharedLogPath Hello są zawsze używane razem toodefine hello identyfikator GUID i lokalizację domyślną hello udostępnionych dziennika dla wszystkich węzłów w klastrze hello. dziennika udostępniony domyślnego Hello jest używany dla wszystkich usług niezawodne, które nie określają ustawienia hello w pliku settings.xml hello hello określonej usługi. Aby uzyskać najlepszą wydajność udostępnionego pliki dziennika należy umieścić na dyskach, które są używane wyłącznie do rywalizacji tooreduce pliku dziennika hello udostępnionych.

SharedLogSizeInMB określa hello toopreallocate miejsca na dysku dla dziennika udostępniony hello domyślne we wszystkich węzłach.  SharedLogId i SharedLogPath toobe określony w kolejności dla toobe SharedLogSizeInMB określony nie jest konieczne.

## <a name="replicator-security-configuration"></a>Konfiguracja zabezpieczeń replikatora
Replikator konfiguracjach zabezpieczeń są używane toosecure kanał komunikacyjny hello, używaną podczas replikacji. Oznacza to, że usługi nie może wyświetlić siebie nawzajem ruch związany z replikacją, zapewnienie danych hello, wysoko dostępne jest także bezpiecznego.
Domyślnie puste zabezpieczeń sekcji konfiguracji uniemożliwia zabezpieczeń replikacji.

### <a name="section-name"></a>Nazwa sekcji
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Konfiguracja replikatora
Replikator konfiguracje są używane tooconfigure hello replikatora, odpowiedzialną za tworzenie stanu dostawcy stanu aktora hello wysoce niezawodne replikacji i przechowywanie stanu hello lokalnie.
Konfiguracja domyślna Hello jest generowany przez hello szablonu Visual Studio i powinny wystarczyć. Ta sekcja zawiera informacje o dodatkowych konfiguracjach, które są dostępne tootune hello replikatora.

### <a name="section-name"></a>Nazwa sekcji
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Nazwy konfiguracji
| Nazwa | Jednostka | Wartość domyślna | Uwagi |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Sekundy |0.015 |Czasie, dla których replikatora hello na dodatkowej czeka powitania po otrzymaniu operacji przed odsyła toohello potwierdzenia podstawowego. Inne toobe potwierdzeń, wysyłane do operacji przetwarzane w ramach tego interwału są wysyłane jako jedna odpowiedź. |
| ReplicatorEndpoint |Nie dotyczy |Brak wartości domyślnej — wymagany parametr |Adres IP i port, który hello replikatora podstawowe i pomocnicze użyje toocommunicate z innych replikatorów hello zestawu replik. To powinien odwoływać się do zasobów punkt końcowy protokołu TCP w hello manifestu usługi. Odwołuje się zbyt[zasoby manifestu usługi](service-fabric-service-manifest-resources.md) tooread więcej informacji na temat definiowania zasobów punktu końcowego w manifeście usługi. |
| MaxReplicationMessageSize |Bajty |50 MB |Maksymalny rozmiar danych replikacji, które mogą być przenoszone w pojedynczym komunikacie. |
| MaxPrimaryReplicationQueueSize |Liczba operacji |8192 |Maksymalna liczba operacji w kolejce głównej hello. Operacja są zwalniane, gdy Replikator głównej hello otrzyma potwierdzenia od wszystkich hello replikatorów dodatkowej. Ta wartość musi być większa niż 64 i potęgą liczby 2. |
| MaxSecondaryReplicationQueueSize |Liczba operacji |16384 |Maksymalna liczba operacji w kolejce dodatkowej hello. Operacja są zwalniane po dokonaniu jej stan wysokiej dostępności za pośrednictwem trwałości. Ta wartość musi być większa niż 64 i potęgą liczby 2. |
| CheckpointThresholdInMB |MB |200 |Ilość miejsca pliku dziennika, po upływie którego stan hello jest w użyciu. |
| MaxRecordSizeInKB |KB |1024 |Największy rozmiar rekordu hello replikatora mogą zapisywać w dzienniku hello. Ta wartość musi być wielokrotnością liczby 4 i większa niż 16. |
| OptimizeLogForLowerDiskUsage |Wartość logiczna |Wartość true |W przypadku wartości true hello dziennika jest skonfigurowana tak, aby hello repliki dedykowanych plik dziennika jest tworzony przy użyciu pliku rozrzedzonego systemu plików NTFS. Zmniejsza to użycie miejsca na dysku rzeczywiste hello hello pliku. W przypadku wartości FAŁSZ o stałej alokacji, które zapewniają najlepszą wydajność zapisu hello jest tworzony plik hello. |
| SharedLogId |Identyfikator GUID |"" |Określa unikatowy identyfikator guid toouse identyfikowanie hello udostępniony plik dziennika używane z tej repliki. Zazwyczaj usług nie należy używać tego ustawienia. Jednak jeśli SharedLogId jest określona, to SharedLogPath należy również określić. |
| SharedLogPath |W pełni kwalifikowana nazwa |"" |Określa pełną ścieżkę hello, której zostanie utworzona hello udostępniony plik dziennika dla tej repliki. Zazwyczaj usług nie należy używać tego ustawienia. Jednak jeśli SharedLogPath jest określona, to SharedLogId należy również określić. |

## <a name="sample-configuration-file"></a>Przykładowy plik konfiguracyjny
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="180" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```

## <a name="remarks"></a>Uwagi
Parametr BatchAcknowledgementInterval Hello Określa opóźnienie replikacji. Wartość "0" powoduje hello można uzyskać najmniejsze możliwe opóźnienia, kosztem hello przepływności (jak więcej komunikatów potwierdzenia musi być wysyłane i przetwarzane, zawierający mniejszą liczbę potwierdzeń).
Hello im większa wartość hello BatchAcknowledgementInterval, hello wyższej hello ogólne przepustowość replikacji na powitania kosztem większego opóźnienia operacji. Bezpośrednio przekłada opóźnienia toohello zatwierdzeń transakcji.

Hello CheckpointThresholdInMB parametru formanty hello ilość miejsca na dysku, który hello replikatora można użyć informacji o stanie toostore w pliku dziennika dedykowanego hello repliki. Zwiększenie tej wartości wyższej tooa niż domyślne hello może skutkować szybsze ponownej konfiguracji po dodaniu nowej repliki toohello zestawu. Jest to powodu przeniesienia stanu częściowego toohello, który odbywa się ze względu na dostępność toohello historii więcej operacji w dzienniku hello. To potencjalnie spowodować wydłużenie czasu odzyskiwania hello replik, po awarii.

Jeśli ustawisz OptimizeForLowerDiskUsage tootrue miejsce w pliku dziennika będą nadmiernie elastycznie tak, aby aktywnej repliki można przechowywać więcej informacji o stanie w swoich plików dziennika, gdy nieaktywnych replik użyje mniej miejsca na dysku. Dzięki temu możliwe toohost więcej replik w węźle. Jeśli ustawisz OptimizeForLowerDiskUsage toofalse informacje o stanie hello są zapisywane pliki dziennika toohello szybciej.

Ustawienie MaxRecordSizeInKB Hello definiuje hello maksymalny rozmiar rekordu, które mogą być zapisywane w pliku dziennika hello przez replikatora hello. W większości przypadków hello domyślny rozmiar rekordu 1024 KB jest optymalna. Jednak jeśli usługa hello powoduje większych danych elementów toobe część informacji o stanie hello, ta wartość trzeba zwiększyć toobe. Brak małego korzyści w podejmowaniu MaxRecordSizeInKB mniejszych niż 1024, jako mniejsze rekordów, użyj tylko hello przestrzeń na powitania mniejszych rekordu. Oczekuje się, że ta wartość musi toobe zmienić tylko w rzadkich przypadkach.

Ustawienia SharedLogId i SharedLogPath Hello są zawsze używane razem toomake usługi użyj oddzielnych dziennika udostępniony z dziennika udostępniony domyślne hello hello węzła. Aby uzyskać najlepszą wydajność, dowolną liczbę usług, jak to możliwe, należy określić hello sam udostępnionych dziennika. Udostępnione pliki dziennika powinna zostać umieszczona na dyskach, które są używane wyłącznie do hello udostępnionego pliku dziennika tooreduce head przepływu rywalizacji. Oczekuje się, że te wartości musi toobe zmienić tylko w rzadkich przypadkach.

