---
title: "Hadoop Sqoop za pomocą Curl w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zdalnie przesyłania zadań Sqoop do usługi HDInsight przy użyciu programu Curl."
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
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="3a7f6-103">Uruchamianie zadań Sqoop z platformą Hadoop w usłudze HDInsight z Curl</span><span class="sxs-lookup"><span data-stu-id="3a7f6-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="3a7f6-104">Dowiedz się, jak używać Curl do uruchomienia zadań Sqoop na klastra usługi Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="3a7f6-105">Zwinięcie służy do pokazują, jak można interakcję z usługą HDInsight przy użyciu pierwotne żądania HTTP można uruchamiać, monitorować i pobrać wyniki zadań Sqoop.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="3a7f6-106">To działanie przy użyciu usługi WebHCat interfejsu API REST (wcześniej znane jako Templeton) pochodzącymi z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="3a7f6-107">Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale dopiero zaczynasz korzystać z usługi HDInsight, zobacz [informacji na temat korzystania z usługi HDInsight w systemie Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="3a7f6-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3a7f6-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3a7f6-108">Prerequisites</span></span>
<span data-ttu-id="3a7f6-109">Aby wykonać kroki opisane w tym artykule, będą potrzebne następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3a7f6-109">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="3a7f6-110">Hadoop w klastrze usługi HDInsight (Linux lub z systemem Windows)</span><span class="sxs-lookup"><span data-stu-id="3a7f6-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="3a7f6-111">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="3a7f6-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="3a7f6-112">jq</span><span class="sxs-lookup"><span data-stu-id="3a7f6-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="3a7f6-113">Przesyłanie zadań Sqoop przy użyciu Curl</span><span class="sxs-lookup"><span data-stu-id="3a7f6-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="3a7f6-114">Używając programu Curl lub innego połączenia REST z usługą WebHCat, należy uwierzytelnić żądania, podając nazwę użytkownika i hasło administratora klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="3a7f6-115">Należy również użyć nazwy klastra jako części identyfikatora URI stosowanego przy wysyłaniu żądań do serwera.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="3a7f6-116">W przypadku poleceń w tej sekcji należy zastąpić ciąg **USERNAME** nazwą użytkownika w celu dokonania uwierzytelnienia w klastrze oraz zastąpić ciąg **PASSWORD** hasłem do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="3a7f6-117">Zastąp ciąg **CLUSTERNAME** nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-117">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="3a7f6-118">Interfejs API REST jest zabezpieczony za pomocą [uwierzytelniania podstawowego](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="3a7f6-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="3a7f6-119">Należy zawsze tworzyć żądania przy użyciu protokołu HTTPS (HTTP Secure), aby mieć pewność, że poświadczenia są bezpiecznie wysyłane do serwera.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="3a7f6-120">W wierszu polecenia wpisz następujące polecenie, aby sprawdzić możliwość nawiązania połączenia z klastrem usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3a7f6-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="3a7f6-121">Użytkownik powinien otrzymywać odpowiedź podobną do następującej:</span><span class="sxs-lookup"><span data-stu-id="3a7f6-121">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="3a7f6-122">W tym poleceniu są używane następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="3a7f6-122">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="3a7f6-123">**-u** — nazwa użytkownika i hasło używane do uwierzytelnienia żądania.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-123">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="3a7f6-124">**-G** — parametr wskazujący, że jest to żądanie GET.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="3a7f6-125">Adres URL, na początek **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, będą takie same dla wszystkich żądań.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="3a7f6-126">Ścieżka, **/status**, wskazuje, czy żądanie jest próbę zwrócenia stanu usługi WebHCat (znanej także jako Templeton) dla serwera.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="3a7f6-127">Poniższa tabela przedstawia zadania sqoop:</span><span class="sxs-lookup"><span data-stu-id="3a7f6-127">Use the following to submit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="3a7f6-128">W tym poleceniu są używane następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="3a7f6-128">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="3a7f6-129">**-d** — od `-G` nie jest używany domyślnie żądania metody POST.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="3a7f6-130">`-d`Określa dane, które są wysyłane z żądania.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-130">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="3a7f6-131">**User.name** — użytkownik, który uruchamia polecenie.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-131">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="3a7f6-132">**polecenie** -Sqoop polecenie do wykonania.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-132">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="3a7f6-133">**statusdir** -katalog, w którym zostanie zapisany stan dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-133">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="3a7f6-134">To polecenie powinien zwrócić identyfikator zadania, który może służyć do sprawdzania stanu zadania.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-134">This command should return a job ID that can be used to check the status of the job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="3a7f6-135">Aby sprawdzić stan zadania, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-135">To check the status of the job, use the following command.</span></span> <span data-ttu-id="3a7f6-136">Zastąp **JOBID** o wartości zwracanej w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-136">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="3a7f6-137">Na przykład, jeśli była zwracana wartość `{"id":"job_1415651640909_0026"}`, następnie **JOBID** będzie `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="3a7f6-138">Jeśli zadanie zostało zakończone, stan będzie **zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-138">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3a7f6-139">To żądanie Curl zwraca dokument JavaScript Object Notation (JSON), informacje o zadaniu; jq służy do pobierania wartości stan.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
2. <span data-ttu-id="3a7f6-140">Gdy stan zadania został zmieniony na **zakończyło się pomyślnie**, wyniki zadania można pobrać z magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="3a7f6-141">`statusdir` Parametr przekazany z zapytaniem zawiera lokalizację pliku wyjściowego; w takim przypadku **wasb: / / / przykład/zwinięcie**.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="3a7f6-142">Ten adres są przechowywane dane wyjściowe zadania w **przykład/zwinięcie** katalogu na domyślnego kontenera magazynu używane przez klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="3a7f6-143">Można wyświetlić listę i takie pliki należy pobierać za pomocą [interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3a7f6-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="3a7f6-144">Na przykład, aby wyświetlić listę plików w **przykład/zwinięcie**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="3a7f6-144">For example, to list files in **example/curl**, use the following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="3a7f6-145">Aby pobrać plik, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="3a7f6-145">To download a file, use the following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="3a7f6-146">Podaj nazwę konta magazynu zawierające obiektu blob przy użyciu `-a` i `-k` parametrów lub zestawu **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_dostępu\_klucza** zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="3a7f6-147">Zobacz < href = "hdinsight przekazywania data.md" target = "_blank", aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="3a7f6-148">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="3a7f6-148">Limitations</span></span>
* <span data-ttu-id="3a7f6-149">Zbiorcze export - opartych na systemie Linux z usługi HDInsight, łącznik Sqoop, używany do eksportowania danych do programu Microsoft SQL Server lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="3a7f6-150">Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop będzie wykonywać wiele operacji wstawienia zamiast przetwarzanie wsadowe operacji insert.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="3a7f6-151">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="3a7f6-151">Summary</span></span>
<span data-ttu-id="3a7f6-152">Jak pokazano w tym dokumencie, można użyć raw żądania HTTP można uruchamiać, monitorować i wyświetlić wyniki zadania Sqoop w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="3a7f6-153">Aby uzyskać więcej informacji dotyczących interfejsu REST używane w tym artykule, zobacz <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Podręcznik interfejsu API REST Sqoop</a>.</span><span class="sxs-lookup"><span data-stu-id="3a7f6-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a7f6-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3a7f6-154">Next steps</span></span>
<span data-ttu-id="3a7f6-155">Ogólne informacje na temat programu Hive z HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3a7f6-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="3a7f6-156">Używanie Sqoop z platformą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a7f6-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="3a7f6-157">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3a7f6-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="3a7f6-158">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a7f6-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3a7f6-159">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a7f6-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="3a7f6-160">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a7f6-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


