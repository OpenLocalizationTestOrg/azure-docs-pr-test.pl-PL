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
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="d1a70-104">Rozwiązywanie problemów z YARN za pomocą usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d1a70-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="d1a70-105">Dowiedz się więcej o hello Najważniejsze problemy i rozwiązania ich podczas pracy z ładunków Apache Hadoop YARN w Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="d1a70-105">Learn about hello top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="d1a70-106">Jak utworzyć nową kolejkę YARN w klastrze</span><span class="sxs-lookup"><span data-stu-id="d1a70-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="d1a70-107">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="d1a70-107">Resolution steps</span></span> 

<span data-ttu-id="d1a70-108">Użyj następujących hello czynnościach w ramach Ambari toocreate nową kolejkę YARN, a następnie saldo alokacji pojemności hello wśród wszystkich kolejek hello.</span><span class="sxs-lookup"><span data-stu-id="d1a70-108">Use hello following steps in Ambari toocreate a new YARN queue, and then balance hello capacity allocation among all hello queues.</span></span> 

<span data-ttu-id="d1a70-109">W tym przykładzie dwie istniejącej kolejki (**domyślne** i **thriftsvr**) są zmienione z 50% pojemności too25% pojemności, co daje hello nowej kolejki (spark) pojemności 50%.</span><span class="sxs-lookup"><span data-stu-id="d1a70-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity too25% capacity, which gives hello new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="d1a70-110">Kolejka</span><span class="sxs-lookup"><span data-stu-id="d1a70-110">Queue</span></span> | <span data-ttu-id="d1a70-111">Pojemność</span><span class="sxs-lookup"><span data-stu-id="d1a70-111">Capacity</span></span> | <span data-ttu-id="d1a70-112">Maksymalna pojemność</span><span class="sxs-lookup"><span data-stu-id="d1a70-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1a70-113">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d1a70-113">default</span></span> | <span data-ttu-id="d1a70-114">25%</span><span class="sxs-lookup"><span data-stu-id="d1a70-114">25%</span></span> | <span data-ttu-id="d1a70-115">50%</span><span class="sxs-lookup"><span data-stu-id="d1a70-115">50%</span></span> |
| <span data-ttu-id="d1a70-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="d1a70-116">thrftsvr</span></span> | <span data-ttu-id="d1a70-117">25%</span><span class="sxs-lookup"><span data-stu-id="d1a70-117">25%</span></span> | <span data-ttu-id="d1a70-118">50%</span><span class="sxs-lookup"><span data-stu-id="d1a70-118">50%</span></span> |
| <span data-ttu-id="d1a70-119">Platforma Spark</span><span class="sxs-lookup"><span data-stu-id="d1a70-119">spark</span></span> | <span data-ttu-id="d1a70-120">50%</span><span class="sxs-lookup"><span data-stu-id="d1a70-120">50%</span></span> | <span data-ttu-id="d1a70-121">50%</span><span class="sxs-lookup"><span data-stu-id="d1a70-121">50%</span></span> |

