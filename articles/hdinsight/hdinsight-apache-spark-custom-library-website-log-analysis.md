---
title: "aaaAnalyze dzienników witryn sieci Web z bibliotekami Python w łączniku Spark - Azure | Dokumentacja firmy Microsoft"
description: "Ten notes pokazano, jak tooanalyze dziennika danych przy użyciu niestandardowa biblioteka z łącznikiem Spark on Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="5f1c0-103">Analizowanie dzienników witryn sieci Web przy użyciu niestandardowa biblioteka języka Python z klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f1c0-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="5f1c0-104">Ten notes pokazano, jak tooanalyze dziennika danych przy użyciu niestandardowa biblioteka z platformy Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-104">This notebook demonstrates how tooanalyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="5f1c0-105">biblioteka języka Python, nazywany jest niestandardowa biblioteka Hello używamy **iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-105">hello custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="5f1c0-106">W tym samouczku jest również dostępny jako notesu Jupyter w klastrze Spark (Linux), które są tworzone w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="5f1c0-107">środowisko notesu Hello umożliwia uruchamianie hello Python wstawki z notesu hello, sama.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-107">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="5f1c0-108">Samouczek hello tooperform z poziomu Notes, tworzenie klastra Spark, uruchom notesu Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), a następnie uruchom notesu hello **analizowanie dzienników z Spark przy użyciu niestandardowych library.ipynb** w obszarze hello  **PySpark** folderu.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-108">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Analyze logs with Spark using a custom library.ipynb** under hello **PySpark** folder.</span></span>
>
>

<span data-ttu-id="5f1c0-109">**Wymagania wstępne:**</span><span class="sxs-lookup"><span data-stu-id="5f1c0-109">**Prerequisites:**</span></span>

<span data-ttu-id="5f1c0-110">Musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="5f1c0-110">You must have hello following:</span></span>

