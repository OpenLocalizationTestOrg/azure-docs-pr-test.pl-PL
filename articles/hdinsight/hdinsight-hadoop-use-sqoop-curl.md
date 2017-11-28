---
title: "aaaUse Hadoop Sqoop z Curl w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooremotely przesłać tooHDInsight zadania Sqoop przy użyciu programu Curl."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="008e7-103">Uruchamianie zadań Sqoop z platformą Hadoop w usłudze HDInsight z Curl</span><span class="sxs-lookup"><span data-stu-id="008e7-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="008e7-104">Dowiedz się, jak klastra toouse Curl toorun Sqoop zadania na platformie Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="008e7-104">Learn how toouse Curl toorun Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="008e7-105">Zwinięcie jest używane toodemonstrate sposób można interakcji z usługą HDInsight przy użyciu raw toorun żądania HTTP, monitor i pobrać hello wyniki zadań Sqoop.</span><span class="sxs-lookup"><span data-stu-id="008e7-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun, monitor, and retrieve hello results of Sqoop jobs.</span></span> <span data-ttu-id="008e7-106">To działanie za pomocą hello WebHCat interfejsu API REST (wcześniej znane jako Templeton) pochodzącymi z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="008e7-106">This works by using hello WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="008e7-107">Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale są nowe tooHDInsight, zobacz [informacji na temat korzystania z usługi HDInsight w systemie Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="008e7-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="008e7-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="008e7-108">Prerequisites</span></span>
<span data-ttu-id="008e7-109">toocomplete hello kroki opisane w tym artykule, będą potrzebne następujące hello:</span><span class="sxs-lookup"><span data-stu-id="008e7-109">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="008e7-110">Hadoop w klastrze usługi HDInsight (Linux lub z systemem Windows)</span><span class="sxs-lookup"><span data-stu-id="008e7-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="008e7-111">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="008e7-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="008e7-112">jq</span><span class="sxs-lookup"><span data-stu-id="008e7-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="008e7-113">Przesyłanie zadań Sqoop przy użyciu Curl</span><span class="sxs-lookup"><span data-stu-id="008e7-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="008e7-114">Po za pomocą Curl lub innego połączenia REST z usługą WebHCat, zapewniając hello nazwę użytkownika i hasło administratora klastra usługi HDInsight hello musi uwierzytelnić się hello żądania.</span><span class="sxs-lookup"><span data-stu-id="008e7-114">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="008e7-115">Należy również użyć nazwy klastra hello jako część hello identyfikator URI (Uniform Resource) używane toosend hello żądań toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="008e7-115">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server.</span></span>
> 
> <span data-ttu-id="008e7-116">Hello poleceń w tej sekcji, Zastąp **USERNAME** hello użytkownika tooauthenticate toohello klastra i Zastąp **hasło** hello hasła dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="008e7-116">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="008e7-117">Zastąp **CLUSTERNAME** o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="008e7-117">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
> 
> <span data-ttu-id="008e7-118">Witaj interfejsu API REST jest zabezpieczony za pomocą [uwierzytelnianie podstawowe](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="008e7-118">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="008e7-119">Należy zawsze tworzyć żądania przy użyciu HTTPS (HTTP Secure) toohelp upewnij się, że poświadczenia są bezpiecznie wysyłane toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="008e7-119">You should always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>
> 
> 

1. <span data-ttu-id="008e7-120">Z wiersza polecenia użyj hello następujące polecenia tooverify, że możesz połączyć tooyour klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="008e7-120">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="008e7-121">Powinien zostać wyświetlony poniżej toohello podobne odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="008e7-121">You should receive a response similar toohello following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="008e7-122">Parametry Hello używane w tym poleceniu są następujące:</span><span class="sxs-lookup"><span data-stu-id="008e7-122">hello parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="008e7-123">**-u** -hello nazwę użytkownika i hasło używane tooauthenticate hello żądania.</span><span class="sxs-lookup"><span data-stu-id="008e7-123">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="008e7-124">**-G** — parametr wskazujący, że jest to żądanie GET.</span><span class="sxs-lookup"><span data-stu-id="008e7-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="008e7-125">Witaj rozpoczęciem powitalne adresu URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, będzie hello takie same dla wszystkich żądań.</span><span class="sxs-lookup"><span data-stu-id="008e7-125">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be hello same for all requests.</span></span> <span data-ttu-id="008e7-126">Ścieżka Hello **/status**, wskazuje, że Żądanie hello jest tooreturn stan usługi WebHCat (znanej także jako Templeton) powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="008e7-126">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> 
2. <span data-ttu-id="008e7-127">Użyj powitania po toosubmit zadania sqoop:</span><span class="sxs-lookup"><span data-stu-id="008e7-127">Use hello following toosubmit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="008e7-128">Parametry Hello używane w tym poleceniu są następujące:</span><span class="sxs-lookup"><span data-stu-id="008e7-128">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="008e7-129">**-d** — od `-G` nie jest używany, domyślnie przyjmowana jest hello żądania metody POST toohello.</span><span class="sxs-lookup"><span data-stu-id="008e7-129">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="008e7-130">`-d`Określa hello wartości danych, które są wysyłane z żądania hello.</span><span class="sxs-lookup"><span data-stu-id="008e7-130">`-d` specifies hello data values that are sent with hello request.</span></span>

        * <span data-ttu-id="008e7-131">**User.name** -hello użytkownik, który uruchamia polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="008e7-131">**user.name** - hello user that is running hello command.</span></span>

        * <span data-ttu-id="008e7-132">**polecenie** — Witaj tooexecute polecenia Sqoop.</span><span class="sxs-lookup"><span data-stu-id="008e7-132">**command** - hello Sqoop command tooexecute.</span></span>

        * <span data-ttu-id="008e7-133">**statusdir** -hello katalogu, w którym hello stanu dla tego zadania zostanie zapisany.</span><span class="sxs-lookup"><span data-stu-id="008e7-133">**statusdir** - hello directory that hello status for this job will be written to.</span></span>

    <span data-ttu-id="008e7-134">To polecenie powinien zwrócić Identyfikatora zadania, które mogą być używane toocheck stan hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="008e7-134">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="008e7-135">Stan hello toocheck hello zadania, hello Użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="008e7-135">toocheck hello status of hello job, use hello following command.</span></span> <span data-ttu-id="008e7-136">Zastąp **JOBID** z wartością hello zwracane w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="008e7-136">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="008e7-137">Na przykład jeśli hello zwrócona została wartość `{"id":"job_1415651640909_0026"}`, następnie **JOBID** będzie `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="008e7-137">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="008e7-138">Jeśli hello zadanie zostało zakończone, stan hello zostanie **zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="008e7-138">If hello job has finished, hello state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="008e7-139">To żądanie Curl zwraca dokument JavaScript Object Notation (JSON), informacje o zadaniu hello; Służy jq tooretrieve hello tylko wartość stanu.</span><span class="sxs-lookup"><span data-stu-id="008e7-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job; jq is used tooretrieve only hello state value.</span></span>
   > 
   > 
2. <span data-ttu-id="008e7-140">Gdy stan hello hello zadania został zmieniony zbyt**zakończyło się pomyślnie**, hello wyników zadania hello można pobrać z magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="008e7-140">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="008e7-141">Witaj `statusdir` przekazany parametr zapytania o hello zawiera lokalizację hello hello pliku wyjściowego; w takim przypadku **wasb: / / / przykład/zwinięcie**.</span><span class="sxs-lookup"><span data-stu-id="008e7-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="008e7-142">Ten adres są przechowywane dane wyjściowe hello hello zadania w hello **przykład/zwinięcie** katalogu na powitania domyślnego kontenera magazynu używane przez klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="008e7-142">This address stores hello output of hello job in hello **example/curl** directory on hello default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="008e7-143">Można wyświetlić listę i takie pliki należy pobierać za pomocą hello [interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="008e7-143">You can list and download these files by using hello [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="008e7-144">Na przykład pliki toolist w **przykład/zwinięcie**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="008e7-144">For example, toolist files in **example/curl**, use hello following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="008e7-145">toodownload plik, użyj następujących hello:</span><span class="sxs-lookup"><span data-stu-id="008e7-145">toodownload a file, use hello following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="008e7-146">Należy określić nazwy konta magazynu hello zawierającej hello obiektów blob przy użyciu hello `-a` i `-k` parametrów lub zestaw hello **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_dostępu\_klucza** zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="008e7-146">You must either specify hello storage account name that contains hello blob by using hello `-a` and `-k` parameters, or set hello **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="008e7-147">Zobacz < href = "hdinsight przekazywania data.md" target = "_blank", aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="008e7-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="008e7-148">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="008e7-148">Limitations</span></span>
* <span data-ttu-id="008e7-149">Masowo export - HDInsight opartych na systemie Linux z, hello Sqoop łącznik używany tooexport danych tooMicrosoft serwera SQL lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.</span><span class="sxs-lookup"><span data-stu-id="008e7-149">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="008e7-150">Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu hello `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop będzie wykonywać wiele operacji wstawienia zamiast przetwarzanie wsadowe hello operacje wstawiania.</span><span class="sxs-lookup"><span data-stu-id="008e7-150">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="008e7-151">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="008e7-151">Summary</span></span>
<span data-ttu-id="008e7-152">Jak pokazano w tym dokumencie, można użyć raw toorun żądania HTTP, monitor i wyświetlić wyniki hello Sqoop zadań w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="008e7-152">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="008e7-153">Aby uzyskać więcej informacji na interfejsie REST hello używane w tym artykule, zobacz hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Podręcznik interfejsu API REST Sqoop</a>.</span><span class="sxs-lookup"><span data-stu-id="008e7-153">For more information on hello REST interface used in this article, see hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="008e7-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="008e7-154">Next steps</span></span>
<span data-ttu-id="008e7-155">Ogólne informacje na temat programu Hive z HDInsight:</span><span class="sxs-lookup"><span data-stu-id="008e7-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="008e7-156">Używanie Sqoop z platformą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="008e7-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="008e7-157">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="008e7-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="008e7-158">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="008e7-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="008e7-159">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="008e7-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="008e7-160">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="008e7-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


