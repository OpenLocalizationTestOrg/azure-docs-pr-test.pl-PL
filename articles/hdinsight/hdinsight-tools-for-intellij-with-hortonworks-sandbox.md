---
title: "zestaw narzędzi platformy Azure dla IntelliJ z piaskownicy Hortonworks aaaUse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse HDInsight narzędzi w zestawie narzędzi Azure for IntelliJ z Hortonworks piaskownicy."
keywords: "narzędzia hadoop hive zapytania, intellij, hortonworks piaskownicy, narzędzi platformy azure dla intellij"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="ccb3b-104">Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="ccb3b-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="ccb3b-105">Dowiedz się, jak hello toouse narzędzia HDInsight Tools for IntelliJ toodevelop Apache Scala aplikacji, a następnie testować aplikacje na [piaskownicy Hortonworks](http://hortonworks.com/products/sandbox/) uruchomione na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-105">Learn how toouse HDInsight Tools for IntelliJ toodevelop Apache Scala applications and then test hello applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="ccb3b-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) jest środowisko deweloperskie zintegrowane Java (IDE) do tworzenia oprogramowania komputera.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="ccb3b-107">Po opracowany i przetestowany aplikacji w piaskownicy Hortonworks można przenieść za[Azure HDInsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them too[Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccb3b-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ccb3b-108">Prerequisites</span></span>

