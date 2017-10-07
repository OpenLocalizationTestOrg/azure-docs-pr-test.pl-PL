---
title: "aaaUse Hadoop z języka Pig z REST w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klastra toouse REST toorun Pig Latin zadania na platformie Hadoop w usłudze Azure HDInsight."
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
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="47c4f-103">Uruchamianie zadań Pig z usługą Hadoop w usłudze HDInsight przy użyciu REST</span><span class="sxs-lookup"><span data-stu-id="47c4f-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="47c4f-104">Dowiedz się, jak toorun Pig Latin zadania przez klaster Azure HDInsight tooan żądań REST.</span><span class="sxs-lookup"><span data-stu-id="47c4f-104">Learn how toorun Pig Latin jobs by making REST requests tooan Azure HDInsight cluster.</span></span> <span data-ttu-id="47c4f-105">Zwinięcie jest używane toodemonstrate sposób można interakcji z usługą HDInsight przy użyciu interfejsu API REST usługi WebHCat hello.</span><span class="sxs-lookup"><span data-stu-id="47c4f-105">Curl is used toodemonstrate how you can interact with HDInsight using hello WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="47c4f-106">Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale są nowe tooHDInsight, zobacz [porady HDInsight opartych na systemie Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="47c4f-106">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="47c4f-107"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="47c4f-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="47c4f-108">Klaster HDInsight Azure (na platformie Hadoop w usłudze HDInsight) (opartych na systemie Linux lub z systemem Windows)</span><span class="sxs-lookup"><span data-stu-id="47c4f-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="47c4f-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="47c4f-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="47c4f-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="47c4f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="47c4f-111">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="47c4f-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="47c4f-112">jq</span><span class="sxs-lookup"><span data-stu-id="47c4f-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="47c4f-113"><a id="curl"></a>Uruchamianie zadań Pig przy użyciu Curl</span><span class="sxs-lookup"><span data-stu-id="47c4f-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="47c4f-114">Witaj interfejsu API REST jest zabezpieczony za pomocą [uwierzytelniania podstawowego dostępu](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="47c4f-114">hello REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="47c4f-115">Zawsze tworzyć żądania przy użyciu tooensure HTTP Secure (HTTPS), że poświadczenia są bezpiecznie wysyłane toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="47c4f-115">Always make requests by using Secure HTTP (HTTPS) tooensure that your credentials are securely sent toohello server.</span></span>
>
> <span data-ttu-id="47c4f-116">Korzystając z polecenia hello w tej sekcji, Zastąp `USERNAME` hello użytkownika tooauthenticate toohello klastra i Zastąp `PASSWORD` hello hasła dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="47c4f-116">When using hello commands in this section, replace `USERNAME` with hello user tooauthenticate toohello cluster, and replace `PASSWORD` with hello password for hello user account.</span></span> <span data-ttu-id="47c4f-117">Zastąp `CLUSTERNAME` o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="47c4f-117">Replace `CLUSTERNAME` with hello name of your cluster.</span></span>
>


1. <span data-ttu-id="47c4f-118">Z wiersza polecenia użyj hello następujące polecenia tooverify, że możesz połączyć tooyour klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="47c4f-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="47c4f-119">Powinien zostać wyświetlony powitania po JSON odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="47c4f-119">You should receive hello following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="47c4f-120">Parametry Hello używane w tym poleceniu są następujące:</span><span class="sxs-lookup"><span data-stu-id="47c4f-120">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="47c4f-121">**-u**: hello nazwę użytkownika i hasło używane tooauthenticate hello żądania</span><span class="sxs-lookup"><span data-stu-id="47c4f-121">**-u**: hello user name and password used tooauthenticate hello request</span></span>
    * <span data-ttu-id="47c4f-122">**-G**: wskazuje, że to żądanie jest żądanie pobrania</span><span class="sxs-lookup"><span data-stu-id="47c4f-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="47c4f-123">Witaj rozpoczęciem powitalne adresu URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, jest hello takie same dla wszystkich żądań.</span><span class="sxs-lookup"><span data-stu-id="47c4f-123">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="47c4f-124">Ścieżka Hello **/status**, oznacza to Żądanie hello stan hello tooreturn WebHCat (znanej także jako Templeton) powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="47c4f-124">hello path, **/status**, indicates that hello request is tooreturn hello status of WebHCat (also known as Templeton) for hello server.</span></span>

2. <span data-ttu-id="47c4f-125">Użyj następującego kodu toosubmit klastra toohello zadania Pig Latin hello:</span><span class="sxs-lookup"><span data-stu-id="47c4f-125">Use hello following code toosubmit a Pig Latin job toohello cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="47c4f-126">Parametry Hello używane w tym poleceniu są następujące:</span><span class="sxs-lookup"><span data-stu-id="47c4f-126">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="47c4f-127">**-d**: ponieważ `-G` nie jest używany, domyślnie przyjmowana jest hello żądania metody POST toohello.</span><span class="sxs-lookup"><span data-stu-id="47c4f-127">**-d**: Because `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="47c4f-128">`-d`Określa hello wartości danych, które są wysyłane z żądania hello.</span><span class="sxs-lookup"><span data-stu-id="47c4f-128">`-d` specifies hello data values that are sent with hello request.</span></span>

    * <span data-ttu-id="47c4f-129">**User.name**: hello użytkownik, który uruchamia polecenie hello</span><span class="sxs-lookup"><span data-stu-id="47c4f-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="47c4f-130">**wykonanie**: hello Pig Latin tooexecute — instrukcje</span><span class="sxs-lookup"><span data-stu-id="47c4f-130">**execute**: hello Pig Latin statements tooexecute</span></span>
    * <span data-ttu-id="47c4f-131">**statusdir**: hello katalogu, w którym hello stanu dla tego zadania jest zapisywany</span><span class="sxs-lookup"><span data-stu-id="47c4f-131">**statusdir**: hello directory that hello status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="47c4f-132">Zwróć uwagę, hello spacje w instrukcjach Pig Latin zastępuje hello `+` znak, gdy jest używany z Curl.</span><span class="sxs-lookup"><span data-stu-id="47c4f-132">Notice that hello spaces in Pig Latin statements are replaced by hello `+` character when used with Curl.</span></span>

    <span data-ttu-id="47c4f-133">To polecenie powinny zostać zwrócone identyfikator zadania, które mogą być używane toocheck hello stan zadania hello, na przykład:</span><span class="sxs-lookup"><span data-stu-id="47c4f-133">This command should return a job ID that can be used toocheck hello status of hello job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="47c4f-134">Stan hello toocheck hello zadania, hello Użyj następującego polecenia</span><span class="sxs-lookup"><span data-stu-id="47c4f-134">toocheck hello status of hello job, use hello following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="47c4f-135">Zastąp `JOBID` z wartością hello zwracane w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="47c4f-135">Replace `JOBID` with hello value returned in hello previous step.</span></span> <span data-ttu-id="47c4f-136">Na przykład jeśli hello zwrócona została wartość `{"id":"job_1415651640909_0026"}`, następnie `JOBID` jest `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="47c4f-136">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="47c4f-137">Jeśli hello zadanie zostało zakończone, stan hello jest **zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="47c4f-137">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="47c4f-138">To żądanie Curl zwraca dokumentu JavaScript Object Notation (JSON), informacje o zadaniu hello i jq jest używane tooretrieve hello tylko wartość stanu.</span><span class="sxs-lookup"><span data-stu-id="47c4f-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job, and jq is used tooretrieve only hello state value.</span></span>

## <span data-ttu-id="47c4f-139"><a id="results"></a>Wyświetl wyniki</span><span class="sxs-lookup"><span data-stu-id="47c4f-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="47c4f-140">Gdy stan hello hello zadania został zmieniony zbyt**zakończyło się pomyślnie**, można pobrać wyników hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="47c4f-140">When hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job.</span></span> <span data-ttu-id="47c4f-141">Witaj `statusdir` przekazany parametr zapytania o hello zawiera lokalizację hello hello pliku wyjściowego; w takim przypadku `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="47c4f-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="47c4f-142">HDInsight można użyć usługi Azure Storage lub usługi Azure Data Lake Store jako hello domyślnego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="47c4f-142">HDInsight can use either Azure Storage or Azure Data Lake Store as hello default data store.</span></span> <span data-ttu-id="47c4f-143">Istnieją różne sposoby tooget hello danych, w zależności od tego, która z nich korzystać.</span><span class="sxs-lookup"><span data-stu-id="47c4f-143">There are various ways tooget at hello data depending on which one you use.</span></span> <span data-ttu-id="47c4f-144">Aby uzyskać więcej informacji, zobacz hello magazynu część hello [informacji opartą na systemie Linux usługą HDInsight](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="47c4f-144">For more information, see hello storage section of hello [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="47c4f-145"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="47c4f-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="47c4f-146">Jak pokazano w tym dokumencie, można użyć raw toorun żądania HTTP, monitor i wyświetlić wyniki hello zadań Pig w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47c4f-146">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="47c4f-147">Aby uzyskać więcej informacji na temat interfejsu REST hello używane w tym artykule, zobacz hello [odwołania WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="47c4f-147">For more information about hello REST interface used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="47c4f-148"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="47c4f-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="47c4f-149">Aby uzyskać ogólne informacje na temat Pig w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="47c4f-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="47c4f-150">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="47c4f-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="47c4f-151">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="47c4f-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="47c4f-152">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="47c4f-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="47c4f-153">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="47c4f-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
