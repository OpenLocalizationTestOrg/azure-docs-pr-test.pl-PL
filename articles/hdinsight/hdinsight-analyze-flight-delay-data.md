---
title: "aaaAnalyze transmitowane opóźnienie danych z platformą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse jednego środowiska Windows PowerShell skryptu toocreate klastra usługi HDInsight, uruchom zadania Hive, uruchom zadanie Sqoop, a następnie usuń hello klastra."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a>Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight
Gałąź umożliwia uruchomionych zadań MapReduce z Hadoop za pomocą skryptów języka przypominającego SQL o nazwie  *[HiveQL][hadoop-hiveql]*, które można zastosować do podsumowania, wyszukiwanie i analizowania dużych ilości danych.

> [!IMPORTANT]
> Witaj czynności w tym dokumencie wymagają klastra usługi HDInsight opartej na systemie Windows. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows). Opis czynności, które pracy z opartą na systemie Linux klastrem, zobacz [analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).

Jedną z najważniejszych zalet hello Azure HDInsight jest oddzielenie hello magazynu danych i zasobów obliczeniowych. HDInsight używa magazynu obiektów Blob platformy Azure do przechowywania danych. Typowe zadania obejmuje trzy części:

1. **Przechowywanie danych w magazynie obiektów Blob Azure.**  Na przykład pogodowe danych czujnika, danych, dzienników sieci web, a w tym przypadku transmitowane opóźnienie danych są zapisywane w magazynie obiektów Blob Azure.
2. **Uruchamianie zadań.** Gdy nadejdzie czas tooprocess hello danych, uruchom skrypt programu Windows PowerShell (lub aplikacja kliencka) toocreate klastra usługi HDInsight, uruchamianie zadań, a następnie usuń hello klastra. Witaj zadania zapisywania wyjściowych danych tooAzure magazynu obiektów Blob. dane wyjściowe Hello jest zachowywana, nawet po usunięciu hello klastra. W ten sposób płacisz za tylko co użytkownik ma używane.
3. **Pobrać dane wyjściowe hello z magazynu obiektów Blob Azure**, lub w tym samouczku eksportu hello danych tooan — bazy danych Azure SQL.

Witaj poniższym diagramie przedstawiono scenariusz hello i struktura hello tego samouczka:

![HDI. FlightDelays.flow][img-hdi-flightdelays-flow]

Należy pamiętać, że numery hello na diagramie hello odpowiadają toohello tytuły sekcji. **M** oznacza hello głównego procesu. **A** oznacza zawartość hello hello dodatku.

Hello głównych części samouczka hello pokazuje, jak toouse jednego środowiska Windows PowerShell skryptu tooperform hello następujące zadania:

* Tworzenie klastra usługi HDInsight.
* Uruchom zadanie Hive hello klastra toocalculate średnie opóźnienia na lotniskach. Witaj transmitowane opóźnienie dane są przechowywane na koncie magazynu obiektów Blob platformy Azure.
* Uruchom Sqoop zadania tooexport hello Hive zadania dane wyjściowe tooan bazy danych Azure SQL.
* Usuń hello klastra usługi HDInsight.

W dodatkach hello hello instrukcje można znaleźć przekazywanie danych opóźnienie transmitowane, ciąg zapytania Hive tworzenia/przekazywania i przygotowywanie bazy danych Azure SQL hello hello Sqoop zadania.

> [!NOTE]
> kroki Hello w tym dokumencie są określonej na podstawie tooWindows klastrów usługi HDInsight. Opis czynności, które pracy z opartą na systemie Linux klastrem, zobacz [analizowanie danych opóźnienie transmitowane przy użyciu Hive w usłudze HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)

### <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka, musi mieć hello następujące elementy:

