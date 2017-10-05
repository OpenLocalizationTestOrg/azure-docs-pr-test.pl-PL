---
title: Tworzenie aplikacji Scala do uruchamiania na klastry Spark - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Tworzenie aplikacji Spark napisane w języku Scala z Apache Maven jako system kompilacji i istniejące archetype Maven dla Scala podał IntelliJ IDEA."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 95dba08744357f8800b05e3d4b892e3a363d5985
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-scala-maven-application-to-run-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="7aff9-103">Tworzenie aplikacji Scala Maven, aby uruchomić w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7aff9-103">Create a Scala Maven application to run on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="7aff9-104">Informacje o sposobie tworzenia aplikacji Spark napisanych w języku Scala za pomocą programu Maven z ROZWIĄZANIEM IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7aff9-104">Learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="7aff9-105">Artykuł używa Apache Maven jako system kompilacji i rozpoczyna się od istniejącej archetype Maven dla Scala podał IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7aff9-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="7aff9-106">Tworzenie aplikacji Scala w IntelliJ IDEA obejmuje następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7aff9-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span></span>

* <span data-ttu-id="7aff9-107">Używanie programu Maven jako system kompilacji.</span><span class="sxs-lookup"><span data-stu-id="7aff9-107">Use Maven as the build system.</span></span>
* <span data-ttu-id="7aff9-108">Zaktualizuj plik projektu Object Model (POM) można rozpoznać zależności modułu Spark.</span><span class="sxs-lookup"><span data-stu-id="7aff9-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span></span>
* <span data-ttu-id="7aff9-109">Pisanie aplikacji w języku Scala.</span><span class="sxs-lookup"><span data-stu-id="7aff9-109">Write your application in Scala.</span></span>
* <span data-ttu-id="7aff9-110">Generuj plik jar, który może być przesyłany do klastrów HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="7aff9-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span></span>
* <span data-ttu-id="7aff9-111">Uruchom aplikację w klastrze Spark przy użyciu programu Livy.</span><span class="sxs-lookup"><span data-stu-id="7aff9-111">Run the application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="7aff9-112">Usługa HDInsight zapewnia również narzędzie wtyczkę IntelliJ IDEA do jej obsługi ułatwiają proces tworzenia i przesyłanie aplikacji do klastra Spark w usłudze HDInsight w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="7aff9-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="7aff9-113">Aby uzyskać więcej informacji, zobacz [Użyj HDInsight Tools Plugin for IntelliJ IDEA tworzenie i przesyłanie aplikacji Spark](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="7aff9-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7aff9-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7aff9-114">Prerequisites</span></span>

* <span data-ttu-id="7aff9-115">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7aff9-115">An Azure subscription.</span></span> <span data-ttu-id="7aff9-116">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7aff9-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7aff9-117">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7aff9-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="7aff9-118">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="7aff9-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="7aff9-119">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="7aff9-119">Oracle Java Development kit.</span></span> <span data-ttu-id="7aff9-120">Możesz zainstalować ją z [tutaj](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="7aff9-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="7aff9-121">Java IDE.</span><span class="sxs-lookup"><span data-stu-id="7aff9-121">A Java IDE.</span></span> <span data-ttu-id="7aff9-122">W tym artykule wykorzystano IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="7aff9-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="7aff9-123">Możesz zainstalować ją z [tutaj](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="7aff9-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="7aff9-124">Instalowanie wtyczki Scala for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="7aff9-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="7aff9-125">Jeśli instalacja IntelliJ IDEA nie Monituj o włączenie wtyczki Scala, uruchom IntelliJ IDEA i kolejnych kroków, aby zainstalować dodatek plug-in:</span><span class="sxs-lookup"><span data-stu-id="7aff9-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through the following steps to install the plugin:</span></span>

