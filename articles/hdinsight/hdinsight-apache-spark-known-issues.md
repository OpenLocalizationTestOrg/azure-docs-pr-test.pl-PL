---
title: "klaster aaaTroubleshoot problemy z platformy Apache Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat problemów powiązanych tooApache klastry Spark w usłudze Azure HDInsight i jak toowork wokół tych."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="bcf73-103">Znane problemy dotyczące klastra Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf73-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="bcf73-104">Ten dokument przechowuje informacje o wszystkich hello znane problemy dotyczące hello Spark w usłudze HDInsight w publicznej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="bcf73-104">This document keeps track of all hello known issues for hello HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="bcf73-105">Livy przecieków sesja interaktywna</span><span class="sxs-lookup"><span data-stu-id="bcf73-105">Livy leaks interactive session</span></span>
<span data-ttu-id="bcf73-106">Podczas Livy ponownego uruchomienia (od Ambari lub powodu ponownego uruchomienia maszyny wirtualnej tooheadnode 0) z sesji interaktywnej wciąż jest aktywny, sesji interakcyjne zadania zostaną ujawnione.</span><span class="sxs-lookup"><span data-stu-id="bcf73-106">When Livy is restarted (from Ambari or due tooheadnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="bcf73-107">W związku z tym nowego zadania może zablokowana na powitania stanu zaakceptowane i nie można uruchomić.</span><span class="sxs-lookup"><span data-stu-id="bcf73-107">Because of this, new jobs can stuck in hello Accepted state, and cannot be started.</span></span>

<span data-ttu-id="bcf73-108">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="bcf73-108">**Mitigation:**</span></span>

<span data-ttu-id="bcf73-109">Użyj hello następujące procedury tooworkaround hello problemu:</span><span class="sxs-lookup"><span data-stu-id="bcf73-109">Use hello following procedure tooworkaround hello issue:</span></span>

1. <span data-ttu-id="bcf73-110">SSH do headnode.</span><span class="sxs-lookup"><span data-stu-id="bcf73-110">Ssh into headnode.</span></span> <span data-ttu-id="bcf73-111">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bcf73-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="bcf73-112">Hello uruchom następujące polecenie toofind hello aplikacji identyfikatorów zadań interakcyjne hello uruchomiony przy użyciu programu Livy.</span><span class="sxs-lookup"><span data-stu-id="bcf73-112">Run hello following command toofind hello application IDs of hello interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="bcf73-113">Witaj domyślne nazwy zadania zostaną Livy Jeśli hello zadań została uruchomiona przy użyciu programu Livy sesji interakcyjne nie jawne nazwy parametrów hello sesji Livy uruchomione przez notesu Jupyter hello Nazwa zadania rozpocznie się o remotesparkmagics_ *.</span><span class="sxs-lookup"><span data-stu-id="bcf73-113">hello default job names will be Livy if hello jobs were started with a Livy interactive session with no explicit names specified, For hello Livy session started by Jupyter notebook, hello job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="bcf73-114">Uruchom następujące polecenie tookill hello te zadania.</span><span class="sxs-lookup"><span data-stu-id="bcf73-114">Run hello following command tookill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="bcf73-115">Nowe zadania zostaną uruchomione.</span><span class="sxs-lookup"><span data-stu-id="bcf73-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="bcf73-116">Platforma Spark historii serwer nie został uruchomiony</span><span class="sxs-lookup"><span data-stu-id="bcf73-116">Spark History Server not started</span></span>
<span data-ttu-id="bcf73-117">Platforma Spark historii serwera nie jest uruchamiana automatycznie po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="bcf73-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="bcf73-118">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="bcf73-118">**Mitigation:**</span></span> 

<span data-ttu-id="bcf73-119">Ręcznie uruchom hello historii serwera z narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="bcf73-119">Manually start hello history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="bcf73-120">Problem uprawnień w katalogu dzienników Spark</span><span class="sxs-lookup"><span data-stu-id="bcf73-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="bcf73-121">Gdy hdiuser przesyła zadanie o spark-submit, jest java.io.FileNotFoundException błąd: /var/log/spark/sparkdriver_hdiuser.log (odmowa uprawnień) i hello dziennik sterownik nie jest zapisywany.</span><span class="sxs-lookup"><span data-stu-id="bcf73-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and hello driver log is not written.</span></span> 

<span data-ttu-id="bcf73-122">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="bcf73-122">**Mitigation:**</span></span>

1. <span data-ttu-id="bcf73-123">Dodaj grupę Hadoop toohello hdiuser.</span><span class="sxs-lookup"><span data-stu-id="bcf73-123">Add hdiuser toohello Hadoop group.</span></span> 
2. <span data-ttu-id="bcf73-124">Podaj 777 uprawnienia na /var/log/spark po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="bcf73-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="bcf73-125">Zaktualizuj lokalizacja dziennika spark hello przy użyciu Ambari toobe katalogu z uprawnieniami 777.</span><span class="sxs-lookup"><span data-stu-id="bcf73-125">Update hello spark log location using Ambari toobe a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="bcf73-126">Uruchom spark — przedstawia jako sudo.</span><span class="sxs-lookup"><span data-stu-id="bcf73-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="bcf73-127">Spark Phoenix łącznik nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="bcf73-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="bcf73-128">Obecnie hello Spark Phoenix łącznik nie jest obsługiwany z klastra usługi HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="bcf73-128">Currently, hello Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="bcf73-129">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="bcf73-129">**Mitigation:**</span></span>

<span data-ttu-id="bcf73-130">Zamiast tego należy użyć hello Spark HBase łącznika.</span><span class="sxs-lookup"><span data-stu-id="bcf73-130">You must use hello Spark-HBase connector instead.</span></span> <span data-ttu-id="bcf73-131">Instrukcje można znaleźć [jak łącznik toouse Spark HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="bcf73-131">For instructions see [How toouse Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-toojupyter-notebooks"></a><span data-ttu-id="bcf73-132">Problemy związane z notesów tooJupyter</span><span class="sxs-lookup"><span data-stu-id="bcf73-132">Issues related tooJupyter notebooks</span></span>
<span data-ttu-id="bcf73-133">Poniżej przedstawiono niektóre notesów pokrewne tooJupyter znane problemy.</span><span class="sxs-lookup"><span data-stu-id="bcf73-133">Following are some known issues related tooJupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="bcf73-134">Notesów znaków innych niż ASCII w nazwach plików</span><span class="sxs-lookup"><span data-stu-id="bcf73-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="bcf73-135">Notesów Jupyter, których można użyć w klastrach Spark HDInsight nie powinna mieć znaki spoza zestawu ASCII w nazwach plików.</span><span class="sxs-lookup"><span data-stu-id="bcf73-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="bcf73-136">Jeśli spróbujesz tooupload pliku za pośrednictwem hello Jupyter interfejsu użytkownika, którego filename spoza zestawu ASCII nie będzie dyskretnie (oznacza to, że Jupyter nie możesz przekazać plik hello, ale go nie albo zgłosić błąd widoczne).</span><span class="sxs-lookup"><span data-stu-id="bcf73-136">If you try tooupload a file through hello Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload hello file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="bcf73-137">Wystąpił błąd podczas ładowania notesów o większych rozmiarach</span><span class="sxs-lookup"><span data-stu-id="bcf73-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="bcf73-138">Można napotkać błąd  **`Error loading notebook`**  podczas ładowania notebooki, które są większe.</span><span class="sxs-lookup"><span data-stu-id="bcf73-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="bcf73-139">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="bcf73-139">**Mitigation:**</span></span>

<span data-ttu-id="bcf73-140">Jeśli ten błąd nie oznacza to, że dane są uszkodzone lub zostały utracone.</span><span class="sxs-lookup"><span data-stu-id="bcf73-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="bcf73-141">Notesy nadal znajdują się na dysku w `/var/lib/jupyter`, i może SSH do tooaccess klastra hello je.</span><span class="sxs-lookup"><span data-stu-id="bcf73-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into hello cluster tooaccess them.</span></span> <span data-ttu-id="bcf73-142">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bcf73-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="bcf73-143">Po połączeniu toohello klastra przy użyciu protokołu SSH, możesz skopiować notesy z komputera lokalnego klastra tooyour (przy użyciu protokołu SCP lub WinSCP) utratę hello tooprevent kopii zapasowej wszystkich ważnych danych w notesie hello.</span><span class="sxs-lookup"><span data-stu-id="bcf73-143">Once you have connected toohello cluster using SSH, you can copy your notebooks from your cluster tooyour local machine (using SCP or WinSCP) as a backup tooprevent hello loss of any important data in hello notebook.</span></span> <span data-ttu-id="bcf73-144">Można następnie tunelu SSH w Twojej headnode na port 8001 tooaccess Jupyter bez pośrednictwa hello bramy.</span><span class="sxs-lookup"><span data-stu-id="bcf73-144">You can then SSH tunnel into your headnode at port 8001 tooaccess Jupyter without going through hello gateway.</span></span>  <span data-ttu-id="bcf73-145">Z tego miejsca, można wyczyścić dane wyjściowe hello notesu i zapisz go ponownie rozmiar toominimize hello notesu.</span><span class="sxs-lookup"><span data-stu-id="bcf73-145">From there, you can clear hello output of your notebook and re-save it toominimize hello notebook’s size.</span></span>

<span data-ttu-id="bcf73-146">tooprevent ten błąd zapobiec w hello w przyszłości, należy wykonać, najlepsze rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="bcf73-146">tooprevent this error from happening in hello future, you must follow some best practices:</span></span>

* <span data-ttu-id="bcf73-147">To mały rozmiar notesu hello tookeep ważne.</span><span class="sxs-lookup"><span data-stu-id="bcf73-147">It is important tookeep hello notebook size small.</span></span> <span data-ttu-id="bcf73-148">Wszystkie dane wyjściowe zadań Spark wysyłany ponownie się, że w notesie hello jest trwały tooJupyter.</span><span class="sxs-lookup"><span data-stu-id="bcf73-148">Any output from your Spark jobs that is sent back tooJupyter is persisted in hello notebook.</span></span>  <span data-ttu-id="bcf73-149">Jest najlepszym rozwiązaniem z Jupyter w ogólne tooavoid systemem `.collect()` w dużych RDD firmy lub dataframes; zamiast tego należy toopeek na RDD zawartość należy wziąć pod uwagę uruchomiona `.take()` lub `.sample()` , tak aby dane wyjściowe nie uzyskać zbyt duży.</span><span class="sxs-lookup"><span data-stu-id="bcf73-149">It is a best practice with Jupyter in general tooavoid running `.collect()` on large RDD’s or dataframes; instead, if you want toopeek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="bcf73-150">Ponadto podczas zapisywania notesu wyczyść wszystkie dane wyjściowe komórek tooreduce hello rozmiar.</span><span class="sxs-lookup"><span data-stu-id="bcf73-150">Also, when you save a notebook, clear all output cells tooreduce hello size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="bcf73-151">Notesu uruchamiania początkowego trwa dłużej, niż oczekiwano</span><span class="sxs-lookup"><span data-stu-id="bcf73-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="bcf73-152">Pierwsza instrukcja kodu w notesu Jupyter przy użyciu Spark magic może zająć więcej niż kilka minut.</span><span class="sxs-lookup"><span data-stu-id="bcf73-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="bcf73-153">**Wyjaśnienie:**</span><span class="sxs-lookup"><span data-stu-id="bcf73-153">**Explanation:**</span></span>

<span data-ttu-id="bcf73-154">Dzieje się tak, ponieważ po uruchomieniu pierwszej komórki kodu hello.</span><span class="sxs-lookup"><span data-stu-id="bcf73-154">This happens because when hello first code cell is run.</span></span> <span data-ttu-id="bcf73-155">W tle hello to inicjuje konfigurację sesji, Spark SQL, i są ustawione kontekstów Hive.</span><span class="sxs-lookup"><span data-stu-id="bcf73-155">In hello background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="bcf73-156">Skonfigurowanie tych kontekstów hello pierwszą instrukcją zostanie uruchomione, a dzięki temu hello wrażenie, że instrukcja hello miały toocomplete dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="bcf73-156">After these contexts are set, hello first statement is run and this gives hello impression that hello statement took a long time toocomplete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a><span data-ttu-id="bcf73-157">Limit czasu notesu Jupyter w tworzeniu hello sesji</span><span class="sxs-lookup"><span data-stu-id="bcf73-157">Jupyter notebook timeout in creating hello session</span></span>
<span data-ttu-id="bcf73-158">Gdy klaster Spark jest za mało zasobów, hello Spark i jądra Pyspark notesu Jupyter hello będzie upłynął limit czasu próby toocreate hello sesji.</span><span class="sxs-lookup"><span data-stu-id="bcf73-158">When Spark cluster is out of resources, hello Spark and Pyspark kernels in hello Jupyter notebook will timeout trying toocreate hello session.</span></span> 

<span data-ttu-id="bcf73-159">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="bcf73-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="bcf73-160">Zwolnij na nim w klastrze Spark przez niektóre zasoby:</span><span class="sxs-lookup"><span data-stu-id="bcf73-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="bcf73-161">Zatrzymywanie innych notesów Spark przechodzi toohello Zamknij i menu zatrzymania lub klikając zamknięcia w Eksploratorze notesu hello.</span><span class="sxs-lookup"><span data-stu-id="bcf73-161">Stopping other Spark notebooks by going toohello Close and Halt menu or clicking Shutdown in hello notebook explorer.</span></span>
   * <span data-ttu-id="bcf73-162">Zatrzymywanie innych aplikacji Spark z YARN.</span><span class="sxs-lookup"><span data-stu-id="bcf73-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="bcf73-163">Uruchom ponownie notesu hello, którą chcesz toostart się.</span><span class="sxs-lookup"><span data-stu-id="bcf73-163">Restart hello notebook you were trying toostart up.</span></span> <span data-ttu-id="bcf73-164">Za mało zasobów powinny być dostępne dla toocreate możesz teraz sesji.</span><span class="sxs-lookup"><span data-stu-id="bcf73-164">Enough resources should be available for you toocreate a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="bcf73-165">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="bcf73-165">See also</span></span>
* [<span data-ttu-id="bcf73-166">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf73-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="bcf73-167">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="bcf73-167">Scenarios</span></span>
* [<span data-ttu-id="bcf73-168">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="bcf73-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="bcf73-169">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="bcf73-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="bcf73-170">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf73-170">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="bcf73-171">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="bcf73-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="bcf73-172">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf73-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="bcf73-173">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="bcf73-173">Create and run applications</span></span>
* [<span data-ttu-id="bcf73-174">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="bcf73-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="bcf73-175">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="bcf73-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="bcf73-176">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="bcf73-176">Tools and extensions</span></span>
* [<span data-ttu-id="bcf73-177">Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala</span><span class="sxs-lookup"><span data-stu-id="bcf73-177">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="bcf73-178">Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="bcf73-178">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="bcf73-179">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf73-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="bcf73-180">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf73-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="bcf73-181">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="bcf73-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="bcf73-182">Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf73-182">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="bcf73-183">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="bcf73-183">Manage resources</span></span>
* [<span data-ttu-id="bcf73-184">Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf73-184">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="bcf73-185">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf73-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

