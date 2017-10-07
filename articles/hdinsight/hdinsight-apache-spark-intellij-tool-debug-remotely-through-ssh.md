---
title: "Azure Toolkit for IntelliJ: aplikacji Spark debugować zdalnie za pośrednictwem SSH | Dokumentacja firmy Microsoft"
description: "Wskazówki krok po kroku w sposób toouse narzędzi HDInsight Tools w zestawie narzędzi Azure dla aplikacji toodebug IntelliJ zdalnie w usłudze HDInsight clusters za pośrednictwem SSH"
keywords: zdalne debugowanie intellij, zdalnego debugowania intellij, ssh, intellij, hdinsight, debugowania intellij, debugowania
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="de425-104">Debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem SSH</span><span class="sxs-lookup"><span data-stu-id="de425-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="de425-105">Ten artykuł zawiera instrukcje krok po kroku toouse narzędzi HDInsight Tools w zestawie narzędzi Azure dla aplikacji toodebug IntelliJ zdalnie w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="de425-105">This article provides step-by-step guidance on how toouse HDInsight Tools in Azure Toolkit for IntelliJ toodebug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="de425-106">toodebug projektu, można również wyświetlić hello [aplikacji Spark w usłudze HDInsight debugowania narzędzi Azure for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) wideo.</span><span class="sxs-lookup"><span data-stu-id="de425-106">toodebug your project, you can also view hello [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="de425-107">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="de425-107">**Prerequisites**</span></span>

