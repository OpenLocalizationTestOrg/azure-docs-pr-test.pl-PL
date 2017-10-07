---
title: "aaaUse MapReduce i programu PowerShell z usługą Hadoop - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse PowerShell tooremotely Uruchom zadań MapReduce z Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="28742-103">Uruchamianie zadań MapReduce z Hadoop w usłudze HDInsight przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="28742-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="28742-104">Ten dokument zawiera przykładowy przy użyciu programu Azure PowerShell toorun zadania MapReduce w usługi Hadoop w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28742-104">This document provides an example of using Azure PowerShell toorun a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="28742-105"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="28742-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="28742-106">**Klaster usługi Azure HDInsight (Hadoop w usłudze HDInsight)**</span><span class="sxs-lookup"><span data-stu-id="28742-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="28742-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="28742-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="28742-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="28742-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="28742-109">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="28742-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="28742-110"><a id="powershell"></a>Uruchomienie zadania MapReduce przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="28742-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="28742-111">Udostępnia program Azure PowerShell *poleceń cmdlet* umożliwiającą tooremotely uruchomienie zadania MapReduce w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28742-111">Azure PowerShell provides *cmdlets* that allow you tooremotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="28742-112">Wewnętrznie, w tym celu za pomocą wywołania REST[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (nazywanych Templeton) systemem hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28742-112">Internally, this is accomplished by using REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="28742-113">Witaj następujące polecenia cmdlet są używane podczas uruchamiania zadań MapReduce w zdalnym klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28742-113">hello following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="28742-114">**Login-AzureRmAccount**: tooyour uwierzytelnia programu Azure PowerShell subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="28742-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription.</span></span>

* <span data-ttu-id="28742-115">**Nowy AzureRmHDInsightMapReduceJobDefinition**: tworzy nowy *definicji zadania* przy użyciu hello określone informacje o MapReduce.</span><span class="sxs-lookup"><span data-stu-id="28742-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using hello specified MapReduce information.</span></span>

* <span data-ttu-id="28742-116">**Start-AzureRmHDInsightJob**: wysyła tooHDInsight definicji zadania hello, uruchamia zadanie hello i zwraca *zadania* obiektów, które mogą być używane toocheck hello stan zadania hello.</span><span class="sxs-lookup"><span data-stu-id="28742-116">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job.</span></span>

* <span data-ttu-id="28742-117">**Czekaj-AzureRmHDInsightJob**: używa stan obiektu zadania hello hello toocheck hello zadania.</span><span class="sxs-lookup"><span data-stu-id="28742-117">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="28742-118">Oczekuje, aż do ukończenia zadania hello lub przekroczono czas oczekiwania hello.</span><span class="sxs-lookup"><span data-stu-id="28742-118">It waits until hello job completes or hello wait time is exceeded.</span></span>

* <span data-ttu-id="28742-119">**Get-AzureRmHDInsightJobOutput**: używane dane wyjściowe hello tooretrieve hello zadania.</span><span class="sxs-lookup"><span data-stu-id="28742-119">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job.</span></span>

<span data-ttu-id="28742-120">Witaj następująca procedura przedstawia sposób toouse toorun te polecenia cmdlet zadania w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="28742-120">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="28742-121">Za pomocą edytora, Zapisz hello następującego kodu jako **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="28742-121">Using an editor, save hello following code as **mapreducejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. <span data-ttu-id="28742-122">Otwórz nowe **programu Azure PowerShell** wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="28742-122">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="28742-123">Zmień lokalizację toohello katalogów hello **mapreducejob.ps1** pliku, a następnie użyj następującego skryptu hello toorun polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="28742-123">Change directories toohello location of hello **mapreducejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="28742-124">Po uruchomieniu skryptu hello monit o nazwę hello hello klastra usługi HDInsight i hello HTTPS/Admin konta nazwę i hasło dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="28742-124">When you run hello script, you are prompted for hello name of hello HDInsight cluster and hello HTTPS/Admin account name and password for hello cluster.</span></span> <span data-ttu-id="28742-125">Mogą być również zostanie wyświetlony monit o tooauthenticate tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="28742-125">You may also be prompted tooauthenticate tooyour Azure subscription.</span></span>

3. <span data-ttu-id="28742-126">Po zakończeniu zadania hello, pojawi się toohello podobne dane wyjściowe następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="28742-126">When hello job completes, you receive output similar toohello following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="28742-127">Te dane wyjściowe wskazuje zadania hello ukończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="28742-127">This output indicates that hello job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="28742-128">Jeśli hello **ExitCode** jest wartością innego niż 0, zobacz [Rozwiązywanie problemów](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="28742-128">If hello **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="28742-129">W tym przykładzie przechowuje także hello pobrane pliki tooan **output.txt** pliku w katalogu hello Uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="28742-129">This example also stores hello downloaded files tooan **output.txt** file in hello directory that you run hello script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="28742-130">Widok danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="28742-130">View output</span></span>

<span data-ttu-id="28742-131">Otwórz hello **output.txt** pliku w hello toosee Edytor tekstu liczby utworzonych przez zadanie hello i wyrazów.</span><span class="sxs-lookup"><span data-stu-id="28742-131">Open hello **output.txt** file in a text editor toosee hello words and counts produced by hello job.</span></span>

> [!NOTE]
> <span data-ttu-id="28742-132">pliki wyjściowe Hello zadania MapReduce są niezmienne.</span><span class="sxs-lookup"><span data-stu-id="28742-132">hello output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="28742-133">Jeśli uruchomisz tego przykładu należy więc toochange hello nazwa pliku wyjściowego hello.</span><span class="sxs-lookup"><span data-stu-id="28742-133">So if you rerun this sample, you need toochange hello name of hello output file.</span></span>

## <span data-ttu-id="28742-134"><a id="troubleshooting"></a>Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="28742-134"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="28742-135">Jeśli żadne informacje nie zostanie zwrócone, po zakończeniu zadania hello, może mieć wystąpił błąd podczas przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="28742-135">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="28742-136">informacje o błędzie tooview dla tego zadania, Dodaj polecenie toohello końca hello hello **mapreducejob.ps1** , zapisz go, a następnie uruchomić.</span><span class="sxs-lookup"><span data-stu-id="28742-136">tooview error information for this job, add hello following command toohello end of hello **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="28742-137">To polecenie cmdlet zwraca informacje hello, które zostało zapisane tooSTDERR na powitania serwera po uruchomieniu zadania hello i może pomóc ustalić, dlaczego zadania hello kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="28742-137">This cmdlet returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="28742-138"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="28742-138"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="28742-139">Jak widać, Azure PowerShell oferuje toorun łatwy sposób na klaster usługi HDInsight, stan zadania hello monitora i pobrać hello w danych wyjściowych zadań MapReduce.</span><span class="sxs-lookup"><span data-stu-id="28742-139">As you can see, Azure PowerShell provides an easy way toorun MapReduce jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="28742-140"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="28742-140"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="28742-141">Aby uzyskać ogólne informacje na temat zadań MapReduce w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="28742-141">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="28742-142">Korzystać z usługi MapReduce na HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="28742-142">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="28742-143">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="28742-143">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="28742-144">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="28742-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="28742-145">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="28742-145">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
