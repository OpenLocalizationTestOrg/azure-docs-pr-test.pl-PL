---
title: "Użyj narzędzi Azure for IntelliJ z piaskownicy Hortonworks | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak za pomocą narzędzi HDInsight w zestawie narzędzi Azure for IntelliJ z Hortonworks piaskownicy."
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
ms.openlocfilehash: c49f185db5a035f70a711bf309b973182d94a2b0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="7e935-104">Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="7e935-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="7e935-105">Dowiedz się, jak narzędzia HDInsight Tools for IntelliJ umożliwia tworzenie aplikacji Apache Scala i przetestowanie aplikacji na [piaskownicy Hortonworks](http://hortonworks.com/products/sandbox/) uruchomione na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="7e935-105">Learn how to use HDInsight Tools for IntelliJ to develop Apache Scala applications and then test the applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="7e935-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) jest środowisko deweloperskie zintegrowane Java (IDE) do tworzenia oprogramowania komputera.</span><span class="sxs-lookup"><span data-stu-id="7e935-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="7e935-107">Po opracowany i przetestowany aplikacji w piaskownicy Hortonworks można przenieść je do [Azure HDInsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e935-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them to [Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e935-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7e935-108">Prerequisites</span></span>

<span data-ttu-id="7e935-109">Przed rozpoczęciem tego samouczka potrzebna będzie:</span><span class="sxs-lookup"><span data-stu-id="7e935-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="7e935-110">Hortonworks Data Platform (HDP) 2.4 dotyczącej piaskownicy Hortonworks uruchomione w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="7e935-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="7e935-111">Aby skonfigurować HDP, zobacz [wprowadzenie w ekosystemie Hadoop z piaskownicą Hadoop na maszynie wirtualnej](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7e935-111">To configure HDP, see [Get started in the Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="7e935-112">Narzędzia HDInsight Tools for IntelliJ przetestowano tylko z HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="7e935-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="7e935-113">Aby uzyskać HDP 2.4, rozwiń węzeł **Hortonworks piaskownicy archiwum** na [lokacji pobiera piaskownicy Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="7e935-113">To get HDP 2.4, expand **Hortonworks Sandbox Archive** on the [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="7e935-114">[Java Developer Kit (JDK) w wersji 1.8 lub nowszej](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="7e935-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="7e935-115">JDK jest wymagane przez zestaw narzędzi Azure for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7e935-115">JDK is required by the Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="7e935-116">[Wersja community IntelliJ IDEA](https://www.jetbrains.com/idea/download) z [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) wtyczki i [narzędzi Azure dla IntelliJ](../azure-toolkit-for-intellij.md) wtyczki.</span><span class="sxs-lookup"><span data-stu-id="7e935-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with the [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and the [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="7e935-117">Narzędzia HDInsight Tools for IntelliJ jest dostępna jako część zestawu narzędzi platformy Azure dla IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7e935-117">HDInsight Tools for IntelliJ is available as a part of the Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="7e935-118">Aby zainstalować dodatki plug-in, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7e935-118">To install the plug-ins, do the following:</span></span>

  1. <span data-ttu-id="7e935-119">Otwórz środowisko IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7e935-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="7e935-120">Na **-Zapraszamy** ekranu wybierz **Konfiguruj**, a następnie wybierz **wtyczek**.</span><span class="sxs-lookup"><span data-stu-id="7e935-120">On the **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="7e935-121">Wybierz **JetBrains zainstalować dodatek** w lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="7e935-121">Select **Install JetBrains plugin** in the lower-left corner.</span></span>
  4. <span data-ttu-id="7e935-122">Użyj funkcji wyszukiwania w celu wyszukania **Scala**, a następnie wybierz **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="7e935-122">Use the search function to search for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="7e935-123">Wybierz **ponowne uruchomienie IntelliJ IDEA** do ukończenia instalacji.</span><span class="sxs-lookup"><span data-stu-id="7e935-123">Select **Restart IntelliJ IDEA** to complete the installation.</span></span>
  6. <span data-ttu-id="7e935-124">Powtórz kroki 4 i 5, aby zainstalować **narzędzi Azure dla IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="7e935-124">Repeat step 4 and 5 to install the **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="7e935-125">Aby uzyskać więcej informacji, zobacz [zainstalować zestaw narzędzi platformy Azure dla IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="7e935-125">For more information, see [Install the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="7e935-126">Tworzenie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="7e935-126">Create a Spark Scala application</span></span>

<span data-ttu-id="7e935-127">W tej sekcji utworzysz przykładowy projekt Scala przy użyciu IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="7e935-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="7e935-128">W następnej sekcji możesz połączyć IntelliJ IDEA piaskownicy Hortonworks (emulatora), przed przesłaniem projektu.</span><span class="sxs-lookup"><span data-stu-id="7e935-128">In the next section, you link IntelliJ IDEA to the Hortonworks Sandbox (emulator) before you submit the project.</span></span>

1. <span data-ttu-id="7e935-129">Otwórz środowisko IntelliJ IDEA ze stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="7e935-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="7e935-130">W **nowy projekt** okno dialogowe, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7e935-130">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="7e935-131">a.</span><span class="sxs-lookup"><span data-stu-id="7e935-131">a.</span></span> <span data-ttu-id="7e935-132">Wybierz **HDInsight** > **Spark w usłudze HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="7e935-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="7e935-133">b.</span><span class="sxs-lookup"><span data-stu-id="7e935-133">b.</span></span> <span data-ttu-id="7e935-134">W **narzędzia kompilacji** listy, wybierz jedną z następujących czynności, w zależności od potrzeb:</span><span class="sxs-lookup"><span data-stu-id="7e935-134">In the **Build tool** list, select either of the following, according to your need:</span></span>

    * <span data-ttu-id="7e935-135">**Maven**, obsługę języka Scala Kreator tworzenia projektu</span><span class="sxs-lookup"><span data-stu-id="7e935-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="7e935-136">**SBT**, do zarządzania zależności i budowania projektu języka Scala</span><span class="sxs-lookup"><span data-stu-id="7e935-136">**SBT**, for managing the dependencies and building for the Scala project</span></span>

   ![Okno dialogowe nowego projektu](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="7e935-138">Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7e935-138">Select **Next**.</span></span>

3. <span data-ttu-id="7e935-139">W następnej **nowy projekt** okna dialogowego pole, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7e935-139">In the next **New Project** dialog box, do the following:</span></span>

    ![Utwórz IntelliJ Scala właściwości projektu](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="7e935-141">a.</span><span class="sxs-lookup"><span data-stu-id="7e935-141">a.</span></span> <span data-ttu-id="7e935-142">W **Nazwa projektu** wprowadź nazwę projektu.</span><span class="sxs-lookup"><span data-stu-id="7e935-142">In the **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="7e935-143">b.</span><span class="sxs-lookup"><span data-stu-id="7e935-143">b.</span></span> <span data-ttu-id="7e935-144">W **lokalizacja projektu** wprowadź lokalizację projektu.</span><span class="sxs-lookup"><span data-stu-id="7e935-144">In the **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="7e935-145">c.</span><span class="sxs-lookup"><span data-stu-id="7e935-145">c.</span></span> <span data-ttu-id="7e935-146">Obok pozycji **SDK projektu** listy rozwijanej wybierz **nowy**, wybierz pozycję **JDK**, a następnie określ folder JDK Java w wersji 1,7 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="7e935-146">Next to the **Project SDK** drop-down list, select **New**, select **JDK**, and then specify the folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="7e935-147">Wybierz **Java 1.8** dla klastra Spark 2.x lub wybierz **Java 1.7** 1.x klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="7e935-147">Select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span> <span data-ttu-id="7e935-148">Lokalizacja domyślna to C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="7e935-148">The default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="7e935-149">d.</span><span class="sxs-lookup"><span data-stu-id="7e935-149">d.</span></span> <span data-ttu-id="7e935-150">W **wersji Spark** listy rozwijanej, Kreator tworzenia projektu Scala integruje poprawnej wersji dla platformy Spark zestawy SDK i Scala.</span><span class="sxs-lookup"><span data-stu-id="7e935-150">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="7e935-151">Jeśli wersja klastra Spark jest starsza niż 2.0, wybierz **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="7e935-151">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="7e935-152">W przeciwnym razie wybierz **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="7e935-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="7e935-153">W tym przykładzie użyto Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="7e935-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="7e935-154">Upewnij się, że używasz repozytorium oznaczone Scala 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="7e935-154">Make sure that you are using the repository marked Scala 2.10.x.</span></span> <span data-ttu-id="7e935-155">Nie używaj repozytorium oznaczone Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="7e935-155">Do not use the repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="7e935-156">Wybierz pozycję **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="7e935-156">Select **Finish**.</span></span>

5. <span data-ttu-id="7e935-157">Jeśli **projektu** widoku nie jest jeszcze otwarty, naciśnij klawisz **Alt + 1** go otworzyć.</span><span class="sxs-lookup"><span data-stu-id="7e935-157">If the **Project** view is not already open, press **Alt+1** to open it.</span></span>

6. <span data-ttu-id="7e935-158">W **Eksplorator projektów**, rozwiń węzeł projektu, a następnie wybierz **src**.</span><span class="sxs-lookup"><span data-stu-id="7e935-158">In **Project Explorer**, expand the project, and then select **src**.</span></span>

7. <span data-ttu-id="7e935-159">Kliknij prawym przyciskiem myszy **src**, wskaż polecenie **nowy**, a następnie wybierz **klasy Scala**.</span><span class="sxs-lookup"><span data-stu-id="7e935-159">Right-click **src**, point to **New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="7e935-160">W **nazwa** wprowadź nazwę, w **rodzaj** wybierz opcję **obiektu**, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e935-160">In the **Name** box, enter a name, in the **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![Utwórz nową klasę Scala okna](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="7e935-162">W pliku .scala Wklej następujący kod:</span><span class="sxs-lookup"><span data-stu-id="7e935-162">In the .scala file, paste the following code:</span></span>

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

10. <span data-ttu-id="7e935-163">Na **kompilacji** menu, wybierz opcję **kompilacji projektu**.</span><span class="sxs-lookup"><span data-stu-id="7e935-163">On the **Build** menu, select **Build project**.</span></span> <span data-ttu-id="7e935-164">Upewnij się, że Kompilacja została pomyślnie ukończona.</span><span class="sxs-lookup"><span data-stu-id="7e935-164">Make sure that the compilation has been completed successfully.</span></span>


## <a name="link-to-the-hortonworks-sandbox"></a><span data-ttu-id="7e935-165">Łącze do piaskownicy Hortonworks</span><span class="sxs-lookup"><span data-stu-id="7e935-165">Link to the Hortonworks Sandbox</span></span>

<span data-ttu-id="7e935-166">Przed połączeniem się piaskownicy Hortonworks (emulatora), musi korzystać z istniejących aplikacji IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7e935-166">Before you can link to a Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="7e935-167">Aby połączyć emulatora, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7e935-167">To link to an emulator, do the following:</span></span>

1. <span data-ttu-id="7e935-168">Otwórz projekt w IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7e935-168">Open the project in IntelliJ.</span></span>

2. <span data-ttu-id="7e935-169">Na **widoku** menu, wybierz opcję **narzędzi systemu Windows**, a następnie wybierz **Eksploratora Azure**.</span><span class="sxs-lookup"><span data-stu-id="7e935-169">On the **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="7e935-170">Rozwiń węzeł **Azure**, kliknij prawym przyciskiem myszy **HDInsight**, a następnie wybierz **Link Emulator**.</span><span class="sxs-lookup"><span data-stu-id="7e935-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="7e935-171">W **emulatora nowe łącze A** okna, wprowadź hasło, które zostały skonfigurowane dla konta głównego piaskownicy Hortonworks, wprowadź wartości podobne do tych na poniższym zrzucie ekranu, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e935-171">In the **Link A New Emulator** window, enter the password that you've configured for the root account of the Hortonworks Sandbox, enter values similar to those in the following screenshot, and then select **OK**.</span></span> 

   ![Okno "Łącze Nowy Emulator"](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="7e935-173">Aby skonfigurować emulator, wybierz **tak**.</span><span class="sxs-lookup"><span data-stu-id="7e935-173">To configure the emulator, select **Yes**.</span></span>

<span data-ttu-id="7e935-174">Po podłączeniu pomyślnie emulator, emulatora (Hortonworks piaskownicy) jest wyświetlane w węźle usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e935-174">When the emulator is connected successfully, the emulator (Hortonworks Sandbox) is listed in the HDInsight node.</span></span>

## <a name="submit-the-spark-scala-application-to-the-hortonworks-sandbox"></a><span data-ttu-id="7e935-175">Przesyłanie aplikacji Spark Scala do piaskownicy Hortonworks</span><span class="sxs-lookup"><span data-stu-id="7e935-175">Submit the Spark Scala application to the Hortonworks Sandbox</span></span>

<span data-ttu-id="7e935-176">Po połączeniu IntelliJ IDEA emulator, możesz przesłać projektu.</span><span class="sxs-lookup"><span data-stu-id="7e935-176">After you have linked IntelliJ IDEA to the emulator, you can submit your project.</span></span>

<span data-ttu-id="7e935-177">Aby przesłać projektu na emulator, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7e935-177">To submit a project to an emulator, do the following:</span></span>

1. <span data-ttu-id="7e935-178">W **Eksplorator projektów**, kliknij prawym przyciskiem myszy projekt, a następnie wybierz **Spark przesyłania aplikacji do usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7e935-178">In **Project Explorer**, right-click the project, and then select **Submit Spark application to HDInsight**.</span></span>

2. <span data-ttu-id="7e935-179">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7e935-179">Do the following:</span></span>

    <span data-ttu-id="7e935-180">a.</span><span class="sxs-lookup"><span data-stu-id="7e935-180">a.</span></span> <span data-ttu-id="7e935-181">W **klastra Spark (tylko w systemie Linux)** listy rozwijanej wybierz użytkownika lokalnego Hortonworks piaskownicy.</span><span class="sxs-lookup"><span data-stu-id="7e935-181">In the **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="7e935-182">b.</span><span class="sxs-lookup"><span data-stu-id="7e935-182">b.</span></span> <span data-ttu-id="7e935-183">W **Nazwa klasy głównym** polu, wybierz lub wprowadź nazwę klasy głównym.</span><span class="sxs-lookup"><span data-stu-id="7e935-183">In the **Main class name** box, choose or enter the main class name.</span></span> <span data-ttu-id="7e935-184">W tym samouczku jest nazwa **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="7e935-184">For this tutorial, the name is **GroupByTest**.</span></span>

3. <span data-ttu-id="7e935-185">Wybierz **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="7e935-185">Select **Submit**.</span></span> <span data-ttu-id="7e935-186">Dzienniki przesyłania zadania są wyświetlane w oknie narzędzia przesyłanie Spark.</span><span class="sxs-lookup"><span data-stu-id="7e935-186">The job submission logs are shown in the Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e935-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7e935-187">Next steps</span></span>

- <span data-ttu-id="7e935-188">Aby dowiedzieć się, jak tworzenie aplikacji dla usługi HDInsight Spark przy użyciu narzędzia HDInsight Tools for IntelliJ, przejdź do [użycia narzędzi HDInsight w zestawie narzędzi Azure for IntelliJ do tworzenie aplikacji Spark dla klastra usługi HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="7e935-188">To learn how to create Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="7e935-189">Aby obejrzeć film wideo narzędzi HDInsight for IntelliJ, przejdź do [wprowadzenie narzędzi HDInsight Tools for IntelliJ rozwoju Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="7e935-189">To watch a video of HDInsight Tools for IntelliJ, go to [Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="7e935-190">Aby dowiedzieć się, jak i debugowanie aplikacji Spark przy użyciu zestawu narzędzi zdalnie w usłudze HDInsight za pośrednictwem protokołu SSH, przejdź do [zdalne debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem protokołu SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="7e935-190">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through SSH, go to [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="7e935-191">Aby dowiedzieć się, jak i debugowanie aplikacji Spark przy użyciu zestawu narzędzi zdalnie w usłudze HDInsight za pośrednictwem sieci VPN, przejdź do [użycia narzędzi HDInsight w zestawie narzędzi Azure for IntelliJ debugowanie aplikacji Spark zdalnie w klastrze HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="7e935-191">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through VPN, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="7e935-192">Aby dowiedzieć się, jak używać narzędzi HDInsight Tools dla programu Eclipse do tworzenia aplikacji Spark, przejdź do [użycia narzędzi HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse tworzenie aplikacji Spark](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="7e935-192">To learn how to use HDInsight Tools for Eclipse to create a Spark application, go to [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="7e935-193">Aby obejrzeć film narzędzi HDInsight Tools dla programu Eclipse, przejdź do [Użyj narzędzia HDInsight dla programu Eclipse tworzenie aplikacji Spark](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="7e935-193">To watch a video of HDInsight Tools for Eclipse, go to [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
