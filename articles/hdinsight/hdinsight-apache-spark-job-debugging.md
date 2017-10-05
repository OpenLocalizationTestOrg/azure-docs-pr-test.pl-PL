---
title: "Debugowanie Apache Spark zadań uruchamianych w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj interfejsu użytkownika YARN, Spark interfejsu użytkownika i serwera Spark historii śledzenie i debugowanie zadań uruchamianych w klastrze Spark w usłudze Azure HDInsight"
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
ms.openlocfilehash: bf66757cc9439a969c9f28abc0b95055ff697c3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a><span data-ttu-id="cd4c9-103">Debugowanie Apache Spark zadań uruchamianych w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd4c9-103">Debug Apache Spark jobs running on Azure HDInsight</span></span>

<span data-ttu-id="cd4c9-104">W tym artykule dowiesz się, jak śledzenie i debugowanie zadań Spark uruchomionych w klastrach HDInsight przy użyciu interfejsu użytkownika YARN, Spark interfejsu użytkownika i serwera historii Spark.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-104">In this article you will learn how to track and debug Spark jobs running on HDInsight clusters using the YARN UI, Spark UI, and the Spark History Server.</span></span> <span data-ttu-id="cd4c9-105">W tym artykule, firma Microsoft uruchomi zadanie Spark przy użyciu Notes dostępnych z klastrem Spark **uczenia maszynowego: analizy predykcyjnej na dane inspekcji żywności przy użyciu MLLib**.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-105">For this article, we will start a Spark job using a notebook available with the Spark cluster, **Machine learning: Predictive analysis on food inspection data using MLLib**.</span></span> <span data-ttu-id="cd4c9-106">Poniższe kroki można użyć do śledzenia aplikacji, która zostanie przesłane za pomocą jakiejkolwiek innej metody, jak również na przykład **przesłać spark**.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-106">You can use the steps below to track an application that you submitted using any other approach as well, for example, **spark-submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd4c9-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cd4c9-107">Prerequisites</span></span>
<span data-ttu-id="cd4c9-108">Należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="cd4c9-108">You must have the following:</span></span>

