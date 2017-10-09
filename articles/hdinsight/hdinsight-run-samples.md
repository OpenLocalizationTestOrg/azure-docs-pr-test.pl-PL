---
title: "Przykłady aaaRun hello Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy przy użyciu usługi Azure HDInsight hello z hello przykłady. Za pomocą skryptów środowiska PowerShell, które uruchamiać programy MapReduce w klastrach danych."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a><span data-ttu-id="483ed-104">Uruchom przykłady MapReduce z Hadoop w HDInsight opartych na systemie Windows</span><span class="sxs-lookup"><span data-stu-id="483ed-104">Run Hadoop MapReduce samples in Windows-based HDInsight</span></span>
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="483ed-105">Zestaw przykładów podano toohelp rozpocząć pracę, uruchomionych zadań MapReduce na klastrów platformy Hadoop za pomocą usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="483ed-105">A set of samples are provided toohelp you get started running MapReduce jobs on Hadoop clusters using Azure HDInsight.</span></span> <span data-ttu-id="483ed-106">Te przykłady są udostępniane na każdym hello HDInsight klastrami zarządzanymi, które można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="483ed-106">These samples are made available on each of hello HDInsight managed clusters that you create.</span></span> <span data-ttu-id="483ed-107">Uruchamianie przykładów zapoznanie się z za pomocą zadania toorun poleceń cmdlet programu Azure PowerShell dotyczących klastrów platformy Hadoop.</span><span class="sxs-lookup"><span data-stu-id="483ed-107">Running these samples familiarize you with using Azure PowerShell cmdlets toorun jobs on Hadoop clusters.</span></span>

