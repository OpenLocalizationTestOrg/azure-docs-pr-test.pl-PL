---
title: "aaaUse oparte na czasie Hadoop Oozie coordinator w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj oparte na czasie koordynatora Hadoop Oozie w usłudze HDInsight, Usługa danych big data. Dowiedz się, jak toodefine Oozie przepływów pracy i koordynatorami i przesyłanie zadań."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a>Używanie na podstawie czasu Oozie coordinator z platformą Hadoop w HDInsight toodefine w przepływach pracy oraz koordynować zadania
W tym artykule dowiesz się, jak toodefine przepływów pracy i koordynatorami i jak tootrigger hello koordynator zadań, na podstawie czasu. Jest przydatne toogo za pośrednictwem [Oozie użycia z usługą HDInsight] [ hdinsight-use-oozie] przed przeczytaniem tego artykułu. Ponadto tooOozie, można również zaplanować zadania przy użyciu fabryki danych Azure. toolearn fabryki danych Azure, zobacz [Use Pig i Hive z fabryką danych](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> W tym artykule wymaga klastra usługi HDInsight opartej na systemie Windows. Dla informacji o korzystaniu z Oozie, w tym zadania na podstawie czasu, w klastrze opartych na systemie Linux, zobacz [Oozie Użyj Hadoop toodefine i Uruchom przepływ pracy na HDInsight opartych na systemie Linux](hdinsight-use-oozie-linux-mac.md)

## <a name="what-is-oozie"></a>Co to jest Oozie
Apache Oozie to system koordynacji/przepływu pracy, który zarządza zadaniami na platformie Hadoop. Jest zintegrowany z hello stosem platformy Hadoop i obsługuje zadania platformy Hadoop dla Apache MapReduce, Apache Pig Apache Hive i Apache Sqoop. Można także używane tooschedule zadania, które są określone tooa systemu, np. programów Java lub skryptów powłoki.

Witaj poniższy obraz przedstawia hello przepływu pracy, który będzie implementowany:

![Diagram przepływu pracy][img-workflow-diagram]

Hello przepływ pracy zawiera dwa działania:

1. Akcja Hive uruchamia hello toocount skrypt HiveQL wystąpień poszczególnych typów poziom dziennika w pliku dziennika log4j. Każdy dziennik log4j składa się z linii pola zawiera [poziom dziennika] pola tooshow hello typu i hello ważność, na przykład:

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    dane wyjściowe skryptu Hive Hello jest podobny do:

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    Aby uzyskać więcej informacji na temat programu Hive, zobacz temat [Use Hive with HDInsight][hdinsight-use-hive] (Korzystanie z programu Hive z usługą HDInsight).
2. Akcja Sqoop eksportuje hello HiveQL akcji dane wyjściowe tooa tabeli w bazie danych Azure SQL. Aby uzyskać więcej informacji o Sqoop, zobacz [Sqoop użycia z usługą HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Obsługiwane wersje Oozie w klastrach HDInsight, zobacz [nowości w wersjach klastra hello dostarczanych z usługą HDInsight?] [hdinsight-versions].
>
>

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka wymagane są następujące hello:

* **Stacja robocza z programem Azure PowerShell**.

    > [!IMPORTANT]
    > Obsługa środowiska Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i zostanie usunięta z dniem 1 stycznia 2017 r. Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.
    >
    > Wykonaj kroki hello [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello najnowszą wersję programu Azure PowerShell. Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) Aby uzyskać więcej informacji.

* **Klaster usługi HDInsight**. Aby uzyskać informacje dotyczące tworzenia klastra usługi HDInsight, zobacz [Tworzenie klastrów usługi HDInsight][hdinsight-provision], lub [Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started]. Konieczne będzie powitania po toogo danych samouczkiem hello:

    <table border = "1">
    <tr><th>Właściwości klastra</th><th>Nazwa zmiennej środowiska Windows PowerShell</th><th>Wartość</th><th>Opis</th></tr>
    <tr><td>Nazwa klastra usługi HDInsight</td><td>$clusterName</td><td></td><td>klaster usługi HDInsight Hello, na którym będzie uruchomiona w tym samouczku.</td></tr>
    <tr><td>Nazwa użytkownika klastra usługi HDInsight</td><td>$clusterUsername</td><td></td><td>Nazwa użytkownika klastra usługi HDInsight Hello. </td></tr>
    <tr><td>Hasło użytkownika klastra usługi HDInsight </td><td>$clusterPassword</td><td></td><td>Witaj hasło użytkownika klastra usługi HDInsight.</td></tr>
    <tr><td>Nazwa konta magazynu platformy Azure</td><td>$storageAccountName</td><td></td><td>Klaster usługi HDInsight toohello dostępne konta magazynu Azure. W tym samouczku Użyj hello domyślne konto magazynu, które zostały określone podczas procesu udostępniania klastra hello.</td></tr>
    <tr><td>Nazwa kontenera obiektów Blob platformy Azure</td><td>$containerName</td><td></td><td>Na przykład użyć hello kontenera magazynu obiektów Blob platformy Azure, służący do hello domyślny system plików klastra usługi HDInsight. Domyślnie ma takie same nazwy co klaster usługi HDInsight hello hello.</td></tr>
    </table>
* **Baza danych Azure SQL**. Należy skonfigurować reguły zapory dla hello bazy danych SQL server tooallow dostęp ze stacji roboczej. Aby uzyskać instrukcje dotyczące tworzenia bazy danych Azure SQL i konfigurowania zapory hello, zobacz [rozpocząć korzystanie z bazy danych Azure SQL] [bazadanychsql get-started]. Ten artykuł zawiera skrypt programu Windows PowerShell do tworzenia tabeli bazy danych Azure SQL hello potrzebne w tym samouczku.

    <table border = "1">
    <tr><th>Właściwości bazy danych SQL</th><th>Nazwa zmiennej środowiska Windows PowerShell</th><th>Wartość</th><th>Opis</th></tr>
    <tr><td>Nazwa serwera bazy danych SQL</td><td>$sqlDatabaseServer</td><td></td><td>Witaj SQL bazy danych serwera toowhich Sqoop spowoduje wyeksportowanie danych. </td></tr>
    <tr><td>Nazwa logowania bazy danych SQL</td><td>$sqlDatabaseLogin</td><td></td><td>Nazwa logowania SQL Database.</td></tr>
    <tr><td>Hasło nazwy logowania bazy danych SQL</td><td>$sqlDatabaseLoginPassword</td><td></td><td>Hasło nazwy logowania bazy danych SQL.</td></tr>
    <tr><td>Nazwa bazy danych SQL</td><td>$sqlDatabaseName</td><td></td><td>toowhich bazy danych Azure SQL Hello Sqoop spowoduje wyeksportowanie danych. </td></tr>
    </table>

  > [!NOTE]
  > Domyślnie baza danych Azure SQL zezwala na połączenia z usługami Azure, takimi jak Azure HDInsight. Wyłączenie tego ustawienia zapory, należy włączyć ją z hello portalu Azure. Aby uzyskać instrukcje dotyczące tworzenia bazy danych SQL i konfigurowania reguł zapory, zobacz [tworzenie i Konfigurowanie bazy danych SQL][sqldatabase-get-started].

> [!NOTE]
> Wypełnianie hello wartości w tabelach hello. Jest przydatne w przypadku przechodzenia przez tego samouczka.

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a>Zdefiniuj Oozie przepływu pracy i hello powiązanych skrypt HiveQL
Oozie definicje przepływów pracy są zapisywane w hPDL (XML procesu definition language). Witaj domyślną nazwą pliku przepływu pracy jest *workflow.xml*.  Będzie Zapisz lokalnie plik hello przepływu pracy, a następnie wdrożyć go toohello klastra usługi HDInsight przy użyciu programu Azure PowerShell w dalszej części tego samouczka.

Witaj akcji gałęzi w przepływie pracy hello wywołuje skrypt HiveQL. Ten plik skryptu zawiera trzy instrukcje HiveQL:

1. **Witaj instrukcji DROP TABLE** usuwa hello log4j tabelę programu Hive, jeśli istnieje.
2. **Instrukcja CREATE TABLE Hello** tworzy log4j gałęzi zewnętrznych tabeli, która wskazuje toohello lokalizację pliku dziennika narzędzia log4j hello;
3. **Witaj lokalizację pliku dziennika narzędzia log4j hello**. Ogranicznik pola Hello ",". Ogranicznik wiersza domyślne Hello jest "\n". Gałąź tabeli zewnętrznej jest plik danych hello używane tooavoid usuwana z oryginalnej lokalizacji hello, w przypadku, gdy chcesz przepływu pracy Oozie hello toorun wiele razy.
4. **Witaj instrukcji INSERT zastąpić** liczby wystąpień hello każdego typu poziomu dziennika z hello log4j tabelę programu Hive i zapisuje lokalizacji magazynu obiektów Blob platformy Azure tooan dane wyjściowe hello.

> [!NOTE]
> Jest to znany problem ścieżki gałęzi. Należy uruchomić na ten problem podczas przesyłania zadania Oozie. Witaj instrukcje dla ustalania hello problemu można znaleźć na powitania TechNet Wiki: [HDInsight Hive błąd: toorename][technetwiki-hive-error].

**wywoływane przez przepływ pracy hello toodefine hello HiveQL skryptu pliku toobe**

1. Utwórz plik tekstowy z hello następującej zawartości:

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    Istnieją trzy zmienne używane w skrypcie hello:

   * ${hiveTableName}
   * ${hiveDataFolder}
   * ${hiveOutputFolder}

     Plik definicji przepływu pracy Hello (workflow.xml w tym samouczku) przekazuje te wartości toothis skrypt HiveQL w czasie wykonywania.
2. Zapisz plik hello jako **C:\Tutorials\UseOozie\useooziewf.hql** przy użyciu kodowania ANSI (ASCII). (Użyj Notatnik, jeśli ta opcja nie są dostępne w edytorze tekstów). Ten plik skryptu będzie klastra usługi HDInsight toohello wdrożone później w samouczku hello.

**toodefine przepływu pracy**

1. Utwórz plik tekstowy z hello następującej zawartości:

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    Istnieją dwie akcje zdefiniowane w przepływie pracy hello. jest Hello start-tooaction *RunHiveScript*. Jeśli akcja hello uruchamia *OK*, następnej akcji hello jest *RunSqoopExport*.

    Witaj RunHiveScript ma kilka zmiennych. Po przesłaniu zadania Oozie hello ze stacji roboczej za pomocą programu Azure PowerShell, przechodzą hello wartości.

    Zmienne przepływu pracy

    <table border = "1">
    <tr><th>Zmienne przepływu pracy</th><th>Opis</th></tr>
    <tr><td>${jobTracker}</td><td>Określ adres URL śledzenia zadań Hadoop hello hello. Użyj <strong>jobtrackerhost:9010</strong> w usłudze HDInsight klastra w wersji 3.0 i 2.0.</td></tr>
    <tr><td>${nameNode}</td><td>Określ adres URL hello hello Hadoop nazwa węzła. Użyj hello domyślnego pliku system wasb: / / adresu, na przykład <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</td></tr>
    <tr><td>${queueName}</td><td>Określa, że nazwa kolejki hello hello zadania zostaną przesłane do. Użyj <strong>domyślne</strong>.</td></tr>
    </table>

    Zmienne akcji gałęzi

    <table border = "1">
    <tr><th>Gałąź zmiennej akcji</th><th>Opis</th></tr>
    <tr><td>${hiveDataFolder}</td><td>katalog źródłowy Hello hello polecenia Hive Create Table.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>folder wyjściowy Hello hello instrukcji INSERT zastąpić.</td></tr>
    <tr><td>${hiveTableName}</td><td>Nazwa Hello hello Hive tabeli, która odwołuje się do plików danych log4j hello.</td></tr>
    </table>

    Zmienne akcji Sqoop

    <table border = "1">
    <tr><th>Sqoop zmiennej akcji</th><th>Opis</th></tr>
    <tr><td>${sqlDatabaseConnectionString}</td><td>Parametry połączenia bazy danych SQL.</td></tr>
    <tr><td>${sqlDatabaseTableName}</td><td>Witaj danych hello toowhere z tabeli bazy danych Azure SQL zostaną wyeksportowane.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>folder wyjściowy Hello hello Hive Wstaw zastąpić instrukcji. Jest to hello tego samego folderu eksportu Sqoop hello (export-dir).</td></tr>
    </table>

    Aby uzyskać więcej informacji o przepływie pracy Oozie i przy użyciu hello przepływu pracy akcji, zobacz [dokumentację Apache Oozie 4.0] [ apache-oozie-400] (dla usługi HDInsight klastra w wersji 3.0) lub [Apache Oozie 3.3.2 Dokumentacja] [ apache-oozie-332] (dla usługi HDInsight klastra w wersji 2.1).

1. Zapisz plik hello jako **C:\Tutorials\UseOozie\workflow.xml** przy użyciu kodowania ANSI (ASCII). (Użyj Notatnik, jeśli ta opcja nie są dostępne w edytorze tekstów).

**Koordynator toodefine**

1. Utwórz plik tekstowy z hello następującej zawartości:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    Istnieje pięć zmienne używane w pliku definicji hello:

   | Zmienna | Opis |
   | --- | --- |
   | ${coordFrequency} |Czas wstrzymania zadania. Częstotliwość zawsze jest wyrażone w minutach. |
   | ${coordStart} |Godzina rozpoczęcia zadania. |
   | ${coordEnd} |Godzina zakończenia zadania. |
   | ${coordTimezone} |Oozie przetwarza koordynator zadań w stałej strefy czasowej z nie czasu letniego (zazwyczaj reprezentowany przy użyciu czasu UTC). Ta strefa czasowa jest określane jako hello "Oozie przetwarzania strefy czasowej." |
   | ${wfPath} |Ścieżka Hello hello workflow.xml.  Jeśli nazwa pliku hello przepływu pracy nie jest hello domyślnej nazwy pliku (workflow.xml), należy ją określić. |
2. Zapisz plik hello jako **C:\Tutorials\UseOozie\coordinator.xml** przy użyciu kodowania ANSI (ASCII) hello. (Użyj Notatnik, jeśli ta opcja nie są dostępne w edytorze tekstów).

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a>Wdrażanie projektu Oozie hello i przygotowania samouczka hello
Zostanie uruchomiony programu Azure PowerShell skryptu tooperform hello poniżej:

* Kopiuj hello magazynu obiektów Blob tooAzure skryptu (useoozie.hql) HiveQL, wasb:///tutorials/useoozie/useoozie.hql.
* Skopiuj workflow.xml toowasb:///tutorials/useoozie/workflow.xml.
* Skopiuj coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.
* Plik danych hello kopiowania (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.
* Tworzenie tabeli bazy danych Azure SQL do przechowywania danych eksportu Sqoop. Nazwa tabeli Hello jest *log4jLogCount*.

**Informacje magazynie usługi HDInsight**

HDInsight używa magazynu obiektów Blob platformy Azure do przechowywania danych. wasb: / / to implementacja firmy Microsoft hello Hadoop distributed file system (HDFS) w magazynie obiektów Blob Azure. Aby uzyskać więcej informacji, zobacz [magazynu obiektów Blob Azure użycia z usługą HDInsight][hdinsight-storage].

Podczas obsługi administracyjnej klastra usługi HDInsight, konta magazynu obiektów Blob platformy Azure i w określonym kontenerze z tego konta zostaje wyznaczony jako hello domyślnego systemu plików, podobnie jak w systemie plików HDFS. Ponadto toothis konta magazynu, można dodać dodatkowe konta magazynu z hello sam subskrypcji platformy Azure lub z różnych subskrypcji Azure, podczas procesu udostępniania hello. Aby uzyskać instrukcje dotyczące dodawania dodatkowych kont magazynu, zobacz [Obsługa administracyjna klastrów HDInsight][hdinsight-provision]. skrypt programu Azure PowerShell hello toosimplify używany w tym samouczku, wszystkie pliki są przechowywane w kontenerze systemu plików domyślne hello hello znajdujący się w */samouczki/useoozie*. Domyślnie ten kontener ma takie same nazwy jak nazwa klastra usługi HDInsight hello hello.
Składnia Hello jest następująca:

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> Tylko hello *wasb: / /* składni jest obsługiwane w klastrze usługi HDInsight w wersji 3.0. Witaj starsze *asv: / /* składnia jest obsługiwana w HDInsight 2.1 i 1.6 klastrów, ale nie jest obsługiwana w klastrach HDInsight 3.0.
>
> Witaj wasb: / / ścieżka jest ścieżką wirtualną. Aby uzyskać więcej informacji, zobacz [magazynu obiektów Blob Azure użycia z usługą HDInsight][hdinsight-storage].

Plik, który jest przechowywany w kontenerze systemu plików domyślne hello jest możliwy z usługi HDInsight przy użyciu dowolnej z hello następujące identyfikatory URI (na przykład używam programu workflow.xml):

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

Jeśli chcesz tooaccess hello pliku bezpośrednio z konta magazynu hello hello nazwa obiektu blob dla pliku hello jest:

    tutorials/useoozie/workflow.xml

**Zrozumienie tabele programu Hive wewnętrznych i zewnętrznych**

Istnieje kilka rzeczy, o których należy tooknow o tabele programu Hive wewnętrznych i zewnętrznych:

* Witaj polecenia CREATE TABLE tworzy wewnętrznej tabeli, znanej także jako zarządzane tabeli. plik danych Hello musi znajdować się w kontenerze domyślna hello.
* Witaj polecenia CREATE TABLE przenosi dane hello plikutoohello/hive/magazynu/<TableName> folderu w hello domyślnego kontenera.
* Witaj polecenia CREATE TABLE zewnętrznych tworzy tabelę zewnętrzną. plik danych Hello może znajdować się poza hello domyślnego kontenera.
* Hello polecenia CREATE TABLE zewnętrznych nie powoduje przeniesienia hello pliku danych.
* Witaj polecenia CREATE TABLE zewnętrznych nie zezwala na wszystkie podfoldery w folderze hello, która została określona w klauzuli lokalizacji hello. Jest to powód hello Dlaczego samouczek hello tworzy kopię pliku sample.log hello.

Aby uzyskać więcej informacji, zobacz [HDInsight: Hive wewnętrznych i zewnętrznych wprowadzenie tabel][cindygross-hive-tables].

**Samouczek hello tooprepare**

1. Otwórz hello programu Windows PowerShell ISE (na ekranie powitania Start systemu Windows 8, wpisz **PowerShell_ISE**, a następnie kliknij przycisk **programu Windows PowerShell ISE**. Aby uzyskać więcej informacji, zobacz [programu Windows PowerShell Start w systemie Windows 8 i Windows][powershell-start]).
2. W dolnym okienku hello Uruchom hello następujące polecenia tooconnect tooyour subskrypcji platformy Azure:

    ```powershell
    Add-AzureAccount
    ```

    Użytkownik będzie tooenter zostanie wyświetlony monit o poświadczenia konta Azure. Ta metoda dodawania połączenia subskrypcji wygaśnie, a po 12 godzinach, konieczne będzie polecenia cmdlet hello toorun ponownie.

   > [!NOTE]
   > Jeśli masz wiele subskrypcji platformy Azure i hello Domyślna subskrypcja nie jest hello z nich ma toouse, użyj hello <strong>AzureSubscription wybierz</strong> tooselect polecenia cmdlet subskrypcji.

3. Skopiuj hello następującego skryptu w okienku skryptów hello, a następnie ustaw zmienne pierwszych sześciu hello:

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    Aby więcej opisy hello zmiennych, zobacz hello [wymagania wstępne](#prerequisites) sekcji, w tym samouczku.

4. Dołącz hello następującego skryptu toohello w okienku skryptów hello:

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. Kliknij przycisk **Uruchom skrypt** lub naciśnij klawisz **F5** toorun hello skryptu. Witaj dane wyjściowe będą podobne do:

    ![Dane wyjściowe przygotowania samouczka][img-preparation-output]

## <a name="run-hello-oozie-project"></a>Uruchom projekt Oozie hello
Program Azure PowerShell obecnie nie udostępnia żadnych poleceń cmdlet do definiowania Oozie zadań. Można użyć hello **Invoke RestMethod** usług sieci web Oozie tooinvoke polecenia cmdlet. Interfejs API usług sieci web Oozie Hello jest JSON interfejsu API REST protokołu HTTP. Aby uzyskać więcej informacji o usługach sieci web Oozie hello interfejsu API, zobacz [dokumentację Apache Oozie 4.0] [ apache-oozie-400] (dla usługi HDInsight klastra w wersji 3.0) lub [dokumentację Apache Oozie 3.3.2] [ apache-oozie-332] (dla usługi HDInsight klastra w wersji 2.1).

**toosubmit Oozie zadania**

1. Otwórz hello programu Windows PowerShell ISE (na ekranie Start systemu Windows 8, wpisz **PowerShell_ISE**, a następnie kliknij przycisk **programu Windows PowerShell ISE**. Aby uzyskać więcej informacji, zobacz [programu Windows PowerShell Start w systemie Windows 8 i Windows][powershell-start]).
2. Następujące hello kopii skryptu w okienku skryptów hello, a następnie zestaw hello zmienne najpierw czternastu (jednak pominąć **$storageUri**).

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    Aby więcej opisy hello zmiennych, zobacz hello [wymagania wstępne](#prerequisites) sekcji, w tym samouczku.

    $coordstart i $coordend są uruchamianie przepływu pracy hello i godzina zakończenia. toofind limit czasu UTC/GMT hello, wyszukaj "czas utc" na bing.com. Witaj $coordFrequency jest częstotliwość w minutach toorun hello w przepływie pracy.
3. Dołącz powitania po toohello skryptu. Ta część definiuje ładunek Oozie hello:

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > Witaj główną różnicą w porównaniu toohello przepływu pracy przesyłanie ładunku plik jest zmienna hello **oozie.coord.application.path**. Po przesłaniu zadania przepływu pracy, należy użyć **oozie.wf.application.path** zamiast tego.

4. Dołącz powitania po toohello skryptu. Ta część sprawdza stan usługi sieci web Oozie hello:

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. Dołącz powitania po toohello skryptu. Ta część tworzy zadanie Oozie:

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > Po przesłaniu zadania przepływu pracy należy inne zadanie hello toostart wywołania sieci web usługi po utworzeniu zadania hello. W takim przypadku zadania koordynatora hello jest wyzwalany przez czas. zadanie Hello rozpocznie się automatycznie.

6. Dołącz powitania po toohello skryptu. Ta część sprawdza stan zadania Oozie hello:

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. (Opcjonalnie) Dołącz powitania po toohello skryptu.

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. Dołącz powitania po toohello skryptu:

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    Usuń znaki # hello, jeśli chcesz, dodatkowe funkcje hello toorun.
9. Jeśli z klastrem usługi HDinsight w wersji 2.1, zastąp "https://$clusterName.azurehdinsight.net:443/oozie/v2/" z "https://$clusterName.azurehdinsight.net:443/oozie/v1/". Klaster usługi HDInsight w wersji 2.1 nie nie obsługuje wersji 2 hello usług sieci web.
10. Kliknij przycisk **Uruchom skrypt** lub naciśnij klawisz **F5** toorun hello skryptu. Witaj dane wyjściowe będą podobne do:

     ![Samouczek uruchomienia przepływu pracy w danych wyjściowych][img-runworkflow-output]
11. Połącz tooyour bazy danych SQL toosee hello wyeksportowane dane.

**Dziennik błędów programu toocheck hello zadania**

tootroubleshoot przepływu pracy, plik dziennika Oozie hello można znaleźć w C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log z hello headnode klastra. Aby uzyskać informacji na temat protokołu RDP, zobacz [administrowanie klastrów usługi HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal].

**Samouczek hello toorerun**

toorerun hello przepływu pracy, należy wykonać następujące zadania hello:

* Usuń plik danych wyjściowych skryptu Hive hello.
* Usuń dane hello hello log4jLogsCount tabeli.

Poniżej przedstawiono przykładowy skrypt programu Windows PowerShell, którego można używać:

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a>Następne kroki
W tym samouczku można przedstawiono sposób toodefine Oozie przepływu pracy i Oozie coordinator oraz jak toorun Oozie coordinator zadania przy użyciu programu Azure PowerShell. toolearn więcej, zobacz następujące artykuły hello:

* [Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started]
* [Użyj magazynu obiektów Blob platformy Azure z usługą HDInsight][hdinsight-storage]
* [Administrowanie HDInsight przy użyciu programu Azure PowerShell][hdinsight-admin-powershell]
* [Przekazywanie danych tooHDInsight][hdinsight-upload-data]
* [Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]
* [Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]
* [Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]
* [Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-java-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
