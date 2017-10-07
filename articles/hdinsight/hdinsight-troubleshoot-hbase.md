---
title: "aaaTroubleshoot HBase przy użyciu usługi Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi na pytania toocommon dotyczące pracy z bazy danych HBase i usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinver
manager: ashitg
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 7/7/2017
ms.author: nitinver
ms.openlocfilehash: 5210184f8ea95628952a95df8c98f5b98e37c53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="66241-103">Rozwiązywanie problemów z bazy danych HBase przy użyciu usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="66241-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="66241-104">Dowiedz się więcej o hello Najważniejsze problemy i rozwiązania ich podczas pracy z bazy danych Apache HBase ładunków w Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="66241-104">Learn about hello top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="66241-105">Jak uruchomić raporty polecenie hbck z wielu regionach nieprzypisane</span><span class="sxs-lookup"><span data-stu-id="66241-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="66241-106">Typowe komunikat o błędzie, że można napotkać podczas uruchamiania hello `hbase hbck` polecenie jest "wiele regionów trwa nieprzypisane lub luk w łańcuchu hello regionów."</span><span class="sxs-lookup"><span data-stu-id="66241-106">A common error message that you might see when you run hello `hbase hbck` command is "multiple regions being unassigned or holes in hello chain of regions."</span></span>

<span data-ttu-id="66241-107">Numer hello regionów, które są niezrównoważone na wszystkich serwerach regionie można wyświetlić w hello głównego HBase interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="66241-107">In hello HBase Master UI, you can see hello number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="66241-108">Następnie można uruchomić `hbase hbck` polecenia toosee luk w łańcuchu region hello.</span><span class="sxs-lookup"><span data-stu-id="66241-108">Then, you can run `hbase hbck` command toosee holes in hello region chain.</span></span>

<span data-ttu-id="66241-109">Luk może być spowodowane hello regionach w trybie offline, tak przydziały hello poprawka najpierw.</span><span class="sxs-lookup"><span data-stu-id="66241-109">Holes might be caused by hello offline regions, so fix hello assignments first.</span></span> 

<span data-ttu-id="66241-110">toobring hello nieprzypisane regionów wstecz tooa normalnym stanie, ukończyć powitalnych następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="66241-110">toobring hello unassigned regions back tooa normal state, complete hello following steps:</span></span>

1. <span data-ttu-id="66241-111">Zaloguj się toohello klastra HDInsight HBase przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="66241-111">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="66241-112">tooconnect z hello dozorcy powłoki, uruchom hello `hbase zkcli` polecenia.</span><span class="sxs-lookup"><span data-stu-id="66241-112">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="66241-113">Uruchom hello `rmr /hbase/regions-in-transition` polecenia lub hello `rmr /hbase-unsecure/regions-in-transition` polecenia.</span><span class="sxs-lookup"><span data-stu-id="66241-113">Run hello `rmr /hbase/regions-in-transition` command or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="66241-114">tooexit z hello `hbase zkcli` powłoki, użyj hello `exit` polecenia.</span><span class="sxs-lookup"><span data-stu-id="66241-114">tooexit from hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="66241-115">Otwórz hello Apache Ambari w interfejsie użytkownika i ponownie uruchom usługę Active głównego HBase hello.</span><span class="sxs-lookup"><span data-stu-id="66241-115">Open hello Apache Ambari UI, and then restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="66241-116">Uruchom hello `hbase hbck` polecenia ponownie (bez żadnych opcji).</span><span class="sxs-lookup"><span data-stu-id="66241-116">Run hello `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="66241-117">Sprawdź dane wyjściowe hello tooensure tego polecenia, przypisanych wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="66241-117">Check hello output of this command tooensure that all regions are being assigned.</span></span>


## <span data-ttu-id="66241-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Jak rozwiązać problemy z limitu czasu, korzystając z polecenia hbck przypisania region</span><span class="sxs-lookup"><span data-stu-id="66241-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="66241-119">Problem</span><span class="sxs-lookup"><span data-stu-id="66241-119">Issue</span></span>

<span data-ttu-id="66241-120">Potencjalną przyczyną problemów limitu czasu, gdy używasz hello `hbck` polecenie może być czy kilku regionach w hello "w ramach przejścia" stanie przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="66241-120">A potential cause for timeout issues when you use hello `hbck` command might be that several regions are in hello "in transition" state for a long time.</span></span> <span data-ttu-id="66241-121">Regionach jest widoczny jako w trybie offline w hello głównego HBase interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="66241-121">You can see those regions as offline in hello HBase Master UI.</span></span> <span data-ttu-id="66241-122">Ponieważ dużej liczby regionów próbujesz tootransition, wzorca bazy danych HBase może limitu czasu i być toobring regionach ponownie do trybu online.</span><span class="sxs-lookup"><span data-stu-id="66241-122">Because a high number of regions are attempting tootransition, HBase Master might timeout and be unable toobring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="66241-123">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="66241-123">Resolution steps</span></span>

1. <span data-ttu-id="66241-124">Zaloguj się toohello klastra HDInsight HBase przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="66241-124">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="66241-125">tooconnect z hello dozorcy powłoki, uruchom hello `hbase zkcli` polecenia.</span><span class="sxs-lookup"><span data-stu-id="66241-125">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="66241-126">Uruchom hello `rmr /hbase/regions-in-transition` lub hello `rmr /hbase-unsecure/regions-in-transition` polecenia.</span><span class="sxs-lookup"><span data-stu-id="66241-126">Run hello `rmr /hbase/regions-in-transition` or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="66241-127">Witaj tooexit `hbase zkcli` powłoki, użyj hello `exit` polecenia.</span><span class="sxs-lookup"><span data-stu-id="66241-127">tooexit hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="66241-128">W hello interfejsu użytkownika narzędzia Ambari Uruchom ponownie usługę Active głównego HBase hello.</span><span class="sxs-lookup"><span data-stu-id="66241-128">In hello Ambari UI, restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="66241-129">Uruchom hello `hbase hbck -fixAssignments` polecenie ponownie.</span><span class="sxs-lookup"><span data-stu-id="66241-129">Run hello `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="66241-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Jak I Wymuś. Wyłącz tryb awaryjny systemu plików HDFS w klastrze</span><span class="sxs-lookup"><span data-stu-id="66241-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="66241-131">Problem</span><span class="sxs-lookup"><span data-stu-id="66241-131">Issue</span></span>

