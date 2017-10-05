---
title: "Hadoop Pig za pomocą REST w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać REST do uruchomienia zadań Pig Latin na klastra usługi Hadoop w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a86864a779b0de1c6d5669cfbba0f3e1a27f1ff1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="ebca2-103">Uruchamianie zadań Pig z usługą Hadoop w usłudze HDInsight przy użyciu REST</span><span class="sxs-lookup"><span data-stu-id="ebca2-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="ebca2-104">Informacje o sposobie uruchamiania zadań Pig Latin dokonując REST żądań do klastra usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ebca2-104">Learn how to run Pig Latin jobs by making REST requests to an Azure HDInsight cluster.</span></span> <span data-ttu-id="ebca2-105">Zwinięcie służy do pokazują, jak można interakcję z usługą HDInsight przy użyciu interfejsu API REST usługi WebHCat.</span><span class="sxs-lookup"><span data-stu-id="ebca2-105">Curl is used to demonstrate how you can interact with HDInsight using the WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="ebca2-106">Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale dopiero zaczynasz korzystać z usługi HDInsight, zobacz [porady HDInsight opartych na systemie Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="ebca2-106">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="ebca2-107"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ebca2-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="ebca2-108">Klaster HDInsight Azure (na platformie Hadoop w usłudze HDInsight) (opartych na systemie Linux lub z systemem Windows)</span><span class="sxs-lookup"><span data-stu-id="ebca2-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ebca2-109">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="ebca2-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ebca2-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="ebca2-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="ebca2-111">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="ebca2-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="ebca2-112">jq</span><span class="sxs-lookup"><span data-stu-id="ebca2-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="ebca2-113"><a id="curl"></a>Uruchamianie zadań Pig przy użyciu Curl</span><span class="sxs-lookup"><span data-stu-id="ebca2-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="ebca2-114">Interfejs API REST jest zabezpieczony za pomocą [uwierzytelniania podstawowego dostępu](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="ebca2-114">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="ebca2-115">Zawsze tworzyć żądania przy użyciu HTTP Secure (HTTPS), aby upewnić się, że poświadczenia są bezpiecznie wysyłane do serwera.</span><span class="sxs-lookup"><span data-stu-id="ebca2-115">Always make requests by using Secure HTTP (HTTPS) to ensure that your credentials are securely sent to the server.</span></span>
>
> <span data-ttu-id="ebca2-116">Korzystając z polecenia w tej sekcji, Zastąp `USERNAME` z użytkownikiem w celu uwierzytelniania w klastrze i Zastąp `PASSWORD` hasłem do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ebca2-116">When using the commands in this section, replace `USERNAME` with the user to authenticate to the cluster, and replace `PASSWORD` with the password for the user account.</span></span> <span data-ttu-id="ebca2-117">Zastąp ciąg `CLUSTERNAME` nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="ebca2-117">Replace `CLUSTERNAME` with the name of your cluster.</span></span>
>


1. <span data-ttu-id="ebca2-118">W wierszu polecenia wpisz następujące polecenie, aby sprawdzić możliwość nawiązania połączenia z klastrem usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ebca2-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="ebca2-119">Powinien zostać wyświetlony następujący odpowiedź w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="ebca2-119">You should receive the following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="ebca2-120">W tym poleceniu są używane następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="ebca2-120">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="ebca2-121">**-u**: nazwa użytkownika i hasło używane do uwierzytelniania żądania</span><span class="sxs-lookup"><span data-stu-id="ebca2-121">**-u**: The user name and password used to authenticate the request</span></span>
    * <span data-ttu-id="ebca2-122">**-G**: wskazuje, że to żądanie jest żądanie pobrania</span><span class="sxs-lookup"><span data-stu-id="ebca2-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="ebca2-123">Adres URL, na początek **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, jest taka sama dla wszystkich żądań.</span><span class="sxs-lookup"><span data-stu-id="ebca2-123">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="ebca2-124">Ścieżka, **/status**, wskazuje, czy żądanie jest powoduje przywrócenie stanu usługi WebHCat (znanej także jako Templeton) dla serwera.</span><span class="sxs-lookup"><span data-stu-id="ebca2-124">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span></span>

2. <span data-ttu-id="ebca2-125">Aby przesłać zadanie Pig Latin do klastra, należy użyć poniższego kodu:</span><span class="sxs-lookup"><span data-stu-id="ebca2-125">Use the following code to submit a Pig Latin job to the cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="ebca2-126">W tym poleceniu są używane następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="ebca2-126">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="ebca2-127">**-d**: ponieważ `-G` nie jest używany domyślnie żądania metody POST.</span><span class="sxs-lookup"><span data-stu-id="ebca2-127">**-d**: Because `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="ebca2-128">`-d`Określa dane, które są wysyłane z żądania.</span><span class="sxs-lookup"><span data-stu-id="ebca2-128">`-d` specifies the data values that are sent with the request.</span></span>

    * <span data-ttu-id="ebca2-129">**User.name**: użytkownik, który uruchamia polecenie</span><span class="sxs-lookup"><span data-stu-id="ebca2-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="ebca2-130">**wykonanie**: instrukcje Pig Latin wykonanie</span><span class="sxs-lookup"><span data-stu-id="ebca2-130">**execute**: The Pig Latin statements to execute</span></span>
    * <span data-ttu-id="ebca2-131">**statusdir**: stan tego zadania jest zapisywany w katalogu</span><span class="sxs-lookup"><span data-stu-id="ebca2-131">**statusdir**: The directory that the status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="ebca2-132">Należy zauważyć, że zastępuje spacje w instrukcjach Pig Latin `+` znak, gdy jest używany z Curl.</span><span class="sxs-lookup"><span data-stu-id="ebca2-132">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span></span>

    <span data-ttu-id="ebca2-133">To polecenie powinny zostać zwrócone identyfikator zadania, który może służyć do sprawdzania stanu zadania, na przykład:</span><span class="sxs-lookup"><span data-stu-id="ebca2-133">This command should return a job ID that can be used to check the status of the job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="ebca2-134">Aby sprawdzić stan zadania, użyj następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="ebca2-134">To check the status of the job, use the following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="ebca2-135">Zastąp `JOBID` o wartości zwracanej w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="ebca2-135">Replace `JOBID` with the value returned in the previous step.</span></span> <span data-ttu-id="ebca2-136">Na przykład, jeśli była zwracana wartość `{"id":"job_1415651640909_0026"}`, następnie `JOBID` jest `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="ebca2-136">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="ebca2-137">Jeśli zadanie zostało zakończone, stan jest **zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="ebca2-137">If the job has finished, the state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ebca2-138">To żądanie Curl zwraca dokument JavaScript Object Notation (JSON), informacje o zadaniu i jq służy do pobierania wartości stan.</span><span class="sxs-lookup"><span data-stu-id="ebca2-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span></span>

## <span data-ttu-id="ebca2-139"><a id="results"></a>Wyświetl wyniki</span><span class="sxs-lookup"><span data-stu-id="ebca2-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="ebca2-140">Gdy stan zadania został zmieniony na **zakończyło się pomyślnie**, można pobrać wyniki zadania.</span><span class="sxs-lookup"><span data-stu-id="ebca2-140">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job.</span></span> <span data-ttu-id="ebca2-141">`statusdir` Parametr przekazany z zapytaniem zawiera lokalizację pliku wyjściowego; w takim przypadku `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="ebca2-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="ebca2-142">HDInsight można użyć usługi Azure Storage lub usługi Azure Data Lake Store jako domyślnego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="ebca2-142">HDInsight can use either Azure Storage or Azure Data Lake Store as the default data store.</span></span> <span data-ttu-id="ebca2-143">Istnieją różne sposoby uzyskania danych, w zależności od tego, która z nich korzystać.</span><span class="sxs-lookup"><span data-stu-id="ebca2-143">There are various ways to get at the data depending on which one you use.</span></span> <span data-ttu-id="ebca2-144">Aby uzyskać więcej informacji, zobacz sekcję magazynu [informacji opartą na systemie Linux usługą HDInsight](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="ebca2-144">For more information, see the storage section of the [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="ebca2-145"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="ebca2-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="ebca2-146">Jak pokazano w tym dokumencie, można użyć raw żądania HTTP można uruchamiać, monitorować i wyświetlić wyniki zadań Pig w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ebca2-146">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="ebca2-147">Aby uzyskać więcej informacji na temat interfejsu REST używane w tym artykule, zobacz [odwołania WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="ebca2-147">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="ebca2-148"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ebca2-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ebca2-149">Aby uzyskać ogólne informacje na temat Pig w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ebca2-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="ebca2-150">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebca2-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="ebca2-151">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ebca2-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ebca2-152">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebca2-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ebca2-153">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebca2-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
