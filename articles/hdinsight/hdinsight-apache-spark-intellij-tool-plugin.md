---
title: "Azure Toolkit for IntelliJ: tworzenie aplikacji Spark dla klastra usługi HDInsight | Dokumentacja firmy Microsoft"
description: "Zestaw narzędzi platformy Azure dla IntelliJ umożliwia tworzenie aplikacji Spark napisanych w języku Scala i przesyłanie ich do klastra Spark w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 19cb8f436fa4d86f323013a5d4b3b50bf6c80a1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="407cb-103">Zestaw narzędzi platformy Azure dla IntelliJ umożliwia tworzenie aplikacji Spark dla klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="407cb-103">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="407cb-104">Użyj narzędzi Azure for IntelliJ wtyczki do tworzenia aplikacji Spark napisanych w języku Scala i przesyłanie ich do klastra Spark w usłudze HDInsight bezpośrednio z IntelliJ zintegrowane środowisko programistyczne (IDE).</span><span class="sxs-lookup"><span data-stu-id="407cb-104">Use the Azure Toolkit for IntelliJ plug-in to develop Spark applications written in Scala, and then submit them to an HDInsight Spark cluster directly from the IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="407cb-105">Można użyć wtyczki na kilka sposobów:</span><span class="sxs-lookup"><span data-stu-id="407cb-105">You can use the plug-in in a few ways:</span></span>

* <span data-ttu-id="407cb-106">Tworzenie i przesyłanie aplikacji Scala Spark w klastrze Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="407cb-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="407cb-107">Dostęp do zasobów klastra Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="407cb-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="407cb-108">Tworzenie i uruchamianie aplikacji Scala Spark lokalnie.</span><span class="sxs-lookup"><span data-stu-id="407cb-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="407cb-109">Aby utworzyć projekt, Wyświetl [tworzenie aplikacji Spark narzędzi Azure dla IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) wideo.</span><span class="sxs-lookup"><span data-stu-id="407cb-109">To create your project, view the [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="407cb-110">Ten dodatek można użyć, aby utworzyć i przesłać aplikacji tylko w przypadku klastra Spark w usłudze HDInsight w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="407cb-110">You can use this plug-in to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="407cb-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="407cb-111">Prerequisites</span></span>

