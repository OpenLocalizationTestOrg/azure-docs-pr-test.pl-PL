---
title: "aaaUse Hadoop Oozie w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Użyj Hadoop Oozie w usłudze HDInsight, Usługa danych big data. Dowiedz się, jak toodefine przepływ Oozie i przesłać zadanie Oozie."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 870098f0-f416-4491-9719-78994bf4a369
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 12d0cf1a01838ab0f4e699c384ce2fb18f85cbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-in-hdinsight"></a><span data-ttu-id="4278b-104">Użyj Oozie z Hadoop toodefine i uruchomić przepływ pracy w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="4278b-104">Use Oozie with Hadoop toodefine and run a workflow in HDInsight</span></span>
[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="4278b-105">Dowiedz się, jak toouse Apache Oozie toodefine przepływu pracy i uruchom hello przepływu pracy w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4278b-105">Learn how toouse Apache Oozie toodefine a workflow and run hello workflow on HDInsight.</span></span> <span data-ttu-id="4278b-106">toolearn o hello Oozie coordinator, zobacz [korzystanie z usługą HDInsight oparte na czasie Hadoop Oozie Coordinator][hdinsight-oozie-coordinator-time].</span><span class="sxs-lookup"><span data-stu-id="4278b-106">toolearn about hello Oozie coordinator, see [Use time-based Hadoop Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time].</span></span> <span data-ttu-id="4278b-107">toolearn fabryki danych Azure, zobacz [Use Pig i Hive z fabryką danych][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="4278b-107">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

<span data-ttu-id="4278b-108">Apache Oozie to system koordynacji/przepływu pracy, który zarządza zadaniami na platformie Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4278b-108">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="4278b-109">Jest zintegrowany z hello stosem platformy Hadoop i obsługuje zadania platformy Hadoop dla Apache MapReduce, Apache Pig Apache Hive i Apache Sqoop.</span><span class="sxs-lookup"><span data-stu-id="4278b-109">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="4278b-110">Można także używane tooschedule zadania, które są określone tooa systemu, np. programów Java lub skryptów powłoki.</span><span class="sxs-lookup"><span data-stu-id="4278b-110">It can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts.</span></span>

<span data-ttu-id="4278b-111">przepływ pracy Hello, który implementuje wykonując instrukcje hello w tym samouczku zawiera dwa działania:</span><span class="sxs-lookup"><span data-stu-id="4278b-111">hello workflow you implement by following hello instructions in this tutorial contains two actions:</span></span>

![Diagram przepływu pracy][img-workflow-diagram]

1. <span data-ttu-id="4278b-113">Akcja Hive uruchamia hello toocount skrypt HiveQL wystąpień poszczególnych typów poziom dziennika w pliku log4j.</span><span class="sxs-lookup"><span data-stu-id="4278b-113">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j file.</span></span> <span data-ttu-id="4278b-114">Każdy plik log4j składa się z linii pola zawiera pole [poziom dziennika] pokazujący hello typ i ważność hello, na przykład:</span><span class="sxs-lookup"><span data-stu-id="4278b-114">Each log4j file consists of a line of fields that contains a [LOG LEVEL] field that shows hello type and hello severity, for example:</span></span>
   
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
   
    <span data-ttu-id="4278b-115">dane wyjściowe skryptu Hive Hello jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="4278b-115">hello Hive script output is similar to:</span></span>
   
        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4
   
    <span data-ttu-id="4278b-116">Aby uzyskać więcej informacji na temat programu Hive, zobacz temat [Use Hive with HDInsight][hdinsight-use-hive] (Korzystanie z programu Hive z usługą HDInsight).</span><span class="sxs-lookup"><span data-stu-id="4278b-116">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="4278b-117">Akcja Sqoop eksportuje hello HiveQL dane wyjściowe tooa tabeli w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="4278b-117">A Sqoop action exports hello HiveQL output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="4278b-118">Aby uzyskać więcej informacji o Sqoop, zobacz [Hadoop Sqoop użycia z usługą HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="4278b-118">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="4278b-119">Obsługiwane wersje Oozie w klastrach HDInsight, zobacz [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="4278b-119">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="4278b-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4278b-120">Prerequisites</span></span>
<span data-ttu-id="4278b-121">Przed rozpoczęciem tego samouczka, musi mieć hello następującego elementu:</span><span class="sxs-lookup"><span data-stu-id="4278b-121">Before you begin this tutorial, you must have hello following item:</span></span>

* <span data-ttu-id="4278b-122">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="4278b-122">**A workstation with Azure PowerShell**.</span></span> 
  

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
  

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="4278b-123">Zdefiniuj Oozie przepływu pracy i hello powiązanych skrypt HiveQL</span><span class="sxs-lookup"><span data-stu-id="4278b-123">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="4278b-124">Oozie definicje przepływów pracy są zapisywane w hPDL (XML procesu Definition Language).</span><span class="sxs-lookup"><span data-stu-id="4278b-124">Oozie workflows definitions are written in hPDL (a XML Process Definition Language).</span></span> <span data-ttu-id="4278b-125">Witaj domyślną nazwą pliku przepływu pracy jest *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="4278b-125">hello default workflow file name is *workflow.xml*.</span></span> <span data-ttu-id="4278b-126">Witaj poniżej znajduje się plik przepływu pracy hello używanej w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="4278b-126">hello following is hello workflow file you use in this tutorial.</span></span>

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

<span data-ttu-id="4278b-127">Istnieją dwie akcje zdefiniowane w przepływie pracy hello.</span><span class="sxs-lookup"><span data-stu-id="4278b-127">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="4278b-128">jest Hello start-tooaction *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="4278b-128">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="4278b-129">Jeśli akcja hello zostanie wykonane pomyślnie, jest hello następnej akcji *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="4278b-129">If hello action runs successfully, hello next action is *RunSqoopExport*.</span></span>

<span data-ttu-id="4278b-130">Witaj RunHiveScript ma kilka zmiennych.</span><span class="sxs-lookup"><span data-stu-id="4278b-130">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="4278b-131">Możesz przekazać wartości powitania po przesłaniu zadania Oozie hello ze stacji roboczej za pomocą programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4278b-131">You pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

<table border = "1">
<tr><th><span data-ttu-id="4278b-132">Zmienne przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="4278b-132">Workflow variables</span></span></th><th><span data-ttu-id="4278b-133">Opis</span><span class="sxs-lookup"><span data-stu-id="4278b-133">Description</span></span></th></tr>
<tr><td><span data-ttu-id="4278b-134">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="4278b-134">${jobTracker}</span></span></td><td><span data-ttu-id="4278b-135">Określa adres URL śledzenia zadań Hadoop hello hello.</span><span class="sxs-lookup"><span data-stu-id="4278b-135">Specifies hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="4278b-136">Użyj <strong>jobtrackerhost:9010</strong> w usłudze HDInsight w wersji 3.0 i 2.1.</span><span class="sxs-lookup"><span data-stu-id="4278b-136">Use <strong>jobtrackerhost:9010</strong> in HDInsight version 3.0 and 2.1.</span></span></td></tr>
<tr><td><span data-ttu-id="4278b-137">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="4278b-137">${nameNode}</span></span></td><td><span data-ttu-id="4278b-138">Określa adres URL hello hello Hadoop nazwa węzła.</span><span class="sxs-lookup"><span data-stu-id="4278b-138">Specifies hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="4278b-139">Użyj hello domyślny adres systemu plików, na przykład <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="4278b-139">Use hello default file system address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
<tr><td><span data-ttu-id="4278b-140">${queueName}</span><span class="sxs-lookup"><span data-stu-id="4278b-140">${queueName}</span></span></td><td><span data-ttu-id="4278b-141">Określa, że nazwa kolejki hello hello zadania jest przesyłany do usługi.</span><span class="sxs-lookup"><span data-stu-id="4278b-141">Specifies hello queue name that hello job is submitted to.</span></span> <span data-ttu-id="4278b-142">Użyj hello <strong>domyślne</strong>.</span><span class="sxs-lookup"><span data-stu-id="4278b-142">Use hello <strong>default</strong>.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="4278b-143">Gałąź zmiennej akcji</span><span class="sxs-lookup"><span data-stu-id="4278b-143">Hive action variable</span></span></th><th><span data-ttu-id="4278b-144">Opis</span><span class="sxs-lookup"><span data-stu-id="4278b-144">Description</span></span></th></tr>
<tr><td><span data-ttu-id="4278b-145">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="4278b-145">${hiveDataFolder}</span></span></td><td><span data-ttu-id="4278b-146">Określa katalog źródłowy hello hello polecenia Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="4278b-146">Specifies hello source directory for hello Hive Create Table command.</span></span></td></tr>
<tr><td><span data-ttu-id="4278b-147">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="4278b-147">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="4278b-148">Określa folder wyjściowy hello hello instrukcji INSERT zastąpić.</span><span class="sxs-lookup"><span data-stu-id="4278b-148">Specifies hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
<tr><td><span data-ttu-id="4278b-149">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="4278b-149">${hiveTableName}</span></span></td><td><span data-ttu-id="4278b-150">Określa nazwę hello hello Hive tabeli, która odwołuje się do plików danych log4j hello.</span><span class="sxs-lookup"><span data-stu-id="4278b-150">Specifies hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="4278b-151">Sqoop zmiennej akcji</span><span class="sxs-lookup"><span data-stu-id="4278b-151">Sqoop action variable</span></span></th><th><span data-ttu-id="4278b-152">Opis</span><span class="sxs-lookup"><span data-stu-id="4278b-152">Description</span></span></th></tr>
<tr><td><span data-ttu-id="4278b-153">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="4278b-153">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="4278b-154">Określa parametry połączenia bazy danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="4278b-154">Specifies hello Azure SQL database connection string.</span></span></td></tr>
<tr><td><span data-ttu-id="4278b-155">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="4278b-155">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="4278b-156">Określa, gdzie hello dane są eksportowane do tabeli w bazie danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="4278b-156">Specifies hello Azure SQL database table where hello data is exported to.</span></span></td></tr>
<tr><td><span data-ttu-id="4278b-157">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="4278b-157">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="4278b-158">Określa folder wyjściowy hello hello Hive Wstaw zastąpić instrukcji.</span><span class="sxs-lookup"><span data-stu-id="4278b-158">Specifies hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="4278b-159">Jest to hello tego samego folderu eksportu Sqoop hello (export-dir).</span><span class="sxs-lookup"><span data-stu-id="4278b-159">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
</table>

<span data-ttu-id="4278b-160">Aby uzyskać więcej informacji o przepływie pracy Oozie i przy użyciu działań przepływu pracy, zobacz [dokumentację Apache Oozie 4.0] [ apache-oozie-400] (dla usługi HDInsight w wersji 3.0 lub nowszej) lub [dokumentację Apache Oozie 3.3.2] [ apache-oozie-332] (dla usługi HDInsight w wersji 2.1).</span><span class="sxs-lookup"><span data-stu-id="4278b-160">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="4278b-161">Witaj akcji gałęzi w przepływie pracy hello wywołuje skrypt HiveQL.</span><span class="sxs-lookup"><span data-stu-id="4278b-161">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="4278b-162">Ten plik skryptu zawiera trzy instrukcje HiveQL:</span><span class="sxs-lookup"><span data-stu-id="4278b-162">This script file contains three HiveQL statements:</span></span>

    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

1. <span data-ttu-id="4278b-163">**Witaj instrukcji DROP TABLE** usuwa hello log4j tabelę programu Hive, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="4278b-163">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="4278b-164">**Instrukcja CREATE TABLE Hello** tworzy log4j tabeli programu Hive zewnętrznych wskazujące toohello lokalizację pliku dziennika narzędzia log4j hello.</span><span class="sxs-lookup"><span data-stu-id="4278b-164">**hello CREATE TABLE statement** creates a log4j Hive external table that points toohello location of hello log4j log file.</span></span> <span data-ttu-id="4278b-165">Ogranicznik pola Hello ",".</span><span class="sxs-lookup"><span data-stu-id="4278b-165">hello field delimiter is ",".</span></span> <span data-ttu-id="4278b-166">Ogranicznik wiersza domyślne Hello jest "\n".</span><span class="sxs-lookup"><span data-stu-id="4278b-166">hello default line delimiter is "\n".</span></span> <span data-ttu-id="4278b-167">Gałąź tabeli zewnętrznej jest plik danych hello tooavoid używane są usunięte z oryginalnej lokalizacji hello, jeśli chcesz toorun hello Oozie w przepływie pracy, wiele razy.</span><span class="sxs-lookup"><span data-stu-id="4278b-167">A Hive external table is used tooavoid hello data file being removed from hello original location if you want toorun hello Oozie workflow multiple times.</span></span>
3. <span data-ttu-id="4278b-168">**Witaj instrukcji INSERT zastąpić** liczby wystąpień hello każdego typu poziomu dziennika z tabeli Hive log4j hello i zapisuje hello dane wyjściowe tooa blob w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4278b-168">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and saves hello output tooa blob in Azure Storage.</span></span>

<span data-ttu-id="4278b-169">Istnieją trzy zmienne używane w skrypcie hello:</span><span class="sxs-lookup"><span data-stu-id="4278b-169">There are three variables used in hello script:</span></span>

* <span data-ttu-id="4278b-170">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="4278b-170">${hiveTableName}</span></span>
* <span data-ttu-id="4278b-171">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="4278b-171">${hiveDataFolder}</span></span>
* <span data-ttu-id="4278b-172">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="4278b-172">${hiveOutputFolder}</span></span>

<span data-ttu-id="4278b-173">Plik definicji przepływu pracy Hello (workflow.xml w tym samouczku) przekazuje te wartości toothis skrypt HiveQL w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="4278b-173">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time.</span></span>

<span data-ttu-id="4278b-174">Zarówno hello plik przepływu pracy, jak i plik HiveQL hello są przechowywane w kontenerze obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="4278b-174">Both hello workflow file and hello HiveQL file are stored in a blob container.</span></span>  <span data-ttu-id="4278b-175">skrypt programu PowerShell, których używasz w dalszej części tego samouczka Hello kopiuje oba pliki toohello domyślne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="4278b-175">hello PowerShell script you use later in this tutorial copies both files toohello default Storage account.</span></span> 

## <a name="submit-oozie-jobs-using-powershell"></a><span data-ttu-id="4278b-176">Przesyłanie zadań Oozie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="4278b-176">Submit Oozie jobs using PowerShell</span></span>
<span data-ttu-id="4278b-177">Program Azure PowerShell obecnie nie udostępnia żadnych poleceń cmdlet do definiowania Oozie zadań.</span><span class="sxs-lookup"><span data-stu-id="4278b-177">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="4278b-178">Można użyć hello **Invoke RestMethod** usług sieci web Oozie tooinvoke polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4278b-178">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="4278b-179">Interfejs API usług sieci web Oozie Hello jest JSON interfejsu API REST protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="4278b-179">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="4278b-180">Aby uzyskać więcej informacji o usługach sieci web Oozie hello interfejsu API, zobacz [dokumentację Apache Oozie 4.0] [ apache-oozie-400] (dla usługi HDInsight w wersji 3.0 lub nowszej) lub [dokumentację Apache Oozie 3.3.2] [ apache-oozie-332] (dla usługi HDInsight w wersji 2.1).</span><span class="sxs-lookup"><span data-stu-id="4278b-180">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="4278b-181">skrypt programu PowerShell w tej sekcji Hello wykonuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4278b-181">hello PowerShell script in this section performs hello following steps:</span></span>

1. <span data-ttu-id="4278b-182">Połącz tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4278b-182">Connect tooAzure.</span></span>
2. <span data-ttu-id="4278b-183">Utwórz grupę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4278b-183">Create an Azure resource group.</span></span> <span data-ttu-id="4278b-184">Aby uzyskać więcej informacji, zobacz [użycia programu Azure PowerShell z usługą Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4278b-184">For more information, see [Use Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
3. <span data-ttu-id="4278b-185">Utwórz serwer bazy danych SQL Azure, bazy danych Azure SQL i dwie tabele.</span><span class="sxs-lookup"><span data-stu-id="4278b-185">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> <span data-ttu-id="4278b-186">Są one używane przez hello Sqoop działań w przepływie pracy hello.</span><span class="sxs-lookup"><span data-stu-id="4278b-186">These are used by hello Sqoop action in hello workflow.</span></span>
   
    <span data-ttu-id="4278b-187">Nazwa tabeli Hello jest *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="4278b-187">hello table name is *log4jLogCount*.</span></span>
4. <span data-ttu-id="4278b-188">Utwórz toorun używane klastra usługi HDInsight Oozie zadania.</span><span class="sxs-lookup"><span data-stu-id="4278b-188">Create an HDInsight cluster used toorun Oozie jobs.</span></span>
   
    <span data-ttu-id="4278b-189">tooexamine hello klastra, można użyć hello portalu Azure lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4278b-189">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="4278b-190">Skopiuj plik przepływu pracy oozie hello i hello HiveQL skryptu pliku toohello domyślnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="4278b-190">Copy hello oozie workflow file and hello HiveQL script file toohello default file system.</span></span>
   
    <span data-ttu-id="4278b-191">Oba pliki są przechowywane w publicznego kontenera obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="4278b-191">Both files are stored in a public Blob container.</span></span>
   
   * <span data-ttu-id="4278b-192">Skopiuj hello HiveQL skryptu (useoozie.hql) tooAzure magazynu (wasb:///tutorials/useoozie/useoozie.hql).</span><span class="sxs-lookup"><span data-stu-id="4278b-192">Copy hello HiveQL script (useoozie.hql) tooAzure Storage (wasb:///tutorials/useoozie/useoozie.hql).</span></span>
   * <span data-ttu-id="4278b-193">Skopiuj workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="4278b-193">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
   * <span data-ttu-id="4278b-194">Plik danych hello kopiowania (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="4278b-194">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
6. <span data-ttu-id="4278b-195">Prześlij zadanie Oozie.</span><span class="sxs-lookup"><span data-stu-id="4278b-195">Submit an Oozie job.</span></span>
   
    <span data-ttu-id="4278b-196">tooexamine hello OOzie wyniki zadania, za pomocą programu Visual Studio lub innych narzędzi tooconnect toohello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4278b-196">tooexamine hello OOzie job results, use Visual Studio or other tools tooconnect toohello Azure SQL Database.</span></span>

<span data-ttu-id="4278b-197">Oto hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="4278b-197">Here is hello script.</span></span>  <span data-ttu-id="4278b-198">Można uruchomić skryptu hello z programu Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="4278b-198">You can run hello script from Windows PowerShell ISE.</span></span> <span data-ttu-id="4278b-199">Wystarczy tooconfigure hello pierwszych 7 zmiennych.</span><span class="sxs-lookup"><span data-stu-id="4278b-199">You only need tooconfigure hello first 7 variables.</span></span>

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure subscription ID>"

    # SQL Database server login credentials used for creating and connecting
    $sqlDatabaseLogin = "<Enter SQL Database Login Name>"
    $sqlDatabasePassword = "<Enter SQL Database Login Password>"

    # HDInsight cluster HTTP user credential used for creating and connectin
    $httpUserName = "admin"  # hello default name is "admin"
    $httpPassword = "<Enter HDInsight Cluster HTTP User Password>"

    # Used for creating Azure service names
    $nameToken = "<Enter an Alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{
        Login-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionId $subscriptionID
    }
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $sqlLoginCredentials = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $sqlLoginCredentials `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }
    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }
    #endregion

    #region - Create SQL database tables
    Write-Host "Creating hello log4jlogs table  ..." -ForegroundColor Green

    $sqlDatabaseTableName = "log4jLogsCount"
    $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
            [Level] [nvarchar](10) NOT NULL,
            [Total] float,
        CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
        (
        [Level] ASC
        )
        )"

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jCountTable
    $cmd.ExecuteNonQuery()

    $conn.close()
    #endregion

    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - copy Oozie workflow and HiveQL files

    Write-Host "Copy workflow definition and HiveQL script file ..." -ForegroundColor Green

    # Both files are stored in a public Blob
    $publicBlobContext = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "useooziewf.hql"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/useooziewf.hql" `
        -Force

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "workflow.xml"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/workflow.xml" `
        -Force

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/workflow.xml

    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/useooziewf.hql

    #endregion

    #region - copy hello sample.log file

    Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green

    Start-CopyAzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -SrcContainer $defaultBlobContainerName `
        -SrcBlob "example/data/sample.log"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -destBlob "$destFolder/data/sample.log" 

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/data/sample.log

    #endregion

    #region - submit Oozie job

    $storageUri="wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net"

    $oozieJobName = $namePrefix + "OozieJob"

    #Oozie WF variables
    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"

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
        <value>$httpUserName</value>
    </property>

    <property>
        <name>oozie.wf.application.path</name>
        <value>$oozieWFPath</value>
    </property>

    </configuration>
    "@

    Write-Host "Checking Oozie server status..." -ForegroundColor Green
    $clusterUriStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/admin/status"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $httpCredential -OutVariable $OozieServerStatus

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieServerSatus = $jsonResponse[0].("systemMode")
    Write-Host "Oozie server status is $oozieServerSatus."

    # create Oozie job
    Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
    Write-Host "`n--------`n$OoziePayload`n--------"
    $clusterUriCreateJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/jobs"
    $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $httpCredential -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName #-debug

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieJobId = $jsonResponse[0].("id")
    Write-Host "Oozie job id is $oozieJobId..."

    # start Oozie job
    Write-Host "Starting hello Oozie job $oozieJobId..." -ForegroundColor Green
    $clusterUriStartJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=start"
    $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $httpCredential | Format-Table -HideTableHeaders #-debug

    # get job status
    Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
    Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

    Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
    $clusterUriGetJobStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $JobStatus = $jsonResponse[0].("status")

    while($JobStatus -notmatch "SUCCEEDED|KILLED")
    {
        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")
        $jobStatus
    }

    Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!" -ForegroundColor Green

    #endregion


<span data-ttu-id="4278b-200">**Witaj toore uruchom samouczek**</span><span class="sxs-lookup"><span data-stu-id="4278b-200">**toore-run hello tutorial**</span></span>

<span data-ttu-id="4278b-201">Uruchom toore hello przepływu pracy, należy usunąć hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4278b-201">toore-run hello workflow, you must delete hello following items:</span></span>

* <span data-ttu-id="4278b-202">Witaj pliku danych wyjściowych skryptu Hive</span><span class="sxs-lookup"><span data-stu-id="4278b-202">hello Hive script output file</span></span>
* <span data-ttu-id="4278b-203">Witaj dane w tabeli log4jLogsCount hello</span><span class="sxs-lookup"><span data-stu-id="4278b-203">hello data in hello log4jLogsCount table</span></span>

<span data-ttu-id="4278b-204">Poniżej przedstawiono przykładowy skrypt programu PowerShell, którego można używać:</span><span class="sxs-lookup"><span data-stu-id="4278b-204">Here is a sample PowerShell script that you can use:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"

    $defaultStorageAccountName = "<AzureStorageAccountName>"
    $defaultBlobContainerName = "<ContainerName>"

    #SQL database variables
    $sqlDatabaseServerName = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabasePassword = "<SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                -ResourceGroupName $resourceGroupName `
                                -Name $defaultStorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $defaultBlobContainerName

    Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = "delete from $sqlDatabaseTableName"
    $cmd.executenonquery()

    $conn.close()

## <a name="next-steps"></a><span data-ttu-id="4278b-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4278b-205">Next steps</span></span>
<span data-ttu-id="4278b-206">W tym samouczku można przedstawiono sposób toodefine Oozie przepływu pracy i jak toorun Oozie zadania przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4278b-206">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job by using PowerShell.</span></span> <span data-ttu-id="4278b-207">toolearn więcej, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="4278b-207">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="4278b-208">[Korzystanie z usługą HDInsight oparte na czasie Oozie Coordinator][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="4278b-208">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="4278b-209">[Rozpocząć korzystanie z usługi Hadoop przy użyciu Hive HDInsight tooanalyze przenośnych słuchawki używana][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="4278b-209">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="4278b-210">[Użyj magazynu obiektów Blob platformy Azure z usługą HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="4278b-210">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="4278b-211">[Administrowanie HDInsight przy użyciu programu PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="4278b-211">[Administer HDInsight using PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="4278b-212">[Przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="4278b-212">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="4278b-213">[Używanie Sqoop z platformą Hadoop w usłudze HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="4278b-213">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="4278b-214">[Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="4278b-214">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="4278b-215">[Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="4278b-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="4278b-216">[Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="4278b-216">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563



[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md


[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: ../sql-database-create-configure.md
[sqldatabase-get-started]: ../sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png  
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
