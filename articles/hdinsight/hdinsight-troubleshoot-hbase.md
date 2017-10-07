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
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a>Rozwiązywanie problemów z bazy danych HBase przy użyciu usługi Azure HDInsight

Dowiedz się więcej o hello Najważniejsze problemy i rozwiązania ich podczas pracy z bazy danych Apache HBase ładunków w Apache Ambari.

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a>Jak uruchomić raporty polecenie hbck z wielu regionach nieprzypisane

Typowe komunikat o błędzie, że można napotkać podczas uruchamiania hello `hbase hbck` polecenie jest "wiele regionów trwa nieprzypisane lub luk w łańcuchu hello regionów."

Numer hello regionów, które są niezrównoważone na wszystkich serwerach regionie można wyświetlić w hello głównego HBase interfejsu użytkownika. Następnie można uruchomić `hbase hbck` polecenia toosee luk w łańcuchu region hello.

Luk może być spowodowane hello regionach w trybie offline, tak przydziały hello poprawka najpierw. 

toobring hello nieprzypisane regionów wstecz tooa normalnym stanie, ukończyć powitalnych następujące kroki:

1. Zaloguj się toohello klastra HDInsight HBase przy użyciu protokołu SSH.
2. tooconnect z hello dozorcy powłoki, uruchom hello `hbase zkcli` polecenia.
3. Uruchom hello `rmr /hbase/regions-in-transition` polecenia lub hello `rmr /hbase-unsecure/regions-in-transition` polecenia.
4. tooexit z hello `hbase zkcli` powłoki, użyj hello `exit` polecenia.
5. Otwórz hello Apache Ambari w interfejsie użytkownika i ponownie uruchom usługę Active głównego HBase hello.
6. Uruchom hello `hbase hbck` polecenia ponownie (bez żadnych opcji). Sprawdź dane wyjściowe hello tooensure tego polecenia, przypisanych wszystkich regionach.


## <a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Jak rozwiązać problemy z limitu czasu, korzystając z polecenia hbck przypisania region

### <a name="issue"></a>Problem

Potencjalną przyczyną problemów limitu czasu, gdy używasz hello `hbck` polecenie może być czy kilku regionach w hello "w ramach przejścia" stanie przez dłuższy czas. Regionach jest widoczny jako w trybie offline w hello głównego HBase interfejsu użytkownika. Ponieważ dużej liczby regionów próbujesz tootransition, wzorca bazy danych HBase może limitu czasu i być toobring regionach ponownie do trybu online.

### <a name="resolution-steps"></a>Kroki rozwiązania

1. Zaloguj się toohello klastra HDInsight HBase przy użyciu protokołu SSH.
2. tooconnect z hello dozorcy powłoki, uruchom hello `hbase zkcli` polecenia.
3. Uruchom hello `rmr /hbase/regions-in-transition` lub hello `rmr /hbase-unsecure/regions-in-transition` polecenia.
4. Witaj tooexit `hbase zkcli` powłoki, użyj hello `exit` polecenia.
5. W hello interfejsu użytkownika narzędzia Ambari Uruchom ponownie usługę Active głównego HBase hello.
6. Uruchom hello `hbase hbck -fixAssignments` polecenie ponownie.

## <a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Jak I Wymuś. Wyłącz tryb awaryjny systemu plików HDFS w klastrze

### <a name="issue"></a>Problem

powitalne lokalnego Hadoop Distributed pliku System (HDFS) jest zablokowana w trybie awaryjnym w klastrze usługi HDInsight hello.

### <a name="detailed-description"></a>Szczegółowy opis

Przyczyną tego błędu może być awarii po uruchomieniu hello następujące polecenia w systemie plików HDFS:

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

Błąd Hello, które można napotkać podczas próby toorun hello polecenia wygląda następująco:

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

### <a name="probable-cause"></a>Prawdopodobna przyczyna

Witaj klastra usługi HDInsight został skalowany w dół tooa bardzo kilku węzłów. Witaj liczba węzłów znajduje się poniżej lub zamknąć współczynnik replikacji systemu plików HDFS toohello.

### <a name="resolution-steps"></a>Kroki rozwiązania 

1. Pobierz stan hello powitalne klastra systemu plików HDFS na powitania HDInsight, uruchamiając następujące polecenia hello:

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
2. Również można sprawdzić integralność hello powitalne klastra systemu plików HDFS na powitania HDInsight przy użyciu hello następującego polecenia:

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

3. Jeśli okaże się, że nie ma żadnych bloków brakujące, uszkodzony lub under-replikowanych lub te bloki można zignorować, uruchom następujące polecenie tootake hello nazwa węzła tryb awaryjny hello:

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a>Jak rozwiązać łączności JDBC lub SQLLine problemy z Apache Phoenix

### <a name="resolution-steps"></a>Kroki rozwiązania

tooconnect z Phoenix, musisz podać adres IP hello aktywnego węzła dozorcy. Upewnij się, że hello dozorcy sqlline.py toowhich usługa próbuje tooconnect jest uruchomiona.
1. Zaloguj się toohello klastra usługi HDInsight przy użyciu protokołu SSH.
2. Wprowadź hello następujące polecenie:
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > Adres IP hello hello aktywnego węzła dozorcy możesz pobrać ze strony hello interfejsu użytkownika narzędzia Ambari. Przejdź za**HBase** > **szybkie linki** > **ZK\* (aktywny)** > **informacji dozorcy**. 

