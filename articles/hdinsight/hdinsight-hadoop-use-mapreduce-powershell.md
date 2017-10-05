---
title: "Należy użyć programu PowerShell i MapReduce z Hadoop — usługa Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zdalne uruchamianie zadań MapReduce z Hadoop w usłudze HDInsight przy użyciu programu PowerShell."
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
ms.openlocfilehash: c3801573808709f29cb1e563ac803f225a28cafc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="a4338-103">Uruchamianie zadań MapReduce z Hadoop w usłudze HDInsight przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4338-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="a4338-104">Ten dokument zawiera przykładowy uruchomienie zadania MapReduce w usługi Hadoop w klastrze usługi HDInsight przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4338-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="a4338-105"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a4338-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="a4338-106">**Klaster usługi Azure HDInsight (Hadoop w usłudze HDInsight)**</span><span class="sxs-lookup"><span data-stu-id="a4338-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a4338-107">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="a4338-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a4338-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="a4338-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="a4338-109">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a4338-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="a4338-110"><a id="powershell"></a>Uruchomienie zadania MapReduce przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4338-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="a4338-111">Udostępnia program Azure PowerShell *poleceń cmdlet* umożliwiającą zdalne uruchamianie zadań MapReduce w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4338-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="a4338-112">Wewnętrznie, jest to zrobić za pomocą wywołania REST [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (nazywanych Templeton) uruchomionego w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4338-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="a4338-113">Następujące polecenia cmdlet są używane podczas uruchamiania zadań MapReduce w zdalnym klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4338-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="a4338-114">**Login-AzureRmAccount**: uwierzytelnianie programu Azure PowerShell do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a4338-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="a4338-115">**Nowy AzureRmHDInsightMapReduceJobDefinition**: tworzy nowy *definicji zadania* przy użyciu określonych informacji MapReduce.</span><span class="sxs-lookup"><span data-stu-id="a4338-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="a4338-116">**Start-AzureRmHDInsightJob**: wysyła definicji zadania w usłudze HDInsight, uruchamia zadanie, a następnie zwraca *zadania* obiektu, który może służyć do sprawdzania stanu zadania.</span><span class="sxs-lookup"><span data-stu-id="a4338-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span></span>

* <span data-ttu-id="a4338-117">**Czekaj-AzureRmHDInsightJob**: używa obiektu zadania, aby sprawdzić stan zadania.</span><span class="sxs-lookup"><span data-stu-id="a4338-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="a4338-118">Oczekuje, aż do ukończenia zadania lub przekroczono czas oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="a4338-118">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="a4338-119">**Get-AzureRmHDInsightJobOutput**: służy do pobierania danych wyjściowych zadania.</span><span class="sxs-lookup"><span data-stu-id="a4338-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="a4338-120">Poniższe kroki pokazują, jak używać tych poleceń cmdlet, aby uruchomić zadanie w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4338-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="a4338-121">Za pomocą edytora, Zapisz poniższy kod jako **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="a4338-121">Using an editor, save the following code as **mapreducejob.ps1**.</span></span>

    <span data-ttu-id="a4338-122">[!code-powershell[główne](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span><span class="sxs-lookup"><span data-stu-id="a4338-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span></span>

2. <span data-ttu-id="a4338-123">Otwórz nowe **programu Azure PowerShell** wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a4338-123">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="a4338-124">Zmień katalogi na lokalizację **mapreducejob.ps1** pliku, a następnie użyj następującego polecenia, aby uruchomić skrypt:</span><span class="sxs-lookup"><span data-stu-id="a4338-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="a4338-125">Po uruchomieniu skryptu, monit o nazwę klastra usługi HDInsight i HTTPS/Admin nazwę konta i hasło dla klastra.</span><span class="sxs-lookup"><span data-stu-id="a4338-125">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span></span> <span data-ttu-id="a4338-126">Może też pojawić się prośba do uwierzytelniania do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a4338-126">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="a4338-127">Po zakończeniu zadania, pojawi się dane wyjściowe podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="a4338-127">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="a4338-128">Te dane wyjściowe wskazuje, czy zadanie zakończone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a4338-128">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a4338-129">Jeśli **ExitCode** jest wartością innego niż 0, zobacz [Rozwiązywanie problemów](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="a4338-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="a4338-130">W tym przykładzie przechowuje także pliki pobrane do **output.txt** pliku w katalogu, w którym należy uruchomić skrypt.</span><span class="sxs-lookup"><span data-stu-id="a4338-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="a4338-131">Widok danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="a4338-131">View output</span></span>

<span data-ttu-id="a4338-132">Otwórz **output.txt** plik w edytorze tekstów, aby zobaczyć słów i liczby utworzonej przez zadanie.</span><span class="sxs-lookup"><span data-stu-id="a4338-132">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span></span>

> [!NOTE]
> <span data-ttu-id="a4338-133">Pliki wyjściowe zadania MapReduce są niezmienne.</span><span class="sxs-lookup"><span data-stu-id="a4338-133">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="a4338-134">Dlatego jeśli uruchomisz tego przykładu musisz zmienić nazwę pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="a4338-134">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <span data-ttu-id="a4338-135"><a id="troubleshooting"></a>Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="a4338-135"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="a4338-136">Jeśli żadne informacje nie zostanie zwrócone, po zakończeniu zadania, może mieć wystąpił błąd podczas przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="a4338-136">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="a4338-137">Aby wyświetlić informacje o błędzie dla tego zadania, należy dodać następujące polecenie na końcu **mapreducejob.ps1** , zapisz go, a następnie uruchomić.</span><span class="sxs-lookup"><span data-stu-id="a4338-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="a4338-138">To polecenie cmdlet zwraca informacje, które zostało zapisane STDERR na serwerze po uruchomieniu zadania i może pomóc ustalić, dlaczego zadanie kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="a4338-138">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="a4338-139"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a4338-139"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="a4338-140">Jak widać, programu Azure PowerShell zapewnia prosty sposób uruchamiania zadań MapReduce na klaster usługi HDInsight, monitorować stan zadania i pobrać dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="a4338-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="a4338-141"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a4338-141"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="a4338-142">Aby uzyskać ogólne informacje na temat zadań MapReduce w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a4338-142">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="a4338-143">Korzystać z usługi MapReduce na HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="a4338-143">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="a4338-144">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a4338-144">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="a4338-145">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4338-145">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a4338-146">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4338-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
