---
title: "Usuń gałąź błędu braku pamięci w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Usuń gałąź błędu braku pamięci w usłudze HDInsight. Scenariusz klienta jest kwerenda w wielu dużych tabel."
keywords: "Brak ustawienia Hive za mało pamięci, błąd pamięci"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 7bce3dff-9825-4fa0-a568-c52a9f7d1dad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: da1247070ade11f78b505524f5e970e18eb16d10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="26325-105">Usuń gałąź błędu braku pamięci w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="26325-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="26325-106">Dowiedz się, jak rozwiązać gałąź błędu braku pamięci podczas przetwarzania dużych tabel, konfigurując ustawienia pamięci Hive.</span><span class="sxs-lookup"><span data-stu-id="26325-106">Learn how to fix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="26325-107">Uruchamianie zapytań Hive względem dużych tabel</span><span class="sxs-lookup"><span data-stu-id="26325-107">Run Hive query against large tables</span></span>

<span data-ttu-id="26325-108">Klient uruchomiono zapytań programu Hive:</span><span class="sxs-lookup"><span data-stu-id="26325-108">A customer ran a Hive query:</span></span>

    SELECT
        COUNT (T1.COLUMN1) as DisplayColumn1,
        …
        …
        ….
    FROM
        TABLE1 T1,
        TABLE2 T2,
        TABLE3 T3,
        TABLE5 T4,
        TABLE6 T5,
        TABLE7 T6
    where (T1.KEY1 = T2.KEY1….
        …
        …

<span data-ttu-id="26325-109">Niektóre różnice tego zapytania:</span><span class="sxs-lookup"><span data-stu-id="26325-109">Some nuances of this query:</span></span>

* <span data-ttu-id="26325-110">T1 jest aliasu wielką tabelę Tabela1, który ma wiele typów kolumn ciągu.</span><span class="sxs-lookup"><span data-stu-id="26325-110">T1 is an alias to a big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="26325-111">Inne tabele że duży, którzy mają dużo kolumn.</span><span class="sxs-lookup"><span data-stu-id="26325-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="26325-112">Wszystkie tabele się wzajemnie, w niektórych przypadkach z wieloma kolumnami TABLE1 i innych.</span><span class="sxs-lookup"><span data-stu-id="26325-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="26325-113">Zapytanie Hive trwało 26 minut na zakończenie na węźle klastra usługi HDInsight A3 24.</span><span class="sxs-lookup"><span data-stu-id="26325-113">The Hive query took 26 minutes to finish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="26325-114">Klient zauważyć następujące ostrzeżenia:</span><span class="sxs-lookup"><span data-stu-id="26325-114">The customer noticed the following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="26325-115">Za pomocą aparat wykonywania platformy Tez.</span><span class="sxs-lookup"><span data-stu-id="26325-115">By using the Tez execution engine.</span></span> <span data-ttu-id="26325-116">Tego samego zapytania został uruchomiony przez 15 minut, a następnie wygenerował następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="26325-116">The same query ran for 15 minutes, and then threw the following error:</span></span>

    Status: Failed
    Vertex failed, vertexName=Map 5, vertexId=vertex_1443634917922_0008_1_05, diagnostics=[Task failed, taskId=task_1443634917922_0008_1_05_000006, diagnostics=[TaskAttempt 0 failed, info=[Error: Failure while running task:java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at
    org.apache.hadoop.hive.ql.exec.tez.TezProcessor.initializeAndRunProcessor(TezProcessor.java:172)
        at org.apache.hadoop.hive.ql.exec.tez.TezProcessor.run(TezProcessor.java:138)
        at
    org.apache.tez.runtime.LogicalIOProcessorRuntimeTask.run(LogicalIOProcessorRuntimeTask.java:324)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:176)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:168)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1628)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:168)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:163)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
    Caused by: java.lang.OutOfMemoryError: Java heap space

<span data-ttu-id="26325-117">Błąd pozostaje podczas używania większe maszyny wirtualnej (na przykład D12).</span><span class="sxs-lookup"><span data-stu-id="26325-117">The error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-the-out-of-memory-error"></a><span data-ttu-id="26325-118">Debugowanie błąd braku pamięci</span><span class="sxs-lookup"><span data-stu-id="26325-118">Debug the out of memory error</span></span>

