---
title: "zadania aaaRun usługi Hadoop przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zadania toorun proste Hive, Pig i MapReduce z bazy danych rozwiązania Cosmos Azure i usłudze Azure HDInsight."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="Azure Cosmos DB-HDInsight"></a>Uruchom zadanie Apache Hive, Pig lub Hadoop przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight
W tym samouczku przedstawiono sposób toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], i [Apache Hadoop] [ apache-hadoop] Zadań MapReduce w usłudze Azure HDInsight z łącznikiem usługi Hadoop DB rozwiązania Cosmos. Łącznik usługi Hadoop rozwiązania cosmos w DB umożliwia tooact rozwiązania Cosmos bazy danych jako źródło i ujście zadań Hive, Pig i MapReduce. W tym samouczku będą używać rozwiązania Cosmos bazy danych jako hello danych źródłowym i docelowym zadania usługi Hadoop.

Po ukończeniu tego samouczka, będziesz w stanie tooanswer hello następujące pytania:

* Jak załadować dane z rozwiązania Cosmos bazy danych przy użyciu zadania Hive, Pig lub MapReduce?
* Sposób przechowywania danych w bazie danych rozwiązania Cosmos przy użyciu zadania Hive, Pig lub MapReduce?

Zalecamy rozpoczęcie pracy od obejrzenia powitania po wideo, w którym przeprowadzana za pomocą zadania Hive za pomocą rozwiązania Cosmos bazę danych i usługi HDInsight.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

Następnie zwróć toothis artykułu, gdy otrzymasz hello pełne szczegóły na uruchamianie zadania usługi analiza danych DB rozwiązania Cosmos w.

> [!TIP]
> Ten samouczek zakłada, że masz wcześniejszego doświadczenia w używaniu platformy Apache Hadoop, Hive i Pig. Jeśli nowy tooApache Hadoop, Hive i Pig, zaleca się odwiedzenie hello [dokumentację Apache Hadoop][apache-hadoop-doc]. W tym samouczku przyjęto założenie, czy masz doświadczenie z rozwiązania Cosmos bazy danych, a konto DB rozwiązania Cosmos. Jeśli jesteś tooCosmos nowej bazy danych lub nie masz konta rozwiązania Cosmos bazy danych, można znaleźć na naszych [wprowadzenie] [ getting-started] strony.
>
>

Nie masz czasu toocomplete hello samouczka i po prostu chcesz skryptów programu PowerShell pełny przykład hello tooget Hive, Pig i MapReduce? Nie ma problemu, pobierz je [tutaj][hdinsight-samples]. Pobieranie Hello zawiera również hello hql, pig i java pliki dla tych przykładów.

## <a name="NewestVersion"></a>Najnowsza wersja
<table border='1'>
    <tr><th>Wersja łącznika usługi Hadoop</th>
        <td>1.2.0</td></tr>
    <tr><th>Identyfikator Uri skryptu</th>
        <td>https://portalcontent.blob.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</td></tr>
    <tr><th>Data modyfikacji</th>
        <td>04/26/2016</td></tr>
    <tr><th>HDInsight obsługiwane wersje</th>
        <td>3.1, 3.2</td></tr>
    <tr><th>Dziennik zmian</th>
        <td>Zaktualizowano rozwiązania Cosmos Azure DB Java SDK too1.6.0</br>
            Dodano obsługę dla kolekcji partycjonowanych jako źródło i ujście</br>
        </td></tr>
</table>

## <a name="Prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem powitalne instrukcje w tym samouczku, upewnij się, że masz następujące hello:

* Konto rozwiązania Cosmos bazy danych, bazy danych i kolekcji dokumentów wewnątrz. Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z bazy danych rozwiązania Cosmos][getting-started]. Importuj przykładowe dane na koncie DB rozwiązania Cosmos z hello [narzędzia importu DB rozwiązania Cosmos][import-data].
* Przepustowość. Odczyty i zapisy z HDInsight będą liczone kierunku jednostek żądania przeznaczonym dla kolekcji.
* Pojemność dodatkowe procedurę składowaną w ramach każdej wyjściowego kolekcji. procedury przechowywane Hello są używane do przesyłania wynikowy dokumentów.
* Wydajność hello wynikowy dokumentów z hello zadań Hive, Pig i MapReduce.
* [*Opcjonalnie*] pojemności dla dodatkowych kolekcji.

