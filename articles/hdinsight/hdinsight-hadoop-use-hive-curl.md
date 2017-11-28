---
title: "Hadoop Hive za pomocą Curl w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zdalnie przesyłania zadań Pig do usługi HDInsight przy użyciu programu Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 8a4f217b046121f85be0585eab18d90c44f21b9e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="701b2-103">Uruchamianie zapytań Hive z usługą Hadoop w usłudze HDInsight za pomocą usługi REST</span><span class="sxs-lookup"><span data-stu-id="701b2-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="701b2-104">Dowiedz się, jak uruchamianie zapytań Hive z usługą Hadoop w usłudze Azure HDInsight klastra za pomocą interfejsu API REST usługi WebHCat.</span><span class="sxs-lookup"><span data-stu-id="701b2-104">Learn how to use the WebHCat REST API to run Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="701b2-105">[Curl](http://curl.haxx.se/) służy do pokazują, jak można interakcję z usługą HDInsight przy użyciu pierwotne żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="701b2-105">[Curl](http://curl.haxx.se/) is used to demonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="701b2-106">[Jq](http://stedolan.github.io/jq/) narzędzie służy do przetwarzania danych JSON zwróconych z pozostałych żądań.</span><span class="sxs-lookup"><span data-stu-id="701b2-106">The [jq](http://stedolan.github.io/jq/) utility is used to process the JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="701b2-107">Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale dopiero zaczynasz korzystać z usługi HDInsight, zobacz [co należy wiedzieć o Hadoop w HDInsight opartych na systemie Linux](hdinsight-hadoop-linux-information.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="701b2-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see the [What you need to know about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="701b2-108"><a id="curl"></a>Uruchamianie zapytań Hive</span><span class="sxs-lookup"><span data-stu-id="701b2-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="701b2-109">Po użyciu cURL lub innego połączenia REST z usługą WebHCat, musi uwierzytelnić żądania, podając nazwę użytkownika i hasło administratora klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="701b2-109">When using cURL or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="701b2-110">W przypadku poleceń w tej sekcji należy zastąpić ciąg **USERNAME** nazwą użytkownika w celu dokonania uwierzytelnienia w klastrze oraz zastąpić ciąg **PASSWORD** hasłem do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="701b2-110">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="701b2-111">Zastąp ciąg **CLUSTERNAME** nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="701b2-111">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="701b2-112">Interfejs API REST jest zabezpieczony za pomocą [uwierzytelniania podstawowego](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="701b2-112">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="701b2-113">Aby upewnić się, że poświadczenia są bezpiecznie wysyłane do serwera, należy zawsze tworzyć żądania przy użyciu protokołu HTTP Secure (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="701b2-113">To help ensure that your credentials are securely sent to the server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="701b2-114">W wierszu polecenia wpisz następujące polecenie, aby sprawdzić możliwość nawiązania połączenia z klastrem usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="701b2-114">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="701b2-115">Pojawi się odpowiedź podobna do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="701b2-115">You receive a response similar to the following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="701b2-116">W tym poleceniu są używane następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="701b2-116">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="701b2-117">**-u** — nazwa użytkownika i hasło używane do uwierzytelnienia żądania.</span><span class="sxs-lookup"><span data-stu-id="701b2-117">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="701b2-118">**-G** — wskazuje, że to żądanie jest operacji GET.</span><span class="sxs-lookup"><span data-stu-id="701b2-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="701b2-119">Adres URL, na początek **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, jest taka sama dla wszystkich żądań.</span><span class="sxs-lookup"><span data-stu-id="701b2-119">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="701b2-120">Ścieżka, **/status**, wskazuje, czy żądanie jest próbę zwrócenia stanu usługi WebHCat (znanej także jako Templeton) dla serwera.</span><span class="sxs-lookup"><span data-stu-id="701b2-120">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> <span data-ttu-id="701b2-121">Możesz również poprosić o wersji programu Hive za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="701b2-121">You can also request the version of Hive by using the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="701b2-122">To żądanie zwraca odpowiedź podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="701b2-122">This request returns a response similar to the following text:</span></span>

       <span data-ttu-id="701b2-123">{"module": "hive", "version": "0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="701b2-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="701b2-124">Należy użyć następującego można utworzyć tabeli o nazwie **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="701b2-124">Use the following to create a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="701b2-125">Używane z tym żądaniem następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="701b2-125">The following parameters used with this request:</span></span>

   * <span data-ttu-id="701b2-126">**-d** — od `-G` nie jest używany domyślnie żądania metody POST.</span><span class="sxs-lookup"><span data-stu-id="701b2-126">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="701b2-127">`-d`Określa dane, które są wysyłane z żądania.</span><span class="sxs-lookup"><span data-stu-id="701b2-127">`-d` specifies the data values that are sent with the request.</span></span>

     * <span data-ttu-id="701b2-128">**User.name** — użytkownik, który uruchamia polecenie.</span><span class="sxs-lookup"><span data-stu-id="701b2-128">**user.name** - The user that is running the command.</span></span>
     * <span data-ttu-id="701b2-129">**wykonanie** -instrukcje HiveQL do wykonania.</span><span class="sxs-lookup"><span data-stu-id="701b2-129">**execute** - The HiveQL statements to execute.</span></span>
     * <span data-ttu-id="701b2-130">**statusdir** — stan tego zadania jest zapisywany w katalogu.</span><span class="sxs-lookup"><span data-stu-id="701b2-130">**statusdir** - The directory that the status for this job is written to.</span></span>

     <span data-ttu-id="701b2-131">Te instrukcje, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="701b2-131">These statements perform the following actions:</span></span>
   * <span data-ttu-id="701b2-132">**DROP TABLE** — Jeśli tabela już istnieje, jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="701b2-132">**DROP TABLE** - If the table already exists, it is deleted.</span></span>
   * <span data-ttu-id="701b2-133">**Tworzenie tabeli zewnętrznej** — tworzy nową tabelę "zewnętrzne" w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="701b2-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="701b2-134">Tabele zewnętrzne przechowywać tylko definicji tabeli w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="701b2-134">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="701b2-135">Dane pozostaną w oryginalnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="701b2-135">The data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="701b2-136">Jeśli oczekujesz zaktualizowania za pomocą zewnętrznego źródła danych, należy użyć tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="701b2-136">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="701b2-137">Na przykład procesu przekazywania danych lub inna operacja MapReduce.</span><span class="sxs-lookup"><span data-stu-id="701b2-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="701b2-138">Usunięcie tabeli zewnętrznej jest **nie** Usuń dane, definicję tabeli.</span><span class="sxs-lookup"><span data-stu-id="701b2-138">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="701b2-139">**FORMAT wiersza** — jak dane są sformatowane.</span><span class="sxs-lookup"><span data-stu-id="701b2-139">**ROW FORMAT** - How the data is formatted.</span></span> <span data-ttu-id="701b2-140">W każdym dzienniku pola są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="701b2-140">The fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="701b2-141">**PRZECHOWYWANE jako lokalizacji TEXTFILE** — przechowywania danych (katalog przykład/danych) i które są przechowywane jako tekst.</span><span class="sxs-lookup"><span data-stu-id="701b2-141">**STORED AS TEXTFILE LOCATION** - Where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="701b2-142">**Wybierz** -wybiera liczbę wszystkich wierszy gdzie kolumna **t4** zawiera wartość **[Błąd]**.</span><span class="sxs-lookup"><span data-stu-id="701b2-142">**SELECT** - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="701b2-143">Ta instrukcja zwraca wartość **3** są trzy wiersze, które zawierają tę wartość.</span><span class="sxs-lookup"><span data-stu-id="701b2-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="701b2-144">Należy zauważyć, że odstępy między instrukcje HiveQL są zastępowane przez `+` znak, gdy jest używany z Curl.</span><span class="sxs-lookup"><span data-stu-id="701b2-144">Notice that the spaces between HiveQL statements are replaced by the `+` character when used with Curl.</span></span> <span data-ttu-id="701b2-145">Wartości w cudzysłowie, które zawierać spacji, takich jak ogranicznik, nie powinna zostać zastąpiona przez `+`.</span><span class="sxs-lookup"><span data-stu-id="701b2-145">Quoted values that contain a space, such as the delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="701b2-146">**INPUT__FILE__NAME takich jak "% 25.log"** -niniejszych ogranicza wyszukiwanie do użycia tylko pliki kończy się rozszerzeniem. dziennika.</span><span class="sxs-lookup"><span data-stu-id="701b2-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits the search to only use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="701b2-147">`%25` Jest formą zakodowane w adresie URL %, więc jest stan aktualny `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="701b2-147">The `%25` is the URL encoded form of %, so the actual condition is `like '%.log'`.</span></span> <span data-ttu-id="701b2-148">% Musi być zakodowany, adres URL, ponieważ jest ona traktowana jako znak specjalny w adresach URL.</span><span class="sxs-lookup"><span data-stu-id="701b2-148">The % has to be URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="701b2-149">To polecenie powinien zwrócić identyfikator zadania, który może służyć do sprawdzania stanu zadania.</span><span class="sxs-lookup"><span data-stu-id="701b2-149">This command should return a job ID that can be used to check the status of the job.</span></span>

       <span data-ttu-id="701b2-150">{"id": "job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="701b2-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="701b2-151">Aby sprawdzić stan zadania, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="701b2-151">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="701b2-152">Zastąp **JOBID** o wartości zwracanej w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="701b2-152">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="701b2-153">Na przykład, jeśli była zwracana wartość `{"id":"job_1415651640909_0026"}`, następnie **JOBID** będzie `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="701b2-153">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="701b2-154">Jeśli zadanie zostało zakończone, stan jest **zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="701b2-154">If the job has finished, the state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="701b2-155">To żądanie Curl zwraca dokument JavaScript Object Notation (JSON), informacje o zadaniu.</span><span class="sxs-lookup"><span data-stu-id="701b2-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job.</span></span> <span data-ttu-id="701b2-156">Jq służy do pobierania wartości stan.</span><span class="sxs-lookup"><span data-stu-id="701b2-156">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="701b2-157">Gdy stan zadania został zmieniony na **zakończyło się pomyślnie**, wyniki zadania można pobrać z magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="701b2-157">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="701b2-158">`statusdir` Parametr przekazany z zapytaniem zawiera lokalizację pliku wyjściowego; w takim przypadku **/przykład/zwinięcie**.</span><span class="sxs-lookup"><span data-stu-id="701b2-158">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="701b2-159">Ten adres przechowuje dane wyjściowe w **przykład/zwinięcie** katalogu w magazynie domyślne klastrów.</span><span class="sxs-lookup"><span data-stu-id="701b2-159">This address stores the output in the **example/curl** directory in the clusters default storage.</span></span>

    <span data-ttu-id="701b2-160">Można wyświetlić listę i takie pliki należy pobierać za pomocą [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="701b2-160">You can list and download these files by using the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="701b2-161">Aby uzyskać więcej informacji na temat używania interfejsu wiersza polecenia Azure z usługą Azure Storage, zobacz [Użyj Azure CLI 2.0 z usługą Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="701b2-161">For more information on using the Azure CLI with Azure Storage, see the [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="701b2-162">Poniższe instrukcje umożliwiają utworzenie nowej tabeli "internal" o nazwie **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="701b2-162">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="701b2-163">Te instrukcje, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="701b2-163">These statements perform the following actions:</span></span>

   * <span data-ttu-id="701b2-164">**Utwórz Tabela Jeśli nie ISTNIEJE** — tworzy tabelę, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="701b2-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="701b2-165">Ta instrukcja tworzy wewnętrznej tabeli, która jest przechowywana w magazynie danych programu Hive i zarządza całkowicie Hive.</span><span class="sxs-lookup"><span data-stu-id="701b2-165">This statement creates an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="701b2-166">W przeciwieństwie do tabel zewnętrznych porzucenie wewnętrznej tabeli powoduje usunięcie danych źródłowych.</span><span class="sxs-lookup"><span data-stu-id="701b2-166">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="701b2-167">**ORC AS PRZECHOWYWANE** -przechowuje dane w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC).</span><span class="sxs-lookup"><span data-stu-id="701b2-167">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="701b2-168">ORC jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych gałęzi.</span><span class="sxs-lookup"><span data-stu-id="701b2-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="701b2-169">**ZASTĄP INSERT... Wybierz** -wybiera wiersze z **log4jLogs** tabeli, która zawiera **[Błąd]**, następnie wstawia dane do **errorLogs** tabeli.</span><span class="sxs-lookup"><span data-stu-id="701b2-169">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>
   * <span data-ttu-id="701b2-170">**Wybierz** -wybiera wszystkie wiersze z nową **errorLogs** tabeli.</span><span class="sxs-lookup"><span data-stu-id="701b2-170">**SELECT** - Selects all rows from the new **errorLogs** table.</span></span>

6. <span data-ttu-id="701b2-171">Za pomocą Identyfikatora zadanie zwracane w celu sprawdzenia stanu zadania.</span><span class="sxs-lookup"><span data-stu-id="701b2-171">Use the job ID returned to check the status of the job.</span></span> <span data-ttu-id="701b2-172">Po zakończyła się pomyślnie, użyj wiersza polecenia platformy Azure zgodnie z opisem wcześniej do pobrania i wyświetlenia wyników.</span><span class="sxs-lookup"><span data-stu-id="701b2-172">Once it has succeeded, use the Azure CLI as described previously to download and view the results.</span></span> <span data-ttu-id="701b2-173">Dane wyjściowe powinny zawierać trzy wiersze, które zawierają **[Błąd]**.</span><span class="sxs-lookup"><span data-stu-id="701b2-173">The output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="701b2-174"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="701b2-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="701b2-175">Ogólne informacje na temat programu Hive z HDInsight:</span><span class="sxs-lookup"><span data-stu-id="701b2-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="701b2-176">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="701b2-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="701b2-177">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="701b2-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="701b2-178">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="701b2-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="701b2-179">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="701b2-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="701b2-180">Jeśli używasz aplikacji Tez przy użyciu Hive, zobacz informacji o debugowaniu w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="701b2-180">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="701b2-181">Użyj widoku Ambari Tez w HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="701b2-181">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="701b2-182">Aby uzyskać więcej informacji dotyczących interfejsu API REST używany w tym dokumencie, zobacz [odwołania WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="701b2-182">For more information on the REST API used in this document, see the [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


