---
title: "klaster notesów Zeppelin aaaUse z platformy Apache Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Instrukcje krok po kroku, w jaki klastrów notesów Zeppelin toouse z platformy Apache Spark w usłudze Azure HDInsight."
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
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="c7edf-103">Korzystanie z notesów Zeppelin z klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7edf-103">Use Zeppelin notebooks with Apache Spark cluster on Azure HDInsight</span></span>

<span data-ttu-id="c7edf-104">Klastry HDInsight Spark obejmują notesów Zeppelin służy toorun zadań Spark.</span><span class="sxs-lookup"><span data-stu-id="c7edf-104">HDInsight Spark clusters include Zeppelin notebooks that you can use toorun Spark jobs.</span></span> <span data-ttu-id="c7edf-105">W tym artykule dowiesz się, jak toouse hello notesu Zeppelin w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7edf-105">In this article, you learn how toouse hello Zeppelin notebook on an HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="c7edf-106">Notesów Zeppelin są dostępne tylko w przypadku 1.6.3 platformy Spark w usłudze HDInsight 3.5 i Spark 2.1.0 na 3,6 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7edf-106">Zeppelin notebooks are available only for Spark 1.6.3 on HDInsight 3.5 and Spark 2.1.0 on HDInsight 3.6.</span></span>
>

<span data-ttu-id="c7edf-107">**Wymagania wstępne:**</span><span class="sxs-lookup"><span data-stu-id="c7edf-107">**Prerequisites:**</span></span>

* <span data-ttu-id="c7edf-108">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7edf-108">An Azure subscription.</span></span> <span data-ttu-id="c7edf-109">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c7edf-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="c7edf-110">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7edf-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="c7edf-111">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="c7edf-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="launch-a-zeppelin-notebook"></a><span data-ttu-id="c7edf-112">Uruchamianie notesu Zeppelin</span><span class="sxs-lookup"><span data-stu-id="c7edf-112">Launch a Zeppelin notebook</span></span>
1. <span data-ttu-id="c7edf-113">W bloku klastra Spark hello, kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Zeppelin**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-113">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Zeppelin Notebook**.</span></span> <span data-ttu-id="c7edf-114">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="c7edf-114">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c7edf-115">Można również przejść hello Zeppelin Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="c7edf-115">You may also reach hello Zeppelin Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="c7edf-116">Zastąp **CLUSTERNAME** o nazwie hello klastra:</span><span class="sxs-lookup"><span data-stu-id="c7edf-116">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. <span data-ttu-id="c7edf-117">Utwórz nowy notes.</span><span class="sxs-lookup"><span data-stu-id="c7edf-117">Create a new notebook.</span></span> <span data-ttu-id="c7edf-118">Okienko nagłówka hello, kliknij **notesu**, a następnie kliknij przycisk **Tworzenie nowej notatki**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-118">From hello header pane, click **Notebook**, and then click **Create New Note**.</span></span>
   
    <span data-ttu-id="c7edf-119">![Tworzenie nowego notesu Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Tworzenie nowego notesu Zeppelin")</span><span class="sxs-lookup"><span data-stu-id="c7edf-119">![Create a new Zeppelin notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Create a new Zeppelin notebook")</span></span>
   
    <span data-ttu-id="c7edf-120">Wprowadź nazwę notesu hello, a następnie kliknij przycisk **utworzyć Uwaga**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-120">Enter a name for hello notebook, and then click **Create Note**.</span></span>
3. <span data-ttu-id="c7edf-121">Ponadto upewnij się, że nagłówek notesu hello wyświetlany jest stan połączenia.</span><span class="sxs-lookup"><span data-stu-id="c7edf-121">Also, make sure hello notebook header shows a connected status.</span></span> <span data-ttu-id="c7edf-122">Jest oznaczany zielonym kropką w hello prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="c7edf-122">It is denoted by a green dot in hello top-right corner.</span></span>
   
    <span data-ttu-id="c7edf-123">![Stan notesu Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notesu stanu")</span><span class="sxs-lookup"><span data-stu-id="c7edf-123">![Zeppelin notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notebook status")</span></span>