<span data-ttu-id="66241-132">powitalne lokalnego Hadoop Distributed pliku System (HDFS) jest zablokowana w trybie awaryjnym w klastrze usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="66241-132">hello local Hadoop Distributed File System (HDFS) is stuck in safe mode on hello HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="66241-133">Szczegółowy opis</span><span class="sxs-lookup"><span data-stu-id="66241-133">Detailed description</span></span>

<span data-ttu-id="66241-134">Przyczyną tego błędu może być awarii po uruchomieniu hello następujące polecenia w systemie plików HDFS:</span><span class="sxs-lookup"><span data-stu-id="66241-134">This error might be caused by a failure when you run hello following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="66241-135">Błąd Hello, które można napotkać podczas próby toorun hello polecenia wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="66241-135">hello error you might see when you try toorun hello command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" tooturn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:4010)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1102)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:630)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:640)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2313)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2309)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:422)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1724)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2307)
        at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1552)
        at org.apache.hadoop.ipc.Client.call(Client.java:1496)
        at org.apache.hadoop.ipc.Client.call(Client.java:1396)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
        at com.sun.proxy.$Proxy10.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:603)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:278)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:194)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:176)
        at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:3061)
        at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:3031)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1162)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1158)
        at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1158)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1150)
        at org.apache.hadoop.fs.FileSystem.mkdirs(FileSystem.java:1898)
        at org.apache.hadoop.fs.shell.Mkdir.processNonexistentPath(Mkdir.java:76)
        at org.apache.hadoop.fs.shell.Command.processArgument(Command.java:273)
        at org.apache.hadoop.fs.shell.Command.processArguments(Command.java:255)
        at org.apache.hadoop.fs.shell.FsCommand.processRawArguments(FsCommand.java:119)
        at org.apache.hadoop.fs.shell.Command.run(Command.java:165)
        at org.apache.hadoop.fs.FsShell.run(FsShell.java:297)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:90)
        at org.apache.hadoop.fs.FsShell.main(FsShell.java:350)
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

### <a name="probable-cause"></a><span data-ttu-id="66241-136">Prawdopodobna przyczyna</span><span class="sxs-lookup"><span data-stu-id="66241-136">Probable cause</span></span>

<span data-ttu-id="66241-137">Witaj klastra usługi HDInsight został skalowany w dół tooa bardzo kilku węzłów.</span><span class="sxs-lookup"><span data-stu-id="66241-137">hello HDInsight cluster has been scaled down tooa very few nodes.</span></span> <span data-ttu-id="66241-138">Witaj liczba węzłów znajduje się poniżej lub zamknąć współczynnik replikacji systemu plików HDFS toohello.</span><span class="sxs-lookup"><span data-stu-id="66241-138">hello number of nodes is below or close toohello HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="66241-139">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="66241-139">Resolution steps</span></span> 