* <span data-ttu-id="483ed-108">[**Word liczba**][hdinsight-sample-wordcount]: liczby wystąpień programu word w pliku tekstowym.</span><span class="sxs-lookup"><span data-stu-id="483ed-108">[**Word count**][hdinsight-sample-wordcount]: Counts word occurrences in a text file.</span></span>
* <span data-ttu-id="483ed-109">[**C# przesyłania strumieniowego wyrazów**][hdinsight-sample-csharp-streaming]: liczby wystąpień programu word w pliku tekstowym przy użyciu hello Hadoop interfejsu strumienia.</span><span class="sxs-lookup"><span data-stu-id="483ed-109">[**C# streaming word count**][hdinsight-sample-csharp-streaming]: Counts word occurrences in a text file using hello Hadoop streaming interface.</span></span>
* <span data-ttu-id="483ed-110">[**Narzędzia do szacowania pi**][hdinsight-sample-pi-estimator]: używa statystycznego (quasi Monte Carlo) metoda tooestimate hello wartość liczby pi.</span><span class="sxs-lookup"><span data-stu-id="483ed-110">[**Pi estimator**][hdinsight-sample-pi-estimator]: Uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span>
* <span data-ttu-id="483ed-111">[**10 GB Graysort**][hdinsight-sample-10gb-graysort]: Uruchom ogólnego przeznaczenia GraySort pliku 10 GB, za pomocą usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="483ed-111">[**10-GB Graysort**][hdinsight-sample-10gb-graysort]: Run a general-purpose GraySort on a 10 GB file by using HDInsight.</span></span> <span data-ttu-id="483ed-112">Istnieją trzy toorun zadania: Teragen toogenerate hello danych, danych hello toosort Terasort i tooconfirm Teravalidate poprawnie sortowane hello danych.</span><span class="sxs-lookup"><span data-stu-id="483ed-112">There are three jobs toorun: Teragen toogenerate hello data, Terasort toosort hello data, and Teravalidate tooconfirm that hello data has been properly sorted.</span></span>

> [!NOTE]
> <span data-ttu-id="483ed-113">Kod źródłowy Hello znajdują się w hello dodatku.</span><span class="sxs-lookup"><span data-stu-id="483ed-113">hello source code can be found in hello Appendix.</span></span>

<span data-ttu-id="483ed-114">Znacznie dodatkową dokumentację istnieje w sieci web powitania dla technologii związanych z platformy Hadoop, takich jak programowania MapReduce opartych na języku Java i przesyłanie strumieniowe i dokumentację dotyczącą hello poleceń cmdlet, które są używane w programie Windows PowerShell skryptów.</span><span class="sxs-lookup"><span data-stu-id="483ed-114">Much additional documentation exists on hello web for Hadoop-related technologies, such as Java-based MapReduce programming and streaming, and documentation about hello cmdlets that are used in Windows PowerShell scripting.</span></span> <span data-ttu-id="483ed-115">Aby uzyskać więcej informacji na temat tych zasobów Zobacz:</span><span class="sxs-lookup"><span data-stu-id="483ed-115">For more information about these resources, see:</span></span>

* [<span data-ttu-id="483ed-116">Tworzenie programów Java MapReduce dla platformy Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="483ed-116">Develop Java MapReduce programs for Hadoop in HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [<span data-ttu-id="483ed-117">Przesyłanie zadań Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="483ed-117">Submit Hadoop jobs in HDInsight</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* <span data-ttu-id="483ed-118">[Wprowadzenie tooAzure HDInsight][hdinsight-introduction]</span><span class="sxs-lookup"><span data-stu-id="483ed-118">[Introduction tooAzure HDInsight][hdinsight-introduction]</span></span>

<span data-ttu-id="483ed-119">Dzisiaj wiele osób wybiera Hive i Pig na MapReduce.</span><span class="sxs-lookup"><span data-stu-id="483ed-119">Nowadays, many people choose Hive and Pig over MapReduce.</span></span>  <span data-ttu-id="483ed-120">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="483ed-120">For more information, see:</span></span>

* [<span data-ttu-id="483ed-121">Korzystanie z programu Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="483ed-121">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="483ed-122">Korzystanie z języka Pig w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="483ed-122">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="483ed-123">**Wymagania wstępne**:</span><span class="sxs-lookup"><span data-stu-id="483ed-123">**Prerequisites**:</span></span>

* <span data-ttu-id="483ed-124">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="483ed-124">**An Azure subscription**.</span></span> <span data-ttu-id="483ed-125">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="483ed-125">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="483ed-126">**klaster usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="483ed-126">**an HDInsight cluster**.</span></span> <span data-ttu-id="483ed-127">Aby uzyskać instrukcje na różne sposoby, w których można tworzyć takie klastry hello, zobacz [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="483ed-127">For instructions on hello various ways in which such clusters can be created, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="483ed-128">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="483ed-128">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="483ed-129">Obsługa środowiska Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i zostanie usunięta z dniem 1 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="483ed-129">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="483ed-130">Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="483ed-130">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="483ed-131">Wykonaj kroki hello w [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello najnowszą wersję programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="483ed-131">Follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="483ed-132">Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="483ed-132">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).</span></span>

## <span data-ttu-id="483ed-133"><a name="hdinsight-sample-wordcount"></a>Liczba - Java w programie Word</span><span class="sxs-lookup"><span data-stu-id="483ed-133"><a name="hdinsight-sample-wordcount"></a>Word count - Java</span></span>
<span data-ttu-id="483ed-134">toosubmit projektu MapReduce, należy najpierw utworzyć definicji zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="483ed-134">toosubmit a MapReduce project, you first create a MapReduce job definition.</span></span> <span data-ttu-id="483ed-135">W definicji zadania hello, należy określić plik jar programu MapReduce hello i hello lokalizację pliku jar hello, który jest **wasb:///example/jars/hadoop-mapreduce-examples.jar**hello nazwę klasy i hello argumentów.</span><span class="sxs-lookup"><span data-stu-id="483ed-135">In hello job definition, you specify hello MapReduce program jar file and hello location of hello jar file, which is **wasb:///example/jars/hadoop-mapreduce-examples.jar**, hello class name, and hello arguments.</span></span>  <span data-ttu-id="483ed-136">Hello wordcount MapReduce program przyjmuje dwa argumenty: hello plik źródłowy, który jest używane toocount słów i hello lokalizacji dla danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="483ed-136">hello wordcount MapReduce program takes two arguments: hello source file that is used toocount words, and hello location for output.</span></span>

<span data-ttu-id="483ed-137">Kod źródłowy Hello znajdują się w hello [dodatek a.](#apendix-a---the-word-count-MapReduce-program-in-java).</span><span class="sxs-lookup"><span data-stu-id="483ed-137">hello source code can be found in hello [Appendix A](#apendix-a---the-word-count-MapReduce-program-in-java).</span></span>

<span data-ttu-id="483ed-138">Procedury hello powstania Java MapReduce programów, zobacz - [programy opracowanie MapReduce Java dla platformy Hadoop w usłudze HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)</span><span class="sxs-lookup"><span data-stu-id="483ed-138">For hello procedure of developing a Java MapReduce program, see - [Develop Java MapReduce programs for Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)</span></span>

<span data-ttu-id="483ed-139">**toosubmit zadania MapReduce liczba programu word**</span><span class="sxs-lookup"><span data-stu-id="483ed-139">**toosubmit a word count MapReduce job**</span></span>

1. <span data-ttu-id="483ed-140">Otwórz **programu Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="483ed-140">Open **Windows PowerShell ISE**.</span></span> <span data-ttu-id="483ed-141">Aby uzyskać instrukcje, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="483ed-141">For instructions, see [Install and configure Azure PowerShell][powershell-install-configure].</span></span>
2. <span data-ttu-id="483ed-142">Wklej hello następującego skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="483ed-142">Paste hello following PowerShell script:</span></span>

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    <span data-ttu-id="483ed-143">Witaj zadania MapReduce tworzy plik o nazwie *części r-00000*, który zawiera wyrazy i hello liczby.</span><span class="sxs-lookup"><span data-stu-id="483ed-143">hello MapReduce job produces a file named *part-r-00000*, which contains words and hello counts.</span></span> <span data-ttu-id="483ed-144">skrypt Hello używa hello **findstr** polecenie toolist wszystkie hello wyrazy, które zawiera *"Brak"*.</span><span class="sxs-lookup"><span data-stu-id="483ed-144">hello script uses hello **findstr** command toolist all hello words that contains *"there"*.</span></span>
3. <span data-ttu-id="483ed-145">Ustaw hello pierwsze trzy zmienne i uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="483ed-145">Set hello first three variables, and run hello script.</span></span>

## <span data-ttu-id="483ed-146"><a name="hdinsight-sample-csharp-streaming"></a>Liczba - C# przesyłania strumieniowego w programie Word</span><span class="sxs-lookup"><span data-stu-id="483ed-146"><a name="hdinsight-sample-csharp-streaming"></a>Word count - C# streaming</span></span>
<span data-ttu-id="483ed-147">Hadoop zapewnia przesyłania strumieniowego tooMapReduce interfejsu API, który umożliwia mapy toowrite i zmniejszyć funkcje w językach innych niż Java.</span><span class="sxs-lookup"><span data-stu-id="483ed-147">Hadoop provides a streaming API tooMapReduce, which enables you toowrite map and reduce functions in languages other than Java.</span></span>

> [!NOTE]
> <span data-ttu-id="483ed-148">Witaj czynności w tym samouczku dotyczą tylko na podstawie tooWindows klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="483ed-148">hello steps in this tutorial apply only tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="483ed-149">Na przykład przesyłania strumieniowego dla klastrów usługi HDInsight opartych na systemie Linux, zobacz [opracowanie Python przesyłania strumieniowego programów dla usługi HDInsight](hdinsight-hadoop-streaming-python.md).</span><span class="sxs-lookup"><span data-stu-id="483ed-149">For an example of streaming for Linux-based HDInsight clusters, see [Develop Python streaming programs for HDInsight](hdinsight-hadoop-streaming-python.md).</span></span>

<span data-ttu-id="483ed-150">Przykład Witaj, mapowania hello i reduktor hello są plikami wykonywalnymi odczytać dane wejściowe hello [stdin] [ stdin-stdout-stderr] (wiersz po wierszu) i wyemituj dane wyjściowe hello zbyt[stdout] [stdin-stdout-stderr].</span><span class="sxs-lookup"><span data-stu-id="483ed-150">In hello example, hello mapper and hello reducer are executables that read hello input from [stdin][stdin-stdout-stderr] (line-by-line) and emit hello output too[stdout][stdin-stdout-stderr].</span></span> <span data-ttu-id="483ed-151">Hello program zlicza wszystkich wyrazów hello w tekście hello.</span><span class="sxs-lookup"><span data-stu-id="483ed-151">hello program counts all hello words in hello text.</span></span>

<span data-ttu-id="483ed-152">Gdy plik wykonywalny jest określona dla **mapowań**, każde zadanie mapowania uruchamia hello plik wykonywalny jako oddzielny proces po zainicjowaniu hello mapowania.</span><span class="sxs-lookup"><span data-stu-id="483ed-152">When an executable is specified for **mappers**, each mapper task launches hello executable as a separate process when hello mapper is initialized.</span></span> <span data-ttu-id="483ed-153">Hello mapowania zadanie jest uruchamiane, jego dane wejściowe są konwertowane na linie i źródła hello wierszy toohello [stdin] [ stdin-stdout-stderr] hello procesu.</span><span class="sxs-lookup"><span data-stu-id="483ed-153">As hello mapper task runs, it converts its input into lines, and feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="483ed-154">W hello międzyczasie mapowania hello zbiera hello w wierszu w danych wyjściowych stdout hello hello procesu.</span><span class="sxs-lookup"><span data-stu-id="483ed-154">In hello meantime, hello mapper collects hello line-oriented output from hello stdout of hello process.</span></span> <span data-ttu-id="483ed-155">Konwertuje każdego wiersza w parę klucza i wartości, które są zbierane jako dane wyjściowe hello hello mapowania.</span><span class="sxs-lookup"><span data-stu-id="483ed-155">It converts each line into a key/value pair, which is collected as hello output of hello mapper.</span></span> <span data-ttu-id="483ed-156">Domyślnie hello prefiks wyrównać toohello pierwszy znak tabulacji jest kluczem hello i hello pozostałej części (z wyjątkiem hello znak tabulacji) wiersza hello jest wartością hello.</span><span class="sxs-lookup"><span data-stu-id="483ed-156">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span> <span data-ttu-id="483ed-157">Jeśli w wierszu hello nie ma żadnych znak tabulacji, cały wiersz jest uznawany za hello klucza i hello wartość jest równa null.</span><span class="sxs-lookup"><span data-stu-id="483ed-157">If there is no Tab character in hello line, entire line is considered as hello key, and hello value is null.</span></span>

<span data-ttu-id="483ed-158">Gdy plik wykonywalny jest określona dla **reduktory**, każde zadanie reduktor uruchamia hello plik wykonywalny jako oddzielny proces po zainicjowaniu reduktor hello.</span><span class="sxs-lookup"><span data-stu-id="483ed-158">When an executable is specified for **reducers**, each reducer task launches hello executable as a separate process when hello reducer is initialized.</span></span> <span data-ttu-id="483ed-159">Jak hello reduktor zadanie jest uruchamiane, jego pary klucza/wartości wejściowe są konwertowane na linie i jego źródła toohello wierszy hello [stdin] [ stdin-stdout-stderr] hello procesu.</span><span class="sxs-lookup"><span data-stu-id="483ed-159">As hello reducer task runs, it converts its input key/values pairs into lines, and it feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="483ed-160">W hello międzyczasie reduktor hello zbiera hello w wierszu w danych wyjściowych z hello [stdout] [ stdin-stdout-stderr] hello procesu.</span><span class="sxs-lookup"><span data-stu-id="483ed-160">In hello meantime, hello reducer collects hello line-oriented output from hello [stdout][stdin-stdout-stderr] of hello process.</span></span> <span data-ttu-id="483ed-161">Konwertuje każdy wiersz tooa para klucza i wartości, które są zbierane jako dane wyjściowe hello reduktor hello.</span><span class="sxs-lookup"><span data-stu-id="483ed-161">It converts each line tooa key/value pair, which is collected as hello output of hello reducer.</span></span> <span data-ttu-id="483ed-162">Domyślnie hello prefiks wyrównać toohello pierwszy znak tabulacji jest kluczem hello i hello pozostałej części (z wyjątkiem hello znak tabulacji) wiersza hello jest wartością hello.</span><span class="sxs-lookup"><span data-stu-id="483ed-162">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span>

<span data-ttu-id="483ed-163">**zadanie liczba word przesyłania strumieniowego toosubmit C#**</span><span class="sxs-lookup"><span data-stu-id="483ed-163">**toosubmit a C# streaming word count job**</span></span>

* <span data-ttu-id="483ed-164">Wykonaj procedurę hello w [Word liczba - Java](#word-count-java)i Zastąp definicji zadania hello powitania po wierszu:</span><span class="sxs-lookup"><span data-stu-id="483ed-164">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    <span data-ttu-id="483ed-165">Plik wyjściowy Hello jest:</span><span class="sxs-lookup"><span data-stu-id="483ed-165">hello output file shall be:</span></span>

        example/data/StreamingOutput/wc.txt/part-00000

## <span data-ttu-id="483ed-166"><a name="hdinsight-sample-pi-estimator"></a>Narzędzia do szacowania PI</span><span class="sxs-lookup"><span data-stu-id="483ed-166"><a name="hdinsight-sample-pi-estimator"></a>PI estimator</span></span>
<span data-ttu-id="483ed-167">narzędzia do szacowania pi Hello używa statystycznego (quasi Monte Carlo) metoda tooestimate hello wartość liczby pi.</span><span class="sxs-lookup"><span data-stu-id="483ed-167">hello pi estimator uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="483ed-168">Punkty losowo umieszczone wewnątrz jednostki kwadratowa również objęty koło wpisanego w tym kwadratowy z obszarem równy toohello prawdopodobieństwo okręgu hello pi/4.</span><span class="sxs-lookup"><span data-stu-id="483ed-168">Points placed at random inside of a unit square also fall within a circle inscribed within that square with a probability equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="483ed-169">od wartości hello 4R, gdzie R jest stosunek hello hello liczbę punktów, które znajdują się wewnątrz hello koło toohello łączną liczbę punktów znajdujące się w ramach kwadratowe hello można oszacować Hello wartość liczby pi.</span><span class="sxs-lookup"><span data-stu-id="483ed-169">hello value of pi can be estimated from hello value of 4R, where R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="483ed-170">Hello większego przykładu hello punktów używana, jest lepiej oszacować hello hello.</span><span class="sxs-lookup"><span data-stu-id="483ed-170">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="483ed-171">skrypt Hello podany dla tego przykładu przesyła zadania jar usługi Hadoop i skonfigurowano toorun o wartości 16 mapy, z których każdy jest wymagane toocompute 10 milionów punktów próbki przez hello wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="483ed-171">hello script provided for this sample submits a Hadoop jar job and is set up toorun with a value 16 maps, each of which is required toocompute 10 million sample points by hello parameter values.</span></span> <span data-ttu-id="483ed-172">Parametr, te wartości mogą być zmieniony tooimprove hello Szacowana wartość liczby pi.</span><span class="sxs-lookup"><span data-stu-id="483ed-172">These parameter values can be changed tooimprove hello estimated value of pi.</span></span> <span data-ttu-id="483ed-173">Odwołanie hello 10 pierwszych miejsc dziesiętnych pi są 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="483ed-173">For reference, hello first 10 decimal places of pi are 3.1415926535.</span></span>

<span data-ttu-id="483ed-174">**zadania narzędzia do szacowania pi toosubmit**</span><span class="sxs-lookup"><span data-stu-id="483ed-174">**toosubmit a pi estimator job**</span></span>

* <span data-ttu-id="483ed-175">Wykonaj procedurę hello w [Word liczba - Java](#word-count-java)i Zastąp definicji zadania hello powitania po wierszu:</span><span class="sxs-lookup"><span data-stu-id="483ed-175">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <span data-ttu-id="483ed-176"><a name="hdinsight-sample-10gb-graysort"></a>Graysort 10 GB</span><span class="sxs-lookup"><span data-stu-id="483ed-176"><a name="hdinsight-sample-10gb-graysort"></a>10-GB Graysort</span></span>
<span data-ttu-id="483ed-177">W przykładzie użyto niewielkie 10GB danych, aby można było uruchomić stosunkowo szybko.</span><span class="sxs-lookup"><span data-stu-id="483ed-177">This sample uses a modest 10GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="483ed-178">Używa ona hello MapReduce aplikacje opracowane przez Owen O'Malley oraz organizacji i Arun Murthy, który won hello roczne ogólnego przeznaczenia ("daytona") terabajt sortowania testu porównawczego w 2009 ze stawką 0.578 TB na minutę (100 TB 173 minut).</span><span class="sxs-lookup"><span data-stu-id="483ed-178">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy that won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009 with a rate of 0.578TB/min (100TB in 173 minutes).</span></span> <span data-ttu-id="483ed-179">Aby uzyskać więcej informacji na ten temat oraz innych sortowania testów porównawczych, zobacz hello [Sortbenchmark](http://sortbenchmark.org/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="483ed-179">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="483ed-180">W tym przykładzie używa trzech zestawów MapReduce programów:</span><span class="sxs-lookup"><span data-stu-id="483ed-180">This sample uses three sets of MapReduce programs:</span></span>

1. <span data-ttu-id="483ed-181">**TeraGen** to program MapReduce służy wiersze hello toogenerate toosort danych.</span><span class="sxs-lookup"><span data-stu-id="483ed-181">**TeraGen** is a MapReduce program that you can use toogenerate hello rows of data toosort.</span></span>
2. <span data-ttu-id="483ed-182">**TeraSort** próbek danych wejściowych hello i używa danych hello toosort MapReduce do całkowitej zamówienia.</span><span class="sxs-lookup"><span data-stu-id="483ed-182">**TeraSort** samples hello input data and uses MapReduce toosort hello data into a total order.</span></span> <span data-ttu-id="483ed-183">TeraSort jest standardowe sortowania funkcji MapReduce, z wyjątkiem niestandardowych partycjonerem, który używa posortowaną listę kluczy N-1 próbkowany, definiujące hello klucza zakresu dla każdego Zmniejsz.</span><span class="sxs-lookup"><span data-stu-id="483ed-183">TeraSort is a standard sort of MapReduce functions, except for a custom partitioner that uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="483ed-184">W szczególności, wszystkie klucze takie przykładowe [i-1] < klucz = < próbki [i] są wysyłane tooreduce i.</span><span class="sxs-lookup"><span data-stu-id="483ed-184">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="483ed-185">To gwarantuje, że elementy wyjściowe hello zmniejszyć i wyświetlane są wszystkie mniejszej niż dane wyjściowe hello zmniejszyć i + 1.</span><span class="sxs-lookup"><span data-stu-id="483ed-185">This guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>
3. <span data-ttu-id="483ed-186">**TeraValidate** jest program MapReduce, która weryfikuje te dane wyjściowe hello globalnie jest sortowana.</span><span class="sxs-lookup"><span data-stu-id="483ed-186">**TeraValidate** is a MapReduce program that validates that hello output is globally sorted.</span></span> <span data-ttu-id="483ed-187">Tworzy jeden mapy dla każdego pliku w katalogu wyjściowego hello, a każda mapa zapewnia, że każdy klucz jest mniejsza lub równa toohello poprzedni.</span><span class="sxs-lookup"><span data-stu-id="483ed-187">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="483ed-188">najpierw funkcja mapy Hello rekordów hello generuje również i ostatniego klucze każdego pliku oraz hello reduce — funkcja zapewnia, że hello pierwszy klucz pliku jest większy niż hello ostatniego klucza i-1 pliku.</span><span class="sxs-lookup"><span data-stu-id="483ed-188">hello map function also generates records of hello first and last keys of each file, and hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="483ed-189">Problemów są zgłaszane jako dane wyjściowe hello zmniejszyć z kluczami hello, które są poza kolejnością.</span><span class="sxs-lookup"><span data-stu-id="483ed-189">Any problems are reported as an output of hello reduce with hello keys that are out of order.</span></span>

<span data-ttu-id="483ed-190">argument wejściowy Hello i format wyjściowy, używany przez wszystkie trzy aplikacje, odczytywać i zapisywać pliki tekstowe hello w prawidłowym formacie hello.</span><span class="sxs-lookup"><span data-stu-id="483ed-190">hello input and output format, used by all three applications, reads and writes hello text files in hello right format.</span></span> <span data-ttu-id="483ed-191">dane wyjściowe Hello hello zmniejszyć replikacji ustawił too1 zamiast domyślnych hello 3, ponieważ hello testu porównawczego kontekstem nie jest wymagane, czy dane wyjściowe hello być replikowane na węzłach toomultiple.</span><span class="sxs-lookup"><span data-stu-id="483ed-191">hello output of hello reduce has replication set too1, instead of hello default 3, because hello benchmark contest does not require that hello output data be replicated on toomultiple nodes.</span></span>

<span data-ttu-id="483ed-192">Trzy zadania są wymagane przez hello próbki, każdy odpowiedni tooone hello MapReduce opisanym w wprowadzenie hello:</span><span class="sxs-lookup"><span data-stu-id="483ed-192">Three tasks are required by hello sample, each corresponding tooone of hello MapReduce programs described in hello introduction:</span></span>

1. <span data-ttu-id="483ed-193">Generowanie danych hello sortowania, uruchamiając hello **TeraGen** zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="483ed-193">Generate hello data for sorting by running hello **TeraGen** MapReduce job.</span></span>
2. <span data-ttu-id="483ed-194">Sortowanie danych hello uruchamiając hello **TeraSort** zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="483ed-194">Sort hello data by running hello **TeraSort** MapReduce job.</span></span>
3. <span data-ttu-id="483ed-195">Upewnij się, że hello dane zostały poprawnie sortowane uruchamiając hello **TeraValidate** zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="483ed-195">Confirm that hello data has been correctly sorted by running hello **TeraValidate** MapReduce job.</span></span>

<span data-ttu-id="483ed-196">**toosubmit hello zadania**</span><span class="sxs-lookup"><span data-stu-id="483ed-196">**toosubmit hello jobs**</span></span>

* <span data-ttu-id="483ed-197">Wykonaj procedurę hello w [Word liczba - Java](#word-count-java), i użyj hello następujące definicje zadań:</span><span class="sxs-lookup"><span data-stu-id="483ed-197">Follow hello procedure in [Word count - Java](#word-count-java), and use hello following job definitions:</span></span>

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a><span data-ttu-id="483ed-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="483ed-198">Next steps</span></span>
<span data-ttu-id="483ed-199">Z tego artykułu i artykuły hello w każdej z próbek hello wiesz, jak przykłady hello toorun dołączonego hello klastrów usługi HDInsight przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="483ed-199">From this article and hello articles in each of hello samples, you learned how toorun hello samples included with hello HDInsight clusters by using Azure PowerShell.</span></span> <span data-ttu-id="483ed-200">Samouczki dotyczące przy użyciu Pig, Hive i MapReduce z usługą HDInsight zobacz następujące tematy hello:</span><span class="sxs-lookup"><span data-stu-id="483ed-200">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="483ed-201">[Rozpocząć korzystanie z usługi Hadoop przy użyciu Hive HDInsight tooanalyze przenośnych słuchawki używana][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="483ed-201">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="483ed-202">[Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="483ed-202">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="483ed-203">[Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="483ed-203">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="483ed-204">[Przesyłanie zadań Hadoop w usłudze HDInsight][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="483ed-204">[Submit Hadoop Jobs in HDInsight][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="483ed-205">[Dokumentację platformy Azure HDInsight SDK][hdinsight-sdk-documentation]</span><span class="sxs-lookup"><span data-stu-id="483ed-205">[Azure HDInsight SDK documentation][hdinsight-sdk-documentation]</span></span>

## <a name="appendix-a---hello-word-count-source-code"></a><span data-ttu-id="483ed-206">Dodatek A - hello kodu źródłowego liczba programu Word</span><span class="sxs-lookup"><span data-stu-id="483ed-206">Appendix A - hello Word count source code</span></span>

```java
package org.apache.hadoop.examples;
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
    extends Mapper<Object, Text, Text, IntWritable>{

private final static IntWritable one = new IntWritable(1);
private Text word = new Text();

public void map(Object key, Text value, Context context
                ) throws IOException, InterruptedException {
    StringTokenizer itr = new StringTokenizer(value.toString());
    while (itr.hasMoreTokens()) {
    word.set(itr.nextToken());
    context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
    extends Reducer<Text,IntWritable,Text,IntWritable> {
private IntWritable result = new IntWritable();

public void reduce(Text key, Iterable<IntWritable> values,
                    Context context
                    ) throws IOException, InterruptedException {
    int sum = 0;
    for (IntWritable val : values) {
    sum += val.get();
    }
    result.set(sum);
    context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
Configuration conf = new Configuration();
String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
if (otherArgs.length != 2) {
    System.err.println("Usage: wordcount <in> <out>");
    System.exit(2);
    }
Job job = new Job(conf, "word count");
job.setJarByClass(WordCount.class);
job.setMapperClass(TokenizerMapper.class);
job.setCombinerClass(IntSumReducer.class);
job.setReducerClass(IntSumReducer.class);
job.setOutputKeyClass(Text.class);
job.setOutputValueClass(IntWritable.class);
FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
    }
```

## <a name="appendix-b---hello-word-count-streaming-source-code"></a><span data-ttu-id="483ed-207">Dodatek B — Witaj wyrazów przesyłania strumieniowego kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="483ed-207">Appendix B - hello word count streaming source code</span></span>
<span data-ttu-id="483ed-208">Hello MapReduce program używa hello cat.exe aplikacji jako tekst hello toostream interfejsu mapowania do konsoli hello i wc.exe hello hello zmniejszyć interfejsu toocount hello liczbę słowa, które są przesyłane strumieniowo z dokumentu.</span><span class="sxs-lookup"><span data-stu-id="483ed-208">hello MapReduce program uses hello cat.exe application as a mapping interface toostream hello text into hello console and hello wc.exe application as hello reduce interface toocount hello number of words that are streamed from a document.</span></span> <span data-ttu-id="483ed-209">Zarówno mapowania hello i reduktor znaków, wiersz po wierszu, od hello Standardowy strumień wejściowy (stdin) i zapis toohello Standardowy strumień wyjściowy (stdout).</span><span class="sxs-lookup"><span data-stu-id="483ed-209">Both hello mapper and reducer read characters, line-by-line, from hello standard input stream (stdin) and write toohello standard output stream (stdout).</span></span>

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

<span data-ttu-id="483ed-210">Witaj mapowania kodu używa pliku cat.cs hello [StreamReader] [ streamreader] obiekt znaków hello tooread hello przychodzących strumienia toohello konsoli, który następnie zapisuje dane hello strumienia toohello Standardowy strumień wyjściowy z hello statycznych [elementu Console.Writeline] [ console-writeline] metody.</span><span class="sxs-lookup"><span data-stu-id="483ed-210">hello mapper code in hello cat.cs file uses a [StreamReader][streamreader] object tooread hello characters of hello incoming stream toohello console, which then writes hello stream toohello standard output stream with hello static [Console.Writeline][console-writeline] method.</span></span>

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

<span data-ttu-id="483ed-211">Witaj reduktor kod używa pliku wc.cs hello [StreamReader] [ streamreader] obiekt tooread znaków z hello Standardowy strumień wejściowy że zostały danych wyjściowych przez hello cat.exe mapowania.</span><span class="sxs-lookup"><span data-stu-id="483ed-211">hello reducer code in hello wc.cs file uses a [StreamReader][streamreader]   object tooread characters from hello standard input stream that have been output by hello cat.exe mapper.</span></span> <span data-ttu-id="483ed-212">Jak odczytuje hello znaków z hello [elementu Console.Writeline] [ console-writeline] metody, liczy słowa hello poprzez zliczanie spacje i znaki końca wiersza na koniec hello każdego wyrazu.</span><span class="sxs-lookup"><span data-stu-id="483ed-212">As it reads hello characters with hello [Console.Writeline][console-writeline] method, it counts hello words by counting spaces and end-of-line characters at hello end of each word.</span></span> <span data-ttu-id="483ed-213">Następnie zapisuje hello całkowita toohello Standardowy strumień wyjściowy z hello [elementu Console.Writeline] [ console-writeline] metody.</span><span class="sxs-lookup"><span data-stu-id="483ed-213">It then writes hello total toohello standard output stream with hello [Console.Writeline][console-writeline] method.</span></span>

## <a name="appendix-c---hello-pi-estimator-source-code"></a><span data-ttu-id="483ed-214">Dodatek C — Witaj kodu źródłowego narzędzia do szacowania Pi</span><span class="sxs-lookup"><span data-stu-id="483ed-214">Appendix C - hello Pi estimator source code</span></span>
<span data-ttu-id="483ed-215">narzędzia do szacowania pi Hello kod języka Java, który zawiera funkcje mapowania i reduktor hello jest dostępna dla kontroli poniżej.</span><span class="sxs-lookup"><span data-stu-id="483ed-215">hello pi estimator Java code that contains hello mapper and reducer functions is available for inspection below.</span></span> <span data-ttu-id="483ed-216">program mapowania Hello następnie liczby hello liczbę tych punktów, które są okręgu hello i generuje określoną liczbę punktów, w losowo wybranym umieszczone wewnątrz kwadrat jednostki.</span><span class="sxs-lookup"><span data-stu-id="483ed-216">hello mapper program generates a specified number of points placed at random inside of a unit square and then counts hello number of those points that are inside hello circle.</span></span> <span data-ttu-id="483ed-217">program reduktor Hello akumuluje punktów zliczane przez mapowań hello i następnie szacuje hello wartość pi z hello 4R formuły, gdzie R jest hello stosunek liczby hello punktów zliczane wewnątrz hello koło toohello łączną liczbę punktów znajdujące się w ramach hello kwadratowe.</span><span class="sxs-lookup"><span data-stu-id="483ed-217">hello reducer program accumulates points counted by hello mappers and then estimates hello value of pi from hello formula 4R, where R is hello ratio of hello number of points counted inside hello circle toohello total number of points that are within hello square.</span></span>

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a><span data-ttu-id="483ed-218">Dodatek D - kod źródłowy graysort 10gb hello</span><span class="sxs-lookup"><span data-stu-id="483ed-218">Appendix D - hello 10gb graysort source code</span></span>
<span data-ttu-id="483ed-219">Kod Hello hello TeraSort MapReduce programu jest widoczne dla kontroli w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="483ed-219">hello code for hello TeraSort MapReduce program is presented for inspection in this section.</span></span>

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