* <span data-ttu-id="cd4c9-109">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-109">An Azure subscription.</span></span> <span data-ttu-id="cd4c9-110">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="cd4c9-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="cd4c9-111">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="cd4c9-112">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="cd4c9-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="cd4c9-113">Powinien mieć uruchomienia notesie  **[uczenia maszynowego: analizy predykcyjnej na dane inspekcji żywności przy użyciu MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-113">You should have started running the notebook, **[Machine learning: Predictive analysis on food inspection data using MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**.</span></span> <span data-ttu-id="cd4c9-114">Aby uzyskać instrukcje na temat uruchamiania tego notesu kliknij link.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-114">For instructions on how to run this notebook, follow the link.</span></span>  

## <a name="track-an-application-in-the-yarn-ui"></a><span data-ttu-id="cd4c9-115">Śledzenie aplikacji w Interfejsie użytkownika YARN</span><span class="sxs-lookup"><span data-stu-id="cd4c9-115">Track an application in the YARN UI</span></span>
1. <span data-ttu-id="cd4c9-116">Uruchom interfejs użytkownika YARN.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-116">Launch the YARN UI.</span></span> <span data-ttu-id="cd4c9-117">W bloku klastra, kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **YARN**.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-117">From the cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>
   
    ![Uruchom interfejs użytkownika YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > <span data-ttu-id="cd4c9-119">Alternatywnie można również uruchomić interfejsie użytkownika YARN z poziomu interfejsu użytkownika narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-119">Alternatively, you can also launch the YARN UI from the Ambari UI.</span></span> <span data-ttu-id="cd4c9-120">Aby uruchomić interfejs użytkownika narzędzia Ambari w bloku klastra, kliknij przycisk **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **pulpit nawigacyjny klastra usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-120">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="cd4c9-121">W interfejsie użytkownika narzędzia Ambari, kliknij przycisk **YARN**, kliknij przycisk **szybkie linki**, kliknij pozycję Menedżer zasobów aktywne, a następnie kliknij przycisk **interfejsu użytkownika Menedżera ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-121">From the Ambari UI, click **YARN**, click **Quick Links**, click the active resource manager, and then click **ResourceManager UI**.</span></span>    
   > 
   > 
2. <span data-ttu-id="cd4c9-122">Ponieważ uruchomiono zadanie Spark za pomocą notesów Jupyter aplikacji ma nazwę **remotesparkmagics** (jest to nazwa dla wszystkich aplikacji, które są uruchamiane z notesów).</span><span class="sxs-lookup"><span data-stu-id="cd4c9-122">Because you started the Spark job using Jupyter notebooks, the application has the name **remotesparkmagics** (this is the name for all applications that are started from the notebooks).</span></span> <span data-ttu-id="cd4c9-123">Kliknij przycisk Identyfikator aplikacji i nazwa aplikacji, aby uzyskać więcej informacji o zadaniu.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-123">Click the application ID against the application name to get more information about the job.</span></span> <span data-ttu-id="cd4c9-124">Spowoduje to uruchomienie widoku aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-124">This launches the application view.</span></span>
   
    ![Znajdź identyfikator aplikacji Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    <span data-ttu-id="cd4c9-126">Dla tych aplikacji, które są uruchamiane z notesów Jupyter, stan jest zawsze **systemem** aż do zakończenia notesu.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-126">For such applications that are launched from the Jupyter notebooks, the status is always **RUNNING** until you exit the notebook.</span></span>
3. <span data-ttu-id="cd4c9-127">Z widoku aplikacji użytkownik może przejść do szczegółów po dowiedzieć kontenery skojarzonych z aplikacji i dzienniki (stdout/stderr).</span><span class="sxs-lookup"><span data-stu-id="cd4c9-127">From the application view, you can drill down further to find out the containers associated with the application and the logs (stdout/stderr).</span></span> <span data-ttu-id="cd4c9-128">Można również Uruchom interfejs użytkownika Spark, klikając połączeń odpowiadający **URL śledzenia**, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-128">You can also launch the Spark UI by clicking the linking corresponding to the **Tracking URL**, as shown below.</span></span> 
   
    ![Pobierz dzienniki kontenera](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-the-spark-ui"></a><span data-ttu-id="cd4c9-130">Śledzenie aplikacji w Interfejsie użytkownika Spark</span><span class="sxs-lookup"><span data-stu-id="cd4c9-130">Track an application in the Spark UI</span></span>
<span data-ttu-id="cd4c9-131">W Interfejsie użytkownika Spark można przejść się do zadań Spark, które są zduplikowany przez aplikację, który został wcześniej uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-131">In the Spark UI, you can drill down into the Spark jobs that are spawned by the application you started earlier.</span></span>

1. <span data-ttu-id="cd4c9-132">Aby uruchomić interfejs użytkownika Spark z widoku aplikacji, kliknij łącze przed **URL śledzenia**, jak pokazano na zrzucie ekranu powyżej.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-132">To launch the Spark UI, from the application view, click the link against the **Tracking URL**, as shown in the screen capture above.</span></span> <span data-ttu-id="cd4c9-133">Można wyświetlić wszystkich zadań Spark, które będą uruchamiane przez aplikację w notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-133">You can see all the Spark jobs that are launched by the application running in the Jupyter notebook.</span></span>
   
    ![Wyświetlanie zadań Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. <span data-ttu-id="cd4c9-135">Kliknij przycisk **modułów** kartę do przetwarzania i przechowywania informacji dotyczących każdego Moduł wykonujący.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-135">Click the **Executors** tab to see processing and storage information for each executor.</span></span> <span data-ttu-id="cd4c9-136">Można również pobierać stos wywołań, klikając **wątku zrzutu** łącza.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-136">You can also retrieve the call stack by clicking on the **Thread Dump** link.</span></span>
   
    ![Widok modułów Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. <span data-ttu-id="cd4c9-138">Kliknij przycisk **etapy** kartę, aby wyświetlić etapy skojarzone z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-138">Click the **Stages** tab to see the stages associated with the application.</span></span>
   
    ![Etapy Spark widoku](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    <span data-ttu-id="cd4c9-140">Na każdym z etapów może mieć wielu zadań, dla których można wyświetlić statystyki wykonania tak samo, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-140">Each stage can have multiple tasks for which you can view execution statistics, like shown below.</span></span>
   
    ![Etapy Spark widoku](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. <span data-ttu-id="cd4c9-142">Na stronie szczegółów etapu można uruchomić wizualizacji grupy DAG.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-142">From the stage details page, you can launch DAG Visualization.</span></span> <span data-ttu-id="cd4c9-143">Rozwiń węzeł **wizualizacji DAG** link w górnej części strony, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-143">Expand the **DAG Visualization** link at the top of the page, as shown below.</span></span>
   
    ![Wyświetl Spark etapy DAG wizualizacji](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    <span data-ttu-id="cd4c9-145">DAG lub bezpośredniego wykres Aclyic reprezentuje różne etapy w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-145">DAG or Direct Aclyic Graph represents the different stages in the application.</span></span> <span data-ttu-id="cd4c9-146">Każde pole blue na wykresie reprezentuje operację Spark wywoływane z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-146">Each blue box in the graph represents a Spark operation invoked from the application.</span></span>
5. <span data-ttu-id="cd4c9-147">Na stronie szczegółów etapu można również uruchomić widoku osi czasu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-147">From the stage details page, you can also launch the application timeline view.</span></span> <span data-ttu-id="cd4c9-148">Rozwiń węzeł **osi czasu zdarzeń** link w górnej części strony, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-148">Expand the **Event Timeline** link at the top of the page, as shown below.</span></span>
   
    ![Wyświetl Spark etapy zdarzeń w osi czasu](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    <span data-ttu-id="cd4c9-150">Zostaną wyświetlone zdarzenia Spark w formie osi czasu.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-150">This displays the Spark events in the form of a timeline.</span></span> <span data-ttu-id="cd4c9-151">Widok osi czasu jest dostępny na trzech poziomach między zadania, zadania i w ramach etapu.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-151">The timeline view is available at three levels, across jobs, within a job, and within a stage.</span></span> <span data-ttu-id="cd4c9-152">Powyższy obraz przechwytuje widoku osi czasu dla danego etapu.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-152">The image above captures the timeline view for a given stage.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="cd4c9-153">W przypadku wybrania **włączyć powiększanie** pole wyboru można przechodzić z lewej i prawej w widoku osi czasu.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-153">If you select the **Enable zooming** check box, you can scroll left and right across the timeline view.</span></span>
   > 
   > 
6. <span data-ttu-id="cd4c9-154">Inne karty w Interfejsie użytkownika Spark dostarczające przydatnych informacji na temat z wystąpieniem platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-154">Other tabs in the Spark UI provide useful information about the Spark instance as well.</span></span>
   
   * <span data-ttu-id="cd4c9-155">Karta magazynu — Jeśli aplikacja tworzy RDDs można znaleźć informacje o tych na karcie pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-155">Storage tab - If your application creates an RDDs, you can find information about those in the Storage tab.</span></span>
   * <span data-ttu-id="cd4c9-156">Karta środowiska — ta karta zawiera wiele przydatnych informacji o wystąpieniu Spark takich jak</span><span class="sxs-lookup"><span data-stu-id="cd4c9-156">Environment tab - This tab provides a lot of useful information about your Spark instance such as the</span></span> 
     * <span data-ttu-id="cd4c9-157">Wersja języka scala</span><span class="sxs-lookup"><span data-stu-id="cd4c9-157">Scala version</span></span>
     * <span data-ttu-id="cd4c9-158">Katalog dziennika zdarzeń skojarzony z klastra</span><span class="sxs-lookup"><span data-stu-id="cd4c9-158">Event log directory associated with the cluster</span></span>
     * <span data-ttu-id="cd4c9-159">Liczba rdzeni Moduł wykonujący dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="cd4c9-159">Number of executor cores for the application</span></span>
     * <span data-ttu-id="cd4c9-160">Itp.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-160">Etc.</span></span>

## <a name="find-information-about-completed-jobs-using-the-spark-history-server"></a><span data-ttu-id="cd4c9-161">Informacje o zakończonych zadań przy użyciu serwera Spark historii</span><span class="sxs-lookup"><span data-stu-id="cd4c9-161">Find information about completed jobs using the Spark History Server</span></span>
<span data-ttu-id="cd4c9-162">Po ukończeniu zadania w serwerze historii Spark jest trwały informacji o zadaniu.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-162">Once a job is completed, the information about the job is persisted in the Spark History Server.</span></span>

1. <span data-ttu-id="cd4c9-163">Można uruchomić serwera historii Spark, w bloku klastra, kliknij przycisk **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **Spark historii serwera**.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-163">To launch the Spark History Server, from the cluster blade, click **Cluster Dashboard**, and then click **Spark History Server**.</span></span>
   
    ![Uruchamianie serwera historii Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > <span data-ttu-id="cd4c9-165">Można również będzie można uruchomić interfejs użytkownika serwera historii Spark w interfejsie użytkownika narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-165">Alternatively, you can also launch the Spark History Server UI from the Ambari UI.</span></span> <span data-ttu-id="cd4c9-166">Aby uruchomić interfejs użytkownika narzędzia Ambari w bloku klastra, kliknij przycisk **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **pulpit nawigacyjny klastra usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-166">To launch the Ambari UI, from the cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="cd4c9-167">W interfejsie użytkownika narzędzia Ambari, kliknij przycisk **Spark**, kliknij przycisk **szybkie linki**, a następnie kliknij przycisk **interfejsu użytkownika serwera historii Spark**.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-167">From the Ambari UI, click **Spark**, click **Quick Links**, and then click **Spark History Server UI**.</span></span>
   > 
   > 
2. <span data-ttu-id="cd4c9-168">Wyświetlona zostanie ukończone aplikacje wymienione.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-168">You will see all the completed applications listed.</span></span> <span data-ttu-id="cd4c9-169">Kliknij przycisk Identyfikator aplikacji, aby przejść do aplikacji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="cd4c9-169">Click an application ID to drill down into an application for more info.</span></span>
   
    ![Uruchamianie serwera historii Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a><span data-ttu-id="cd4c9-171">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cd4c9-171">See also</span></span>
*  [<span data-ttu-id="cd4c9-172">Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd4c9-172">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a><span data-ttu-id="cd4c9-173">Dla analityków danych</span><span class="sxs-lookup"><span data-stu-id="cd4c9-173">For data analysts</span></span>

* [<span data-ttu-id="cd4c9-174">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="cd4c9-174">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="cd4c9-175">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności</span><span class="sxs-lookup"><span data-stu-id="cd4c9-175">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="cd4c9-176">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd4c9-176">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="cd4c9-177">Analiza danych telemetrycznych usługi Application Insight przy użyciu platformy Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd4c9-177">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="cd4c9-178">Użyj Caffe Azure HDInsight Spark dla rozproszonych learning bezpośrednich</span><span class="sxs-lookup"><span data-stu-id="cd4c9-178">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="cd4c9-179">Dla deweloperów platformy Spark</span><span class="sxs-lookup"><span data-stu-id="cd4c9-179">For Spark developers</span></span>

* [<span data-ttu-id="cd4c9-180">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="cd4c9-180">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="cd4c9-181">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="cd4c9-181">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="cd4c9-182">Tworzenie i przesyłanie aplikacji Spark Scala przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="cd4c9-182">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="cd4c9-183">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="cd4c9-183">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="cd4c9-184">Zdalne debugowanie aplikacji Spark przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="cd4c9-184">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="cd4c9-185">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd4c9-185">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="cd4c9-186">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd4c9-186">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="cd4c9-187">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="cd4c9-187">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="cd4c9-188">Instalacja oprogramowania Jupyter na komputerze i nawiązywanie połączenia z klastrem Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd4c9-188">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