4. <span data-ttu-id="c7edf-124">Załaduj przykładowe dane do tabeli tymczasowej.</span><span class="sxs-lookup"><span data-stu-id="c7edf-124">Load sample data into a temporary table.</span></span> <span data-ttu-id="c7edf-125">Podczas tworzenia klastra Spark w usłudze HDInsight, hello przykładowy plik danych **hvac.csv**, jest skopiowany toohello skojarzone konto magazynu w obszarze **\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-125">When you create a Spark cluster in HDInsight, hello sample data file, **hvac.csv**, is copied toohello associated storage account under **\HdiSamples\SensorSampleData\hvac**.</span></span>
   
    <span data-ttu-id="c7edf-126">W hello akapitu pusty jest domyślnie tworzona w hello nowy notes Wklej hello następującego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="c7edf-126">In hello empty paragraph that is created by default in hello new notebook, paste hello following snippet.</span></span>
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
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
   
    <span data-ttu-id="c7edf-127">Naciśnij klawisz **SHIFT + ENTER** lub kliknij przycisk hello **odtwarzanie** przycisk dla hello akapitu toorun hello fragmentu.</span><span class="sxs-lookup"><span data-stu-id="c7edf-127">Press **SHIFT + ENTER** or click hello **Play** button for hello paragraph toorun hello snippet.</span></span> <span data-ttu-id="c7edf-128">Stan Hello na powitania prawym dolnym rogu akapitu hello powinien postępu z GOTOWY do czasu tooFINISHED uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="c7edf-128">hello status on hello right-corner of hello paragraph should progress from READY, PENDING, RUNNING tooFINISHED.</span></span> <span data-ttu-id="c7edf-129">dane wyjściowe Hello zostaną wyświetlone u dołu hello hello tym samym obiekcie paragraph.</span><span class="sxs-lookup"><span data-stu-id="c7edf-129">hello output shows up at hello bottom of hello same paragraph.</span></span> <span data-ttu-id="c7edf-130">Zrzut ekranu Hello wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="c7edf-130">hello screenshot looks like hello following:</span></span>
   
    <span data-ttu-id="c7edf-131">![Tworzenie tabeli tymczasowej od danych pierwotnych](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Tworzenie tabeli tymczasowej od danych pierwotnych")</span><span class="sxs-lookup"><span data-stu-id="c7edf-131">![Create a temporary table from raw data](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Create a temporary table from raw data")</span></span>
   
    <span data-ttu-id="c7edf-132">Można też podać akapitu tooeach tytułu.</span><span class="sxs-lookup"><span data-stu-id="c7edf-132">You can also provide a title tooeach paragraph.</span></span> <span data-ttu-id="c7edf-133">W prawym górnym rogu powitania kliknij hello **ustawienia** ikonę, a następnie kliknij przycisk **Pokaż tytuł**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-133">From hello right-hand corner, click hello **Settings** icon, and then click **Show title**.</span></span>
5. <span data-ttu-id="c7edf-134">Teraz możesz uruchomić instrukcje Spark SQL na powitania **hvac** tabeli.</span><span class="sxs-lookup"><span data-stu-id="c7edf-134">You can now run Spark SQL statements on hello **hvac** table.</span></span> <span data-ttu-id="c7edf-135">Wklej hello następujące zapytanie w nowy akapit.</span><span class="sxs-lookup"><span data-stu-id="c7edf-135">Paste hello following query in a new paragraph.</span></span> <span data-ttu-id="c7edf-136">Witaj zapytanie pobiera identyfikator budynku hello i hello różnicy między hello docelowych i rzeczywistego temperatury dla każdego opierając się na dany dzień.</span><span class="sxs-lookup"><span data-stu-id="c7edf-136">hello query retrieves hello building ID and hello difference between hello target and actual temperatures for each building on a given date.</span></span> <span data-ttu-id="c7edf-137">Naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-137">Press **SHIFT + ENTER**.</span></span>
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    <span data-ttu-id="c7edf-138">Witaj **% sql** instrukcji na początku hello informuje hello notesu toouse hello Livy Scala interpreter.</span><span class="sxs-lookup"><span data-stu-id="c7edf-138">hello **%sql** statement at hello beginning tells hello notebook toouse hello Livy Scala interpreter.</span></span>
   
    <span data-ttu-id="c7edf-139">Witaj Poniższy zrzut ekranu przedstawia hello dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c7edf-139">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="c7edf-140">![Uruchom instrukcję Spark SQL za pomocą notesu hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "zestawienia Spark SQL za pomocą notesu hello")</span><span class="sxs-lookup"><span data-stu-id="c7edf-140">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "Run a Spark SQL statement using hello notebook")</span></span>
   
     <span data-ttu-id="c7edf-141">Kliknij przycisk hello wyświetlania opcje (wyróżniane na prostokąt) tooswitch między różne reprezentacje dla hello samych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c7edf-141">Click hello display options (highlighted in rectangle) tooswitch between different representations for hello same output.</span></span> <span data-ttu-id="c7edf-142">Kliknij przycisk **ustawienia** toochoose jakie consitutes hello klucza i wartości w danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="c7edf-142">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="c7edf-143">Witaj Przechwytywanie ekranu powyżej używa **buildingID** jako klucz hello i średnią hello **temp_diff** jako wartość hello.</span><span class="sxs-lookup"><span data-stu-id="c7edf-143">hello screen capture above uses **buildingID** as hello key and hello average of **temp_diff** as hello value.</span></span>
