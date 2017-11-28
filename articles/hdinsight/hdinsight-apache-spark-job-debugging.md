---
title: "aaaDebug Apache Spark, że zadania uruchomione w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj interfejsu użytkownika YARN, Spark interfejsu użytkownika i historię Spark serwera tootrack i debugowanie zadań uruchamianych w klastrze Spark w usłudze Azure HDInsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="ca6aa-103">Debugowanie Apache Spark zadań uruchamianych w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ca6aa-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="ca6aa-104">W tym artykule dowiesz się, jak tootrack i debugowania Spark zadania uruchomione w klastrach HDInsight przy użyciu hello interfejsie użytkownika YARN, Spark interfejsu użytkownika i hello Spark historii serwera.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-104">In this article you will learn how tootrack and debug Spark jobs running on HDInsight clusters using hello YARN UI, Spark UI, and hello Spark History Server.</span></span> <span data-ttu-id="ca6aa-105">W tym artykule, firma Microsoft uruchomi zadanie Spark przy użyciu Notes dostępnych z klastrem Spark hello, **uczenia maszynowego: analizy predykcyjnej na dane inspekcji żywności przy użyciu MLLib**.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-105">For this article, we will start a Spark job using a notebook available with hello Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="ca6aa-106">Można użyć hello kroków poniżej tootrack aplikacji, która zostanie przesłane za pomocą jakiejkolwiek innej metody, jak również na przykład **przesłać spark**.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-106">You can use hello steps below tootrack an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca6aa-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ca6aa-107">Prerequisites</span></span>
<span data-ttu-id="ca6aa-108">Musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ca6aa-108">You must have hello following:</span></span>

* <span data-ttu-id="ca6aa-109">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-109">An Azure subscription.</span></span> <span data-ttu-id="ca6aa-110">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ca6aa-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="ca6aa-111">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="ca6aa-112">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ca6aa-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="ca6aa-113">Powinien mieć uruchomienia notesu hello  **[uczenia maszynowego: analizy predykcyjnej na dane inspekcji żywności przy użyciu MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-113">You should have started running hello notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="ca6aa-114">Aby uzyskać instrukcje dotyczące toorun tego notesu wykonaj hello łącza.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-114">For instructions on how toorun this notebook, follow hello link.</span></span>  

