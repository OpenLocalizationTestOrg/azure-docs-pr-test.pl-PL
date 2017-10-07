---
title: "aaaTroubleshoot Hive za pomocą usługi Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi na pytania toocommon dotyczące pracy z Apache Hive i usłudze Azure HDInsight."
keywords: "Azure HDInsight, Hive, często zadawane pytania, rozwiązywanie problemów z przewodnika, często zadawane pytania"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a>Rozwiązywanie problemów z Hive za pomocą usługi Azure HDInsight

Dowiedz się więcej o hello najczęściej zadawane pytania i ich rozwiązania podczas pracy z Apache Hive ładunków w Apache Ambari.


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a>Jak wyeksportować na potrzeby magazynu metadanych Hive i zaimportuj go w innym klastrze


### <a name="resolution-steps"></a>Kroki rozwiązania

1. Połącz toohello klastra usługi HDInsight przy użyciu klienta Secure Shell (SSH). Aby uzyskać więcej informacji, zobacz [dodatkowe materiały](#additional-reading-end).

2. Uruchom następujące polecenie na powitania klastra usługi HDInsight, z którego mają potrzeby magazynu metadanych tooexport hello hello:

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  To polecenie generuje plik o nazwie allatables.sql.

3. Skopiuj hello pliku alltables.sql toohello nowego klastra usługi HDInsight, a następnie uruchom następujące polecenie hello:

  ```apache
  hive -f alltables.sql
  ```

Kod Hello w hello kroki rozwiązania przyjęto założenie, że dane, które są ścieżki w nowym klastrze hello hello sam jako ścieżek danych hello na powitania stary klaster. Jeśli ścieżki danych hello są różne, można ręcznie edytować tooreflect pliku alltables.sql hello wygenerowany wszelkie zmiany.

### <a name="additional-reading"></a>Dodatkowe materiały

- [Połącz tooan klastra usługi HDInsight przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a>Jak znaleźć gałęzi dzienniki w klastrze

### <a name="resolution-steps"></a>Kroki rozwiązania

1. Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH. Aby uzyskać więcej informacji, zobacz **dodatkowe materiały**.

2. dzienniki klienta Hive tooview, hello Użyj następującego polecenia:

  ```apache
  /tmp/<username>/hive.log 
  ```

3. Dzienniki potrzeby magazynu metadanych Hive tooview, hello Użyj następującego polecenia:

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. Dzienniki Hiveserver tooview, użyj hello następujące polecenie:

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a>Dodatkowe materiały

- [Połącz tooan klastra usługi HDInsight przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a>Jak uruchomić hello powłoki gałąź o określonej konfiguracji w klastrze

### <a name="resolution-steps"></a>Kroki rozwiązania

1. Określ parę klucz wartość konfiguracji podczas uruchamiania hello powłoki Hive. Aby uzyskać więcej informacji, zobacz [dodatkowe materiały](#additional-reading-end).

  ```apache
  hive -hiveconf a=b 
  ```

2. toolist wszystkie konfiguracje skuteczne na gałąź powłoki, hello Użyj następującego polecenia:

  ```apache
  hive> set;
  ```

  Na przykład użyć powitania po powłoka poleceń programu Hive toostart z rejestrowaniem debugowania włączone na powitania konsoli:

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a>Dodatkowe materiały

- [Właściwości konfiguracji gałęzi](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Jak analizować dane Tez DAG na ścieżkę krytyczną klastra


### <a name="resolution-steps"></a>Kroki rozwiązania
 
1. tooanalyze Apache Tez skierowany wykresu acyklicznego (DAG) na wykresie klastra o znaczeniu krytycznym, Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH. Aby uzyskać więcej informacji, zobacz [dodatkowe materiały](#additional-reading-end).

2. W wierszu polecenia Uruchom następujące polecenie hello:
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. toolist innych analizatorów, które mogą być używane tooanalyze Tez DAG, użyj hello następujące polecenie:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  Należy podać przykład programu jako pierwszego argumentu hello.

  Program prawidłowe nazwy zawierają:
    - **ContainerReuseAnalyzer**: drukowanie szczegółów ponownemu kontenera w grupie DAG
    - **CriticalPath**: Znajdź hello ścieżkę krytyczną do grupy DAG
    - **LocalityAnalyzer**: drukowanie szczegółów miejscowości, w grupie DAG
    - **ShuffleTimeAnalyzer**: analizowanie szczegóły godziny losowa hello w grupie DAG
    - **SkewAnalyzer**: analizowanie hello pochylenia szczegółów w grupie DAG
    - **SlowNodeAnalyzer**: drukowanie szczegółów węzła w grupie DAG
    - **SlowTaskIdentifier**: szczegóły powolne zadania drukowania w grupie DAG
    - **SlowestVertexAnalyzer**: drukowanie najwolniejsze szczegółów wierzchołków w grupie DAG
    - **SpillAnalyzer**: szczegóły usuwania wycieków drukowania w grupie DAG
    - **TaskConcurrencyAnalyzer**: drukowanie szczegółów współbieżności zadań hello w grupie DAG
    - **VertexLevelCriticalPathAnalyzer**: Znajdź ścieżkę krytyczną hello na poziomie wierzchołków w grupie DAG


### <a name="additional-reading"></a>Dodatkowe materiały

- [Połącz tooan klastra usługi HDInsight przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a>W jaki sposób pobierać dane Tez DAG z klastra


#### <a name="resolution-steps"></a>Kroki rozwiązania

Istnieją dwa sposoby toocollect hello Tez DAG danych:

- Z wiersza polecenia hello:
 
    Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH. W wierszu polecenia hello uruchom następujące polecenia hello:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- Użyj hello Ambari Tez widoku:
   
  1. Przejdź tooAmbari. 
  2. Widok Przejdź tooTez (w obszarze hello Kafelki ikonę w prawym górnym rogu hello). 
  3. Wybierz hello ma tooview grupy DAG.
  4. Wybierz **pobierania danych**.

### <a name="additional-reading-end"></a>Dodatkowe materiały

[Połącz tooan klastra usługi HDInsight przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md)






