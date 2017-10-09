---
title: "aaaUse Hadoop Hive z Curl w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przesyłania tooremotely Pig zadania tooHDInsight przy użyciu programu Curl."
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
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="eec52-103">Uruchamianie zapytań Hive z usługą Hadoop w usłudze HDInsight za pomocą usługi REST</span><span class="sxs-lookup"><span data-stu-id="eec52-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="eec52-104">Dowiedz się, jak toouse hello interfejsu API REST usługi WebHCat toorun Hive zapytania Hadoop w usłudze Azure HDInsight klastrze.</span><span class="sxs-lookup"><span data-stu-id="eec52-104">Learn how toouse hello WebHCat REST API toorun Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="eec52-105">[Curl](http://curl.haxx.se/) jest używane toodemonstrate, jak można interakcję z usługą HDInsight przy użyciu pierwotne żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="eec52-105">[Curl](http://curl.haxx.se/) is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="eec52-106">Witaj [jq](http://stedolan.github.io/jq/) narzędzie jest używane tooprocess hello JSON zwrócono dane z żądania REST.</span><span class="sxs-lookup"><span data-stu-id="eec52-106">hello [jq](http://stedolan.github.io/jq/) utility is used tooprocess hello JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="eec52-107">Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale są nowe tooHDInsight, zobacz hello [potrzebnych tooknow dotyczące usługi Hadoop w HDInsight opartych na systemie Linux](hdinsight-hadoop-linux-information.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="eec52-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see hello [What you need tooknow about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="eec52-108"><a id="curl"></a>Uruchamianie zapytań Hive</span><span class="sxs-lookup"><span data-stu-id="eec52-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="eec52-109">Po za pomocą cURL lub innego połączenia REST z usługą WebHCat, zapewniając hello nazwę użytkownika i hasło administratora klastra usługi HDInsight hello musi uwierzytelnić się hello żądania.</span><span class="sxs-lookup"><span data-stu-id="eec52-109">When using cURL or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="eec52-110">Hello poleceń w tej sekcji, Zastąp **USERNAME** hello użytkownika tooauthenticate toohello klastra i Zastąp **hasło** hello hasła dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="eec52-110">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="eec52-111">Zastąp **CLUSTERNAME** o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="eec52-111">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="eec52-112">Witaj interfejsu API REST jest zabezpieczony za pomocą [uwierzytelnianie podstawowe](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="eec52-112">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="eec52-113">toohelp upewnij się, że poświadczenia są bezpiecznie wysyłane toohello server, zawsze tworzyć żądania przy użyciu protokołu HTTP Secure (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="eec52-113">toohelp ensure that your credentials are securely sent toohello server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="eec52-114">Z wiersza polecenia użyj hello następujące polecenia tooverify, że możesz połączyć tooyour klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="eec52-114">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="eec52-115">Pojawi się odpowiedź toohello podobne, następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="eec52-115">You receive a response similar toohello following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="eec52-116">Parametry Hello używane w tym poleceniu są następujące:</span><span class="sxs-lookup"><span data-stu-id="eec52-116">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="eec52-117">**-u** -hello nazwę użytkownika i hasło używane tooauthenticate hello żądania.</span><span class="sxs-lookup"><span data-stu-id="eec52-117">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="eec52-118">**-G** — wskazuje, że to żądanie jest operacji GET.</span><span class="sxs-lookup"><span data-stu-id="eec52-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="eec52-119">Witaj rozpoczęciem powitalne adresu URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, jest hello takie same dla wszystkich żądań.</span><span class="sxs-lookup"><span data-stu-id="eec52-119">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="eec52-120">Ścieżka Hello **/status**, wskazuje, że Żądanie hello jest tooreturn stan usługi WebHCat (znanej także jako Templeton) powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="eec52-120">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> <span data-ttu-id="eec52-121">Możesz również zażądać hello wersję gałęzi przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eec52-121">You can also request hello version of Hive by using hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="eec52-122">To żądanie zwraca odpowiedź toohello podobne, następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="eec52-122">This request returns a response similar toohello following text:</span></span>

       <span data-ttu-id="eec52-123">{"module": "hive", "version": "0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="eec52-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="eec52-124">Użyj powitania po toocreate tabela o nazwie **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="eec52-124">Use hello following toocreate a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="eec52-125">następujące parametry używane z tym żądaniem Hello:</span><span class="sxs-lookup"><span data-stu-id="eec52-125">hello following parameters used with this request:</span></span>

   * <span data-ttu-id="eec52-126">**-d** — od `-G` nie jest używany, domyślnie przyjmowana jest hello żądania metody POST toohello.</span><span class="sxs-lookup"><span data-stu-id="eec52-126">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="eec52-127">`-d`Określa hello wartości danych, które są wysyłane z żądania hello.</span><span class="sxs-lookup"><span data-stu-id="eec52-127">`-d` specifies hello data values that are sent with hello request.</span></span>

     * <span data-ttu-id="eec52-128">**User.name** -hello użytkownik, który uruchamia polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="eec52-128">**user.name** - hello user that is running hello command.</span></span>
     * <span data-ttu-id="eec52-129">**wykonanie** — Witaj tooexecute instrukcje HiveQL.</span><span class="sxs-lookup"><span data-stu-id="eec52-129">**execute** - hello HiveQL statements tooexecute.</span></span>
     * <span data-ttu-id="eec52-130">**statusdir** -hello katalogu, w którym hello stanu dla tego zadania jest zapisywany.</span><span class="sxs-lookup"><span data-stu-id="eec52-130">**statusdir** - hello directory that hello status for this job is written to.</span></span>

     <span data-ttu-id="eec52-131">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="eec52-131">These statements perform hello following actions:</span></span>
   * <span data-ttu-id="eec52-132">**DROP TABLE** — Jeśli hello tabela już istnieje, jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="eec52-132">**DROP TABLE** - If hello table already exists, it is deleted.</span></span>
   * <span data-ttu-id="eec52-133">**Tworzenie tabeli zewnętrznej** — tworzy nową tabelę "zewnętrzne" w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="eec52-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="eec52-134">Tabele zewnętrzne przechowywać tylko hello definicji tabeli w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="eec52-134">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="eec52-135">Hello danych pozostaje w hello oryginalnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="eec52-135">hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="eec52-136">Jeśli oczekujesz hello zaktualizowane przez źródło zewnętrzne podstawowej toobe danych należy użyć tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="eec52-136">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="eec52-137">Na przykład procesu przekazywania danych lub inna operacja MapReduce.</span><span class="sxs-lookup"><span data-stu-id="eec52-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="eec52-138">Usunięcie tabeli zewnętrznej jest **nie** usunąć dane hello, tylko hello definicji tabeli.</span><span class="sxs-lookup"><span data-stu-id="eec52-138">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="eec52-139">**FORMAT wiersza** — sposób formatowania danych hello.</span><span class="sxs-lookup"><span data-stu-id="eec52-139">**ROW FORMAT** - How hello data is formatted.</span></span> <span data-ttu-id="eec52-140">Witaj pól w każdym dzienniku są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="eec52-140">hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="eec52-141">**PRZECHOWYWANE jako lokalizacji TEXTFILE** — w przypadku, gdy są przechowywane dane hello (katalog hello przykład/danych) i które są przechowywane jako tekst.</span><span class="sxs-lookup"><span data-stu-id="eec52-141">**STORED AS TEXTFILE LOCATION** - Where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="eec52-142">**Wybierz** -wybiera liczbę wszystkich wierszy gdzie kolumna **t4** zawiera wartość hello **[Błąd]**.</span><span class="sxs-lookup"><span data-stu-id="eec52-142">**SELECT** - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="eec52-143">Ta instrukcja zwraca wartość **3** są trzy wiersze, które zawierają tę wartość.</span><span class="sxs-lookup"><span data-stu-id="eec52-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="eec52-144">Zwróć uwagę, hello spacji między instrukcje HiveQL zastępuje hello `+` znak, gdy jest używany z Curl.</span><span class="sxs-lookup"><span data-stu-id="eec52-144">Notice that hello spaces between HiveQL statements are replaced by hello `+` character when used with Curl.</span></span> <span data-ttu-id="eec52-145">Wartości w cudzysłowie, zawierające spację, takich jak ogranicznik hello nie powinna zostać zastąpiona przez `+`.</span><span class="sxs-lookup"><span data-stu-id="eec52-145">Quoted values that contain a space, such as hello delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="eec52-146">**INPUT__FILE__NAME takich jak '% 25.log'** — ta instrukcja limity hello wyszukiwania tooonly używanych plików kończy się rozszerzeniem. dziennika.</span><span class="sxs-lookup"><span data-stu-id="eec52-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits hello search tooonly use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="eec52-147">Witaj `%25` jest hello zakodowane w adresie URL formularza %, więc warunek rzeczywiste hello jest `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="eec52-147">hello `%25` is hello URL encoded form of %, so hello actual condition is `like '%.log'`.</span></span> <span data-ttu-id="eec52-148">Hello % ma URL toobe zakodowane, ponieważ jest ona traktowana jako znak specjalny w adresach URL.</span><span class="sxs-lookup"><span data-stu-id="eec52-148">hello % has toobe URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="eec52-149">To polecenie powinien zwrócić Identyfikatora zadania, które mogą być używane toocheck stan hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="eec52-149">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

       <span data-ttu-id="eec52-150">{"id": "job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="eec52-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="eec52-151">Stan hello toocheck hello zadania, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="eec52-151">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="eec52-152">Zastąp **JOBID** z wartością hello zwracane w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="eec52-152">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="eec52-153">Na przykład jeśli hello zwrócona została wartość `{"id":"job_1415651640909_0026"}`, następnie **JOBID** będzie `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="eec52-153">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="eec52-154">Jeśli hello zadanie zostało zakończone, stan hello jest **zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="eec52-154">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="eec52-155">To żądanie Curl zwraca dokument JavaScript Object Notation (JSON), informacje o zadaniu hello.</span><span class="sxs-lookup"><span data-stu-id="eec52-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job.</span></span> <span data-ttu-id="eec52-156">Służy Jq tooretrieve hello tylko wartość stanu.</span><span class="sxs-lookup"><span data-stu-id="eec52-156">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="eec52-157">Gdy stan hello hello zadania został zmieniony zbyt**zakończyło się pomyślnie**, hello wyników zadania hello można pobrać z magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eec52-157">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="eec52-158">Witaj `statusdir` przekazany parametr zapytania o hello zawiera lokalizację hello hello pliku wyjściowego; w takim przypadku **/przykład/zwinięcie**.</span><span class="sxs-lookup"><span data-stu-id="eec52-158">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="eec52-159">Ten adres są przechowywane dane wyjściowe hello w hello **przykład/zwinięcie** katalogu w hello klastrów domyślnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="eec52-159">This address stores hello output in hello **example/curl** directory in hello clusters default storage.</span></span>

    <span data-ttu-id="eec52-160">Można wyświetlić listę i takie pliki należy pobierać za pomocą hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eec52-160">You can list and download these files by using hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="eec52-161">Aby uzyskać więcej informacji na temat używania hello wiersza polecenia platformy Azure z usługą Azure Storage, zobacz hello [Użyj Azure CLI 2.0 z usługą Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="eec52-161">For more information on using hello Azure CLI with Azure Storage, see hello [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="eec52-162">Użyj hello następujące instrukcje toocreate nową tabelę "internal" o nazwie **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="eec52-162">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="eec52-163">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="eec52-163">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="eec52-164">**Utwórz Tabela Jeśli nie ISTNIEJE** — tworzy tabelę, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="eec52-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="eec52-165">Ta instrukcja tworzy wewnętrznej tabeli, który jest przechowywany w magazynie danych Hive hello i zarządza całkowicie Hive.</span><span class="sxs-lookup"><span data-stu-id="eec52-165">This statement creates an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="eec52-166">W przeciwieństwie do tabel zewnętrznych porzucenie wewnętrznej tabeli usuwa hello również danych źródłowych.</span><span class="sxs-lookup"><span data-stu-id="eec52-166">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="eec52-167">**ORC AS PRZECHOWYWANE** -przechowuje dane hello w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC).</span><span class="sxs-lookup"><span data-stu-id="eec52-167">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="eec52-168">ORC jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych gałęzi.</span><span class="sxs-lookup"><span data-stu-id="eec52-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="eec52-169">**ZASTĄP INSERT... Wybierz** -wybiera wiersze z hello **log4jLogs** tabeli, która zawiera **[Błąd]**, a następnie wstawia hello danych do hello **errorLogs** tabeli.</span><span class="sxs-lookup"><span data-stu-id="eec52-169">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>
   * <span data-ttu-id="eec52-170">**Wybierz** -wybiera wszystkie wiersze z nowego hello **errorLogs** tabeli.</span><span class="sxs-lookup"><span data-stu-id="eec52-170">**SELECT** - Selects all rows from hello new **errorLogs** table.</span></span>

6. <span data-ttu-id="eec52-171">Za pomocą Identyfikatora zadania hello zwrócił stan hello toocheck hello zadania.</span><span class="sxs-lookup"><span data-stu-id="eec52-171">Use hello job ID returned toocheck hello status of hello job.</span></span> <span data-ttu-id="eec52-172">Po zakończyła się pomyślnie, należy użyć wiersza polecenia platformy Azure, jak opisano wcześniej toodownload i wyświetlania wyników hello hello.</span><span class="sxs-lookup"><span data-stu-id="eec52-172">Once it has succeeded, use hello Azure CLI as described previously toodownload and view hello results.</span></span> <span data-ttu-id="eec52-173">dane wyjściowe Hello powinien zawierać trzy wiersze, które zawierają **[Błąd]**.</span><span class="sxs-lookup"><span data-stu-id="eec52-173">hello output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="eec52-174"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eec52-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="eec52-175">Ogólne informacje na temat programu Hive z HDInsight:</span><span class="sxs-lookup"><span data-stu-id="eec52-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="eec52-176">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="eec52-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="eec52-177">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="eec52-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="eec52-178">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="eec52-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="eec52-179">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="eec52-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="eec52-180">Jeśli używasz aplikacji Tez przy użyciu Hive, zobacz powitania po dokumentów dla informacji debugowania:</span><span class="sxs-lookup"><span data-stu-id="eec52-180">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="eec52-181">Użyj hello widoku Ambari Tez w HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="eec52-181">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="eec52-182">Aby uzyskać więcej informacji na powitania interfejsu API REST używany w tym dokumencie, zobacz hello [odwołania WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="eec52-182">For more information on hello REST API used in this document, see hello [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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


