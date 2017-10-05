---
title: "Użyj MapReduce i Curl z platformą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zdalne uruchamianie zadań MapReduce z Hadoop w usłudze HDInsight przy użyciu programu Curl."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 8238bb829df95dcb8c99c0b7fff53c627a56f47c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="a230b-103">Uruchamianie zadań MapReduce z Hadoop w usłudze HDInsight za pomocą usługi REST</span><span class="sxs-lookup"><span data-stu-id="a230b-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="a230b-104">Dowiedz się, jak za pomocą interfejsu API REST usługi WebHCat do uruchomienia zadań MapReduce na platformie Hadoop w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a230b-104">Learn how to use the WebHCat REST API to run MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="a230b-105">Zwinięcie służy do pokazują, jak można interakcję z usługą HDInsight przy użyciu pierwotne żądania HTTP do uruchomienia zadań MapReduce.</span><span class="sxs-lookup"><span data-stu-id="a230b-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="a230b-106">Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale jesteś nowym użytkownikiem usługi HDInsight, zobacz [co należy wiedzieć o opartych na systemie Linux platformą Hadoop w HDInsight](hdinsight-hadoop-linux-information.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="a230b-106">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see the [What you need to know about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="a230b-107"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a230b-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="a230b-108">Usługi w klastrze usługi HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="a230b-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="a230b-109">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="a230b-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="a230b-110">jq</span><span class="sxs-lookup"><span data-stu-id="a230b-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="a230b-111"><a id="curl"></a>Uruchamianie zadań MapReduce przy użyciu programu Curl</span><span class="sxs-lookup"><span data-stu-id="a230b-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="a230b-112">Gdy używasz Curl lub innego połączenia REST z usługą WebHCat, wymagane jest uwierzytelnienie żądania przez podanie nazwy użytkownika administratora klastra usługi HDInsight i hasła.</span><span class="sxs-lookup"><span data-stu-id="a230b-112">When you use Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="a230b-113">Należy użyć nazwy klastra jako część identyfikatora URI, który służy do wysyłania żądań do serwera.</span><span class="sxs-lookup"><span data-stu-id="a230b-113">You must use the cluster name as part of the URI that is used to send the requests to the server.</span></span>
>
> <span data-ttu-id="a230b-114">Dla poleceń w tej sekcji należy zastąpić **USERNAME** z użytkownikiem w celu uwierzytelniania w klastrze i **hasło** hasłem do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a230b-114">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="a230b-115">Zastąp ciąg **CLUSTERNAME** nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="a230b-115">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="a230b-116">Interfejs API REST jest zabezpieczony za pomocą [uwierzytelniania podstawowego dostępu](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="a230b-116">The REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="a230b-117">Należy zawsze tworzyć żądania przy użyciu protokołu HTTPS, aby upewnić się, że poświadczenia są bezpiecznie wysyłane do serwera.</span><span class="sxs-lookup"><span data-stu-id="a230b-117">You should always make requests by using HTTPS to ensure that your credentials are securely sent to the server.</span></span>


1. <span data-ttu-id="a230b-118">W wierszu polecenia wpisz następujące polecenie, aby sprawdzić możliwość nawiązania połączenia z klastrem usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a230b-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="a230b-119">Powinien otrzymywać odpowiedź podobną do następujących JSON:</span><span class="sxs-lookup"><span data-stu-id="a230b-119">You should receive a response similar to the following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="a230b-120">W tym poleceniu są używane następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="a230b-120">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="a230b-121">**-u**: Określa nazwę użytkownika i hasło używane do uwierzytelniania żądania</span><span class="sxs-lookup"><span data-stu-id="a230b-121">**-u**: Indicates the user name and password used to authenticate the request</span></span>
   * <span data-ttu-id="a230b-122">**-G**: oznacza, że ta operacja jest żądanie pobrania</span><span class="sxs-lookup"><span data-stu-id="a230b-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="a230b-123">Początek identyfikatora URI **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, jest taka sama dla wszystkich żądań.</span><span class="sxs-lookup"><span data-stu-id="a230b-123">The beginning of the URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span>