* <span data-ttu-id="de425-108">**Narzędzia HDInsight Tools w Azure Toolkit for IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="de425-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="de425-109">To narzędzie jest częścią zestawu narzędzi Azure for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="de425-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="de425-110">Aby uzyskać więcej informacji, zobacz [zainstalować zestaw narzędzi platformy Azure dla IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="de425-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="de425-111">**Azure Toolkit for IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="de425-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="de425-112">Użyj tej aplikacji Spark toocreate zestawu narzędzi dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="de425-112">Use this toolkit toocreate Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="de425-113">Aby uzyskać więcej informacji, postępuj zgodnie z instrukcjami hello [użyj narzędzi Azure dla aplikacji Spark toocreate IntelliJ dla klastra usługi HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="de425-113">For more information, follow hello instructions in [Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="de425-114">**Usługa HDInsight SSH z nazwy użytkownika i hasła zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="de425-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="de425-115">Aby uzyskać więcej informacji, zobacz [połączyć tooHDInsight (Hadoop) przy użyciu protokołu SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) i [używanie protokołu SSH tunelowania tooaccess Ambari web UI, JobHistory, NameNode, Oozie i innych sieci web UI](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="de425-115">For more information, see [Connect tooHDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="de425-116">Tworzenie aplikacji Spark Scala i skonfiguruj ją do zdalnego debugowania</span><span class="sxs-lookup"><span data-stu-id="de425-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="de425-117">Uruchom IntelliJ IDEA, a następnie utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="de425-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="de425-118">W hello **nowy projekt** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="de425-118">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="de425-119">a.</span><span class="sxs-lookup"><span data-stu-id="de425-119">a.</span></span> <span data-ttu-id="de425-120">Wybierz **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="de425-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="de425-121">b.</span><span class="sxs-lookup"><span data-stu-id="de425-121">b.</span></span> <span data-ttu-id="de425-122">Wybierz język Java lub Scala szablon na podstawie preferencji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="de425-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="de425-123">Wybierz między hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="de425-123">Select between hello following options:</span></span>

      - <span data-ttu-id="de425-124">**Platforma Spark w usłudze HDInsight (Scala)**</span><span class="sxs-lookup"><span data-stu-id="de425-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="de425-125">**Platforma Spark w usłudze HDInsight (Java)**</span><span class="sxs-lookup"><span data-stu-id="de425-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="de425-126">**Platforma Spark dla klastra usługi HDInsight wykonywania próbki (Scala)**</span><span class="sxs-lookup"><span data-stu-id="de425-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="de425-127">W tym przykładzie użyto **Spark dla próbki Uruchom klastra usługi HDInsight (Scala)** szablonu.</span><span class="sxs-lookup"><span data-stu-id="de425-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="de425-128">c.</span><span class="sxs-lookup"><span data-stu-id="de425-128">c.</span></span> <span data-ttu-id="de425-129">W hello **narzędzia kompilacji** listy, wybierz opcję powitania po, zgodnie z tooyour potrzeby:</span><span class="sxs-lookup"><span data-stu-id="de425-129">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      - <span data-ttu-id="de425-130">**Maven**, obsługę języka Scala Kreator tworzenia projektu</span><span class="sxs-lookup"><span data-stu-id="de425-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="de425-131">**SBT**, do zarządzania hello zależności i budowania hello Scala projektu</span><span class="sxs-lookup"><span data-stu-id="de425-131">**SBT**, for managing hello dependencies and building for hello Scala project</span></span> 

      ![Tworzenie projektu debugowania](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="de425-133">d.</span><span class="sxs-lookup"><span data-stu-id="de425-133">d.</span></span> <span data-ttu-id="de425-134">Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="de425-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="de425-135">W hello dalej **nowy projekt** oknie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="de425-135">In hello next **New Project** window, do hello following:</span></span>

   ![Wybierz hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="de425-137">a.</span><span class="sxs-lookup"><span data-stu-id="de425-137">a.</span></span> <span data-ttu-id="de425-138">Wprowadź nazwę projektu i lokalizacja projektu.</span><span class="sxs-lookup"><span data-stu-id="de425-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="de425-139">b.</span><span class="sxs-lookup"><span data-stu-id="de425-139">b.</span></span> <span data-ttu-id="de425-140">W hello **SDK projektu** listy rozwijanej wybierz **Java 1.8** dla **Spark 2.x** klastra lub wybierz **Java 1.7** dla **Spark 1. x** klastra.</span><span class="sxs-lookup"><span data-stu-id="de425-140">In hello **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="de425-141">c.</span><span class="sxs-lookup"><span data-stu-id="de425-141">c.</span></span> <span data-ttu-id="de425-142">W hello **wersji Spark** listy rozwijanej, Kreator tworzenia projektu Scala hello integruje hello poprawnej wersji dla platformy Spark zestawy SDK i Scala.</span><span class="sxs-lookup"><span data-stu-id="de425-142">In hello **Spark Version** drop-down list, hello Scala project creation wizard integrates hello correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="de425-143">Jeśli hello klastra spark w wersji starszej niż 2.0, wybierz **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="de425-143">If hello spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="de425-144">W przeciwnym razie wybierz **Spark 2.x.**</span><span class="sxs-lookup"><span data-stu-id="de425-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="de425-145">W tym przykładzie użyto **Spark pkt 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="de425-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="de425-146">d.</span><span class="sxs-lookup"><span data-stu-id="de425-146">d.</span></span> <span data-ttu-id="de425-147">Wybierz pozycję **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="de425-147">Select **Finish**.</span></span>

4. <span data-ttu-id="de425-148">Wybierz **src** > **głównego** > **scala** tooopen kodu w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="de425-148">Select **src** > **main** > **scala** tooopen your code in hello project.</span></span> <span data-ttu-id="de425-149">W tym przykładzie użyto hello **SparkCore_wasbloTest** skryptu.</span><span class="sxs-lookup"><span data-stu-id="de425-149">This example uses hello **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="de425-150">Witaj tooaccess **Edytuj konfiguracje** menu, wybierz hello ikonę w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="de425-150">tooaccess hello **Edit Configurations** menu, select hello icon in hello upper-right corner.</span></span> <span data-ttu-id="de425-151">Z tego menu można utworzyć lub edytować hello konfiguracji do zdalnego debugowania.</span><span class="sxs-lookup"><span data-stu-id="de425-151">From this menu, you can create or edit hello configurations for remote debugging.</span></span>

   ![Edycja konfiguracji](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="de425-153">W hello **konfiguracji uruchomienia/debugowania** okno dialogowe, wybierz opcję hello — znak plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="de425-153">In hello **Run/Debug Configurations** dialog box, select hello plus sign (**+**).</span></span> <span data-ttu-id="de425-154">Następnie wybierz hello **Prześlij zadanie Spark** opcji.</span><span class="sxs-lookup"><span data-stu-id="de425-154">Then select hello **Submit Spark Job** option.</span></span>

   ![Dodawanie nowej konfiguracji](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="de425-156">Wprowadź informacje dotyczące **nazwa**, **klastra Spark**, i **Nazwa klasy głównym**.</span><span class="sxs-lookup"><span data-stu-id="de425-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="de425-157">Następnie wybierz **konfiguracji zaawansowanej**.</span><span class="sxs-lookup"><span data-stu-id="de425-157">Then select **Advanced configuration**.</span></span> 

   ![Uruchom konfiguracje debugowania](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="de425-159">W hello **Spark przesyłanie Advanced Configuration** okno dialogowe, wybierz opcję **Spark włączenia debugowania zdalnego**.</span><span class="sxs-lookup"><span data-stu-id="de425-159">In hello **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="de425-160">Wprowadź nazwę użytkownika SSH hello, a następnie wprowadź hasło lub użyć pliku klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="de425-160">Enter hello SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="de425-161">toosave hello konfigurację, kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="de425-161">toosave hello configuration, select **OK**.</span></span>

   ![Włączanie debugowania zdalnego Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="de425-163">Hello konfiguracji jest teraz zapisać nazwą hello, podane.</span><span class="sxs-lookup"><span data-stu-id="de425-163">hello configuration is now saved with hello name you provided.</span></span> <span data-ttu-id="de425-164">Szczegóły konfiguracji hello tooview, wybierz hello jest nazwa konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="de425-164">tooview hello configuration details, select hello configuration name.</span></span> <span data-ttu-id="de425-165">Wybierz zmiany toomake **Edytuj konfiguracje**.</span><span class="sxs-lookup"><span data-stu-id="de425-165">toomake changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="de425-166">Po ukończeniu hello ustawienia konfiguracji można uruchomić projektu hello względem klastra zdalnego hello lub wykonania zdalnego debugowania.</span><span class="sxs-lookup"><span data-stu-id="de425-166">After you complete hello configurations settings, you can run hello project against hello remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-tooperform-remote-debugging"></a><span data-ttu-id="de425-167">Dowiedz się, jak tooperform debugowanie zdalne</span><span class="sxs-lookup"><span data-stu-id="de425-167">Learn how tooperform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="de425-168">Scenariusz 1: Wykonania zdalnego wykonywania</span><span class="sxs-lookup"><span data-stu-id="de425-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="de425-169">W tej sekcji zostanie przedstawiony zostanie sposób toodebug sterowniki i modułów.</span><span class="sxs-lookup"><span data-stu-id="de425-169">In this section, we show you how toodebug drivers and executors.</span></span>

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. <span data-ttu-id="de425-170">Ustawianie punktów podziału, a następnie wybierz hello **debugowania** ikony.</span><span class="sxs-lookup"><span data-stu-id="de425-170">Set up breaking points, and then select hello **Debug** icon.</span></span>

   ![Wybierz ikonę debugowania hello](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="de425-172">Podczas wykonywania programu hello osiągnie punkt podziału hello, zobacz **sterownika** kartę i dwa **Moduł wykonujący** karty w hello **debugera** okienka.</span><span class="sxs-lookup"><span data-stu-id="de425-172">When hello program execution reaches hello breaking point, you see a **Driver** tab and two **Executor** tabs in hello **Debugger** pane.</span></span> <span data-ttu-id="de425-173">Wybierz hello **Program Wznów** toocontinue ikona uruchamiania kodu hello, który następnie osiągnie hello następnego punktu przerwania i koncentruje się na powitania odpowiadającego **Moduł wykonujący** kartę. Możesz przejrzeć dzienniki wykonywania hello na powitania odpowiadającego **konsoli** kartę.</span><span class="sxs-lookup"><span data-stu-id="de425-173">Select hello **Resume Program** icon toocontinue running hello code, which then reaches hello next breakpoint and focuses on hello corresponding **Executor** tab. You can review hello execution logs on hello corresponding **Console** tab.</span></span>

   ![Karta debugowanie](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="de425-175">Scenariusz 2: Wykonaj debugowanie zdalne i naprawienie usterki</span><span class="sxs-lookup"><span data-stu-id="de425-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="de425-176">W tej sekcji zostanie przedstawiony zostanie sposób wartość zmiennej hello aktualizacji toodynamically przy użyciu hello IntelliJ debugowania dla prostego poprawkę możliwości.</span><span class="sxs-lookup"><span data-stu-id="de425-176">In this section, we show you how toodynamically update hello variable value by using hello IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="de425-177">W hello poniższy przykład kodu ponieważ istnieje już plik docelowy hello jest zgłaszany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="de425-177">In hello following code example, an exception is thrown because hello target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="de425-178">debugowanie zdalne tooperform i naprawienie usterki</span><span class="sxs-lookup"><span data-stu-id="de425-178">tooperform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="de425-179">Skonfiguruj dwa punkty podziału, a następnie wybierz hello **debugowania** hello toostart ikona zdalnego debugowania procesu.</span><span class="sxs-lookup"><span data-stu-id="de425-179">Set up two breaking points, and then select hello **Debug** icon toostart hello remote debugging process.</span></span>

2. <span data-ttu-id="de425-180">Kod Hello zatrzymuje się na powitania pierwszego punktu podziału, a parametr hello i informacje o zmiennych są wyświetlane w hello **zmienne** okienka.</span><span class="sxs-lookup"><span data-stu-id="de425-180">hello code stops at hello first breaking point, and hello parameter and variable information are shown in hello **Variables** pane.</span></span> 

3. <span data-ttu-id="de425-181">Wybierz hello **Program Wznów** toocontinue ikony.</span><span class="sxs-lookup"><span data-stu-id="de425-181">Select hello **Resume Program** icon toocontinue.</span></span> <span data-ttu-id="de425-182">Kod Hello zatrzymuje się na powitania drugiego punktu.</span><span class="sxs-lookup"><span data-stu-id="de425-182">hello code stops at hello second point.</span></span> <span data-ttu-id="de425-183">Witaj wyjątek zostanie przechwycony zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="de425-183">hello exception is caught as expected.</span></span>

  ![Zgłoś błąd](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="de425-185">Wybierz hello **Program Wznów** ikonę ponownie.</span><span class="sxs-lookup"><span data-stu-id="de425-185">Select hello **Resume Program** icon again.</span></span> <span data-ttu-id="de425-186">Witaj **HDInsight Spark przesyłanie** okno wyświetla błąd "zadanie uruchamianie nie powiodło się".</span><span class="sxs-lookup"><span data-stu-id="de425-186">hello **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Przesyłanie błędów](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="de425-188">Wybierz wartość zmiennej hello aktualizacji toodynamically przy użyciu hello IntelliJ debugowania możliwości **debugowania** ponownie.</span><span class="sxs-lookup"><span data-stu-id="de425-188">toodynamically update hello variable value by using hello IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="de425-189">Witaj **zmienne** okienko zostanie wyświetlony ponownie.</span><span class="sxs-lookup"><span data-stu-id="de425-189">hello **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="de425-190">Kliknij prawym przyciskiem myszy docelowy hello na powitania **debugowania** , a następnie wybierz **ustaw wartość**.</span><span class="sxs-lookup"><span data-stu-id="de425-190">Right-click hello target on hello **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="de425-191">Następnie wprowadź nową wartość dla zmiennej hello.</span><span class="sxs-lookup"><span data-stu-id="de425-191">Next, enter a new value for hello variable.</span></span> <span data-ttu-id="de425-192">Następnie wybierz **Enter** toosave hello wartość.</span><span class="sxs-lookup"><span data-stu-id="de425-192">Then select **Enter** toosave hello value.</span></span> 

  ![Ustaw wartość](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="de425-194">Wybierz hello **Program Wznów** program hello toorun toocontinue ikony.</span><span class="sxs-lookup"><span data-stu-id="de425-194">Select hello **Resume Program** icon toocontinue toorun hello program.</span></span> <span data-ttu-id="de425-195">Tym razem nie jest wyjątek.</span><span class="sxs-lookup"><span data-stu-id="de425-195">This time, no exception is caught.</span></span> <span data-ttu-id="de425-196">Można zauważyć, że projekt hello działa pomyślnie bez żadnych wyjątków.</span><span class="sxs-lookup"><span data-stu-id="de425-196">You can see that hello project runs successfully without any exceptions.</span></span>

  ![Debugowanie bez wyjątku](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="de425-198"><a name="seealso"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de425-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="de425-199">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="de425-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="de425-200">Demonstracja</span><span class="sxs-lookup"><span data-stu-id="de425-200">Demo</span></span>
* <span data-ttu-id="de425-201">Tworzenie projektu Scala (klip wideo): [tworzenie Spark Scala aplikacji](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="de425-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="de425-202">Debugowanie zdalne (klip wideo): [użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie w klastrze usługi HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="de425-202">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="de425-203">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="de425-203">Scenarios</span></span>
* [<span data-ttu-id="de425-204">Platforma Spark w usłudze BI: wykonaj interakcyjna analiza danych przy użyciu platformy Spark w usłudze HDInsight z narzędzi do analizy Biznesowej</span><span class="sxs-lookup"><span data-stu-id="de425-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="de425-205">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w HDInsight tooanalyze tworzenia temperatury użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="de425-205">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="de425-206">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="de425-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="de425-207">Przesyłanie strumieniowe Spark: Korzystanie z platformy Spark w usłudze HDInsight toobuild w czasie rzeczywistym przesyłania strumieniowego aplikacji</span><span class="sxs-lookup"><span data-stu-id="de425-207">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="de425-208">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="de425-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="de425-209">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="de425-209">Create and run applications</span></span>
* [<span data-ttu-id="de425-210">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="de425-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="de425-211">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="de425-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="de425-212">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="de425-212">Tools and extensions</span></span>
* [<span data-ttu-id="de425-213">Użyj narzędzi Azure dla aplikacji Spark toocreate IntelliJ dla klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="de425-213">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="de425-214">Użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie za pośrednictwem sieci VPN</span><span class="sxs-lookup"><span data-stu-id="de425-214">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="de425-215">Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy</span><span class="sxs-lookup"><span data-stu-id="de425-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="de425-216">Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse toocreate Spark aplikacji</span><span class="sxs-lookup"><span data-stu-id="de425-216">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="de425-217">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="de425-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="de425-218">Jądra dostępne dla notesu Jupyter w klastrze Spark powitania dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="de425-218">Kernels available for Jupyter notebook in hello Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="de425-219">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="de425-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="de425-220">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="de425-220">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="de425-221">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="de425-221">Manage resources</span></span>
* [<span data-ttu-id="de425-222">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="de425-222">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="de425-223">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="de425-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