1. <span data-ttu-id="66241-140">Pobierz stan hello powitalne klastra systemu plików HDFS na powitania HDInsight, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="66241-140">Get hello status of hello HDFS on hello HDInsight cluster by running hello following commands:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   ```

   ```apache
   hdiuser@hn0-spark2:~$ hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   Safe mode is ON
   Configured Capacity: 3372381241344 (3.07 TB)
   Present Capacity: 3138625077248 (2.85 TB)
   DFS Remaining: 3102710317056 (2.82 TB)
   DFS Used: 35914760192 (33.45 GB)
   DFS Used%: 1.14%
   Under replicated blocks: 0
   Blocks with corrupt replicas: 0
   Missing blocks: 0
   Missing blocks (with replication factor 1): 0

   -------------------------------------------------
   Live datanodes (8):

   Name: 10.0.0.17:30010 (10.0.0.17)
   Hostname: 10.0.0.17
   Decommission Status : Normal
   Configured Capacity: 421547655168 (392.60 GB)
   DFS Used: 5288128512 (4.92 GB)
   Non DFS Used: 29087272960 (27.09 GB)
   DFS Remaining: 387172253696 (360.58 GB)
   DFS Used%: 1.25%
   DFS Remaining%: 91.85%
   Configured Cache Capacity: 0 (0 B)
   Cache Used: 0 (0 B)
   Cache Remaining: 0 (0 B)
   Cache Used%: 100.00%
   Cache Remaining%: 0.00%
   Xceivers: 2
   Last contact: Wed Apr 05 16:22:00 UTC 2017
   ...

   ```
2. <span data-ttu-id="66241-141">Również można sprawdzić integralność hello powitalne klastra systemu plików HDFS na powitania HDInsight przy użyciu hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="66241-141">You also can check hello integrity of hello HDFS on hello HDInsight cluster by using hello following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting toonamenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
   FSCK started by hdiuser (auth:SIMPLE) from /10.0.0.22 for path / at Wed Apr 05 16:40:28 UTC 2017
   ....................................................................................................

   ....................................................................................................
   ..................Status: HEALTHY
   Total size:    9330539472 B
   Total dirs:    37
   Total files:   2618
   Total symlinks:                0 (Files currently being written: 2)
   Total blocks (validated):      2535 (avg. block size 3680686 B)
   Minimally replicated blocks:   2535 (100.0 %)
   Over-replicated blocks:        0 (0.0 %)
   Under-replicated blocks:       0 (0.0 %)
   Mis-replicated blocks:         0 (0.0 %)
   Default replication factor:    3
   Average block replication:     3.0
   Corrupt blocks:                0
   Missing replicas:              0 (0.0 %)
   Number of data-nodes:          8
   Number of racks:               1
   FSCK ended at Wed Apr 05 16:40:28 UTC 2017 in 187 milliseconds

   hello filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="66241-142">Jeśli okaże się, że nie ma żadnych bloków brakujące, uszkodzony lub under-replikowanych lub te bloki można zignorować, uruchom następujące polecenie tootake hello nazwa węzła tryb awaryjny hello:</span><span class="sxs-lookup"><span data-stu-id="66241-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run hello following command tootake hello name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="66241-143">Jak rozwiązać łączności JDBC lub SQLLine problemy z Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="66241-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="66241-144">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="66241-144">Resolution steps</span></span>

<span data-ttu-id="66241-145">tooconnect z Phoenix, musisz podać adres IP hello aktywnego węzła dozorcy.</span><span class="sxs-lookup"><span data-stu-id="66241-145">tooconnect with Phoenix, you must provide hello IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="66241-146">Upewnij się, że hello dozorcy sqlline.py toowhich usługa próbuje tooconnect jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="66241-146">Ensure that hello ZooKeeper service toowhich sqlline.py is trying tooconnect is up and running.</span></span>
1. <span data-ttu-id="66241-147">Zaloguj się toohello klastra usługi HDInsight przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="66241-147">Sign in toohello HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="66241-148">Wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="66241-148">Enter hello following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="66241-149">Adres IP hello hello aktywnego węzła dozorcy możesz pobrać ze strony hello interfejsu użytkownika narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="66241-149">You can get hello IP address of hello active ZooKeeper node from hello Ambari UI.</span></span> <span data-ttu-id="66241-150">Przejdź za**HBase** > **szybkie linki** > **ZK\* (aktywny)** > **informacji dozorcy**.</span><span class="sxs-lookup"><span data-stu-id="66241-150">Go too**HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="66241-151">Jeśli hello sqlline.py łączy tooPhoenix i jest nie limitu czasu, hello uruchom następujące polecenie toovalidate hello dostępności i kondycji Phoenix:</span><span class="sxs-lookup"><span data-stu-id="66241-151">If hello sqlline.py connects tooPhoenix and does not timeout, run hello following command toovalidate hello availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="66241-152">Jeśli to polecenie działa, nie ma żadnych problem.</span><span class="sxs-lookup"><span data-stu-id="66241-152">If this command works, there is no issue.</span></span> <span data-ttu-id="66241-153">adres IP Hello podany przez użytkownika hello mogą być niepoprawne.</span><span class="sxs-lookup"><span data-stu-id="66241-153">hello IP address provided by hello user might be incorrect.</span></span> <span data-ttu-id="66241-154">Jeśli polecenie hello wstrzymuje przez dłuższy czas, a następnie wyświetla hello następujący błąd, jednak toostep 5.</span><span class="sxs-lookup"><span data-stu-id="66241-154">However, if hello command pauses for an extended time and then displays hello following error, continue toostep 5.</span></span>

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="66241-155">Uruchom hello poniższych poleceń z hello węzła głównego (hn0) toodiagnose hello warunek hello Phoenix systemu. Tabela katalogu:</span><span class="sxs-lookup"><span data-stu-id="66241-155">Run hello following commands from hello head node (hn0) toodiagnose hello condition of hello Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="66241-156">polecenie Hello powinny zostać zwrócone następujące toohello podobne w błąd:</span><span class="sxs-lookup"><span data-stu-id="66241-156">hello command should return an error similar toohello following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="66241-157">W hello interfejsu użytkownika narzędzia Ambari wykonaj następujące kroki toorestart hello HMaster usługi na wszystkich węzłach dozorcy hello:</span><span class="sxs-lookup"><span data-stu-id="66241-157">In hello Ambari UI, complete hello following steps toorestart hello HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="66241-158">W hello **Podsumowanie** sekcji hbase, przejdź zbyt**HBase** > **głównego HBase aktywny**.</span><span class="sxs-lookup"><span data-stu-id="66241-158">In hello **Summary** section of HBase, go too**HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="66241-159">W hello **składniki** sekcji, uruchom ponownie usługę głównego HBase hello.</span><span class="sxs-lookup"><span data-stu-id="66241-159">In hello **Components** section, restart hello HBase Master service.</span></span>
    3. <span data-ttu-id="66241-160">Powtórz te kroki dla wszystkich pozostałych **głównego HBase wstrzymania** usług.</span><span class="sxs-lookup"><span data-stu-id="66241-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="66241-161">Można podjąć toofive minut hello głównego HBase usługi toostabilize i Zakończ proces odzyskiwania hello.</span><span class="sxs-lookup"><span data-stu-id="66241-161">It can take up toofive minutes for hello HBase Master service toostabilize and finish hello recovery process.</span></span> <span data-ttu-id="66241-162">Po kilku minutach Powtórz hello sqlline.py polecenia tooconfirm tego hello systemu. Tabela katalogu jest uruchomiony i że można tworzyć zapytania.</span><span class="sxs-lookup"><span data-stu-id="66241-162">After a few minutes, repeat hello sqlline.py commands tooconfirm that hello SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="66241-163">Gdy hello systemu. Tabela katalogu zapasowego toonormal, tooPhoenix problem łączności hello powinien zostać automatycznie rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="66241-163">When hello SYSTEM.CATALOG table is back toonormal, hello connectivity issue tooPhoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-toofail-toostart"></a><span data-ttu-id="66241-164">Co powoduje, że serwer główny toofail toostart</span><span class="sxs-lookup"><span data-stu-id="66241-164">What causes a master server toofail toostart</span></span>

### <a name="error"></a><span data-ttu-id="66241-165">Błąd</span><span class="sxs-lookup"><span data-stu-id="66241-165">Error</span></span> 

<span data-ttu-id="66241-166">Niepodzielne zmiany nazwy awarii.</span><span class="sxs-lookup"><span data-stu-id="66241-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="66241-167">Szczegółowy opis</span><span class="sxs-lookup"><span data-stu-id="66241-167">Detailed description</span></span>

<span data-ttu-id="66241-168">W trakcie uruchamiania hello HMaster wykonuje wiele kroków inicjowania.</span><span class="sxs-lookup"><span data-stu-id="66241-168">During hello startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="66241-169">Dotyczy to przenoszenia danych od początku hello (TMP) danych toohello folderu.</span><span class="sxs-lookup"><span data-stu-id="66241-169">These include moving data from hello scratch (.tmp) folder toohello data folder.</span></span> <span data-ttu-id="66241-170">HMaster również analizuje toosee folderu dzienników z wyprzedzeniem zapisu (WALs) hello przypadku serwerom odpowiadać regionu i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="66241-170">HMaster also looks at hello write-ahead logs (WALs) folder toosee if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="66241-171">Podczas uruchamiania HMaster jest podstawowy `list` polecenia w tych folderach.</span><span class="sxs-lookup"><span data-stu-id="66241-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="66241-172">Jeśli w dowolnym momencie HMaster widzi nieoczekiwany plik w żadnym z tych folderów, zgłasza wyjątek, a nie uruchamia.</span><span class="sxs-lookup"><span data-stu-id="66241-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="66241-173">Prawdopodobna przyczyna</span><span class="sxs-lookup"><span data-stu-id="66241-173">Probable cause</span></span>

<span data-ttu-id="66241-174">W dziennikach serwera region hello spróbuj osi czasu hello tooidentify hello utworzenia pliku, a następnie sprawdź, czy było tworzone awarii procesu wokół hello czasu hello pliku.</span><span class="sxs-lookup"><span data-stu-id="66241-174">In hello region server logs, try tooidentify hello timeline of hello file creation, and then see if there was a process crash around hello time hello file was created.</span></span> <span data-ttu-id="66241-175">(Skontaktuj się z tooassist obsługi bazy danych HBase w ten sposób.) Dzięki temu nam zapewniają bardziej niezawodne mechanizmy, tak, aby uniknąć naciśnięcie tego błędu i upewnij się, proces bezpiecznego zamknięcia systemu.</span><span class="sxs-lookup"><span data-stu-id="66241-175">(Contact HBase support tooassist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="66241-176">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="66241-176">Resolution steps</span></span>

<span data-ttu-id="66241-177">Stos wywołań hello i spróbuj toodetermine folderów, które mogą być przyczyną problemu hello (na przykład może to być hello WALs folder lub TMP hello).</span><span class="sxs-lookup"><span data-stu-id="66241-177">Check hello call stack and try toodetermine which folder might be causing hello problem (for instance, it might be hello WALs folder or hello .tmp folder).</span></span> <span data-ttu-id="66241-178">Następnie w Eksploratorze chmury lub za pomocą poleceń systemu plików HDFS, spróbuj toolocate hello problem pliku.</span><span class="sxs-lookup"><span data-stu-id="66241-178">Then, in Cloud Explorer or by using HDFS commands, try toolocate hello problem file.</span></span> <span data-ttu-id="66241-179">Zazwyczaj jest to \*-renamePending.json pliku.</span><span class="sxs-lookup"><span data-stu-id="66241-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="66241-180">(hello \*— plik renamePending.json jest plik dziennika, który został użyty operacji zmiany nazwy atomic hello tooimplement hello WASB sterownika.</span><span class="sxs-lookup"><span data-stu-id="66241-180">(hello \*-renamePending.json file is a journal file that's used tooimplement hello atomic rename operation in hello WASB driver.</span></span> <span data-ttu-id="66241-181">Właściwym toobugs w tej implementacji, te pliki mogą pozostać za pośrednictwem po awarii procesów itd.) Wymuś Usuń ten plik w Eksploratorze chmury lub za pomocą poleceń systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="66241-181">Due toobugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="66241-182">Czasami może znajdować się plik tymczasowy o nazwie przypominać *$$$. $$$* w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="66241-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="66241-183">Masz toouse HDFS `ls` polecenie toosee tego pliku; nie widać hello plików w Eksploratorze chmury.</span><span class="sxs-lookup"><span data-stu-id="66241-183">You have toouse HDFS `ls` command toosee this file; you cannot see hello file in Cloud Explorer.</span></span> <span data-ttu-id="66241-184">toodelete ten plik, użyj hello systemu plików HDFS polecenia `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="66241-184">toodelete this file, use hello HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="66241-185">Po uruchomieniu tych poleceń, HMaster należy zacząć od razu.</span><span class="sxs-lookup"><span data-stu-id="66241-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="66241-186">Błąd</span><span class="sxs-lookup"><span data-stu-id="66241-186">Error</span></span>