6. <span data-ttu-id="c7edf-144">Można również uruchomić używania zmiennych w zapytaniu hello instrukcje Spark SQL.</span><span class="sxs-lookup"><span data-stu-id="c7edf-144">You can also run Spark SQL statements using variables in hello query.</span></span> <span data-ttu-id="c7edf-145">Witaj dalej fragment kodu przedstawia sposób toodefine zmiennej, **Temp**, w zapytaniu hello z hello możliwe wartości ma tooquery z.</span><span class="sxs-lookup"><span data-stu-id="c7edf-145">hello next snippet shows how toodefine a variable, **Temp**, in hello query with hello possible values you want tooquery with.</span></span> <span data-ttu-id="c7edf-146">Przy pierwszym uruchomieniu zapytania hello, menu rozwijane jest automatycznie wypełniana określone dla zmiennej hello hello wartości.</span><span class="sxs-lookup"><span data-stu-id="c7edf-146">When you first run hello query, a drop-down is automatically populated with hello values you specified for hello variable.</span></span>
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    <span data-ttu-id="c7edf-147">Wklej następujący fragment kodu w nowy akapit i naciśnij klawisz **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-147">Paste this snippet in a new paragraph and press **SHIFT + ENTER**.</span></span> <span data-ttu-id="c7edf-148">Witaj Poniższy zrzut ekranu przedstawia hello dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c7edf-148">hello following screenshot shows hello output.</span></span>
   
    <span data-ttu-id="c7edf-149">![Uruchom instrukcję Spark SQL za pomocą notesu hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "zestawienia Spark SQL za pomocą notesu hello")</span><span class="sxs-lookup"><span data-stu-id="c7edf-149">![Run a Spark SQL statement using hello notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "Run a Spark SQL statement using hello notebook")</span></span>
   
    <span data-ttu-id="c7edf-150">Następnych kwerend można wybrać nową wartość z listy rozwijanej hello i ponownie uruchom zapytanie hello.</span><span class="sxs-lookup"><span data-stu-id="c7edf-150">For subsequent queries, you can select a new value from hello drop-down and run hello query again.</span></span> <span data-ttu-id="c7edf-151">Kliknij przycisk **ustawienia** toochoose jakie consitutes hello klucza i wartości w danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="c7edf-151">Click **Settings** toochoose what consitutes hello key and values in hello output.</span></span> <span data-ttu-id="c7edf-152">Witaj Przechwytywanie ekranu powyżej używa **buildingID** jako klucz hello hello średnią **temp_diff** jako wartość hello i **targettemp** jako hello grupy.</span><span class="sxs-lookup"><span data-stu-id="c7edf-152">hello screen capture above uses **buildingID** as hello key, hello average of **temp_diff** as hello value, and **targettemp** as hello group.</span></span>
