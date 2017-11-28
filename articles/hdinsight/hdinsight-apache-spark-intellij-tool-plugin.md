---
title: "Azure Toolkit for IntelliJ: tworzenie aplikacji Spark dla klastra usługi HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj hello Azure zestawu narzędzi dla aplikacji Spark toodevelop IntelliJ napisanych w języku Scala i przesłać je tooan klastra Spark w usłudze HDInsight."
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
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="7f9bb-103">Użyj narzędzi Azure dla aplikacji Spark toocreate IntelliJ dla klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9bb-103">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="7f9bb-104">Użyj hello Azure zestawu narzędzi dla aplikacji Spark toodevelop wtyczkę IntelliJ napisanych w języku Scala, a następnie prześlij je tooan klastra Spark w usłudze HDInsight bezpośrednio z hello IntelliJ zintegrowane środowisko programistyczne (IDE).</span><span class="sxs-lookup"><span data-stu-id="7f9bb-104">Use hello Azure Toolkit for IntelliJ plug-in toodevelop Spark applications written in Scala, and then submit them tooan HDInsight Spark cluster directly from hello IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="7f9bb-105">Program hello wtyczki na kilka sposobów:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-105">You can use hello plug-in in a few ways:</span></span>

* <span data-ttu-id="7f9bb-106">Tworzenie i przesyłanie aplikacji Scala Spark w klastrze Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="7f9bb-107">Dostęp do zasobów klastra Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="7f9bb-108">Tworzenie i uruchamianie aplikacji Scala Spark lokalnie.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="7f9bb-109">toocreate Twojego projektu, widok hello [tworzenie aplikacji Spark przy użyciu hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) wideo.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-109">toocreate your project, view hello [Create Spark Applications with hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f9bb-110">Można użyć tej wtyczki toocreate i przesyłanie aplikacji tylko w przypadku klastra Spark w usłudze HDInsight w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-110">You can use this plug-in toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="7f9bb-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7f9bb-111">Prerequisites</span></span>