> [!WARNING]
> Kolejność tworzenia hello tooavoid nową kolekcję podczas każdego zadania hello możesz wydrukować toostdout wyniki hello, Zapisz hello dane wyjściowe tooyour WASB kontenera lub określić już istniejącą kolekcję. W przypadku hello określając istniejącą kolekcję, zostanie utworzona nowych dokumentów w kolekcji hello i już istniejących dokumentów będzie dotyczył tylko, jeśli istnieje konflikt w *identyfikatorów*. **Łącznik Hello automatycznie spowoduje zastąpienie istniejących dokumentów konflikt identyfikatorów**. Można wyłączyć tę funkcję, ustawiając hello upsert opcji toofalse. Jeśli występuje konflikt upsert ma wartość false, zakończy się niepowodzeniem zadania usługi Hadoop hello; raportowania błędów konflikt identyfikatora.
>
>

## <a name="ProvisionHDInsight"></a>Krok 1: Tworzenie nowego klastra usługi HDInsight
Ten samouczek używa akcji skryptu z toocustomize Azure Portal hello z klastrem usługi HDInsight. W tym samouczku używamy toocreate Azure Portal hello z klastrem usługi HDInsight. Aby uzyskać instrukcje dotyczące sposobu toouse poleceń cmdlet programu PowerShell lub hello zestawu .NET SDK usługi HDInsight, zapoznaj się [HDInsight dostosować klastry za pomocą akcji skryptu] [ hdinsight-custom-provision] artykułu.

1. Zaloguj się toohello [Azure Portal][azure-portal].
2. Kliknij przycisk **+ nowy** u góry hello hello lewy pasek nawigacyjny, wyszukaj **HDInsight** w hello górnym pasku wyszukiwania na powitania nowy blok.
3. **HDInsight** opublikowanych przez **Microsoft** pojawi się u góry hello hello wyników. Kliknij go, a następnie kliknij przycisk **Utwórz**.
4. Utwórz bloku na powitania nowego klastra usługi HDInsight, wprowadź użytkownika **nazwy klastra** i wybierz hello **subskrypcji** ma tooprovision tego zasobu w obszarze.

    <table border='1'>
        <tr><td>Nazwa klastra</td><td>Nazwa klastra hello.<br/>
Nazwa DNS musi uruchomić i kończyć się znakiem alfanumeryczne i może zawierać kresek.<br/>
pole Hello musi być ciągiem od 3 do 63 znaków.</td></tr>
        <tr><td>Nazwa subskrypcji</td>
            <td>Jeśli masz więcej niż jedną subskrypcję platformy Azure, wybierz subskrypcję hello, który będzie hostem z klastrem usługi HDInsight. </td></tr>
    </table>
5.Kliknij przycisk **wybierz typ klastra** i hello ustaw następujące właściwości toohello określone wartości.

    <table border='1'>
        <tr><td>Typ klastra</td><td><strong>Hadoop</strong></td></tr>
        <tr><td>Warstwy klastrów</td><td><strong>Standardowa</strong></td></tr>
        <tr><td>System operacyjny</td><td><strong>Windows</strong></td></tr>
        <tr><td>Wersja</td><td>Najnowsza wersja</td></tr>
    </table>

    Teraz, kliknij przycisk **wybierz**.

    ![Podaj szczegóły klastra Hadoop HDInsight][image-customprovision-page1]
6. Polecenie **poświadczenia** tooset Twoje poświadczenia logowania i zdalnego dostępu. Wybierz użytkownika **nazwa użytkownika logowania klastra** i **hasło logowania klastra**.

    Tooremote w klastrze, wybierz opcję *tak* u dołu bloku hello hello i podaj nazwę użytkownika i hasło.
7. Polecenie **źródła danych** dostęp do lokalizacji głównej dla danych tooset. Wybierz hello **metodę wyboru** i określenia już istniejącego konta magazynu lub Utwórz nową.
8. Na hello na tym samym bloku, określ **domyślny kontener** i **lokalizacji**. I kliknij przycisk **wybierz**.

   > [!NOTE]
   > Wybierz lokalizację tooyour Zamknij region konta DB rozwiązania Cosmos w celu poprawy wydajności
   >
   >
