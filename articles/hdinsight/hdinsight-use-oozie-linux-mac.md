---
title: "przepływy pracy Hadoop Oozie aaaUse w HDInsight opartych na systemie Linux | Dokumentacja firmy Microsoft"
description: "Użyj Hadoop Oozie w HDInsight opartych na systemie Linux. Dowiedz się, jak toodefine przepływ Oozie i przesłać zadanie Oozie."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="7edae-104">Użyj Oozie z Hadoop toodefine i uruchomić przepływ pracy na HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="7edae-104">Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="7edae-105">Dowiedz się, jak toouse Apache Oozie z platformą Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7edae-105">Learn how toouse Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="7edae-106">Apache Oozie to system koordynacji/przepływu pracy, który zarządza zadaniami na platformie Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7edae-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="7edae-107">Oozie jest zintegrowany z hello stosem platformy Hadoop i obsługuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="7edae-107">Oozie is integrated with hello Hadoop stack, and it supports hello following jobs:</span></span>

* <span data-ttu-id="7edae-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="7edae-108">Apache MapReduce</span></span>
* <span data-ttu-id="7edae-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="7edae-109">Apache Pig</span></span>
* <span data-ttu-id="7edae-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="7edae-110">Apache Hive</span></span>
* <span data-ttu-id="7edae-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="7edae-111">Apache Sqoop</span></span>

<span data-ttu-id="7edae-112">Oozie mogą być również używane tooschedule zadania, które są określone tooa systemu, np. programów Java lub skryptów powłoki</span><span class="sxs-lookup"><span data-stu-id="7edae-112">Oozie can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="7edae-113">Inną opcją w przypadku definiowania przepływów pracy z usługą HDInsight jest fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="7edae-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="7edae-114">toolearn więcej informacji na temat fabryki danych Azure, zobacz [Use Pig i Hive z fabryką danych][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="7edae-114">toolearn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7edae-115">Oozie nie jest włączona w usłudze HDInsight z przyłączonych do domeny.</span><span class="sxs-lookup"><span data-stu-id="7edae-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7edae-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7edae-116">Prerequisites</span></span>

