---
title: "Korzystanie z języka Pig Hadoop przy użyciu programu PowerShell w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak umożliwiają przesyłanie zadań Pig do klastra usługi Hadoop w usłudze HDInsight przy użyciu programu Azure PowerShell."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 28904b07609ffb40a8195278fd1afd3957896733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-run-pig-jobs-with-hdinsight"></a><span data-ttu-id="ccb93-103">Uruchamianie zadań Pig z usługą HDInsight przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccb93-103">Use Azure PowerShell to run Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="ccb93-104">Ten dokument zawiera przykład do przesyłania zadań Pig do platformy Hadoop w klastrze usługi HDInsight przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccb93-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="ccb93-105">Pig umożliwia zapisu zadań MapReduce przy użyciu języka (Pig Latin) tego przekształcenia danych modeli, a nie mapy i zmniejszyć funkcji.</span><span class="sxs-lookup"><span data-stu-id="ccb93-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="ccb93-106">Niniejszy dokument nie daje szczegółowy opis wykonaj instrukcje Pig Latin przykłady.</span><span class="sxs-lookup"><span data-stu-id="ccb93-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span></span> <span data-ttu-id="ccb93-107">Aby uzyskać informacje na temat Pig Latin używana w tym przykładzie, zobacz [Use Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="ccb93-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="ccb93-108"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ccb93-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="ccb93-109">**Klaster Azure HDInsight**</span><span class="sxs-lookup"><span data-stu-id="ccb93-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ccb93-110">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="ccb93-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ccb93-111">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="ccb93-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="ccb93-112">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ccb93-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="ccb93-113"><a id="powershell"></a>Uruchamianie zadań Pig przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccb93-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="ccb93-114">Udostępnia program Azure PowerShell *poleceń cmdlet* umożliwiającą zdalne uruchamianie zadań Pig w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ccb93-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="ccb93-115">Wewnętrznie PowerShell korzysta z wywołań REST [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) uruchomione w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ccb93-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span></span>

<span data-ttu-id="ccb93-116">Następujące polecenia cmdlet są używane podczas uruchamiania zadań Pig w zdalnym klastrze usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ccb93-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="ccb93-117">**Login-AzureRmAccount**: uwierzytelnianie programu Azure PowerShell do subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ccb93-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription</span></span>
* <span data-ttu-id="ccb93-118">**Nowy AzureRmHDInsightPigJobDefinition**: tworzy *definicji zadania* przy użyciu określonego instrukcje Pig Latin</span><span class="sxs-lookup"><span data-stu-id="ccb93-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements</span></span>
* <span data-ttu-id="ccb93-119">**Start-AzureRmHDInsightJob**: wysyła definicji zadania w usłudze HDInsight, uruchamia zadanie, a następnie zwraca *zadania* obiektu, który może służyć do sprawdzania stanu zadania</span><span class="sxs-lookup"><span data-stu-id="ccb93-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="ccb93-120">**Czekaj-AzureRmHDInsightJob**: używa obiektu zadania, aby sprawdzić stan zadania.</span><span class="sxs-lookup"><span data-stu-id="ccb93-120">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="ccb93-121">Oczekuje, aż zadanie zostało zakończone, lub czas oczekiwania został przekroczony.</span><span class="sxs-lookup"><span data-stu-id="ccb93-121">It waits until the job has completed, or the wait time has been exceeded.</span></span>
* <span data-ttu-id="ccb93-122">**Get-AzureRmHDInsightJobOutput**: służy do pobierania danych wyjściowych zadania</span><span class="sxs-lookup"><span data-stu-id="ccb93-122">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>

<span data-ttu-id="ccb93-123">Poniższe kroki pokazują, jak używać tych poleceń cmdlet, aby uruchomić zadanie w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ccb93-123">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="ccb93-124">Za pomocą edytora, Zapisz poniższy kod jako **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="ccb93-124">Using an editor, save the following code as **pigjob.ps1**.</span></span>

    <span data-ttu-id="ccb93-125">[!code-powershell[główne](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span><span class="sxs-lookup"><span data-stu-id="ccb93-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span></span>

1. <span data-ttu-id="ccb93-126">Otwórz wiersz polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccb93-126">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="ccb93-127">Zmień katalogi na lokalizację **pigjob.ps1** pliku, a następnie użyj następującego polecenia, aby uruchomić skrypt:</span><span class="sxs-lookup"><span data-stu-id="ccb93-127">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="ccb93-128">Zostanie wyświetlony monit logowania do Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ccb93-128">You are prompted to log in to your Azure subscription.</span></span> <span data-ttu-id="ccb93-129">Następnie zostanie wyświetlona prośba o HTTPs/Admin nazwę konta i hasło dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ccb93-129">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span></span>

2. <span data-ttu-id="ccb93-130">Po zakończeniu zadania, jego powinny zostać zwrócone informacje podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="ccb93-130">When the job completes, it should return information similar to the following text:</span></span>

        Start the Pig job ...
        Wait for the Pig job to complete ...
        Display the standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="ccb93-131"><a id="troubleshooting"></a>Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="ccb93-131"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="ccb93-132">Jeśli żadne informacje nie zostanie zwrócone, po zakończeniu zadania, może mieć wystąpił błąd podczas przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="ccb93-132">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="ccb93-133">Aby wyświetlić informacje o błędzie dla tego zadania, należy dodać następujące polecenie na końcu **pigjob.ps1** , zapisz go, a następnie uruchomić.</span><span class="sxs-lookup"><span data-stu-id="ccb93-133">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print the output of the Pig job.
    Write-Host "Display the standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="ccb93-134">To zwraca informacje, które zostało zapisane STDERR na serwerze po uruchomieniu zadania i może pomóc ustalić, dlaczego zadanie kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="ccb93-134">This returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="ccb93-135"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="ccb93-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="ccb93-136">Jak widać, programu Azure PowerShell zapewnia prosty sposób uruchamiania zadań Pig na klaster usługi HDInsight, monitorować stan zadania i pobrać dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="ccb93-136">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="ccb93-137"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ccb93-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="ccb93-138">Aby uzyskać ogólne informacje na temat Pig w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ccb93-138">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="ccb93-139">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ccb93-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="ccb93-140">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ccb93-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ccb93-141">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ccb93-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ccb93-142">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="ccb93-142">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