9. Polecenie **cennik** tooselect hello liczbę i rodzaj węzłach. Później można zachować hello domyślnej konfiguracji i skali hello liczba węzłów procesu roboczego.
10. Kliknij przycisk **konfiguracji opcjonalnej**, następnie **akcji skryptu** w hello opcjonalne blok konfiguracji.

     W akcji skryptu wprowadź następujące informacje toocustomize hello z klastrem usługi HDInsight.

     <table border='1'>
         <tr><th>Właściwość</th><th>Wartość</th></tr>
         <tr><td>Nazwa</td>
             <td>Określ nazwę hello akcji skryptu.</td></tr>
         <tr><td>Identyfikator URI skryptu</td>
             <td>Określ hello URI toohello skrypt, który jest wywołana toocustomize hello klastra.</br></br>
Wprowadź: </br> <strong>https://portalcontent.blob.Core.Windows.NET/scriptaction/documentdb-hadoop-Installer-v04.ps1</strong>.</td></tr>
         <tr><td>Główny</td>
             <td>Kliknij przycisk hello wyboru toorun hello skrypt programu PowerShell na powitania Head węzła.</br></br>
             <strong>Zaznacz to pole wyboru</strong>.</td></tr>
         <tr><td>Węzeł roboczy</td>
             <td>Kliknij przycisk hello wyboru toorun hello skrypt programu PowerShell na powitania węzła procesu roboczego.</br></br>
             <strong>Zaznacz to pole wyboru</strong>.</td></tr>
         <tr><td>Dozorca</td>
             <td>Kliknij przycisk hello wyboru toorun hello skrypt programu PowerShell na powitania dozorcy.</br></br>
             <strong>Zbędny</strong>.
             </td></tr>
         <tr><td>Parametry</td>
             <td>Określ parametry hello, jeśli są wymagane przez skrypt hello.</br></br>
             <strong>Brak parametrów potrzebne</strong>.</td></tr>
     </table>
11.Tworzyć nowe **grupy zasobów** lub użyj istniejącej grupy zasobów w ramach Twojej subskrypcji platformy Azure.
12. Teraz, sprawdź **toodashboard numeru Pin** tootrack jego wdrożenia i kliknij przycisk **Utwórz**!

## <a name="InstallCmdlets"></a>Krok 2: Instalowanie i konfigurowanie programu Azure PowerShell
1. Zainstaluj program Azure PowerShell. Instrukcje można znaleźć [tutaj][powershell-install-configure].

   > [!NOTE]
   > Można również tylko dla zapytań programu Hive, można użyć edytora online Hive w usłudze HDInsight. toodo tak, zaloguj się w toohello [Azure Portal][azure-portal], kliknij przycisk **HDInsight** na powitania w okienku po lewej stronie tooview lista klastrów usługi HDInsight. Kliknij klaster hello mają zapytań programu Hive toorun na, a następnie kliknij przycisk **konsoli zapytania**.
   >
   >
2. Otwórz hello Azure PowerShell zintegrowane skryptów środowiska:

   * Na komputerze z systemem Windows 8 lub Windows Server 2012 lub nowszym, można użyć wbudowanych hello wyszukiwania. Na ekranie startowym hello wpisz **programu powershell ise** i kliknij przycisk **Enter**.
   * Na komputerze z systemem w wersji starszej niż Windows 8 lub Windows Server 2012 Użyj hello Start menu. W hello Start menu, wpisz **wiersza polecenia** w polu wyszukiwania hello, a następnie na liście hello wyników, kliknij przycisk **wiersza polecenia**. W hello wiersza polecenia, wpisz **powershell_ise** i kliknij przycisk **Enter**.
3. Dodaj konto platformy Azure.

   1. W okienku konsoli hello, wpisz **Add-AzureAccount** i kliknij przycisk **Enter**.
   2. Wpisz adres e-mail hello skojarzone z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**.
   3. Wpisz hasło powitania dla subskrypcji platformy Azure.
   4. Kliknij przycisk **Zaloguj**.