- <span data-ttu-id="7f9bb-112">Klaster Apache Spark w usłudze HDInsight w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="7f9bb-113">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="7f9bb-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="7f9bb-114">Oracle Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="7f9bb-115">Można ją zainstalować, korzystając z hello [witryny sieci Web programu Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="7f9bb-115">You can install it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="7f9bb-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-116">IntelliJ IDEA.</span></span> <span data-ttu-id="7f9bb-117">W tym artykule używa wersji 2017.1.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-117">This article uses version 2017.1.</span></span> <span data-ttu-id="7f9bb-118">Można ją zainstalować, korzystając z hello [JetBrains witryny sieci Web](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="7f9bb-118">You can install it from hello [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="7f9bb-119">Zainstaluj zestaw narzędzi platformy Azure dla IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7f9bb-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="7f9bb-120">Aby uzyskać instrukcje instalacji, zobacz [zainstalować zestaw narzędzi platformy Azure dla IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="7f9bb-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="7f9bb-121">Zaloguj się tooyour subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7f9bb-121">Sign in tooyour Azure subscription</span></span>

1. <span data-ttu-id="7f9bb-122">Uruchom hello IntelliJ IDE, a następnie otwórz Eksploratora Azure.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-122">Start hello IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="7f9bb-123">Na powitania **widoku** menu, wybierz opcję **okna narzędzi**, a następnie wybierz **Eksploratora Azure**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-123">On hello **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![łącze Eksploratora Azure Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="7f9bb-125">Kliknij prawym przyciskiem myszy hello **Azure** węzeł, a następnie wybierz **logowania**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-125">Right-click hello **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="7f9bb-126">W hello **Azure logowania** wybierz pozycję **Zaloguj się**, a następnie wprowadź poświadczenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-126">In hello **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Hello Azure logowania — okno dialogowe](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="7f9bb-128">Po zalogowaniu hello **Wybierz subskrypcje** list okno dialogowe hello wszystkie subskrypcje platformy Azure, które są skojarzone z hello poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-128">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions that are associated with hello credentials.</span></span> <span data-ttu-id="7f9bb-129">Wybierz hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-129">Select hello **Select** button.</span></span>

    ![Wybierz subskrypcje Hello — okno dialogowe](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="7f9bb-131">Na powitania **Eksploratora Azure** karcie, rozwiń **HDInsight** hello tooview klastry Spark w usłudze HDInsight, które są w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-131">On hello **Azure Explorer** tab, expand **HDInsight** tooview hello HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Klastry HDInsight Spark w Eksploratorze Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="7f9bb-133">tooview hello zasobów (na przykład konta magazynu) skojarzonych z hello klastra, można rozwinąć węzła nazwy klastra.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-133">tooview hello resources (for example, storage accounts) that are associated with hello cluster, you can further expand a cluster-name node.</span></span>
   
    ![Nazwa klastra węzłów](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="7f9bb-135">Uruchamianie aplikacji Spark Scala w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9bb-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="7f9bb-136">Uruchom IntelliJ IDEA, a następnie utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="7f9bb-137">W hello **nowy projekt** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-137">In hello **New Project** dialog box, do hello following:</span></span> 

   <span data-ttu-id="7f9bb-138">a.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-138">a.</span></span> <span data-ttu-id="7f9bb-139">Wybierz **HDInsight** > **Spark w usłudze HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="7f9bb-140">b.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-140">b.</span></span> <span data-ttu-id="7f9bb-141">W hello **narzędzia kompilacji** listy, wybierz opcję powitania po, zgodnie z tooyour potrzeby:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-141">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="7f9bb-142">**Maven**, obsługę języka Scala Kreator tworzenia projektu</span><span class="sxs-lookup"><span data-stu-id="7f9bb-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="7f9bb-143">**SBT**, do zarządzania hello zależności i budowania hello Scala projektu</span><span class="sxs-lookup"><span data-stu-id="7f9bb-143">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![okno dialogowe Nowy projekt Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="7f9bb-145">Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-145">Select **Next**.</span></span>

3. <span data-ttu-id="7f9bb-146">Kreator tworzenia projektu Scala Hello automatycznie wykrywa, czy po zainstalowaniu hello Scala wtyczki.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-146">hello Scala project-creation wizard automatically detects whether you've installed hello Scala plug-in.</span></span> <span data-ttu-id="7f9bb-147">Wybierz **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-147">Select **Install**.</span></span>

   ![Scala wtyczki wyboru](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="7f9bb-149">Witaj toodownload Scala wtyczki, wybierz pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-149">toodownload hello Scala plug-in, select **OK**.</span></span> <span data-ttu-id="7f9bb-150">Wykonaj hello instrukcje toorestart IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-150">Follow hello instructions toorestart IntelliJ.</span></span> 

   ![okno dialogowe instalacji Hello Scala wtyczki](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="7f9bb-152">W hello **nowy projekt** oknie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-152">In hello **New Project** window, do hello following:</span></span>  

    ![Wybieranie hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="7f9bb-154">a.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-154">a.</span></span> <span data-ttu-id="7f9bb-155">Wprowadź nazwę projektu i lokalizację.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-155">Enter a project name and location.</span></span>

   <span data-ttu-id="7f9bb-156">b.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-156">b.</span></span> <span data-ttu-id="7f9bb-157">W hello **SDK projektu** listy rozwijanej wybierz **Java 1.8** dla klastra 2.x Spark hello, lub wybierz **Java 1.7** hello Spark 1.x klastra.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-157">In hello **Project SDK** drop-down list, select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span>

   <span data-ttu-id="7f9bb-158">c.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-158">c.</span></span> <span data-ttu-id="7f9bb-159">W hello **wersji Spark** listy rozwijanej, Kreator tworzenia projektu Scala integruje hello poprawnej wersji dla platformy Spark zestawy SDK i Scala.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-159">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="7f9bb-160">Jeśli hello klastra Spark w wersji starszej niż 2.0, wybierz **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-160">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="7f9bb-161">W przeciwnym razie wybierz **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="7f9bb-162">W tym przykładzie użyto **Spark pkt 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="7f9bb-163">Wybierz pozycję **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="7f9bb-163">Select **Finish**.</span></span>

7. <span data-ttu-id="7f9bb-164">Projekt Spark Hello automatycznie utworzy artefaktu.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-164">hello Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="7f9bb-165">tooview hello artefaktu, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-165">tooview hello artifact, do hello following:</span></span>

   <span data-ttu-id="7f9bb-166">a.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-166">a.</span></span> <span data-ttu-id="7f9bb-167">Na powitania **pliku** menu, wybierz opcję **struktury projektu**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-167">On hello **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="7f9bb-168">b.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-168">b.</span></span> <span data-ttu-id="7f9bb-169">W hello **struktury projektu** okno dialogowe, wybierz opcję **artefakty** tooview hello domyślne artefaktu, który jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-169">In hello **Project Structure** dialog box, select **Artifacts** tooview hello default artifact that is created.</span></span> <span data-ttu-id="7f9bb-170">Można również utworzyć własne artefaktu, wybierając hello — znak plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="7f9bb-170">You can also create your own artifact by selecting hello plus sign (**+**).</span></span>

      ![Informacje o artefaktów w hello — okno dialogowe](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="7f9bb-172">Należy dodać kodu źródłowego aplikacji, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-172">Add your application source code by doing hello following:</span></span>

   <span data-ttu-id="7f9bb-173">a.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-173">a.</span></span> <span data-ttu-id="7f9bb-174">W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy **src**, punktu zbyt**nowy**, a następnie wybierz **klasy Scala**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-174">In Project Explorer, right-click **src**, point too**New**, and then select **Scala Class**.</span></span>
      
      ![Polecenia służące do tworzenia klasy Scala w Eksploratorze projektu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="7f9bb-176">b.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-176">b.</span></span> <span data-ttu-id="7f9bb-177">W hello **Utwórz nową klasę Scala** okna dialogowego polu, podaj nazwę, wybierz **obiektu** w hello **rodzaj** , a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-177">In hello **Create New Scala Class** dialog box, provide a name, select **Object** in hello **Kind** box, and then select **OK**.</span></span>
      
      ![Tworzenie nowej klasy Scala, okno dialogowe](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="7f9bb-179">c.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-179">c.</span></span> <span data-ttu-id="7f9bb-180">W hello **MyClusterApp.scala** plików, Wklej hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-180">In hello **MyClusterApp.scala** file, paste hello following code.</span></span> <span data-ttu-id="7f9bb-181">Witaj kod odczytuje dane hello z HVAC.csv (dostępne na wszystkich klastrach HDInsight Spark), pobiera hello wiersze, które mają tylko jedna cyfra hello siódmego kolumny w pliku CSV hello i zapisuje dane wyjściowe hello zbyt**/HVACOut** w obszarze hello domyślne kontener magazynu hello klaster.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-181">hello code reads hello data from HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that have only one digit in hello seventh column in hello CSV file, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="7f9bb-182">Uruchom aplikację hello w klastrze Spark w usłudze HDInsight, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-182">Run hello application on an HDInsight Spark cluster by doing hello following:</span></span>

   <span data-ttu-id="7f9bb-183">a.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-183">a.</span></span> <span data-ttu-id="7f9bb-184">W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy nazwę projektu hello, a następnie wybierz **tooHDInsight przesyłanie aplikacji Spark**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-184">In Project Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>
      
      ![polecenie tooHDInsight przesyłanie aplikacji Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="7f9bb-186">b.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-186">b.</span></span> <span data-ttu-id="7f9bb-187">Możesz są tooenter zostanie wyświetlony monit o poświadczenia subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-187">You are prompted tooenter your Azure subscription credentials.</span></span> <span data-ttu-id="7f9bb-188">W hello **przesyłanie Spark** okno dialogowe, podaj hello następujące wartości, a następnie wybierz **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-188">In hello **Spark Submission** dialog box, provide hello following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="7f9bb-189">Aby uzyskać **Spark klastrów (tylko w systemie Linux)**, wybierz hello klaster Spark w usłudze HDInsight, na którym ma zostać toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-189">For **Spark clusters (Linux only)**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>

      * <span data-ttu-id="7f9bb-190">Wybierz artefakt z projektu IntelliJ hello, lub wybierz jedną z dysku twardego hello.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-190">Select an artifact from hello IntelliJ project, or select one from hello hard drive.</span></span>

      * <span data-ttu-id="7f9bb-191">W hello **Nazwa klasy głównym** polu Wybierz hello wielokropka (**...** ), wybierz klasy głównym hello w kodzie źródłowym aplikacji, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-191">In hello **Main class name** box, select hello ellipsis (**...**), select hello main class in your application source code, and then select **OK**.</span></span>

        ![okno dialogowe Wybieranie klasy głównym Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="7f9bb-193">Kod aplikacji hello w tym przykładzie wymaga argumentów wiersza polecenia lub odwołać słoików lub pliki, można pozostawić hello pozostałe pola puste.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-193">Because hello application code in this example does not require command-line arguments or reference JARs or files, you can leave hello remaining boxes empty.</span></span> <span data-ttu-id="7f9bb-194">Po podaniu wszystkich informacji hello hello — okno dialogowe powinno przypominać powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-194">After you provide all hello information, hello dialog box should resemble hello following image.</span></span>
        
        ![okno dialogowe przesyłanie Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="7f9bb-196">c.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-196">c.</span></span> <span data-ttu-id="7f9bb-197">Witaj **przesyłanie Spark** u dołu hello hello powinien rozpocząć hello postęp wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-197">hello **Spark Submission** tab at hello bottom of hello window should start displaying hello progress.</span></span> <span data-ttu-id="7f9bb-198">Mogą również wstrzymać aplikacja hello, wybierając przycisk hello red hello **przesyłanie Spark** okna.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-198">You can also stop hello application by selecting hello red button in hello **Spark Submission** window.</span></span>
      
      ![Witaj przesyłanie Spark okna](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="7f9bb-200">toolearn tooaccess hello dane wyjściowe zadania, zobacz hello "dostępu i zarządzania klastrami Spark w usłudze HDInsight przy użyciu zestawu narzędzi platformy Azure dla IntelliJ" sekcji w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-200">toolearn how tooaccess hello job output, see hello "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="7f9bb-201">Uruchom lub debugowanie aplikacji Spark Scala w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9bb-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="7f9bb-202">Zalecamy również inny sposób przesyłania hello Spark aplikacji toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-202">We also recommend another way of submitting hello Spark application toohello cluster.</span></span> <span data-ttu-id="7f9bb-203">Możesz to zrobić przez ustawienie parametrów hello w hello **konfiguracji uruchomienia/debugowania** IDE.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-203">You can do so by setting hello parameters in hello **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="7f9bb-204">Aby uzyskać więcej informacji, zobacz [zdalne debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem protokołu SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="7f9bb-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="7f9bb-205">Dostęp i zarządzania klastrami Spark w usłudze HDInsight przy użyciu zestawu narzędzi platformy Azure dla IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7f9bb-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="7f9bb-206">Różne operacje można wykonywać za pomocą narzędzi Azure for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="7f9bb-207">Wyświetl zadania hello dostępu</span><span class="sxs-lookup"><span data-stu-id="7f9bb-207">Access hello job view</span></span>
1. <span data-ttu-id="7f9bb-208">W Eksploratorze Azure rozwiń **HDInsight**, rozwiń nazwę klastra Spark hello, a następnie wybierz **zadania**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-208">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then select **Jobs**.</span></span>  

    ![Zadania widoku węzła](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="7f9bb-210">W okienku po prawej stronie powitania, hello **widoku zadania Spark** karcie są wyświetlane wszystkie aplikacje hello, które zostały uruchomione w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-210">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="7f9bb-211">Wybierz nazwę hello aplikacji hello, dla której ma zostać toosee więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-211">Select hello name of hello application for which you want toosee more details.</span></span>

    ![Szczegóły aplikacji](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="7f9bb-213">toodisplay podstawowe uruchomione zadania informacje, przesuń kursor myszy hello wykres zadania.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-213">toodisplay basic running job information, hover over hello job graph.</span></span> <span data-ttu-id="7f9bb-214">Wykres etapy hello tooview i informacje, które generuje każde zadanie, wybierz węzeł na powitania wykres zadania.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-214">tooview hello stages graph and information that every job generates, select a node on hello job graph.</span></span>

    ![Szczegóły etap zadania](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="7f9bb-216">tooview często używane dzienniki, taką jak *Stderr sterownika*, *Stdout sterownika*, i *informacji o katalogu*, wybierz pozycję hello **dziennika** kartę.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-216">tooview frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select hello **Log** tab.</span></span>

    ![Szczegóły dziennika](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="7f9bb-218">Można również wyświetlić hello historii Spark interfejsu użytkownika i hello interfejsie użytkownika YARN (na poziomie aplikacji hello), klikając łącze u góry okna hello hello.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-218">You can also view hello Spark history UI and hello YARN UI (at hello application level) by selecting a link at hello top of hello window.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="7f9bb-219">Dostęp do serwera historii Spark hello</span><span class="sxs-lookup"><span data-stu-id="7f9bb-219">Access hello Spark history server</span></span>
1. <span data-ttu-id="7f9bb-220">W Eksploratorze Azure rozwiń **HDInsight**, kliknij prawym przyciskiem myszy nazwę klastra Spark, a następnie wybierz **Otwórz użytkownika usługi Historia Spark**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="7f9bb-221">Po wyświetleniu monitu wprowadź poświadczenia administratora klastra hello, które określona podczas konfigurowania klastra hello.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-221">When you're prompted, enter hello cluster's admin credentials, which you specified when you set up hello cluster.</span></span>

3. <span data-ttu-id="7f9bb-222">Na powitania Spark historii serwera pulpitu nawigacyjnego można użyć toolook Nazwa aplikacji hello aplikacji hello właśnie zakończono uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-222">On hello Spark history server dashboard, you can use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="7f9bb-223">W hello poprzedzających kodu, należy określić nazwę aplikacji hello przy użyciu `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-223">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="7f9bb-224">W związku z tym jest nazwa aplikacji Spark **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="7f9bb-225">Uruchom hello Ambari portalu</span><span class="sxs-lookup"><span data-stu-id="7f9bb-225">Start hello Ambari portal</span></span>
1. <span data-ttu-id="7f9bb-226">W Eksploratorze Azure rozwiń **HDInsight**, kliknij prawym przyciskiem myszy nazwę klastra Spark, a następnie wybierz **Otwórz Portal zarządzania klastra (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="7f9bb-227">Po wyświetleniu monitu wprowadź poświadczenia administratora hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-227">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="7f9bb-228">Te poświadczenia zostały określone podczas procesu instalacji hello klastra.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-228">You specified these credentials during hello cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="7f9bb-229">Zarządzać subskrypcjami platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7f9bb-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="7f9bb-230">Domyślnie zestaw narzędzi platformy Azure dla IntelliJ wymieniono klastry Spark hello wszystkie subskrypcje platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-230">By default, Azure Toolkit for IntelliJ lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="7f9bb-231">W razie potrzeby można określić, które mają tooaccess subskrypcje hello.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-231">If necessary, you can specify hello subscriptions that you want tooaccess.</span></span> 

1. <span data-ttu-id="7f9bb-232">W Eksploratorze Azure, kliknij prawym przyciskiem myszy hello **Azure** węzła głównego, a następnie wybierz **Zarządzaj subskrypcjami**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-232">In Azure Explorer, right-click hello **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="7f9bb-233">Okno dialogowe hello, wyczyść hello pola wyboru dalej toohello subskrypcje czy nie ma tooaccess, a następnie wybierz **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-233">In hello dialog box, clear hello check boxes next toohello subscriptions that you don't want tooaccess, and then select **Close**.</span></span> <span data-ttu-id="7f9bb-234">Możesz też wybrać **Wyloguj** Jeśli chcesz toosign poza subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-234">You can also select **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="7f9bb-235">Uruchamianie aplikacji Spark Scala lokalnie</span><span class="sxs-lookup"><span data-stu-id="7f9bb-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="7f9bb-236">Umożliwia zestawu narzędzi platformy Azure dla aplikacji Spark Scala toorun IntelliJ lokalnie na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-236">You can use Azure Toolkit for IntelliJ toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="7f9bb-237">aplikacji Hello zwykle nie wymagają dostępu toocluster zasoby, takie jak kontenery magazynu i można uruchomić i przetestować je lokalnie.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-237">hello applications usually don't need access toocluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="7f9bb-238">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7f9bb-238">Prerequisite</span></span>
<span data-ttu-id="7f9bb-239">Gdy używasz lokalnych aplikacji Spark Scala hello na komputerze z systemem Windows, można uzyskać wyjątku, zgodnie z objaśnieniem w [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="7f9bb-239">While you're running hello local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="7f9bb-240">Wystąpił wyjątek Hello, ponieważ brakuje WinUtils.exe w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-240">hello exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="7f9bb-241">tooresolve ten błąd [Pobierz hello wykonywalnego](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) lokalizacji tooa **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-241">tooresolve this error, [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="7f9bb-242">Następnie należy dodać zmienną środowiskową hello **HADOOP_HOME**i ustaw wartość hello zmiennej hello zbyt**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-242">Then, add hello environment variable **HADOOP_HOME**, and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="7f9bb-243">Uruchamianie aplikacji Spark Scala lokalnej</span><span class="sxs-lookup"><span data-stu-id="7f9bb-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="7f9bb-244">Uruchom IntelliJ IDEA i tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="7f9bb-245">W hello **nowy projekt** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-245">In hello **New Project** dialog box, do hello following:</span></span>
   
    <span data-ttu-id="7f9bb-246">a.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-246">a.</span></span> <span data-ttu-id="7f9bb-247">Wybierz **HDInsight** > **Spark dla próbki uruchamiania lokalnego HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="7f9bb-248">b.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-248">b.</span></span> <span data-ttu-id="7f9bb-249">W hello **narzędzia kompilacji** listy, wybierz opcję powitania po, zgodnie z tooyour potrzeby:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-249">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="7f9bb-250">**Maven**, obsługę języka Scala Kreator tworzenia projektu</span><span class="sxs-lookup"><span data-stu-id="7f9bb-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="7f9bb-251">**SBT**, do zarządzania hello zależności i budowania hello Scala projektu</span><span class="sxs-lookup"><span data-stu-id="7f9bb-251">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![okno dialogowe Nowy projekt Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="7f9bb-253">Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="7f9bb-254">W następnym oknie hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-254">In hello next window, do hello following:</span></span>
   
    <span data-ttu-id="7f9bb-255">a.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-255">a.</span></span> <span data-ttu-id="7f9bb-256">Wprowadź nazwę projektu i lokalizację.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-256">Enter a project name and location.</span></span>

    <span data-ttu-id="7f9bb-257">b.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-257">b.</span></span> <span data-ttu-id="7f9bb-258">W hello **SDK projektu** listy rozwijanej wybierz wersję Java, która jest nowsza niż wersja 1.7.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-258">In hello **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="7f9bb-259">c.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-259">c.</span></span> <span data-ttu-id="7f9bb-260">W hello **wersji Spark** listy rozwijanej, wybierz hello wersję języka Scala, które mają toouse: Scala 2.11.x dla platformy Spark w wersji 2.0 lub Scala 2.10.x dla wersji 1.6 Spark.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-260">In hello **Spark Version** drop-down list, select hello version of Scala that you want toouse: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![okno dialogowe Nowy projekt Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="7f9bb-262">Wybierz pozycję **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="7f9bb-262">Select **Finish**.</span></span>

6. <span data-ttu-id="7f9bb-263">Przykładowy kod dodaje Hello szablonu (**LogQuery**) w obszarze hello **src** folderu, który można uruchomić lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-263">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![Lokalizacja LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="7f9bb-265">Kliknij prawym przyciskiem myszy hello **LogQuery** aplikacji, a następnie wybierz **Uruchom "LogQuery"**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-265">Right-click hello **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="7f9bb-266">Na powitania **Uruchom** karty u dołu hello, zobacz dane wyjściowe podobne hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-266">On hello **Run** tab at hello bottom, you see an output like hello following:</span></span>
   
   ![Aplikacji Spark lokalnego wynik uruchomienia](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a><span data-ttu-id="7f9bb-268">Konwertowanie istniejących IntelliJ IDEA toouse aplikacji Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7f9bb-268">Convert existing IntelliJ IDEA applications toouse Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="7f9bb-269">Możesz przekonwertować hello istniejących Spark Scala aplikacji utworzonych w toobe IntelliJ IDEA zgodne z zestawu narzędzi Azure for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-269">You can convert hello existing Spark Scala applications that you created in IntelliJ IDEA toobe compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="7f9bb-270">Następnie można użyć hello wtyczki toosubmit hello aplikacji tooan klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-270">You can then use hello plug-in toosubmit hello applications tooan HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="7f9bb-271">Dla istniejącej aplikacji Spark Scala, który został utworzony za pomocą IntelliJ IDEA Otwórz plik .iml skojarzone hello.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open hello associated .iml file.</span></span>

2. <span data-ttu-id="7f9bb-272">W katalogu głównym hello jest poziom **modułu** element podobnie następującej hello:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-272">At hello root level is a **module** element like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="7f9bb-273">Edytuj hello element tooadd `UniqueKey="HDInsightTool"` tak hello **modułu** element wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-273">Edit hello element tooadd `UniqueKey="HDInsightTool"` so that hello **module** element looks like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="7f9bb-274">Zapisz zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-274">Save hello changes.</span></span> <span data-ttu-id="7f9bb-275">Aplikacja teraz powinno być zgodne z narzędzi Azure dla IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="7f9bb-276">Można przetestować go, klikając prawym przyciskiem myszy nazwę projektu hello w obszarze Eksplorator projektów.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-276">You can test it by right-clicking hello project name in Project Explorer.</span></span> <span data-ttu-id="7f9bb-277">menu podręczne Hello ma teraz opcję hello **tooHDInsight przesyłanie aplikacji Spark**.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-277">hello pop-up menu now has hello option **Submit Spark Application tooHDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7f9bb-278">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="7f9bb-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="7f9bb-279">Błąd podczas uruchamiania lokalnego: *Użyj większego rozmiaru sterty*</span><span class="sxs-lookup"><span data-stu-id="7f9bb-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="7f9bb-280">W wersji 1.6 Spark Jeśli używasz SDK Java 32-bitowych podczas przebiegu lokalnego, może wystąpić hello następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter hello following errors:</span></span>

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

<span data-ttu-id="7f9bb-281">Te błędy się tak zdarzyć, ponieważ rozmiar stosu hello nie jest wystarczająco duży dla Spark toorun.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-281">These errors happen because hello heap size is not large enough for Spark toorun.</span></span> <span data-ttu-id="7f9bb-282">Platforma Spark wymaga co najmniej 471 MB.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="7f9bb-283">(Aby uzyskać więcej informacji, zobacz [SPARK 12081](https://issues.apache.org/jira/browse/SPARK-12081).) Jeden prostym rozwiązaniem jest toouse SDK Java 64-bitowych.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is toouse a 64-bit Java SDK.</span></span> <span data-ttu-id="7f9bb-284">Możesz również zmienić ustawienia maszyny JVM hello w IntelliJ przez dodanie hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="7f9bb-284">You can also change hello JVM settings in IntelliJ by adding hello following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Dodawanie toohello opcje "Opcje maszyny Wirtualnej" pole w IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="7f9bb-286">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="7f9bb-286">FAQ</span></span>
<span data-ttu-id="7f9bb-287">Wybierz toosubmit aplikacji tooAzure Data Lake Store, **Interactive** tryb podczas procesu hello Azure logowania.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-287">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="7f9bb-288">W przypadku wybrania **automatycznego** tryb, możesz uzyskać wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-288">If you select **Automated** mode, you can get an error.</span></span>

![interakcyjny rejestrowanie](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="7f9bb-290">Teraz możemy go rozwiązał.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-290">Now, we resolved it.</span></span> <span data-ttu-id="7f9bb-291">Możesz wybrać toosubmit Azure Data Lake klastra aplikacji przy użyciu dowolnej metody logowania.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-291">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="7f9bb-292">Opinie i znane problemy</span><span class="sxs-lookup"><span data-stu-id="7f9bb-292">Feedback and known issues</span></span>
<span data-ttu-id="7f9bb-293">Przeglądanie wyjść Spark bezpośrednio nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="7f9bb-294">Jeśli masz jakiekolwiek sugestie lub opinii lub jeśli wystąpią problemy, korzystając z tego dodatku, wiadomość e-mail na adres hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="7f9bb-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="7f9bb-295"><a name="seealso"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f9bb-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="7f9bb-296">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9bb-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="7f9bb-297">Demonstracja</span><span class="sxs-lookup"><span data-stu-id="7f9bb-297">Demo</span></span>
* <span data-ttu-id="7f9bb-298">Tworzenie projektu Scala (klip wideo): [tworzenie Spark Scala aplikacji](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="7f9bb-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="7f9bb-299">Debugowanie zdalne (klip wideo): [użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie w klastrze usługi HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="7f9bb-299">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="7f9bb-300">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="7f9bb-300">Scenarios</span></span>
* [<span data-ttu-id="7f9bb-301">Platforma Spark w usłudze BI: wykonaj interakcyjna analiza danych przy użyciu platformy Spark w usłudze HDInsight z narzędzi do analizy Biznesowej</span><span class="sxs-lookup"><span data-stu-id="7f9bb-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="7f9bb-302">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w HDInsight tooanalyze tworzenia temperatury użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="7f9bb-302">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="7f9bb-303">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9bb-303">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="7f9bb-304">Przesyłanie strumieniowe Spark: Korzystanie z platformy Spark w usłudze HDInsight toobuild w czasie rzeczywistym przesyłania strumieniowego aplikacji</span><span class="sxs-lookup"><span data-stu-id="7f9bb-304">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="7f9bb-305">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9bb-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="7f9bb-306">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="7f9bb-306">Creating and running applications</span></span>
* [<span data-ttu-id="7f9bb-307">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="7f9bb-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="7f9bb-308">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="7f9bb-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="7f9bb-309">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="7f9bb-309">Tools and extensions</span></span>
* [<span data-ttu-id="7f9bb-310">Użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie za pośrednictwem sieci VPN</span><span class="sxs-lookup"><span data-stu-id="7f9bb-310">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="7f9bb-311">Użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie za pośrednictwem SSH</span><span class="sxs-lookup"><span data-stu-id="7f9bb-311">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="7f9bb-312">Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="7f9bb-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="7f9bb-313">Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse toocreate Spark aplikacji</span><span class="sxs-lookup"><span data-stu-id="7f9bb-313">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="7f9bb-314">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9bb-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="7f9bb-315">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9bb-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="7f9bb-316">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="7f9bb-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="7f9bb-317">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9bb-317">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="7f9bb-318">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="7f9bb-318">Managing resources</span></span>
* [<span data-ttu-id="7f9bb-319">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9bb-319">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="7f9bb-320">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f9bb-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

