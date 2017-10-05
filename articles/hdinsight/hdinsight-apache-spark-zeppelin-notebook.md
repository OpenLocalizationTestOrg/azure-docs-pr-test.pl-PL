---
title: "Korzystanie z notesów Zeppelin z klastra Apache Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Instrukcje krok po kroku dotyczące sposobu używania notesów Zeppelin z klastrami Apache Spark w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7fe5e3ec68e82945b972d2dd44f2cc3b8cf395d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="689f8-103">Korzystanie z notesów Zeppelin z klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="689f8-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="689f8-104">Klastry HDInsight Spark obejmują notesów Zeppelin, których można użyć do uruchomienia zadań Spark.</span><span class="sxs-lookup"><span data-stu-id="689f8-104">HDInsight Spark clusters include Zeppelin notebooks that you can use to run Spark jobs.</span></span> <span data-ttu-id="689f8-105">W tym artykule Dowiedz się jak używać notesu Zeppelin w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="689f8-105">In this article, you learn how to use the Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="689f8-106">Notesów Zeppelin są dostępne tylko w przypadku 1.6.3 platformy Spark w usłudze HDInsight 3.5 i Spark 2.1.0 na 3,6 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="689f8-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="689f8-107">**Wymagania wstępne:**</span><span class="sxs-lookup"><span data-stu-id="689f8-107">**Prerequisites:**</span></span>