- <span data-ttu-id="407cb-112">Klaster Apache Spark w usłudze HDInsight w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="407cb-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="407cb-113">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="407cb-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="407cb-114">Oracle Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="407cb-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="407cb-115">Możesz zainstalować ją z [witryny sieci Web programu Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="407cb-115">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="407cb-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="407cb-116">IntelliJ IDEA.</span></span> <span data-ttu-id="407cb-117">W tym artykule używa wersji 2017.1.</span><span class="sxs-lookup"><span data-stu-id="407cb-117">This article uses version 2017.1.</span></span> <span data-ttu-id="407cb-118">Możesz zainstalować ją z [JetBrains witryny sieci Web](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="407cb-118">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="407cb-119">Zainstaluj zestaw narzędzi platformy Azure dla IntelliJ</span><span class="sxs-lookup"><span data-stu-id="407cb-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="407cb-120">Aby uzyskać instrukcje instalacji, zobacz [zainstalować zestaw narzędzi platformy Azure dla IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="407cb-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="407cb-121">Zaloguj się do Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="407cb-121">Sign in to your Azure subscription</span></span>

1. <span data-ttu-id="407cb-122">Uruchom IntelliJ IDE, a następnie otwórz Eksploratora Azure.</span><span class="sxs-lookup"><span data-stu-id="407cb-122">Start the IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="407cb-123">Na **widoku** menu, wybierz opcję **okna narzędzi**, a następnie wybierz **Eksploratora Azure**.</span><span class="sxs-lookup"><span data-stu-id="407cb-123">On the **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![Łącze Eksploratora Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="407cb-125">Kliknij prawym przyciskiem myszy **Azure** węzeł, a następnie wybierz **logowania**.</span><span class="sxs-lookup"><span data-stu-id="407cb-125">Right-click the **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="407cb-126">W **Azure logowania** wybierz pozycję **Zaloguj się**, a następnie wprowadź poświadczenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="407cb-126">In the **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Okno dialogowe Azure logowania](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="407cb-128">Po zalogowaniu, **Wybierz subskrypcje** okno dialogowe wyświetla wszystkie subskrypcje platformy Azure, które są skojarzone z poświadczeniami.</span><span class="sxs-lookup"><span data-stu-id="407cb-128">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions that are associated with the credentials.</span></span> <span data-ttu-id="407cb-129">Wybierz **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="407cb-129">Select the **Select** button.</span></span>

    ![Okno dialogowe Wybieranie subskrypcji](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="407cb-131">Na **Eksploratora Azure** karcie, rozwiń **HDInsight** do wyświetlania klastrów HDInsight Spark, które znajdują się w Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="407cb-131">On the **Azure Explorer** tab, expand **HDInsight** to view the HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Klastry HDInsight Spark w Eksploratorze Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="407cb-133">Aby wyświetlić zasoby, które są skojarzone z klastrem (na przykład konta magazynu), można rozwinąć węzła nazwy klastra.</span><span class="sxs-lookup"><span data-stu-id="407cb-133">To view the resources (for example, storage accounts) that are associated with the cluster, you can further expand a cluster-name node.</span></span>
   
    ![Nazwa klastra węzłów](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="407cb-135">Uruchamianie aplikacji Spark Scala w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="407cb-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="407cb-136">Uruchom IntelliJ IDEA, a następnie utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="407cb-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="407cb-137">W **nowy projekt** okno dialogowe, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="407cb-137">In the **New Project** dialog box, do the following:</span></span> 

   <span data-ttu-id="407cb-138">a.</span><span class="sxs-lookup"><span data-stu-id="407cb-138">a.</span></span> <span data-ttu-id="407cb-139">Wybierz **HDInsight** > **Spark w usłudze HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="407cb-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="407cb-140">b.</span><span class="sxs-lookup"><span data-stu-id="407cb-140">b.</span></span> <span data-ttu-id="407cb-141">W **narzędzia kompilacji** listy, wybierz jedną z następujących czynności, w zależności od potrzeb:</span><span class="sxs-lookup"><span data-stu-id="407cb-141">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="407cb-142">**Maven**, obsługę języka Scala Kreator tworzenia projektu</span><span class="sxs-lookup"><span data-stu-id="407cb-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="407cb-143">**SBT**, do zarządzania zależności i budowania projektu języka Scala</span><span class="sxs-lookup"><span data-stu-id="407cb-143">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![Okno dialogowe nowego projektu](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="407cb-145">Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="407cb-145">Select **Next**.</span></span>

3. <span data-ttu-id="407cb-146">Kreator tworzenia projektu Scala automatycznie wykrywa, czy po zainstalowaniu Scala wtyczki.</span><span class="sxs-lookup"><span data-stu-id="407cb-146">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span></span> <span data-ttu-id="407cb-147">Wybierz **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="407cb-147">Select **Install**.</span></span>

   ![Scala wtyczki wyboru](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="407cb-149">Aby pobrać dodatek plug-in Scala, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="407cb-149">To download the Scala plug-in, select **OK**.</span></span> <span data-ttu-id="407cb-150">Postępuj zgodnie z instrukcjami, aby ponownie uruchomić środowisko IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="407cb-150">Follow the instructions to restart IntelliJ.</span></span> 

   ![Okno dialogowe Scala wtyczki instalacji](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="407cb-152">W **nowy projekt** okna, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="407cb-152">In the **New Project** window, do the following:</span></span>  

    ![Wybieranie Spark zestawu SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="407cb-154">a.</span><span class="sxs-lookup"><span data-stu-id="407cb-154">a.</span></span> <span data-ttu-id="407cb-155">Wprowadź nazwę projektu i lokalizację.</span><span class="sxs-lookup"><span data-stu-id="407cb-155">Enter a project name and location.</span></span>

   <span data-ttu-id="407cb-156">b.</span><span class="sxs-lookup"><span data-stu-id="407cb-156">b.</span></span> <span data-ttu-id="407cb-157">W **SDK projektu** listy rozwijanej wybierz **Java 1.8** dla klastra Spark 2.x lub wybierz **Java 1.7** 1.x klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="407cb-157">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span>

   <span data-ttu-id="407cb-158">c.</span><span class="sxs-lookup"><span data-stu-id="407cb-158">c.</span></span> <span data-ttu-id="407cb-159">W **wersji Spark** listy rozwijanej, Kreator tworzenia projektu Scala integruje poprawnej wersji dla platformy Spark zestawy SDK i Scala.</span><span class="sxs-lookup"><span data-stu-id="407cb-159">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="407cb-160">Jeśli wersja klastra Spark jest starsza niż 2.0, wybierz **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="407cb-160">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="407cb-161">W przeciwnym razie wybierz **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="407cb-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="407cb-162">W tym przykładzie użyto **Spark pkt 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="407cb-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="407cb-163">Wybierz pozycję **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="407cb-163">Select **Finish**.</span></span>

7. <span data-ttu-id="407cb-164">Projekt Spark automatycznie utworzy artefaktu.</span><span class="sxs-lookup"><span data-stu-id="407cb-164">The Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="407cb-165">Aby wyświetlić artefakt, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="407cb-165">To view the artifact, do the following:</span></span>

   <span data-ttu-id="407cb-166">a.</span><span class="sxs-lookup"><span data-stu-id="407cb-166">a.</span></span> <span data-ttu-id="407cb-167">Na **pliku** menu, wybierz opcję **struktury projektu**.</span><span class="sxs-lookup"><span data-stu-id="407cb-167">On the **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="407cb-168">b.</span><span class="sxs-lookup"><span data-stu-id="407cb-168">b.</span></span> <span data-ttu-id="407cb-169">W **struktury projektu** okno dialogowe, wybierz opcję **artefakty** Aby wyświetlić artefaktu domyślny, który jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="407cb-169">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span></span> <span data-ttu-id="407cb-170">Można również tworzyć własne artefaktu, wybierając znak plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="407cb-170">You can also create your own artifact by selecting the plus sign (**+**).</span></span>

      ![W oknie dialogowym, informacje o artefaktów](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="407cb-172">Dodaj kod źródłowy aplikacji, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="407cb-172">Add your application source code by doing the following:</span></span>

   <span data-ttu-id="407cb-173">a.</span><span class="sxs-lookup"><span data-stu-id="407cb-173">a.</span></span> <span data-ttu-id="407cb-174">W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy **src**, wskaż polecenie **nowy**, a następnie wybierz **klasy Scala**.</span><span class="sxs-lookup"><span data-stu-id="407cb-174">In Project Explorer, right-click **src**, point to **New**, and then select **Scala Class**.</span></span>
      
      ![Polecenia służące do tworzenia klasy Scala w Eksploratorze projektu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="407cb-176">b.</span><span class="sxs-lookup"><span data-stu-id="407cb-176">b.</span></span> <span data-ttu-id="407cb-177">W **Utwórz nową klasę Scala** okna dialogowego polu, podaj nazwę, wybierz **obiektu** w **rodzaj** , a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="407cb-177">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span></span>
      
      ![Tworzenie nowej klasy Scala, okno dialogowe](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="407cb-179">c.</span><span class="sxs-lookup"><span data-stu-id="407cb-179">c.</span></span> <span data-ttu-id="407cb-180">W **MyClusterApp.scala** plików, wklej następujący kod.</span><span class="sxs-lookup"><span data-stu-id="407cb-180">In the **MyClusterApp.scala** file, paste the following code.</span></span> <span data-ttu-id="407cb-181">Ten kod odczytuje dane z HVAC.csv (dostępne na wszystkich klastrach HDInsight Spark), pobiera wierszy, które zawierają tylko jedna cyfra siódmego kolumny w pliku CSV i zapisuje dane wyjściowe do **/HVACOut** w obszarze domyślnego kontenera magazynu dla klastra.</span><span class="sxs-lookup"><span data-stu-id="407cb-181">The code reads the data from HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that have only one digit in the seventh column in the CSV file, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find the rows that have only one digit in the seventh column in the CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="407cb-182">Uruchom aplikację w klastrze Spark w usłudze HDInsight, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="407cb-182">Run the application on an HDInsight Spark cluster by doing the following:</span></span>

   <span data-ttu-id="407cb-183">a.</span><span class="sxs-lookup"><span data-stu-id="407cb-183">a.</span></span> <span data-ttu-id="407cb-184">W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy nazwę projektu, a następnie wybierz **przesyłanie aplikacji Spark HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="407cb-184">In Project Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>
      
      ![Aplikacji Spark przesłać do polecenia HDInsight](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="407cb-186">b.</span><span class="sxs-lookup"><span data-stu-id="407cb-186">b.</span></span> <span data-ttu-id="407cb-187">Monit o podanie poświadczeń subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="407cb-187">You are prompted to enter your Azure subscription credentials.</span></span> <span data-ttu-id="407cb-188">W **przesyłanie Spark** okno dialogowe, podaj następujące wartości, a następnie wybierz **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="407cb-188">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="407cb-189">Aby uzyskać **Spark klastrów (tylko w systemie Linux)**, wybierz klaster Spark w usłudze HDInsight, na którym chcesz uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="407cb-189">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span></span>

      * <span data-ttu-id="407cb-190">Wybierz artefakt z projektu IntelliJ lub wybierz jeden z dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="407cb-190">Select an artifact from the IntelliJ project, or select one from the hard drive.</span></span>

      * <span data-ttu-id="407cb-191">W **Nazwa klasy głównym** wybierz wielokropek (**...** ), wybierz klasy głównym w kodzie źródłowym aplikacji, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="407cb-191">In the **Main class name** box, select the ellipsis (**...**), select the main class in your application source code, and then select **OK**.</span></span>

        ![Okno dialogowe Wybieranie klasy głównym](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="407cb-193">Kod aplikacji, w tym przykładzie wymaga argumentów wiersza polecenia lub odwołać słoików lub pliki, pozostałe pola można pozostawić pusty.</span><span class="sxs-lookup"><span data-stu-id="407cb-193">Because the application code in this example does not require command-line arguments or reference JARs or files, you can leave the remaining boxes empty.</span></span> <span data-ttu-id="407cb-194">Po podaniu wszystkich informacji okno dialogowe powinno przypominać następujące obrazu.</span><span class="sxs-lookup"><span data-stu-id="407cb-194">After you provide all the information, the dialog box should resemble the following image.</span></span>
        
        ![Okno dialogowe przesyłanie Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="407cb-196">c.</span><span class="sxs-lookup"><span data-stu-id="407cb-196">c.</span></span> <span data-ttu-id="407cb-197">**Przesyłanie Spark** u dołu okna powinna zaczynać się wyświetlanie postępu.</span><span class="sxs-lookup"><span data-stu-id="407cb-197">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span></span> <span data-ttu-id="407cb-198">Można również Zatrzymaj aplikację, wybierając czerwony przycisk w **przesyłanie Spark** okna.</span><span class="sxs-lookup"><span data-stu-id="407cb-198">You can also stop the application by selecting the red button in the **Spark Submission** window.</span></span>
      
      ![Przesłanie Spark okna](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="407cb-200">Aby dowiedzieć się, jak uzyskać dostępu do danych wyjściowych zadania, zobacz "dostępu i zarządzania klastrami Spark w usłudze HDInsight przy użyciu zestawu narzędzi platformy Azure dla IntelliJ" sekcji w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="407cb-200">To learn how to access the job output, see the "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="407cb-201">Uruchom lub debugowanie aplikacji Spark Scala w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="407cb-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="407cb-202">Zalecamy również innym sposobem przesyłanie aplikacji Spark dla klastra.</span><span class="sxs-lookup"><span data-stu-id="407cb-202">We also recommend another way of submitting the Spark application to the cluster.</span></span> <span data-ttu-id="407cb-203">Możesz to zrobić przez ustawienie parametrów **konfiguracji uruchomienia/debugowania** IDE.</span><span class="sxs-lookup"><span data-stu-id="407cb-203">You can do so by setting the parameters in the **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="407cb-204">Aby uzyskać więcej informacji, zobacz [zdalne debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem protokołu SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="407cb-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="407cb-205">Dostęp i zarządzania klastrami Spark w usłudze HDInsight przy użyciu zestawu narzędzi platformy Azure dla IntelliJ</span><span class="sxs-lookup"><span data-stu-id="407cb-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="407cb-206">Różne operacje można wykonywać za pomocą narzędzi Azure for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="407cb-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="407cb-207">Dostęp do widoku zadania</span><span class="sxs-lookup"><span data-stu-id="407cb-207">Access the job view</span></span>
1. <span data-ttu-id="407cb-208">W Eksploratorze Azure rozwiń **HDInsight**, rozwiń nazwę klastra Spark, a następnie wybierz **zadania**.</span><span class="sxs-lookup"><span data-stu-id="407cb-208">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span></span>  

    ![Zadania widoku węzła](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="407cb-210">W okienku po prawej stronie **widoku zadania Spark** karcie są wyświetlane wszystkie aplikacje, które zostały uruchomione w klastrze.</span><span class="sxs-lookup"><span data-stu-id="407cb-210">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="407cb-211">Wybierz nazwę aplikacji, dla którego chcesz zobaczyć więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="407cb-211">Select the name of the application for which you want to see more details.</span></span>

    ![Szczegóły aplikacji](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="407cb-213">Aby wyświetlić podstawowe informacje o zadaniu uruchomione, umieść kursor nad wykresu zadania.</span><span class="sxs-lookup"><span data-stu-id="407cb-213">To display basic running job information, hover over the job graph.</span></span> <span data-ttu-id="407cb-214">Aby wyświetlić wykres etapów i informacje, które generuje każde zadanie, wybierz węzeł na wykresie zadania.</span><span class="sxs-lookup"><span data-stu-id="407cb-214">To view the stages graph and information that every job generates, select a node on the job graph.</span></span>

    ![Szczegóły etap zadania](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="407cb-216">Często używane dzienniki, taką jak *Stderr sterownika*, *Stdout sterownika*, i *informacji o katalogu*, wybierz pozycję **dziennika** kartę.</span><span class="sxs-lookup"><span data-stu-id="407cb-216">To view frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select the **Log** tab.</span></span>

    ![Szczegóły dziennika](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="407cb-218">Można również wyświetlić historię Spark interfejsu użytkownika i interfejsie użytkownika YARN (na poziomie aplikacji), klikając łącze w górnej części okna.</span><span class="sxs-lookup"><span data-stu-id="407cb-218">You can also view the Spark history UI and the YARN UI (at the application level) by selecting a link at the top of the window.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="407cb-219">Dostęp do serwera historii Spark</span><span class="sxs-lookup"><span data-stu-id="407cb-219">Access the Spark history server</span></span>
1. <span data-ttu-id="407cb-220">W Eksploratorze Azure rozwiń **HDInsight**, kliknij prawym przyciskiem myszy nazwę klastra Spark, a następnie wybierz **Otwórz użytkownika usługi Historia Spark**.</span><span class="sxs-lookup"><span data-stu-id="407cb-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="407cb-221">Po wyświetleniu monitu wprowadź poświadczenia administratora klastra, które zostało określone podczas konfigurowania klastra.</span><span class="sxs-lookup"><span data-stu-id="407cb-221">When you're prompted, enter the cluster's admin credentials, which you specified when you set up the cluster.</span></span>

3. <span data-ttu-id="407cb-222">Na pulpicie nawigacyjnym serwera Spark historii nazwę aplikacji służy do wyszukania aplikacji właśnie zakończono uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="407cb-222">On the Spark history server dashboard, you can use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="407cb-223">W powyższym kodzie, należy określić nazwę aplikacji przy użyciu `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="407cb-223">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="407cb-224">W związku z tym jest nazwa aplikacji Spark **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="407cb-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="407cb-225">Uruchom portalu Ambari</span><span class="sxs-lookup"><span data-stu-id="407cb-225">Start the Ambari portal</span></span>
1. <span data-ttu-id="407cb-226">W Eksploratorze Azure rozwiń **HDInsight**, kliknij prawym przyciskiem myszy nazwę klastra Spark, a następnie wybierz **Otwórz Portal zarządzania klastra (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="407cb-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="407cb-227">Po wyświetleniu monitu wprowadź poświadczenia administratora klastra.</span><span class="sxs-lookup"><span data-stu-id="407cb-227">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="407cb-228">Te poświadczenia zostały określone podczas procesu konfigurowania klastra.</span><span class="sxs-lookup"><span data-stu-id="407cb-228">You specified these credentials during the cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="407cb-229">Zarządzać subskrypcjami platformy Azure</span><span class="sxs-lookup"><span data-stu-id="407cb-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="407cb-230">Domyślnie zestaw narzędzi platformy Azure dla IntelliJ wymieniono klastry Spark wszystkie subskrypcje platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="407cb-230">By default, Azure Toolkit for IntelliJ lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="407cb-231">Jeśli to konieczne, można określić subskrypcje, które chcesz uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="407cb-231">If necessary, you can specify the subscriptions that you want to access.</span></span> 

1. <span data-ttu-id="407cb-232">W Eksploratorze Azure, kliknij prawym przyciskiem myszy **Azure** węzła głównego, a następnie wybierz **Zarządzaj subskrypcjami**.</span><span class="sxs-lookup"><span data-stu-id="407cb-232">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="407cb-233">W oknie dialogowym, wyczyść pola wyboru obok subskrypcje, które nie mają dostępu, a następnie wybierz **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="407cb-233">In the dialog box, clear the check boxes next to the subscriptions that you don't want to access, and then select **Close**.</span></span> <span data-ttu-id="407cb-234">Możesz też wybrać **Wyloguj** Aby wylogować się z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="407cb-234">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="407cb-235">Uruchamianie aplikacji Spark Scala lokalnie</span><span class="sxs-lookup"><span data-stu-id="407cb-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="407cb-236">Zestaw narzędzi platformy Azure dla IntelliJ umożliwia uruchamianie aplikacji Spark Scala lokalnie na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="407cb-236">You can use Azure Toolkit for IntelliJ to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="407cb-237">Aplikacje zazwyczaj nie potrzebują dostępu do zasobów klastra, takich jak kontenery magazynu i można uruchomić i przetestować je lokalnie.</span><span class="sxs-lookup"><span data-stu-id="407cb-237">The applications usually don't need access to cluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="407cb-238">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="407cb-238">Prerequisite</span></span>
<span data-ttu-id="407cb-239">Gdy używasz lokalnych aplikacji Spark Scala na komputerze z systemem Windows, można uzyskać wyjątku, zgodnie z objaśnieniem w [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="407cb-239">While you're running the local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="407cb-240">Wyjątek występuje, ponieważ brakuje WinUtils.exe w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="407cb-240">The exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="407cb-241">Aby rozwiązać ten problem, [Pobierz plik wykonywalny](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) do lokalizacji, takie jak **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="407cb-241">To resolve this error, [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="407cb-242">Następnie należy dodać zmienną środowiskową **HADOOP_HOME**, a następnie ustaw wartość zmiennej **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="407cb-242">Then, add the environment variable **HADOOP_HOME**, and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="407cb-243">Uruchamianie aplikacji Spark Scala lokalnej</span><span class="sxs-lookup"><span data-stu-id="407cb-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="407cb-244">Uruchom IntelliJ IDEA i tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="407cb-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="407cb-245">W **nowy projekt** okno dialogowe, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="407cb-245">In the **New Project** dialog box, do the following:</span></span>
   
    <span data-ttu-id="407cb-246">a.</span><span class="sxs-lookup"><span data-stu-id="407cb-246">a.</span></span> <span data-ttu-id="407cb-247">Wybierz **HDInsight** > **Spark dla próbki uruchamiania lokalnego HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="407cb-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="407cb-248">b.</span><span class="sxs-lookup"><span data-stu-id="407cb-248">b.</span></span> <span data-ttu-id="407cb-249">W **narzędzia kompilacji** listy, wybierz jedną z następujących czynności, w zależności od potrzeb:</span><span class="sxs-lookup"><span data-stu-id="407cb-249">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="407cb-250">**Maven**, obsługę języka Scala Kreator tworzenia projektu</span><span class="sxs-lookup"><span data-stu-id="407cb-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="407cb-251">**SBT**, do zarządzania zależności i budowania projektu języka Scala</span><span class="sxs-lookup"><span data-stu-id="407cb-251">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![Okno dialogowe nowego projektu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="407cb-253">Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="407cb-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="407cb-254">W następnym oknie wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="407cb-254">In the next window, do the following:</span></span>
   
    <span data-ttu-id="407cb-255">a.</span><span class="sxs-lookup"><span data-stu-id="407cb-255">a.</span></span> <span data-ttu-id="407cb-256">Wprowadź nazwę projektu i lokalizację.</span><span class="sxs-lookup"><span data-stu-id="407cb-256">Enter a project name and location.</span></span>

    <span data-ttu-id="407cb-257">b.</span><span class="sxs-lookup"><span data-stu-id="407cb-257">b.</span></span> <span data-ttu-id="407cb-258">W **SDK projektu** listy rozwijanej wybierz wersję Java, która jest nowsza niż wersja 1.7.</span><span class="sxs-lookup"><span data-stu-id="407cb-258">In the **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="407cb-259">c.</span><span class="sxs-lookup"><span data-stu-id="407cb-259">c.</span></span> <span data-ttu-id="407cb-260">W **wersji Spark** listy rozwijanej wybierz wersję języka Scala, którego chcesz używać: Scala 2.11.x dla platformy Spark w wersji 2.0 lub Scala 2.10.x dla wersji 1.6 Spark.</span><span class="sxs-lookup"><span data-stu-id="407cb-260">In the **Spark Version** drop-down list, select the version of Scala that you want to use: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![Okno dialogowe nowego projektu](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="407cb-262">Wybierz pozycję **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="407cb-262">Select **Finish**.</span></span>

6. <span data-ttu-id="407cb-263">Przykładowy kod dodaje szablonu (**LogQuery**) w obszarze **src** folderu, który można uruchomić lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="407cb-263">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![Lokalizacja LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="407cb-265">Kliknij prawym przyciskiem myszy **LogQuery** aplikacji, a następnie wybierz **Uruchom "LogQuery"**.</span><span class="sxs-lookup"><span data-stu-id="407cb-265">Right-click the **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="407cb-266">Na **Uruchom** kartę na dole pojawić się dane wyjściowe, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="407cb-266">On the **Run** tab at the bottom, you see an output like the following:</span></span>
   
   ![Aplikacji Spark lokalnego wynik uruchomienia](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-to-use-azure-toolkit-for-intellij"></a><span data-ttu-id="407cb-268">Konwertowanie istniejących aplikacji IntelliJ IDEA do użycia narzędzi Azure for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="407cb-268">Convert existing IntelliJ IDEA applications to use Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="407cb-269">Możesz przekształcić istniejącą Spark Scala aplikacji utworzonej w IntelliJ IDEA, aby był zgodny z narzędzi Azure dla IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="407cb-269">You can convert the existing Spark Scala applications that you created in IntelliJ IDEA to be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="407cb-270">Następnie można wtyczki przesyłania aplikacji do klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="407cb-270">You can then use the plug-in to submit the applications to an HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="407cb-271">Dla istniejącej aplikacji Spark Scala, który został utworzony za pomocą IntelliJ IDEA Otwórz plik .iml skojarzone.</span><span class="sxs-lookup"><span data-stu-id="407cb-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open the associated .iml file.</span></span>

2. <span data-ttu-id="407cb-272">W katalogu głównym poziom jest **modułu** element podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="407cb-272">At the root level is a **module** element like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="407cb-273">Zmodyfikuj element, aby dodać `UniqueKey="HDInsightTool"` , aby **modułu** element wygląda podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="407cb-273">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="407cb-274">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="407cb-274">Save the changes.</span></span> <span data-ttu-id="407cb-275">Aplikacja teraz powinno być zgodne z narzędzi Azure dla IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="407cb-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="407cb-276">Można przetestować go, klikając prawym przyciskiem myszy nazwę projektu w Eksploratorze projektu.</span><span class="sxs-lookup"><span data-stu-id="407cb-276">You can test it by right-clicking the project name in Project Explorer.</span></span> <span data-ttu-id="407cb-277">Menu podręczne ma teraz opcję **przesyłanie aplikacji Spark HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="407cb-277">The pop-up menu now has the option **Submit Spark Application to HDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="407cb-278">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="407cb-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="407cb-279">Błąd podczas uruchamiania lokalnego: *Użyj większego rozmiaru sterty*</span><span class="sxs-lookup"><span data-stu-id="407cb-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="407cb-280">W wersji 1.6 Spark Jeśli używasz SDK Java 32-bitowych podczas przebiegu lokalnego, mogą wystąpić następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="407cb-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter the following errors:</span></span>

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

<span data-ttu-id="407cb-281">Te błędy się tak zdarzyć, ponieważ rozmiar stosu nie jest wystarczająco duży dla Spark do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="407cb-281">These errors happen because the heap size is not large enough for Spark to run.</span></span> <span data-ttu-id="407cb-282">Platforma Spark wymaga co najmniej 471 MB.</span><span class="sxs-lookup"><span data-stu-id="407cb-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="407cb-283">(Aby uzyskać więcej informacji, zobacz [SPARK 12081](https://issues.apache.org/jira/browse/SPARK-12081).) Jeden prostym rozwiązaniem jest korzystanie z zestawu SDK Java 64-bitowych.</span><span class="sxs-lookup"><span data-stu-id="407cb-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is to use a 64-bit Java SDK.</span></span> <span data-ttu-id="407cb-284">Możesz również zmienić ustawienia maszyny JVM w IntelliJ, dodając następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="407cb-284">You can also change the JVM settings in IntelliJ by adding the following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Dodanie opcji do pola "Opcje maszyny Wirtualnej" IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="407cb-286">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="407cb-286">FAQ</span></span>
<span data-ttu-id="407cb-287">Aby przesłać aplikacji do usługi Azure Data Lake Store, wybierz **Interactive** tryb podczas Azure procesu logowania.</span><span class="sxs-lookup"><span data-stu-id="407cb-287">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="407cb-288">W przypadku wybrania **automatycznego** tryb, możesz uzyskać wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="407cb-288">If you select **Automated** mode, you can get an error.</span></span>

![interakcyjny rejestrowanie](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="407cb-290">Teraz możemy go rozwiązał.</span><span class="sxs-lookup"><span data-stu-id="407cb-290">Now, we resolved it.</span></span> <span data-ttu-id="407cb-291">Można wybrać Azure Data Lake klastra do przesyłania aplikacji przy użyciu dowolnej metody logowania.</span><span class="sxs-lookup"><span data-stu-id="407cb-291">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="407cb-292">Opinie i znane problemy</span><span class="sxs-lookup"><span data-stu-id="407cb-292">Feedback and known issues</span></span>
<span data-ttu-id="407cb-293">Przeglądanie wyjść Spark bezpośrednio nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="407cb-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="407cb-294">Jeśli masz jakiekolwiek sugestie lub opinii lub jeśli wystąpią problemy, korzystając z tego dodatku, wiadomość e-mail na adres hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="407cb-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="407cb-295"><a name="seealso"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="407cb-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="407cb-296">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="407cb-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="407cb-297">Demonstracja</span><span class="sxs-lookup"><span data-stu-id="407cb-297">Demo</span></span>
* <span data-ttu-id="407cb-298">Tworzenie projektu Scala (klip wideo): [tworzenie Spark Scala aplikacji](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="407cb-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="407cb-299">Debugowanie zdalne (klip wideo): [użyj narzędzi Azure dla IntelliJ debugowanie aplikacji Spark zdalnie w klastrze usługi HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="407cb-299">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="407cb-300">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="407cb-300">Scenarios</span></span>
* [<span data-ttu-id="407cb-301">Platforma Spark w usłudze BI: wykonaj interakcyjna analiza danych przy użyciu platformy Spark w usłudze HDInsight z narzędzi do analizy Biznesowej</span><span class="sxs-lookup"><span data-stu-id="407cb-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="407cb-302">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="407cb-302">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="407cb-303">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności</span><span class="sxs-lookup"><span data-stu-id="407cb-303">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="407cb-304">Przesyłanie strumieniowe Spark: Korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="407cb-304">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="407cb-305">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="407cb-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="407cb-306">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="407cb-306">Creating and running applications</span></span>
* [<span data-ttu-id="407cb-307">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="407cb-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="407cb-308">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="407cb-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="407cb-309">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="407cb-309">Tools and extensions</span></span>
* [<span data-ttu-id="407cb-310">Debugowanie aplikacji Spark zdalnie za pośrednictwem sieci VPN przy użyciu zestawu narzędzi Azure for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="407cb-310">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="407cb-311">Debugowanie aplikacji Spark zdalnie za pośrednictwem usługi SSH przy użyciu zestawu narzędzi Azure for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="407cb-311">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="407cb-312">Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="407cb-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="407cb-313">Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse tworzenie aplikacji Spark</span><span class="sxs-lookup"><span data-stu-id="407cb-313">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="407cb-314">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="407cb-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="407cb-315">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="407cb-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="407cb-316">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="407cb-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="407cb-317">Instalacja oprogramowania Jupyter na komputerze i nawiązywanie połączenia z klastrem Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="407cb-317">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="407cb-318">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="407cb-318">Managing resources</span></span>
* [<span data-ttu-id="407cb-319">Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="407cb-319">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="407cb-320">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="407cb-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

