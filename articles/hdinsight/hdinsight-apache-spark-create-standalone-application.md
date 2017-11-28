---
title: aaaCreate Scala aplikacji toorun na klastry Spark - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Tworzenie aplikacji Spark napisanych w języku Scala z Apache Maven, jak hello kompilacji systemu i istniejące archetype Maven dla Scala podał IntelliJ IDEA."
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
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="78f1f-103">Utwórz toorun aplikacji Scala Maven w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="78f1f-103">Create a Scala Maven application toorun on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="78f1f-104">Dowiedz się, jak toocreate aplikacji Spark, napisanych w języku Scala za pomocą programu Maven z ROZWIĄZANIEM IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="78f1f-104">Learn how toocreate a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="78f1f-105">Artykuł Hello używa Apache Maven hello systemu do kompilacji i rozpoczyna się od istniejącej archetype Maven dla Scala podał IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="78f1f-105">hello article uses Apache Maven as hello build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="78f1f-106">Tworzenie aplikacji Scala w IntelliJ IDEA obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="78f1f-106">Creating a Scala application in IntelliJ IDEA involves hello following steps:</span></span>

* <span data-ttu-id="78f1f-107">Używanie programu Maven jako hello system kompilacji.</span><span class="sxs-lookup"><span data-stu-id="78f1f-107">Use Maven as hello build system.</span></span>
* <span data-ttu-id="78f1f-108">Aktualizowanie projektu Object Model (POM) pliku tooresolve Spark modułu zależności.</span><span class="sxs-lookup"><span data-stu-id="78f1f-108">Update Project Object Model (POM) file tooresolve Spark module dependencies.</span></span>
* <span data-ttu-id="78f1f-109">Pisanie aplikacji w języku Scala.</span><span class="sxs-lookup"><span data-stu-id="78f1f-109">Write your application in Scala.</span></span>
* <span data-ttu-id="78f1f-110">Wygeneruj plik jar, które mogą być przesłane tooHDInsight klastry Spark.</span><span class="sxs-lookup"><span data-stu-id="78f1f-110">Generate a jar file that can be submitted tooHDInsight Spark clusters.</span></span>
* <span data-ttu-id="78f1f-111">Uruchom aplikację hello w klastrze Spark przy użyciu programu Livy.</span><span class="sxs-lookup"><span data-stu-id="78f1f-111">Run hello application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="78f1f-112">Usługa HDInsight zapewnia również IntelliJ IDEA wtyczki narzędzia tooease hello proces tworzenia i przesyłanie aplikacji tooan klastra Spark w usłudze HDInsight w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="78f1f-112">HDInsight also provides an IntelliJ IDEA plugin tool tooease hello process of creating and submitting applications tooan HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="78f1f-113">Aby uzyskać więcej informacji, zobacz [Użyj HDInsight Tools Plugin for IntelliJ IDEA toocreate i przesyłanie aplikacji Spark](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="78f1f-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="78f1f-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="78f1f-114">Prerequisites</span></span>

* <span data-ttu-id="78f1f-115">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="78f1f-115">An Azure subscription.</span></span> <span data-ttu-id="78f1f-116">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="78f1f-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="78f1f-117">Klaster Apache Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78f1f-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="78f1f-118">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="78f1f-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="78f1f-119">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="78f1f-119">Oracle Java Development kit.</span></span> <span data-ttu-id="78f1f-120">Możesz zainstalować ją z [tutaj](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="78f1f-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="78f1f-121">Java IDE.</span><span class="sxs-lookup"><span data-stu-id="78f1f-121">A Java IDE.</span></span> <span data-ttu-id="78f1f-122">W tym artykule wykorzystano IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="78f1f-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="78f1f-123">Możesz zainstalować ją z [tutaj](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="78f1f-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="78f1f-124">Instalowanie wtyczki Scala for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="78f1f-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="78f1f-125">IntelliJ IDEA instalacji nie nie Monituj o włączenie wtyczki Scala, uruchom IntelliJ IDEA i przejść za pomocą hello następujące kroki tooinstall hello wtyczki:</span><span class="sxs-lookup"><span data-stu-id="78f1f-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through hello following steps tooinstall hello plugin:</span></span>

1. <span data-ttu-id="78f1f-126">Uruchom IntelliJ IDEA i na ekranie powitalnym kliknij **Konfiguruj** , a następnie kliknij przycisk **wtyczek**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Włączanie wtyczki scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="78f1f-128">Na następnym ekranie powitania kliknij **JetBrains zainstalować dodatek** z hello lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="78f1f-128">In hello next screen, click **Install JetBrains plugin** from hello lower left corner.</span></span> <span data-ttu-id="78f1f-129">W hello **Przeglądaj wtyczek JetBrains** okno dialogowe zostanie otwarte, wyszukaj Scala, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-129">In hello **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Instalowanie wtyczki scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="78f1f-131">Po zainstalowaniu dodatku hello pomyślnie, kliknij przycisk hello **przycisk Uruchom ponownie IntelliJ IDEA** toorestart hello IDE.</span><span class="sxs-lookup"><span data-stu-id="78f1f-131">After hello plugin installs successfully, click hello **Restart IntelliJ IDEA button** toorestart hello IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="78f1f-132">Tworzenie projektu Scala autonomiczny</span><span class="sxs-lookup"><span data-stu-id="78f1f-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="78f1f-133">Uruchom IntelliJ IDEA i Utwórz nowy projekt.</span><span class="sxs-lookup"><span data-stu-id="78f1f-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="78f1f-134">W powitalne okno dialogowe Nowy projekt, wprowadź hello następujące opcje, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-134">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>
   
    ![Utwórz projekt Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="78f1f-136">Wybierz **Maven** jako hello typu projektu.</span><span class="sxs-lookup"><span data-stu-id="78f1f-136">Select **Maven** as hello project type.</span></span>
   * <span data-ttu-id="78f1f-137">Określ **projekt zestawu SDK**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="78f1f-138">Kliknij przycisk Nowy i zwykle Przejdź katalogu instalacyjnego Java toohello `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="78f1f-138">Click New and navigate toohello Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="78f1f-139">Wybierz hello **Utwórz z archetype** opcji.</span><span class="sxs-lookup"><span data-stu-id="78f1f-139">Select hello **Create from archetype** option.</span></span>
   * <span data-ttu-id="78f1f-140">Wybierz z listy hello archetypes, **org.scala tools.archetypes:scala-archetype — prosty**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-140">From hello list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="78f1f-141">Spowoduje to utworzenie struktury katalogów prawo hello i pobrać wymagane hello domyślnego zależności toowrite Scala programu.</span><span class="sxs-lookup"><span data-stu-id="78f1f-141">This will create hello right directory structure and download hello required default dependencies toowrite Scala program.</span></span>
2. <span data-ttu-id="78f1f-142">Podaj odpowiednie wartości dla **GroupId**, **ArtifactId**, i **wersji**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="78f1f-143">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-143">Click **Next**.</span></span>
3. <span data-ttu-id="78f1f-144">W hello następne okno dialogowe, której określić katalog macierzysty Maven i inne ustawienia użytkownika, zaakceptuj ustawienia domyślne hello, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-144">In hello next dialog box, where you specify Maven home directory and other user settings, accept hello defaults and click **Next**.</span></span>
4. <span data-ttu-id="78f1f-145">W ostatniej okno dialogowe hello, określ nazwę projektu i lokalizację, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-145">In hello last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="78f1f-146">Usuń hello **MySpec.Scala** o plików **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-146">Delete hello **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="78f1f-147">Nie trzeba to dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="78f1f-147">You do not need this for hello application.</span></span>
6. <span data-ttu-id="78f1f-148">W razie potrzeby zmień nazwy plików źródła i test domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="78f1f-148">If required, rename hello default source and test files.</span></span> <span data-ttu-id="78f1f-149">W lewym okienku hello w hello IntelliJ IDEA, przejdź zbyt**src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-149">From hello left pane in hello IntelliJ IDEA, navigate too**src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="78f1f-150">Kliknij prawym przyciskiem myszy **App.scala**, kliknij przycisk **Refaktoryzuj**, kliknij przycisk Zmień nazwę pliku i okno dialogowe hello, podaj nazwę nowego hello aplikacji hello, a następnie kliknij przycisk **Refaktoryzuj**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in hello dialog box, provide hello new name for hello application and then click **Refactor**.</span></span>
   
    ![Zmień nazwy plików](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="78f1f-152">W kolejnych krokach hello spowoduje zaktualizowanie hello pom.xml toodefine hello zależności dla aplikacji Spark Scala hello.</span><span class="sxs-lookup"><span data-stu-id="78f1f-152">In hello subsequent steps, you will update hello pom.xml toodefine hello dependencies for hello Spark Scala application.</span></span> <span data-ttu-id="78f1f-153">Te zależności toobe pobrana i rozwiązany automatycznie, należy odpowiednio skonfigurować Maven.</span><span class="sxs-lookup"><span data-stu-id="78f1f-153">For those dependencies toobe downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Skonfigurować automatyczne pobieranie Maven](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="78f1f-155">Z hello **pliku** menu, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-155">From hello **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="78f1f-156">W hello **ustawienia** oknie dialogowym Wybierz zbyt**, wykonanie, wdrożenie kompilacji** > **Build Tools** > **Maven**  >  **Importowania**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-156">In hello **Settings** dialog box, navigate too**Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="78f1f-157">Wybierz opcję hello zbyt**Import Maven projektów automatycznie**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-157">Select hello option too**Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="78f1f-158">Kliknij przycisk **Zastosuj**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="78f1f-159">Zaktualizuj tooinclude plik źródłowy języka Scala hello kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="78f1f-159">Update hello Scala source file tooinclude your application code.</span></span> <span data-ttu-id="78f1f-160">Otwórz i Zastąp hello istniejących przykładowego kodu z hello następującego kodu i Zapisz zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="78f1f-160">Open and replace hello existing sample code with hello following code and save hello changes.</span></span> <span data-ttu-id="78f1f-161">Ten kod odczytuje dane hello z hello HVAC.csv (dostępne na wszystkich klastrach HDInsight Spark), pobiera hello wiersze z tylko jedną cyfrę w kolumnie szóstego hello i zapisuje dane wyjściowe hello zbyt**/HVACOut** obszarze hello domyślny magazyn kontener hello klastra.</span><span class="sxs-lookup"><span data-stu-id="78f1f-161">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello sixth column, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="78f1f-162">Zaktualizuj hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="78f1f-162">Update hello pom.xml.</span></span>
   
   1. <span data-ttu-id="78f1f-163">W ramach `<project>\<properties>` Dodaj hello:</span><span class="sxs-lookup"><span data-stu-id="78f1f-163">Within `<project>\<properties>` add hello following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="78f1f-164">W ramach `<project>\<dependencies>` Dodaj hello:</span><span class="sxs-lookup"><span data-stu-id="78f1f-164">Within `<project>\<dependencies>` add hello following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="78f1f-165">Zapisz zmiany toopom.xml.</span><span class="sxs-lookup"><span data-stu-id="78f1f-165">Save changes toopom.xml.</span></span>
10. <span data-ttu-id="78f1f-166">Utwórz plik JAR hello.</span><span class="sxs-lookup"><span data-stu-id="78f1f-166">Create hello .jar file.</span></span> <span data-ttu-id="78f1f-167">IntelliJ IDEA umożliwia tworzenie JAR jako artefaktu projektu.</span><span class="sxs-lookup"><span data-stu-id="78f1f-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="78f1f-168">Wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="78f1f-168">Perform hello following steps.</span></span>
    
    1. <span data-ttu-id="78f1f-169">Z hello **pliku** menu, kliknij przycisk **struktury projektu**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-169">From hello **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="78f1f-170">W hello **struktury projektu** okno dialogowe, kliknij przycisk **artefakty** a następnie kliknij przycisk hello oraz symboli.</span><span class="sxs-lookup"><span data-stu-id="78f1f-170">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="78f1f-171">Na powitania wyskakującym oknie dialogowym kliknij pozycję **JAR**, a następnie kliknij przycisk **z modułów z zależnościami**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-171">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="78f1f-173">W hello **utworzyć JAR z modułów** okna dialogowego, kliknij przycisk wielokropka hello (![wielokropka](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) przed hello **klasy głównym**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-173">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against hello **Main Class**.</span></span>
    4. <span data-ttu-id="78f1f-174">W hello **Wybierz klasy głównym** okno dialogowe, wybierz hello klasy, która jest wyświetlany domyślnie, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-174">In hello **Select Main Class** dialog box, select hello class that appears by default and then click **OK**.</span></span>
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="78f1f-176">W hello **utworzyć JAR z modułów** okna dialogowego polu należy upewnić się, ta opcja hello zbyt**wyodrębnić docelowy toohello JAR** jest zaznaczone, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-176">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="78f1f-177">Spowoduje to utworzenie jednego JAR z wszystkie zależności.</span><span class="sxs-lookup"><span data-stu-id="78f1f-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="78f1f-179">Hello dane wyjściowe układu karcie wyświetlane są wszystkie słoików hello, które są dołączane jako część hello projekt Maven.</span><span class="sxs-lookup"><span data-stu-id="78f1f-179">hello output layout tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="78f1f-180">Można wybrać i hello Usuń te, na którym hello Scala aplikacji nie ma żadnych zależności bezpośrednich.</span><span class="sxs-lookup"><span data-stu-id="78f1f-180">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="78f1f-181">Dla aplikacji hello jest tworzone w tym miejscu, należy usunąć wszystkie elementy oprócz hello ostatnią (**danych wyjściowych kompilacji SparkSimpleApp**).</span><span class="sxs-lookup"><span data-stu-id="78f1f-181">For hello application we are creating here, you can remove all but hello last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="78f1f-182">Wybierz toodelete słoików hello, a następnie kliknij przycisk hello **usunąć** ikony.</span><span class="sxs-lookup"><span data-stu-id="78f1f-182">Select hello jars toodelete and then click hello **Delete** icon.</span></span>
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="78f1f-184">Upewnij się, że **kompilacji w upewnij** pole jest zaznaczone, co zapewnia, że jar hello jest tworzony za każdym razem, gdy projekt hello jest utworzony lub zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="78f1f-184">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="78f1f-185">Kliknij przycisk **zastosować** , a następnie **OK**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="78f1f-186">Na pasku menu hello, kliknij przycisk **kompilacji**, a następnie kliknij przycisk **projektu należy**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-186">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="78f1f-187">Możesz również kliknąć **artefaktów kompilacji** toocreate hello jar.</span><span class="sxs-lookup"><span data-stu-id="78f1f-187">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="78f1f-188">Hello jar dane wyjściowe utworzony na podstawie **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="78f1f-188">hello output jar is created under **\out\artifacts**.</span></span>
       
        ![Utwórz JAR](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a><span data-ttu-id="78f1f-190">Uruchamianie aplikacji hello w klastrze Spark hello</span><span class="sxs-lookup"><span data-stu-id="78f1f-190">Run hello application on hello Spark cluster</span></span>
<span data-ttu-id="78f1f-191">Aplikacja hello toorun na powitania klastra, należy wykonać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="78f1f-191">toorun hello application on hello cluster, you must do hello following:</span></span>

* <span data-ttu-id="78f1f-192">**Kopiuj hello aplikacji jar toohello magazynu Azure blob** skojarzony z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="78f1f-192">**Copy hello application jar toohello Azure storage blob** associated with hello cluster.</span></span> <span data-ttu-id="78f1f-193">Można użyć [ **AzCopy**](../storage/common/storage-use-azcopy.md), więc toodo, narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="78f1f-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="78f1f-194">Istnieje wiele innych klientów również użyć tooupload danych.</span><span class="sxs-lookup"><span data-stu-id="78f1f-194">There are a lot of other clients as well that you can use tooupload data.</span></span> <span data-ttu-id="78f1f-195">Można znaleźć więcej informacji na temat je pod adresem [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="78f1f-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="78f1f-196">**Użyj toosubmit Livy zadanie aplikacji zdalnie** toohello klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="78f1f-196">**Use Livy toosubmit an application job remotely** toohello Spark cluster.</span></span> <span data-ttu-id="78f1f-197">Klastry Spark w usłudze HDInsight obejmuje Livy ujawniającym punkty końcowe REST, tooremotely przesyłania zadań Spark.</span><span class="sxs-lookup"><span data-stu-id="78f1f-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints tooremotely submit Spark jobs.</span></span> <span data-ttu-id="78f1f-198">Aby uzyskać więcej informacji, zobacz [zadania przesyłania Spark klastrów zdalnie przy użyciu programu Livy z platformy Spark w usłudze HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="78f1f-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="78f1f-199">Następny krok</span><span class="sxs-lookup"><span data-stu-id="78f1f-199">Next step</span></span>

<span data-ttu-id="78f1f-200">W niniejszym artykule możesz przedstawiono sposób toocreate Spark scala aplikacji.</span><span class="sxs-lookup"><span data-stu-id="78f1f-200">In this article you learned how toocreate a Spark scala application.</span></span> <span data-ttu-id="78f1f-201">ADVANCE toohello dalej artykułu toolearn jak toorun tej aplikacji na HDInsight Spark klastra przy użyciu programu Livy.</span><span class="sxs-lookup"><span data-stu-id="78f1f-201">Advance toohello next article toolearn how toorun this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="78f1f-202">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="78f1f-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

