---
title: "aaaUse oparte na czasie Hadoop Oozie coordinator w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj oparte na czasie koordynatora Hadoop Oozie w usłudze HDInsight, Usługa danych big data. Dowiedz się, jak toodefine Oozie przepływów pracy i koordynatorami i przesyłanie zadań."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a><span data-ttu-id="b2733-104">Używanie na podstawie czasu Oozie coordinator z platformą Hadoop w HDInsight toodefine w przepływach pracy oraz koordynować zadania</span><span class="sxs-lookup"><span data-stu-id="b2733-104">Use time-based Oozie coordinator with Hadoop in HDInsight toodefine workflows and coordinate jobs</span></span>
<span data-ttu-id="b2733-105">W tym artykule dowiesz się, jak toodefine przepływów pracy i koordynatorami i jak tootrigger hello koordynator zadań, na podstawie czasu.</span><span class="sxs-lookup"><span data-stu-id="b2733-105">In this article, you'll learn how toodefine workflows and coordinators, and how tootrigger hello coordinator jobs, based on time.</span></span> <span data-ttu-id="b2733-106">Jest przydatne toogo za pośrednictwem [Oozie użycia z usługą HDInsight] [ hdinsight-use-oozie] przed przeczytaniem tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="b2733-106">It is helpful toogo through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="b2733-107">Ponadto tooOozie, można również zaplanować zadania przy użyciu fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="b2733-107">In addition tooOozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="b2733-108">toolearn fabryki danych Azure, zobacz [Use Pig i Hive z fabryką danych](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b2733-108">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b2733-109">W tym artykule wymaga klastra usługi HDInsight opartej na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="b2733-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="b2733-110">Dla informacji o korzystaniu z Oozie, w tym zadania na podstawie czasu, w klastrze opartych na systemie Linux, zobacz [Oozie Użyj Hadoop toodefine i Uruchom przepływ pracy na HDInsight opartych na systemie Linux](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="b2733-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="b2733-111">Co to jest Oozie</span><span class="sxs-lookup"><span data-stu-id="b2733-111">What is Oozie</span></span>
<span data-ttu-id="b2733-112">Apache Oozie to system koordynacji/przepływu pracy, który zarządza zadaniami na platformie Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b2733-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="b2733-113">Jest zintegrowany z hello stosem platformy Hadoop i obsługuje zadania platformy Hadoop dla Apache MapReduce, Apache Pig Apache Hive i Apache Sqoop.</span><span class="sxs-lookup"><span data-stu-id="b2733-113">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="b2733-114">Można także używane tooschedule zadania, które są określone tooa systemu, np. programów Java lub skryptów powłoki.</span><span class="sxs-lookup"><span data-stu-id="b2733-114">It can also be used tooschedule jobs that are specific tooa system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="b2733-115">Witaj poniższy obraz przedstawia hello przepływu pracy, który będzie implementowany:</span><span class="sxs-lookup"><span data-stu-id="b2733-115">hello following image shows hello workflow you will implement:</span></span>

![Diagram przepływu pracy][img-workflow-diagram]

<span data-ttu-id="b2733-117">Hello przepływ pracy zawiera dwa działania:</span><span class="sxs-lookup"><span data-stu-id="b2733-117">hello workflow contains two actions:</span></span>