<span data-ttu-id="26325-119">Technicznej i zespoły inżynierów razem ustalono na jeden z problemów, co powoduje błąd braku pamięci [znany problem opisany w Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="26325-119">Our support and engineering teams together found one of the issues causing the out of memory error was a [known issue described in the Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if the sum  of tables sizes in the map join is less than noconditionaltask.size the plan would generate a Map join, the issue with this is that the calculation doesnt take into account the overhead introduced by different HashTable implementation as results if the sum of input sizes is smaller than the noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="26325-120">**Hive.auto.convert.join.noconditionaltask** hive site.xml pliku zostało ustawione na **true**:</span><span class="sxs-lookup"><span data-stu-id="26325-120">The **hive.auto.convert.join.noconditionaltask** in the hive-site.xml file was set to **true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables the optimization about converting common join into mapjoin based on the input file size.
              If this parameter is on, and the sum of size for n-1 of the tables/partitions for a n-way join is smaller than the
              specified size, the join is directly converted to a mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="26325-121">Prawdopodobnie mapy sprzężenia została przyczynę miejsca na stercie Java naszych błędu pamięci.</span><span class="sxs-lookup"><span data-stu-id="26325-121">It is likely map join was the cause of the Java Heap Space our of memory error.</span></span> <span data-ttu-id="26325-122">Zgodnie z objaśnieniem w blogu [Hadoop Yarn ustawienia pamięci w usłudze HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), gdy Tez aparat wykonywania jest używana sterty miejsca używanego faktycznie należy do kontenera aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="26325-122">As explained in the blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used the heap space used actually belongs to the Tez container.</span></span> <span data-ttu-id="26325-123">Zobacz poniższy obraz opisujące pamięci kontenera aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="26325-123">See the following image describing the Tez container memory.</span></span>

![Diagram pamięci kontenera tez: Hive błąd braku pamięci](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="26325-125">Zgodnie z sugestią, wpis w blogu, następujące ustawienia pamięci dwóch Definiowanie pamięci kontenera na stercie: **hive.tez.container.size** i **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="26325-125">As the blog post suggests, the following two memory settings define the container memory for the heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="26325-126">Naszym doświadczeniu wyjątku braku pamięci oznacza to, że rozmiar kontenera jest za mały.</span><span class="sxs-lookup"><span data-stu-id="26325-126">From our experience, the out of memory exception does not mean the container size is too small.</span></span> <span data-ttu-id="26325-127">Oznacza to, że rozmiar sterty Java (hive.tez.java.opts) jest za mały.</span><span class="sxs-lookup"><span data-stu-id="26325-127">It means the Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="26325-128">Aby zawsze, gdy zostanie wyświetlony za mało pamięci, możesz zwiększyć **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="26325-128">So whenever you see out of memory, you can try to increase **hive.tez.java.opts**.</span></span> <span data-ttu-id="26325-129">W razie potrzeby może zajść konieczność zwiększenia **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="26325-129">If needed you might have to increase **hive.tez.container.size**.</span></span> <span data-ttu-id="26325-130">**Java.opts** ustawienie powinno być około 80% **container.size**.</span><span class="sxs-lookup"><span data-stu-id="26325-130">The **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="26325-131">Ustawienie **hive.tez.java.opts** zawsze musi być mniejsza niż **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="26325-131">The setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="26325-132">Ponieważ maszyny D12 ma 28GB pamięci RAM, zdecydowaliśmy się użyć kontenera o rozmiarze 10GB (10240MB) i przypisać 80% java.opts:</span><span class="sxs-lookup"><span data-stu-id="26325-132">Because a D12 machine has 28GB memory, we decided to use a container size of 10GB (10240MB) and assign 80% to java.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="26325-133">Przy użyciu nowych ustawień kwerendy bazy danych pomyślnie wykonał poniżej 10 minut.</span><span class="sxs-lookup"><span data-stu-id="26325-133">With the new settings, the query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26325-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="26325-134">Next steps</span></span>

<span data-ttu-id="26325-135">Pobieranie za mało pamięci błąd nie musi oznaczać, że rozmiar kontenera jest za mały.</span><span class="sxs-lookup"><span data-stu-id="26325-135">Getting an OOM error doesn't necessarily mean the container size is too small.</span></span> <span data-ttu-id="26325-136">Zamiast tego należy skonfigurować ustawienia pamięci, dzięki czemu rozmiar stosu zwiększa się i jest co najmniej 80% rozmiar pamięci kontenera.</span><span class="sxs-lookup"><span data-stu-id="26325-136">Instead, you should configure the memory settings so that the heap size is increased and is at least 80% of the container memory size.</span></span> <span data-ttu-id="26325-137">Do optymalizacji zapytań programu Hive, zobacz [zoptymalizować Hive zapytania dla platformy Hadoop w usłudze HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="26325-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>