1. <span data-ttu-id="7aff9-126">Uruchom IntelliJ IDEA i na ekranie powitalnym kliknij **Konfiguruj** , a następnie kliknij przycisk **wtyczek**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Włączanie wtyczki scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="7aff9-128">Na następnym ekranie kliknij **JetBrains zainstalować dodatek** z lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="7aff9-128">In the next screen, click **Install JetBrains plugin** from the lower left corner.</span></span> <span data-ttu-id="7aff9-129">W **Przeglądaj wtyczek JetBrains** okno dialogowe zostanie otwarte, wyszukaj Scala, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-129">In the **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Instalowanie wtyczki scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="7aff9-131">Po zainstalowaniu dodatku plug-in pomyślnie, kliknij przycisk **przycisk Uruchom ponownie IntelliJ IDEA** ponowne uruchomienie IDE.</span><span class="sxs-lookup"><span data-stu-id="7aff9-131">After the plugin installs successfully, click the **Restart IntelliJ IDEA button** to restart the IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="7aff9-132">Tworzenie projektu Scala autonomiczny</span><span class="sxs-lookup"><span data-stu-id="7aff9-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="7aff9-133">Uruchom IntelliJ IDEA i Utwórz nowy projekt.</span><span class="sxs-lookup"><span data-stu-id="7aff9-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="7aff9-134">W oknie dialogowym projektu nowe wybierz następujące opcje, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-134">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Utwórz projekt Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="7aff9-136">Wybierz **Maven** jako typ projektu.</span><span class="sxs-lookup"><span data-stu-id="7aff9-136">Select **Maven** as the project type.</span></span>
   * <span data-ttu-id="7aff9-137">Określ **projekt zestawu SDK**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="7aff9-138">Kliknij przycisk Nowy i przejdź do katalogu instalacyjnego programu Java zwykle `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="7aff9-138">Click New and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="7aff9-139">Wybierz **Utwórz z archetype** opcji.</span><span class="sxs-lookup"><span data-stu-id="7aff9-139">Select the **Create from archetype** option.</span></span>
   * <span data-ttu-id="7aff9-140">Wybierz z listy archetypes **org.scala tools.archetypes:scala-archetype — prosty**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-140">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="7aff9-141">Spowoduje to utworzenie struktury katalogów prawo i pobrać zależności wymagane domyślne można zapisać Scala program.</span><span class="sxs-lookup"><span data-stu-id="7aff9-141">This will create the right directory structure and download the required default dependencies to write Scala program.</span></span>
2. <span data-ttu-id="7aff9-142">Podaj odpowiednie wartości dla **GroupId**, **ArtifactId**, i **wersji**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="7aff9-143">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-143">Click **Next**.</span></span>
3. <span data-ttu-id="7aff9-144">W oknie dialogowym dalej, której określić katalog macierzysty Maven i inne ustawienia użytkownika, zaakceptuj ustawienia domyślne, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-144">In the next dialog box, where you specify Maven home directory and other user settings, accept the defaults and click **Next**.</span></span>
4. <span data-ttu-id="7aff9-145">W oknie dialogowym ostatnich, określ nazwę projektu i lokalizację, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-145">In the last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="7aff9-146">Usuń **MySpec.Scala** o plików **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-146">Delete the **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="7aff9-147">Nie trzeba to dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7aff9-147">You do not need this for the application.</span></span>
6. <span data-ttu-id="7aff9-148">W razie potrzeby zmień nazwę domyślnych plików źródła i testowania.</span><span class="sxs-lookup"><span data-stu-id="7aff9-148">If required, rename the default source and test files.</span></span> <span data-ttu-id="7aff9-149">W lewym okienku w IntelliJ IDEA, przejdź do **src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-149">From the left pane in the IntelliJ IDEA, navigate to **src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="7aff9-150">Kliknij prawym przyciskiem myszy **App.scala**, kliknij przycisk **Refaktoryzuj**, kliknij przycisk Zmień nazwę pliku, a w oknie dialogowym podaj nową nazwę dla aplikacji, a następnie kliknij przycisk **Refaktoryzuj**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in the dialog box, provide the new name for the application and then click **Refactor**.</span></span>
   
    ![Zmień nazwy plików](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="7aff9-152">W kolejnych krokach spowoduje zaktualizowanie pom.xml do Definiowanie zależności dla aplikacji Spark Scala.</span><span class="sxs-lookup"><span data-stu-id="7aff9-152">In the subsequent steps, you will update the pom.xml to define the dependencies for the Spark Scala application.</span></span> <span data-ttu-id="7aff9-153">Te zależności do pobrania i rozwiązany automatycznie należy odpowiednio skonfigurować Maven.</span><span class="sxs-lookup"><span data-stu-id="7aff9-153">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Skonfigurować automatyczne pobieranie Maven](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="7aff9-155">Z **pliku** menu, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-155">From the **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="7aff9-156">W **ustawienia** okna dialogowego wybierz opcję **, wykonanie, wdrożenie kompilacji** > **Build Tools** > **Maven** > **importowanie**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-156">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="7aff9-157">Wybierz opcję **Import Maven projektów automatycznie**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-157">Select the option to **Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="7aff9-158">Kliknij przycisk **Zastosuj**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="7aff9-159">Zaktualizuj Scala pliku źródłowego, aby uwzględnić kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7aff9-159">Update the Scala source file to include your application code.</span></span> <span data-ttu-id="7aff9-160">Otwórz i Zastąp istniejące przykładowy kod następujący kod i Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="7aff9-160">Open and replace the existing sample code with the following code and save the changes.</span></span> <span data-ttu-id="7aff9-161">Ten kod odczytuje dane z HVAC.csv (dostępne na wszystkich klastrach HDInsight Spark), pobiera wiersze z tylko jedną cyfrę w kolumnie szóstego i zapisuje dane wyjściowe do **/HVACOut** w obszarze domyślnego kontenera magazynu dla klastra.</span><span class="sxs-lookup"><span data-stu-id="7aff9-161">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO to wasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows which have only one digit in the 7th column in the CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="7aff9-162">Zaktualizuj pom.xml.</span><span class="sxs-lookup"><span data-stu-id="7aff9-162">Update the pom.xml.</span></span>
   
   1. <span data-ttu-id="7aff9-163">W ramach `<project>\<properties>` Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="7aff9-163">Within `<project>\<properties>` add the following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="7aff9-164">W ramach `<project>\<dependencies>` Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="7aff9-164">Within `<project>\<dependencies>` add the following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="7aff9-165">Zapisz zmiany w pom.xml.</span><span class="sxs-lookup"><span data-stu-id="7aff9-165">Save changes to pom.xml.</span></span>
10. <span data-ttu-id="7aff9-166">Utwórz plik JAR.</span><span class="sxs-lookup"><span data-stu-id="7aff9-166">Create the .jar file.</span></span> <span data-ttu-id="7aff9-167">IntelliJ IDEA umożliwia tworzenie JAR jako artefaktu projektu.</span><span class="sxs-lookup"><span data-stu-id="7aff9-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="7aff9-168">Wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="7aff9-168">Perform the following steps.</span></span>
    
    1. <span data-ttu-id="7aff9-169">Z **pliku** menu, kliknij przycisk **struktury projektu**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-169">From the **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="7aff9-170">W **struktury projektu** okno dialogowe, kliknij przycisk **artefakty** , a następnie kliknij znak plus.</span><span class="sxs-lookup"><span data-stu-id="7aff9-170">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="7aff9-171">W wyświetlonym oknie dialogowym, kliknij polecenie **JAR**, a następnie kliknij przycisk **z modułów z zależnościami**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-171">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="7aff9-173">W **utworzyć JAR z modułów** okna dialogowego, kliknij przycisk wielokropka (![wielokropka](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) przed **klasy głównym**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-173">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against the **Main Class**.</span></span>
    4. <span data-ttu-id="7aff9-174">W **Wybierz klasy głównym** okno dialogowe, wybierz klasę, która jest wyświetlany domyślnie, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-174">In the **Select Main Class** dialog box, select the class that appears by default and then click **OK**.</span></span>
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="7aff9-176">W **utworzyć JAR z modułów** okna dialogowego upewnij się, że opcja **Wyodrębnij do docelowego JAR** jest zaznaczone, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-176">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="7aff9-177">Spowoduje to utworzenie jednego JAR z wszystkie zależności.</span><span class="sxs-lookup"><span data-stu-id="7aff9-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="7aff9-179">Karta Układ danych wyjściowych zawiera listę wszystkich słoików, które są częścią projektu Maven.</span><span class="sxs-lookup"><span data-stu-id="7aff9-179">The output layout tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="7aff9-180">Można wybrać i usunąć te, na którym aplikacja Scala nie ma żadnych zależności bezpośrednich.</span><span class="sxs-lookup"><span data-stu-id="7aff9-180">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="7aff9-181">Dla aplikacji jest tworzone w tym miejscu, należy usunąć wszystkie oprócz ostatnią (**danych wyjściowych kompilacji SparkSimpleApp**).</span><span class="sxs-lookup"><span data-stu-id="7aff9-181">For the application we are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="7aff9-182">Wybierz słoików usunąć, a następnie kliknij przycisk **usunąć** ikony.</span><span class="sxs-lookup"><span data-stu-id="7aff9-182">Select the jars to delete and then click the **Delete** icon.</span></span>
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="7aff9-184">Upewnij się, że **kompilacji w upewnij** pole jest zaznaczone, co zapewnia, że jar jest tworzony za każdym razem, gdy projekt jest utworzony lub zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="7aff9-184">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="7aff9-185">Kliknij przycisk **zastosować** , a następnie **OK**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="7aff9-186">Na pasku menu kliknij **kompilacji**, a następnie kliknij przycisk **projektu należy**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-186">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="7aff9-187">Możesz również kliknąć **artefaktów kompilacji** utworzyć jar.</span><span class="sxs-lookup"><span data-stu-id="7aff9-187">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="7aff9-188">Dane wyjściowe jar utworzony na podstawie **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="7aff9-188">The output jar is created under **\out\artifacts**.</span></span>
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-the-application-on-the-spark-cluster"></a><span data-ttu-id="7aff9-190">Uruchom aplikację w klastrze Spark</span><span class="sxs-lookup"><span data-stu-id="7aff9-190">Run the application on the Spark cluster</span></span>
<span data-ttu-id="7aff9-191">Aby uruchomić aplikację w klastrze, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7aff9-191">To run the application on the cluster, you must do the following:</span></span>

* <span data-ttu-id="7aff9-192">**Skopiuj jar aplikacji do obiektu blob magazynu Azure** skojarzony z klastrem.</span><span class="sxs-lookup"><span data-stu-id="7aff9-192">**Copy the application jar to the Azure storage blob** associated with the cluster.</span></span> <span data-ttu-id="7aff9-193">Można użyć [ **AzCopy**](../storage/common/storage-use-azcopy.md), narzędzie wiersza polecenia, aby to zrobić.</span><span class="sxs-lookup"><span data-stu-id="7aff9-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="7aff9-194">Istnieje wiele innych klientów, jak również służy do przekazywania danych.</span><span class="sxs-lookup"><span data-stu-id="7aff9-194">There are a lot of other clients as well that you can use to upload data.</span></span> <span data-ttu-id="7aff9-195">Można znaleźć więcej informacji na temat je pod adresem [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="7aff9-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="7aff9-196">**Użyj programu Livy można przesłać zadania aplikacji zdalnie** do klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="7aff9-196">**Use Livy to submit an application job remotely** to the Spark cluster.</span></span> <span data-ttu-id="7aff9-197">Klastry Spark w usłudze HDInsight obejmuje Livy ujawniającym punkty końcowe REST do zdalnego przesyłania zadań Spark.</span><span class="sxs-lookup"><span data-stu-id="7aff9-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span></span> <span data-ttu-id="7aff9-198">Aby uzyskać więcej informacji, zobacz [zadania przesyłania Spark klastrów zdalnie przy użyciu programu Livy z platformy Spark w usłudze HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="7aff9-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="7aff9-199">Następny krok</span><span class="sxs-lookup"><span data-stu-id="7aff9-199">Next step</span></span>

<span data-ttu-id="7aff9-200">W tym artykule przedstawiono sposób tworzenia aplikacji Spark scala.</span><span class="sxs-lookup"><span data-stu-id="7aff9-200">In this article you learned how to create a Spark scala application.</span></span> <span data-ttu-id="7aff9-201">Przejdź do następnego artykuł, aby dowiedzieć się, jak uruchomić tę aplikację w klastrze Spark w usłudze HDInsight przy użyciu programu Livy.</span><span class="sxs-lookup"><span data-stu-id="7aff9-201">Advance to the next article to learn how to run this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="7aff9-202">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="7aff9-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