4. powitania po diagram identyfikuje hello ważne części środowiska skryptów programu PowerShell Azure.

    ![Diagram do programu Azure PowerShell][azure-powershell-diagram]

## <a name="RunHive"></a>Krok 3: Uruchomienie zadania Hive za pomocą rozwiązania Cosmos bazę danych i usługi HDInsight
> [!IMPORTANT]
> Wszystkie zmienne określają < > musi być wypełnione przy użyciu ustawień konfiguracji.
>
>

1. Ustaw hello następujące zmienne w okienku skrypt programu PowerShell.

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p>Zacznijmy konstruowanie ciągu zapytania. Firma Microsoft będzie Napisz zapytanie Hive, które przyjmuje sygnatury czasowe wygenerowany przez system (_ts) i unikatowe identyfikatory (_rid) z kolekcji bazy danych Azure rozwiązania Cosmos wszystkie dokumenty, zlicza wszystkie dokumenty za minutę hello, a następnie zapisuje wyniki hello do nowej kolekcji bazy danych Azure rozwiązania Cosmos.</p>

    <p>Najpierw utwórz tabeli programu Hive z naszych kolekcji bazy danych Azure rozwiązania Cosmos. Dodaj powitania po toohello fragment kodu skryptu PowerShell okienko <strong>po</strong> hello fragment kodu z #1. Upewnij się, że zawierają hello opcjonalne DocumentDB.query parametru t przycinania _ts toojust dokumentów i _rid firmy Microsoft.</p>

   > [!NOTE]
   > **Nazewnictwo DocumentDB.inputCollections nie błędu.** Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wejściowe: </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. Następnie utwórz tabeli programu Hive dla kolekcji danych wyjściowych hello. właściwości dokumentu Hello danych wyjściowych będzie hello miesiąc, dzień, godzinę, minutę i hello całkowita liczba wystąpień.

   > [!NOTE]
   > **Jeszcze ponownie nazewnictwa DocumentDB.outputCollections nie błędu.** Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wyjściowe: </br>
   > "*DocumentDB.outputCollections*"="*\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 1\>*,*\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 2\>*" </br> nazwy kolekcji Hello są oddzielone bez spacji, za pomocą tylko jednego przecinka. </br></br>
   > Dokumenty będą okrężnego rozproszonych w wielu kolekcjach. Wsadowe dokumentów będą przechowywane w jednej kolekcji, a następnie drugi partii dokumenty będą przechowywane w kolekcji dalej hello i tak dalej.
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. Na koniec załóżmy zgadzają hello dokumentów przez miesiąc, dzień, godzinę i wyniki hello minutę i Wstaw do hello output tabelę programu Hive.

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. Dodaj powitania po toocreate fragment kodu skryptu definicji zadania Hive z hello poprzednie zapytanie.

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    Można również użyć hello — plik przełącznika toospecify HiveQL pliku skryptu w systemie plików HDFS.
4. Dodaj powitania po czas rozpoczęcia hello toosave fragment i przesłać zadania technologii Hive hello.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. Dodaj następujące toowait dla toocomplete zadania Hive hello hello.

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. Dodaj powitania po tooprint hello standardowe Wyjście i hello rozpoczęcia i zakończenia godzin.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. **Uruchom** nowy skrypt! **Kliknij przycisk** zielony hello wykonania przycisku.
8. Sprawdzanie wyników hello. Zaloguj się na powitania [Azure Portal][azure-portal].

   1. Kliknij przycisk <strong>Przeglądaj</strong> na powitania po lewej stronie panelu. </br>
   2. Kliknij przycisk <strong>wszystko</strong> na powitania prawym górnym rogu hello przeglądania panelu. </br>
   3. Znajdź i kliknij <strong>kont DB rozwiązania Cosmos Azure</strong>. </br>
   4. Następnie znaleźć Twoje <strong>konto bazy danych Azure rozwiązania Cosmos</strong>, następnie <strong>bazy danych DB rozwiązania Cosmos Azure</strong> i <strong>Azure rozwiązania Cosmos DB kolekcji</strong> skojarzone z określonej w kolekcji danych wyjściowych hello Zapytanie Hive.</br>
   5. Na koniec kliknij <strong>Eksploratora dokumentów</strong> pod <strong>Developer Tools</strong>.</br></p>

   Zostanie wyświetlone powitalne wyniki zapytania Hive.

   ![Wyniki zapytania hive][image-hive-query-results]