* <span data-ttu-id="689f8-108">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="689f8-108">An Azure subscription.</span></span> <span data-ttu-id="689f8-109">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="689f8-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="689f8-110">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="689f8-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="689f8-111">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="689f8-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="689f8-112">Uruchamianie notesu Zeppelin</span><span class="sxs-lookup"><span data-stu-id="689f8-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="689f8-113">W bloku klastra Spark kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Zeppelin**.</span><span class="sxs-lookup"><span data-stu-id="689f8-113">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="689f8-114">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora klastra.</span><span class="sxs-lookup"><span data-stu-id="689f8-114">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="689f8-115">Można również przejść Zeppelin Notebook dla klastra, otwierając następujący adres URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="689f8-115">You may also reach the Zeppelin Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="689f8-116">Zastąp ciąg **CLUSTERNAME** nazwą klastra:</span><span class="sxs-lookup"><span data-stu-id="689f8-116">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="689f8-117">Utwórz nowy notes.</span><span class="sxs-lookup"><span data-stu-id="689f8-117">Create a new notebook.</span></span> <span data-ttu-id="689f8-118">Okienko nagłówka kliknij **notesu**, a następnie kliknij przycisk **Tworzenie nowej notatki**.</span><span class="sxs-lookup"><span data-stu-id="689f8-118">From the header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="689f8-119">![Tworzenie nowego notesu Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Tworzenie nowego notesu Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="689f8-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="689f8-120">Wprowadź nazwę notesu, a następnie kliknij przycisk **utworzyć Uwaga**.</span><span class="sxs-lookup"><span data-stu-id="689f8-120">Enter a name for the notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="689f8-121">Ponadto upewnij się, że nagłówek notesu wyświetlany jest stan połączenia.</span><span class="sxs-lookup"><span data-stu-id="689f8-121">Also, make sure the notebook header shows a connected status.</span></span> <span data-ttu-id="689f8-122">Jest oznaczany zielonym kropką w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="689f8-122">It is denoted by a green dot in the top-right corner.</span></span>
   
    <span data-ttu-id="689f8-123">![Stan notesu Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notesu stanu")</span><span class="sxs-lookup"><span data-stu-id="689f8-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="689f8-124">Załaduj przykładowe dane do tabeli tymczasowej.</span><span class="sxs-lookup"><span data-stu-id="689f8-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="689f8-125">Podczas tworzenia klastra Spark w usłudze HDInsight przykładowy plik danych **hvac.csv**, jest kopiowany do skojarzonego konta magazynu w obszarze **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="689f8-125">When you create a Spark cluster in HDInsight, the sample data file, **hvac.csv**, is copied to the associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="689f8-126">W pusty akapit, który jest tworzony nowy notes domyślnie Wklej poniższy fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="689f8-126">In the empty paragraph that is created by default in the new notebook, paste the following snippet.</span></span>
   
        %livy.spark
        //The above magic instructs Zeppelin to use the Livy Scala interpreter
   
        // Create an RDD using the default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map the values in the .csv file to the schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    <span data-ttu-id="689f8-127">Naciśnij klawisz **SHIFT + ENTER** lub kliknij przycisk **odtwarzanie** przycisk akapitu uruchomić fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="689f8-127">Press **SHIFT + ENTER** or click the **Play** button for the paragraph to run the snippet.</span></span> <span data-ttu-id="689f8-128">Stan w prawym dolnym rogu akapitu powinien postępu z gotowe do czasu działania na ZAKOŃCZONE.</span><span class="sxs-lookup"><span data-stu-id="689f8-128">The status on the right-corner of the paragraph should progress from READY, PENDING, RUNNING to FINISHED.</span></span> <span data-ttu-id="689f8-129">Dane wyjściowe zostaną wyświetlone u dołu tej samej akapitu.</span><span class="sxs-lookup"><span data-stu-id="689f8-129">The output shows up at the bottom of the same paragraph.</span></span> <span data-ttu-id="689f8-130">Zrzut ekranu wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="689f8-130">The screenshot looks like the following:</span></span>
   
    <span data-ttu-id="689f8-131">![Tworzenie tabeli tymczasowej od danych pierwotnych](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Tworzenie tabeli tymczasowej od danych pierwotnych")</span><span class="sxs-lookup"><span data-stu-id="689f8-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="689f8-132">Można też podać tytuł do każdego akapitu.</span><span class="sxs-lookup"><span data-stu-id="689f8-132">You can also provide a title to each paragraph.</span></span> <span data-ttu-id="689f8-133">W prawym górnym rogu, kliknij przycisk **ustawienia** ikonę, a następnie kliknij przycisk **Pokaż tytuł**.</span><span class="sxs-lookup"><span data-stu-id="689f8-133">From the right-hand corner, click the **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="689f8-134">Teraz możesz uruchomić instrukcje Spark SQL **hvac** tabeli.</span><span class="sxs-lookup"><span data-stu-id="689f8-134">You can now run Spark SQL statements on the **hvac** table.</span></span> <span data-ttu-id="689f8-135">Wklej poniższe zapytanie nowy akapit.</span><span class="sxs-lookup"><span data-stu-id="689f8-135">Paste the following query in a new paragraph.</span></span> <span data-ttu-id="689f8-136">Zapytanie pobiera identyfikator budynku i różnica między docelowy i rzeczywistego temperatury dla każdego opierając się na dany dzień.</span><span class="sxs-lookup"><span data-stu-id="689f8-136">The query retrieves the building ID and the difference between the target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="689f8-137">Naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="689f8-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="689f8-138">**% Sql** instrukcji na początku informuje, aby użyć interpreter języka Scala Livy.</span><span class="sxs-lookup"><span data-stu-id="689f8-138">The **%sql** statement at the beginning tells the notebook to use the Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="689f8-139">Poniższy zrzut ekranu przedstawia dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="689f8-139">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="689f8-140">![Uruchom instrukcję Spark SQL za pomocą notesu](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "zestawienia Spark SQL za pomocą notesu")</span><span class="sxs-lookup"><span data-stu-id="689f8-140">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using the notebook")</span></span>
   
     <span data-ttu-id="689f8-141">Kliknij opcje wyświetlania (wyróżnione prostokąt), aby przełączyć między różne reprezentacje tych samych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="689f8-141">Click the display options (highlighted in rectangle) to switch between different representations for the same output.</span></span> <span data-ttu-id="689f8-142">Kliknij przycisk **ustawienia** wybierz jakie consitutes klucza i wartości w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="689f8-142">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="689f8-143">Przechwytywanie ekranu powyżej używa **buildingID** jako klucz i średnią **temp_diff** jako wartość.</span><span class="sxs-lookup"><span data-stu-id="689f8-143">The screen capture above uses **buildingID** as the key and the average of **temp_diff** as the value.</span></span>
6. <span data-ttu-id="689f8-144">Można również uruchomić Spark SQL instrukcje używania zmiennych w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="689f8-144">You can also run Spark SQL statements using variables in the query.</span></span> <span data-ttu-id="689f8-145">Dalej fragment kodu przedstawia sposób zdefiniowania zmiennej, **Temp**, kwerendy za pomocą możliwe wartości chcesz zbadać za pomocą.</span><span class="sxs-lookup"><span data-stu-id="689f8-145">The next snippet shows how to define a variable, **Temp**, in the query with the possible values you want to query with.</span></span> <span data-ttu-id="689f8-146">Przy pierwszym uruchomieniu zapytania, menu rozwijane jest automatycznie wypełniane przy użyciu wartości określone dla zmiennej.</span><span class="sxs-lookup"><span data-stu-id="689f8-146">When you first run the query, a drop-down is automatically populated with the values you specified for the variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="689f8-147">Wklej następujący fragment kodu w nowy akapit i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="689f8-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="689f8-148">Poniższy zrzut ekranu przedstawia dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="689f8-148">The following screenshot shows the output.</span></span>
   
    <span data-ttu-id="689f8-149">![Uruchom instrukcję Spark SQL za pomocą notesu](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "zestawienia Spark SQL za pomocą notesu")</span><span class="sxs-lookup"><span data-stu-id="689f8-149">![Run a Spark SQL statement using the notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using the notebook")</span></span>
   
    <span data-ttu-id="689f8-150">Następnych kwerend można wybrać nową wartość z listy rozwijanej i ponownie uruchom zapytanie.</span><span class="sxs-lookup"><span data-stu-id="689f8-150">For subsequent queries, you can select a new value from the drop-down and run the query again.</span></span> <span data-ttu-id="689f8-151">Kliknij przycisk **ustawienia** wybierz jakie consitutes klucza i wartości w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="689f8-151">Click **Settings** to choose what consitutes the key and values in the output.</span></span> <span data-ttu-id="689f8-152">Przechwytywanie ekranu powyżej używa **buildingID** jako klucz średnią **temp_diff** jako wartość, i **targettemp** jako grupa.</span><span class="sxs-lookup"><span data-stu-id="689f8-152">The screen capture above uses **buildingID** as the key, the average of **temp_diff** as the value, and **targettemp** as the group.</span></span>
7. <span data-ttu-id="689f8-153">Uruchom ponownie interpreter Livy, aby zakończyć działanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="689f8-153">Restart the Livy interpreter to exit the application.</span></span> <span data-ttu-id="689f8-154">Aby to zrobić, Otwórz okno Ustawienia interpreter klikając zalogowanego w nazwie użytkownika w prawym górnym rogu, a następnie kliknij przycisk **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="689f8-154">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="689f8-155">![Uruchamianie interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="689f8-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="689f8-156">Przewiń do Livy interpreter ustawienia, a następnie kliknij przycisk **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="689f8-156">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="689f8-157">![Uruchom ponownie Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Uruchom ponownie Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="689f8-157">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-the-notebook"></a><span data-ttu-id="689f8-158">Jak korzystanie z zewnętrznych pakietów z notesu?</span><span class="sxs-lookup"><span data-stu-id="689f8-158">How do I use external packages with the notebook?</span></span>
<span data-ttu-id="689f8-159">Notesu Zeppelin w klastrze Apache Spark w usłudze HDInsight (Linux) można skonfigurować na korzystanie z pakietów zewnętrznych, przyczyniły się społeczności, które nie są uwzględniane out-of--box w klastrze.</span><span class="sxs-lookup"><span data-stu-id="689f8-159">You can configure the Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) to use external, community-contributed packages that are not included out-of-the-box in the cluster.</span></span> <span data-ttu-id="689f8-160">Możesz przeszukać [repozytorium Maven](http://search.maven.org/) Aby uzyskać pełną listę pakietów, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="689f8-160">You can search the [Maven repository](http://search.maven.org/) for the complete list of packages that are available.</span></span> <span data-ttu-id="689f8-161">Można również uzyskać listę dostępnych pakietów z innych źródeł.</span><span class="sxs-lookup"><span data-stu-id="689f8-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="689f8-162">Na przykład pełną listę społeczności przyczyniły się do pakietów znajduje się w temacie [pakietów Spark](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="689f8-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="689f8-163">W tym artykule, wyświetlona zostanie sposób użycia [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakietu z notesem Jupyter.</span><span class="sxs-lookup"><span data-stu-id="689f8-163">In this article, you will see how to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with the Jupyter notebook.</span></span>

1. <span data-ttu-id="689f8-164">Otwórz ustawienia interpreter.</span><span class="sxs-lookup"><span data-stu-id="689f8-164">Open interpreter settings.</span></span> <span data-ttu-id="689f8-165">W prawym górnym rogu kliknij zalogowanego w nazwie użytkownika, a następnie kliknij **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="689f8-165">From the top-right corner, click the logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="689f8-166">![Uruchamianie interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="689f8-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="689f8-167">Przewiń do Livy interpreter ustawienia, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="689f8-167">Scroll to Livy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="689f8-168">![Zmień ustawienia interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "zmiany ustawień interpretera")</span><span class="sxs-lookup"><span data-stu-id="689f8-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="689f8-169">Dodaj nowy klucz o nazwie **livy.spark.jars.packages** i ustaw jej wartość w formacie `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="689f8-169">Add a new key, called **livy.spark.jars.packages** and set its value in the format `group:id:version`.</span></span> <span data-ttu-id="689f8-170">Tak więc, jeśli chcesz użyć [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakietu, należy ustawić wartość klucza `com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="689f8-170">So, if you want to use the [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set the value of the key to `com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="689f8-171">![Zmień ustawienia interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "zmiany ustawień interpretera")</span><span class="sxs-lookup"><span data-stu-id="689f8-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="689f8-172">Kliknij przycisk **zapisać** i uruchom ponownie Livy interpreter.</span><span class="sxs-lookup"><span data-stu-id="689f8-172">Click **Save** and then restart the Livy interpreter.</span></span>
4. <span data-ttu-id="689f8-173">**Porada**: Jeśli chcesz zrozumieć sposób został odebrany w wartość klucza wprowadzony powyżej, poniżej przedstawiono sposób.</span><span class="sxs-lookup"><span data-stu-id="689f8-173">**Tip**: If you want to understand how to arrive at the value of the key entered above, here's how.</span></span>
   
    <span data-ttu-id="689f8-174">a.</span><span class="sxs-lookup"><span data-stu-id="689f8-174">a.</span></span> <span data-ttu-id="689f8-175">Zlokalizuj pakiet w repozytorium Maven.</span><span class="sxs-lookup"><span data-stu-id="689f8-175">Locate the package in the Maven Repository.</span></span> <span data-ttu-id="689f8-176">W tym samouczku użyliśmy [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="689f8-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="689f8-177">b.</span><span class="sxs-lookup"><span data-stu-id="689f8-177">b.</span></span> <span data-ttu-id="689f8-178">Z repozytorium, Zbierz wartości **GroupId**, **ArtifactId**, i **wersji**.</span><span class="sxs-lookup"><span data-stu-id="689f8-178">From the repository, gather the values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="689f8-179">![Pakiety zewnętrzne za pomocą notesu Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "pakiety zewnętrzne za pomocą notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="689f8-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="689f8-180">c.</span><span class="sxs-lookup"><span data-stu-id="689f8-180">c.</span></span> <span data-ttu-id="689f8-181">Łączenie trzech oddzieloną dwukropkiem (**:**).</span><span class="sxs-lookup"><span data-stu-id="689f8-181">Concatenate the three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-the-zeppelin-notebooks-saved"></a><span data-ttu-id="689f8-182">Gdzie są zapisywane notesów Zeppelin?</span><span class="sxs-lookup"><span data-stu-id="689f8-182">Where are the Zeppelin notebooks saved?</span></span>
<span data-ttu-id="689f8-183">Notesów Zeppelin są zapisywane headnodes klastra.</span><span class="sxs-lookup"><span data-stu-id="689f8-183">The Zeppelin notebooks are saved to the cluster headnodes.</span></span> <span data-ttu-id="689f8-184">Aby usunąć klaster, jak również zostaną usunięte notebooki.</span><span class="sxs-lookup"><span data-stu-id="689f8-184">So, if you delete the cluster, the notebooks will be deleted as well.</span></span> <span data-ttu-id="689f8-185">Jeśli chcesz zachować notesy do późniejszego użytku w innych klastrach, należy je wyeksportować po zakończeniu wykonywania zadań.</span><span class="sxs-lookup"><span data-stu-id="689f8-185">If you want to preserve your notebooks for later use on other clusters, you must export them after you have finished running the jobs.</span></span> <span data-ttu-id="689f8-186">Aby wyeksportować Notes, kliknij przycisk **wyeksportować** ikony, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="689f8-186">To export a notebook, click the **Export** icon as shown in the image below.</span></span>

<span data-ttu-id="689f8-187">![Pobierz notesu](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Pobierz notesu")</span><span class="sxs-lookup"><span data-stu-id="689f8-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download the notebook")</span></span>

<span data-ttu-id="689f8-188">Spowoduje to zapisanie notesu jako plik JSON w lokalizacji pobierania.</span><span class="sxs-lookup"><span data-stu-id="689f8-188">This saves the notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="689f8-189">Zarządzanie sesjami programu Livy</span><span class="sxs-lookup"><span data-stu-id="689f8-189">Livy session management</span></span>
<span data-ttu-id="689f8-190">Po uruchomieniu pierwszym akapicie kodu w notesie Zeppelin w nowej sesji programu Livy jest tworzony w klastrze Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="689f8-190">When you run the first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="689f8-191">Ta sesja jest współużytkowana przez wszystkie notesów Zeppelin, które następnie utworzysz.</span><span class="sxs-lookup"><span data-stu-id="689f8-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="689f8-192">Jeśli z jakiegoś powodu Livy sesja jest skasowane (ponowne uruchomienie klastra, itp.), nie będzie można uruchamiać zadania z Zeppelin notesu.</span><span class="sxs-lookup"><span data-stu-id="689f8-192">If for some reason the Livy session is killed (cluster reboot, etc.), you will not be able to run jobs from the Zeppelin notebook.</span></span>

<span data-ttu-id="689f8-193">Przed rozpoczęciem wykonywania zadań z notesu Zeppelin w takim przypadku należy wykonać następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="689f8-193">In such a case, you must perform the following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="689f8-194">Uruchom ponownie interpreter Livy z Zeppelin notesu.</span><span class="sxs-lookup"><span data-stu-id="689f8-194">Restart the Livy interpreter from the Zeppelin notebook.</span></span> <span data-ttu-id="689f8-195">Aby to zrobić, Otwórz okno Ustawienia interpreter klikając zalogowanego w nazwie użytkownika w prawym górnym rogu, a następnie kliknij przycisk **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="689f8-195">To do so, open interpreter settings by clicking the logged in user name from the top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="689f8-196">![Uruchamianie interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="689f8-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="689f8-197">Przewiń do Livy interpreter ustawienia, a następnie kliknij przycisk **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="689f8-197">Scroll to Livy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="689f8-198">![Uruchom ponownie Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Uruchom ponownie Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="689f8-198">![Restart the Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart the Zeppelin intepreter")</span></span>
3. <span data-ttu-id="689f8-199">Uruchom komórki kodu z istniejącego notesu Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="689f8-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="689f8-200">Spowoduje to utworzenie nowej sesji programu Livy klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="689f8-200">This creates a new Livy session in the HDInsight cluster.</span></span>

## <span data-ttu-id="689f8-201"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="689f8-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="689f8-202">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="689f8-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="689f8-203">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="689f8-203">Scenarios</span></span>
* [<span data-ttu-id="689f8-204">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="689f8-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="689f8-205">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="689f8-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="689f8-206">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności</span><span class="sxs-lookup"><span data-stu-id="689f8-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="689f8-207">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="689f8-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="689f8-208">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="689f8-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="689f8-209">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="689f8-209">Create and run applications</span></span>
* [<span data-ttu-id="689f8-210">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="689f8-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="689f8-211">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="689f8-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="689f8-212">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="689f8-212">Tools and extensions</span></span>
* [<span data-ttu-id="689f8-213">Tworzenie i przesyłanie aplikacji Spark Scala przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="689f8-213">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="689f8-214">Zdalne debugowanie aplikacji Spark przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="689f8-214">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="689f8-215">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="689f8-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="689f8-216">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="689f8-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="689f8-217">Instalacja oprogramowania Jupyter na komputerze i nawiązywanie połączenia z klastrem Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="689f8-217">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="689f8-218">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="689f8-218">Manage resources</span></span>
* [<span data-ttu-id="689f8-219">Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="689f8-219">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="689f8-220">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="689f8-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