3. Jeśli hello sqlline.py łączy tooPhoenix i jest nie limitu czasu, hello uruchom następujące polecenie toovalidate hello dostępności i kondycji Phoenix:

   ```apache
           !tables
           !quit
   ```      
4. Jeśli to polecenie działa, nie ma żadnych problem. adres IP Hello podany przez użytkownika hello mogą być niepoprawne. Jeśli polecenie hello wstrzymuje przez dłuższy czas, a następnie wyświetla hello następujący błąd, jednak toostep 5.

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. Uruchom hello poniższych poleceń z hello węzła głównego (hn0) toodiagnose hello warunek hello Phoenix systemu. Tabela katalogu:

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   polecenie Hello powinny zostać zwrócone następujące toohello podobne w błąd: 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. W hello interfejsu użytkownika narzędzia Ambari wykonaj następujące kroki toorestart hello HMaster usługi na wszystkich węzłach dozorcy hello:

    1. W hello **Podsumowanie** sekcji hbase, przejdź zbyt**HBase** > **głównego HBase aktywny**. 
    2. W hello **składniki** sekcji, uruchom ponownie usługę głównego HBase hello.
    3. Powtórz te kroki dla wszystkich pozostałych **głównego HBase wstrzymania** usług. 

Można podjąć toofive minut hello głównego HBase usługi toostabilize i Zakończ proces odzyskiwania hello. Po kilku minutach Powtórz hello sqlline.py polecenia tooconfirm tego hello systemu. Tabela katalogu jest uruchomiony i że można tworzyć zapytania. 

Gdy hello systemu. Tabela katalogu zapasowego toonormal, tooPhoenix problem łączności hello powinien zostać automatycznie rozwiązane.


## <a name="what-causes-a-master-server-toofail-toostart"></a>Co powoduje, że serwer główny toofail toostart

### <a name="error"></a>Błąd 

Niepodzielne zmiany nazwy awarii.

### <a name="detailed-description"></a>Szczegółowy opis

W trakcie uruchamiania hello HMaster wykonuje wiele kroków inicjowania. Dotyczy to przenoszenia danych od początku hello (TMP) danych toohello folderu. HMaster również analizuje toosee folderu dzienników z wyprzedzeniem zapisu (WALs) hello przypadku serwerom odpowiadać regionu i tak dalej. 

Podczas uruchamiania HMaster jest podstawowy `list` polecenia w tych folderach. Jeśli w dowolnym momencie HMaster widzi nieoczekiwany plik w żadnym z tych folderów, zgłasza wyjątek, a nie uruchamia.  

### <a name="probable-cause"></a>Prawdopodobna przyczyna

W dziennikach serwera region hello spróbuj osi czasu hello tooidentify hello utworzenia pliku, a następnie sprawdź, czy było tworzone awarii procesu wokół hello czasu hello pliku. (Skontaktuj się z tooassist obsługi bazy danych HBase w ten sposób.) Dzięki temu nam zapewniają bardziej niezawodne mechanizmy, tak, aby uniknąć naciśnięcie tego błędu i upewnij się, proces bezpiecznego zamknięcia systemu.

### <a name="resolution-steps"></a>Kroki rozwiązania

Stos wywołań hello i spróbuj toodetermine folderów, które mogą być przyczyną problemu hello (na przykład może to być hello WALs folder lub TMP hello). Następnie w Eksploratorze chmury lub za pomocą poleceń systemu plików HDFS, spróbuj toolocate hello problem pliku. Zazwyczaj jest to \*-renamePending.json pliku. (hello \*— plik renamePending.json jest plik dziennika, który został użyty operacji zmiany nazwy atomic hello tooimplement hello WASB sterownika. Właściwym toobugs w tej implementacji, te pliki mogą pozostać za pośrednictwem po awarii procesów itd.) Wymuś Usuń ten plik w Eksploratorze chmury lub za pomocą poleceń systemu plików HDFS. 