## <a name="RunPig"></a>Krok 4: Uruchom zadanie Pig przy użyciu rozwiązania Cosmos bazę danych i usługi HDInsight
> [!IMPORTANT]
> Wszystkie zmienne określają < > musi być wypełnione przy użyciu ustawień konfiguracji.
>
>

1. Ustaw hello następujące zmienne w okienku skrypt programu PowerShell.

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p>Zacznijmy konstruowanie ciągu zapytania. Firma Microsoft będzie Napisz zapytanie Pig, które przyjmuje sygnatury czasowe wygenerowany przez system (_ts) i unikatowe identyfikatory (_rid) z kolekcji bazy danych Azure rozwiązania Cosmos wszystkie dokumenty, zlicza wszystkie dokumenty za minutę hello, a następnie zapisuje wyniki hello do nowej kolekcji bazy danych Azure rozwiązania Cosmos.</p>
    <p>Po pierwsze ładowanie dokumentów z rozwiązania Cosmos bazy danych do usługi HDInsight. Dodaj powitania po toohello fragment kodu skryptu PowerShell okienko <strong>po</strong> hello fragment kodu z #1. Upewnij się, tooadd DocumentDB naszych _ts toojust dokumentów oraz _rid tootrim parametru zapytania usługi DocumentDB toohello opcjonalne zapytania.</p>

   > [!NOTE]
   > Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wejściowe: </br>
   > "*\<Nazwa kolekcji usługi DocumentDB w danych wejściowych 1\>*,*\<Nazwa kolekcji usługi DocumentDB w danych wejściowych 2\>*"</br> nazwy kolekcji Hello są oddzielone bez spacji, za pomocą tylko jednego przecinka. </b>
   >
   >

    Dokumenty będą okrężnego rozproszonych w wielu kolekcjach. Wsadowe dokumentów będą przechowywane w jednej kolekcji, a następnie drugi partii dokumenty będą przechowywane w kolekcji dalej hello i tak dalej.

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. Następnie Załóżmy zgadzają hello dokumentów przez hello miesiąc, dzień, godzinę, minutę i hello całkowita liczba wystąpień.

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. Na koniec załóżmy przechowywać wyniki hello w naszej nowej kolekcji danych wyjściowych.

   > [!NOTE]
   > Tak, firma Microsoft Zezwalaj na dodawanie wielu kolekcji jako dane wyjściowe: </br>
   > "\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 1\>,\<Nazwa kolekcji usługi DocumentDB w danych wyjściowych 2\>"</br> nazwy kolekcji Hello są oddzielone bez spacji, za pomocą tylko jednego przecinka.</br>
   > Dokumenty będą być rozproszone okrężnego w obrębie hello wielu kolekcji. Wsadowe dokumentów będą przechowywane w jednej kolekcji, a następnie drugi partii dokumenty będą przechowywane w kolekcji dalej hello i tak dalej.
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. Dodaj powitania po toocreate fragment kodu skryptu definicji zadania Pig z hello poprzednie zapytanie.

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    Można również użyć hello — plik przełącznika toospecify pliku skryptu Pig na system plików HDFS.
6. Dodaj powitania po czas rozpoczęcia hello toosave fragment i przesłać zadania programu Pig hello.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. Dodaj powitania po toowait dla hello Pig zadania toocomplete.

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. Dodaj powitania po tooprint hello standardowe Wyjście i hello rozpoczęcia i zakończenia godzin.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. **Uruchom** nowy skrypt! **Kliknij przycisk** zielony hello wykonania przycisku.
10. Sprawdzanie wyników hello. Zaloguj się na powitania [Azure Portal][azure-portal].

    1. Kliknij przycisk <strong>Przeglądaj</strong> na powitania po lewej stronie panelu. </br>
    2. Kliknij przycisk <strong>wszystko</strong> na powitania prawym górnym rogu hello przeglądania panelu. </br>
    3. Znajdź i kliknij <strong>kont DB rozwiązania Cosmos Azure</strong>. </br>
    4. Następnie znaleźć Twoje <strong>konto bazy danych Azure rozwiązania Cosmos</strong>, następnie <strong>bazy danych DB rozwiązania Cosmos Azure</strong> i <strong>Azure rozwiązania Cosmos DB kolekcji</strong> skojarzone z określonej w kolekcji danych wyjściowych hello Kwerenda Pig.</br>
    5. Na koniec kliknij <strong>Eksploratora dokumentów</strong> pod <strong>Developer Tools</strong>.</br></p>

    Zostanie wyświetlone hello wyników kwerendy Pig.

    ![Wyniki zapytania pig][image-pig-query-results]