<span data-ttu-id="66241-187">Żaden adres serwera znajduje się w *hbase: meta* dla regionu xxx.</span><span class="sxs-lookup"><span data-stu-id="66241-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="66241-188">Szczegółowy opis</span><span class="sxs-lookup"><span data-stu-id="66241-188">Detailed description</span></span>

<span data-ttu-id="66241-189">Może pojawić się komunikat w klastrze systemu Linux, która wskazuje, że hello *hbase: meta* tabeli nie jest w trybie online.</span><span class="sxs-lookup"><span data-stu-id="66241-189">You might see a message on your Linux cluster that indicates that hello *hbase: meta* table is not online.</span></span> <span data-ttu-id="66241-190">Uruchomiona `hbck` może raportować który "hbase: meta tabeli replicaId 0 nie została znaleziona na dowolny region."</span><span class="sxs-lookup"><span data-stu-id="66241-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="66241-191">Witaj może to oznaczać HMaster nie można zainicjować po ponownym uruchomieniu bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="66241-191">hello problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="66241-192">W dziennikach HMaster hello, można napotkać wiadomość hello: "żaden adres serwera na liście hbase: meta dla regionu hbase: kopii zapasowej \<nazwa regionu\>".</span><span class="sxs-lookup"><span data-stu-id="66241-192">In hello HMaster logs, you might see hello message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="66241-193">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="66241-193">Resolution steps</span></span>

