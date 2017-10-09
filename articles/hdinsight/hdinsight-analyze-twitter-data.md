---
title: "aaaAnalyze danych Twitter z platformą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Hive tooanalyze Twitter danych na platformie Hadoop w HDInsight toofind hello częstotliwości użycia określonego wyrazu."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a>Analizowanie danych Twitter przy użyciu Hive w usłudze HDInsight
Społecznościowych witryn sieci Web są jednym z głównych wymusza pobudzenie hello przyjmowania danych big data. Publiczny interfejsów API dostarczonych przez witryn, takie jak Twitter są użyteczne źródło danych do analizowania i zrozumienie trendów popularnych.
W tym samouczku zostanie uzyskać tweetów za pomocą usługi Twitter, przesyłanie strumieniowe interfejsu API, a następnie użyj Apache Hive w usłudze Azure HDInsight tooget listę użytkowników usługi Twitter, których wysłane hello większość tweetów, zawierających określony wyraz.

> [!IMPORTANT]
> Witaj czynności w tym dokumencie wymagają klastra usługi HDInsight opartej na systemie Windows. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows). Dla klastra opartych na systemie Linux tooa określonych czynności [Twitter analizowanie danych przy użyciu Hive w usłudze HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka wymagane są następujące hello:

* **Stacja robocza** przy użyciu programu Azure PowerShell zainstalowana i skonfigurowana.

    tooexecute skryptów programu Windows PowerShell, należy uruchomić program Azure PowerShell jako administrator i ustawić zasady wykonywania hello także*RemoteSigned*. Zobacz [skryptów programu Windows PowerShell Uruchom][powershell-script].

    Przed uruchomieniem skryptów programu Windows PowerShell, upewnij się, że są połączone tooyour subskrypcji platformy Azure przy użyciu następującego polecenia cmdlet hello:

    ```powershell
    Login-AzureRmAccount
    ```

    Jeśli masz wiele subskrypcji Azure, użyj następującego polecenia cmdlet tooset hello bieżącej subskrypcji hello:

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > Obsługa programu Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i została usunięta z dniem 1 stycznia 2017 r. Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.
    >
    > Wykonaj kroki hello [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello najnowszą wersję programu Azure PowerShell. Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) Aby uzyskać więcej informacji.

* **Klaster Azure HDInsight**. Aby uzyskać instrukcje dotyczące inicjowania obsługi klastra, zobacz [rozpocząć korzystanie z usługi HDInsight] [ hdinsight-get-started] lub [Obsługa administracyjna klastrów HDInsight][hdinsight-provision]. Nazwa klastra hello trzeba będzie później w samouczku hello.

Witaj poniższej tabeli wymieniono pliki hello używane w tym samouczku:

| Pliki | Opis |
| --- | --- |
| /Tutorials/Twitter/Data/tweets.txt |Witaj źródło danych pod kątem hello zadania Hive. |
| /Tutorials/Twitter/Output |folder wyjściowy Hello hello zadania Hive. Witaj domyślną nazwę pliku wyjściowego zadania Hive jest **000000_0**. |
| Tutorials/Twitter/Twitter.hql |plik skryptu HiveQL Hello. |
| /Tutorials/Twitter/JobStatus |Witaj stan zadania usługi Hadoop. |

## <a name="get-twitter-feed"></a>Twitter Get źródła danych
W tym samouczku użyjesz hello [przesyłania strumieniowego interfejsów API w usłudze Twitter][twitter-streaming-api]. Witaj określonych Twitter przesyłania strumieniowego korzystasz z interfejsu API jest [stanów/filter][twitter-statuses-filter].

> [!NOTE]
> Plik zawierający 10 000 tweetów i plik skryptu Hive hello (opisane w następnej sekcji hello) zostały przekazane w publicznego kontenera obiektów Blob. W tej sekcji można pominąć, jeśli chcesz toouse hello przekazać pliki.

[Tweetów danych](https://dev.twitter.com/docs/platform-objects/tweets) są przechowywane w formacie JavaScript Object Notation (JSON) hello, który zawiera złożone, zagnieżdżone struktury. Zamiast zapisywania wielu wierszy kodu, korzystając z konwencjonalnej język programowania, można przekształcić tej struktury zagnieżdżone do tabeli programu Hive, dzięki czemu mogą być przeszukiwane przez język SQL (Structured Query) — takie jak języka o nazwie HiveQL.

Twitter używa API tooits dostępu tooprovide autoryzacji OAuth. OAuth to protokół uwierzytelniania, umożliwiający użytkownikom tooapprove aplikacji tooact w ich imieniu bez udostępniania swoje hasło. Więcej informacji można znaleźć w folderze [oauth.net](http://oauth.net/) lub hello znakomity [tooOAuth przewodnik dla początkujących](http://hueniverse.com/oauth/) z Hueniverse.

Witaj pierwszy krok toouse OAuth jest toocreate nową aplikację w witrynie Twitter Developer hello.

**toocreate aplikacji Twitter**

1. Zaloguj się za[https://apps.twitter.com/](https://apps.twitter.com/). Kliknij przycisk hello **Zamów teraz** łącza, jeśli nie masz konta w usłudze Twitter.
2. Kliknij przycisk **Utwórz nową aplikację**.
3. Wprowadź **nazwa**, **opis**, **witryny sieci Web**. Można uzupełnić adres URL hello **witryny sieci Web** pola. Witaj w poniższej tabeli przedstawiono niektóre przykładowe wartości toouse:

   | Pole | Wartość |
   | --- | --- |
   |  Nazwa |MyHDInsightApp |
   |  Opis |MyHDInsightApp |
   |  Witryna sieci Web |http://www.myhdinsightapp.com |
4. Sprawdź **tak, zgadzam się**, a następnie kliknij przycisk **tworzenie aplikacji Twitter**.
5. Kliknij przycisk hello **uprawnienia** kartę hello domyślne uprawnienia **tylko do odczytu**. To jest wystarczająca dla tego samouczka.
6. Kliknij przycisk hello **kluczy i tokenów dostępu** kartę.
7. Kliknij przycisk **Utwórz moje tokenu dostępu**.
8. Kliknij przycisk **OAuth testu** w hello prawym górnym rogu strony hello.
9. Zapisz **konsumenta**, **klucz tajny klienta**, **token dostępu**, i **klucz tajny tokenu dostępu**. Potrzebujesz wartości hello później w samouczku hello.

W tym samouczku użyjesz wywołania usługi sieci web hello toomake środowiska Windows PowerShell. C# .NET przykładowy, [analizowanie w czasie rzeczywistym usługi Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight][hdinsight-hbase-twitter-sentiment]. Witaj wywołania usługi sieci web innych popularnych narzędzie toomake jest [ *Curl*][curl]. Zwinięcie można pobrać z [tutaj][curl-download].

> [!NOTE]
> Korzystając z polecenia curl hello w systemie Windows, użyj podwójnych cudzysłowów zamiast apostrofy dla wartości opcji hello.

**tweetów tooget**

1. Otwórz hello Windows PowerShell Integrated Scripting Environment (ISE). (Na ekranie powitania Start systemu Windows 8, wpisz **PowerShell_ISE** , a następnie kliknij przycisk **programu Windows PowerShell ISE**. Zobacz [uruchomić środowisko Windows PowerShell w systemie Windows 8 i Windows][powershell-start].)
2. Skopiuj hello następującego skryptu w okienku skryptów hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Ustaw hello pierwsze pięć tooeight zmienne w skrypcie hello:

    Zmienna|Opis
    ---|---
    $clusterName|Jest to nazwa hello klastra usługi HDInsight hello miejscu aplikacji hello toorun.
    $oauth_consumer_key|To jest aplikacja usługi Twitter hello **konsumenta** zapisanej wcześniej podczas tworzenia aplikacji Twitter hello.
    $oauth_consumer_secret|To jest aplikacja usługi Twitter hello **klucz tajny klienta** zapisanej wcześniej.
    $oauth_token|To jest aplikacja usługi Twitter hello **token dostępu** zapisanej wcześniej.
    $oauth_token_secret|To jest aplikacja usługi Twitter hello **klucz tajny tokenu dostępu** zapisanej wcześniej.
    $destBlobName|Jest to nazwa obiektu blob danych wyjściowych hello. Witaj, wartość domyślna to **tutorials/twitter/data/tweets.txt**. Jeśli zmienisz hello wartość domyślną, konieczne będzie skryptów programu Windows PowerShell hello tooupdate odpowiednio.
    $trackString|Usługa sieci web Hello zwróci słowa kluczowe powiązane toothese tweetów. Witaj, wartość domyślna to **HDInsight Azure, chmury,**. Zmiana wartości domyślnej hello odpowiednio spowoduje zaktualizowanie hello skryptów programu Windows PowerShell.
    $lineMax|wartość Hello Określa, ile skryptu hello tweetów będzie odczytywać. Trwa około 3 minuty tooread tweetów 100. Można ustawić większą liczbę, ale ich może zająć więcej czasu toodownload.

1. Naciśnij klawisz **F5** toorun hello skryptu. Jeśli wystąpiły problemy, jako obejście, wybierz wszystkie wiersze hello, a następnie naciśnij klawisz **F8**.
2. Zostanie wyświetlona "Zakończ"! na końcu hello hello danych wyjściowych. Komunikaty o błędach pojawi się czerwone.

Jako procedury weryfikacji można sprawdzić pliku wyjściowego hello **/tutorials/twitter/data/tweets.txt**, w magazynie obiektów Blob platformy Azure za pomocą Eksploratora usługi storage platformy Azure lub programu Azure PowerShell. Aby uzyskać przykładowy skrypt programu Windows PowerShell do wyświetlania listy plików, zobacz [magazynu obiektów Blob użycia z usługą HDInsight][hdinsight-storage-powershell].

## <a name="create-hiveql-script"></a>Utwórz skrypt HiveQL
Przy użyciu programu Azure PowerShell, można uruchomić wiele instrukcje HiveQL co w czasie, lub pakietu hello instrukcji HiveQL do pliku skryptu. W tym samouczku utworzysz skrypt HiveQL. plik skryptu Hello musi być przekazana tooAzure magazynu obiektów Blob. W następnej sekcji hello należy uruchomić plik skryptu hello przy użyciu programu Azure PowerShell.

> [!NOTE]
> plik skryptu Hive Hello i plik zawierający 10 000 tweetów zostały przekazane w publicznego kontenera obiektów Blob. W tej sekcji można pominąć, jeśli chcesz toouse hello przekazać pliki.

Witaj skrypt HiveQL zostaną wykonane następujące hello:

1. **Witaj tweets_raw tabelę** w przypadku, gdy tabela hello już istnieje.
2. **Tworzenie tabeli Hive tweets_raw hello**. Ta gałąź strukturalnych Tabela tymczasowa przechowuje dane powitania dla dalszego wyodrębniania, transformacji i ładowania (ETL) przetwarzania. Aby uzyskać informacje na partycje, zobacz [samouczek Hive][apache-hive-tutorial].
3. **Ładowanie danych** z folderu źródłowego hello, /tutorials/twitter/data. teraz została przekształcona Hello dużych tweetów dataset w formacie JSON zagnieżdżonych w strukturze tabeli tymczasowej gałęzi.
4. **Upuść hello tweetów tabeli** w przypadku, gdy tabela hello już istnieje.
5. **Utwórz tabelę tweetów hello**. Aby przed dataset tweetów hello można badać przy korzystaniu z programu Hive, musisz toorun inny proces ETL. Ten proces ETL definiuje bardziej szczegółowe schemat tabeli hello danych, które są przechowywane w tabeli "twitter_raw" hello.
6. **Wstaw tabelę Zastąp**. To złożony skryptu Hive zostanie zaczną działać poza zestaw długich zadań MapReduce przez hello klastra usługi Hadoop. W zależności od rozmiar zestawu danych i hello klastra może to potrwać około 10 minut.
7. **Wstaw zastąpić katalogu**. Uruchom zapytanie i dane wyjściowe plik tooa dataset hello. To zapytanie spowoduje zwrócenie listy użytkowników usługi Twitter wysyłane większość tweetów, znajdujące się na powitania word "Azure".

**toocreate gałąź skryptów i przekaż go tooAzure**

1. Otwórz program Windows PowerShell ISE.
2. Skopiuj hello następującego skryptu w okienku skryptów hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Ustaw hello najpierw dwie zmienne w skrypcie hello:

   | Zmienna | Opis |
   | --- | --- |
   |  $clusterName |Wprowadź nazwę klastra usługi HDInsight hello, w której mają toorun hello aplikacji. |
   |  $subscriptionID |Wprowadź swój identyfikator subskrypcji platformy Azure. |
   |  $sourceDataPath |Witaj gdzie zapytań programu Hive hello będzie odczytywać dane hello lokalizacji magazynu obiektów Blob platformy Azure. Nie trzeba toochange tej zmiennej. |
   |  $outputPath |Witaj lokalizacji magazynu obiektów Blob platformy Azure, gdzie zapytań programu Hive hello dane wyjściowe obejmują hello wyników. Nie trzeba toochange tej zmiennej. |
   |  $hqlScriptFile |Witaj lokalizację i nazwę pliku hello pliku skryptu hello HiveQL. Nie trzeba toochange tej zmiennej. |
4. Naciśnij klawisz **F5** toorun hello skryptu. Jeśli wystąpiły problemy, jako obejście, wybierz wszystkie wiersze hello, a następnie naciśnij klawisz **F8**.
5. Zostanie wyświetlona "Zakończ"! na końcu hello hello danych wyjściowych. Komunikaty o błędach pojawi się czerwone.

Jako procedury weryfikacji można sprawdzić pliku wyjściowego hello **/tutorials/twitter/twitter.hql**, w magazynie obiektów Blob platformy Azure za pomocą Eksploratora usługi storage platformy Azure lub programu Azure PowerShell. Aby uzyskać przykładowy skrypt programu Windows PowerShell do wyświetlania listy plików, zobacz [magazynu obiektów Blob użycia z usługą HDInsight][hdinsight-storage-powershell].

## <a name="process-twitter-data-by-using-hive"></a>Przetwarzaj dane Twitter przy użyciu usługi Hive
Zakończono wszystkie hello prac. Można teraz wywołać skryptu Hive hello i hello wyniki sprawdzenia.

### <a name="submit-a-hive-job"></a>Przesłać zadania technologii Hive
Użyj następującego skryptu Hive hello toorun skrypt programu Windows PowerShell hello. Konieczne będzie tooset hello pierwszej zmiennej.

> [!NOTE]
> Witaj toouse tweetów i skrypt HiveQL, który został przekazany w hello ostatnich dwóch sekcjach too"/tutorials/twitter/twitter.hql $hqlScriptFile zestaw hello". toouse hello te, które zostały przekazane tooa publicznego obiektu blob dla Ciebie, ustawić $hqlScriptFile także"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a>Sprawdzanie wyników hello
Użyj następującego skryptu programu Windows PowerShell, toocheck hello dane wyjściowe zadania Hive hello. Należy najpierw dwie zmienne hello tooset.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> tabelę programu Hive Hello używa \001 hello ogranicznik pola. Ogranicznik Hello nie jest widoczny w danych wyjściowych hello.

Po wyniki analizy hello zostały umieszczone w magazynie obiektów Blob platformy Azure, można wyeksportować hello danych tooan Azure SQL bazy danych/programu SQL server, wyeksportować hello tooExcel danych za pomocą dodatku Power Query lub połączyć dane toohello aplikacji przy użyciu hello Hive sterownik ODBC. Aby uzyskać więcej informacji, zobacz [Sqoop użycia z usługą HDInsight][hdinsight-use-sqoop], [analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-delay-data], [ Łączenie programu Excel tooHDInsight z dodatku Power Query][hdinsight-power-query], i [tooHDInsight łączenie programu Excel z hello sterownik Microsoft Hive ODBC][hdinsight-hive-odbc].

## <a name="next-steps"></a>Następne kroki
W tym samouczku zaobserwowano, jak tootransform bez struktury zestawu danych JSON w strukturze tooquery tabeli Hive Eksplorowanie i analizowanie danych z serwisem Twitter przy użyciu usługi HDInsight w systemie Azure. toolearn więcej, zobacz:

* [Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started]
* [Analizowanie w czasie rzeczywistym usługi Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight][hdinsight-hbase-twitter-sentiment]
* [Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-delay-data]
* [Łączenie programu Excel tooHDInsight z dodatku Power Query][hdinsight-power-query]
* [Łączenie programu Excel tooHDInsight z hello sterownik Microsoft Hive ODBC][hdinsight-hive-odbc]
* [Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