* <span data-ttu-id="5f1c0-111">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-111">An Azure subscription.</span></span> <span data-ttu-id="5f1c0-112">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5f1c0-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="5f1c0-113">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="5f1c0-114">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="5f1c0-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="5f1c0-115">Zapisz dane pierwotne jako RDD</span><span class="sxs-lookup"><span data-stu-id="5f1c0-115">Save raw data as an RDD</span></span>
<span data-ttu-id="5f1c0-116">W tej sekcji użyjesz hello [Jupyter](https://jupyter.org) notesu skojarzone z klastra Apache Spark w usłudze HDInsight toorun zadania, które przetwarzać dane pierwotne próbki i zapisz go jako tabeli programu Hive.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-116">In this section, we use hello [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight toorun jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="5f1c0-117">Witaj przykładowych danych jest plik CSV (hvac.csv) dostępne na wszystkich klastrach domyślnie.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-117">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="5f1c0-118">Gdy dane są zapisywane jako tabeli programu Hive, w następnej sekcji hello firma Microsoft będzie łączyć toohello tabeli Hive za pomocą narzędzi analizy Biznesowej, takich jak Power BI i Tableau.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-118">Once your data is saved as a Hive table, in hello next section we will connect toohello Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="5f1c0-119">Z hello [portalu Azure](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej).</span><span class="sxs-lookup"><span data-stu-id="5f1c0-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="5f1c0-120">Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="5f1c0-121">W bloku klastra Spark powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="5f1c0-122">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5f1c0-123">Można również przejść hello Jupyter Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="5f1c0-124">Zastąp **CLUSTERNAME** o nazwie hello klastra:</span><span class="sxs-lookup"><span data-stu-id="5f1c0-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="5f1c0-125">Utwórz nowy notes.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-125">Create a new notebook.</span></span> <span data-ttu-id="5f1c0-126">Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="5f1c0-127">![Tworzenie nowego notesu Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Tworzenie nowego notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="5f1c0-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="5f1c0-128">Nowy notes jest utworzony i otwarty z hello nazwie Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="5f1c0-129">Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="5f1c0-130">![Podaj nazwę notesu hello](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Podaj nazwę notesu hello")</span><span class="sxs-lookup"><span data-stu-id="5f1c0-130">![Provide a name for hello notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for hello notebook")</span></span>
5. <span data-ttu-id="5f1c0-131">Ponieważ Notes jądro PySpark hello został utworzony, nie trzeba toocreate kontekstów jawnie.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="5f1c0-132">konteksty Spark i Hive Hello zostanie automatycznie utworzone automatycznie po uruchomieniu pierwszej komórki kodu hello.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-132">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="5f1c0-133">Możesz zacząć od importowania typów hello, które są wymagane dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-133">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="5f1c0-134">Witaj następującego fragmentu kodu w pustej komórce Wklej, a następnie naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-134">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="5f1c0-135">Utwórz RDD przy użyciu danych dziennika próbki hello już dostępne w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-135">Create an RDD using hello sample log data already available on hello cluster.</span></span> <span data-ttu-id="5f1c0-136">Są dostępne dane hello w hello domyślnego konta magazynu skojarzone z klastrem hello na **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-136">You can access hello data in hello default storage account associated with hello cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="5f1c0-137">Pobierz przykładowy dziennik Ustaw tooverify tego hello poprzedniego kroku została ukończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-137">Retrieve a sample log set tooverify that hello previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="5f1c0-138">Powinny być widoczne następujące dane wyjściowe podobne toohello:</span><span class="sxs-lookup"><span data-stu-id="5f1c0-138">You should see an output similar toohello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="5f1c0-139">Analizowanie danych dziennika przy użyciu niestandardowa biblioteka języka Python</span><span class="sxs-lookup"><span data-stu-id="5f1c0-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="5f1c0-140">W powyższych danych wyjściowych hello hello pierwszych kilku wierszy zawierają informacje o nagłówku hello i każdym wierszu pozostałych dopasowuje schematu hello opisane w tym nagłówka.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-140">In hello output above, hello first couple lines include hello header information and each remaining line matches hello schema described in that header.</span></span> <span data-ttu-id="5f1c0-141">Podczas analizowania dzienników takie może być skomplikowane.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="5f1c0-142">Tak, używamy niestandardowa biblioteka języka Python (**iislogparser.py**), które służą do analizowania tych dzienników znacznie łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="5f1c0-143">Domyślnie ta biblioteka jest dołączana do klastra Spark w usłudze HDInsight w **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="5f1c0-144">Ta biblioteka nie działa jednak w hello `PYTHONPATH` , nie można użyć przy użyciu instrukcji importu, takich jak `import iislogparser`.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-144">However, this library is not in hello `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="5f1c0-145">toouse tej biblioteki, możemy przeprowadzić dystrybucję go węzłów procesu roboczego hello tooall.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-145">toouse this library, we must distribute it tooall hello worker nodes.</span></span> <span data-ttu-id="5f1c0-146">Uruchom hello następującego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-146">Run hello following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="5f1c0-147">`iislogparser`udostępnia funkcję `parse_log_line` zwracającą `None` Jeśli wiersz dziennika jest wiersz nagłówka i zwraca wystąpienie klasy hello `LogLine` klasy, jeśli wykryje wiersza dziennika.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of hello `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="5f1c0-148">Użyj hello `LogLine` tooextract klasy hello tylko wiersze dziennika z hello RDD:</span><span class="sxs-lookup"><span data-stu-id="5f1c0-148">Use hello `LogLine` class tooextract only hello log lines from hello RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="5f1c0-149">Pobrać kilka tooverify wyodrębnionego dziennika wiersze, które hello kroku została ukończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-149">Retrieve a couple of extracted log lines tooverify that hello step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="5f1c0-150">Hello dane wyjściowe powinny być podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5f1c0-150">hello output should be similar toohello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="5f1c0-151">Hello `LogLine` klasy, z kolei ma niektóre przydatne metody, takie jak `is_error()`, która zwraca czy wpis dziennika ma kod błędu.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-151">hello `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="5f1c0-152">Użyj hello toocompute liczba błędów w wierszach dziennika hello wyodrębnione, a następnie zalogowanie wszystkich hello błędy tooa inny plik.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-152">Use this toocompute hello number of errors in hello extracted log lines, and then log all hello errors tooa different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="5f1c0-153">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="5f1c0-153">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="5f1c0-154">Można również użyć **Matplotlib** tooconstruct wizualizacji danych hello.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-154">You can also use **Matplotlib** tooconstruct a visualization of hello data.</span></span> <span data-ttu-id="5f1c0-155">Na przykład jeśli chcesz tooisolate hello przyczynę żądania, które są uruchamiane przez długi czas, można toofind hello pliki, przyjmujących hello większość czasu tooserve średnio.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-155">For example, if you want tooisolate hello cause of requests that run for a long time, you might want toofind hello files that take hello most time tooserve on average.</span></span>
   <span data-ttu-id="5f1c0-156">Poniższy fragment Hello pobiera hello top 25 zasobów, których przez większość czasu tooserve żądanie.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-156">hello snippet below retrieves hello top 25 resources that took most time tooserve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="5f1c0-157">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="5f1c0-157">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. <span data-ttu-id="5f1c0-158">Można również prezentować te informacje w postaci hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-158">You can also present this information in hello form of plot.</span></span> <span data-ttu-id="5f1c0-159">Jako pierwszy krok toocreate wykresu, poinformuj nas najpierw utworzyć tabeli tymczasowej **AverageTime**.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-159">As a first step toocreate a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="5f1c0-160">Witaj tabeli grup Witaj rejestruje przez toosee czasu, jeśli było żadnych nietypowe opóźnienia rzędu w dowolnym momencie konkretnego.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-160">hello table groups hello logs by time toosee if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="5f1c0-161">Następnie możesz uruchomić powitania po tooget zapytania SQL wszystkie rekordy hello w hello **AverageTime** tabeli.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-161">You can then run hello following SQL query tooget all hello records in hello **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="5f1c0-162">Witaj `%%sql` magic następuje `-o averagetime` gwarantuje, że hello wyników kwerendy hello jest trwały lokalnie na serwerze Jupyter hello (zazwyczaj hello headnode hello klastra).</span><span class="sxs-lookup"><span data-stu-id="5f1c0-162">hello `%%sql` magic followed by `-o averagetime` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="5f1c0-163">dane wyjściowe Hello jest utrwalony jako [Pandas](http://pandas.pydata.org/) dataframe z hello określona nazwa **averagetime**.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-163">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **averagetime**.</span></span>

   <span data-ttu-id="5f1c0-164">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="5f1c0-164">You should see an output like hello following:</span></span>

   <span data-ttu-id="5f1c0-165">![Dane wyjściowe kwerendy SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "wyników zapytania SQL")</span><span class="sxs-lookup"><span data-stu-id="5f1c0-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="5f1c0-166">Aby uzyskać więcej informacji na temat hello `%%sql` magicznych, zobacz [obsługiwane parametry z hello %% sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="5f1c0-166">For more information about hello `%%sql` magic, see [Parameters supported with hello %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="5f1c0-167">Teraz możesz używać Matplotlib, tooconstruct wizualizację danych, toocreate wykresu użycie biblioteki.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-167">You can now use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="5f1c0-168">Ponieważ kreślenia hello musi być utworzony na podstawie hello lokalnie utrwalone **averagetime** dataframe, fragment kodu hello musi rozpoczynać się od hello `%%local` magic.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-168">Because hello plot must be created from hello locally persisted **averagetime** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="5f1c0-169">Dzięki temu, że kod hello uruchamiane lokalnie na serwerze Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-169">This ensures that hello code is run locally on hello Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="5f1c0-170">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="5f1c0-170">You should see an output like hello following:</span></span>

   <span data-ttu-id="5f1c0-171">![Dane wyjściowe Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="5f1c0-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="5f1c0-172">Po zakończeniu uruchamiania aplikacji hello należy zamknięcia hello notesu toorelease hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-172">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="5f1c0-173">toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-173">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="5f1c0-174">To spowoduje zamknięcie i zamknij hello notesu.</span><span class="sxs-lookup"><span data-stu-id="5f1c0-174">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="5f1c0-175"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5f1c0-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="5f1c0-176">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f1c0-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="5f1c0-177">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="5f1c0-177">Scenarios</span></span>
* [<span data-ttu-id="5f1c0-178">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="5f1c0-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="5f1c0-179">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="5f1c0-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="5f1c0-180">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f1c0-180">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="5f1c0-181">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="5f1c0-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="5f1c0-182">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="5f1c0-182">Create and run applications</span></span>
* [<span data-ttu-id="5f1c0-183">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="5f1c0-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5f1c0-184">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="5f1c0-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="5f1c0-185">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="5f1c0-185">Tools and extensions</span></span>
* [<span data-ttu-id="5f1c0-186">Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="5f1c0-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="5f1c0-187">Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="5f1c0-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="5f1c0-188">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f1c0-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="5f1c0-189">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f1c0-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="5f1c0-190">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="5f1c0-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="5f1c0-191">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f1c0-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="5f1c0-192">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="5f1c0-192">Manage resources</span></span>
* [<span data-ttu-id="5f1c0-193">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f1c0-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="5f1c0-194">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f1c0-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