<span data-ttu-id="ccb3b-109">Przed rozpoczęciem tego samouczka potrzebna będzie:</span><span class="sxs-lookup"><span data-stu-id="ccb3b-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="ccb3b-110">Hortonworks Data Platform (HDP) 2.4 dotyczącej piaskownicy Hortonworks uruchomione w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="ccb3b-111">Zobacz tooconfigure HDP, [wprowadzenie w ekosystemie Hadoop hello z piaskownicą Hadoop na maszynie wirtualnej](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-111">tooconfigure HDP, see [Get started in hello Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="ccb3b-112">Narzędzia HDInsight Tools for IntelliJ przetestowano tylko z HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="ccb3b-113">Rozwiń tooget HDP 2.4 **archiwum piaskownicy Hortonworks** na powitania [lokacji pobiera piaskownicy Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-113">tooget HDP 2.4, expand **Hortonworks Sandbox Archive** on hello [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="ccb3b-114">[Java Developer Kit (JDK) w wersji 1.8 lub nowszej](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="ccb3b-115">JDK jest wymagany przez hello Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-115">JDK is required by hello Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="ccb3b-116">[Wersja community IntelliJ IDEA](https://www.jetbrains.com/idea/download) z hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) wtyczki i hello [narzędzi Azure dla IntelliJ](../azure-toolkit-for-intellij.md) wtyczki.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="ccb3b-117">Narzędzia HDInsight Tools for IntelliJ jest dostępna jako część hello Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-117">HDInsight Tools for IntelliJ is available as a part of hello Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="ccb3b-118">Witaj tooinstall dodatków plug-in, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ccb3b-118">tooinstall hello plug-ins, do hello following:</span></span>

  1. <span data-ttu-id="ccb3b-119">Otwórz środowisko IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="ccb3b-120">Na powitania **-Zapraszamy** ekranu wybierz **Konfiguruj**, a następnie wybierz **wtyczek**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-120">On hello **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="ccb3b-121">Wybierz **JetBrains zainstalować dodatek** w hello lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-121">Select **Install JetBrains plugin** in hello lower-left corner.</span></span>
  4. <span data-ttu-id="ccb3b-122">Użyj hello wyszukiwania funkcji toosearch dla **Scala**, a następnie wybierz **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-122">Use hello search function toosearch for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="ccb3b-123">Wybierz **ponowne uruchomienie IntelliJ IDEA** toocomplete hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-123">Select **Restart IntelliJ IDEA** toocomplete hello installation.</span></span>
  6. <span data-ttu-id="ccb3b-124">Powtórz kroki 4 i 5 tooinstall hello **narzędzi Azure dla IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-124">Repeat step 4 and 5 tooinstall hello **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="ccb3b-125">Aby uzyskać więcej informacji, zobacz [hello instalacji narzędzi Azure dla IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-125">For more information, see [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="ccb3b-126">Tworzenie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="ccb3b-126">Create a Spark Scala application</span></span>

<span data-ttu-id="ccb3b-127">W tej sekcji utworzysz przykładowy projekt Scala przy użyciu IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="ccb3b-128">W następnej sekcji hello możesz połączyć toohello IntelliJ IDEA piaskownicy Hortonworks (emulatora) przed wysłaniem hello projektu.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-128">In hello next section, you link IntelliJ IDEA toohello Hortonworks Sandbox (emulator) before you submit hello project.</span></span>

1. <span data-ttu-id="ccb3b-129">Otwórz środowisko IntelliJ IDEA ze stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="ccb3b-130">W hello **nowy projekt** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ccb3b-130">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="ccb3b-131">a.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-131">a.</span></span> <span data-ttu-id="ccb3b-132">Wybierz **HDInsight** > **Spark w usłudze HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="ccb3b-133">b.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-133">b.</span></span> <span data-ttu-id="ccb3b-134">W hello **narzędzia kompilacji** listy, wybierz opcję powitania po, zgodnie z tooyour potrzeby:</span><span class="sxs-lookup"><span data-stu-id="ccb3b-134">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

    * <span data-ttu-id="ccb3b-135">**Maven**, obsługę języka Scala Kreator tworzenia projektu</span><span class="sxs-lookup"><span data-stu-id="ccb3b-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="ccb3b-136">**SBT**, do zarządzania hello zależności i budowania hello Scala projektu</span><span class="sxs-lookup"><span data-stu-id="ccb3b-136">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

   ![okno dialogowe Nowy projekt Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="ccb3b-138">Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-138">Select **Next**.</span></span>

3. <span data-ttu-id="ccb3b-139">W hello dalej **nowy projekt** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ccb3b-139">In hello next **New Project** dialog box, do hello following:</span></span>

    ![Utwórz IntelliJ Scala właściwości projektu](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="ccb3b-141">a.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-141">a.</span></span> <span data-ttu-id="ccb3b-142">W hello **Nazwa projektu** wprowadź nazwę projektu.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-142">In hello **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="ccb3b-143">b.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-143">b.</span></span> <span data-ttu-id="ccb3b-144">W hello **lokalizacja projektu** wprowadź lokalizację projektu.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-144">In hello **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="ccb3b-145">c.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-145">c.</span></span> <span data-ttu-id="ccb3b-146">Dalej toohello **projekt zestawu SDK** listy rozwijanej wybierz **nowy**, wybierz pozycję **JDK**, a następnie określ folder hello JDK Java w wersji 1,7 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-146">Next toohello **Project SDK** drop-down list, select **New**, select **JDK**, and then specify hello folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="ccb3b-147">Wybierz **Java 1.8** dla klastra 2.x Spark hello, lub wybierz **Java 1.7** hello Spark 1.x klastra.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-147">Select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span> <span data-ttu-id="ccb3b-148">Witaj domyślna lokalizacja to C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-148">hello default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="ccb3b-149">d.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-149">d.</span></span> <span data-ttu-id="ccb3b-150">W hello **wersji Spark** listy rozwijanej, Kreator tworzenia projektu Scala integruje hello poprawnej wersji dla platformy Spark zestawy SDK i Scala.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-150">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="ccb3b-151">Jeśli hello klastra Spark w wersji starszej niż 2.0, wybierz **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-151">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="ccb3b-152">W przeciwnym razie wybierz **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="ccb3b-153">W tym przykładzie użyto Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="ccb3b-154">Upewnij się, że używasz repozytorium hello oznaczone Scala 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-154">Make sure that you are using hello repository marked Scala 2.10.x.</span></span> <span data-ttu-id="ccb3b-155">Nie używaj repozytorium hello oznaczone Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-155">Do not use hello repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="ccb3b-156">Wybierz pozycję **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-156">Select **Finish**.</span></span>

5. <span data-ttu-id="ccb3b-157">Jeśli hello **projektu** widoku nie jest jeszcze otwarty, naciśnij klawisz **Alt + 1** tooopen go.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-157">If hello **Project** view is not already open, press **Alt+1** tooopen it.</span></span>

6. <span data-ttu-id="ccb3b-158">W **Eksplorator projektów**, rozwiń hello projektu, a następnie wybierz **src**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-158">In **Project Explorer**, expand hello project, and then select **src**.</span></span>

7. <span data-ttu-id="ccb3b-159">Kliknij prawym przyciskiem myszy **src**, punktu zbyt**nowy**, a następnie wybierz **klasy Scala**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-159">Right-click **src**, point too**New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="ccb3b-160">W hello **nazwa** wprowadź nazwę, w hello **rodzaj** wybierz opcję **obiektu**, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-160">In hello **Name** box, enter a name, in hello **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![okno Utwórz nową klasę Scala Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="ccb3b-162">W pliku .scala hello Wklej hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="ccb3b-162">In hello .scala file, paste hello following code:</span></span>

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. <span data-ttu-id="ccb3b-163">Na powitania **kompilacji** menu, wybierz opcję **kompilacji projektu**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-163">On hello **Build** menu, select **Build project**.</span></span> <span data-ttu-id="ccb3b-164">Upewnij się, że hello Kompilacja została pomyślnie ukończona.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-164">Make sure that hello compilation has been completed successfully.</span></span>


## <a name="link-toohello-hortonworks-sandbox"></a><span data-ttu-id="ccb3b-165">Łącze toohello Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="ccb3b-165">Link toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="ccb3b-166">Przed połączeniem tooa piaskownicy Hortonworks (emulatora), musi korzystać z istniejących aplikacji IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-166">Before you can link tooa Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="ccb3b-167">toolink tooan emulator, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ccb3b-167">toolink tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="ccb3b-168">Witaj Otwórz projekt w IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-168">Open hello project in IntelliJ.</span></span>

2. <span data-ttu-id="ccb3b-169">Na powitania **widoku** menu, wybierz opcję **narzędzi systemu Windows**, a następnie wybierz **Eksploratora Azure**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-169">On hello **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="ccb3b-170">Rozwiń węzeł **Azure**, kliknij prawym przyciskiem myszy **HDInsight**, a następnie wybierz **Link Emulator**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="ccb3b-171">W hello **emulatora nowe łącze A** okna, wprowadź hasło hello skonfigurowano dla konta głównego hello hello Hortonworks piaskownicy, wprowadź wartości podobnie toothose w hello następującego zrzutu ekranu, a następnie wybierz **OK** .</span><span class="sxs-lookup"><span data-stu-id="ccb3b-171">In hello **Link A New Emulator** window, enter hello password that you've configured for hello root account of hello Hortonworks Sandbox, enter values similar toothose in hello following screenshot, and then select **OK**.</span></span> 

   ![okno "Łącze Nowy Emulator" Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="ccb3b-173">emulator hello tooconfigure, wybierz opcję **tak**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-173">tooconfigure hello emulator, select **Yes**.</span></span>

<span data-ttu-id="ccb3b-174">Jeśli hello emulator jest połączony pomyślnie, hello emulatora (Hortonworks piaskownicy) jest wyświetlane w węźle HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-174">When hello emulator is connected successfully, hello emulator (Hortonworks Sandbox) is listed in hello HDInsight node.</span></span>

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a><span data-ttu-id="ccb3b-175">Przedstawia toohello aplikacji Spark Scala hello Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="ccb3b-175">Submit hello Spark Scala application toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="ccb3b-176">Po połączeniu IntelliJ IDEA toohello emulatora, możesz przesłać projektu.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-176">After you have linked IntelliJ IDEA toohello emulator, you can submit your project.</span></span>

<span data-ttu-id="ccb3b-177">toosubmit emulatora tooan projektu hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ccb3b-177">toosubmit a project tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="ccb3b-178">W **Eksplorator projektów**, kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **tooHDInsight aplikacji Spark przesłać**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-178">In **Project Explorer**, right-click hello project, and then select **Submit Spark application tooHDInsight**.</span></span>

2. <span data-ttu-id="ccb3b-179">Witaj, po:</span><span class="sxs-lookup"><span data-stu-id="ccb3b-179">Do hello following:</span></span>

    <span data-ttu-id="ccb3b-180">a.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-180">a.</span></span> <span data-ttu-id="ccb3b-181">W hello **klastra Spark (tylko w systemie Linux)** listy rozwijanej wybierz użytkownika lokalnego Hortonworks piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-181">In hello **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="ccb3b-182">b.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-182">b.</span></span> <span data-ttu-id="ccb3b-183">W hello **Nazwa klasy głównym** polu, wybierz lub wprowadź nazwę klasy głównym hello.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-183">In hello **Main class name** box, choose or enter hello main class name.</span></span> <span data-ttu-id="ccb3b-184">W tym samouczku, nazwa hello jest **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-184">For this tutorial, hello name is **GroupByTest**.</span></span>

3. <span data-ttu-id="ccb3b-185">Wybierz **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-185">Select **Submit**.</span></span> <span data-ttu-id="ccb3b-186">Dzienniki przesyłania zadania Hello są wyświetlane w okna narzędzia przesyłanie Spark hello.</span><span class="sxs-lookup"><span data-stu-id="ccb3b-186">hello job submission logs are shown in hello Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccb3b-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ccb3b-187">Next steps</span></span>

- <span data-ttu-id="ccb3b-188">toolearn jak toocreate aplikacji Spark dla usługi HDInsight przy użyciu narzędzia HDInsight Tools for IntelliJ, przejdź zbyt[użycia narzędzi HDInsight w zestawie narzędzi Azure dla aplikacji Spark toocreate IntelliJ dla klastra usługi HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-188">toolearn how toocreate Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="ccb3b-189">toowatch wideo narzędzia HDInsight Tools for IntelliJ, przejdź zbyt[wprowadzenie narzędzi HDInsight Tools for IntelliJ rozwoju Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-189">toowatch a video of HDInsight Tools for IntelliJ, go too[Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="ccb3b-190">toolearn jak toodebug aplikacji Spark przy użyciu hello toolkit zdalnie w usłudze HDInsight za pośrednictwem protokołu SSH, zbyt Przejdź[zdalne debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem protokołu SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-190">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through SSH, go too[Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="ccb3b-191">toolearn jak toodebug aplikacji Spark przy użyciu hello toolkit zdalnie w usłudze HDInsight za pośrednictwem sieci VPN, zbyt Przejdź[użycia narzędzi HDInsight w zestawie narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie w klastrze HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-191">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through VPN, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="ccb3b-192">jak toouse narzędzi HDInsight Tools dla programu Eclipse toocreate aplikacji Spark, przejdź zbyt toolearn[użycia narzędzi HDInsight w zestawie narzędzi Azure dla programu Eclipse toocreate Spark aplikacji](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-192">toolearn how toouse HDInsight Tools for Eclipse toocreate a Spark application, go too[Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="ccb3b-193">toowatch wideo narzędzi HDInsight Tools dla programu Eclipse, przejdź zbyt[Użyj narzędzia HDInsight dla aplikacji Spark toocreate Eclipse](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="ccb3b-193">toowatch a video of HDInsight Tools for Eclipse, go too[Use HDInsight Tool for Eclipse toocreate Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
