---
title: "aaaUse MapReduce i Curl z platformą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooremotely uruchamiania zadań MapReduce z Hadoop w usłudze HDInsight przy użyciu programu Curl."
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
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="e6533-103">Uruchamianie zadań MapReduce z Hadoop w usłudze HDInsight za pomocą usługi REST</span><span class="sxs-lookup"><span data-stu-id="e6533-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="e6533-104">Dowiedz się, jak toouse hello interfejsu API REST usługi WebHCat toorun MapReduce zadania na platformie Hadoop w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6533-104">Learn how toouse hello WebHCat REST API toorun MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="e6533-105">Zwinięcie jest używane toodemonstrate, jak można interakcję z usługą HDInsight przy użyciu raw zadań MapReduce toorun żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="e6533-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="e6533-106">Jeśli znasz już przy użyciu serwerów opartych na systemie Linux platformą Hadoop, ale są nowe tooHDInsight, zobacz hello [potrzebnych tooknow o opartych na systemie Linux platformą Hadoop w HDInsight](hdinsight-hadoop-linux-information.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e6533-106">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see hello [What you need tooknow about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="e6533-107"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e6533-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="e6533-108">Usługi w klastrze usługi HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="e6533-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="e6533-109">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="e6533-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="e6533-110">jq</span><span class="sxs-lookup"><span data-stu-id="e6533-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="e6533-111"><a id="curl"></a>Uruchamianie zadań MapReduce przy użyciu programu Curl</span><span class="sxs-lookup"><span data-stu-id="e6533-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="e6533-112">Użycie Curl lub innego połączenia REST z usługą WebHCat, muszą uwierzytelnić żądania hello przez podanie nazwy użytkownika administratora klastra usługi HDInsight hello i hasła.</span><span class="sxs-lookup"><span data-stu-id="e6533-112">When you use Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="e6533-113">Należy użyć nazwy klastra hello jako część hello identyfikator URI, który jest używany toosend hello żądań toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="e6533-113">You must use hello cluster name as part of hello URI that is used toosend hello requests toohello server.</span></span>
>
> <span data-ttu-id="e6533-114">Hello poleceń w tej sekcji, Zastąp **USERNAME** hello użytkownika tooauthenticate toohello klastra i **hasło** hello hasła dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="e6533-114">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="e6533-115">Zastąp **CLUSTERNAME** o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e6533-115">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="e6533-116">Witaj interfejsu API REST jest zabezpieczony za pomocą [uwierzytelniania podstawowego dostępu](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="e6533-116">hello REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="e6533-117">Należy zawsze tworzyć żądania przy użyciu tooensure HTTPS, że poświadczenia są bezpiecznie wysyłane toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="e6533-117">You should always make requests by using HTTPS tooensure that your credentials are securely sent toohello server.</span></span>


1. <span data-ttu-id="e6533-118">Z wiersza polecenia użyj hello następujące polecenia tooverify, że możesz połączyć tooyour klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e6533-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="e6533-119">Powinien zostać wyświetlony podobne toohello o następujące JSON odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="e6533-119">You should receive a response similar toohello following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="e6533-120">Parametry Hello używane w tym poleceniu są następujące:</span><span class="sxs-lookup"><span data-stu-id="e6533-120">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="e6533-121">**-u**: wskazuje hello nazwę użytkownika i hasło używane tooauthenticate hello żądania</span><span class="sxs-lookup"><span data-stu-id="e6533-121">**-u**: Indicates hello user name and password used tooauthenticate hello request</span></span>
   * <span data-ttu-id="e6533-122">**-G**: oznacza, że ta operacja jest żądanie pobrania</span><span class="sxs-lookup"><span data-stu-id="e6533-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="e6533-123">Witaj, początek hello identyfikatora URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, jest hello takie same dla wszystkich żądań.</span><span class="sxs-lookup"><span data-stu-id="e6533-123">hello beginning of hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span>

2. <span data-ttu-id="e6533-124">toosubmit zadania MapReduce, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e6533-124">toosubmit a MapReduce job, use hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="e6533-125">koniec Hello hello identyfikatora URI (/ mapreduce/jar) określa, że usługi WebHCat to żądanie rozpoczęcia zadania MapReduce z klasy w pliku jar.</span><span class="sxs-lookup"><span data-stu-id="e6533-125">hello end of hello URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="e6533-126">Parametry Hello używane w tym poleceniu są następujące:</span><span class="sxs-lookup"><span data-stu-id="e6533-126">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="e6533-127">**-d**: `-G` nie jest używana, więc żądania hello domyślne toohello metody POST.</span><span class="sxs-lookup"><span data-stu-id="e6533-127">**-d**: `-G` is not used, so hello request defaults toohello POST method.</span></span> <span data-ttu-id="e6533-128">`-d`Określa hello wartości danych, które są wysyłane z żądania hello.</span><span class="sxs-lookup"><span data-stu-id="e6533-128">`-d` specifies hello data values that are sent with hello request.</span></span>
    * <span data-ttu-id="e6533-129">**User.name**: hello użytkownik, który uruchamia polecenie hello</span><span class="sxs-lookup"><span data-stu-id="e6533-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="e6533-130">**JAR**: uruchomiono hello lokalizacji pliku jar hello, który zawiera toobe klasy</span><span class="sxs-lookup"><span data-stu-id="e6533-130">**jar**: hello location of hello jar file that contains class toobe ran</span></span>
    * <span data-ttu-id="e6533-131">**Klasa**: hello klasy, która zawiera logikę MapReduce hello</span><span class="sxs-lookup"><span data-stu-id="e6533-131">**class**: hello class that contains hello MapReduce logic</span></span>
    * <span data-ttu-id="e6533-132">**ARG**: hello toobe Argumenty przekazane toohello zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="e6533-132">**arg**: hello arguments toobe passed toohello MapReduce job.</span></span> <span data-ttu-id="e6533-133">W takim przypadku hello wejściowych katalogu plików i hello tekst, który są używane dla danych wyjściowych hello</span><span class="sxs-lookup"><span data-stu-id="e6533-133">In this case, hello input text file and hello directory that are used for hello output</span></span>

     <span data-ttu-id="e6533-134">Identyfikator zadania, które mogą być używane toocheck hello stan zadania hello powinny zostać zwrócone przez to polecenie:</span><span class="sxs-lookup"><span data-stu-id="e6533-134">This command should return a job ID that can be used toocheck hello status of hello job:</span></span>

       <span data-ttu-id="e6533-135">{"id": "job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="e6533-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="e6533-136">Stan hello toocheck hello zadania, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e6533-136">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="e6533-137">Zastąp hello **JOBID** z wartością hello zwracane w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="e6533-137">Replace hello **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="e6533-138">Na przykład jeśli hello zwrócona została wartość `{"id":"job_1415651640909_0026"}`, następnie hello byłoby JOBID `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="e6533-138">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then hello JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="e6533-139">Jeśli zakończeniu zadania hello hello stanu zwrócony `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="e6533-139">If hello job is complete, hello state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e6533-140">To żądanie Curl zwraca informacje o zadaniu hello dokumentu JSON.</span><span class="sxs-lookup"><span data-stu-id="e6533-140">This Curl request returns a JSON document with information about hello job.</span></span> <span data-ttu-id="e6533-141">Służy Jq tooretrieve hello tylko wartość stanu.</span><span class="sxs-lookup"><span data-stu-id="e6533-141">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="e6533-142">Gdy stan hello hello zadania został zmieniony zbyt`SUCCEEDED`, hello wyników zadania hello można pobrać z magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e6533-142">When hello state of hello job has changed too`SUCCEEDED`, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="e6533-143">Witaj `statusdir` parametr przekazywany z zapytaniem hello zawiera lokalizację hello hello pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="e6533-143">hello `statusdir` parameter that is passed with hello query contains hello location of hello output file.</span></span> <span data-ttu-id="e6533-144">W tym przykładzie lokalizacji hello jest `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="e6533-144">In this example, hello location is `/example/curl`.</span></span> <span data-ttu-id="e6533-145">Ten adres przechowuje hello dane wyjściowe zadania hello w magazynie domyślne klastrów hello na `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="e6533-145">This address stores hello output of hello job in hello clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="e6533-146">Można wyświetlić listę i takie pliki należy pobierać za pomocą hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e6533-146">You can list and download these files by using hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="e6533-147">Aby uzyskać więcej informacji na temat pracy z obiektami blob z hello wiersza polecenia platformy Azure, zobacz hello [hello Using Azure CLI 2.0 z usługą Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e6533-147">For more information on working with blobs from hello Azure CLI, see hello [Using hello Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="e6533-148"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e6533-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="e6533-149">Aby uzyskać ogólne informacje na temat zadań MapReduce w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e6533-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="e6533-150">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6533-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="e6533-151">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e6533-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="e6533-152">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6533-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e6533-153">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6533-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="e6533-154">Aby uzyskać więcej informacji na temat interfejsu REST hello, który jest używany w tym artykule, zobacz hello [odwołania WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="e6533-154">For more information about hello REST interface that is used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>