* **Subskrypcja platformy Azure**. Zobacz artykuł [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Stacja robocza z programem Azure PowerShell**.

    > [!IMPORTANT]
    > Obsługa programu Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i została usunięta z dniem 1 stycznia 2017 r. Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.
    >
    > Wykonaj kroki hello [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello najnowszą wersję programu Azure PowerShell. Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) Aby uzyskać więcej informacji.

**Pliki używane w tym samouczku**

W tym samouczku używana hello punktualności linii lotniczych dane transmitowane z [badań i innowacyjnych administracyjnej technologii, biura statystyk transportu lub RICIE][rita-website].
Kopię powitalne dane zostały przekazane tooan kontenera magazynu obiektów Blob platformy Azure z uprawnieniem dostępu publicznego obiektu Blob hello.
Część skrypt programu PowerShell kopiuje dane hello z hello publicznych obiektów blob kontenera toohello domyślnego kontenera obiektów blob klastra. Hello HiveQL skryptu jest również skopiować toohello tego samego kontenera obiektów Blob.
Jeśli chcesz, aby toolearn jak tooget/przekazywania hello danych tooyour właścicielem konta magazynu i jak hello toocreate/przekazywania HiveQL skryptu plików, zobacz [dodatek a.](#appendix-a) i [dodatek B](#appendix-b).

Witaj poniższej tabeli wymieniono pliki hello używane w tym samouczku:

<table border="1">
<tr><th>Pliki</th><th>Opis</th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td>plik skryptu HiveQL Hello używany przez hello zadania Hive. Ten skrypt został przekazany tooan konta magazynu obiektów Blob Azure o dostępie hello. <a href="#appendix-b">Dodatek B</a> zawiera instrukcje dotyczące przygotowania i przekazywanie tego pliku tooyour własnych Azure konta magazynu obiektów Blob.</td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td>Dane wejściowe dla zadania Hive hello. Witaj dane zostały przekazane tooan konta magazynu obiektów Blob Azure o dostępie hello. <a href="#appendix-a">Dodatek a.</a> zawiera instrukcje dotyczące pobierania danych hello i przekazać hello danych tooyour własnych Azure konta magazynu obiektów Blob.</td></tr>
<tr><td>\tutorials\flightdelays\output</td><td>Ścieżka wyjściowa Hello hello zadania Hive. Kontener domyślny Hello jest używany do przechowywania danych wyjściowych hello.</td></tr>
<tr><td>\tutorials\flightdelays\jobstatus</td><td>Witaj Hive zadania stanu folder hello domyślnego kontenera.</td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a>Tworzenie klastra i uruchamianie zadania Hive/Sqoop
MapReduce z Hadoop jest przetwarzanie wsadowe. Hello większości toorun ekonomiczny sposób zadania Hive jest toocreate klastra hello zadania i usunąć hello zadania po zakończeniu zadania hello. Witaj poniższy skrypt obejmuje hello całego procesu.
Aby uzyskać więcej informacji na temat tworzenia klastra usługi HDInsight i uruchamiania zadań Hive, zobacz [klastrów utworzyć Hadoop w usłudze HDInsight] [ hdinsight-provision] i [używanie Hive z usługą HDInsight][hdinsight-use-hive].

**zapytań programu Hive hello toorun przez programu Azure PowerShell**

1. Tworzenie za pomocą instrukcji hello w tabeli bazy danych i hello Azure SQL dla danych wyjściowych zadania Sqoop hello [dodatku C](#appendix-c).
2. Otwórz program Windows PowerShell ISE, a następnie uruchom hello następującego skryptu:

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. Połączenia bazy danych SQL tooyour i zobacz opóźnienia średni transmitowane przez miasto tabeli AvgDelays hello:

    ![HDI. FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <a id="appendix-a"></a>Dodatek A - przekazywania transmitowane opóźnienie danych tooAzure magazynu obiektów Blob
Przekazywanie hello plików danych i plików skryptów HiveQL hello (zobacz [dodatek B](#appendix-b)) wymaga niektórych planowania. pomysł Hello jest toostore hello danych plików i plików HiveQL hello przed utworzeniem klastra usługi HDInsight i uruchamiania zadania Hive hello. Dostępne są dwie opcje:

* **Użyj hello samo konto magazynu Azure, które będą używane przez klaster usługi HDInsight hello jako hello domyślnego systemu plików.** Ponieważ klaster usługi HDInsight hello będzie mieć klucz dostępu do konta magazynu hello, nie potrzebujesz toomake dodatkowe zmiany.
* **Użyj innego konta magazynu Azure z hello klastra usługi HDInsight domyślnego systemu plików.** Jeśli hello tak jest, należy zmodyfikować hello tworzenia część hello skrypt znalezione w programie Windows PowerShell [klaster tworzenia usługi HDInsight i uruchamiania zadań Hive/Sqoop](#runjob) toolink hello konta magazynu jako dodatkowe konta magazynu. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Hadoop w usłudze HDInsight][hdinsight-provision]. klaster usługi HDInsight Hello wie, następnie hello klucza dostępu dla konta magazynu hello.

> [!NOTE]
> Witaj ścieżki do magazynu obiektów Blob dla pliku danych jest trudna kodowanych w pliku skryptu HiveQL hello powitalne. Należy zaktualizować go odpowiednio.

**dane transmitowane hello toodownload**

1. Przeglądaj zbyt[badań i innowacyjnych technologii administracji, biura statystyk transportu][rita-website].
2. Na stronie powitania wybierz hello następujące wartości:

    <table border="1">
    <tr><th>Nazwa</th><th>Wartość</th></tr>
    <tr><td>Filtr roku</td><td>2013 </td></tr>
    <tr><td>Filtruj okres</td><td>Stycznia</td></tr>
    <tr><td>Pola</td><td>*Rok*, *FlightDate*, *UniqueCarrier*, *operatora*, *FlightNum*, *OriginAirportID*, *pochodzenia*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*,  *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (Usuń zaznaczenie wszystkich innych pól)</td></tr>
    </table>
3.Kliknij przycisk **Pobierz**.
4. Rozpakuj hello pliku toohello **C:\Tutorials\FlightDelay\2013Data** folderu. Każdy plik jest plikiem CSV i jest rozmiar około 60GB.
5. Zmień nazwę toohello pliku hello hello miesiąca, który zawiera dane dla. Na przykład, czy nazwany hello pliku zawierającego dane stycznia hello *January.csv*.
6. Powtórz kroki 2 i 5 toodownload pliku dla każdego hello 12 miesięcy w 2013. Konieczne będzie co najmniej jednego pliku toorun hello samouczka.

**tooupload hello transmitowane opóźnienie danych tooAzure magazynu obiektów Blob**

1. Przygotowanie hello parametrów:

    <table border="1">
    <tr><th>Nazwa zmiennej</th><th>Uwagi</th></tr>
    <tr><td>$storageAccountName</td><td>Witaj miejscu tooupload hello danych do konta usługi Magazyn Azure.</td></tr>
    <tr><td>$blobContainerName</td><td>Witaj, w którym ma tooupload hello danych do kontenera obiektów Blob.</td></tr>
    </table>
2. Otwórz program Azure PowerShell ISE.
3. Wklej hello następującego skryptu w okienku skryptów hello:

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. Naciśnij klawisz **F5** toorun hello skryptu.

Jeśli wybierzesz toouse inną metodę przekazywania plików hello, upewnij się, czy ścieżka pliku hello jest samouczki/flightdelay/danych. Składnia Hello dla uzyskiwania dostępu do plików hello jest następująca:

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

Ścieżka Hello samouczki/flightdelay/dane są hello wirtualny utworzony folder po przekazaniu plików hello. Sprawdź, czy pliki 12, po jednej dla każdego miesiąca.

> [!NOTE]
> Należy zaktualizować tooread zapytania Hive hello z hello nowej lokalizacji.
>
> Należy skonfigurować hello kontenera dostępu uprawnienia toobe publicznego lub powiązać toohello konta magazynu hello klastra usługi HDInsight. W przeciwnym razie wartość ciągu zapytania Hive hello nie będą mogli tooaccess hello danych plików.

- - -

## <a id="appendix-b"></a>Dodatek B — tworzenie i przekazywanie skrypt HiveQL
Przy użyciu programu Azure PowerShell, można uruchomić wiele instrukcje HiveQL co w czasie, lub pakietu hello instrukcji HiveQL do pliku skryptu. W tej sekcji przedstawiono, jak toocreate skrypt HiveQL i przekazywania hello skryptu tooAzure magazynu obiektów Blob przy użyciu programu Azure PowerShell. Gałąź wymaga toobe skrypty HiveQL hello przechowywanych w magazynie obiektów Blob platformy Azure.

Witaj skrypt HiveQL zostaną wykonane następujące hello:

1. **Witaj delays_raw tabelę**, w przypadku, gdy tabela hello już istnieje.
2. **Tworzenie tabeli Hive zewnętrznych delays_raw hello** wskazanie lokalizacji magazynu obiektów Blob toohello hello transmitowane opóźnienie plików. To zapytanie określa, czy pola są rozdzielone "," i zakończenia wierszy przy "\n". Stanowi to problem, gdy wartości pól zawierać przecinków, ponieważ gałąź nie może odróżnić przecinkami, która jest ogranicznik pola i jedną, która jest częścią wartość pola (co jest przypadku hello w wartości pól pochodzenia\_MIASTA\_nazwę i DOCELOWY\_ MIASTO\_nazwy). tooaddress hello tego zapytania tworzy TEMP kolumn danych toohold niepoprawnie jest podzielony na kolumny.
3. **Tabelę opóźnienia hello**, w przypadku, gdy tabela hello już istnieje.
4. **Utwórz tabelę opóźnienia hello**. Jest przydatne tooclean zapasowych hello przed dalsze przetwarzanie. To zapytanie tworzy nową tabelę, *opóźnienia*, z tabeli delays_raw hello. Należy pamiętać, że hello TEMP kolumn (jak już wspomniano) nie są kopiowane i że hello **podciąg** funkcji jest używane tooremove cudzysłów hello danych.
5. **Obliczeniowe hello pogody średnie opóźnienie i grup hello wyników przez nazwę miejscowości.** Zostanie również dane wyjściowe hello wyniki tooBlob magazynu. Należy pamiętać, zapytania hello spowoduje usunięcie danych hello apostrofów i które pominie wierszy, gdzie wartość hello **weather_delay** ma wartość null. Jest to konieczne, ponieważ Sqoop, używane w dalszej części tego samouczka nie bezpiecznie obsłużyć te wartości domyślne.

Aby uzyskać pełną listę poleceń HiveQL hello, zobacz [Hive języka definicji danych][hadoop-hiveql]. Każde polecenie HiveQL musi kończyć się średnikiem.

**plik skryptu HiveQL toocreate**

1. Przygotowanie hello parametrów:

    <table border="1">
    <tr><th>Nazwa zmiennej</th><th>Uwagi</th></tr>
    <tr><td>$storageAccountName</td><td>Witaj konta magazynu Azure, gdzie chcesz skrypt HiveQL hello tooupload.</td></tr>
    <tr><td>$blobContainerName</td><td>Witaj, którym chcesz skrypt HiveQL hello tooupload kontenera obiektów Blob.</td></tr>
    </table>
2. Otwórz program Azure PowerShell ISE.
3. Skopiuj i Wklej hello następującego skryptu w okienku skryptów hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    Poniżej przedstawiono hello zmiennych w skrypcie hello:

   * **$hqlLocalFileName** -skryptu hello zapisuje plik skryptu HiveQL hello lokalnie przed przekazaniem go tooBlob magazynu. Jest to nazwa pliku hello. Witaj, wartość domyślna to <u>C:\tutorials\flightdelay\flightdelays.hql</u>.
   * **$hqlBlobName** — jest to hello HiveQL nazwę pliku skryptu obiektów blob używane w hello magazynu obiektów Blob platformy Azure. Wartość domyślna Hello jest tutorials/flightdelay/flightdelays.hql. Ponieważ hello zostanie zapisany plik bezpośrednio tooAzure magazynu obiektów Blob, nie istnieje "/" na początku hello hello nazwa obiektu blob. Jeśli chcesz tooaccess hello pliku z magazynu obiektów Blob, konieczne będzie tooadd "/" na początku hello hello nazwy pliku.
   * **$srcDataFolder** i **$dstDataFolder** -= "data samouczki/flightdelay" = "samouczki flightdelay/wyjściowej"

- - -
## <a id="appendix-c"></a>Dodatek C — przygotowanie bazy danych Azure SQL dla hello Sqoop dane wyjściowe zadania
**Baza danych SQL hello tooprepare (Scal to z hello skryptu Sqoop)**

1. Przygotowanie hello parametrów:

    <table border="1">
    <tr><th>Nazwa zmiennej</th><th>Uwagi</th></tr>
    <tr><td>$sqlDatabaseServerName</td><td>Nazwa serwera bazy danych Azure SQL hello Hello. Wprowadź nic toocreate nowego serwera.</td></tr>
    <tr><td>$sqlDatabaseUsername</td><td>Witaj nazwę logowania dla serwera bazy danych Azure SQL hello. $SqlDatabaseServerName w przypadku istniejącego serwera, używane tooauthenticate z serwerem hello są hello logowania i hasło logowania. W przeciwnym razie są one używane toocreate nowego serwera.</td></tr>
    <tr><td>$sqlDatabasePassword</td><td>Witaj hasło logowania dla serwera bazy danych Azure SQL hello.</td></tr>
    <tr><td>$sqlDatabaseLocation</td><td>Ta wartość jest używana tylko wtedy, gdy tworzysz nowy serwer bazy danych platformy Azure.</td></tr>
    <tr><td>$sqlDatabaseName</td><td>Baza danych SQL Hello używany toocreate hello AvgDelays tabeli dla hello Sqoop zadania. Utworzy bazę danych o nazwie HDISqoop pozostawić je puste. Nazwa tabeli Hello hello Sqoop dane wyjściowe z zadania to AvgDelays. </td></tr>
    </table>
2. Otwórz program Azure PowerShell ISE.
3. Skopiuj i Wklej hello następującego skryptu w okienku skryptów hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > Witaj skrypt używa usługi transfer (REST) representational stanu, http://bot.whatismyipaddress.com, tooretrieve zewnętrzny adres IP. adres IP Hello jest używany do utworzenia reguły zapory dla serwera bazy danych SQL.

    Poniżej przedstawiono niektóre zmienne używane w skrypcie hello:

   * **$ipAddressRestService** -hello wartość domyślna to http://bot.whatismyipaddress.com. Jest on publiczny adres IP usługi REST do pobierania zewnętrzny adres IP. Korzystania z innych usług, jeśli chcesz. Hello pobrane za pośrednictwem usługi hello zewnętrzny adres IP będzie używany toocreate reguły zapory dla serwera bazy danych Azure SQL, aby umożliwić dostęp hello bazy danych ze stacji roboczej (przy użyciu skryptu programu Windows PowerShell).
   * **$fireWallRuleName** — jest to nazwa hello hello reguły zapory dla serwera bazy danych Azure SQL hello. Nazwa domyślnej Hello jest <u>FlightDelay</u>. Można zmienić jego nazwę, jeśli chcesz.
   * **$sqlDatabaseMaxSizeGB** — ta wartość jest używana tylko wtedy, gdy tworzysz nowy serwer bazy danych Azure SQL. Witaj, wartość domyślna to 10GB. 10GB to wystarczający do celów tego samouczka.
   * **$sqlDatabaseName** — ta wartość jest używana tylko wtedy, gdy tworzysz nową bazę danych Azure SQL. Wartość domyślna Hello jest HDISqoop. Jeśli należy zmienić jego nazwę, należy zaktualizować odpowiednio skrypt programu Windows PowerShell Sqoop hello.
4. Naciśnij klawisz **F5** toorun hello skryptu.
5. Sprawdzanie poprawności danych wyjściowych skryptu hello. Upewnij się, że skrypt hello zostało wykonane pomyślnie.

## <a id="nextsteps"></a> Następne kroki
Teraz wiesz, jak tooupload tooAzure pliku magazynu obiektów Blob, w jaki sposób toopopulate gałąź tabeli za pomocą hello danych z magazynu obiektów Blob platformy Azure, jak toorun Hive zapytań i w jaki sposób toouse Sqoop tooexport dane z bazy danych Azure SQL tooan systemu plików HDFS. toolearn więcej, zobacz następujące artykuły hello:

* [Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started]
* [Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]
* [Korzystanie z Oozie z usługą HDInsight][hdinsight-use-oozie]
* [Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]
* [Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]
* [Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-mapreduce]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
