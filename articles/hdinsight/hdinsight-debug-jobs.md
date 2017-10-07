---
title: "Debugowanie Hadoop w usłudze HDInsight: Sprawdź dzienniki i interpretować komunikaty o błędach - Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat wiadomości powitania błąd, który może pojawić się w przypadku administrowania HDInsight przy użyciu programu PowerShell i czynności, które można wykonać toorecover."
services: hdinsight
tags: azure-portal
editor: cgronlun
manager: jhubbard
author: mumian
documentationcenter: 
ms.assetid: 7e6ceb0e-8be8-4911-bc80-20714030a3ad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 2f12a40e9dcac32ce2e11d66d60d8b3b212ecb53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-hdinsight-logs"></a>Analizowanie dzienników usługi HDInsight
Poszczególnych klastrów Hadoop w usłudze Azure HDInsight ma konto usługi Azure storage używane jako hello domyślnego systemu plików. Konto magazynu Hello jest określane jako domyślne konto magazynu hello. Klaster używa hello magazynu tabel Azure i hello magazynu obiektów Blob na powitania domyślny magazyn konta toostore jej dzienników.  toofind limit hello domyślne konto magazynu dla klastra, zobacz [klastrów zarządzania Hadoop w HDInsight](hdinsight-administer-use-management-portal.md#find-the-default-storage-account). Dzienniki Hello zachowują się w hello konta magazynu, nawet po usunięciu klastra hello.

## <a name="logs-written-tooazure-tables"></a>Dzienniki zapisane tooAzure tabel
Hello Dzienniki zapisane tabele tooAzure Podaj jeden poziom wgląd w działania wykonywane z klastrem usługi HDInsight.

Podczas tworzenia klastra usługi HDInsight 6 tabele są tworzone automatycznie dla opartych na systemie Linux klastrów w magazynie tabel domyślne hello:

* hdinsightagentlog
* syslog
* daemonlog
* hadoopservicelog
* ambariserverlog
* ambariagentlog

3 tabele są tworzone w przypadku klastrów z systemem Windows:

* setuplog: dziennika zdarzeń/wyjątków podczas inicjowania obsługi administracyjnej/tworzenia klastrów usługi HDInsight.
* hadoopinstalllog: dziennika zdarzeń/wyjątków napotkanych podczas instalowania na powitania klastra usługi Hadoop. W tej tabeli mogą być przydatne w debugowaniu problemów związanych tooclusters utworzony z użyciem niestandardowych parametrów.
* hadoopservicelog: dziennika zdarzeń/wyjątki zarejestrowane przez wszystkie usługi Hadoop. W tej tabeli mogą być przydatne w debugowaniu problemów toojob pokrewne błędy w klastrach HDInsight.

nazwy plików tabeli Hello są **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**.

Te tabele zawiera hello następujące pola:

* ClusterDnsName
* NazwaSkładnika
* eventTimestamp
* Host
* MALoggingHash
* Komunikat
* N
* PreciseTimeStamp
* Rola
* RowIndex
* Dzierżawy
* ZNACZNIK CZASU
* TraceLevel

### <a name="tools-for-accessing-hello-logs"></a>Narzędzia do uzyskiwania dostępu do dzienników hello
Brak dostępnych wiele narzędzi do uzyskiwania dostępu do danych w tych tabelach:

* Visual Studio
* Eksplorator usługi Azure Storage
* Dodatek Power Query dla programu Excel

#### <a name="use-power-query-for-excel"></a>Użyj dodatku Power Query dla programu Excel
Dodatek Power Query mogą być instalowane z [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379). Zobacz hello pobierania strony hello wymagania systemowe

**tooopen dodatku Power Query toouse i analizować hello logowania do usługi**

1. Otwórz **programu Microsoft Excel**.
2. Z hello **dodatku Power Query** menu, kliknij przycisk **Azure z**, a następnie kliknij przycisk **z Microsoft Azure Table storage**.
   
    ![HDInsight Hadoop Excel PowerQuery otworzyć magazynu tabel Azure](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. Wprowadź nazwę konta magazynu hello. Może to być hello krótką nazwę lub hello nazwy FQDN.
4. Wprowadź klucz konta magazynu hello. Zostanie wyświetlona lista tabel:
   
    ![HDInsight Hadoop dzienników przechowywanych w magazynie tabel platformy Azure](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. Kliknij prawym przyciskiem myszy hello hadoopservicelog tabeli w hello **Nawigator** okienka, a następnie wybierz **Edytuj**. Zostanie wyświetlona 4 kolumny. Opcjonalnie można usunąć hello **klucza partycji**, **klucz wiersza**, i **sygnatury czasowej** kolumn, wybierając je, a następnie klikając **Usuń kolumny** Opcje hello hello Wstążce.
6. Powitania kliknij ikonę na powitania rozwiń kolumny toochoose hello kolumn tooimport w arkuszu programu Excel hello zawartości. Dla tego pokazu wybrano TraceLevel i NazwaSkładnika: ją zapewnić mnie kilku podstawowych informacji, na którym składników ma problemy.
   
    ![Dzienniki usługi Hadoop w HDInsight Wybieranie kolumn](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. Kliknij przycisk **OK** tooimport hello danych.
8. Wybierz hello **TraceLevel**, roli i **NazwaSkładnika** kolumny, a następnie kliknij przycisk **Group By** formantu hello Wstążce.
9. Kliknij przycisk **OK** w hello Group By — okno dialogowe
10. Kliknij przycisk ** zastosować & Zamknij **.

W razie potrzeby można teraz używać toofilter programu Excel i sortowanie. Oczywiście można tooinclude innych kolumn (np. wiadomości) w kolejności toodrill w dół do problemy występują, ale zaznaczanie i grupowanie kolumn hello opisane powyżej zapewnia zadowalający obraz, co się dzieje z usługi Hadoop. Witaj informacje o tym samym może być zastosowane toohello setuplog i hadoopinstalllog tabeli.

#### <a name="use-visual-studio"></a>Korzystanie z programu Visual Studio
**toouse programu Visual Studio**

1. Otwórz program Visual Studio.
2. Z hello **widoku** menu, kliknij przycisk **Eksplorator chmury**. Lub po prostu kliknij **CTRL +\, CTRL + X**.
3. Z **Eksplorator chmury**, wybierz pozycję **typów zasobów**.  Witaj innych dostępną opcją jest **grup zasobów**.
4. Rozwiń węzeł **kont magazynu**, hello domyślne konto magazynu dla klastra, a następnie **tabel**.
5. Kliknij dwukrotnie **hadoopservicelog**.
6. Dodaj filtr. Na przykład:
   
        TraceLevel eq 'ERROR'
   
    ![Dzienniki usługi Hadoop w HDInsight Wybieranie kolumn](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    Aby uzyskać więcej informacji na temat tworzenia filtrów, zobacz [utworzenia filtru ciągów hello projektanta tabel](../vs-azure-tools-table-designer-construct-filter-strings.md).

## <a name="logs-written-tooazure-blob-storage"></a>Dzienniki Written tooAzure magazynu obiektów Blob
[Hello rejestruje tabel napisane tooAzure](#log-written-to-azure-tables) zapewnia jeden poziom wgląd w działania wykonywane z klastrem usługi HDInsight. Jednak te tabele nie udostępniają dzienniki poziomie zadania, które mogą być pomocne w przechodzenia na wyższy poziom na problemy podczas występowania. tooprovide to następny poziom szczegółów, HDInsight klastry są skonfigurowane toowrite konta magazynu obiektów Blob tooyour dzienników zadań dla dowolnego zadania, który jest przesyłany przez Templeton. W praktyce oznacza to zadania przesłane za pomocą poleceń cmdlet programu PowerShell usługi Microsoft Azure hello lub hello API przesyłania zadania .NET, nie zadania przesłane za pośrednictwem protokołu RDP/polecenia-wiersza toohello klastra dostępu. 

Zobacz dzienniki hello tooview, [logowania YARN dostęp do aplikacji opartych na systemie Linux usługi HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md).

Aby uzyskać więcej informacji o dziennikach aplikacji, zobacz [uproszczenie zarządzania logowania użytkownika i dostępu w YARN](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/).

## <a name="view-cluster-health-and-job-logs"></a>Wyświetl dzienniki klastra kondycji i zadania
### <a name="access-hadoop-ui"></a>Dostęp do interfejsu użytkownika platformy Hadoop
Witaj portalu Azure kliknij bloku HDInsight klastra Nazwa tooopen hello klastra. W bloku klastra powitania kliknij **pulpitu nawigacyjnego**.

![Uruchomienie klastra pulpitu nawigacyjnego](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

Po wyświetleniu monitu wprowadź poświadczenia administratora klastra hello. W konsoli zapytania, którego kliknięcie spowoduje otwarcie hello, kliknij przycisk **interfejsu użytkownika Hadoop**.

![Uruchom interfejs użytkownika platformy Hadoop](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-hello-yarn-ui"></a>Witaj dostępu Yarn interfejsu użytkownika
Witaj portalu Azure kliknij bloku HDInsight klastra Nazwa tooopen hello klastra. W bloku klastra powitania kliknij **pulpitu nawigacyjnego**. Po wyświetleniu monitu wprowadź poświadczenia administratora klastra hello. W konsoli zapytania, którego kliknięcie spowoduje otwarcie hello, kliknij przycisk **interfejsie użytkownika YARN**.

Program hello interfejsie użytkownika YARN toodo hello poniżej:

* **Pobierz stan klastra**. W okienku po lewej stronie powitania, rozwiń węzeł **klastra**i kliknij przycisk **o**. Obecnie ten klaster Szczegóły stanu, takie jak Suma przydzielonej pamięci, użyto, rdzeni stanu Menedżera zasobów klastra hello, klaster wersji itp.
  
    ![Uruchomienie klastra pulpitu nawigacyjnego](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* **Pobierz stan węzła**. W okienku po lewej stronie powitania, rozwiń węzeł **klastra**i kliknij przycisk **węzłów**. Ta lista zawiera wszystkie węzły hello w klastrze hello, adres HTTP każdego węzła, węzeł tooeach przydzielone zasoby itd.
* **Monitorowanie stanu zadania**. W okienku po lewej stronie powitania, rozwiń węzeł **klastra**, a następnie kliknij przycisk **aplikacji** toolist hello wszystkich zadań w klastrze hello. Jeśli chcesz, aby toolook na zadań w określonej stanu (np. uruchamianie nowego, przesłane, itp.), kliknij odpowiednie łącze hello w obszarze **aplikacji**. Po kliknięciu dalsze toofind nazwę zadania hello więcej informacji na temat hello zadania takie tym hello danych wyjściowych dzienników, itp.

### <a name="access-hello-hbase-ui"></a>Witaj dostępu do bazy danych HBase interfejsu użytkownika
Witaj portalu Azure kliknij bloku HDInsight HBase klastra Nazwa tooopen hello klastra. W bloku klastra powitania kliknij **pulpitu nawigacyjnego**. Po wyświetleniu monitu wprowadź poświadczenia administratora klastra hello. W konsoli zapytania, którego kliknięcie spowoduje otwarcie hello, kliknij przycisk **interfejsu użytkownika bazy danych HBase**.

## <a name="hdinsight-error-codes"></a>Kody błędów HDInsight
Witaj komunikaty o błędach wymienione w tej sekcji znajdują się użytkownicy hello toohelp platformy Hadoop w usłudze Azure HDInsight poznać możliwe błędy napotykane przez nich można podczas administrowania usługą hello przy użyciu programu Azure PowerShell i tooadvise ich na powitania kroki który może zostać pobrany toorecover hello błędu.

Niektóre z tych komunikaty o błędach można także znaleźć w hello portalu Azure po toomanage używanych w usłudze hdinsight. Inne komunikaty o błędach mogą wystąpić, ale jest mniej szczegółowe ze względu na ograniczenia toohello hello czynności zaradczych możliwe w tym kontekście. Inne komunikaty o błędach są zawarte w kontekstach hello hello środki zaradcze w przypadku oczywiste. 

### <a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided
* **Opis elementu**: Podaj szczegóły bazy danych Azure SQL dla co najmniej jeden składnik w kolejności toouse ustawienia niestandardowe dotyczące gałęzi i Oozie magazyny.
* **Środki zaradcze**: hello użytkownik powinien toosupply prawidłowemu żądaniu hello SQL Azure potrzeby magazynu metadanych i spróbuj ponownie.  

### <a id="AzureRegionNotSupported"></a>AzureRegionNotSupported
* **Opis elementu**: nie można utworzyć klastra w regionie *nameOfYourRegion*. Nieprawidłowy region usługi HDInsight przy użyciu, a następnie ponów żądanie.
* **Środki zaradcze**: klienta należy utworzyć hello regionu klastra, który obsługuje obecnie: Azja południowo-wschodnia, Europa Zachodnia, Europa Północna, wschodnie stany USA lub zachodnie stany USA.  

### <a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound
* **Opis**: nie można odnaleźć serwera hello hello żądanego rekordu klastra.  
* **Środki zaradcze**: ponów próbę wykonania operacji hello.

### <a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord
* **Opis elementu**: nazwa DNS klastra *yourDnsName* jest nieprawidłowy. Sprawdź, czy nazwa rozpoczyna się i kończy się wyrazem alfanumerycznego i może zawierać tylko "-" znaki specjalne  
* **Środki zaradcze**: Upewnij się, że używasz prawidłowej nazwy DNS dla klastra, który rozpoczyna się i kończy się wyrazem alfanumeryczne zawiera żadnych specjalnych znaki inne niż hello dash "-", a następnie ponów próbę wykonania operacji hello.

### <a id="ClusterNameUnavailable"></a>ClusterNameUnavailable
* **Opis elementu**: Nazwa klastra *yourClusterName* jest niedostępny. Wybierz inną nazwę.  
* **Środki zaradcze**: hello użytkownik powinien Określ NazwaKlastra, która jest unikatowa i nie istnieje i spróbuj ponownie. Jeśli użytkownik hello używa hello portalu, powitalne interfejsu użytkownika będzie powiadamiać użytkowników, jeśli nazwa klastra jest już używana podczas hello Utwórz kroki.

### <a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid
* **Opis elementu**: hasło klastra jest nieprawidłowe. Hasło musi zawierać co najmniej 10 znaków i musi zawierać co najmniej jedną cyfrę, wielką literę, małą literę i znak specjalny nie może zawierać spacji i nie może zawierać nazwy użytkownika hello jako część.  
* **Środki zaradcze**: Podaj hasło prawidłowym klastrem i ponów próbę wykonania operacji hello.

### <a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid
* **Opis elementu**: nazwa użytkownika klastra jest nieprawidłowy. Upewnij się, że nazwa użytkownika nie zawiera znaków specjalnych ani spacji.  
* **Środki zaradcze**: Podaj nazwę użytkownika z prawidłowym klastrem i ponów próbę wykonania operacji hello.

### <a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord
* **Opis elementu**: nazwa DNS klastra *yourDnsClusterName* jest nieprawidłowy. Sprawdź, czy nazwa rozpoczyna się i kończy się wyrazem alfanumerycznego i może zawierać tylko "-" znaki specjalne  
* **Środki zaradcze**: Podaj prawidłową nazwę klastra DNS użytkownika i ponów próbę wykonania operacji hello.

### <a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName
* **Opis elementu**: nazwa kontenera w identyfikatorze URI *yourcontainerURI* i nazwa DNS *yourDnsName* w żądaniu musi hello treści takie same.  
* **Środki zaradcze**: Upewnij się, że Twoje nazwa kontenera i nazwy DNS są takie same hello i ponów próbę wykonania operacji hello.

### <a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound
* **Opis elementu**: Konfiguracja klastra nieprawidłowy. Nie można toofind żadnych danych definicji węzeł w węźle rozmiar.  
* **Środki zaradcze**: ponów próbę wykonania operacji hello.

### <a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure
* **Opis elementu**: usunięcie wdrożenia nie powiodło się dla hello klastra  
* **Środki zaradcze**: wykonaj ponownie operację usuwania hello.

### <a id="DnsMappingNotFound"></a>DnsMappingNotFound
* **Opis elementu**: błąd konfiguracji usługi. Nie można odnaleźć wymaganych informacji mapowanie DNS.  
* **Środki zaradcze**: Usuwanie klastra i utworzenie nowego klastra.

### <a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest
* **Opis elementu**: zduplikowana próba utworzenia kontenera klastra. Istnieje rekord dla *nameOfYourContainer* , ale nie są zgodne elementy ETag.
* **Środki zaradcze**: Podaj unikatową nazwę dla kontenera hello i ponów próbę hello operacji tworzenia.

### <a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService
* **Opis elementu**: Usługa hostowana *nameOfYourHostedService* zawiera już klastra. Usługa hostowana nie może zawierać wielu klastrów  
* **Środki zaradcze**: klastra hostów hello z innej usługi hostowanej.

### <a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus
* **Opis elementu**: hello serwera nie może zaktualizować stanu hello hello wdrażania klastra.  
* **Środki zaradcze**: ponów próbę wykonania operacji hello. Jeśli występuje wiele razy, skontaktuj się z CSS.

### <a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered
* **Opis elementu**: klastra *yourClusterName* została usunięta w ramach obsługi. Utwórz ponownie hello klastra.
* **Środki zaradcze**: ponownie utwórz hello klastra.

### <a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound
* **Opis elementu**: Konfiguracja klastra nieprawidłowy. Nie można znaleźć w węźle rozmiary konfiguracji wymaganego węzła głównego.
* **Środki zaradcze**: ponów próbę wykonania operacji hello.

### <a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure
* **Opis elementu**: usługi hostowanej toocreate *nameOfYourHostedService*. Ponów żądanie.  
* **Środki zaradcze**: Żądanie hello ponów próbę.

### <a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment
* **Opis elementu**: usługi hostowanej *nameOfYourHostedService* ma już wdrożenia produkcyjnego. Usługa hostowana nie może zawierać wielu wdrożeń produkcyjnych. Ponów żądanie hello z inną nazwę klastra.
* **Środki zaradcze**: Wybierz inną nazwę klastra i wykonaj ponownie hello żądania.

### <a id="HostedServiceNotFound"></a>HostedServiceNotFound
* **Opis elementu**: usługi hostowanej *nameOfYourHostedService* dla nie można znaleźć hello klastra.  
* **Środki zaradcze**: Jeśli klaster hello jest w stanie błędu, usuń go, a następnie spróbuj ponownie.

### <a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment
* **Opis elementu**: usługi hostowanej *nameOfYourHostedService* ma nie skojarzonego wdrożenia.  
* **Środki zaradcze**: Jeśli klaster hello jest w stanie błędu, usuń go, a następnie spróbuj ponownie.

### <a id="InsufficientResourcesCores"></a>InsufficientResourcesCores
* **Opis elementu**: hello SubscriptionId *yourSubscriptionId* nie ma klastra po lewej stronie toocreate rdzeni *yourClusterName*. Wymagane: *resourcesRequired*, dostępne: *resourcesAvailable*.  
* **Środki zaradcze**: zwolnić zasoby w ramach subskrypcji lub zwiększyć liczbę subskrypcji toohello dostępne zasoby hello i ponów toocreate hello klastra.

### <a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices
* **Opis elementu**: identyfikator subskrypcji *yourSubscriptionId* nie ma limitu przydziału dla nowego klastra usługi hostowanej toocreate *yourClusterName*.  
* **Środki zaradcze**: zwolnić zasoby w ramach subskrypcji lub zwiększyć liczbę subskrypcji toohello dostępne zasoby hello i ponów toocreate hello klastra.

### <a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest
* **Opis elementu**: hello serwer napotkał błąd wewnętrzny. Ponów żądanie.  
* **Środki zaradcze**: Żądanie hello ponów próbę.

### <a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation
* **Opis elementu**: lokalizacja magazynu Azure *dataRegionName* nie jest prawidłową lokalizacją. Upewnij się, że hello region jest poprawny i ponów żądanie.
* **Środki zaradcze**: Wybierz lokalizację magazynu, który obsługuje HDInsight, sprawdź, czy klaster wspólnie i ponów próbę wykonania operacji hello.

### <a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode
* **Opis elementu**: rozmiar nieprawidłowy maszyny Wirtualnej dla węzły danych. Tylko rozmiar "Dużych maszyna wirtualna" jest obsługiwany dla wszystkich węzłów danych.  
* **Środki zaradcze**: Określ rozmiar węzła hello obsługiwane hello węzeł danych i ponów próbę wykonania operacji hello.

### <a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode
* **Opis elementu**: rozmiar nieprawidłowy maszyny Wirtualnej dla węzła głównego. Tylko rozmiar "ExtraLarge maszyna wirtualna" jest obsługiwana dla węzła głównego.  
* **Środki zaradcze**: Określ rozmiar węzła hello obsługiwana dla węzła głównego hello i ponów próbę wykonania operacji hello

### <a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion
* **Opis elementu**: identyfikator subskrypcji *yourSubscriptionId* używany nie ma wystarczających uprawnień tooexecute operacji usuwania dla klastra *yourClusterName*.  
* **Środki zaradcze**: Jeśli klaster hello jest w stanie błędu, Porzuć go, a następnie spróbuj ponownie.  

### <a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName
* **Opis elementu**: nazwa kontenera obiektów blob konta magazynu zewnętrznego *yourContainerName* jest nieprawidłowy. Upewnij się, że nazwa rozpoczyna się od litery i zawiera tylko małe litery, cyfry i łączniki.  
* **Środki zaradcze**: Podaj prawidłową nazwę konta magazynu obiektów blob kontenera i ponów próbę wykonania operacji hello.

### <a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey
* **Opis**: Konfiguracja dla konta magazynu zewnętrznego *yourStorageAccountName* jest wymagane toohave szczegółów klucza tajnego toobe zestawu.  
* **Środki zaradcze**: Określ prawidłowy klucz tajny dla konta magazynu hello i ponów próbę wykonania operacji hello.

### <a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat
* **Opis elementu**: nagłówek wersji *yourVersionHeader* nie jest w nieprawidłowym formacie rrrr mm-dd.  
* **Środki zaradcze**: Określ prawidłowy format dla nagłówka wersji hello i ponów żądanie hello.

### <a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode
* **Opis elementu**: Konfiguracja klastra nieprawidłowy. Znaleziono więcej niż jedną konfigurację węzła głównego.  
* **Środki zaradcze**: Edycja hello konfiguracji tak określono tylko jeden węzeł head.

### <a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest
* **Opis elementu**: nie można ukończyć operacji hello w ramach dozwolone czasu hello lub hello maksymalną liczbę ponownych prób to możliwe. Ponów żądanie.  
* **Środki zaradcze**: Żądanie hello ponów próbę.

### <a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty
* **Opis elementu**: parametr *yourParameterName* nie może mieć wartości null ani być pusta.  
* **Środki zaradcze**: Określ prawidłową wartość dla parametru hello.

### <a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure
* **Opis elementu**: co najmniej jeden hello klastra tworzenia żądania w danych wejściowych jest nieprawidłowa. Upewnij się, hello wartości wejściowe są poprawne i ponów żądanie.  
* **Środki zaradcze**: Upewnij się, że hello wartości wejściowe są poprawne i ponów żądanie.

### <a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable
* **Opis elementu**: możliwości Region nie jest dostępna dla regionu *yourRegionName* i identyfikator subskrypcji *yourSubscriptionId*.  
* **Środki zaradcze**: Określ region, który obsługuje klastry usługi HDInsight. Witaj publicznie obsługiwane regiony to: Azja południowo-wschodnia, Europa Zachodnia, Europa Północna, wschodnie stany USA lub zachodnie stany USA.

### <a id="StorageAccountNotColocated"></a>StorageAccountNotColocated
* **Opis elementu**: Konto magazynu *yourStorageAccountName* znajduje się w regionie *currentRegionName*. Powinien być taki sam jak region klastra hello *yourClusterRegionName*.  
* **Środki zaradcze**: Określ konto magazynu w hello na tym samym regionie, który znajduje się w klastrze lub jeśli dane są już na koncie magazynu hello, Utwórz nowy klaster w hello tego samego regionu hello istniejącego konta magazynu. Jeśli używasz portalu hello hello interfejsu użytkownika będzie powiadamiać użytkowników, tego problemu z wyprzedzeniem.

### <a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive
* **Opis elementu**: podany identyfikator subskrypcji *yourSubscriptionId* nie jest aktywny.  
* **Środki zaradcze**: ponownie aktywować subskrypcję lub pobrać nowe prawidłowej subskrypcji.

### <a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound
* **Opis elementu**: identyfikator subskrypcji *yourSubscriptionId* nie można odnaleźć.  
* **Środki zaradcze**: Sprawdź, czy identyfikator subskrypcji jest prawidłowy i ponów próbę wykonania operacji hello.

### <a id="UnableToResolveDNS"></a>UnableToResolveDNS
* **Opis elementu**: nie można tooresolve DNS *yourDnsUrl*. Sprawdź, czy hello w pełni kwalifikowany adres URL dla punktu końcowego obiektu blob hello jest dostępne.  
* **Środki zaradcze**: Podaj adres URL nieprawidłowy obiekt blob. Hello adres URL musi być pełni prawidłową, w tym począwszy *http://* i kończący się w *.com*.

### <a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource
* **Opis elementu**: tooverify lokalizację zasobu *yourDnsUrl*. Sprawdź, czy hello w pełni kwalifikowany adres URL dla punktu końcowego obiektu blob hello jest dostępne.  
* **Środki zaradcze**: Podaj adres URL nieprawidłowy obiekt blob. Hello adres URL musi być pełni prawidłową, w tym począwszy *http://* i kończący się w *.com*.

### <a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable
* **Opis elementu**: możliwości wersji nie jest dostępna dla wersji *specifiedVersion* i identyfikator subskrypcji *yourSubscriptionId*.  
* **Środki zaradcze**: Wybierz wersję, która jest dostępna i ponów próbę wykonania operacji hello.

### <a id="VersionNotSupported"></a>VersionNotSupported
* **Opis elementu**: wersja *specifiedVersion* nie jest obsługiwane.
* **Środki zaradcze**: Wybierz obsługiwaną wersję i ponów próbę wykonania operacji hello.

### <a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion
* **Opis elementu**: wersja *specifiedVersion* nie jest dostępna w regionie Azure *specifiedRegion*.  
* **Środki zaradcze**: Wybierz wersję, który jest obsługiwany w regionie hello określony i ponów próbę wykonania operacji hello.

### <a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound
* **Opis elementu**: Konfiguracja klastra nieprawidłowy. Nie można odnaleźć w kont zewnętrznych wymaganej konfiguracji konta WASB.  
* **Środki zaradcze**: Sprawdź, czy konto hello istnieje i jest poprawnie określona w konfiguracji i ponów próbę wykonania operacji hello.

## <a name="next-steps"></a>Następne kroki
* [Użyj widoków Ambari toodebug Tez zadania w usłudze HDInsight](hdinsight-debug-ambari-tez-view.md)
* [Włącz zrzuty stosu dla usługi Hadoop w HDInsight opartych na systemie Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [Zarządzanie klastrami usługi HDInsight za pomocą hello Interfejsu sieci Web Ambari](hdinsight-hadoop-manage-ambari.md)

