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
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a>Usuń gałąź błędu braku pamięci w usłudze Azure HDInsight

Dowiedz się, jak toofix gałąź błędu braku pamięci podczas przetwarzania dużych tabel, konfigurując ustawienia pamięci Hive.

## <a name="run-hive-query-against-large-tables"></a>Uruchamianie zapytań Hive względem dużych tabel

Klient uruchomiono zapytań programu Hive:

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

Niektóre różnice tego zapytania:

* T1 jest alias tooa big tabeli Tabela1, który ma wiele typów kolumn ciąg.
* Inne tabele że duży, którzy mają dużo kolumn.
* Wszystkie tabele się wzajemnie, w niektórych przypadkach z wieloma kolumnami TABLE1 i innych.

Zapytanie Hive Hello trwało toofinish 26 minut w klastrze A3 HDInsight 24 węzła. powitania klienta zauważony hello następujące ostrzeżenia:

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

Za pomocą hello Tez wykonywania aparatu. Witaj tego samego zapytania został uruchomiony przez 15 minut, a następnie zwrócił następujący błąd hello:

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

Błąd Hello pozostaje podczas używania większe maszyny wirtualnej (na przykład D12).


## <a name="debug-hello-out-of-memory-error"></a>Debugowanie hello błąd braku pamięci

Technicznej i zespoły inżynierów razem ustalono na jeden z problemów hello powoduje hello błędu braku pamięci [znany problem opisany w hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

Witaj **hive.auto.convert.join.noconditionaltask** hello hive-site.xml pliku zostało ustawione zbyt**true**:

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

Prawdopodobnie mapy sprzężenia została hello przyczynę hello miejsca na stercie Java naszych błędu pamięci. Zgodnie z objaśnieniem w blogu hello [Hadoop Yarn ustawienia pamięci w usłudze HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), jeśli aparat wykonywania jest używane miejsce na stercie hello używanych aplikacji Tez faktycznie należy toohello Tez kontenera. Zobacz powitania po obrazu opisujący hello Tez kontenera pamięci.

![Diagram pamięci kontenera tez: Hive błąd braku pamięci](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

Jak sugeruje hello wpis w blogu, hello następujące dwa ustawienia pamięci Definiowanie pamięci kontenera hello stosu hello: **hive.tez.container.size** i **hive.tez.java.opts**. Naszym doświadczeniu hello wyjątek braku pamięci oznacza to, że rozmiar kontenera hello jest za mały. Oznacza to, że hello rozmiar stosu Java (hive.tez.java.opts) jest za mały. Dlatego w każdym przypadku, gdy zostanie wyświetlony za mało pamięci, możesz spróbować tooincrease **hive.tez.java.opts**. Jeśli to konieczne może być tooincrease **hive.tez.container.size**. Witaj **java.opts** ustawienie powinno być około 80% **container.size**.

> [!NOTE]
> Ustawienie Hello **hive.tez.java.opts** zawsze musi być mniejsza niż **hive.tez.container.size**.
> 
> 

Ponieważ maszyny D12 ma 28GB pamięci RAM, firma Microsoft zdecydowała toouse kontenera o rozmiarze 10GB (10240MB) i przypisać toojava.opts 80%:

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

Z nowymi ustawieniami hello hello kwerendy bazy danych pomyślnie wykonał poniżej 10 minut.

## <a name="next-steps"></a>Następne kroki

Pobieranie błąd za mało pamięci nie musi oznaczać, że rozmiar kontenera hello jest za mały. Zamiast tego należy skonfigurować ustawienia pamięci hello, dzięki czemu rozmiar stosu hello zwiększa się i jest co najmniej 80% rozmiar pamięci kontenera hello. Do optymalizacji zapytań programu Hive, zobacz [zoptymalizować Hive zapytania dla platformy Hadoop w usłudze HDInsight](hdinsight-hadoop-optimize-hive-query.md).
