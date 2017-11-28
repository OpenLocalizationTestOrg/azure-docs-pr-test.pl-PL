---
title: "aaaUse Hadoop Hive przy użyciu programu PowerShell w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Użyj programu PowerShell zapytań programu Hive toorun w Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="e24a9-103">Uruchamianie zapytań Hive przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e24a9-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="e24a9-104">Ten dokument zawiera przykładowy w hello grupy zasobów platformy Azure tryb toorun zapytań programu Hive w Hadoop w klastrze usługi HDInsight przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e24a9-104">This document provides an example of using Azure PowerShell in hello Azure Resource Group mode toorun Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="e24a9-105">Niniejszy dokument nie daje szczegółowy opis wykonaj instrukcje HiveQL hello, które są używane w przykładach hello.</span><span class="sxs-lookup"><span data-stu-id="e24a9-105">This document does not provide a detailed description of what hello HiveQL statements that are used in hello examples do.</span></span> <span data-ttu-id="e24a9-106">Aby uzyskać informacje na powitania HiveQL, który jest używany w tym przykładzie, zobacz [używanie Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="e24a9-106">For information on hello HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="e24a9-107">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="e24a9-107">**Prerequisites**</span></span>

* <span data-ttu-id="e24a9-108">**Klaster Azure HDInsight**: nie ma znaczenia, czy klaster hello jest systemu Windows lub opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="e24a9-108">**An Azure HDInsight cluster**: It does not matter whether hello cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e24a9-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e24a9-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e24a9-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="e24a9-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e24a9-111">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="e24a9-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="e24a9-112">Uruchamianie zapytań Hive przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e24a9-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="e24a9-113">Udostępnia program Azure PowerShell *poleceń cmdlet* umożliwiającą tooremotely uruchamiania zapytań Hive w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e24a9-113">Azure PowerShell provides *cmdlets* that allow you tooremotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="e24a9-114">Wewnętrznie, poleceń cmdlet hello wywołań REST zbyt[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) na powitania klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e24a9-114">Internally, hello cmdlets make REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on hello HDInsight cluster.</span></span>

<span data-ttu-id="e24a9-115">Witaj następujące polecenia cmdlet są używane podczas uruchamiania zapytań Hive w zdalnym klastrze usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e24a9-115">hello following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="e24a9-116">**Dodaj-AzureRmAccount**: tooyour uwierzytelnia programu Azure PowerShell subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e24a9-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription</span></span>
* <span data-ttu-id="e24a9-117">**Nowy AzureRmHDInsightHiveJobDefinition**: tworzy *definicji zadania* przy użyciu hello określone instrukcje HiveQL</span><span class="sxs-lookup"><span data-stu-id="e24a9-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using hello specified HiveQL statements</span></span>
* <span data-ttu-id="e24a9-118">**Start-AzureRmHDInsightJob**: wysyła tooHDInsight definicji zadania hello, uruchamia zadanie hello i zwraca *zadania* obiektów, które mogą być używane toocheck hello stan zadania hello</span><span class="sxs-lookup"><span data-stu-id="e24a9-118">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="e24a9-119">**Czekaj-AzureRmHDInsightJob**: używa stan obiektu zadania hello hello toocheck hello zadania.</span><span class="sxs-lookup"><span data-stu-id="e24a9-119">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="e24a9-120">Oczekuje, aż do ukończenia zadania hello lub przekroczono czas oczekiwania hello.</span><span class="sxs-lookup"><span data-stu-id="e24a9-120">It waits until hello job completes or hello wait time is exceeded.</span></span>
* <span data-ttu-id="e24a9-121">**Get-AzureRmHDInsightJobOutput**: używane tooretrieve hello dane wyjściowe zadania hello</span><span class="sxs-lookup"><span data-stu-id="e24a9-121">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>
* <span data-ttu-id="e24a9-122">**Wywołanie AzureRmHDInsightHiveJob**: używane toorun instrukcje HiveQL.</span><span class="sxs-lookup"><span data-stu-id="e24a9-122">**Invoke-AzureRmHDInsightHiveJob**: Used toorun HiveQL statements.</span></span> <span data-ttu-id="e24a9-123">To polecenie cmdlet bloki hello zapytanie kończy, a następnie zwraca wyniki hello</span><span class="sxs-lookup"><span data-stu-id="e24a9-123">This cmdlet blocks hello query completes, then returns hello results</span></span>
* <span data-ttu-id="e24a9-124">**Użyj AzureRmHDInsightCluster**: ustawia hello bieżącego toouse klastra dla hello **Invoke AzureRmHDInsightHiveJob** polecenia</span><span class="sxs-lookup"><span data-stu-id="e24a9-124">**Use-AzureRmHDInsightCluster**: Sets hello current cluster toouse for hello **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="e24a9-125">Witaj następująca procedura przedstawia sposób toouse toorun te polecenia cmdlet zadania w klastrze usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e24a9-125">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="e24a9-126">Za pomocą edytora, Zapisz hello następującego kodu jako **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="e24a9-126">Using an editor, save hello following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="e24a9-127">Otwórz nowe **programu Azure PowerShell** wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e24a9-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="e24a9-128">Zmień lokalizację toohello katalogów hello **hivejob.ps1** pliku, a następnie użyj następującego skryptu hello toorun polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="e24a9-128">Change directories toohello location of hello **hivejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="e24a9-129">Po uruchomieniu skryptu hello jest monitem tooenter hello klastra nazwę i hello HTTPS/poświadczeń konta administratora klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e24a9-129">When hello script runs, you are prompted tooenter hello cluster name and hello HTTPS/Admin account credentials for hello cluster.</span></span> <span data-ttu-id="e24a9-130">Mogą być również zostanie wyświetlony monit o toolog w tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e24a9-130">You may also be prompted toolog in tooyour Azure subscription.</span></span>

3. <span data-ttu-id="e24a9-131">Po ukończeniu zadania hello zwraca toohello podobne informacje po thext:</span><span class="sxs-lookup"><span data-stu-id="e24a9-131">When hello job completes, it returns information similar toohello following thext:</span></span>

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="e24a9-132">Jak wspomniano wcześniej, **Invoke-Hive** można toorun używane zapytanie i poczekaj, aż hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e24a9-132">As mentioned earlier, **Invoke-Hive** can be used toorun a query and wait for hello response.</span></span> <span data-ttu-id="e24a9-133">Użyj następującego skryptu toosee działanie Invoke-Hive hello:</span><span class="sxs-lookup"><span data-stu-id="e24a9-133">Use hello following script toosee how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="e24a9-134">dane wyjściowe Hello wygląda hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="e24a9-134">hello output looks like hello following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="e24a9-135">Dłużej HiveQL zapytań, można użyć hello Azure PowerShell **ciągów tutaj** polecenia cmdlet lub HiveQL pliki skryptów.</span><span class="sxs-lookup"><span data-stu-id="e24a9-135">For longer HiveQL queries, you can use hello Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="e24a9-136">powitania po fragment kodu przedstawia sposób toouse hello **Invoke-Hive** toorun polecenia cmdlet skrypt HiveQL.</span><span class="sxs-lookup"><span data-stu-id="e24a9-136">hello following snippet shows how toouse hello **Invoke-Hive** cmdlet toorun a HiveQL script file.</span></span> <span data-ttu-id="e24a9-137">Witaj HiveQL pliku skryptu muszą być przekazywane toowasb: / /.</span><span class="sxs-lookup"><span data-stu-id="e24a9-137">hello HiveQL script file must be uploaded toowasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="e24a9-138">Aby uzyskać więcej informacji na temat **ciągów tutaj**, zobacz <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">przy użyciu systemu Windows PowerShell tutaj — ciągi</a>.</span><span class="sxs-lookup"><span data-stu-id="e24a9-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e24a9-139">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="e24a9-139">Troubleshooting</span></span>

<span data-ttu-id="e24a9-140">Jeśli żadne informacje nie zostanie zwrócone, po zakończeniu zadania hello, może mieć wystąpił błąd podczas przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="e24a9-140">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="e24a9-141">informacje o błędzie tooview dla tego zadania, Dodaj hello toohello końca hello **hivejob.ps1** , zapisz go, a następnie uruchomić.</span><span class="sxs-lookup"><span data-stu-id="e24a9-141">tooview error information for this job, add hello following toohello end of hello **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="e24a9-142">To polecenie cmdlet zwraca hello informacji zapisywanych tooSTDERR na powitania serwera po uruchomieniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="e24a9-142">This cmdlet returns hello information that is written tooSTDERR on hello server when you ran hello job.</span></span>

## <a name="summary"></a><span data-ttu-id="e24a9-143">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e24a9-143">Summary</span></span>

<span data-ttu-id="e24a9-144">Jak widać, Azure PowerShell oferuje łatwe toorun zapytań programu Hive w klastrze usługi HDInsight, monitor hello stan zadania i pobrać dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="e24a9-144">As you can see, Azure PowerShell provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e24a9-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e24a9-145">Next steps</span></span>

<span data-ttu-id="e24a9-146">Aby uzyskać ogólne informacje na temat programu Hive w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e24a9-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="e24a9-147">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e24a9-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="e24a9-148">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e24a9-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="e24a9-149">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e24a9-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e24a9-150">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e24a9-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
