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
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a>Użyj Oozie z Hadoop toodefine i uruchomić przepływ pracy na HDInsight opartych na systemie Linux

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

Dowiedz się, jak toouse Apache Oozie z platformą Hadoop w usłudze HDInsight. Apache Oozie to system koordynacji/przepływu pracy, który zarządza zadaniami na platformie Hadoop. Oozie jest zintegrowany z hello stosem platformy Hadoop i obsługuje hello następujące zadania:

* Apache MapReduce
* Apache Pig
* Apache Hive
* Apache Sqoop

Oozie mogą być również używane tooschedule zadania, które są określone tooa systemu, np. programów Java lub skryptów powłoki

> [!NOTE]
> Inną opcją w przypadku definiowania przepływów pracy z usługą HDInsight jest fabryki danych Azure. toolearn więcej informacji na temat fabryki danych Azure, zobacz [Use Pig i Hive z fabryką danych][azure-data-factory-pig-hive].

> [!IMPORTANT]
> Oozie nie jest włączona w usłudze HDInsight z przyłączonych do domeny.

## <a name="prerequisites"></a>Wymagania wstępne

* **Klaster usługi HDInsight**: zobacz [Rozpoczynanie pracy z usługą HDInsight w systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

  > [!IMPORTANT]
  > kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="example-workflow"></a>Przykładowy przepływ pracy

przepływ pracy Hello używane w tym dokumencie zawiera dwa działania. Akcje są definicje dla zadania, takie jak uruchomienie Hive, Sqoop, MapReduce lub inny proces:

![Diagram przepływu pracy][img-workflow-diagram]

1. Akcja Hive uruchamia skrypt HiveQL tooextract rekordy z hello **hivesampletable** dołączone do usługi HDInsight. Każdy wiersz danych opisuje odwiedziny od określonego urządzenia przenośnego. format rekordu Hello zostaną wyświetlone podobne toohello następującego tekstu:

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    Witaj skryptu Hive używane w tym dokumencie zlicza hello łączna liczba wizyt dla poszczególnych platform (takich jak Android lub iPhone) i przechowuje hello liczby tooa nową tabelę programu Hive.

    Aby uzyskać więcej informacji na temat programu Hive, zobacz temat [Use Hive with HDInsight][hdinsight-use-hive] (Korzystanie z programu Hive z usługą HDInsight).

2. Akcja Sqoop eksportuje zawartość hello hello nowej gałęzi tooa tabeli w bazie danych Azure SQL. Aby uzyskać więcej informacji o Sqoop, zobacz [Hadoop Sqoop użycia z usługą HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Obsługiwane wersje Oozie w klastrach HDInsight, zobacz [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight][hdinsight-versions].

## <a name="create-hello-working-directory"></a>Utwórz katalog roboczy hello

Oozie oczekuje zasoby wymagane toobe zadania przechowywane w hello sam katalogu. W tym przykładzie użyto **wasb: / / / samouczki/useoozie**. Ten katalog i katalog danych hello przechowujący hello nową tabelę programu Hive utworzone przez ten przepływ pracy, należy użyć następującego polecenia toocreate hello:

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> Witaj `-p` parametr powoduje, że wszystkie katalogi w toobe ścieżka hello utworzony. Witaj **danych** katalog jest używany toohold dane używane przez hello **useooziewf.hql** skryptu.

Również uruchomić następujące polecenie, które zapewnia, że Oozie mogą personifikować konta użytkownika podczas uruchamiania zadań Hive i Sqoop hello. Zastąp **USERNAME** z nazwy logowania:

```
sudo adduser USERNAME users
```

> [!NOTE]
> Błędy można zignorować ten użytkownik hello jest już członkiem hello `users` grupy.

## <a name="add-a-database-driver"></a>Dodaj sterownik bazy danych

Ponieważ ten przepływ pracy używa Sqoop tooexport danych tooSQL bazy danych, należy udostępnić kopię sterownik JDBC hello używane tooSQL tootalk bazy danych. Użyj hello następujące polecenia toocopy on toohello katalogu roboczego:

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

Jeśli przepływ pracy używane inne zasoby, takie jak jar zawierający aplikację MapReduce, będzie potrzebny tooadd także tych zasobów.

## <a name="define-hello-hive-query"></a>Zdefiniuj zapytanie Hive hello

Użyj hello następujące kroki toocreate skrypt HiveQL, który definiuje kwerendę, która jest używana w przepływie pracy Oozie w dalszej części tego dokumentu.

1. Połącz toohello klastra przy użyciu protokołu SSH. Witaj następujące polecenie jest przykładem przy użyciu hello `ssh` polecenia. Zastąp __USERNAME__ użytkownika SSH hello hello klastra. Zastąp __CLUSTERNAME__ o nazwie hello hello klastra usługi HDInsight.

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Hello połączenia SSH używając hello następujące polecenia toocreate pliku:

    ```
    nano useooziewf.hql
    ```

3. Po otwarciu edytora nano hello Użyj następującego zapytania jako hello zawartość pliku hello hello:

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    Istnieją dwie zmienne używane w skrypcie hello:

    * **${hiveTableName}**: zawiera nazwę hello toobe tabeli hello utworzone

    * **${hiveDataFolder}**: plikami hello lokalizacji toostore hello danych dla tabeli hello

    Plik definicji przepływu pracy Hello (workflow.xml w tym samouczku) przekazuje te wartości toothis skrypt HiveQL w czasie wykonywania

4. Edytor hello tooexit, naciśnij klawisze Ctrl-X. Po wyświetleniu monitu wybierz **Y** toosave hello pliku, a następnie użyj **Enter** toouse hello **useooziewf.hql** nazwę pliku.

5. Użyj następujących hello polecenia toocopy **useooziewf.hql** za**wasb:///tutorials/useoozie/useooziewf.hql**:

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    Te polecenia przechowywania hello **useooziewf.hql** pliku w magazynie hello zgodnego systemem plików HDFS hello klastra.

## <a name="define-hello-workflow"></a>Zdefiniuj hello przepływu pracy

Oozie definicje przepływów pracy są zapisywane w hPDL (XML procesu Definition Language). Użyj hello następującego przepływu pracy hello toodefine kroki:

1. Za pomocą powitania po instrukcji toocreate i edytować plik:

    ```
    nano workflow.xml
    ```

2. Po otwarciu edytora nano hello wprowadź powitania po XML jako zawartość pliku hello:

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

    Istnieją dwie akcje zdefiniowane w przepływie pracy hello:

   * **RunHiveScript**: Ta akcja jest akcji uruchamiania hello i uruchamia hello **useooziewf.hql** wykonanie skryptu technologii Hive

   * **RunSqoopExport**: Ta akcja eksportuje dane hello utworzone na podstawie tooSQL skryptu Hive hello bazy danych przy użyciu Sqoop. Ta akcja działa tylko wtedy, jeśli hello **RunHiveScript** akcja zakończy się pomyślnie.

     przepływ pracy Hello ma kilka wpisów, takich jak `${jobTracker}`. Te wpisy są zastępowane przez wartości używanej w definicji zadania hello. Witaj definicji zadania jest tworzony w dalszej części tego dokumentu.

     Również Uwaga hello `<archive>sqljdbc4.jar</arcive>` wpis w sekcji Sqoop hello. Ten wpis informuje Oozie toomake to archiwum dostępne dla Sqoop po uruchomieniu tej akcji.

3. Następnie użyj klawiszy Ctrl-X **Y** i **Enter** toosave hello pliku.

4. Użyj hello następujące polecenie toocopy hello **workflow.xml** pliku zbyt**/tutorials/useoozie/workflow.xml**:

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a>Utwórz bazę danych hello

toocreate bazy danych SQL Azure, wykonaj kroki hello hello [Utwórz bazę danych SQL](../sql-database/sql-database-get-started.md) dokumentu. Podczas tworzenia hello bazy danych, użyj `oozietest` jako hello Nazwa bazy danych. Również Zanotuj nazwę hello powitania serwera bazy danych.

### <a name="create-hello-table"></a>Utwórz tabelę hello

> [!NOTE]
> Istnieje wiele sposobów tooconnect tooSQL bazy danych toocreate tabeli. Witaj, użyj czynności po [protokół FreeTDS](http://www.freetds.org/) z klastrem usługi HDInsight hello.


1. Użyj następującego polecenia tooinstall protokół FreeTDS w klastrze usługi HDInsight hello hello:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. Po zainstalowaniu protokół FreeTDS Użyj hello następujące polecenia tooconnect toohello bazy danych programu SQL server, utworzonej wcześniej:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    Pojawi się toohello podobne dane wyjściowe następującego tekstu:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. Na powitania `1>` monit, wprowadź hello następujące wiersze:

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    Gdy hello `GO` instrukcja została wprowadzona, poprzednie instrukcje hello są oceniane. Te instrukcje tworzenia tabeli o nazwie **mobiledata** używany przez hello przepływ pracy.

    Utworzono hello Użyj następującego tooverify, który hello tabeli:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Zostaną wyświetlone dane wyjściowe toohello podobne następującego tekstu:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. Wprowadź `exit` na powitania `1>` Monituj tooexit hello tsql narzędzia.

## <a name="create-hello-job-definition"></a>Tworzenie definicji zadania hello

definicji zadania Hello opisano, gdzie toofind hello workflow.xml. Opisano również where toofind inne pliki używane przez przepływ pracy hello (na przykład useooziewf.hql). Definiuje także hello wartości dla właściwości używane w przepływie pracy hello i skojarzone pliki.

1. Hello Użyj następującego polecenia tooget hello pełny adres hello domyślnego magazynu. Ten adres jest używany w pliku konfiguracyjnym hello później:

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    To polecenie zwraca informacje toohello podobne po XML:

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > Jeśli hello klastra usługi HDInsight używa magazynu Azure jako hello domyślny magazyn, hello `<value>` zaczynać zawartość elementu `wasb://`. Jeśli zamiast niego jest używana usługa Azure Data Lake Store, rozpoczyna się od `adl://`.

    Zapisz zawartość hello hello `<value>` elementu, ponieważ jest używany w następnych krokach hello.

2. Użyj hello następujące polecenie tooget FQDN hello headnode klastra. Te informacje są używane dla hello JobTracker adres klastra hello:

    ```
    hostname -f
    ```

    To polecenie zwróci informacje toohello podobne następującego tekstu:

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    Hello port używany do hello JobTracker jest 8050, tak aby hello toouse pełny adres dla hello JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.

3. Użyj powitania po toocreate hello Oozie zadania definicji konfiguracji:

    ```
    nano job.xml
    ```

4. Po otwarciu edytora nano hello Użyj powitania po XML jako hello zawartość pliku hello:

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

   * Zastąp wszystkie wystąpienia  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  z wartością hello otrzymany wcześniej do magazynu domyślnego.

     > [!WARNING]
     > Jeśli ścieżka hello jest `wasb` ścieżki, należy użyć hello pełną ścieżkę. Nie Skróć go toojust `wasb:///`.

   * Zastąp **JOBTRACKERADDRESS** z hello adres JobTracker/ResourceManager otrzymany wcześniej.
   * Zastąp **twojanazwa** nazwą logowania użytkownika hello klastra usługi HDInsight.
   * Zastąp **serverName**, **adminLogin**, i **adminPassword** hello informacje z bazy danych SQL Azure.

     Większość informacji hello w tym pliku jest używane toopopulate hello wartości używany w plikach workflow.xml lub ooziewf.hql hello (np. ${nameNode}.)

     > [!NOTE]
     > Witaj **oozie.wf.application.path** where definiuje ona toofind hello workflow.xml pliku, który zawiera hello przepływ pracy został uruchomiony przez to zadanie.

5. Następnie użyj klawiszy Ctrl-X **Y** i **Enter** toosave hello pliku.

## <a name="submit-and-manage-hello-job"></a>Prześlij i zarządzanie hello zadania

Hello poniższe kroki Użyj hello Oozie polecenia toosubmit i Zarządzaj przepływami pracy Oozie w klastrze hello. Przyjazny interfejs Hello polecenia Oozie znajduje się nad hello [interfejsu API REST Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

> [!IMPORTANT]
> Korzystając z polecenia Oozie hello, należy użyć dla hello HDInsight headnode hello nazwy FQDN. Ta nazwa FQDN jest dostępna tylko w klastrze hello lub jeśli hello klaster znajduje się w sieci wirtualnej platformy Azure, z innych komputerów na powitania tej samej sieci.


1. Użyj powitania po tooobtain hello adresu URL toohello Oozie usługi:

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    To polecenie zwróci toohello podobne informacje po XML:

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    Witaj `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` fragment jest hello toouse adres URL z hello Oozie polecenia.

2. Po toocreate zmienną środowiskową hello adresu URL, dzięki czemu nie trzeba tootype hello użyj go dla każdego polecenia:

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    Zamień adres URL hello hello jedną otrzymany wcześniej.
3. Użyj powitania po toosubmit hello zadania:

    ```
    oozie job -config job.xml -submit
    ```

    To polecenie ładuje informacje o zadaniu na powitania **job.xml** i przesyła tooOozie, ale nie, nie można go uruchomić.

    Po zakończeniu wykonywania polecenia hello powinien zostać zwrócony identyfikator hello hello zadania. Na przykład `0000005-150622124850154-oozie-oozi-W`. Ten identyfikator jest używany toomanage hello zadania.

4. Wyświetl stan hello hello zadania przy użyciu hello następujące polecenie:

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > Zastąp `<JOBID>` z hello identyfikator zwrócony hello poprzedniego kroku.

    To polecenie zwróci informacje toohello podobne następującego tekstu:

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

    To zadanie ma stan `PREP`. Ten stan wskazuje hello zadania został utworzony, ale nie jest uruchomiona.

5. Witaj Użyj następującego polecenia toostart hello zadania:

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > Zastąp `<JOBID>` z hello identyfikator zwrócony wcześniej.

    Jeśli po wykonaniu tego polecenia możesz sprawdzić stan hello, jest w stanie uruchomienia, a hello akcje w ramach zadania hello jest zwracane są informacje.

6. Po pomyślnym zakończeniu zadania hello, można sprawdzić, czy dane hello został wygenerowany i wyeksportować toohello tabela bazy danych SQL za pomocą następującego polecenia hello:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    Na powitania `1>` monit, wprowadź hello następujące zapytania:

    ```
    SELECT * FROM mobiledata
    GO
    ```

    zwrócone informacje Hello jest podobne toohello następującego tekstu:

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

Aby uzyskać więcej informacji na powitania polecenia Oozie, zobacz [narzędzia wiersza polecenia Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).

## <a name="oozie-rest-api"></a>Oozie interfejsu API REST

Witaj Oozie interfejsu API REST umożliwia toobuild własnych narzędzi, które współpracują z Oozie. HDInsight określone informacje na temat przy użyciu interfejsu API REST Oozie hello są następujące Hello:

* **Identyfikator URI**: hello interfejsu API REST można uzyskać z poza hello klastra`https://CLUSTERNAME.azurehdinsight.net/oozie`

* **Uwierzytelnianie**: uwierzytelniania toohello interfejsu API przy użyciu konta klastra HTTP hello (Administrator) i hasło. Na przykład:

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

Aby uzyskać więcej informacji na temat używania hello Oozie interfejsu API REST, zobacz [API usług sieci Web Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

## <a name="oozie-web-ui"></a>Oozie interfejsu użytkownika sieci Web

Hello Oozie interfejs sieci Web zawiera widok opartych na sieci web do stanu hello Oozie zadań w klastrze hello. Interfejs użytkownika sieci web Hello umożliwia hello tooview następujących informacji:

* Stan zadania
* Definicji zadania
* Konfiguracja
* Wykres hello akcje w zadaniu hello
* Dzienników hello zadania

Można również wyświetlić szczegóły dla działania w ramach zadania.

tooaccess hello Oozie interfejs sieci Web, użyj hello następujące kroki:

1. Tworzenie klastra usługi HDInsight toohello tunelu SSH. Aby uzyskać informacje, zobacz hello [Użyj SSH Tunneling z usługą HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) dokumentu.

2. Po utworzeniu tunelu, otwórz hello interfejsu użytkownika sieci web Ambari w przeglądarce sieci web. Witaj identyfikatora URI dla witryny Ambari hello jest **https://CLUSTERNAME.azurehdinsight.net**. Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight opartej na systemie Linux.

3. W lewej części strony hello hello, wybierz **Oozie**, następnie **szybkie linki**, a na końcu **Oozie interfejs sieci Web**.

    ![Obraz powitania menu](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. Witaj toodisplaying domyślne ustawienia interfejsu użytkownika sieci Web Oozie uruchomionych zadań przepływu pracy. Wybierz wszystkie zadania przepływu pracy, toosee **wszystkie zadania**.

    ![Wszystkie zadania wyświetlane](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. Wybierz więcej informacji o zadaniu hello tooview zadania.

    ![Informacji o zadaniu](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. Na karcie informacji o zadaniu hello możesz wyświetlać informacje podstawowe zadania i hello poszczególnych działań w ramach zadania hello. U góry hello, można wyświetlić przy użyciu karty hello hello definicji zadania, zadania konfiguracji, hello dostępu dziennik zadań i wyświetlanie skierowane acykliczne Graph (DAG) hello zadania.

   * **Dziennik zadań**: Wybierz hello **GetLogs** przycisk tooget wszystkich dzienników zadania hello, lub użyj hello **filtr wyszukiwania wprowadź** pola toofilter dzienniki

       ![Dziennik zadań](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * **JobDAG**: hello DAG jest graficznego przeglądu hello ścieżek danych przez przepływ pracy hello

       ![Zadanie DAG](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. Wybierając jedną z akcji hello z hello **informacji o zadaniu** kartę wyświetlenie informacji dotyczących hello akcji. Na przykład wybierz hello **RunHiveScript** akcji.

    ![Informacje o akcji](./media/hdinsight-use-oozie-linux-mac/action.png)

8. Aby wyświetlić szczegóły hello akcji, takich jak toohello łącze **adres URL konsoli**. To łącze mogą być używane tooview JobTracker informacje hello zadania.

## <a name="scheduling-jobs"></a>Planowanie zadań

Koordynator Hello umożliwia toospecify rozpoczęcia, zakończenia i wystąpienie częstotliwość zadań. toodefine harmonogram hello przepływu pracy, użyj hello następujące kroki:

1. Użyj powitania po toocreate plik o nazwie **coordinator.xml**:

    ```
    nano coordinator.xml
    ```

    Użyj powitania po XML jako hello zawartość pliku hello:

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
    > Witaj `${...}` zmienne są zastępowane przez wartości w definicji zadania hello w czasie wykonywania. zmienne Hello są:
    >
    > * `${coordFrequency}`: Czas między uruchomionych wystąpień hello zadania.
    > ** `${coordStart}`: godzina rozpoczęcia zadania hello.
    > * `${coordEnd}`: godzina zakończenia zadania hello.
    > * `${coordTimezone}`: Koordynator zadań znajdują się w stałej strefy czasowej nie czasu letniego (zazwyczaj reprezentowany przy użyciu czasu UTC). Ta strefa czasowa jest określane jako hello "Oozie przetwarzania strefy czasowej."
    > * `${wfPath}`: hello workflow.xml toohello ścieżki.

2. Witaj toosave plików, użyj klawiszy Ctrl-X **Y**, i **Enter**.

3. Użyj hello następujące polecenia toocopy hello pliku toohello katalog roboczy dla tego zadania:

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. Użyj powitania po toomodify hello **job.xml** pliku:

    ```
    nano job.xml
    ```

    Wprowadź hello następujące zmiany:

   * tooinstruct oozie toorun hello koordynatora zamiast pliku hello przepływu pracy, zmień `<name>oozie.wf.application.path</name>` zbyt`<name>oozie.coord.application.path</name>`.

   * Witaj tooset `workflowPath` zmiennej używanej przez koordynatora hello dodać powitania po XML:

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       Zastąp hello `wasb://mycontainer@mystorageaccount.blob.core.windows` tekst na powitania wartość używana w innych pozycji w pliku job.xml hello.

   * toodefine hello rozpoczęcia, zakończenia i częstotliwości hello koordynatora, Dodaj powitania po XML:

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

       Te wartości są ustawiane too12 czas rozpoczęcia hello: 00 PM na 10 maja 2017 hello tooMay czas zakończenia 12, 2017 r. Interwał powitania codziennie uruchomienia tego zadania. częstotliwość Hello jest w minutach, więc 24 godziny x 60 minut = 1440 minut. Na koniec hello strefę czasową ustawiono tooUTC.

5. Następnie użyj klawiszy Ctrl-X **Y** i **Enter** toosave hello pliku.

6. toorun hello zadania hello Użyj następującego polecenia:

    ```
    oozie job -config job.xml -run
    ```

    To polecenie przesyła i uruchamia zadanie hello.

7. Jeśli odwiedź hello Oozie interfejs sieci Web i wybierz hello **koordynator zadań** kartę, zobacz informacje toohello podobne po obrazu:

    ![Koordynator kartę zadania](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    Witaj **Materialization dalej** wpis zawiera hello następnym hello uruchomionych zadań.

8. Podobne toohello wcześniej zadania przepływu pracy, wybierając hello wpisem zadań w interfejsie użytkownika sieci web hello Wyświetla informacje na powitania zadania:

    ![Informacji o zadaniu koordynatora](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > Ten obraz zawiera tylko pomyślnie uruchamia zadanie hello nie poszczególnych działań w przepływie pracy hello zaplanowane. toosee, który, wybierz jedną z hello **akcji** wpisów.

    ![Informacje o akcji](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Witaj Oozie interfejsu użytkownika umożliwia tooview Oozie dzienniki. Zawiera ona także dzienniki tooJobTracker łącza do zadań MapReduce uruchomione przez hello przepływu pracy. powinny być Hello wzorzec do rozwiązywania problemów:

1. Wyświetl zadanie hello w interfejsie użytkownika sieci Web Oozie.

2. Jeśli istnieje komunikat o błędzie lub awaria dla określonej akcji, wybierz hello toosee akcji, jeśli hello **komunikat o błędzie** pole zawiera więcej informacji na powitania awarii.

3. Jeśli to możliwe, użyj hello adresu URL z tooview akcji hello więcej szczegółów (takich jak dzienniki JobTracker) dla akcji hello.

Witaj poniżej przedstawiono określonych błędów mogą wystąpić, i w jaki sposób tooresolve je.

### <a name="ja009-cannot-initialize-cluster"></a>JA009: Nie można zainicjować klastra

**Objawy**: hello zmiany stanu zadania za**zawieszone**. Szczegóły dotyczące zadania hello stan hello RunHiveScript jako **START_MANUAL**. Wybranie akcji hello powoduje wyświetlenie hello następujący komunikat o błędzie:

    JA009: Cannot initialize Cluster. Please check your configuration for map

**Przyczyna**: hello WASB adresy używane w hello **job.xml** plik nie zawiera kontenera magazynu hello lub nazwy konta magazynu. format adresu WASB Hello musi być `wasb://containername@storageaccountname.blob.core.windows.net`.

**Rozdzielczość**: Zmień adresy WASB hello używane przez zadanie hello.

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a>JA002: Oozie nie jest dozwolona tooimpersonate &lt;użytkownika >

**Objawy**: hello zmiany stanu zadania za**zawieszone**. Szczegóły dotyczące zadania hello stan hello RunHiveScript jako **START_MANUAL**. Wybranie akcji hello przedstawia hello następujący komunikat o błędzie:

    JA002: User: oozie is not allowed tooimpersonate <USER>

**Przyczyna**: bieżące ustawienia uprawnienia nie zezwalają na Oozie tooimpersonate hello określone konto użytkownika.

**Rozdzielczość**: Oozie jest dozwolona tooimpersonate użytkowników w hello **użytkowników** grupy. Użyj hello `groups USERNAME` toosee hello grup, które hello konto użytkownika jest członkiem. Jeśli użytkownik hello nie jest elementem członkowskim hello **użytkowników** grupy, użyj hello następujące polecenia tooadd hello użytkownika toohello grupy:

    sudo adduser USERNAME users

> [!NOTE]
> Może upłynąć kilka minut, zanim HDInsight rozpoznaje, że został dodany użytkownik hello toohello grupy.

### <a name="launcher-error-sqoop"></a>Uruchamianie błąd (Sqoop)

**Objawy**: hello zmiany stanu zadania za**KILLED**. Szczegóły dotyczące zadania hello stan hello RunSqoopExport jako **błąd**. Wybranie akcji hello przedstawia hello następujący komunikat o błędzie:

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

**Przyczyna**: Sqoop jest tooload hello sterowników wymaganych tooaccess hello baza danych.

**Rozdzielczość**: korzystając z zadania Oozie Sqoop, należy uwzględnić hello sterownik bazy danych z hello inne zasoby (na przykład hello workflow.xml) używana przez zadanie hello. Także odwoływać archiwum hello zawierający hello sterownik bazy danych z hello `<sqoop>...</sqoop>` sekcji hello workflow.xml.

Na przykład hello zadania w tym dokumencie, możesz użyć hello następujące kroki:

1. Skopiuj hello sqljdbc4.1.jar pliku toohello /tutorials/useoozie katalogu:

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. Modyfikowanie hello tooadd workflow.xml powitania po XML w nowym wierszu powyżej `</sqoop>`:

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a>Następne kroki

W tym samouczku można przedstawiono sposób toodefine Oozie przepływu pracy i w jaki sposób toorun Oozie zadania. toolearn więcej informacji na temat pracy z usługą HDInsight, zobacz następujące artykuły hello:

* [Korzystanie z usługą HDInsight oparte na czasie Oozie Coordinator][hdinsight-oozie-coordinator-time]
* [Przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight][hdinsight-upload-data]
* [Używanie Sqoop z platformą Hadoop w usłudze HDInsight][hdinsight-use-sqoop]
* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight][hdinsight-use-hive]
* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight][hdinsight-use-pig]
* [Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-mapreduce]

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
