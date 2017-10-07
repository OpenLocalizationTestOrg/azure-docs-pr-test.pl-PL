---
title: "narzędzia tooAzure aaaMigrate Menedżera zasobów dla usługi HDInsight | Dokumentacja firmy Microsoft"
description: "Jak narzędzia tooAzure toomigrate programowanie Menedżera zasobów dla klastrów usługi HDInsight"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="c47fe-103">Migrowanie tooAzure narzędzi programistycznych opartych na Menedżera zasobów dla klastrów usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="c47fe-103">Migrating tooAzure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="c47fe-104">HDInsight wycofano narzędzi Azure Service Manager ASM dla usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c47fe-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="c47fe-105">Jeśli był używany programu Azure PowerShell, interfejsu wiersza polecenia Azure lub hello zestawu .NET SDK HDInsight toowork z klastrami usługi HDInsight, to toouse zachęca hello Azure Resource Manager ARM-bitowego programu PowerShell, interfejsu wiersza polecenia i zestawu .NET SDK w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c47fe-105">If you have been using Azure PowerShell, Azure CLI, or hello HDInsight .NET SDK toowork with HDInsight clusters, you are encouraged toouse hello Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="c47fe-106">Ten artykuł zawiera wskaźniki dotyczące toomigrate toohello nowe opartego na architekturze ARM podejście.</span><span class="sxs-lookup"><span data-stu-id="c47fe-106">This article provides pointers on how toomigrate toohello new ARM-based approach.</span></span> <span data-ttu-id="c47fe-107">Wszędzie tam, gdzie ma to zastosowanie, w tym artykule jest także punktów hello różnic między hello ASM i ARM podejścia dla usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c47fe-107">Wherever applicable, this article also points out hello differences between hello ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c47fe-108">Hello obsługę funkcji ASM programu PowerShell, interfejsu wiersza polecenia, jak i zestawu .NET SDK nie będzie kontynuowane na **1 stycznia 2017**.</span><span class="sxs-lookup"><span data-stu-id="c47fe-108">hello support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a><span data-ttu-id="c47fe-109">Migrowanie tooAzure interfejsu wiersza polecenia Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c47fe-109">Migrating Azure CLI tooAzure Resource Manager</span></span>
<span data-ttu-id="c47fe-110">Hello Azure CLI teraz domyślne tooAzure tryb Resource Manager (ARM), chyba że w przypadku uaktualniania z poprzedniej instalacji; w takim przypadku należy toouse hello `azure config mode arm` tryb tooARM tooswitch polecenia.</span><span class="sxs-lookup"><span data-stu-id="c47fe-110">hello Azure CLI now defaults tooAzure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need toouse hello `azure config mode arm` command tooswitch tooARM mode.</span></span>