2. <span data-ttu-id="a230b-124">Aby przesłać zadania MapReduce, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a230b-124">To submit a MapReduce job, use the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="a230b-125">Koniec identyfikatora URI (/ mapreduce/jar) określa, że usługi WebHCat to żądanie rozpoczęcia zadania MapReduce z klasy w pliku jar.</span><span class="sxs-lookup"><span data-stu-id="a230b-125">The end of the URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="a230b-126">W tym poleceniu są używane następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="a230b-126">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="a230b-127">**-d**: `-G` nie jest używana, więc domyślnie żądania metody POST.</span><span class="sxs-lookup"><span data-stu-id="a230b-127">**-d**: `-G` is not used, so the request defaults to the POST method.</span></span> <span data-ttu-id="a230b-128">`-d`Określa dane, które są wysyłane z żądania.</span><span class="sxs-lookup"><span data-stu-id="a230b-128">`-d` specifies the data values that are sent with the request.</span></span>
    * <span data-ttu-id="a230b-129">**User.name**: użytkownik, który uruchamia polecenie</span><span class="sxs-lookup"><span data-stu-id="a230b-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="a230b-130">**JAR**: uruchomiono lokalizacji pliku jar, który zawiera klasę jako</span><span class="sxs-lookup"><span data-stu-id="a230b-130">**jar**: The location of the jar file that contains class to be ran</span></span>
    * <span data-ttu-id="a230b-131">**Klasa**: klasa, która zawiera logikę MapReduce</span><span class="sxs-lookup"><span data-stu-id="a230b-131">**class**: The class that contains the MapReduce logic</span></span>
    * <span data-ttu-id="a230b-132">**ARG**: argumenty do przekazania do zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="a230b-132">**arg**: The arguments to be passed to the MapReduce job.</span></span> <span data-ttu-id="a230b-133">W tym przypadku, pliku wejściowego tekstu i katalog, w którym są używane dla danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="a230b-133">In this case, the input text file and the directory that are used for the output</span></span>

     <span data-ttu-id="a230b-134">To polecenie powinny zostać zwrócone identyfikator zadania, który może służyć do sprawdzania stanu zadania:</span><span class="sxs-lookup"><span data-stu-id="a230b-134">This command should return a job ID that can be used to check the status of the job:</span></span>

       <span data-ttu-id="a230b-135">{"id": "job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="a230b-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="a230b-136">Aby sprawdzić stan zadania, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a230b-136">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="a230b-137">Zastąp **JOBID** o wartości zwracanej w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="a230b-137">Replace the **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="a230b-138">Na przykład, jeśli była zwracana wartość `{"id":"job_1415651640909_0026"}`, następnie będzie identyfikator JOBID `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="a230b-138">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then the JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="a230b-139">Jeśli zadanie zostało zakończone, zwracany jest stan `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="a230b-139">If the job is complete, the state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a230b-140">To żądanie Curl zwraca informacje o zadaniu dokumentu JSON.</span><span class="sxs-lookup"><span data-stu-id="a230b-140">This Curl request returns a JSON document with information about the job.</span></span> <span data-ttu-id="a230b-141">Jq służy do pobierania wartości stan.</span><span class="sxs-lookup"><span data-stu-id="a230b-141">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="a230b-142">Gdy stan zadania został zmieniony na `SUCCEEDED`, wyniki zadania można pobrać z magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a230b-142">When the state of the job has changed to `SUCCEEDED`, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="a230b-143">`statusdir` Parametr przekazywany z zapytaniem zawiera lokalizację pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="a230b-143">The `statusdir` parameter that is passed with the query contains the location of the output file.</span></span> <span data-ttu-id="a230b-144">W tym przykładzie jest lokalizacja `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="a230b-144">In this example, the location is `/example/curl`.</span></span> <span data-ttu-id="a230b-145">Ten adres przechowuje dane wyjściowe zadania w magazynie domyślne klastrów w `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="a230b-145">This address stores the output of the job in the clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="a230b-146">Można wyświetlić listę i takie pliki należy pobierać za pomocą [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a230b-146">You can list and download these files by using the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="a230b-147">Aby uzyskać więcej informacji na temat pracy z obiektami blob z wiersza polecenia platformy Azure, zobacz [przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure z usługą Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="a230b-147">For more information on working with blobs from the Azure CLI, see the [Using the Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="a230b-148"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a230b-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="a230b-149">Aby uzyskać ogólne informacje na temat zadań MapReduce w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a230b-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="a230b-150">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a230b-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="a230b-151">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a230b-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="a230b-152">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a230b-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a230b-153">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a230b-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="a230b-154">Aby uzyskać więcej informacji na temat interfejsu REST, który jest używany w tym artykule, zobacz [odwołania WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="a230b-154">For more information about the REST interface that is used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>