1. <span data-ttu-id="d1a70-122">Wybierz hello **widoków Ambari** ikonę, a następnie wybierz opcję hello grid — wzorzec.</span><span class="sxs-lookup"><span data-stu-id="d1a70-122">Select hello **Ambari Views** icon, and then select hello grid pattern.</span></span> <span data-ttu-id="d1a70-123">Następnie wybierz pozycję **menedżera kolejek YARN**.</span><span class="sxs-lookup"><span data-stu-id="d1a70-123">Next, select **YARN Queue Manager**.</span></span>

    ![Wybierz ikonę widoków Ambari hello](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="d1a70-125">Wybierz hello **domyślne** kolejki.</span><span class="sxs-lookup"><span data-stu-id="d1a70-125">Select hello **default** queue.</span></span>

    ![Wybierz hello domyślnej kolejki](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="d1a70-127">Dla hello **domyślne** kolejka, zmień hello **pojemności** z % too25 50%.</span><span class="sxs-lookup"><span data-stu-id="d1a70-127">For hello **default** queue, change hello **capacity** from 50% too25%.</span></span> <span data-ttu-id="d1a70-128">Dla hello **thriftsvr** kolejka, zmień hello **pojemności** too25%.</span><span class="sxs-lookup"><span data-stu-id="d1a70-128">For hello **thriftsvr** queue, change hello **capacity** too25%.</span></span>

    ![Zmień hello pojemności too25% hello domyślnych i thriftsvr kolejek](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="d1a70-130">Wybierz nową kolejkę, toocreate **dodać kolejki**.</span><span class="sxs-lookup"><span data-stu-id="d1a70-130">toocreate a new queue, select **Add Queue**.</span></span>

    ![Wybierz opcję Dodaj kolejki](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="d1a70-132">Nazwa nowej kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="d1a70-132">Name hello new queue.</span></span>

    ![Nazwa kolejki hello Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="d1a70-134">Pozostaw hello **pojemności** wartości na 50%, a następnie wybierz opcję hello **akcje** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d1a70-134">Leave hello **capacity** values at 50%, and then select hello **Actions** button.</span></span>

    ![Wybierz przycisk akcje hello](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="d1a70-136">Wybierz **Zapisz i Odśwież kolejek**.</span><span class="sxs-lookup"><span data-stu-id="d1a70-136">Select **Save and Refresh Queues**.</span></span>

    ![Wybierz polecenie Zapisz i Odśwież kolejek](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="d1a70-138">Te zmiany są widoczne natychmiast na powitania interfejsie użytkownika YARN harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="d1a70-138">These changes are visible immediately on hello YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="d1a70-139">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="d1a70-139">Additional reading</span></span>

- [<span data-ttu-id="d1a70-140">YARN CapacityScheduler</span><span class="sxs-lookup"><span data-stu-id="d1a70-140">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="d1a70-141">W jaki sposób pobierać dzienników YARN z klastra</span><span class="sxs-lookup"><span data-stu-id="d1a70-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="d1a70-142">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="d1a70-142">Resolution steps</span></span> 

1. <span data-ttu-id="d1a70-143">Połącz toohello klastra usługi HDInsight przy użyciu klienta Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="d1a70-143">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="d1a70-144">Aby uzyskać więcej informacji, zobacz [dodatkowe materiały](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="d1a70-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="d1a70-145">toolist wszystkie hello identyfikatorów aplikacji hello YARN aplikacji, które są aktualnie uruchomione, uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d1a70-145">toolist all hello application IDs of hello YARN applications that are currently running, run hello following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="d1a70-146">Witaj identyfikatory są wymienione w hello **APPLICATIONID** kolumny.</span><span class="sxs-lookup"><span data-stu-id="d1a70-146">hello IDs are listed in hello **APPLICATIONID** column.</span></span> <span data-ttu-id="d1a70-147">Dzienniki można pobrać z hello **APPLICATIONID** kolumny.</span><span class="sxs-lookup"><span data-stu-id="d1a70-147">You can download logs from hello **APPLICATIONID** column.</span></span>

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

3. <span data-ttu-id="d1a70-148">Dzienniki kontenera YARN toodownload dla wszystkich aplikacji wzorców, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d1a70-148">toodownload YARN container logs for all application masters, use hello following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="d1a70-149">To polecenie tworzy plik dziennika o nazwie amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="d1a70-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="d1a70-150">toodownload YARN kontenera dzienniki dla tylko hello najnowszej aplikacji master, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d1a70-150">toodownload YARN container logs for only hello latest application master, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="d1a70-151">To polecenie tworzy plik dziennika o nazwie latestamlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="d1a70-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="d1a70-152">Dzienniki kontenera YARN toodownload hello pierwszy wzorców dwóch aplikacji, należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d1a70-152">toodownload YARN container logs for hello first two application masters, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="d1a70-153">To polecenie tworzy plik dziennika o nazwie first2amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="d1a70-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="d1a70-154">Użyj wszystkich dzienników YARN kontenera toodownload hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d1a70-154">toodownload all YARN container logs, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="d1a70-155">To polecenie tworzy plik dziennika o nazwie logs.txt.</span><span class="sxs-lookup"><span data-stu-id="d1a70-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="d1a70-156">toodownload hello kontenera dziennik YARN dla określonego kontenera hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d1a70-156">toodownload hello YARN container log for a specific container, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="d1a70-157">To polecenie tworzy plik dziennika o nazwie containerlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="d1a70-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="d1a70-158"><a name="additional-reading-2"></a>Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="d1a70-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="d1a70-159">Połącz tooHDInsight (Hadoop) przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="d1a70-159">Connect tooHDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [<span data-ttu-id="d1a70-160">Apache Hadoop YARN pojęcia i aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1a70-160">Apache Hadoop YARN concepts and applications</span></span>](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)