1. <span data-ttu-id="66241-194">W hello powłoki HBase wprowadź hello następującego polecenia (zmiana wartości rzeczywistych zgodnie z wymaganiami):</span><span class="sxs-lookup"><span data-stu-id="66241-194">In hello HBase shell, enter hello following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="66241-195">Usuń hello *hbase: przestrzeń nazw* wpisu.</span><span class="sxs-lookup"><span data-stu-id="66241-195">Delete hello *hbase: namespace* entry.</span></span> <span data-ttu-id="66241-196">Ten wpis może być hello sam błąd, który jest zgłaszane, gdy hello *hbase: przestrzeń nazw* jest skanowany w tabeli.</span><span class="sxs-lookup"><span data-stu-id="66241-196">This entry might be hello same error that's being reported when hello *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="66241-197">toobring zapasową bazy danych HBase w stanie uruchomienia, w hello interfejsu użytkownika narzędzia Ambari, uruchom ponownie usługę Active HMaster hello.</span><span class="sxs-lookup"><span data-stu-id="66241-197">toobring up HBase in a running state, in hello Ambari UI, restart hello Active HMaster service.</span></span>  

4. <span data-ttu-id="66241-198">W hello powłoki HBase, toobring wszystkie tabele w trybie offline, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="66241-198">In hello HBase shell, toobring up all offline tables, run hello following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="66241-199">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="66241-199">Additional reading</span></span>