<span data-ttu-id="c47fe-111">podstawowe polecenia Hello tego wiersza polecenia platformy Azure z usługą HDInsight przy użyciu usługi Azure Service Management (ASM) pod warunkiem toowork hello są takie same hello podczas przy użyciu programu ARM; Jednak niektóre parametry i przełączników mogą mieć nowych nazw, a dostępnych wiele nowych parametrów podczas przy użyciu programu ARM.</span><span class="sxs-lookup"><span data-stu-id="c47fe-111">hello basic commands that hello Azure CLI provided toowork with HDInsight using Azure Service Management (ASM) are hello same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="c47fe-112">Na przykład może teraz użyć `azure hdinsight cluster create` toospecify hello Azure Virtual Network, powinny zostać utworzone w klastrze lub Hive i informacji na potrzeby magazynu metadanych Oozie.</span><span class="sxs-lookup"><span data-stu-id="c47fe-112">For example, you can now use `azure hdinsight cluster create` toospecify hello Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="c47fe-113">Dostępne są następujące podstawowe polecenia do pracy z usługą HDInsight przy użyciu usługi Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="c47fe-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="c47fe-114">`azure hdinsight cluster create`-Tworzy nowy klaster usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="c47fe-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="c47fe-115">`azure hdinsight cluster delete`— Usuwa istniejącego klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="c47fe-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="c47fe-116">`azure hdinsight cluster show`-wyświetlać informacje na temat istniejącego klastra</span><span class="sxs-lookup"><span data-stu-id="c47fe-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="c47fe-117">`azure hdinsight cluster list`— Wyświetla klastrów usługi HDInsight dla subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c47fe-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="c47fe-118">Użyj hello `-h` przełącznika tooinspect hello parametry i opcje dostępne dla każdego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c47fe-118">Use hello `-h` switch tooinspect hello parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="c47fe-119">Nowe polecenia</span><span class="sxs-lookup"><span data-stu-id="c47fe-119">New commands</span></span>
<span data-ttu-id="c47fe-120">Są dostępne z usługi Azure Resource Manager nowego polecenia:</span><span class="sxs-lookup"><span data-stu-id="c47fe-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="c47fe-121">`azure hdinsight cluster resize`-dynamicznie zmiany hello liczba węzłów procesu roboczego w klastrze hello</span><span class="sxs-lookup"><span data-stu-id="c47fe-121">`azure hdinsight cluster resize` - dynamically changes hello number of worker nodes in hello cluster</span></span>
* <span data-ttu-id="c47fe-122">`azure hdinsight cluster enable-http-access`— Umożliwia klastra toohello dostępu protokołu HTTPs (na domyślne)</span><span class="sxs-lookup"><span data-stu-id="c47fe-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access toohello cluster (on by default)</span></span>
* <span data-ttu-id="c47fe-123">`azure hdinsight cluster disable-http-access`— Wyłącza HTTPs dostęp toohello klastra</span><span class="sxs-lookup"><span data-stu-id="c47fe-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access toohello cluster</span></span>
* <span data-ttu-id="c47fe-124">`azure hdinsight script-action`-Zawiera polecenia służące do tworzenia/Zarządzanie akcji skryptu w klastrze</span><span class="sxs-lookup"><span data-stu-id="c47fe-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="c47fe-125">`azure hdinsight config`-Zawiera polecenia służące do tworzenia pliku konfiguracji, który może być używany z hello `hdinsight cluster create` polecenia tooprovide informacje o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c47fe-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with hello `hdinsight cluster create` command tooprovide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="c47fe-126">Przestarzałe poleceń</span><span class="sxs-lookup"><span data-stu-id="c47fe-126">Deprecated commands</span></span>
<span data-ttu-id="c47fe-127">Jeśli używasz hello `azure hdinsight job` tooyour klastra usługi HDInsight polecenia toosubmit zadań, nie są one dostępne za pośrednictwem hello poleceń ARM.</span><span class="sxs-lookup"><span data-stu-id="c47fe-127">If you use hello `azure hdinsight job` commands toosubmit jobs tooyour HDInsight cluster, these are not available through hello ARM commands.</span></span> <span data-ttu-id="c47fe-128">Tooprogrammatically przesyłania zadań tooHDInsight ze skryptów, należy zamiast tego należy używać hello dostarczanych z usługą HDInsight interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="c47fe-128">If you need tooprogrammatically submit jobs tooHDInsight from scripts, you should instead use hello REST APIs provided by HDInsight.</span></span> <span data-ttu-id="c47fe-129">Aby uzyskać więcej informacji na przesyłanie zadań przy użyciu interfejsów API REST zobacz następujące dokumenty hello.</span><span class="sxs-lookup"><span data-stu-id="c47fe-129">For more information on submitting jobs using REST APIs, see hello following documents.</span></span>