1. <span data-ttu-id="b2733-118">Akcja Hive uruchamia hello toocount skrypt HiveQL wystąpień poszczególnych typów poziom dziennika w pliku dziennika log4j.</span><span class="sxs-lookup"><span data-stu-id="b2733-118">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="b2733-119">Każdy dziennik log4j składa się z linii pola zawiera [poziom dziennika] pola tooshow hello typu i hello ważność, na przykład:</span><span class="sxs-lookup"><span data-stu-id="b2733-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field tooshow hello type and hello severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="b2733-120">dane wyjściowe skryptu Hive Hello jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="b2733-120">hello Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="b2733-121">Aby uzyskać więcej informacji na temat programu Hive, zobacz temat [Use Hive with HDInsight][hdinsight-use-hive] (Korzystanie z programu Hive z usługą HDInsight).</span><span class="sxs-lookup"><span data-stu-id="b2733-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="b2733-122">Akcja Sqoop eksportuje hello HiveQL akcji dane wyjściowe tooa tabeli w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="b2733-122">A Sqoop action exports hello HiveQL action output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="b2733-123">Aby uzyskać więcej informacji o Sqoop, zobacz [Sqoop użycia z usługą HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="b2733-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="b2733-124">Obsługiwane wersje Oozie w klastrach HDInsight, zobacz [nowości w wersjach klastra hello dostarczanych z usługą HDInsight?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="b2733-124">For supported Oozie versions on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="b2733-125">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b2733-125">Prerequisites</span></span>
<span data-ttu-id="b2733-126">Przed rozpoczęciem tego samouczka wymagane są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="b2733-126">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="b2733-127">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b2733-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b2733-128">Obsługa środowiska Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i zostanie usunięta z dniem 1 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="b2733-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="b2733-129">Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b2733-129">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="b2733-130">Wykonaj kroki hello [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello najnowszą wersję programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2733-130">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="b2733-131">Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b2733-131">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="b2733-132">**Klaster usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b2733-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="b2733-133">Aby uzyskać informacje dotyczące tworzenia klastra usługi HDInsight, zobacz [Tworzenie klastrów usługi HDInsight][hdinsight-provision], lub [Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="b2733-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="b2733-134">Konieczne będzie powitania po toogo danych samouczkiem hello:</span><span class="sxs-lookup"><span data-stu-id="b2733-134">You will need hello following data toogo through hello tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="b2733-135">Właściwości klastra</span><span class="sxs-lookup"><span data-stu-id="b2733-135">Cluster property</span></span></th><th><span data-ttu-id="b2733-136">Nazwa zmiennej środowiska Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2733-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="b2733-137">Wartość</span><span class="sxs-lookup"><span data-stu-id="b2733-137">Value</span></span></th><th><span data-ttu-id="b2733-138">Opis</span><span class="sxs-lookup"><span data-stu-id="b2733-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="b2733-139">Nazwa klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2733-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="b2733-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="b2733-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="b2733-141">klaster usługi HDInsight Hello, na którym będzie uruchomiona w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b2733-141">hello HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="b2733-142">Nazwa użytkownika klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2733-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="b2733-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="b2733-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="b2733-144">Nazwa użytkownika klastra usługi HDInsight Hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-144">hello HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="b2733-145">Hasło użytkownika klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="b2733-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="b2733-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="b2733-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="b2733-147">Witaj hasło użytkownika klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2733-147">hello HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="b2733-148">Nazwa konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b2733-148">Azure storage account name</span></span></td><td><span data-ttu-id="b2733-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="b2733-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="b2733-150">Klaster usługi HDInsight toohello dostępne konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="b2733-150">An Azure Storage account available toohello HDInsight cluster.</span></span> <span data-ttu-id="b2733-151">W tym samouczku Użyj hello domyślne konto magazynu, które zostały określone podczas procesu udostępniania klastra hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-151">For this tutorial, use hello default storage account that you specified during hello cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="b2733-152">Nazwa kontenera obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b2733-152">Azure Blob container name</span></span></td><td><span data-ttu-id="b2733-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="b2733-153">$containerName</span></span></td><td></td><td><span data-ttu-id="b2733-154">Na przykład użyć hello kontenera magazynu obiektów Blob platformy Azure, służący do hello domyślny system plików klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2733-154">For this example, use hello Azure Blob storage container that is used for hello default HDInsight cluster file system.</span></span> <span data-ttu-id="b2733-155">Domyślnie ma takie same nazwy co klaster usługi HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-155">By default, it has hello same name as hello HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="b2733-156">
* **Baza danych Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="b2733-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="b2733-157">Należy skonfigurować reguły zapory dla hello bazy danych SQL server tooallow dostęp ze stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="b2733-157">You must configure a firewall rule for hello SQL Database server tooallow access from your workstation.</span></span> <span data-ttu-id="b2733-158">Aby uzyskać instrukcje dotyczące tworzenia bazy danych Azure SQL i konfigurowania zapory hello, zobacz [rozpocząć korzystanie z bazy danych Azure SQL] [bazadanychsql get-started].</span><span class="sxs-lookup"><span data-stu-id="b2733-158">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="b2733-159">Ten artykuł zawiera skrypt programu Windows PowerShell do tworzenia tabeli bazy danych Azure SQL hello potrzebne w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b2733-159">This article provides a Windows PowerShell script for creating hello Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="b2733-160">Właściwości bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="b2733-160">SQL database property</span></span></th><th><span data-ttu-id="b2733-161">Nazwa zmiennej środowiska Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2733-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="b2733-162">Wartość</span><span class="sxs-lookup"><span data-stu-id="b2733-162">Value</span></span></th><th><span data-ttu-id="b2733-163">Opis</span><span class="sxs-lookup"><span data-stu-id="b2733-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="b2733-164">Nazwa serwera bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="b2733-164">SQL database server name</span></span></td><td><span data-ttu-id="b2733-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="b2733-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="b2733-166">Witaj SQL bazy danych serwera toowhich Sqoop spowoduje wyeksportowanie danych.</span><span class="sxs-lookup"><span data-stu-id="b2733-166">hello SQL database server toowhich Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="b2733-167">Nazwa logowania bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="b2733-167">SQL database login name</span></span></td><td><span data-ttu-id="b2733-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="b2733-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="b2733-169">Nazwa logowania SQL Database.</span><span class="sxs-lookup"><span data-stu-id="b2733-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="b2733-170">Hasło nazwy logowania bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="b2733-170">SQL database login password</span></span></td><td><span data-ttu-id="b2733-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="b2733-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="b2733-172">Hasło nazwy logowania bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="b2733-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="b2733-173">Nazwa bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="b2733-173">SQL database name</span></span></td><td><span data-ttu-id="b2733-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="b2733-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="b2733-175">toowhich bazy danych Azure SQL Hello Sqoop spowoduje wyeksportowanie danych.</span><span class="sxs-lookup"><span data-stu-id="b2733-175">hello Azure SQL database toowhich Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="b2733-176">Domyślnie baza danych Azure SQL zezwala na połączenia z usługami Azure, takimi jak Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b2733-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="b2733-177">Wyłączenie tego ustawienia zapory, należy włączyć ją z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b2733-177">If this firewall setting is disabled, you must enable it from hello Azure Portal.</span></span> <span data-ttu-id="b2733-178">Aby uzyskać instrukcje dotyczące tworzenia bazy danych SQL i konfigurowania reguł zapory, zobacz [tworzenie i Konfigurowanie bazy danych SQL][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="b2733-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="b2733-179">Wypełnianie hello wartości w tabelach hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-179">Fill-in hello values in hello tables.</span></span> <span data-ttu-id="b2733-180">Jest przydatne w przypadku przechodzenia przez tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="b2733-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="b2733-181">Zdefiniuj Oozie przepływu pracy i hello powiązanych skrypt HiveQL</span><span class="sxs-lookup"><span data-stu-id="b2733-181">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="b2733-182">Oozie definicje przepływów pracy są zapisywane w hPDL (XML procesu definition language).</span><span class="sxs-lookup"><span data-stu-id="b2733-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="b2733-183">Witaj domyślną nazwą pliku przepływu pracy jest *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="b2733-183">hello default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="b2733-184">Będzie Zapisz lokalnie plik hello przepływu pracy, a następnie wdrożyć go toohello klastra usługi HDInsight przy użyciu programu Azure PowerShell w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="b2733-184">You will save hello workflow file locally, and then deploy it toohello HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="b2733-185">Witaj akcji gałęzi w przepływie pracy hello wywołuje skrypt HiveQL.</span><span class="sxs-lookup"><span data-stu-id="b2733-185">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="b2733-186">Ten plik skryptu zawiera trzy instrukcje HiveQL:</span><span class="sxs-lookup"><span data-stu-id="b2733-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="b2733-187">**Witaj instrukcji DROP TABLE** usuwa hello log4j tabelę programu Hive, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="b2733-187">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="b2733-188">**Instrukcja CREATE TABLE Hello** tworzy log4j gałęzi zewnętrznych tabeli, która wskazuje toohello lokalizację pliku dziennika narzędzia log4j hello;</span><span class="sxs-lookup"><span data-stu-id="b2733-188">**hello CREATE TABLE statement** creates a log4j Hive external table, which points toohello location of hello log4j log file;</span></span>
3. <span data-ttu-id="b2733-189">**Witaj lokalizację pliku dziennika narzędzia log4j hello**.</span><span class="sxs-lookup"><span data-stu-id="b2733-189">**hello location of hello log4j log file**.</span></span> <span data-ttu-id="b2733-190">Ogranicznik pola Hello ",".</span><span class="sxs-lookup"><span data-stu-id="b2733-190">hello field delimiter is ",".</span></span> <span data-ttu-id="b2733-191">Ogranicznik wiersza domyślne Hello jest "\n".</span><span class="sxs-lookup"><span data-stu-id="b2733-191">hello default line delimiter is "\n".</span></span> <span data-ttu-id="b2733-192">Gałąź tabeli zewnętrznej jest plik danych hello używane tooavoid usuwana z oryginalnej lokalizacji hello, w przypadku, gdy chcesz przepływu pracy Oozie hello toorun wiele razy.</span><span class="sxs-lookup"><span data-stu-id="b2733-192">A Hive external table is used tooavoid hello data file being removed from hello original location, in case you want toorun hello Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="b2733-193">**Witaj instrukcji INSERT zastąpić** liczby wystąpień hello każdego typu poziomu dziennika z hello log4j tabelę programu Hive i zapisuje lokalizacji magazynu obiektów Blob platformy Azure tooan dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-193">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and it saves hello output tooan Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="b2733-194">Jest to znany problem ścieżki gałęzi.</span><span class="sxs-lookup"><span data-stu-id="b2733-194">There is a known Hive path issue.</span></span> <span data-ttu-id="b2733-195">Należy uruchomić na ten problem podczas przesyłania zadania Oozie.</span><span class="sxs-lookup"><span data-stu-id="b2733-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="b2733-196">Witaj instrukcje dla ustalania hello problemu można znaleźć na powitania TechNet Wiki: [HDInsight Hive błąd: toorename][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="b2733-196">hello instructions for fixing hello issue can be found on hello TechNet Wiki: [HDInsight Hive error: Unable toorename][technetwiki-hive-error].</span></span>

<span data-ttu-id="b2733-197">**wywoływane przez przepływ pracy hello toodefine hello HiveQL skryptu pliku toobe**</span><span class="sxs-lookup"><span data-stu-id="b2733-197">**toodefine hello HiveQL script file toobe called by hello workflow**</span></span>

1. <span data-ttu-id="b2733-198">Utwórz plik tekstowy z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="b2733-198">Create a text file with hello following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="b2733-199">Istnieją trzy zmienne używane w skrypcie hello:</span><span class="sxs-lookup"><span data-stu-id="b2733-199">There are three variables used in hello script:</span></span>

   * <span data-ttu-id="b2733-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="b2733-200">${hiveTableName}</span></span>
   * <span data-ttu-id="b2733-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="b2733-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="b2733-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="b2733-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="b2733-203">Plik definicji przepływu pracy Hello (workflow.xml w tym samouczku) przekazuje te wartości toothis skrypt HiveQL w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="b2733-203">hello workflow definition file (workflow.xml in this tutorial) will pass these values toothis HiveQL script at run time.</span></span>
2. <span data-ttu-id="b2733-204">Zapisz plik hello jako **C:\Tutorials\UseOozie\useooziewf.hql** przy użyciu kodowania ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="b2733-204">Save hello file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="b2733-205">(Użyj Notatnik, jeśli ta opcja nie są dostępne w edytorze tekstów). Ten plik skryptu będzie klastra usługi HDInsight toohello wdrożone później w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed toohello HDInsight cluster later in hello tutorial.</span></span>

<span data-ttu-id="b2733-206">**toodefine przepływu pracy**</span><span class="sxs-lookup"><span data-stu-id="b2733-206">**toodefine a workflow**</span></span>

1. <span data-ttu-id="b2733-207">Utwórz plik tekstowy z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="b2733-207">Create a text file with hello following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="b2733-208">Istnieją dwie akcje zdefiniowane w przepływie pracy hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-208">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="b2733-209">jest Hello start-tooaction *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="b2733-209">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="b2733-210">Jeśli akcja hello uruchamia *OK*, następnej akcji hello jest *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="b2733-210">If hello action runs *OK*, hello next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="b2733-211">Witaj RunHiveScript ma kilka zmiennych.</span><span class="sxs-lookup"><span data-stu-id="b2733-211">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="b2733-212">Po przesłaniu zadania Oozie hello ze stacji roboczej za pomocą programu Azure PowerShell, przechodzą hello wartości.</span><span class="sxs-lookup"><span data-stu-id="b2733-212">You will pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="b2733-213">Zmienne przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="b2733-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="b2733-214">Zmienne przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="b2733-214">Workflow variables</span></span></th><th><span data-ttu-id="b2733-215">Opis</span><span class="sxs-lookup"><span data-stu-id="b2733-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="b2733-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="b2733-216">${jobTracker}</span></span></td><td><span data-ttu-id="b2733-217">Określ adres URL śledzenia zadań Hadoop hello hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-217">Specify hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="b2733-218">Użyj <strong>jobtrackerhost:9010</strong> w usłudze HDInsight klastra w wersji 3.0 i 2.0.</span><span class="sxs-lookup"><span data-stu-id="b2733-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="b2733-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="b2733-219">${nameNode}</span></span></td><td><span data-ttu-id="b2733-220">Określ adres URL hello hello Hadoop nazwa węzła.</span><span class="sxs-lookup"><span data-stu-id="b2733-220">Specify hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="b2733-221">Użyj hello domyślnego pliku system wasb: / / adresu, na przykład <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="b2733-221">Use hello default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="b2733-222">${queueName}</span><span class="sxs-lookup"><span data-stu-id="b2733-222">${queueName}</span></span></td><td><span data-ttu-id="b2733-223">Określa, że nazwa kolejki hello hello zadania zostaną przesłane do.</span><span class="sxs-lookup"><span data-stu-id="b2733-223">Specifies hello queue name that hello job will be submitted to.</span></span> <span data-ttu-id="b2733-224">Użyj <strong>domyślne</strong>.</span><span class="sxs-lookup"><span data-stu-id="b2733-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="b2733-225">Zmienne akcji gałęzi</span><span class="sxs-lookup"><span data-stu-id="b2733-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="b2733-226">Gałąź zmiennej akcji</span><span class="sxs-lookup"><span data-stu-id="b2733-226">Hive action variable</span></span></th><th><span data-ttu-id="b2733-227">Opis</span><span class="sxs-lookup"><span data-stu-id="b2733-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="b2733-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="b2733-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="b2733-229">katalog źródłowy Hello hello polecenia Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="b2733-229">hello source directory for hello Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="b2733-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="b2733-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="b2733-231">folder wyjściowy Hello hello instrukcji INSERT zastąpić.</span><span class="sxs-lookup"><span data-stu-id="b2733-231">hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="b2733-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="b2733-232">${hiveTableName}</span></span></td><td><span data-ttu-id="b2733-233">Nazwa Hello hello Hive tabeli, która odwołuje się do plików danych log4j hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-233">hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="b2733-234">Zmienne akcji Sqoop</span><span class="sxs-lookup"><span data-stu-id="b2733-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="b2733-235">Sqoop zmiennej akcji</span><span class="sxs-lookup"><span data-stu-id="b2733-235">Sqoop action variable</span></span></th><th><span data-ttu-id="b2733-236">Opis</span><span class="sxs-lookup"><span data-stu-id="b2733-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="b2733-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="b2733-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="b2733-238">Parametry połączenia bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="b2733-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="b2733-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="b2733-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="b2733-240">Witaj danych hello toowhere z tabeli bazy danych Azure SQL zostaną wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="b2733-240">hello Azure SQL database table toowhere hello data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="b2733-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="b2733-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="b2733-242">folder wyjściowy Hello hello Hive Wstaw zastąpić instrukcji.</span><span class="sxs-lookup"><span data-stu-id="b2733-242">hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="b2733-243">Jest to hello tego samego folderu eksportu Sqoop hello (export-dir).</span><span class="sxs-lookup"><span data-stu-id="b2733-243">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="b2733-244">Aby uzyskać więcej informacji o przepływie pracy Oozie i przy użyciu hello przepływu pracy akcji, zobacz [dokumentację Apache Oozie 4.0] [ apache-oozie-400] (dla usługi HDInsight klastra w wersji 3.0) lub [Apache Oozie 3.3.2 Dokumentacja] [ apache-oozie-332] (dla usługi HDInsight klastra w wersji 2.1).</span><span class="sxs-lookup"><span data-stu-id="b2733-244">For more information about Oozie workflow and using hello workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="b2733-245">Zapisz plik hello jako **C:\Tutorials\UseOozie\workflow.xml** przy użyciu kodowania ANSI (ASCII).</span><span class="sxs-lookup"><span data-stu-id="b2733-245">Save hello file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="b2733-246">(Użyj Notatnik, jeśli ta opcja nie są dostępne w edytorze tekstów).</span><span class="sxs-lookup"><span data-stu-id="b2733-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="b2733-247">**Koordynator toodefine**</span><span class="sxs-lookup"><span data-stu-id="b2733-247">**toodefine coordinator**</span></span>

1. <span data-ttu-id="b2733-248">Utwórz plik tekstowy z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="b2733-248">Create a text file with hello following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="b2733-249">Istnieje pięć zmienne używane w pliku definicji hello:</span><span class="sxs-lookup"><span data-stu-id="b2733-249">There are five variables used in hello definition file:</span></span>

   | <span data-ttu-id="b2733-250">Zmienna</span><span class="sxs-lookup"><span data-stu-id="b2733-250">Variable</span></span> | <span data-ttu-id="b2733-251">Opis</span><span class="sxs-lookup"><span data-stu-id="b2733-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="b2733-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="b2733-252">${coordFrequency}</span></span> |<span data-ttu-id="b2733-253">Czas wstrzymania zadania.</span><span class="sxs-lookup"><span data-stu-id="b2733-253">Job pause time.</span></span> <span data-ttu-id="b2733-254">Częstotliwość zawsze jest wyrażone w minutach.</span><span class="sxs-lookup"><span data-stu-id="b2733-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="b2733-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="b2733-255">${coordStart}</span></span> |<span data-ttu-id="b2733-256">Godzina rozpoczęcia zadania.</span><span class="sxs-lookup"><span data-stu-id="b2733-256">Job start time.</span></span> |
   | <span data-ttu-id="b2733-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="b2733-257">${coordEnd}</span></span> |<span data-ttu-id="b2733-258">Godzina zakończenia zadania.</span><span class="sxs-lookup"><span data-stu-id="b2733-258">Job end time.</span></span> |
   | <span data-ttu-id="b2733-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="b2733-259">${coordTimezone}</span></span> |<span data-ttu-id="b2733-260">Oozie przetwarza koordynator zadań w stałej strefy czasowej z nie czasu letniego (zazwyczaj reprezentowany przy użyciu czasu UTC).</span><span class="sxs-lookup"><span data-stu-id="b2733-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="b2733-261">Ta strefa czasowa jest określane jako hello "Oozie przetwarzania strefy czasowej."</span><span class="sxs-lookup"><span data-stu-id="b2733-261">This time zone is referred as hello "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="b2733-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="b2733-262">${wfPath}</span></span> |<span data-ttu-id="b2733-263">Ścieżka Hello hello workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="b2733-263">hello path for hello workflow.xml.</span></span>  <span data-ttu-id="b2733-264">Jeśli nazwa pliku hello przepływu pracy nie jest hello domyślnej nazwy pliku (workflow.xml), należy ją określić.</span><span class="sxs-lookup"><span data-stu-id="b2733-264">If hello workflow file name is not hello default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="b2733-265">Zapisz plik hello jako **C:\Tutorials\UseOozie\coordinator.xml** przy użyciu kodowania ANSI (ASCII) hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-265">Save hello file as **C:\Tutorials\UseOozie\coordinator.xml** by using hello ANSI (ASCII) encoding.</span></span> <span data-ttu-id="b2733-266">(Użyj Notatnik, jeśli ta opcja nie są dostępne w edytorze tekstów).</span><span class="sxs-lookup"><span data-stu-id="b2733-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a><span data-ttu-id="b2733-267">Wdrażanie projektu Oozie hello i przygotowania samouczka hello</span><span class="sxs-lookup"><span data-stu-id="b2733-267">Deploy hello Oozie project and prepare hello tutorial</span></span>
<span data-ttu-id="b2733-268">Zostanie uruchomiony programu Azure PowerShell skryptu tooperform hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="b2733-268">You will run an Azure PowerShell script tooperform hello following:</span></span>

* <span data-ttu-id="b2733-269">Kopiuj hello magazynu obiektów Blob tooAzure skryptu (useoozie.hql) HiveQL, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="b2733-269">Copy hello HiveQL script (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="b2733-270">Skopiuj workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="b2733-270">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="b2733-271">Skopiuj coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="b2733-271">Copy coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="b2733-272">Plik danych hello kopiowania (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="b2733-272">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="b2733-273">Tworzenie tabeli bazy danych Azure SQL do przechowywania danych eksportu Sqoop.</span><span class="sxs-lookup"><span data-stu-id="b2733-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="b2733-274">Nazwa tabeli Hello jest *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="b2733-274">hello table name is *log4jLogCount*.</span></span>

<span data-ttu-id="b2733-275">**Informacje magazynie usługi HDInsight**</span><span class="sxs-lookup"><span data-stu-id="b2733-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="b2733-276">HDInsight używa magazynu obiektów Blob platformy Azure do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="b2733-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="b2733-277">wasb: / / to implementacja firmy Microsoft hello Hadoop distributed file system (HDFS) w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b2733-277">wasb:// is Microsoft's implementation of hello Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="b2733-278">Aby uzyskać więcej informacji, zobacz [magazynu obiektów Blob Azure użycia z usługą HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="b2733-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="b2733-279">Podczas obsługi administracyjnej klastra usługi HDInsight, konta magazynu obiektów Blob platformy Azure i w określonym kontenerze z tego konta zostaje wyznaczony jako hello domyślnego systemu plików, podobnie jak w systemie plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="b2733-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as hello default file system, like in HDFS.</span></span> <span data-ttu-id="b2733-280">Ponadto toothis konta magazynu, można dodać dodatkowe konta magazynu z hello sam subskrypcji platformy Azure lub z różnych subskrypcji Azure, podczas procesu udostępniania hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-280">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or from different Azure subscriptions during hello provisioning process.</span></span> <span data-ttu-id="b2733-281">Aby uzyskać instrukcje dotyczące dodawania dodatkowych kont magazynu, zobacz [Obsługa administracyjna klastrów HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="b2733-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="b2733-282">skrypt programu Azure PowerShell hello toosimplify używany w tym samouczku, wszystkie pliki są przechowywane w kontenerze systemu plików domyślne hello hello znajdujący się w */samouczki/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="b2733-282">toosimplify hello Azure PowerShell script used in this tutorial, all of hello files are stored in hello default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="b2733-283">Domyślnie ten kontener ma takie same nazwy jak nazwa klastra usługi HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-283">By default, this container has hello same name as hello HDInsight cluster name.</span></span>
<span data-ttu-id="b2733-284">Składnia Hello jest następująca:</span><span class="sxs-lookup"><span data-stu-id="b2733-284">hello syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="b2733-285">Tylko hello *wasb: / /* składni jest obsługiwane w klastrze usługi HDInsight w wersji 3.0.</span><span class="sxs-lookup"><span data-stu-id="b2733-285">Only hello *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="b2733-286">Witaj starsze *asv: / /* składnia jest obsługiwana w HDInsight 2.1 i 1.6 klastrów, ale nie jest obsługiwana w klastrach HDInsight 3.0.</span><span class="sxs-lookup"><span data-stu-id="b2733-286">hello older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="b2733-287">Witaj wasb: / / ścieżka jest ścieżką wirtualną.</span><span class="sxs-lookup"><span data-stu-id="b2733-287">hello wasb:// path is a virtual path.</span></span> <span data-ttu-id="b2733-288">Aby uzyskać więcej informacji, zobacz [magazynu obiektów Blob Azure użycia z usługą HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="b2733-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="b2733-289">Plik, który jest przechowywany w kontenerze systemu plików domyślne hello jest możliwy z usługi HDInsight przy użyciu dowolnej z hello następujące identyfikatory URI (na przykład używam programu workflow.xml):</span><span class="sxs-lookup"><span data-stu-id="b2733-289">A file that is stored in hello default file system container can be accessed from HDInsight by using any of hello following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="b2733-290">Jeśli chcesz tooaccess hello pliku bezpośrednio z konta magazynu hello hello nazwa obiektu blob dla pliku hello jest:</span><span class="sxs-lookup"><span data-stu-id="b2733-290">If you want tooaccess hello file directly from hello storage account, hello blob name for hello file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="b2733-291">**Zrozumienie tabele programu Hive wewnętrznych i zewnętrznych**</span><span class="sxs-lookup"><span data-stu-id="b2733-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="b2733-292">Istnieje kilka rzeczy, o których należy tooknow o tabele programu Hive wewnętrznych i zewnętrznych:</span><span class="sxs-lookup"><span data-stu-id="b2733-292">There are a few things you need tooknow about Hive internal and external tables:</span></span>

* <span data-ttu-id="b2733-293">Witaj polecenia CREATE TABLE tworzy wewnętrznej tabeli, znanej także jako zarządzane tabeli.</span><span class="sxs-lookup"><span data-stu-id="b2733-293">hello CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="b2733-294">plik danych Hello musi znajdować się w kontenerze domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-294">hello data file must be located in hello default container.</span></span>
* <span data-ttu-id="b2733-295">Witaj polecenia CREATE TABLE przenosi dane hello plikutoohello/hive/magazynu/<TableName> folderu w hello domyślnego kontenera.</span><span class="sxs-lookup"><span data-stu-id="b2733-295">hello CREATE TABLE command moves hello data file toohello /hive/warehouse/<TableName> folder in hello default container.</span></span>
* <span data-ttu-id="b2733-296">Witaj polecenia CREATE TABLE zewnętrznych tworzy tabelę zewnętrzną.</span><span class="sxs-lookup"><span data-stu-id="b2733-296">hello CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="b2733-297">plik danych Hello może znajdować się poza hello domyślnego kontenera.</span><span class="sxs-lookup"><span data-stu-id="b2733-297">hello data file can be located outside hello default container.</span></span>
* <span data-ttu-id="b2733-298">Hello polecenia CREATE TABLE zewnętrznych nie powoduje przeniesienia hello pliku danych.</span><span class="sxs-lookup"><span data-stu-id="b2733-298">hello CREATE EXTERNAL TABLE command does not move hello data file.</span></span>
* <span data-ttu-id="b2733-299">Witaj polecenia CREATE TABLE zewnętrznych nie zezwala na wszystkie podfoldery w folderze hello, która została określona w klauzuli lokalizacji hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-299">hello CREATE EXTERNAL TABLE command doesn't allow any subfolders under hello folder that is specified in hello LOCATION clause.</span></span> <span data-ttu-id="b2733-300">Jest to powód hello Dlaczego samouczek hello tworzy kopię pliku sample.log hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-300">This is hello reason why hello tutorial makes a copy of hello sample.log file.</span></span>

<span data-ttu-id="b2733-301">Aby uzyskać więcej informacji, zobacz [HDInsight: Hive wewnętrznych i zewnętrznych wprowadzenie tabel][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="b2733-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="b2733-302">**Samouczek hello tooprepare**</span><span class="sxs-lookup"><span data-stu-id="b2733-302">**tooprepare hello tutorial**</span></span>

1. <span data-ttu-id="b2733-303">Otwórz hello programu Windows PowerShell ISE (na ekranie powitania Start systemu Windows 8, wpisz **PowerShell_ISE**, a następnie kliknij przycisk **programu Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="b2733-303">Open hello Windows PowerShell ISE (in hello Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="b2733-304">Aby uzyskać więcej informacji, zobacz [programu Windows PowerShell Start w systemie Windows 8 i Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="b2733-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="b2733-305">W dolnym okienku hello Uruchom hello następujące polecenia tooconnect tooyour subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="b2733-305">In hello bottom pane, run hello following command tooconnect tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="b2733-306">Użytkownik będzie tooenter zostanie wyświetlony monit o poświadczenia konta Azure.</span><span class="sxs-lookup"><span data-stu-id="b2733-306">You will be prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="b2733-307">Ta metoda dodawania połączenia subskrypcji wygaśnie, a po 12 godzinach, konieczne będzie polecenia cmdlet hello toorun ponownie.</span><span class="sxs-lookup"><span data-stu-id="b2733-307">This method of adding a subscription connection times out, and after 12 hours, you will have toorun hello cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b2733-308">Jeśli masz wiele subskrypcji platformy Azure i hello Domyślna subskrypcja nie jest hello z nich ma toouse, użyj hello <strong>AzureSubscription wybierz</strong> tooselect polecenia cmdlet subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b2733-308">If you have multiple Azure subscriptions and hello default subscription is not hello one you want toouse, use hello <strong>Select-AzureSubscription</strong> cmdlet tooselect a subscription.</span></span>

3. <span data-ttu-id="b2733-309">Skopiuj hello następującego skryptu w okienku skryptów hello, a następnie ustaw zmienne pierwszych sześciu hello:</span><span class="sxs-lookup"><span data-stu-id="b2733-309">Copy hello following script into hello script pane, and then set hello first six variables:</span></span>

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    <span data-ttu-id="b2733-310">Aby więcej opisy hello zmiennych, zobacz hello [wymagania wstępne](#prerequisites) sekcji, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b2733-310">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="b2733-311">Dołącz hello następującego skryptu toohello w okienku skryptów hello:</span><span class="sxs-lookup"><span data-stu-id="b2733-311">Append hello following toohello script in hello script pane:</span></span>

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="b2733-312">Kliknij przycisk **Uruchom skrypt** lub naciśnij klawisz **F5** toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="b2733-312">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="b2733-313">Witaj dane wyjściowe będą podobne do:</span><span class="sxs-lookup"><span data-stu-id="b2733-313">hello output will be similar to:</span></span>

    ![Dane wyjściowe przygotowania samouczka][img-preparation-output]

## <a name="run-hello-oozie-project"></a><span data-ttu-id="b2733-315">Uruchom projekt Oozie hello</span><span class="sxs-lookup"><span data-stu-id="b2733-315">Run hello Oozie project</span></span>
<span data-ttu-id="b2733-316">Program Azure PowerShell obecnie nie udostępnia żadnych poleceń cmdlet do definiowania Oozie zadań.</span><span class="sxs-lookup"><span data-stu-id="b2733-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="b2733-317">Można użyć hello **Invoke RestMethod** usług sieci web Oozie tooinvoke polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b2733-317">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="b2733-318">Interfejs API usług sieci web Oozie Hello jest JSON interfejsu API REST protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="b2733-318">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="b2733-319">Aby uzyskać więcej informacji o usługach sieci web Oozie hello interfejsu API, zobacz [dokumentację Apache Oozie 4.0] [ apache-oozie-400] (dla usługi HDInsight klastra w wersji 3.0) lub [dokumentację Apache Oozie 3.3.2] [ apache-oozie-332] (dla usługi HDInsight klastra w wersji 2.1).</span><span class="sxs-lookup"><span data-stu-id="b2733-319">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="b2733-320">**toosubmit Oozie zadania**</span><span class="sxs-lookup"><span data-stu-id="b2733-320">**toosubmit an Oozie job**</span></span>

1. <span data-ttu-id="b2733-321">Otwórz hello programu Windows PowerShell ISE (na ekranie Start systemu Windows 8, wpisz **PowerShell_ISE**, a następnie kliknij przycisk **programu Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="b2733-321">Open hello Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="b2733-322">Aby uzyskać więcej informacji, zobacz [programu Windows PowerShell Start w systemie Windows 8 i Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="b2733-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="b2733-323">Następujące hello kopii skryptu w okienku skryptów hello, a następnie zestaw hello zmienne najpierw czternastu (jednak pominąć **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="b2733-323">Copy hello following script into hello script pane, and then set hello first fourteen variables (however, skip **$storageUri**).</span></span>

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    <span data-ttu-id="b2733-324">Aby więcej opisy hello zmiennych, zobacz hello [wymagania wstępne](#prerequisites) sekcji, w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b2733-324">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="b2733-325">$coordstart i $coordend są uruchamianie przepływu pracy hello i godzina zakończenia.</span><span class="sxs-lookup"><span data-stu-id="b2733-325">$coordstart and $coordend are hello workflow starting and ending time.</span></span> <span data-ttu-id="b2733-326">toofind limit czasu UTC/GMT hello, wyszukaj "czas utc" na bing.com. Witaj $coordFrequency jest częstotliwość w minutach toorun hello w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="b2733-326">toofind out hello UTC/GMT time, search "utc time" on bing.com. hello $coordFrequency is how often in minutes you want toorun hello workflow.</span></span>
3. <span data-ttu-id="b2733-327">Dołącz powitania po toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="b2733-327">Append hello following toohello script.</span></span> <span data-ttu-id="b2733-328">Ta część definiuje ładunek Oozie hello:</span><span class="sxs-lookup"><span data-stu-id="b2733-328">This part defines hello Oozie payload:</span></span>

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > <span data-ttu-id="b2733-329">Witaj główną różnicą w porównaniu toohello przepływu pracy przesyłanie ładunku plik jest zmienna hello **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="b2733-329">hello major difference compared toohello workflow submission payload file is hello variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="b2733-330">Po przesłaniu zadania przepływu pracy, należy użyć **oozie.wf.application.path** zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="b2733-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="b2733-331">Dołącz powitania po toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="b2733-331">Append hello following toohello script.</span></span> <span data-ttu-id="b2733-332">Ta część sprawdza stan usługi sieci web Oozie hello:</span><span class="sxs-lookup"><span data-stu-id="b2733-332">This part checks hello Oozie web service status:</span></span>

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="b2733-333">Dołącz powitania po toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="b2733-333">Append hello following toohello script.</span></span> <span data-ttu-id="b2733-334">Ta część tworzy zadanie Oozie:</span><span class="sxs-lookup"><span data-stu-id="b2733-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="b2733-335">Po przesłaniu zadania przepływu pracy należy inne zadanie hello toostart wywołania sieci web usługi po utworzeniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-335">When you submit a workflow job, you must make another web service call toostart hello job after hello job is created.</span></span> <span data-ttu-id="b2733-336">W takim przypadku zadania koordynatora hello jest wyzwalany przez czas.</span><span class="sxs-lookup"><span data-stu-id="b2733-336">In this case, hello coordinator job is triggered by time.</span></span> <span data-ttu-id="b2733-337">zadanie Hello rozpocznie się automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b2733-337">hello job will start automatically.</span></span>

6. <span data-ttu-id="b2733-338">Dołącz powitania po toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="b2733-338">Append hello following toohello script.</span></span> <span data-ttu-id="b2733-339">Ta część sprawdza stan zadania Oozie hello:</span><span class="sxs-lookup"><span data-stu-id="b2733-339">This part checks hello Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. <span data-ttu-id="b2733-340">(Opcjonalnie) Dołącz powitania po toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="b2733-340">(Optional) Append hello following toohello script.</span></span>

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="b2733-341">Dołącz powitania po toohello skryptu:</span><span class="sxs-lookup"><span data-stu-id="b2733-341">Append hello following toohello script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="b2733-342">Usuń znaki # hello, jeśli chcesz, dodatkowe funkcje hello toorun.</span><span class="sxs-lookup"><span data-stu-id="b2733-342">Remove hello # signs if you want toorun hello additional functions.</span></span>
9. <span data-ttu-id="b2733-343">Jeśli z klastrem usługi HDinsight w wersji 2.1, zastąp "https://$clusterName.azurehdinsight.net:443/oozie/v2/" z "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span><span class="sxs-lookup"><span data-stu-id="b2733-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="b2733-344">Klaster usługi HDInsight w wersji 2.1 nie nie obsługuje wersji 2 hello usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="b2733-344">HDInsight cluster version 2.1 does not supports version 2 of hello web services.</span></span>
10. <span data-ttu-id="b2733-345">Kliknij przycisk **Uruchom skrypt** lub naciśnij klawisz **F5** toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="b2733-345">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="b2733-346">Witaj dane wyjściowe będą podobne do:</span><span class="sxs-lookup"><span data-stu-id="b2733-346">hello output will be similar to:</span></span>

     ![Samouczek uruchomienia przepływu pracy w danych wyjściowych][img-runworkflow-output]
11. <span data-ttu-id="b2733-348">Połącz tooyour bazy danych SQL toosee hello wyeksportowane dane.</span><span class="sxs-lookup"><span data-stu-id="b2733-348">Connect tooyour SQL Database toosee hello exported data.</span></span>

<span data-ttu-id="b2733-349">**Dziennik błędów programu toocheck hello zadania**</span><span class="sxs-lookup"><span data-stu-id="b2733-349">**toocheck hello job error log**</span></span>

<span data-ttu-id="b2733-350">tootroubleshoot przepływu pracy, plik dziennika Oozie hello można znaleźć w C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log z hello headnode klastra.</span><span class="sxs-lookup"><span data-stu-id="b2733-350">tootroubleshoot a workflow, hello Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from hello cluster headnode.</span></span> <span data-ttu-id="b2733-351">Aby uzyskać informacji na temat protokołu RDP, zobacz [administrowanie klastrów usługi HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="b2733-351">For information on RDP, see [Administering HDInsight clusters using hello Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="b2733-352">**Samouczek hello toorerun**</span><span class="sxs-lookup"><span data-stu-id="b2733-352">**toorerun hello tutorial**</span></span>

<span data-ttu-id="b2733-353">toorerun hello przepływu pracy, należy wykonać następujące zadania hello:</span><span class="sxs-lookup"><span data-stu-id="b2733-353">toorerun hello workflow, you must perform hello following tasks:</span></span>

* <span data-ttu-id="b2733-354">Usuń plik danych wyjściowych skryptu Hive hello.</span><span class="sxs-lookup"><span data-stu-id="b2733-354">Delete hello Hive script output file.</span></span>
* <span data-ttu-id="b2733-355">Usuń dane hello hello log4jLogsCount tabeli.</span><span class="sxs-lookup"><span data-stu-id="b2733-355">Delete hello data in hello log4jLogsCount table.</span></span>

<span data-ttu-id="b2733-356">Poniżej przedstawiono przykładowy skrypt programu Windows PowerShell, którego można używać:</span><span class="sxs-lookup"><span data-stu-id="b2733-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="b2733-357">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2733-357">Next steps</span></span>
<span data-ttu-id="b2733-358">W tym samouczku można przedstawiono sposób toodefine Oozie przepływu pracy i Oozie coordinator oraz jak toorun Oozie coordinator zadania przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2733-358">In this tutorial, you learned how toodefine an Oozie workflow and an Oozie coordinator, and how toorun an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="b2733-359">toolearn więcej, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="b2733-359">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="b2733-360">[Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="b2733-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="b2733-361">[Użyj magazynu obiektów Blob platformy Azure z usługą HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="b2733-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="b2733-362">[Administrowanie HDInsight przy użyciu programu Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="b2733-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="b2733-363">[Przekazywanie danych tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="b2733-363">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="b2733-364">[Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="b2733-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="b2733-365">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="b2733-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="b2733-366">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="b2733-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="b2733-367">[Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="b2733-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
