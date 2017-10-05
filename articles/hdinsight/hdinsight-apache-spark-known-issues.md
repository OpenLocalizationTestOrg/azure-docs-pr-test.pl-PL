---
title: "Rozwiązywanie problemów z klastra Apache Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat związane z klastrami Apache Spark w usłudze Azure HDInsight i sposobu obejścia tych problemów."
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
ms.openlocfilehash: 3a493a2c35a6cdd31bb1e4ff66113a8f8d97d4f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="1898b-103">Znane problemy dotyczące klastra Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="1898b-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="1898b-104">Ten dokument przechowuje informacje o znanych problemów w publicznej wersji zapoznawczej HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="1898b-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="1898b-105">Livy przecieków sesja interaktywna</span><span class="sxs-lookup"><span data-stu-id="1898b-105">Livy leaks interactive session</span></span>
<span data-ttu-id="1898b-106">Podczas Livy ponownego uruchomienia (od Ambari lub z powodu ponownego uruchomienia maszyny wirtualnej headnode 0) z sesji interaktywnej wciąż jest aktywny, sesji interakcyjne zadania zostaną ujawnione.</span><span class="sxs-lookup"><span data-stu-id="1898b-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="1898b-107">W związku z tym nowe zadania można zablokowane w stanie zaakceptowane i nie można uruchomić.</span><span class="sxs-lookup"><span data-stu-id="1898b-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span></span>

<span data-ttu-id="1898b-108">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="1898b-108">**Mitigation:**</span></span>

<span data-ttu-id="1898b-109">Użyj poniższej procedury w celu obejścia tego problemu:</span><span class="sxs-lookup"><span data-stu-id="1898b-109">Use the following procedure to workaround the issue:</span></span>

1. <span data-ttu-id="1898b-110">SSH do headnode.</span><span class="sxs-lookup"><span data-stu-id="1898b-110">Ssh into headnode.</span></span> <span data-ttu-id="1898b-111">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1898b-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="1898b-112">Uruchom następujące polecenie, aby znaleźć identyfikatory aplikacji interaktywnych zadania uruchamiane za pośrednictwem programu Livy.</span><span class="sxs-lookup"><span data-stu-id="1898b-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="1898b-113">Nazwy zostaną określone Livy Jeśli zadań została uruchomiona przy użyciu programu Livy sesji interakcyjne nie jawne nazwy sesji dla Livy uruchomione przez notesu Jupyter zadania domyślna nazwa zadania rozpoczyna się od remotesparkmagics_ *.</span><span class="sxs-lookup"><span data-stu-id="1898b-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="1898b-114">Uruchom następujące polecenie, aby kill te zadania.</span><span class="sxs-lookup"><span data-stu-id="1898b-114">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="1898b-115">Nowe zadania zostaną uruchomione.</span><span class="sxs-lookup"><span data-stu-id="1898b-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="1898b-116">Platforma Spark historii serwer nie został uruchomiony</span><span class="sxs-lookup"><span data-stu-id="1898b-116">Spark History Server not started</span></span>
<span data-ttu-id="1898b-117">Platforma Spark historii serwera nie jest uruchamiana automatycznie po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="1898b-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="1898b-118">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="1898b-118">**Mitigation:**</span></span> 

<span data-ttu-id="1898b-119">Ręcznie uruchom serwer historii z narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="1898b-119">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="1898b-120">Problem uprawnień w katalogu dzienników Spark</span><span class="sxs-lookup"><span data-stu-id="1898b-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="1898b-121">Gdy hdiuser przesyła zadanie o spark-submit, jest java.io.FileNotFoundException błąd: /var/log/spark/sparkdriver_hdiuser.log (odmowa uprawnień) i dziennika sterownik nie jest zapisywany.</span><span class="sxs-lookup"><span data-stu-id="1898b-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span></span> 

<span data-ttu-id="1898b-122">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="1898b-122">**Mitigation:**</span></span>

1. <span data-ttu-id="1898b-123">Dodaj hdiuser do grupy usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1898b-123">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="1898b-124">Podaj 777 uprawnienia na /var/log/spark po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="1898b-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="1898b-125">Zaktualizuj lokalizację dziennika spark przy użyciu narzędzia Ambari katalogiem 777 uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="1898b-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="1898b-126">Uruchom spark — przedstawia jako sudo.</span><span class="sxs-lookup"><span data-stu-id="1898b-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="1898b-127">Spark Phoenix łącznik nie jest obsługiwany.</span><span class="sxs-lookup"><span data-stu-id="1898b-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="1898b-128">Obecnie łącznik Spark Phoenix nie jest obsługiwany z klastra usługi HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="1898b-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="1898b-129">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="1898b-129">**Mitigation:**</span></span>