* <span data-ttu-id="7edae-117">**Klaster usługi HDInsight**: zobacz [Rozpoczynanie pracy z usługą HDInsight w systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="7edae-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7edae-118">kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="7edae-118">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="7edae-119">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="7edae-119">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7edae-120">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="7edae-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="7edae-121">Przykładowy przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="7edae-121">Example workflow</span></span>

<span data-ttu-id="7edae-122">przepływ pracy Hello używane w tym dokumencie zawiera dwa działania.</span><span class="sxs-lookup"><span data-stu-id="7edae-122">hello workflow used in this document contains two actions.</span></span> <span data-ttu-id="7edae-123">Akcje są definicje dla zadania, takie jak uruchomienie Hive, Sqoop, MapReduce lub inny proces:</span><span class="sxs-lookup"><span data-stu-id="7edae-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Diagram przepływu pracy][img-workflow-diagram]

1. <span data-ttu-id="7edae-125">Akcja Hive uruchamia skrypt HiveQL tooextract rekordy z hello **hivesampletable** dołączone do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7edae-125">A Hive action runs a HiveQL script tooextract records from hello **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="7edae-126">Każdy wiersz danych opisuje odwiedziny od określonego urządzenia przenośnego.</span><span class="sxs-lookup"><span data-stu-id="7edae-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="7edae-127">format rekordu Hello zostaną wyświetlone podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="7edae-127">hello record format appears similar toohello following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="7edae-128">Witaj skryptu Hive używane w tym dokumencie zlicza hello łączna liczba wizyt dla poszczególnych platform (takich jak Android lub iPhone) i przechowuje hello liczby tooa nową tabelę programu Hive.</span><span class="sxs-lookup"><span data-stu-id="7edae-128">hello Hive script used in this document counts hello total visits for each platform (such as Android or iPhone) and stores hello counts tooa new Hive table.</span></span>

    <span data-ttu-id="7edae-129">Aby uzyskać więcej informacji na temat programu Hive, zobacz temat [Use Hive with HDInsight][hdinsight-use-hive] (Korzystanie z programu Hive z usługą HDInsight).</span><span class="sxs-lookup"><span data-stu-id="7edae-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="7edae-130">Akcja Sqoop eksportuje zawartość hello hello nowej gałęzi tooa tabeli w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="7edae-130">A Sqoop action exports hello contents of hello new Hive table tooa table in an Azure SQL database.</span></span> <span data-ttu-id="7edae-131">Aby uzyskać więcej informacji o Sqoop, zobacz [Hadoop Sqoop użycia z usługą HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="7edae-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="7edae-132">Obsługiwane wersje Oozie w klastrach HDInsight, zobacz [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="7edae-132">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-hello-working-directory"></a><span data-ttu-id="7edae-133">Utwórz katalog roboczy hello</span><span class="sxs-lookup"><span data-stu-id="7edae-133">Create hello working directory</span></span>

<span data-ttu-id="7edae-134">Oozie oczekuje zasoby wymagane toobe zadania przechowywane w hello sam katalogu.</span><span class="sxs-lookup"><span data-stu-id="7edae-134">Oozie expects resources required for a job toobe stored in hello same directory.</span></span> <span data-ttu-id="7edae-135">W tym przykładzie użyto **wasb: / / / samouczki/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="7edae-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="7edae-136">Ten katalog i katalog danych hello przechowujący hello nową tabelę programu Hive utworzone przez ten przepływ pracy, należy użyć następującego polecenia toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-136">Use hello following command toocreate this directory, and hello data directory that holds hello new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="7edae-137">Witaj `-p` parametr powoduje, że wszystkie katalogi w toobe ścieżka hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="7edae-137">hello `-p` parameter causes all directories in hello path toobe created.</span></span> <span data-ttu-id="7edae-138">Witaj **danych** katalog jest używany toohold dane używane przez hello **useooziewf.hql** skryptu.</span><span class="sxs-lookup"><span data-stu-id="7edae-138">hello **data** directory is used toohold data used by hello **useooziewf.hql** script.</span></span>

<span data-ttu-id="7edae-139">Również uruchomić następujące polecenie, które zapewnia, że Oozie mogą personifikować konta użytkownika podczas uruchamiania zadań Hive i Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-139">Also run hello following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="7edae-140">Zastąp **USERNAME** z nazwy logowania:</span><span class="sxs-lookup"><span data-stu-id="7edae-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="7edae-141">Błędy można zignorować ten użytkownik hello jest już członkiem hello `users` grupy.</span><span class="sxs-lookup"><span data-stu-id="7edae-141">You can ignore errors that hello user is already a member of hello `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="7edae-142">Dodaj sterownik bazy danych</span><span class="sxs-lookup"><span data-stu-id="7edae-142">Add a database driver</span></span>

<span data-ttu-id="7edae-143">Ponieważ ten przepływ pracy używa Sqoop tooexport danych tooSQL bazy danych, należy udostępnić kopię sterownik JDBC hello używane tooSQL tootalk bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7edae-143">Since this workflow uses Sqoop tooexport data tooSQL Database, you must provide a copy of hello JDBC driver used tootalk tooSQL Database.</span></span> <span data-ttu-id="7edae-144">Użyj hello następujące polecenia toocopy on toohello katalogu roboczego:</span><span class="sxs-lookup"><span data-stu-id="7edae-144">Use hello following command toocopy it toohello working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="7edae-145">Jeśli przepływ pracy używane inne zasoby, takie jak jar zawierający aplikację MapReduce, będzie potrzebny tooadd także tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="7edae-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need tooadd these resources as well.</span></span>

## <a name="define-hello-hive-query"></a><span data-ttu-id="7edae-146">Zdefiniuj zapytanie Hive hello</span><span class="sxs-lookup"><span data-stu-id="7edae-146">Define hello Hive query</span></span>

<span data-ttu-id="7edae-147">Użyj hello następujące kroki toocreate skrypt HiveQL, który definiuje kwerendę, która jest używana w przepływie pracy Oozie w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="7edae-147">Use hello following steps toocreate a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="7edae-148">Połącz toohello klastra przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="7edae-148">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="7edae-149">Witaj następujące polecenie jest przykładem przy użyciu hello `ssh` polecenia.</span><span class="sxs-lookup"><span data-stu-id="7edae-149">hello following command is an example of using hello `ssh` command.</span></span> <span data-ttu-id="7edae-150">Zastąp __USERNAME__ użytkownika SSH hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="7edae-150">Replace __USERNAME__ with hello SSH user for hello cluster.</span></span> <span data-ttu-id="7edae-151">Zastąp __CLUSTERNAME__ o nazwie hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7edae-151">Replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="7edae-152">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7edae-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="7edae-153">Hello połączenia SSH używając hello następujące polecenia toocreate pliku:</span><span class="sxs-lookup"><span data-stu-id="7edae-153">From hello SSH connection, use hello following command toocreate a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="7edae-154">Po otwarciu edytora nano hello Użyj następującego zapytania jako hello zawartość pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-154">Once hello nano editor opens, use hello following query as hello contents of hello file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="7edae-155">Istnieją dwie zmienne używane w skrypcie hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-155">There are two variables used in hello script:</span></span>

    * <span data-ttu-id="7edae-156">**${hiveTableName}**: zawiera nazwę hello toobe tabeli hello utworzone</span><span class="sxs-lookup"><span data-stu-id="7edae-156">**${hiveTableName}**: contains hello name of hello table toobe created</span></span>

    * <span data-ttu-id="7edae-157">**${hiveDataFolder}**: plikami hello lokalizacji toostore hello danych dla tabeli hello</span><span class="sxs-lookup"><span data-stu-id="7edae-157">**${hiveDataFolder}**: contains hello location toostore hello data files for hello table</span></span>

    <span data-ttu-id="7edae-158">Plik definicji przepływu pracy Hello (workflow.xml w tym samouczku) przekazuje te wartości toothis skrypt HiveQL w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="7edae-158">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time</span></span>

4. <span data-ttu-id="7edae-159">Edytor hello tooexit, naciśnij klawisze Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="7edae-159">tooexit hello editor, press Ctrl-X.</span></span> <span data-ttu-id="7edae-160">Po wyświetleniu monitu wybierz **Y** toosave hello pliku, a następnie użyj **Enter** toouse hello **useooziewf.hql** nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="7edae-160">When prompted, select **Y** toosave hello file, then use **Enter** toouse hello **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="7edae-161">Użyj następujących hello polecenia toocopy **useooziewf.hql** za**wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="7edae-161">Use hello following commands toocopy **useooziewf.hql** too**wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="7edae-162">Te polecenia przechowywania hello **useooziewf.hql** pliku w magazynie hello zgodnego systemem plików HDFS hello klastra.</span><span class="sxs-lookup"><span data-stu-id="7edae-162">These commands store hello **useooziewf.hql** file on hello HDFS-compatible storage for hello cluster.</span></span>

## <a name="define-hello-workflow"></a><span data-ttu-id="7edae-163">Zdefiniuj hello przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="7edae-163">Define hello workflow</span></span>

<span data-ttu-id="7edae-164">Oozie definicje przepływów pracy są zapisywane w hPDL (XML procesu Definition Language).</span><span class="sxs-lookup"><span data-stu-id="7edae-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="7edae-165">Użyj hello następującego przepływu pracy hello toodefine kroki:</span><span class="sxs-lookup"><span data-stu-id="7edae-165">Use hello following steps toodefine hello workflow:</span></span>

1. <span data-ttu-id="7edae-166">Za pomocą powitania po instrukcji toocreate i edytować plik:</span><span class="sxs-lookup"><span data-stu-id="7edae-166">Use hello following statement toocreate and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="7edae-167">Po otwarciu edytora nano hello wprowadź powitania po XML jako zawartość pliku hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-167">Once hello nano editor opens, enter hello following XML as hello file contents:</span></span>

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
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
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

    <span data-ttu-id="7edae-168">Istnieją dwie akcje zdefiniowane w przepływie pracy hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-168">There are two actions defined in hello workflow:</span></span>

   * <span data-ttu-id="7edae-169">**RunHiveScript**: Ta akcja jest akcji uruchamiania hello i uruchamia hello **useooziewf.hql** wykonanie skryptu technologii Hive</span><span class="sxs-lookup"><span data-stu-id="7edae-169">**RunHiveScript**: This action is hello start action, and runs hello **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="7edae-170">**RunSqoopExport**: Ta akcja eksportuje dane hello utworzone na podstawie tooSQL skryptu Hive hello bazy danych przy użyciu Sqoop.</span><span class="sxs-lookup"><span data-stu-id="7edae-170">**RunSqoopExport**: This action exports hello data created from hello Hive script tooSQL Database using Sqoop.</span></span> <span data-ttu-id="7edae-171">Ta akcja działa tylko wtedy, jeśli hello **RunHiveScript** akcja zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="7edae-171">This action only runs if hello **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="7edae-172">przepływ pracy Hello ma kilka wpisów, takich jak `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="7edae-172">hello workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="7edae-173">Te wpisy są zastępowane przez wartości używanej w definicji zadania hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-173">These entries are replaced by values you use in hello job definition.</span></span> <span data-ttu-id="7edae-174">Witaj definicji zadania jest tworzony w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="7edae-174">hello job definition is created later in this document.</span></span>

     <span data-ttu-id="7edae-175">Również Uwaga hello `<archive>sqljdbc4.jar</arcive>` wpis w sekcji Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-175">Also note hello `<archive>sqljdbc4.jar</arcive>` entry in hello Sqoop section.</span></span> <span data-ttu-id="7edae-176">Ten wpis informuje Oozie toomake to archiwum dostępne dla Sqoop po uruchomieniu tej akcji.</span><span class="sxs-lookup"><span data-stu-id="7edae-176">This entry instructs Oozie toomake this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="7edae-177">Następnie użyj klawiszy Ctrl-X **Y** i **Enter** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="7edae-177">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

4. <span data-ttu-id="7edae-178">Użyj hello następujące polecenie toocopy hello **workflow.xml** pliku zbyt**/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="7edae-178">Use hello following command toocopy hello **workflow.xml** file too**/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a><span data-ttu-id="7edae-179">Utwórz bazę danych hello</span><span class="sxs-lookup"><span data-stu-id="7edae-179">Create hello database</span></span>

<span data-ttu-id="7edae-180">toocreate bazy danych SQL Azure, wykonaj kroki hello hello [Utwórz bazę danych SQL](../sql-database/sql-database-get-started.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="7edae-180">toocreate an Azure SQL Database, follow hello steps in hello [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="7edae-181">Podczas tworzenia hello bazy danych, użyj `oozietest` jako hello Nazwa bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7edae-181">When creating hello database, use `oozietest` as hello database name.</span></span> <span data-ttu-id="7edae-182">Również Zanotuj nazwę hello powitania serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7edae-182">Also make a note of hello name of hello database server.</span></span>

### <a name="create-hello-table"></a><span data-ttu-id="7edae-183">Utwórz tabelę hello</span><span class="sxs-lookup"><span data-stu-id="7edae-183">Create hello table</span></span>

> [!NOTE]
> <span data-ttu-id="7edae-184">Istnieje wiele sposobów tooconnect tooSQL bazy danych toocreate tabeli.</span><span class="sxs-lookup"><span data-stu-id="7edae-184">There are many ways tooconnect tooSQL Database toocreate a table.</span></span> <span data-ttu-id="7edae-185">Witaj, użyj czynności po [protokół FreeTDS](http://www.freetds.org/) z klastrem usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-185">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="7edae-186">Użyj następującego polecenia tooinstall protokół FreeTDS w klastrze usługi HDInsight hello hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-186">Use hello following command tooinstall FreeTDS on hello HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="7edae-187">Po zainstalowaniu protokół FreeTDS Użyj hello następujące polecenia tooconnect toohello bazy danych programu SQL server, utworzonej wcześniej:</span><span class="sxs-lookup"><span data-stu-id="7edae-187">Once FreeTDS has been installed, use hello following command tooconnect toohello SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="7edae-188">Pojawi się toohello podobne dane wyjściowe następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="7edae-188">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. <span data-ttu-id="7edae-189">Na powitania `1>` monit, wprowadź hello następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="7edae-189">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="7edae-190">Gdy hello `GO` instrukcja została wprowadzona, poprzednie instrukcje hello są oceniane.</span><span class="sxs-lookup"><span data-stu-id="7edae-190">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="7edae-191">Te instrukcje tworzenia tabeli o nazwie **mobiledata** używany przez hello przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="7edae-191">These statements create a table named **mobiledata** that is used by hello workflow.</span></span>

    <span data-ttu-id="7edae-192">Utworzono hello Użyj następującego tooverify, który hello tabeli:</span><span class="sxs-lookup"><span data-stu-id="7edae-192">Use hello following tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="7edae-193">Zostaną wyświetlone dane wyjściowe toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="7edae-193">You see output similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="7edae-194">Wprowadź `exit` na powitania `1>` Monituj tooexit hello tsql narzędzia.</span><span class="sxs-lookup"><span data-stu-id="7edae-194">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="create-hello-job-definition"></a><span data-ttu-id="7edae-195">Tworzenie definicji zadania hello</span><span class="sxs-lookup"><span data-stu-id="7edae-195">Create hello job definition</span></span>

<span data-ttu-id="7edae-196">definicji zadania Hello opisano, gdzie toofind hello workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="7edae-196">hello job definition describes where toofind hello workflow.xml.</span></span> <span data-ttu-id="7edae-197">Opisano również where toofind inne pliki używane przez przepływ pracy hello (na przykład useooziewf.hql). Definiuje także hello wartości dla właściwości używane w przepływie pracy hello i skojarzone pliki.</span><span class="sxs-lookup"><span data-stu-id="7edae-197">It also describes where toofind other files used by hello workflow (such as useooziewf.hql.) It also defines hello values for properties used within hello workflow and associated files.</span></span>

1. <span data-ttu-id="7edae-198">Hello Użyj następującego polecenia tooget hello pełny adres hello domyślnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="7edae-198">Use hello following command tooget hello full address of hello default storage.</span></span> <span data-ttu-id="7edae-199">Ten adres jest używany w pliku konfiguracyjnym hello później:</span><span class="sxs-lookup"><span data-stu-id="7edae-199">This address is used in hello configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="7edae-200">To polecenie zwraca informacje toohello podobne po XML:</span><span class="sxs-lookup"><span data-stu-id="7edae-200">This command returns information similar toohello following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="7edae-201">Jeśli hello klastra usługi HDInsight używa magazynu Azure jako hello domyślny magazyn, hello `<value>` zaczynać zawartość elementu `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="7edae-201">If hello HDInsight cluster uses Azure Storage as hello default storage, hello `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="7edae-202">Jeśli zamiast niego jest używana usługa Azure Data Lake Store, rozpoczyna się od `adl://`.</span><span class="sxs-lookup"><span data-stu-id="7edae-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="7edae-203">Zapisz zawartość hello hello `<value>` elementu, ponieważ jest używany w następnych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-203">Save hello contents of hello `<value>` element, as it is used in hello next steps.</span></span>

2. <span data-ttu-id="7edae-204">Użyj hello następujące polecenie tooget FQDN hello headnode klastra.</span><span class="sxs-lookup"><span data-stu-id="7edae-204">Use hello following command tooget FQDN of hello cluster headnode.</span></span> <span data-ttu-id="7edae-205">Te informacje są używane dla hello JobTracker adres klastra hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-205">This information is used for hello JobTracker address for hello cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="7edae-206">To polecenie zwróci informacje toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="7edae-206">This returns information similar toohello following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="7edae-207">Hello port używany do hello JobTracker jest 8050, tak aby hello toouse pełny adres dla hello JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="7edae-207">hello port used for hello JobTracker is 8050, so hello full address toouse for hello JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="7edae-208">Użyj powitania po toocreate hello Oozie zadania definicji konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="7edae-208">Use hello following toocreate hello Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="7edae-209">Po otwarciu edytora nano hello Użyj powitania po XML jako hello zawartość pliku hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-209">Once hello nano editor opens, use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
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
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * <span data-ttu-id="7edae-210">Zastąp wszystkie wystąpienia  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  z wartością hello otrzymany wcześniej do magazynu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="7edae-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with hello value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="7edae-211">Jeśli ścieżka hello jest `wasb` ścieżki, należy użyć hello pełną ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="7edae-211">If hello path is a `wasb` path, you must use hello full path.</span></span> <span data-ttu-id="7edae-212">Nie Skróć go toojust `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="7edae-212">Do not shorten it toojust `wasb:///`.</span></span>

   * <span data-ttu-id="7edae-213">Zastąp **JOBTRACKERADDRESS** z hello adres JobTracker/ResourceManager otrzymany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7edae-213">Replace **JOBTRACKERADDRESS** with hello JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="7edae-214">Zastąp **twojanazwa** nazwą logowania użytkownika hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7edae-214">Replace **YourName** with your login name for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="7edae-215">Zastąp **serverName**, **adminLogin**, i **adminPassword** hello informacje z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7edae-215">Replace **serverName**, **adminLogin**, and **adminPassword** with hello information for your Azure SQL Database.</span></span>

     <span data-ttu-id="7edae-216">Większość informacji hello w tym pliku jest używane toopopulate hello wartości używany w plikach workflow.xml lub ooziewf.hql hello (np. ${nameNode}.)</span><span class="sxs-lookup"><span data-stu-id="7edae-216">Most of hello information in this file is used toopopulate hello values used in hello workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="7edae-217">Witaj **oozie.wf.application.path** where definiuje ona toofind hello workflow.xml pliku, który zawiera hello przepływ pracy został uruchomiony przez to zadanie.</span><span class="sxs-lookup"><span data-stu-id="7edae-217">hello **oozie.wf.application.path** entry defines where toofind hello workflow.xml file, which contains hello workflow ran by this job.</span></span>

5. <span data-ttu-id="7edae-218">Następnie użyj klawiszy Ctrl-X **Y** i **Enter** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="7edae-218">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

## <a name="submit-and-manage-hello-job"></a><span data-ttu-id="7edae-219">Prześlij i zarządzanie hello zadania</span><span class="sxs-lookup"><span data-stu-id="7edae-219">Submit and manage hello job</span></span>

<span data-ttu-id="7edae-220">Hello poniższe kroki Użyj hello Oozie polecenia toosubmit i Zarządzaj przepływami pracy Oozie w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-220">hello following steps use hello Oozie command toosubmit and manage Oozie workflows on hello cluster.</span></span> <span data-ttu-id="7edae-221">Przyjazny interfejs Hello polecenia Oozie znajduje się nad hello [interfejsu API REST Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="7edae-221">hello Oozie command is a friendly interface over hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7edae-222">Korzystając z polecenia Oozie hello, należy użyć dla hello HDInsight headnode hello nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="7edae-222">When using hello Oozie command, you must use hello FQDN for hello HDInsight headnode.</span></span> <span data-ttu-id="7edae-223">Ta nazwa FQDN jest dostępna tylko w klastrze hello lub jeśli hello klaster znajduje się w sieci wirtualnej platformy Azure, z innych komputerów na powitania tej samej sieci.</span><span class="sxs-lookup"><span data-stu-id="7edae-223">This FQDN is only accessible from hello cluster, or if hello cluster is on an Azure Virtual Network, from other machines on hello same network.</span></span>


1. <span data-ttu-id="7edae-224">Użyj powitania po tooobtain hello adresu URL toohello Oozie usługi:</span><span class="sxs-lookup"><span data-stu-id="7edae-224">Use hello following tooobtain hello URL toohello Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="7edae-225">To polecenie zwróci toohello podobne informacje po XML:</span><span class="sxs-lookup"><span data-stu-id="7edae-225">This returns information similar toohello following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="7edae-226">Witaj `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` fragment jest hello toouse adres URL z hello Oozie polecenia.</span><span class="sxs-lookup"><span data-stu-id="7edae-226">hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is hello URL toouse with hello Oozie command.</span></span>

2. <span data-ttu-id="7edae-227">Po toocreate zmienną środowiskową hello adresu URL, dzięki czemu nie trzeba tootype hello użyj go dla każdego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7edae-227">Use hello following toocreate an environment variable for hello URL, so you don't have tootype it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="7edae-228">Zamień adres URL hello hello jedną otrzymany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7edae-228">Replace hello URL with hello one you received earlier.</span></span>
3. <span data-ttu-id="7edae-229">Użyj powitania po toosubmit hello zadania:</span><span class="sxs-lookup"><span data-stu-id="7edae-229">Use hello following toosubmit hello job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="7edae-230">To polecenie ładuje informacje o zadaniu na powitania **job.xml** i przesyła tooOozie, ale nie, nie można go uruchomić.</span><span class="sxs-lookup"><span data-stu-id="7edae-230">This command loads hello job information from **job.xml** and submits it tooOozie, but does not run it.</span></span>

    <span data-ttu-id="7edae-231">Po zakończeniu wykonywania polecenia hello powinien zostać zwrócony identyfikator hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="7edae-231">Once hello command completes, it should return hello ID of hello job.</span></span> <span data-ttu-id="7edae-232">Na przykład `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="7edae-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="7edae-233">Ten identyfikator jest używany toomanage hello zadania.</span><span class="sxs-lookup"><span data-stu-id="7edae-233">This ID is used toomanage hello job.</span></span>

4. <span data-ttu-id="7edae-234">Wyświetl stan hello hello zadania przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7edae-234">View hello status of hello job using hello following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="7edae-235">Zastąp `<JOBID>` z hello identyfikator zwrócony hello poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="7edae-235">Replace `<JOBID>` with hello ID returned in hello previous step.</span></span>

    <span data-ttu-id="7edae-236">To polecenie zwróci informacje toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="7edae-236">This returns information similar toohello following text:</span></span>

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    <span data-ttu-id="7edae-237">To zadanie ma stan `PREP`.</span><span class="sxs-lookup"><span data-stu-id="7edae-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="7edae-238">Ten stan wskazuje hello zadania został utworzony, ale nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="7edae-238">This status indicates that hello job was created, but not started.</span></span>

5. <span data-ttu-id="7edae-239">Witaj Użyj następującego polecenia toostart hello zadania:</span><span class="sxs-lookup"><span data-stu-id="7edae-239">Use hello following command toostart hello job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="7edae-240">Zastąp `<JOBID>` z hello identyfikator zwrócony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7edae-240">Replace `<JOBID>` with hello ID returned previously.</span></span>

    <span data-ttu-id="7edae-241">Jeśli po wykonaniu tego polecenia możesz sprawdzić stan hello, jest w stanie uruchomienia, a hello akcje w ramach zadania hello jest zwracane są informacje.</span><span class="sxs-lookup"><span data-stu-id="7edae-241">If you check hello status after this command, it is in a running state, and information is returned for hello actions within hello job.</span></span>

6. <span data-ttu-id="7edae-242">Po pomyślnym zakończeniu zadania hello, można sprawdzić, czy dane hello został wygenerowany i wyeksportować toohello tabela bazy danych SQL za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-242">Once hello task completes successfully, you can verify that hello data was generated and exported toohello SQL Database table by using hello following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="7edae-243">Na powitania `1>` monit, wprowadź hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="7edae-243">At hello `1>` prompt, enter hello following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="7edae-244">zwrócone informacje Hello jest podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="7edae-244">hello information returned is similar toohello following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="7edae-245">Aby uzyskać więcej informacji na powitania polecenia Oozie, zobacz [narzędzia wiersza polecenia Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="7edae-245">For more information on hello Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="7edae-246">Oozie interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="7edae-246">Oozie REST API</span></span>

<span data-ttu-id="7edae-247">Witaj Oozie interfejsu API REST umożliwia toobuild własnych narzędzi, które współpracują z Oozie.</span><span class="sxs-lookup"><span data-stu-id="7edae-247">hello Oozie REST API allows you toobuild your own tools that work with Oozie.</span></span> <span data-ttu-id="7edae-248">HDInsight określone informacje na temat przy użyciu interfejsu API REST Oozie hello są następujące Hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-248">hello following are HDInsight specific information about using hello Oozie REST API:</span></span>

* <span data-ttu-id="7edae-249">**Identyfikator URI**: hello interfejsu API REST można uzyskać z poza hello klastra`https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="7edae-249">**URI**: hello REST API can be accessed from outside hello cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="7edae-250">**Uwierzytelnianie**: uwierzytelniania toohello interfejsu API przy użyciu konta klastra HTTP hello (Administrator) i hasło.</span><span class="sxs-lookup"><span data-stu-id="7edae-250">**Authentication**: Authenticate toohello API using hello cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="7edae-251">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7edae-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="7edae-252">Aby uzyskać więcej informacji na temat używania hello Oozie interfejsu API REST, zobacz [API usług sieci Web Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="7edae-252">For more information on using hello Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="7edae-253">Oozie interfejsu użytkownika sieci Web</span><span class="sxs-lookup"><span data-stu-id="7edae-253">Oozie Web UI</span></span>

<span data-ttu-id="7edae-254">Hello Oozie interfejs sieci Web zawiera widok opartych na sieci web do stanu hello Oozie zadań w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-254">hello Oozie Web UI provides a web-based view into hello status of Oozie jobs on hello cluster.</span></span> <span data-ttu-id="7edae-255">Interfejs użytkownika sieci web Hello umożliwia hello tooview następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="7edae-255">hello web UI allows you tooview hello following information:</span></span>

* <span data-ttu-id="7edae-256">Stan zadania</span><span class="sxs-lookup"><span data-stu-id="7edae-256">Job status</span></span>
* <span data-ttu-id="7edae-257">Definicji zadania</span><span class="sxs-lookup"><span data-stu-id="7edae-257">Job definition</span></span>
* <span data-ttu-id="7edae-258">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="7edae-258">Configuration</span></span>
* <span data-ttu-id="7edae-259">Wykres hello akcje w zadaniu hello</span><span class="sxs-lookup"><span data-stu-id="7edae-259">A graph of hello actions in hello job</span></span>
* <span data-ttu-id="7edae-260">Dzienników hello zadania</span><span class="sxs-lookup"><span data-stu-id="7edae-260">Logs for hello job</span></span>

<span data-ttu-id="7edae-261">Można również wyświetlić szczegóły dla działania w ramach zadania.</span><span class="sxs-lookup"><span data-stu-id="7edae-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="7edae-262">tooaccess hello Oozie interfejs sieci Web, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7edae-262">tooaccess hello Oozie Web UI, use hello following steps:</span></span>

1. <span data-ttu-id="7edae-263">Tworzenie klastra usługi HDInsight toohello tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="7edae-263">Create an SSH tunnel toohello HDInsight cluster.</span></span> <span data-ttu-id="7edae-264">Aby uzyskać informacje, zobacz hello [Użyj SSH Tunneling z usługą HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="7edae-264">For information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="7edae-265">Po utworzeniu tunelu, otwórz hello interfejsu użytkownika sieci web Ambari w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="7edae-265">Once a tunnel has been created, open hello Ambari web UI in your web browser.</span></span> <span data-ttu-id="7edae-266">Witaj identyfikatora URI dla witryny Ambari hello jest **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="7edae-266">hello URI for hello Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="7edae-267">Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="7edae-267">Replace **CLUSTERNAME** with hello name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="7edae-268">W lewej części strony hello hello, wybierz **Oozie**, następnie **szybkie linki**, a na końcu **Oozie interfejs sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="7edae-268">From hello left side of hello page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![Obraz powitania menu](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="7edae-270">Witaj toodisplaying domyślne ustawienia interfejsu użytkownika sieci Web Oozie uruchomionych zadań przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="7edae-270">hello Oozie Web UI defaults toodisplaying running Workflow Jobs.</span></span> <span data-ttu-id="7edae-271">Wybierz wszystkie zadania przepływu pracy, toosee **wszystkie zadania**.</span><span class="sxs-lookup"><span data-stu-id="7edae-271">toosee all workflow jobs, select **All Jobs**.</span></span>

    ![Wszystkie zadania wyświetlane](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="7edae-273">Wybierz więcej informacji o zadaniu hello tooview zadania.</span><span class="sxs-lookup"><span data-stu-id="7edae-273">Select a job tooview more information about hello job.</span></span>

    ![Informacji o zadaniu](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="7edae-275">Na karcie informacji o zadaniu hello możesz wyświetlać informacje podstawowe zadania i hello poszczególnych działań w ramach zadania hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-275">From hello Job Info tab, you can see basic job information and hello individual actions within hello job.</span></span> <span data-ttu-id="7edae-276">U góry hello, można wyświetlić przy użyciu karty hello hello definicji zadania, zadania konfiguracji, hello dostępu dziennik zadań i wyświetlanie skierowane acykliczne Graph (DAG) hello zadania.</span><span class="sxs-lookup"><span data-stu-id="7edae-276">Using hello tabs at hello top you can view hello Job Definition, Job Configuration, access hello Job Log or view a Directed Acyclic Graph (DAG) of hello job.</span></span>

   * <span data-ttu-id="7edae-277">**Dziennik zadań**: Wybierz hello **GetLogs** przycisk tooget wszystkich dzienników zadania hello, lub użyj hello **filtr wyszukiwania wprowadź** pola toofilter dzienniki</span><span class="sxs-lookup"><span data-stu-id="7edae-277">**Job Log**: Select hello **GetLogs** button tooget all logs for hello job, or use hello **Enter Search Filter** field toofilter logs</span></span>

       ![Dziennik zadań](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="7edae-279">**JobDAG**: hello DAG jest graficznego przeglądu hello ścieżek danych przez przepływ pracy hello</span><span class="sxs-lookup"><span data-stu-id="7edae-279">**JobDAG**: hello DAG is a graphical overview of hello data paths taken through hello workflow</span></span>

       ![Zadanie DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="7edae-281">Wybierając jedną z akcji hello z hello **informacji o zadaniu** kartę wyświetlenie informacji dotyczących hello akcji.</span><span class="sxs-lookup"><span data-stu-id="7edae-281">Selecting one of hello actions from hello **Job Info** tab brings up information for hello action.</span></span> <span data-ttu-id="7edae-282">Na przykład wybierz hello **RunHiveScript** akcji.</span><span class="sxs-lookup"><span data-stu-id="7edae-282">For example, select hello **RunHiveScript** action.</span></span>

    ![Informacje o akcji](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="7edae-284">Aby wyświetlić szczegóły hello akcji, takich jak toohello łącze **adres URL konsoli**.</span><span class="sxs-lookup"><span data-stu-id="7edae-284">You can see details for hello action, such as a link toohello **Console URL**.</span></span> <span data-ttu-id="7edae-285">To łącze mogą być używane tooview JobTracker informacje hello zadania.</span><span class="sxs-lookup"><span data-stu-id="7edae-285">This link can be used tooview JobTracker information for hello job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="7edae-286">Planowanie zadań</span><span class="sxs-lookup"><span data-stu-id="7edae-286">Scheduling jobs</span></span>

<span data-ttu-id="7edae-287">Koordynator Hello umożliwia toospecify rozpoczęcia, zakończenia i wystąpienie częstotliwość zadań.</span><span class="sxs-lookup"><span data-stu-id="7edae-287">hello coordinator allows you toospecify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="7edae-288">toodefine harmonogram hello przepływu pracy, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7edae-288">toodefine a schedule for hello workflow, use hello following steps:</span></span>

1. <span data-ttu-id="7edae-289">Użyj powitania po toocreate plik o nazwie **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="7edae-289">Use hello following toocreate a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="7edae-290">Użyj powitania po XML jako hello zawartość pliku hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-290">Use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > <span data-ttu-id="7edae-291">Witaj `${...}` zmienne są zastępowane przez wartości w definicji zadania hello w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="7edae-291">hello `${...}` variables are replaced by values in hello job definition at run-time.</span></span> <span data-ttu-id="7edae-292">zmienne Hello są:</span><span class="sxs-lookup"><span data-stu-id="7edae-292">hello variables are:</span></span>
    >
    > * <span data-ttu-id="7edae-293">`${coordFrequency}`: Czas między uruchomionych wystąpień hello zadania.</span><span class="sxs-lookup"><span data-stu-id="7edae-293">`${coordFrequency}`: Time between running instances of hello job.</span></span>
    > <span data-ttu-id="7edae-294">** `${coordStart}`: godzina rozpoczęcia zadania hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-294">** `${coordStart}`: hello job start time.</span></span>
    > * <span data-ttu-id="7edae-295">`${coordEnd}`: godzina zakończenia zadania hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-295">`${coordEnd}`: hello job end time.</span></span>
    > * <span data-ttu-id="7edae-296">`${coordTimezone}`: Koordynator zadań znajdują się w stałej strefy czasowej nie czasu letniego (zazwyczaj reprezentowany przy użyciu czasu UTC).</span><span class="sxs-lookup"><span data-stu-id="7edae-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="7edae-297">Ta strefa czasowa jest określane jako hello "Oozie przetwarzania strefy czasowej."</span><span class="sxs-lookup"><span data-stu-id="7edae-297">This time zone is referred as hello "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="7edae-298">`${wfPath}`: hello workflow.xml toohello ścieżki.</span><span class="sxs-lookup"><span data-stu-id="7edae-298">`${wfPath}`: hello path toohello workflow.xml.</span></span>

2. <span data-ttu-id="7edae-299">Witaj toosave plików, użyj klawiszy Ctrl-X **Y**, i **Enter**.</span><span class="sxs-lookup"><span data-stu-id="7edae-299">toosave hello file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="7edae-300">Użyj hello następujące polecenia toocopy hello pliku toohello katalog roboczy dla tego zadania:</span><span class="sxs-lookup"><span data-stu-id="7edae-300">Use hello following command toocopy hello file toohello working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="7edae-301">Użyj powitania po toomodify hello **job.xml** pliku:</span><span class="sxs-lookup"><span data-stu-id="7edae-301">Use hello following toomodify hello **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="7edae-302">Wprowadź hello następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="7edae-302">Make hello following changes:</span></span>

   * <span data-ttu-id="7edae-303">tooinstruct oozie toorun hello koordynatora zamiast pliku hello przepływu pracy, zmień `<name>oozie.wf.application.path</name>` zbyt`<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="7edae-303">tooinstruct oozie toorun hello coordinator file instead of hello workflow, change `<name>oozie.wf.application.path</name>` too`<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="7edae-304">Witaj tooset `workflowPath` zmiennej używanej przez koordynatora hello dodać powitania po XML:</span><span class="sxs-lookup"><span data-stu-id="7edae-304">tooset hello `workflowPath` variable used by hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="7edae-305">Zastąp hello `wasb://mycontainer@mystorageaccount.blob.core.windows` tekst na powitania wartość używana w innych pozycji w pliku job.xml hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-305">Replace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` text with hello value used in other entries in hello job.xml file.</span></span>

   * <span data-ttu-id="7edae-306">toodefine hello rozpoczęcia, zakończenia i częstotliwości hello koordynatora, Dodaj powitania po XML:</span><span class="sxs-lookup"><span data-stu-id="7edae-306">toodefine hello start, end, and frequency for hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       <span data-ttu-id="7edae-307">Te wartości są ustawiane too12 czas rozpoczęcia hello: 00 PM na 10 maja 2017 hello tooMay czas zakończenia 12, 2017 r.</span><span class="sxs-lookup"><span data-stu-id="7edae-307">These values set hello start time too12:00PM on May 10, 2017, hello end time tooMay 12, 2017.</span></span> <span data-ttu-id="7edae-308">Interwał powitania codziennie uruchomienia tego zadania.</span><span class="sxs-lookup"><span data-stu-id="7edae-308">hello interval for running this job daily.</span></span> <span data-ttu-id="7edae-309">częstotliwość Hello jest w minutach, więc 24 godziny x 60 minut = 1440 minut.</span><span class="sxs-lookup"><span data-stu-id="7edae-309">hello frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="7edae-310">Na koniec hello strefę czasową ustawiono tooUTC.</span><span class="sxs-lookup"><span data-stu-id="7edae-310">Finally, hello timezone is set tooUTC.</span></span>

5. <span data-ttu-id="7edae-311">Następnie użyj klawiszy Ctrl-X **Y** i **Enter** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="7edae-311">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

6. <span data-ttu-id="7edae-312">toorun hello zadania hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7edae-312">toorun hello job, use hello following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="7edae-313">To polecenie przesyła i uruchamia zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-313">This command submits and starts hello job.</span></span>

7. <span data-ttu-id="7edae-314">Jeśli odwiedź hello Oozie interfejs sieci Web i wybierz hello **koordynator zadań** kartę, zobacz informacje toohello podobne po obrazu:</span><span class="sxs-lookup"><span data-stu-id="7edae-314">If you visit hello Oozie Web UI and select hello **Coordinator Jobs** tab, you see information similar toohello following image:</span></span>

    ![Koordynator kartę zadania](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="7edae-316">Witaj **Materialization dalej** wpis zawiera hello następnym hello uruchomionych zadań.</span><span class="sxs-lookup"><span data-stu-id="7edae-316">hello **Next Materialization** entry contains hello next time that hello job runs.</span></span>

8. <span data-ttu-id="7edae-317">Podobne toohello wcześniej zadania przepływu pracy, wybierając hello wpisem zadań w interfejsie użytkownika sieci web hello Wyświetla informacje na powitania zadania:</span><span class="sxs-lookup"><span data-stu-id="7edae-317">Similar toohello earlier workflow job, selecting hello job entry in hello web UI displays information on hello job:</span></span>

    ![Informacji o zadaniu koordynatora](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="7edae-319">Ten obraz zawiera tylko pomyślnie uruchamia zadanie hello nie poszczególnych działań w przepływie pracy hello zaplanowane.</span><span class="sxs-lookup"><span data-stu-id="7edae-319">This image only shows successful runs of hello job, not individual actions within hello scheduled workflow.</span></span> <span data-ttu-id="7edae-320">toosee, który, wybierz jedną z hello **akcji** wpisów.</span><span class="sxs-lookup"><span data-stu-id="7edae-320">toosee that, select one of hello **Action** entries.</span></span>

    ![Informacje o akcji](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="7edae-322">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="7edae-322">Troubleshooting</span></span>

<span data-ttu-id="7edae-323">Witaj Oozie interfejsu użytkownika umożliwia tooview Oozie dzienniki.</span><span class="sxs-lookup"><span data-stu-id="7edae-323">hello Oozie UI allows you tooview Oozie logs.</span></span> <span data-ttu-id="7edae-324">Zawiera ona także dzienniki tooJobTracker łącza do zadań MapReduce uruchomione przez hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="7edae-324">It also contains links tooJobTracker logs for MapReduce tasks started by hello workflow.</span></span> <span data-ttu-id="7edae-325">powinny być Hello wzorzec do rozwiązywania problemów:</span><span class="sxs-lookup"><span data-stu-id="7edae-325">hello pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="7edae-326">Wyświetl zadanie hello w interfejsie użytkownika sieci Web Oozie.</span><span class="sxs-lookup"><span data-stu-id="7edae-326">View hello job in Oozie Web UI.</span></span>

2. <span data-ttu-id="7edae-327">Jeśli istnieje komunikat o błędzie lub awaria dla określonej akcji, wybierz hello toosee akcji, jeśli hello **komunikat o błędzie** pole zawiera więcej informacji na powitania awarii.</span><span class="sxs-lookup"><span data-stu-id="7edae-327">If there is an error or failure for a specific action, select hello action toosee if hello **Error Message** field provides more information on hello failure.</span></span>

3. <span data-ttu-id="7edae-328">Jeśli to możliwe, użyj hello adresu URL z tooview akcji hello więcej szczegółów (takich jak dzienniki JobTracker) dla akcji hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-328">If available, use hello URL from hello action tooview more details (such as JobTracker logs) for hello action.</span></span>

<span data-ttu-id="7edae-329">Witaj poniżej przedstawiono określonych błędów mogą wystąpić, i w jaki sposób tooresolve je.</span><span class="sxs-lookup"><span data-stu-id="7edae-329">hello following are specific errors you may encounter, and how tooresolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="7edae-330">JA009: Nie można zainicjować klastra</span><span class="sxs-lookup"><span data-stu-id="7edae-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="7edae-331">**Objawy**: hello zmiany stanu zadania za**zawieszone**.</span><span class="sxs-lookup"><span data-stu-id="7edae-331">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="7edae-332">Szczegóły dotyczące zadania hello stan hello RunHiveScript jako **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="7edae-332">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="7edae-333">Wybranie akcji hello powoduje wyświetlenie hello następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="7edae-333">Selecting hello action displays hello following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="7edae-334">**Przyczyna**: hello WASB adresy używane w hello **job.xml** plik nie zawiera kontenera magazynu hello lub nazwy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7edae-334">**Cause**: hello WASB addresses used in hello **job.xml** file do not contain hello storage container or storage account name.</span></span> <span data-ttu-id="7edae-335">format adresu WASB Hello musi być `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="7edae-335">hello WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="7edae-336">**Rozdzielczość**: Zmień adresy WASB hello używane przez zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-336">**Resolution**: Change hello WASB addresses used by hello job.</span></span>

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a><span data-ttu-id="7edae-337">JA002: Oozie nie jest dozwolona tooimpersonate &lt;użytkownika ></span><span class="sxs-lookup"><span data-stu-id="7edae-337">JA002: Oozie is not allowed tooimpersonate &lt;USER></span></span>

<span data-ttu-id="7edae-338">**Objawy**: hello zmiany stanu zadania za**zawieszone**.</span><span class="sxs-lookup"><span data-stu-id="7edae-338">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="7edae-339">Szczegóły dotyczące zadania hello stan hello RunHiveScript jako **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="7edae-339">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="7edae-340">Wybranie akcji hello przedstawia hello następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="7edae-340">Selecting hello action shows hello following error message:</span></span>

    JA002: User: oozie is not allowed tooimpersonate <USER>

<span data-ttu-id="7edae-341">**Przyczyna**: bieżące ustawienia uprawnienia nie zezwalają na Oozie tooimpersonate hello określone konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7edae-341">**Cause**: Current permission settings do not allow Oozie tooimpersonate hello specified user account.</span></span>

<span data-ttu-id="7edae-342">**Rozdzielczość**: Oozie jest dozwolona tooimpersonate użytkowników w hello **użytkowników** grupy.</span><span class="sxs-lookup"><span data-stu-id="7edae-342">**Resolution**: Oozie is allowed tooimpersonate users in hello **users** group.</span></span> <span data-ttu-id="7edae-343">Użyj hello `groups USERNAME` toosee hello grup, które hello konto użytkownika jest członkiem.</span><span class="sxs-lookup"><span data-stu-id="7edae-343">Use hello `groups USERNAME` toosee hello groups that hello user account is a member of.</span></span> <span data-ttu-id="7edae-344">Jeśli użytkownik hello nie jest elementem członkowskim hello **użytkowników** grupy, użyj hello następujące polecenia tooadd hello użytkownika toohello grupy:</span><span class="sxs-lookup"><span data-stu-id="7edae-344">If hello user is not a member of hello **users** group, use hello following command tooadd hello user toohello group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="7edae-345">Może upłynąć kilka minut, zanim HDInsight rozpoznaje, że został dodany użytkownik hello toohello grupy.</span><span class="sxs-lookup"><span data-stu-id="7edae-345">It may take several minutes before HDInsight recognizes that hello user has been added toohello group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="7edae-346">Uruchamianie błąd (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="7edae-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="7edae-347">**Objawy**: hello zmiany stanu zadania za**KILLED**.</span><span class="sxs-lookup"><span data-stu-id="7edae-347">**Symptoms**: hello job status changes too**KILLED**.</span></span> <span data-ttu-id="7edae-348">Szczegóły dotyczące zadania hello stan hello RunSqoopExport jako **błąd**.</span><span class="sxs-lookup"><span data-stu-id="7edae-348">Details for hello job show hello RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="7edae-349">Wybranie akcji hello przedstawia hello następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="7edae-349">Selecting hello action shows hello following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="7edae-350">**Przyczyna**: Sqoop jest tooload hello sterowników wymaganych tooaccess hello baza danych.</span><span class="sxs-lookup"><span data-stu-id="7edae-350">**Cause**: Sqoop is unable tooload hello database driver required tooaccess hello database.</span></span>

<span data-ttu-id="7edae-351">**Rozdzielczość**: korzystając z zadania Oozie Sqoop, należy uwzględnić hello sterownik bazy danych z hello inne zasoby (na przykład hello workflow.xml) używana przez zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="7edae-351">**Resolution**: When using Sqoop from an Oozie job, you must include hello database driver with hello other resources (such as hello workflow.xml) used by hello job.</span></span> <span data-ttu-id="7edae-352">Także odwoływać archiwum hello zawierający hello sterownik bazy danych z hello `<sqoop>...</sqoop>` sekcji hello workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="7edae-352">Also Reference hello archive containing hello database driver from hello `<sqoop>...</sqoop>` section of hello workflow.xml.</span></span>

<span data-ttu-id="7edae-353">Na przykład hello zadania w tym dokumencie, możesz użyć hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7edae-353">For example, for hello job in this document, you would use hello following steps:</span></span>

1. <span data-ttu-id="7edae-354">Skopiuj hello sqljdbc4.1.jar pliku toohello /tutorials/useoozie katalogu:</span><span class="sxs-lookup"><span data-stu-id="7edae-354">Copy hello sqljdbc4.1.jar file toohello /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="7edae-355">Modyfikowanie hello tooadd workflow.xml powitania po XML w nowym wierszu powyżej `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="7edae-355">Modify hello workflow.xml tooadd hello following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="7edae-356">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7edae-356">Next steps</span></span>

<span data-ttu-id="7edae-357">W tym samouczku można przedstawiono sposób toodefine Oozie przepływu pracy i w jaki sposób toorun Oozie zadania.</span><span class="sxs-lookup"><span data-stu-id="7edae-357">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job.</span></span> <span data-ttu-id="7edae-358">toolearn więcej informacji na temat pracy z usługą HDInsight, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="7edae-358">toolearn more about working with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="7edae-359">[Korzystanie z usługą HDInsight oparte na czasie Oozie Coordinator][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="7edae-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="7edae-360">[Przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="7edae-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="7edae-361">[Używanie Sqoop z platformą Hadoop w usłudze HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="7edae-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="7edae-362">[Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="7edae-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="7edae-363">[Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="7edae-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="7edae-364">[Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="7edae-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

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