7. <span data-ttu-id="c7edf-153">Uruchom ponownie hello Livy interpreter tooexit hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c7edf-153">Restart hello Livy interpreter tooexit hello application.</span></span> <span data-ttu-id="c7edf-154">toodo, Otwórz ustawienia interpreter klikając hello zalogowany nazwy użytkownika z hello prawym górnym rogu, a następnie kliknij przycisk **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-154">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="c7edf-155">![Uruchamianie interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="c7edf-155">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
8. <span data-ttu-id="c7edf-156">Przewiń tooLivy interpreter ustawienia, a następnie kliknij przycisk **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-156">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="c7edf-157">![Uruchom ponownie hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "ponowne uruchomienie hello Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="c7edf-157">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a><span data-ttu-id="c7edf-158">Jak korzystanie z zewnętrznych pakietów z notesem hello?</span><span class="sxs-lookup"><span data-stu-id="c7edf-158">How do I use external packages with hello notebook?</span></span>
<span data-ttu-id="c7edf-159">W klastrze Apache Spark na HDInsight (Linux) toouse zewnętrznych, przyczyniły się społeczności pakiety, które nie są uwzględniane out-of box hello klastra można skonfigurować hello Zeppelin notesu.</span><span class="sxs-lookup"><span data-stu-id="c7edf-159">You can configure hello Zeppelin notebook in Apache Spark cluster on HDInsight (Linux) toouse external, community-contributed packages that are not included out-of-the-box in hello cluster.</span></span> <span data-ttu-id="c7edf-160">Możesz przeszukać hello [repozytorium Maven](http://search.maven.org/) dla hello pełną listę pakietów, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="c7edf-160">You can search hello [Maven repository](http://search.maven.org/) for hello complete list of packages that are available.</span></span> <span data-ttu-id="c7edf-161">Można również uzyskać listę dostępnych pakietów z innych źródeł.</span><span class="sxs-lookup"><span data-stu-id="c7edf-161">You can also get a list of available packages from other sources.</span></span> <span data-ttu-id="c7edf-162">Na przykład pełną listę społeczności przyczyniły się do pakietów znajduje się w temacie [pakietów Spark](http://spark-packages.org/).</span><span class="sxs-lookup"><span data-stu-id="c7edf-162">For example, a complete list of community-contributed packages is available at [Spark Packages](http://spark-packages.org/).</span></span>

<span data-ttu-id="c7edf-163">W tym artykule, zobaczysz jak toouse hello [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakietu z hello notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="c7edf-163">In this article, you will see how toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package with hello Jupyter notebook.</span></span>

1. <span data-ttu-id="c7edf-164">Otwórz ustawienia interpreter.</span><span class="sxs-lookup"><span data-stu-id="c7edf-164">Open interpreter settings.</span></span> <span data-ttu-id="c7edf-165">Z hello prawym górnym rogu, kliknij hello rejestrowane w nazwie użytkownika, a następnie kliknij **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-165">From hello top-right corner, click hello logged in user name, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="c7edf-166">![Uruchamianie interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="c7edf-166">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="c7edf-167">Przewiń tooLivy interpreter ustawienia, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-167">Scroll tooLivy interpreter settings and then click **Edit**.</span></span>
   
    <span data-ttu-id="c7edf-168">![Zmień ustawienia interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "zmiany ustawień interpretera")</span><span class="sxs-lookup"><span data-stu-id="c7edf-168">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Change interpreter settings")</span></span>
3. <span data-ttu-id="c7edf-169">Dodaj nowy klucz o nazwie **livy.spark.jars.packages** i ustaw jej wartość w formacie hello `group:id:version`.</span><span class="sxs-lookup"><span data-stu-id="c7edf-169">Add a new key, called **livy.spark.jars.packages** and set its value in hello format `group:id:version`.</span></span> <span data-ttu-id="c7edf-170">Tak, jeśli chcesz toouse hello [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakietu, należy ustawić wartość hello klucza hello zbyt`com.databricks:spark-csv_2.10:1.4.0`.</span><span class="sxs-lookup"><span data-stu-id="c7edf-170">So, if you want toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, you must set hello value of hello key too`com.databricks:spark-csv_2.10:1.4.0`.</span></span>
   
    <span data-ttu-id="c7edf-171">![Zmień ustawienia interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "zmiany ustawień interpretera")</span><span class="sxs-lookup"><span data-stu-id="c7edf-171">![Change interpreter settings](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Change interpreter settings")</span></span>
   
    <span data-ttu-id="c7edf-172">Kliknij przycisk **zapisać** i uruchom ponownie hello Livy interpreter.</span><span class="sxs-lookup"><span data-stu-id="c7edf-172">Click **Save** and then restart hello Livy interpreter.</span></span>
4. <span data-ttu-id="c7edf-173">**Porada**: Jeśli chcesz toounderstand wprowadzania tooarrive na powitania wartość klucza hello powyżej, w tym sposób.</span><span class="sxs-lookup"><span data-stu-id="c7edf-173">**Tip**: If you want toounderstand how tooarrive at hello value of hello key entered above, here's how.</span></span>
   
    <span data-ttu-id="c7edf-174">a.</span><span class="sxs-lookup"><span data-stu-id="c7edf-174">a.</span></span> <span data-ttu-id="c7edf-175">Zlokalizuj pakiet hello w hello repozytorium Maven.</span><span class="sxs-lookup"><span data-stu-id="c7edf-175">Locate hello package in hello Maven Repository.</span></span> <span data-ttu-id="c7edf-176">W tym samouczku użyliśmy [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span><span class="sxs-lookup"><span data-stu-id="c7edf-176">For this tutorial, we used [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).</span></span>
   
    <span data-ttu-id="c7edf-177">b.</span><span class="sxs-lookup"><span data-stu-id="c7edf-177">b.</span></span> <span data-ttu-id="c7edf-178">Z repozytorium hello Zbierz wartości hello **GroupId**, **ArtifactId**, i **wersji**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-178">From hello repository, gather hello values for **GroupId**, **ArtifactId**, and **Version**.</span></span>
   
    <span data-ttu-id="c7edf-179">![Pakiety zewnętrzne za pomocą notesu Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "pakiety zewnętrzne za pomocą notesu Jupyter")</span><span class="sxs-lookup"><span data-stu-id="c7edf-179">![Use external packages with Jupyter notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Use external packages with Jupyter notebook")</span></span>
   
    <span data-ttu-id="c7edf-180">c.</span><span class="sxs-lookup"><span data-stu-id="c7edf-180">c.</span></span> <span data-ttu-id="c7edf-181">Łączenie hello trzech wartości oddzielonych dwukropkiem (**:**).</span><span class="sxs-lookup"><span data-stu-id="c7edf-181">Concatenate hello three values, separated by a colon (**:**).</span></span>
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a><span data-ttu-id="c7edf-182">Gdzie są hello notesów Zeppelin zapisać?</span><span class="sxs-lookup"><span data-stu-id="c7edf-182">Where are hello Zeppelin notebooks saved?</span></span>
<span data-ttu-id="c7edf-183">notesów Zeppelin Hello są zapisywane toohello headnodes klastra.</span><span class="sxs-lookup"><span data-stu-id="c7edf-183">hello Zeppelin notebooks are saved toohello cluster headnodes.</span></span> <span data-ttu-id="c7edf-184">Dlatego po usunięciu klastra hello notesów hello zostaną również usunięte.</span><span class="sxs-lookup"><span data-stu-id="c7edf-184">So, if you delete hello cluster, hello notebooks will be deleted as well.</span></span> <span data-ttu-id="c7edf-185">Jeśli chcesz toopreserve notesy do późniejszego użytku w innych klastrach, należy wyeksportować je po zakończeniu działania zadań hello.</span><span class="sxs-lookup"><span data-stu-id="c7edf-185">If you want toopreserve your notebooks for later use on other clusters, you must export them after you have finished running hello jobs.</span></span> <span data-ttu-id="c7edf-186">tooexport notesu, kliknij przycisk hello **wyeksportować** ikony, jak pokazano w poniższym obrazie hello.</span><span class="sxs-lookup"><span data-stu-id="c7edf-186">tooexport a notebook, click hello **Export** icon as shown in hello image below.</span></span>

<span data-ttu-id="c7edf-187">![Pobierz notesu](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "notesu hello pobierania")</span><span class="sxs-lookup"><span data-stu-id="c7edf-187">![Download notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "Download hello notebook")</span></span>

<span data-ttu-id="c7edf-188">To notesu hello jest zapisywany w formacie JSON w lokalizacji pobierania.</span><span class="sxs-lookup"><span data-stu-id="c7edf-188">This saves hello notebook as a JSON file in your download location.</span></span>

## <a name="livy-session-management"></a><span data-ttu-id="c7edf-189">Zarządzanie sesjami programu Livy</span><span class="sxs-lookup"><span data-stu-id="c7edf-189">Livy session management</span></span>
<span data-ttu-id="c7edf-190">Po uruchomieniu hello pierwszym akapicie kodu w notesie Zeppelin w nowej sesji programu Livy jest tworzony w klastrze Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7edf-190">When you run hello first code paragraph in your Zeppelin notebook, a new Livy session is created in your HDInsight Spark cluster.</span></span> <span data-ttu-id="c7edf-191">Ta sesja jest współużytkowana przez wszystkie notesów Zeppelin, które następnie utworzysz.</span><span class="sxs-lookup"><span data-stu-id="c7edf-191">This session is shared across all Zeppelin notebooks that you subsequently create.</span></span> <span data-ttu-id="c7edf-192">Jeśli dla niektórych hello Przyczyna Livy sesja jest skasowane (ponowne uruchomienie klastra, itp.), nie będą mogli toorun zadań hello Zeppelin notesu.</span><span class="sxs-lookup"><span data-stu-id="c7edf-192">If for some reason hello Livy session is killed (cluster reboot, etc.), you will not be able toorun jobs from hello Zeppelin notebook.</span></span>

<span data-ttu-id="c7edf-193">W takim przypadku należy wykonać następujące kroki, przed rozpoczęciem uruchomionych zadań z notesu Zeppelin hello.</span><span class="sxs-lookup"><span data-stu-id="c7edf-193">In such a case, you must perform hello following steps before you can start running jobs from a Zeppelin notebook.</span></span> 

1. <span data-ttu-id="c7edf-194">Uruchom ponownie hello interpreter Livy z hello Zeppelin notesu.</span><span class="sxs-lookup"><span data-stu-id="c7edf-194">Restart hello Livy interpreter from hello Zeppelin notebook.</span></span> <span data-ttu-id="c7edf-195">toodo, Otwórz ustawienia interpreter klikając hello zalogowany nazwy użytkownika z hello prawym górnym rogu, a następnie kliknij przycisk **Interpreter**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-195">toodo so, open interpreter settings by clicking hello logged in user name from hello top-right corner, and then click **Interpreter**.</span></span>
   
    <span data-ttu-id="c7edf-196">![Uruchamianie interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive danych wyjściowych")</span><span class="sxs-lookup"><span data-stu-id="c7edf-196">![Launch interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive output")</span></span>
2. <span data-ttu-id="c7edf-197">Przewiń tooLivy interpreter ustawienia, a następnie kliknij przycisk **ponownego uruchomienia**.</span><span class="sxs-lookup"><span data-stu-id="c7edf-197">Scroll tooLivy interpreter settings and then click **Restart**.</span></span>
   
    <span data-ttu-id="c7edf-198">![Uruchom ponownie hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "ponowne uruchomienie hello Zeppelin intepreter")</span><span class="sxs-lookup"><span data-stu-id="c7edf-198">![Restart hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "Restart hello Zeppelin intepreter")</span></span>
3. <span data-ttu-id="c7edf-199">Uruchom komórki kodu z istniejącego notesu Zeppelin.</span><span class="sxs-lookup"><span data-stu-id="c7edf-199">Run a code cell from an existing Zeppelin notebook.</span></span> <span data-ttu-id="c7edf-200">Spowoduje to utworzenie nowej sesji programu Livy hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7edf-200">This creates a new Livy session in hello HDInsight cluster.</span></span>

## <span data-ttu-id="c7edf-201"><a name="seealso"></a>Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c7edf-201"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="c7edf-202">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7edf-202">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="c7edf-203">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="c7edf-203">Scenarios</span></span>
* [<span data-ttu-id="c7edf-204">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="c7edf-204">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c7edf-205">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="c7edf-205">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c7edf-206">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7edf-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c7edf-207">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="c7edf-207">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c7edf-208">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7edf-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="c7edf-209">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="c7edf-209">Create and run applications</span></span>
* [<span data-ttu-id="c7edf-210">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="c7edf-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c7edf-211">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="c7edf-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c7edf-212">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="c7edf-212">Tools and extensions</span></span>
* [<span data-ttu-id="c7edf-213">Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="c7edf-213">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c7edf-214">Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="c7edf-214">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c7edf-215">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7edf-215">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c7edf-216">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="c7edf-216">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c7edf-217">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7edf-217">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="c7edf-218">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="c7edf-218">Manage resources</span></span>
* [<span data-ttu-id="c7edf-219">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7edf-219">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c7edf-220">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7edf-220">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







