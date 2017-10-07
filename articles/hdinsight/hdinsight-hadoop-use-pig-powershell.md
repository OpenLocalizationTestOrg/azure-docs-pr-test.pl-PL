---
title: "aaaUse Hadoop Pig przy użyciu programu PowerShell w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klastra tooa zadań Pig toosubmit Hadoop w usłudze HDInsight przy użyciu programu Azure PowerShell."
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
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a><span data-ttu-id="9880a-103">Korzystanie z zadań Pig toorun programu Azure PowerShell z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9880a-103">Use Azure PowerShell toorun Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="9880a-104">Ten dokument zawiera przykładowy w klastrze usługi HDInsight przy użyciu programu Azure PowerShell toosubmit Pig zadania tooa Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9880a-104">This document provides an example of using Azure PowerShell toosubmit Pig jobs tooa Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="9880a-105">Pig umożliwia zadań MapReduce toowrite przy użyciu modeli przekształcenia danych języka (Pig Latin), a nie mapy i zmniejszyć funkcji.</span><span class="sxs-lookup"><span data-stu-id="9880a-105">Pig allows you toowrite MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="9880a-106">Niniejszy dokument nie daje szczegółowy opis wykonaj instrukcje Pig Latin hello używany w przykładach hello.</span><span class="sxs-lookup"><span data-stu-id="9880a-106">This document does not provide a detailed description of what hello Pig Latin statements used in hello examples do.</span></span> <span data-ttu-id="9880a-107">Informacje o hello Pig Latin używana w tym przykładzie, zobacz [Use Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="9880a-107">For information about hello Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="9880a-108"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9880a-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="9880a-109">**Klaster Azure HDInsight**</span><span class="sxs-lookup"><span data-stu-id="9880a-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9880a-110">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9880a-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9880a-111">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="9880a-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="9880a-112">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9880a-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="9880a-113"><a id="powershell"></a>Uruchamianie zadań Pig przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="9880a-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="9880a-114">Udostępnia program Azure PowerShell *poleceń cmdlet* umożliwiającą tooremotely uruchamiania zadań Pig w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9880a-114">Azure PowerShell provides *cmdlets* that allow you tooremotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="9880a-115">Wewnętrznie, programu PowerShell używa wywołania REST zbyt[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) uruchomiona w klastrze HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="9880a-115">Internally, PowerShell uses REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="9880a-116">Witaj następujące polecenia cmdlet są używane podczas uruchamiania zadań Pig w zdalnym klastrze usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9880a-116">hello following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="9880a-117">**Login-AzureRmAccount**: tooyour uwierzytelnia programu Azure PowerShell subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9880a-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure Subscription</span></span>
* <span data-ttu-id="9880a-118">**Nowy AzureRmHDInsightPigJobDefinition**: tworzy *definicji zadania* przy użyciu hello określony Pig Latin — instrukcje</span><span class="sxs-lookup"><span data-stu-id="9880a-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using hello specified Pig Latin statements</span></span>
* <span data-ttu-id="9880a-119">**Start-AzureRmHDInsightJob**: wysyła tooHDInsight definicji zadania hello, uruchamia zadanie hello i zwraca *zadania* obiektów, które mogą być używane toocheck hello stan zadania hello</span><span class="sxs-lookup"><span data-stu-id="9880a-119">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="9880a-120">**Czekaj-AzureRmHDInsightJob**: używa stan obiektu zadania hello hello toocheck hello zadania.</span><span class="sxs-lookup"><span data-stu-id="9880a-120">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="9880a-121">Go oczekuje, aż hello zadanie zostało zakończone, lub hello czas oczekiwania został przekroczony.</span><span class="sxs-lookup"><span data-stu-id="9880a-121">It waits until hello job has completed, or hello wait time has been exceeded.</span></span>
* <span data-ttu-id="9880a-122">**Get-AzureRmHDInsightJobOutput**: używane tooretrieve hello dane wyjściowe zadania hello</span><span class="sxs-lookup"><span data-stu-id="9880a-122">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>

<span data-ttu-id="9880a-123">Witaj następująca procedura przedstawia sposób toouse toorun te polecenia cmdlet zadania w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9880a-123">hello following steps demonstrate how toouse these cmdlets toorun a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="9880a-124">Za pomocą edytora, Zapisz hello następującego kodu jako **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="9880a-124">Using an editor, save hello following code as **pigjob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. <span data-ttu-id="9880a-125">Otwórz wiersz polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9880a-125">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="9880a-126">Zmień lokalizację toohello katalogów hello **pigjob.ps1** pliku, a następnie użyj następującego skryptu hello toorun polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="9880a-126">Change directories toohello location of hello **pigjob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="9880a-127">Jesteś zostanie wyświetlony monit o toolog w tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9880a-127">You are prompted toolog in tooyour Azure subscription.</span></span> <span data-ttu-id="9880a-128">Następnie zostanie wyświetlona prośba o hello HTTPs/Admin konta nazwy i hasła dla klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="9880a-128">Then, you are asked for hello HTTPs/Admin account name and password for hello HDInsight cluster.</span></span>

2. <span data-ttu-id="9880a-129">Po zakończeniu zadania hello, powinien on zwrócić informacje toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="9880a-129">When hello job completes, it should return information similar toohello following text:</span></span>

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="9880a-130"><a id="troubleshooting"></a>Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="9880a-130"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="9880a-131">Jeśli żadne informacje nie zostanie zwrócone, po zakończeniu zadania hello, może mieć wystąpił błąd podczas przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="9880a-131">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="9880a-132">informacje o błędzie tooview dla tego zadania, Dodaj polecenie toohello końca hello hello **pigjob.ps1** , zapisz go, a następnie uruchomić.</span><span class="sxs-lookup"><span data-stu-id="9880a-132">tooview error information for this job, add hello following command toohello end of hello **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="9880a-133">To polecenie zwróci hello informacje, które zostało zapisane tooSTDERR na powitania serwera po uruchomieniu zadania hello, a może pomóc ustalić, dlaczego zadania hello kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="9880a-133">This returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="9880a-134"><a id="summary"></a>Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="9880a-134"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="9880a-135">Jak widać, Azure PowerShell oferuje toorun łatwy sposób na klaster usługi HDInsight, stan zadania hello monitora i pobrać hello w danych wyjściowych zadań Pig.</span><span class="sxs-lookup"><span data-stu-id="9880a-135">As you can see, Azure PowerShell provides an easy way toorun Pig jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="9880a-136"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9880a-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="9880a-137">Aby uzyskać ogólne informacje na temat Pig w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9880a-137">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="9880a-138">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9880a-138">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="9880a-139">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9880a-139">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="9880a-140">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9880a-140">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9880a-141">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9880a-141">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
