---
title: "aaaFix gałąź błędu braku pamięci w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Usuń gałąź błędu braku pamięci w usłudze HDInsight. Scenariusz klienta Hello jest kwerenda w wielu dużych tabel."
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
ms.openlocfilehash: 00a12969322c1e74434ba6593ffd098f342edd84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="be3ce-105">Usuń gałąź błędu braku pamięci w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="be3ce-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="be3ce-106">Dowiedz się, jak toofix gałąź błędu braku pamięci podczas przetwarzania dużych tabel, konfigurując ustawienia pamięci Hive.</span><span class="sxs-lookup"><span data-stu-id="be3ce-106">Learn how toofix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="be3ce-107">Uruchamianie zapytań Hive względem dużych tabel</span><span class="sxs-lookup"><span data-stu-id="be3ce-107">Run Hive query against large tables</span></span>

<span data-ttu-id="be3ce-108">Klient uruchomiono zapytań programu Hive:</span><span class="sxs-lookup"><span data-stu-id="be3ce-108">A customer ran a Hive query:</span></span>

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

<span data-ttu-id="be3ce-109">Niektóre różnice tego zapytania:</span><span class="sxs-lookup"><span data-stu-id="be3ce-109">Some nuances of this query:</span></span>

* <span data-ttu-id="be3ce-110">T1 jest alias tooa big tabeli Tabela1, który ma wiele typów kolumn ciąg.</span><span class="sxs-lookup"><span data-stu-id="be3ce-110">T1 is an alias tooa big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="be3ce-111">Inne tabele że duży, którzy mają dużo kolumn.</span><span class="sxs-lookup"><span data-stu-id="be3ce-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="be3ce-112">Wszystkie tabele się wzajemnie, w niektórych przypadkach z wieloma kolumnami TABLE1 i innych.</span><span class="sxs-lookup"><span data-stu-id="be3ce-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="be3ce-113">Zapytanie Hive Hello trwało toofinish 26 minut w klastrze A3 HDInsight 24 węzła.</span><span class="sxs-lookup"><span data-stu-id="be3ce-113">hello Hive query took 26 minutes toofinish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="be3ce-114">powitania klienta zauważony hello następujące ostrzeżenia:</span><span class="sxs-lookup"><span data-stu-id="be3ce-114">hello customer noticed hello following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="be3ce-115">Za pomocą hello Tez wykonywania aparatu.</span><span class="sxs-lookup"><span data-stu-id="be3ce-115">By using hello Tez execution engine.</span></span> <span data-ttu-id="be3ce-116">Witaj tego samego zapytania został uruchomiony przez 15 minut, a następnie zwrócił następujący błąd hello:</span><span class="sxs-lookup"><span data-stu-id="be3ce-116">hello same query ran for 15 minutes, and then threw hello following error:</span></span>

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

<span data-ttu-id="be3ce-117">Błąd Hello pozostaje podczas używania większe maszyny wirtualnej (na przykład D12).</span><span class="sxs-lookup"><span data-stu-id="be3ce-117">hello error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-hello-out-of-memory-error"></a><span data-ttu-id="be3ce-118">Debugowanie hello błąd braku pamięci</span><span class="sxs-lookup"><span data-stu-id="be3ce-118">Debug hello out of memory error</span></span>