## <a name="track-an-application-in-hello-yarn-ui"></a><span data-ttu-id="ca6aa-115">Śledzenie aplikacji w interfejsie użytkownika YARN hello</span><span class="sxs-lookup"><span data-stu-id="ca6aa-115">Track an application in hello YARN UI</span></span>
1. <span data-ttu-id="ca6aa-116">Uruchom program hello interfejsie użytkownika YARN.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-116">Launch hello YARN UI.</span></span> <span data-ttu-id="ca6aa-117">W bloku klastra powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **YARN**.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-117">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Uruchom interfejs użytkownika YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="ca6aa-119">Można również będzie można uruchomić hello interfejsie użytkownika YARN z hello interfejsu użytkownika narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-119">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="ca6aa-120">toolaunch hello interfejsu użytkownika narzędzia Ambari, w bloku klastra powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **pulpit nawigacyjny klastra usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-120">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="ca6aa-121">Hello interfejsu użytkownika narzędzia Ambari, kliknij **YARN**, kliknij przycisk **szybkie linki**, kliknij pozycję Menedżer zasobów active hello, a następnie kliknij przycisk **interfejsu użytkownika Menedżera ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-121">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="ca6aa-122">Ponieważ uruchomiono zadanie Spark hello za pomocą notesów Jupyter aplikacji hello ma nazwę hello **remotesparkmagics** (jest to nazwa powitania dla wszystkich aplikacji, które są uruchamiane z notesów hello).</span><span class="sxs-lookup"><span data-stu-id="ca6aa-122">Because you started hello Spark job using Jupyter notebooks, hello application has hello name **remotesparkmagics** (this is hello name for all applications that are started from hello notebooks).</span></span> <span data-ttu-id="ca6aa-123">Kliknij identyfikator aplikacji hello przed tooget nazwy aplikacji hello więcej informacji na temat hello zadania.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-123">Click hello application ID against hello application name tooget more information about hello job.</span></span> <span data-ttu-id="ca6aa-124">Spowoduje to uruchomienie widoku aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-124">This launches hello application view.</span></span>
   
    ![Znajdź identyfikator aplikacji Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="ca6aa-126">Dla tych aplikacji, które są uruchamiane z notesów Jupyter hello, stan hello jest zawsze **systemem** aż do zakończenia hello notesu.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-126">For such applications that are launched from hello Jupyter notebooks, hello status is always **RUNNING** until you exit hello notebook.</span></span>
3. <span data-ttu-id="ca6aa-127">Z widoku aplikacji hello można przejść dalsze toofind limit kontenery hello skojarzone z aplikacji hello i dzienniki hello (stdout/stderr).</span><span class="sxs-lookup"><span data-stu-id="ca6aa-127">From hello application view, you can drill down further toofind out hello containers associated with hello application and hello logs (stdout/stderr).</span></span> <span data-ttu-id="ca6aa-128">Hello Spark interfejsu użytkownika również można uruchomić, klikając hello łączenie odpowiedniego toohello **URL śledzenia**, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-128">You can also launch hello Spark UI by clicking hello linking corresponding toohello **Tracking URL**, as shown below.</span></span> 
   
    ![Pobierz dzienniki kontenera](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a><span data-ttu-id="ca6aa-130">Śledzenie aplikacji w hello Spark interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="ca6aa-130">Track an application in hello Spark UI</span></span>
<span data-ttu-id="ca6aa-131">W hello Spark interfejsu użytkownika można przejść się do hello Spark zadania, które są zduplikowany przez aplikacji hello, który został wcześniej uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-131">In hello Spark UI, you can drill down into hello Spark jobs that are spawned by hello application you started earlier.</span></span>

1. <span data-ttu-id="ca6aa-132">toolaunch hello Spark interfejsu użytkownika, z widoku aplikacji hello, kliknij łącze hello przed hello **URL śledzenia**, jak pokazano w hello Przechwytywanie ekranu powyżej.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-132">toolaunch hello Spark UI, from hello application view, click hello link against hello **Tracking URL**, as shown in hello screen capture above.</span></span> <span data-ttu-id="ca6aa-133">Wszystkie zadania Spark hello, które będą uruchamiane przez aplikacja hello notesu Jupyter hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-133">You can see all hello Spark jobs that are launched by hello application running in hello Jupyter notebook.</span></span>
   
    ![Wyświetlanie zadań Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="ca6aa-135">Kliknij przycisk hello **modułów** karcie toosee przetwarzania i przechowywania informacji dla każdego Moduł wykonujący.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-135">Click hello **Executors** tab toosee processing and storage information for each executor.</span></span> <span data-ttu-id="ca6aa-136">Można również pobierać hello stos wywołań, klikając hello **wątku zrzutu** łącza.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-136">You can also retrieve hello call stack by clicking on hello **Thread Dump** link.</span></span>
   
    ![Widok modułów Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="ca6aa-138">Kliknij przycisk hello **etapy** karcie etapy hello toosee skojarzoną z aplikacją hello.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-138">Click hello **Stages** tab toosee hello stages associated with hello application.</span></span>
   
    ![Etapy Spark widoku](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="ca6aa-140">Na każdym z etapów może mieć wielu zadań, dla których można wyświetlić statystyki wykonania tak samo, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Etapy Spark widoku](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="ca6aa-142">Na stronie szczegółów etap hello można uruchomić wizualizacji DAG.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-142">From hello stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="ca6aa-143">Rozwiń węzeł hello **wizualizacji DAG** łącze u góry hello hello strony, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-143">Expand hello **DAG Visualization** link at hello top of hello page, as shown below.</span></span>
   
    ![Wyświetl Spark etapy DAG wizualizacji](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="ca6aa-145">DAG lub bezpośredniego wykres Aclyic reprezentuje hello różnych etapach aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-145">DAG or Direct Aclyic Graph represents hello different stages in hello application.</span></span> <span data-ttu-id="ca6aa-146">Każde pole blue wykresie hello reprezentuje operację Spark wywoływane z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-146">Each blue box in hello graph represents a Spark operation invoked from hello application.</span></span>
5. <span data-ttu-id="ca6aa-147">Na stronie szczegółów etap hello możesz uruchomić widoku osi czasu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-147">From hello stage details page, you can also launch hello application timeline view.</span></span> <span data-ttu-id="ca6aa-148">Rozwiń węzeł hello **osi czasu zdarzeń** łącze u góry hello hello strony, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-148">Expand hello **Event Timeline** link at hello top of hello page, as shown below.</span></span>
   
    ![Wyświetl Spark etapy zdarzeń w osi czasu](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="ca6aa-150">Zostaną wyświetlone zdarzenia Spark hello w postaci hello osi czasu.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-150">This displays hello Spark events in hello form of a timeline.</span></span> <span data-ttu-id="ca6aa-151">Widok osi czasu Hello jest dostępny na trzech poziomach między zadania, zadania i w ramach etapu.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-151">hello timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="ca6aa-152">Powyższy obraz powitania przechwytuje hello widoku osi czasu dla danego etapu.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-152">hello image above captures hello timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ca6aa-153">W przypadku wybrania hello **włączyć powiększanie** pole wyboru można przechodzić z lewej i prawej między hello widoku osi czasu.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-153">If you select hello **Enable zooming** check box, you can scroll left and right across hello timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="ca6aa-154">Inne karty w hello interfejsu użytkownika Spark dostarczające przydatnych informacji na temat hello Spark również wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-154">Other tabs in hello Spark UI provide useful information about hello Spark instance as well.</span></span>
   
   * <span data-ttu-id="ca6aa-155">Karta magazynu — Jeśli aplikacja tworzy RDDs można znaleźć informacje o tych hello karcie magazynu.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-155">Storage tab - If your application creates an RDDs, you can find information about those in hello Storage tab.</span></span>
   * <span data-ttu-id="ca6aa-156">Karta środowiska — ta karta zawiera wiele przydatnych informacji o Spark wystąpienia takich jak hello</span><span class="sxs-lookup"><span data-stu-id="ca6aa-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as hello</span></span> 
     * <span data-ttu-id="ca6aa-157">Wersja języka scala</span><span class="sxs-lookup"><span data-stu-id="ca6aa-157">Scala version</span></span>
     * <span data-ttu-id="ca6aa-158">Katalog dziennika zdarzeń skojarzony z klastrem hello</span><span class="sxs-lookup"><span data-stu-id="ca6aa-158">Event log directory associated with hello cluster</span></span>
     * <span data-ttu-id="ca6aa-159">Liczba rdzeni Moduł wykonujący dla aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="ca6aa-159">Number of executor cores for hello application</span></span>
     * <span data-ttu-id="ca6aa-160">Itp.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a><span data-ttu-id="ca6aa-161">Informacje o zakończonych zadań przy użyciu hello Spark historii serwera</span><span class="sxs-lookup"><span data-stu-id="ca6aa-161">Find information about completed jobs using hello Spark History Server</span></span>
<span data-ttu-id="ca6aa-162">Po ukończeniu zadania w hello Spark historii serwera jest trwały hello informacji o zadaniu hello.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-162">Once a job is completed, hello information about hello job is persisted in hello Spark History Server.</span></span>

1. <span data-ttu-id="ca6aa-163">toolaunch hello Spark historii serwera, w bloku klastra powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **Spark historii serwera**.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-163">toolaunch hello Spark History Server, from hello cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Uruchamianie serwera historii Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="ca6aa-165">Można również będzie można uruchomić hello interfejsu użytkownika serwera historii Spark z hello interfejsu użytkownika narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-165">Alternatively, you can also launch hello Spark History Server UI from hello Ambari UI.</span></span> <span data-ttu-id="ca6aa-166">toolaunch hello interfejsu użytkownika narzędzia Ambari, w bloku klastra powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **pulpit nawigacyjny klastra usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-166">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="ca6aa-167">Hello interfejsu użytkownika narzędzia Ambari, kliknij **Spark**, kliknij przycisk **szybkie linki**, a następnie kliknij przycisk **interfejsu użytkownika serwera historii Spark**.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-167">From hello Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="ca6aa-168">Zostanie wyświetlone wszystkie aplikacje ukończyć powitalnych wymienione.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-168">You will see all hello completed applications listed.</span></span> <span data-ttu-id="ca6aa-169">Kliknij przycisk toodrill identyfikator aplikacji w dół do aplikacji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="ca6aa-169">Click an application ID toodrill down into an application for more info.</span></span>
   
    ![Uruchamianie serwera historii Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="ca6aa-171">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ca6aa-171">See also</span></span>
*  [<span data-ttu-id="ca6aa-172">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ca6aa-172">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="ca6aa-173">Dla analityków danych</span><span class="sxs-lookup"><span data-stu-id="ca6aa-173">For data analysts</span></span>

* [<span data-ttu-id="ca6aa-174">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="ca6aa-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="ca6aa-175">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="ca6aa-175">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ca6aa-176">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ca6aa-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="ca6aa-177">Analiza danych telemetrycznych usługi Application Insight przy użyciu platformy Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ca6aa-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="ca6aa-178">Użyj Caffe Azure HDInsight Spark dla rozproszonych learning bezpośrednich</span><span class="sxs-lookup"><span data-stu-id="ca6aa-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="ca6aa-179">Dla deweloperów platformy Spark</span><span class="sxs-lookup"><span data-stu-id="ca6aa-179">For Spark developers</span></span>

* [<span data-ttu-id="ca6aa-180">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="ca6aa-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ca6aa-181">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="ca6aa-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="ca6aa-182">Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="ca6aa-182">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="ca6aa-183">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="ca6aa-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="ca6aa-184">Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="ca6aa-184">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="ca6aa-185">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ca6aa-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="ca6aa-186">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ca6aa-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="ca6aa-187">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="ca6aa-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="ca6aa-188">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ca6aa-188">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