Czasami może znajdować się plik tymczasowy o nazwie przypominać *$$$. $$$* w tej lokalizacji. Masz toouse HDFS `ls` polecenie toosee tego pliku; nie widać hello plików w Eksploratorze chmury. toodelete ten plik, użyj hello systemu plików HDFS polecenia `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.  

Po uruchomieniu tych poleceń, HMaster należy zacząć od razu. 

### <a name="error"></a>Błąd

Żaden adres serwera znajduje się w *hbase: meta* dla regionu xxx.

### <a name="detailed-description"></a>Szczegółowy opis

Może pojawić się komunikat w klastrze systemu Linux, która wskazuje, że hello *hbase: meta* tabeli nie jest w trybie online. Uruchomiona `hbck` może raportować który "hbase: meta tabeli replicaId 0 nie została znaleziona na dowolny region." Witaj może to oznaczać HMaster nie można zainicjować po ponownym uruchomieniu bazy danych HBase. W dziennikach HMaster hello, można napotkać wiadomość hello: "żaden adres serwera na liście hbase: meta dla regionu hbase: kopii zapasowej \<nazwa regionu\>".  

### <a name="resolution-steps"></a>Kroki rozwiązania

1. W hello powłoki HBase wprowadź hello następującego polecenia (zmiana wartości rzeczywistych zgodnie z wymaganiami):  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. Usuń hello *hbase: przestrzeń nazw* wpisu. Ten wpis może być hello sam błąd, który jest zgłaszane, gdy hello *hbase: przestrzeń nazw* jest skanowany w tabeli.

3. toobring zapasową bazy danych HBase w stanie uruchomienia, w hello interfejsu użytkownika narzędzia Ambari, uruchom ponownie usługę Active HMaster hello.  

4. W hello powłoki HBase, toobring wszystkie tabele w trybie offline, uruchom następujące polecenie hello:

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a>Dodatkowe materiały

[Tabeli HBase hello tooprocess](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a>Błąd

Limit czasu HMaster z too"java.io.IOException podobne wyjątek krytyczny: 300000ms upłynął limit czasu oczekiwania na przestrzeni nazw tabeli toobe przypisane."

### <a name="detailed-description"></a>Szczegółowy opis

Ten problem może wystąpić, jeśli masz wiele tabel i regionów, które nie zostały opróżnione po ponownym uruchomieniu usługi HMaster. Ponowne uruchomienie może zakończyć się niepowodzeniem i pojawi się hello poprzedzających komunikat o błędzie.  

### <a name="probable-cause"></a>Prawdopodobna przyczyna

Jest to znany problem dotyczący hello HMaster usługi. Zadania uruchamiania ogólne klastra może zająć dużo czasu. HMaster zamknięty, ponieważ hello przestrzeni nazw tabeli nie jest jeszcze przypisana. Dzieje się tak tylko w scenariuszach, w którym dużych ilości danych unflushed istnieje i nie wystarcza limitem czasu równym 5 minut.
  
### <a name="resolution-steps"></a>Kroki rozwiązania

1. W hello interfejsu użytkownika narzędzia Ambari, przejdź do pozycji zbyt**HBase** > **Configs**. W pliku niestandardowej bazy danych hbase-site.xml hello Dodaj hello następujące ustawienia: 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. Uruchom ponownie usługi hello wymagane (HMaster i prawdopodobnie innych usług HBase).  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a>Na serwerze regionu co powoduje błąd ponownego uruchomienia

### <a name="issue"></a>Problem

Błąd ponownego uruchomienia na serwerze, na region może być niemożliwe przez następujące najlepsze rozwiązania. Zaleca się wstrzymanie działania mocno obciążone, planując toorestart HBase region serwerów. Jeśli tooconnect z regionu serwerów aplikacji będzie nadal występować, gdy trwa zamykanie, operacji ponownego uruchomienia serwera region hello będzie przebiegać wolniej za kilka minut. Jest również dobrym rozwiązaniem toofirst opróżniania hello wszystkich tabel. Odwołania dotyczące tooflush tabele, zobacz [HDInsight HBase: jak klaster HBase hello tooimprove ponownym przez opróżnianie tabel](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).

Jeśli użytkownik inicjuje hello operacji ponownego uruchomienia na serwerach region HBase z hello interfejsu użytkownika narzędzia Ambari, natychmiast zobaczysz czy serwery region hello zakończył działanie, ale nie ich ponownego uruchomienia od razu. 

Oto, co dzieje się w tle hello: 

1. Witaj Ambari agent wysyła serwer region toohello żądania zatrzymania.
2. Hello Ambari agent czeka na 30 sekund na powitania region serwera tooshut w dół bezpiecznie zamknąć. 
3. Jeśli aplikacja nadal tooconnect z serwerem region hello, powitania serwera nie będą natychmiast zamknięty. limit czasu 30 sekund Hello wygasa, zanim nastąpi jego zamknięcia. 
4. Po 30 sekund, hello Ambari agent wysyła życie polecenia kill (`kill -9`) serwera region toohello polecenia. Można to zobaczyć w dzienniku agenta ambari hello (w /var hello/dziennika/katalogu węzła procesu roboczego odpowiednich hello):

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
Ze względu na powitania niespodziewane wyłączanie port hello skojarzony z procesem hello może nie można zwolnić, nawet jeśli proces serwera region hello jest zatrzymana. Taka sytuacja może prowadzić tooan AddressBindException podczas uruchamiania serwera region hello pokazane na powitania po dzienników. Można to sprawdzić w hello region-server.log w katalogu /var/log/hbase hello na powitania węzłów procesu roboczego, gdy serwer region hello nie toostart. 

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

### <a name="resolution-steps"></a>Kroki rozwiązania

1. Spróbuj tooreduce obciążenia hello hello HBase region serwerów, przed rozpoczęciem ponownego uruchomienia komputera. 
2. Można również polecenia (Jeśli krok 1 nie Pomoc), spróbuj toomanually ponowne uruchomienie region hello serwerów na powitania węzłów procesu roboczego przy użyciu następującego:

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