<span data-ttu-id="1898b-130">Zamiast tego należy użyć łącznika Spark HBase.</span><span class="sxs-lookup"><span data-stu-id="1898b-130">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="1898b-131">Instrukcje można znaleźć [sposobu korzystania z łącznika Spark HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="1898b-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="1898b-132">Problemy związane z notesów Jupyter</span><span class="sxs-lookup"><span data-stu-id="1898b-132">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="1898b-133">Poniżej przedstawiono niektóre znane problemy związane z notesów Jupyter.</span><span class="sxs-lookup"><span data-stu-id="1898b-133">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="1898b-134">Notesów znaków innych niż ASCII w nazwach plików</span><span class="sxs-lookup"><span data-stu-id="1898b-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="1898b-135">Notesów Jupyter, których można użyć w klastrach Spark HDInsight nie powinna mieć znaki spoza zestawu ASCII w nazwach plików.</span><span class="sxs-lookup"><span data-stu-id="1898b-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="1898b-136">Próba przekazania pliku za pośrednictwem interfejsu użytkownika Jupyter mającej filename spoza zestawu ASCII nie będzie dyskretnie (to znaczy Jupyter nie możesz przekazać plik, ale go nie albo zgłosić błąd widoczne).</span><span class="sxs-lookup"><span data-stu-id="1898b-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="1898b-137">Wystąpił błąd podczas ładowania notesów o większych rozmiarach</span><span class="sxs-lookup"><span data-stu-id="1898b-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="1898b-138">Można napotkać błąd  **`Error loading notebook`**  podczas ładowania notebooki, które są większe.</span><span class="sxs-lookup"><span data-stu-id="1898b-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="1898b-139">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="1898b-139">**Mitigation:**</span></span>

<span data-ttu-id="1898b-140">Jeśli ten błąd nie oznacza to, że dane są uszkodzone lub zostały utracone.</span><span class="sxs-lookup"><span data-stu-id="1898b-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="1898b-141">Notesy nadal znajdują się na dysku w `/var/lib/jupyter`, i może SSH w klastrze, aby uzyskiwać do nich dostęp.</span><span class="sxs-lookup"><span data-stu-id="1898b-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="1898b-142">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1898b-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="1898b-143">Po połączeniu się z klastrem przy użyciu protokołu SSH, możesz skopiować notesy z klastra na komputerze lokalnym (przy użyciu protokołu SCP lub WinSCP) jako kopię zapasową, aby uniknąć utraty ważnych danych w notesie.</span><span class="sxs-lookup"><span data-stu-id="1898b-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="1898b-144">Można następnie tunelu SSH w Twojej headnode 8001 dostęp bez pośrednictwa bramy Jupyter do portu.</span><span class="sxs-lookup"><span data-stu-id="1898b-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="1898b-145">Z tego miejsca możesz wyczyścić dane wyjściowe notesu i Zapisz ponownie, aby zminimalizować rozmiar notesu.</span><span class="sxs-lookup"><span data-stu-id="1898b-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span></span>

<span data-ttu-id="1898b-146">Aby uniknąć tego błędu w przyszłości w przyszłości, należy wykonać najlepsze rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="1898b-146">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="1898b-147">Należy zachować mały rozmiar notesu.</span><span class="sxs-lookup"><span data-stu-id="1898b-147">It is important to keep the notebook size small.</span></span> <span data-ttu-id="1898b-148">Żadnych danych wyjściowych z zadaniami Spark, które są wysyłane do aplikacji Jupyter jest trwały notesu.</span><span class="sxs-lookup"><span data-stu-id="1898b-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="1898b-149">Ogólnie jest najlepszym rozwiązaniem z Jupyter w celu uniknięcia uruchomiona `.collect()` w dużych RDD firmy lub dataframes; zamiast tego, jeśli chcesz uzyskać wgląd w zawartość RDD, należy wziąć pod uwagę uruchomiona `.take()` lub `.sample()` , tak aby dane wyjściowe nie uzyskać zbyt duży.</span><span class="sxs-lookup"><span data-stu-id="1898b-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="1898b-150">Ponadto podczas zapisywania Notes wyczyść wszystkie dane wyjściowe komórek, aby zmniejszyć rozmiar.</span><span class="sxs-lookup"><span data-stu-id="1898b-150">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="1898b-151">Notesu uruchamiania początkowego trwa dłużej, niż oczekiwano</span><span class="sxs-lookup"><span data-stu-id="1898b-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="1898b-152">Pierwsza instrukcja kodu w notesu Jupyter przy użyciu Spark magic może zająć więcej niż kilka minut.</span><span class="sxs-lookup"><span data-stu-id="1898b-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="1898b-153">**Wyjaśnienie:**</span><span class="sxs-lookup"><span data-stu-id="1898b-153">**Explanation:**</span></span>

<span data-ttu-id="1898b-154">Dzieje się tak, ponieważ po uruchomieniu pierwszej komórki kodu.</span><span class="sxs-lookup"><span data-stu-id="1898b-154">This happens because when the first code cell is run.</span></span> <span data-ttu-id="1898b-155">W tle to inicjuje konfigurację sesji, Spark SQL, i są ustawione kontekstów Hive.</span><span class="sxs-lookup"><span data-stu-id="1898b-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="1898b-156">Po kontekstów te są ustawione, pierwsza instrukcja jest uruchamiane, co powoduje wrażenie który instrukcji przez długi czas do ukończenia.</span><span class="sxs-lookup"><span data-stu-id="1898b-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="1898b-157">Limit czasu notesu Jupyter w tworzenia sesji</span><span class="sxs-lookup"><span data-stu-id="1898b-157">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="1898b-158">Gdy klaster Spark jest za mało zasobów, Spark i Pyspark jądra notesu Jupyter będzie limit czasu próby utworzenia sesji.</span><span class="sxs-lookup"><span data-stu-id="1898b-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span></span> 

<span data-ttu-id="1898b-159">**Środki zaradcze:**</span><span class="sxs-lookup"><span data-stu-id="1898b-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="1898b-160">Zwolnij na nim w klastrze Spark przez niektóre zasoby:</span><span class="sxs-lookup"><span data-stu-id="1898b-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="1898b-161">Zatrzymywanie innych notesów Spark, przechodząc do menu Close and Halt lub kliknąć przycisk zamykania w Eksploratorze notesu.</span><span class="sxs-lookup"><span data-stu-id="1898b-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="1898b-162">Zatrzymywanie innych aplikacji Spark z YARN.</span><span class="sxs-lookup"><span data-stu-id="1898b-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="1898b-163">Uruchom ponownie notesu, który chcesz uruchomić.</span><span class="sxs-lookup"><span data-stu-id="1898b-163">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="1898b-164">Za mało zasobów powinny być dostępne dla Ciebie do utworzenia sesji teraz.</span><span class="sxs-lookup"><span data-stu-id="1898b-164">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="1898b-165">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1898b-165">See also</span></span>
* [<span data-ttu-id="1898b-166">Przegląd: platforma Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1898b-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="1898b-167">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="1898b-167">Scenarios</span></span>
* [<span data-ttu-id="1898b-168">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="1898b-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="1898b-169">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC</span><span class="sxs-lookup"><span data-stu-id="1898b-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="1898b-170">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności</span><span class="sxs-lookup"><span data-stu-id="1898b-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="1898b-171">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="1898b-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="1898b-172">Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="1898b-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="1898b-173">Tworzenie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="1898b-173">Create and run applications</span></span>
* [<span data-ttu-id="1898b-174">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="1898b-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="1898b-175">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="1898b-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="1898b-176">Narzędzia i rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="1898b-176">Tools and extensions</span></span>
* [<span data-ttu-id="1898b-177">Tworzenie i przesyłanie aplikacji Spark Scala przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="1898b-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="1898b-178">Zdalne debugowanie aplikacji Spark przy użyciu dodatku HDInsight Tools Plugin for IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="1898b-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="1898b-179">Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="1898b-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="1898b-180">Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="1898b-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="1898b-181">Korzystanie z zewnętrznych pakietów z notesami Jupyter</span><span class="sxs-lookup"><span data-stu-id="1898b-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="1898b-182">Instalacja oprogramowania Jupyter na komputerze i nawiązywanie połączenia z klastrem Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="1898b-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="1898b-183">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="1898b-183">Manage resources</span></span>
* [<span data-ttu-id="1898b-184">Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1898b-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="1898b-185">Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="1898b-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