<span data-ttu-id="be3ce-119">Technicznej i zespoły inżynierów razem ustalono na jeden z problemów hello powoduje hello błędu braku pamięci [znany problem opisany w hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="be3ce-119">Our support and engineering teams together found one of hello issues causing hello out of memory error was a [known issue described in hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="be3ce-120">Witaj **hive.auto.convert.join.noconditionaltask** hello hive-site.xml pliku zostało ustawione zbyt**true**:</span><span class="sxs-lookup"><span data-stu-id="be3ce-120">hello **hive.auto.convert.join.noconditionaltask** in hello hive-site.xml file was set too**true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="be3ce-121">Prawdopodobnie mapy sprzężenia została hello przyczynę hello miejsca na stercie Java naszych błędu pamięci.</span><span class="sxs-lookup"><span data-stu-id="be3ce-121">It is likely map join was hello cause of hello Java Heap Space our of memory error.</span></span> <span data-ttu-id="be3ce-122">Zgodnie z objaśnieniem w blogu hello [Hadoop Yarn ustawienia pamięci w usłudze HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), jeśli aparat wykonywania jest używane miejsce na stercie hello używanych aplikacji Tez faktycznie należy toohello Tez kontenera.</span><span class="sxs-lookup"><span data-stu-id="be3ce-122">As explained in hello blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used hello heap space used actually belongs toohello Tez container.</span></span> <span data-ttu-id="be3ce-123">Zobacz powitania po obrazu opisujący hello Tez kontenera pamięci.</span><span class="sxs-lookup"><span data-stu-id="be3ce-123">See hello following image describing hello Tez container memory.</span></span>

![Diagram pamięci kontenera tez: Hive błąd braku pamięci](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="be3ce-125">Jak sugeruje hello wpis w blogu, hello następujące dwa ustawienia pamięci Definiowanie pamięci kontenera hello stosu hello: **hive.tez.container.size** i **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="be3ce-125">As hello blog post suggests, hello following two memory settings define hello container memory for hello heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="be3ce-126">Naszym doświadczeniu hello wyjątek braku pamięci oznacza to, że rozmiar kontenera hello jest za mały.</span><span class="sxs-lookup"><span data-stu-id="be3ce-126">From our experience, hello out of memory exception does not mean hello container size is too small.</span></span> <span data-ttu-id="be3ce-127">Oznacza to, że hello rozmiar stosu Java (hive.tez.java.opts) jest za mały.</span><span class="sxs-lookup"><span data-stu-id="be3ce-127">It means hello Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="be3ce-128">Dlatego w każdym przypadku, gdy zostanie wyświetlony za mało pamięci, możesz spróbować tooincrease **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="be3ce-128">So whenever you see out of memory, you can try tooincrease **hive.tez.java.opts**.</span></span> <span data-ttu-id="be3ce-129">Jeśli to konieczne może być tooincrease **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="be3ce-129">If needed you might have tooincrease **hive.tez.container.size**.</span></span> <span data-ttu-id="be3ce-130">Witaj **java.opts** ustawienie powinno być około 80% **container.size**.</span><span class="sxs-lookup"><span data-stu-id="be3ce-130">hello **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="be3ce-131">Ustawienie Hello **hive.tez.java.opts** zawsze musi być mniejsza niż **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="be3ce-131">hello setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="be3ce-132">Ponieważ maszyny D12 ma 28GB pamięci RAM, firma Microsoft zdecydowała toouse kontenera o rozmiarze 10GB (10240MB) i przypisać toojava.opts 80%:</span><span class="sxs-lookup"><span data-stu-id="be3ce-132">Because a D12 machine has 28GB memory, we decided toouse a container size of 10GB (10240MB) and assign 80% toojava.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="be3ce-133">Z nowymi ustawieniami hello hello kwerendy bazy danych pomyślnie wykonał poniżej 10 minut.</span><span class="sxs-lookup"><span data-stu-id="be3ce-133">With hello new settings, hello query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be3ce-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be3ce-134">Next steps</span></span>

<span data-ttu-id="be3ce-135">Pobieranie błąd za mało pamięci nie musi oznaczać, że rozmiar kontenera hello jest za mały.</span><span class="sxs-lookup"><span data-stu-id="be3ce-135">Getting an OOM error doesn't necessarily mean hello container size is too small.</span></span> <span data-ttu-id="be3ce-136">Zamiast tego należy skonfigurować ustawienia pamięci hello, dzięki czemu rozmiar stosu hello zwiększa się i jest co najmniej 80% rozmiar pamięci kontenera hello.</span><span class="sxs-lookup"><span data-stu-id="be3ce-136">Instead, you should configure hello memory settings so that hello heap size is increased and is at least 80% of hello container memory size.</span></span> <span data-ttu-id="be3ce-137">Do optymalizacji zapytań programu Hive, zobacz [zoptymalizować Hive zapytania dla platformy Hadoop w usłudze HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="be3ce-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>