* [<span data-ttu-id="c47fe-130">Uruchamianie zadań MapReduce z Hadoop w usłudze HDInsight przy użyciu programu cURL</span><span class="sxs-lookup"><span data-stu-id="c47fe-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="c47fe-131">Uruchamianie zapytań Hive z usługą Hadoop w usłudze HDInsight przy użyciu programu cURL</span><span class="sxs-lookup"><span data-stu-id="c47fe-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="c47fe-132">Uruchamianie zadań Pig z usługą Hadoop w usłudze HDInsight przy użyciu programu cURL</span><span class="sxs-lookup"><span data-stu-id="c47fe-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="c47fe-133">Aby informacji na temat innych sposobów toorun MapReduce, Hive i wieprzowa interaktywnego, zobacz [Użyj MapReduce z Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md), [używanie Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md), i [Use Pig z platformą Hadoop w HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="c47fe-133">For information on other ways toorun MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="c47fe-134">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c47fe-134">Examples</span></span>
<span data-ttu-id="c47fe-135">**Tworzenie klastra**</span><span class="sxs-lookup"><span data-stu-id="c47fe-135">**Creating a cluster**</span></span>

* <span data-ttu-id="c47fe-136">Polecenie stary (ASM)-`azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="c47fe-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="c47fe-137">Nowe polecenie (ARM)-`azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="c47fe-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="c47fe-138">**Usuwanie klastra**</span><span class="sxs-lookup"><span data-stu-id="c47fe-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="c47fe-139">Polecenie stary (ASM)-`azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="c47fe-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="c47fe-140">Nowe polecenie (ARM)-`azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="c47fe-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="c47fe-141">**Lista klastrów**</span><span class="sxs-lookup"><span data-stu-id="c47fe-141">**List clusters**</span></span>

* <span data-ttu-id="c47fe-142">Polecenie stary (ASM)-`azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="c47fe-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="c47fe-143">Nowe polecenie (ARM)-`azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="c47fe-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="c47fe-144">Dla polecenia listy hello, określając hello grupy zasobów przy użyciu `-g` zwróci tylko klastry hello w hello określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c47fe-144">For hello list command, specifying hello resource group using `-g` will return only hello clusters in hello specified resource group.</span></span>
> 
> 

<span data-ttu-id="c47fe-145">**Pokaż informacje o klastrze**</span><span class="sxs-lookup"><span data-stu-id="c47fe-145">**Show cluster information**</span></span>

* <span data-ttu-id="c47fe-146">Polecenie stary (ASM)-`azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="c47fe-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="c47fe-147">Nowe polecenie (ARM)-`azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="c47fe-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a><span data-ttu-id="c47fe-148">Migrowanie tooAzure programu PowerShell usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c47fe-148">Migrating Azure PowerShell tooAzure Resource Manager</span></span>
<span data-ttu-id="c47fe-149">Witaj ogólne informacje dotyczące programu Azure PowerShell w trybie Azure Resource Manager (ARM) hello można znaleźć w folderze [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c47fe-149">hello general information about Azure PowerShell in hello Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="c47fe-150">Witaj poleceń cmdlet programu Azure PowerShell ARM może być zainstalowane obok siebie z hello ASM poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c47fe-150">hello Azure PowerShell ARM cmdlets can be installed side-by-side with hello ASM cmdlets.</span></span> <span data-ttu-id="c47fe-151">polecenia cmdlet Hello z dwóch trybów hello można rozróżnić przy użyciu ich nazw.</span><span class="sxs-lookup"><span data-stu-id="c47fe-151">hello cmdlets from hello two modes can be distinguished by their names.</span></span>  <span data-ttu-id="c47fe-152">Tryb ARM Hello ma *AzureRmHDInsight* w nazwach polecenia cmdlet hello porównanie zbyt*AzureHDInsight* w trybie ASM hello.</span><span class="sxs-lookup"><span data-stu-id="c47fe-152">hello ARM mode has *AzureRmHDInsight* in hello cmdlet names comparing too*AzureHDInsight* in hello ASM mode.</span></span>  <span data-ttu-id="c47fe-153">Na przykład *AzureRmHDInsightCluster nowy* vs. *Nowy AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="c47fe-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="c47fe-154">Parametry i opcje może mieć nazwy wiadomości i dostępnych wiele nowych parametrów podczas przy użyciu programu ARM.</span><span class="sxs-lookup"><span data-stu-id="c47fe-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="c47fe-155">Na przykład kilka poleceń cmdlet wymagają nowy przełącznik o nazwie *- ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="c47fe-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="c47fe-156">Przed użyciem polecenia cmdlet usługi HDInsight hello, możesz połączyć tooyour konto platformy Azure i Utwórz nową grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="c47fe-156">Before you can use hello HDInsight cmdlets, you must connect tooyour Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="c47fe-157">Login-AzureRmAccount lub [AzureRmProfile wybierz](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="c47fe-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="c47fe-158">Zobacz [uwierzytelniania nazwy głównej usługi z usługą Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="c47fe-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="c47fe-159">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c47fe-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="c47fe-160">Zmieniono nazwę polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="c47fe-160">Renamed cmdlets</span></span>
<span data-ttu-id="c47fe-161">Witaj toolist polecenia cmdlet funkcji ASM usługi HDInsight w konsoli środowiska Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c47fe-161">toolist hello HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="c47fe-162">Witaj Poniższa tabela zawiera listę poleceń cmdlet funkcji ASM hello i nazw w trybie ARM hello:</span><span class="sxs-lookup"><span data-stu-id="c47fe-162">hello following table lists hello ASM cmdlets and their names in hello ARM mode:</span></span>

| <span data-ttu-id="c47fe-163">Polecenia cmdlet funkcji ASM</span><span class="sxs-lookup"><span data-stu-id="c47fe-163">ASM cmdlets</span></span> | <span data-ttu-id="c47fe-164">Polecenia cmdlet ARM</span><span class="sxs-lookup"><span data-stu-id="c47fe-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="c47fe-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="c47fe-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="c47fe-166">Dodaj AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="c47fe-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="c47fe-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="c47fe-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="c47fe-168">Dodaj AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="c47fe-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="c47fe-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="c47fe-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="c47fe-170">Dodaj AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="c47fe-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="c47fe-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="c47fe-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="c47fe-172">Dodaj AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="c47fe-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="c47fe-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="c47fe-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="c47fe-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="c47fe-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="c47fe-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="c47fe-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="c47fe-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="c47fe-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="c47fe-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="c47fe-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="c47fe-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="c47fe-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="c47fe-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="c47fe-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="c47fe-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="c47fe-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="c47fe-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="c47fe-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="c47fe-182">Udziel AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="c47fe-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="c47fe-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="c47fe-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="c47fe-184">Udziel AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="c47fe-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="c47fe-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="c47fe-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="c47fe-186">Wywołanie AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="c47fe-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="c47fe-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="c47fe-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="c47fe-188">Nowe AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="c47fe-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="c47fe-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="c47fe-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="c47fe-190">Nowe AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="c47fe-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="c47fe-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="c47fe-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="c47fe-192">Nowe AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="c47fe-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="c47fe-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="c47fe-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="c47fe-194">Nowe AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="c47fe-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="c47fe-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="c47fe-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="c47fe-196">Nowe AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="c47fe-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="c47fe-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="c47fe-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="c47fe-198">Nowe AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="c47fe-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="c47fe-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="c47fe-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="c47fe-200">Nowe AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="c47fe-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="c47fe-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="c47fe-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="c47fe-202">Usuń AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="c47fe-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="c47fe-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="c47fe-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="c47fe-204">Odwołaj AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="c47fe-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="c47fe-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="c47fe-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="c47fe-206">Odwołaj AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="c47fe-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="c47fe-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="c47fe-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="c47fe-208">Zestaw AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="c47fe-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="c47fe-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="c47fe-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="c47fe-210">Zestaw AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="c47fe-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="c47fe-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="c47fe-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="c47fe-212">Start AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="c47fe-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="c47fe-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="c47fe-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="c47fe-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="c47fe-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="c47fe-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="c47fe-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="c47fe-216">Użyj AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="c47fe-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="c47fe-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="c47fe-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="c47fe-218">AzureRmHDInsightJob oczekiwania</span><span class="sxs-lookup"><span data-stu-id="c47fe-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="c47fe-219">Nowe polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="c47fe-219">New cmdlets</span></span>
<span data-ttu-id="c47fe-220">Oto Hello hello nowe polecenia cmdlet, które są dostępne tylko w trybie ARM hello.</span><span class="sxs-lookup"><span data-stu-id="c47fe-220">hello following are hello new cmdlets that are only available in hello ARM mode.</span></span> 

<span data-ttu-id="c47fe-221">**Akcja skryptu pokrewnych poleceń cmdlet:**</span><span class="sxs-lookup"><span data-stu-id="c47fe-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="c47fe-222">**Get-AzureRmHDInsightPersistedScriptAction**: hello pobiera utrwalone akcji skryptu dla klastra i wyświetla je w porządku chronologicznym lub pobiera szczegóły dla akcji utrwalonych skryptów określony.</span><span class="sxs-lookup"><span data-stu-id="c47fe-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets hello persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="c47fe-223">**Get-AzureRmHDInsightScriptActionHistory**: pobiera historii akcji skryptu hello klastra i wyświetla go w odwrotnej kolejności chronologicznej lub pobiera szczegóły akcji wcześniej wykonanie skryptu.</span><span class="sxs-lookup"><span data-stu-id="c47fe-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets hello script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="c47fe-224">**Usuń AzureRmHDInsightPersistedScriptAction**: usuwa akcji utrwalonego skryptu z klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c47fe-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="c47fe-225">**Zestaw AzureRmHDInsightPersistedScriptAction**: ustawia toobe akcji skryptu wcześniej wykonanych akcji utrwalonego skryptu.</span><span class="sxs-lookup"><span data-stu-id="c47fe-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action toobe a persisted script action.</span></span>
* <span data-ttu-id="c47fe-226">**Przedstawia AzureRmHDInsightScriptAction**: przesyła nowy klaster Azure HDInsight tooan akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="c47fe-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action tooan Azure HDInsight cluster.</span></span> 

<span data-ttu-id="c47fe-227">Użycie dodatkowych informacji, zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c47fe-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="c47fe-228">**Tożsamość Clsuter pokrewnych poleceń cmdlet:**</span><span class="sxs-lookup"><span data-stu-id="c47fe-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="c47fe-229">**Dodaj AzureRmHDInsightClusterIdentity**: dodaje obiekt konfiguracji klastra tożsamości tooa klastra, dzięki czemu hello klastra usługi HDInsight mogą uzyskiwać dostęp do usługi Azure Data Lake magazynów.</span><span class="sxs-lookup"><span data-stu-id="c47fe-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity tooa cluster configuration object so that hello HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="c47fe-230">Zobacz [tworzenia klastra usługi HDInsight z Data Lake Store za pomocą programu Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c47fe-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="c47fe-231">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c47fe-231">Examples</span></span>
<span data-ttu-id="c47fe-232">**Tworzenie klastra**</span><span class="sxs-lookup"><span data-stu-id="c47fe-232">**Create cluster**</span></span>

<span data-ttu-id="c47fe-233">Polecenie stary (ASM):</span><span class="sxs-lookup"><span data-stu-id="c47fe-233">Old command (ASM):</span></span> 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

<span data-ttu-id="c47fe-234">Nowe polecenie (ARM):</span><span class="sxs-lookup"><span data-stu-id="c47fe-234">New command (ARM):</span></span>

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


<span data-ttu-id="c47fe-235">**Usuwanie klastra**</span><span class="sxs-lookup"><span data-stu-id="c47fe-235">**Delete cluster**</span></span>

<span data-ttu-id="c47fe-236">Polecenie stary (ASM):</span><span class="sxs-lookup"><span data-stu-id="c47fe-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="c47fe-237">Nowe polecenie (ARM):</span><span class="sxs-lookup"><span data-stu-id="c47fe-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="c47fe-238">**Klaster listą**</span><span class="sxs-lookup"><span data-stu-id="c47fe-238">**List cluster**</span></span>

<span data-ttu-id="c47fe-239">Polecenie stary (ASM):</span><span class="sxs-lookup"><span data-stu-id="c47fe-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="c47fe-240">Nowe polecenie (ARM):</span><span class="sxs-lookup"><span data-stu-id="c47fe-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="c47fe-241">**Pokaż klastra**</span><span class="sxs-lookup"><span data-stu-id="c47fe-241">**Show cluster**</span></span>

<span data-ttu-id="c47fe-242">Polecenie stary (ASM):</span><span class="sxs-lookup"><span data-stu-id="c47fe-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="c47fe-243">Nowe polecenie (ARM):</span><span class="sxs-lookup"><span data-stu-id="c47fe-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="c47fe-244">Inne przykłady</span><span class="sxs-lookup"><span data-stu-id="c47fe-244">Other samples</span></span>
* [<span data-ttu-id="c47fe-245">Tworzenie klastrów usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="c47fe-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="c47fe-246">Przesyłania zadań Hive</span><span class="sxs-lookup"><span data-stu-id="c47fe-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="c47fe-247">Przesyłanie zadań Pig</span><span class="sxs-lookup"><span data-stu-id="c47fe-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="c47fe-248">Przesyłanie zadań Sqoop</span><span class="sxs-lookup"><span data-stu-id="c47fe-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="c47fe-249">Migrowanie toohello opartego na architekturze ARM HDInsight zestawu SDK .NET</span><span class="sxs-lookup"><span data-stu-id="c47fe-249">Migrating toohello ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="c47fe-250">Witaj, na podstawie zarządzania usługą Azure [zestawu .NET SDK usługi HDInsight (ASM)](https://msdn.microsoft.com/library/azure/mt416619.aspx) jest już przestarzały.</span><span class="sxs-lookup"><span data-stu-id="c47fe-250">hello Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="c47fe-251">Są zachęcani toouse hello na podstawie zarządzania zasobami Azure [zestawu .NET SDK usługi HDInsight (ARM)](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="c47fe-251">You are encouraged toouse hello Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="c47fe-252">Witaj następujące pakiety usługi HDInsight opartych na funkcji ASM są przestarzałe.</span><span class="sxs-lookup"><span data-stu-id="c47fe-252">hello following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="c47fe-253">Ta sekcja zawiera wskaźniki toomore informacje na temat tooperform niektórych zadań z wykorzystaniem hello opartego na architekturze ARM zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="c47fe-253">This section provides pointers toomore information on how tooperform certain tasks using hello ARM-based SDK.</span></span>

| <span data-ttu-id="c47fe-254">Jak... przy użyciu hello SDK HDInsight oparte na usłudze ARM</span><span class="sxs-lookup"><span data-stu-id="c47fe-254">How to... using hello ARM-based HDInsight SDK</span></span> | <span data-ttu-id="c47fe-255">Linki</span><span class="sxs-lookup"><span data-stu-id="c47fe-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="c47fe-256">Tworzenie klastrów usługi HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="c47fe-257">Zobacz [Tworzenie klastrów usługi HDInsight przy użyciu zestawu .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="c47fe-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="c47fe-258">Dostosowywanie klastra przy użyciu akcji skryptu przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="c47fe-259">Zobacz [dostosować HDInsight Linux klastrów za pomocą akcji skryptu](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="c47fe-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="c47fe-260">Uwierzytelniania aplikacji interaktywnego przy użyciu usługi Azure Active Directory przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="c47fe-261">Zobacz [uruchamianie zapytań Hive przy użyciu zestawu .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="c47fe-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="c47fe-262">fragment kodu Hello w tym artykule używa hello podejście uwierzytelnianie interakcyjne.</span><span class="sxs-lookup"><span data-stu-id="c47fe-262">hello code snippet in this article uses hello interactive authentication approach.</span></span> |
| <span data-ttu-id="c47fe-263">Uwierzytelniania aplikacji nieinteraktywnie przy użyciu usługi Azure Active Directory przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="c47fe-264">Zobacz [utworzyć nieinterakcyjnych aplikacji dla usługi HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="c47fe-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="c47fe-265">Przesłać zadania technologii Hive, przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="c47fe-266">Zobacz [Hive przesyłania zadań](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="c47fe-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="c47fe-267">Przesłać zadania programu Pig przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="c47fe-268">Zobacz [Pig przesyłania zadań](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="c47fe-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="c47fe-269">Prześlij zadanie Sqoop przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="c47fe-270">Zobacz [Sqoop przesyłania zadań](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="c47fe-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="c47fe-271">Lista klastrów usługi HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="c47fe-272">Zobacz [klastrów usługi HDInsight listy](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="c47fe-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="c47fe-273">Skalowanie klastrów usługi HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="c47fe-274">Zobacz [klastrów usługi HDInsight skali](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="c47fe-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="c47fe-275">Klastry tooHDInsight dostępu do przydzielenia/odwołania przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-275">Grant/revoke access tooHDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="c47fe-276">Zobacz [Grant/revoke dostępu tooHDInsight klastrów](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="c47fe-276">See [Grant/revoke access tooHDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="c47fe-277">Zaktualizuj poświadczenia użytkownika HTTP dla klastrów usługi HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="c47fe-278">Zobacz [HTTP aktualizacji poświadczeń użytkownika do klastrów usługi HDInsight](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="c47fe-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="c47fe-279">Znajdź hello domyślne konto magazynu dla klastrów usługi HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-279">Find hello default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="c47fe-280">Zobacz [znaleźć hello domyślne konto magazynu dla klastrów usługi HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="c47fe-280">See [Find hello default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="c47fe-281">Usuwać klastry usługi HDInsight przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c47fe-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="c47fe-282">Zobacz [klastrów HDInsight usunąć](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="c47fe-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="c47fe-283">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c47fe-283">Examples</span></span>
<span data-ttu-id="c47fe-284">Poniżej przedstawiono kilka przykładów w sposób operacja jest wykonywane przy użyciu hello ASM na podstawie zestawu SDK i fragment kodu równoważne hello na powitania opartego na architekturze ARM zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="c47fe-284">Following are some examples on how an operation is performed using hello ASM-based SDK and hello equivalent code snippet for hello ARM-based SDK.</span></span>

<span data-ttu-id="c47fe-285">**Tworzenie klienta CRUD klastra**</span><span class="sxs-lookup"><span data-stu-id="c47fe-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="c47fe-286">Polecenie stary (ASM)</span><span class="sxs-lookup"><span data-stu-id="c47fe-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="c47fe-287">Nowe polecenie (ARM) (autoryzacji głównej usługi)</span><span class="sxs-lookup"><span data-stu-id="c47fe-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="c47fe-288">Nowe polecenie (ARM) (Autoryzacja użytkownika)</span><span class="sxs-lookup"><span data-stu-id="c47fe-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="c47fe-289">**Tworzenie klastra**</span><span class="sxs-lookup"><span data-stu-id="c47fe-289">**Creating a cluster**</span></span>

* <span data-ttu-id="c47fe-290">Polecenie stary (ASM)</span><span class="sxs-lookup"><span data-stu-id="c47fe-290">Old command (ASM)</span></span>
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* <span data-ttu-id="c47fe-291">Nowe polecenie (ARM)</span><span class="sxs-lookup"><span data-stu-id="c47fe-291">New command (ARM)</span></span>
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

<span data-ttu-id="c47fe-292">**Włączanie dostępu HTTP**</span><span class="sxs-lookup"><span data-stu-id="c47fe-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="c47fe-293">Polecenie stary (ASM)</span><span class="sxs-lookup"><span data-stu-id="c47fe-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="c47fe-294">Nowe polecenie (ARM)</span><span class="sxs-lookup"><span data-stu-id="c47fe-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="c47fe-295">**Usuwanie klastra**</span><span class="sxs-lookup"><span data-stu-id="c47fe-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="c47fe-296">Polecenie stary (ASM)</span><span class="sxs-lookup"><span data-stu-id="c47fe-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="c47fe-297">Nowe polecenie (ARM)</span><span class="sxs-lookup"><span data-stu-id="c47fe-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