## <a name="RunMapReduce"></a>Krok 5: Uruchomienie zadania MapReduce przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight
1. Ustaw hello następujące zmienne w okienku skrypt programu PowerShell.

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. Firma Microsoft będzie wykonywać zadania MapReduce, które zlicza hello liczba wystąpień dla każdej właściwości dokumentu z kolekcji bazy danych Azure rozwiązania Cosmos. Dodaj następujący fragment kodu skryptu **po** fragment hello powyżej.

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > TallyProperties v01.jar zawiera hello Instalacja niestandardowa programu hello łącznika usługi Hadoop DB rozwiązania Cosmos.
   >
   >
3. Dodaj następujące zadania MapReduce hello toosubmit polecenia hello.

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    Dodatkowo toohello definicji zadania MapReduce, można też podać nazwy klastra usługi HDInsight hello miejscu zadania MapReduce hello toorun i poświadczenia hello. Witaj AzureHDInsightJob rozpoczęcia jest wywołania asynchronicznego. toocheck hello ukończenia zadania hello, użyj hello *AzureHDInsightJob oczekiwania* polecenia cmdlet.
4. Dodaj następujące polecenie toocheck hello błędy uruchomione zadania MapReduce hello.

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. **Uruchom** nowy skrypt! **Kliknij przycisk** zielony hello wykonania przycisku.
6. Sprawdzanie wyników hello. Zaloguj się na powitania [Azure Portal][azure-portal].

   1. Kliknij przycisk <strong>Przeglądaj</strong> na powitania po lewej stronie panelu.
   2. Kliknij przycisk <strong>wszystko</strong> na powitania prawym górnym rogu hello przeglądania panelu.
   3. Znajdź i kliknij <strong>kont DB rozwiązania Cosmos Azure</strong>.
   4. Następnie znaleźć Twoje <strong>konto bazy danych Azure rozwiązania Cosmos</strong>, następnie <strong>bazy danych DB rozwiązania Cosmos Azure</strong> i <strong>Azure rozwiązania Cosmos DB kolekcji</strong> skojarzone z określonej w kolekcji danych wyjściowych hello zadania MapReduce.
   5. Na koniec kliknij <strong>Eksploratora dokumentów</strong> pod <strong>Developer Tools</strong>.

      Zostanie wyświetlone powitalne wyników zadania MapReduce.

      ![MapReduce wyników zapytania][image-mapreduce-query-results]

## <a name="NextSteps"></a>Następne kroki
Gratulacje! Właśnie uruchomiono pierwszy zadań Hive, Pig i MapReduce przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight.

Mamy Otwórz powierzając jej ich konserwację naszych łącznika usługi Hadoop. Jeśli chcesz, można współtworzyć na [GitHub][github].

toolearn więcej, zobacz następujące artykuły hello:

* [Tworzenie aplikacji Java z usługi Documentdb][documentdb-java-application]
* [Tworzenie programów Java MapReduce dla platformy Hadoop w usłudze HDInsight][hdinsight-develop-deploy-java-mapreduce]
* [Rozpocząć korzystanie z usługi Hadoop przy użyciu Hive HDInsight tooanalyze przenośnych słuchawki używana][hdinsight-get-started]
* [Korzystać z usługi MapReduce z usługą HDInsight][hdinsight-use-mapreduce]
* [Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]
* [Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]
* [Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-hadoop-customize-cluster]

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
