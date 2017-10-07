---
title: "aaaTroubleshoot YARN za pomocą usługi Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi na pytania toocommon dotyczące pracy z Apache Hadoop YARN i usłudze Azure HDInsight."
keywords: "Azure HDInsight, YARN, często zadawane pytania, rozwiązywanie problemów z przewodnika, często zadawane pytania"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a>Rozwiązywanie problemów z YARN za pomocą usługi Azure HDInsight

Dowiedz się więcej o hello Najważniejsze problemy i rozwiązania ich podczas pracy z ładunków Apache Hadoop YARN w Apache Ambari.

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a>Jak utworzyć nową kolejkę YARN w klastrze


### <a name="resolution-steps"></a>Kroki rozwiązania 

Użyj następujących hello czynnościach w ramach Ambari toocreate nową kolejkę YARN, a następnie saldo alokacji pojemności hello wśród wszystkich kolejek hello. 

W tym przykładzie dwie istniejącej kolejki (**domyślne** i **thriftsvr**) są zmienione z 50% pojemności too25% pojemności, co daje hello nowej kolejki (spark) pojemności 50%.
| Kolejka | Pojemność | Maksymalna pojemność |
| --- | --- | --- | --- |
| Domyślne | 25% | 50% |
| thrftsvr | 25% | 50% |
| Platforma Spark | 50% | 50% |

1. Wybierz hello **widoków Ambari** ikonę, a następnie wybierz opcję hello grid — wzorzec. Następnie wybierz pozycję **menedżera kolejek YARN**.

    ![Wybierz ikonę widoków Ambari hello](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. Wybierz hello **domyślne** kolejki.

    ![Wybierz hello domyślnej kolejki](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. Dla hello **domyślne** kolejka, zmień hello **pojemności** z % too25 50%. Dla hello **thriftsvr** kolejka, zmień hello **pojemności** too25%.

    ![Zmień hello pojemności too25% hello domyślnych i thriftsvr kolejek](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. Wybierz nową kolejkę, toocreate **dodać kolejki**.

    ![Wybierz opcję Dodaj kolejki](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. Nazwa nowej kolejki hello.

    ![Nazwa kolejki hello Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. Pozostaw hello **pojemności** wartości na 50%, a następnie wybierz opcję hello **akcje** przycisku.

    ![Wybierz przycisk akcje hello](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. Wybierz **Zapisz i Odśwież kolejek**.

    ![Wybierz polecenie Zapisz i Odśwież kolejek](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

Te zmiany są widoczne natychmiast na powitania interfejsie użytkownika YARN harmonogramu.

### <a name="additional-reading"></a>Dodatkowe materiały

- [YARN CapacityScheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a>W jaki sposób pobierać dzienników YARN z klastra


### <a name="resolution-steps"></a>Kroki rozwiązania 

1. Połącz toohello klastra usługi HDInsight przy użyciu klienta Secure Shell (SSH). Aby uzyskać więcej informacji, zobacz [dodatkowe materiały](#additional-reading-2).

2. toolist wszystkie hello identyfikatorów aplikacji hello YARN aplikacji, które są aktualnie uruchomione, uruchom hello następujące polecenie:

    ```apache
    yarn top
    ```
    Witaj identyfikatory są wymienione w hello **APPLICATIONID** kolumny. Dzienniki można pobrać z hello **APPLICATIONID** kolumny.

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. Dzienniki kontenera YARN toodownload dla wszystkich aplikacji wzorców, użyj hello następujące polecenie:
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    To polecenie tworzy plik dziennika o nazwie amlogs.txt. 

4. toodownload YARN kontenera dzienniki dla tylko hello najnowszej aplikacji master, użyj hello następujące polecenie:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    To polecenie tworzy plik dziennika o nazwie latestamlogs.txt. 

4. Dzienniki kontenera YARN toodownload hello pierwszy wzorców dwóch aplikacji, należy użyć hello następujące polecenie:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    To polecenie tworzy plik dziennika o nazwie first2amlogs.txt. 

5. Użyj wszystkich dzienników YARN kontenera toodownload hello następujące polecenie:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    To polecenie tworzy plik dziennika o nazwie logs.txt. 

6. toodownload hello kontenera dziennik YARN dla określonego kontenera hello Użyj następującego polecenia:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    To polecenie tworzy plik dziennika o nazwie containerlogs.txt.

### <a name="additional-reading-2"></a>Dodatkowe materiały

- [Połącz tooHDInsight (Hadoop) przy użyciu protokołu SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [Apache Hadoop YARN pojęcia i aplikacji](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)