[<span data-ttu-id="66241-200">Tabeli HBase hello tooprocess</span><span class="sxs-lookup"><span data-stu-id="66241-200">Unable tooprocess hello HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="66241-201">Błąd</span><span class="sxs-lookup"><span data-stu-id="66241-201">Error</span></span>

<span data-ttu-id="66241-202">Limit czasu HMaster z too"java.io.IOException podobne wyjątek krytyczny: 300000ms upłynął limit czasu oczekiwania na przestrzeni nazw tabeli toobe przypisane."</span><span class="sxs-lookup"><span data-stu-id="66241-202">HMaster times out with a fatal exception similar too"java.io.IOException: Timedout 300000ms waiting for namespace table toobe assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="66241-203">Szczegółowy opis</span><span class="sxs-lookup"><span data-stu-id="66241-203">Detailed description</span></span>

<span data-ttu-id="66241-204">Ten problem może wystąpić, jeśli masz wiele tabel i regionów, które nie zostały opróżnione po ponownym uruchomieniu usługi HMaster.</span><span class="sxs-lookup"><span data-stu-id="66241-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="66241-205">Ponowne uruchomienie może zakończyć się niepowodzeniem i pojawi się hello poprzedzających komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="66241-205">Restart might fail, and you'll see hello preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="66241-206">Prawdopodobna przyczyna</span><span class="sxs-lookup"><span data-stu-id="66241-206">Probable cause</span></span>

<span data-ttu-id="66241-207">Jest to znany problem dotyczący hello HMaster usługi.</span><span class="sxs-lookup"><span data-stu-id="66241-207">This is a known issue with hello HMaster service.</span></span> <span data-ttu-id="66241-208">Zadania uruchamiania ogólne klastra może zająć dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="66241-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="66241-209">HMaster zamknięty, ponieważ hello przestrzeni nazw tabeli nie jest jeszcze przypisana.</span><span class="sxs-lookup"><span data-stu-id="66241-209">HMaster shuts down because hello namespace table isn’t yet assigned.</span></span> <span data-ttu-id="66241-210">Dzieje się tak tylko w scenariuszach, w którym dużych ilości danych unflushed istnieje i nie wystarcza limitem czasu równym 5 minut.</span><span class="sxs-lookup"><span data-stu-id="66241-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="66241-211">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="66241-211">Resolution steps</span></span>

1. <span data-ttu-id="66241-212">W hello interfejsu użytkownika narzędzia Ambari, przejdź do pozycji zbyt**HBase** > **Configs**.</span><span class="sxs-lookup"><span data-stu-id="66241-212">In hello Ambari UI, go too**HBase** > **Configs**.</span></span> <span data-ttu-id="66241-213">W pliku niestandardowej bazy danych hbase-site.xml hello Dodaj hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="66241-213">In hello custom hbase-site.xml file, add hello following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="66241-214">Uruchom ponownie usługi hello wymagane (HMaster i prawdopodobnie innych usług HBase).</span><span class="sxs-lookup"><span data-stu-id="66241-214">Restart hello required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="66241-215">Na serwerze regionu co powoduje błąd ponownego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="66241-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="66241-216">Problem</span><span class="sxs-lookup"><span data-stu-id="66241-216">Issue</span></span>

<span data-ttu-id="66241-217">Błąd ponownego uruchomienia na serwerze, na region może być niemożliwe przez następujące najlepsze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="66241-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="66241-218">Zaleca się wstrzymanie działania mocno obciążone, planując toorestart HBase region serwerów.</span><span class="sxs-lookup"><span data-stu-id="66241-218">We recommend that you pause heavy workload activity when you are planning toorestart HBase region servers.</span></span> <span data-ttu-id="66241-219">Jeśli tooconnect z regionu serwerów aplikacji będzie nadal występować, gdy trwa zamykanie, operacji ponownego uruchomienia serwera region hello będzie przebiegać wolniej za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="66241-219">If an application continues tooconnect with region servers when shutdown is in progress, hello region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="66241-220">Jest również dobrym rozwiązaniem toofirst opróżniania hello wszystkich tabel.</span><span class="sxs-lookup"><span data-stu-id="66241-220">Also, it's a good idea toofirst flush all hello tables.</span></span> <span data-ttu-id="66241-221">Odwołania dotyczące tooflush tabele, zobacz [HDInsight HBase: jak klaster HBase hello tooimprove ponownym przez opróżnianie tabel](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span><span class="sxs-lookup"><span data-stu-id="66241-221">For a reference on how tooflush tables, see [HDInsight HBase: How tooimprove hello HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="66241-222">Jeśli użytkownik inicjuje hello operacji ponownego uruchomienia na serwerach region HBase z hello interfejsu użytkownika narzędzia Ambari, natychmiast zobaczysz czy serwery region hello zakończył działanie, ale nie ich ponownego uruchomienia od razu.</span><span class="sxs-lookup"><span data-stu-id="66241-222">If you initiate hello restart operation on HBase region servers from hello Ambari UI, you immediately see that hello region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="66241-223">Oto, co dzieje się w tle hello:</span><span class="sxs-lookup"><span data-stu-id="66241-223">Here's what's happening behind hello scenes:</span></span> 

1. <span data-ttu-id="66241-224">Witaj Ambari agent wysyła serwer region toohello żądania zatrzymania.</span><span class="sxs-lookup"><span data-stu-id="66241-224">hello Ambari agent sends a stop request toohello region server.</span></span>
2. <span data-ttu-id="66241-225">Hello Ambari agent czeka na 30 sekund na powitania region serwera tooshut w dół bezpiecznie zamknąć.</span><span class="sxs-lookup"><span data-stu-id="66241-225">hello Ambari agent waits for 30 seconds for hello region server tooshut down gracefully.</span></span> 
3. <span data-ttu-id="66241-226">Jeśli aplikacja nadal tooconnect z serwerem region hello, powitania serwera nie będą natychmiast zamknięty.</span><span class="sxs-lookup"><span data-stu-id="66241-226">If your application continues tooconnect with hello region server, hello server won't shut down immediately.</span></span> <span data-ttu-id="66241-227">limit czasu 30 sekund Hello wygasa, zanim nastąpi jego zamknięcia.</span><span class="sxs-lookup"><span data-stu-id="66241-227">hello 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="66241-228">Po 30 sekund, hello Ambari agent wysyła życie polecenia kill (`kill -9`) serwera region toohello polecenia.</span><span class="sxs-lookup"><span data-stu-id="66241-228">After 30 seconds, hello Ambari agent sends a force-kill (`kill -9`) command toohello region server.</span></span> <span data-ttu-id="66241-229">Można to zobaczyć w dzienniku agenta ambari hello (w /var hello/dziennika/katalogu węzła procesu roboczego odpowiednich hello):</span><span class="sxs-lookup"><span data-stu-id="66241-229">You can see this in hello ambari-agent log (in hello /var/log/ directory of hello respective worker node):</span></span>

   ```apache
           2017-03-21 13:22:09,171 - Execute['/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/current/hbase-regionserver/conf stop regionserver'] {'only_if': 'ambari-sudo.sh  -H -E t
           est -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1', 'on_timeout': '! ( ambari-sudo.sh  -H -E test -
           f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H 
           -E cat /var/run/hbase/hbase-hbase-regionserver.pid`', 'timeout': 30, 'user': 'hbase'}
           2017-03-21 13:22:40,268 - Executing '! ( ambari-sudo.sh  -H -E test -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >
           /dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid`'. Reason: Execution of 'ambari-sudo.sh su hbase -l -s /bin/bash -c 'export  
           PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/var/lib/ambari-agent ; /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/curre
           nt/hbase-regionserver/conf stop regionserver was killed due timeout after 30 seconds
           2017-03-21 13:22:40,285 - File['/var/run/hbase/hbase-hbase-regionserver.pid'] {'action': ['delete']}
           2017-03-21 13:22:40,285 - Deleting File['/var/run/hbase/hbase-hbase-regionserver.pid']
   ```
<span data-ttu-id="66241-230">Ze względu na powitania niespodziewane wyłączanie port hello skojarzony z procesem hello może nie można zwolnić, nawet jeśli proces serwera region hello jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="66241-230">Because of hello abrupt shutdown, hello port associated with hello process might not be released, even though hello region server process is stopped.</span></span> <span data-ttu-id="66241-231">Taka sytuacja może prowadzić tooan AddressBindException podczas uruchamiania serwera region hello pokazane na powitania po dzienników.</span><span class="sxs-lookup"><span data-stu-id="66241-231">This situation can lead tooan AddressBindException when hello region server is starting, as shown in hello following logs.</span></span> <span data-ttu-id="66241-232">Można to sprawdzić w hello region-server.log w katalogu /var/log/hbase hello na powitania węzłów procesu roboczego, gdy serwer region hello nie toostart.</span><span class="sxs-lookup"><span data-stu-id="66241-232">You can verify this in hello region-server.log in hello /var/log/hbase directory on hello worker nodes where hello region server fails toostart.</span></span> 

   ```apache

   2017-03-21 13:25:47,061 ERROR [main] regionserver.HRegionServerCommandLine: Region server exiting
   java.lang.RuntimeException: Failed construction of Regionserver: class org.apache.hadoop.hbase.regionserver.HRegionServer
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2636)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.start(HRegionServerCommandLine.java:64)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.run(HRegionServerCommandLine.java:87)
   at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
   at org.apache.hadoop.hbase.util.ServerCommandLine.doMain(ServerCommandLine.java:126)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.main(HRegionServer.java:2651)
        
   Caused by: java.lang.reflect.InvocationTargetException
   at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
   at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
   at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2634)
   ... 5 more
        
   Caused by: java.net.BindException: Problem binding too/10.2.0.4:16020 : Address already in use
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2497)
   at org.apache.hadoop.hbase.ipc.RpcServer$Listener.<init>(RpcServer.java:580)
   at org.apache.hadoop.hbase.ipc.RpcServer.<init>(RpcServer.java:1982)
   at org.apache.hadoop.hbase.regionserver.RSRpcServices.<init>(RSRpcServices.java:863)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.createRpcServices(HRegionServer.java:632)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.<init>(HRegionServer.java:532)
   ... 10 more
        
   Caused by: java.net.BindException: Address already in use
   at sun.nio.ch.Net.bind0(Native Method)
   at sun.nio.ch.Net.bind(Net.java:463)
   at sun.nio.ch.Net.bind(Net.java:455)
   at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
   at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2495)
   ... 15 more
   ```

### <a name="resolution-steps"></a><span data-ttu-id="66241-233">Kroki rozwiązania</span><span class="sxs-lookup"><span data-stu-id="66241-233">Resolution steps</span></span>

1. <span data-ttu-id="66241-234">Spróbuj tooreduce obciążenia hello hello HBase region serwerów, przed rozpoczęciem ponownego uruchomienia komputera.</span><span class="sxs-lookup"><span data-stu-id="66241-234">Try tooreduce hello load on hello HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="66241-235">Można również polecenia (Jeśli krok 1 nie Pomoc), spróbuj toomanually ponowne uruchomienie region hello serwerów na powitania węzłów procesu roboczego przy użyciu następującego:</span><span class="sxs-lookup"><span data-stu-id="66241-235">Alternatively (if step 1 doesn't help), try toomanually restart region servers on hello worker nodes by using hello following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

