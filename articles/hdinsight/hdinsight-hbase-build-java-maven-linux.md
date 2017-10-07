---
title: Klient HBase aaaJava - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse aplikacji bazy danych Apache HBase opartych na języku Java toobuild Apache Maven, następnie wdrożyć go tooHBase w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: 
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 41ef92b2900280dd59089c4fa40686c44133b337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-java-applications-for-apache-hbase"></a>Tworzenie aplikacji Java dla bazy danych Apache HBase

Dowiedz się, jak toocreate [bazy danych Apache HBase](http://hbase.apache.org/) aplikacji w języku Java. Z bazy danych HBase w usłudze Azure HDInsight za pomocą aplikacji hello.

Witaj kroków w tym dokumencie [Maven](http://maven.apache.org/) toocreate i kompilacji projektu hello. Zarządzanie projektami oprogramowania i zrozumienia narzędzie, które umożliwia toobuild oprogramowania, dokumentacji i raporty dla projektów języka Java będzie maven.

> [!NOTE]
> Witaj kroki opisane w tym dokumencie zostały ostatnio przetestowana 3,6 HDInsight.

> [!IMPORTANT]
> kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="requirements"></a>Wymagania

* [Platformy Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 lub nowszy.

    > [!NOTE]
    > HDInsight w wersji 3.5 lub nowszej wymaga Java 8. Wcześniejszych wersji usługi hdinsight wymagają Java 7.

* [Maven](http://maven.apache.org/)

* [Klaster HDInsight Azure opartej na systemie Linux z bazy danych HBase](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > kroki Hello w tym dokumencie zostały przetestowane w wersjach klastra usługi HDInsight 3.4 i 3.5. wartości domyślnych Hello w przykładach są dla klastra usługi HDInsight 3.5.

## <a name="create-hello-project"></a>Utwórz projekt hello

1. W wierszu polecenia hello w środowisku projektowania Zmień katalogi toohello lokalizację toocreate hello projektu, na przykład `cd code\hbase`.

2. Użyj hello **mvn** polecenia, który jest instalowany z Maven, hello toogenerate tworzenia szkieletu do projektu hello.

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > Jeśli używasz programu PowerShell, należy ująć hello `-D` parametrów w podwójny cudzysłów.
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    To polecenie tworzy katalog z hello sama nazwa jak hello **artifactID** parametr (**hbaseapp** w tym przykładzie.) Ten katalog zawiera hello następujące elementy:

   * **pom.XML**: hello projektu Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) zawiera informacje i konfiguracji projektu hello toobuild szczegóły używanego.
   * **SRC**: hello katalog, który zawiera hello **main/java/com/microsoft/przykłady** katalogu, w którym autor aplikacji hello.

3. Usuń hello `src/test/java/com/microsoft/examples/apptest.java` pliku. Nie można użyć w tym przykładzie.

## <a name="update-hello-project-object-model"></a>Aktualizacja hello modelu obiektowego projektu

1. Edytuj hello `pom.xml` plik i dodać hello następującego kodu wewnątrz hello `<dependencies>` sekcji:

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    W tej sekcji wskazuje projekt hello musi **klienta hbase** i **phoenix core** składników. W czasie kompilacji te zależności są pobierane z hello domyślne Maven repozytorium. Można użyć hello [Maven centralnym repozytorium wyszukiwania](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn więcej informacji na temat tej zależności.

   > [!IMPORTANT]
   > numer wersji Hello hello hbase klient musi odpowiadać wersji hello HBase, która jest dostarczana z klastrem usługi HDInsight. Użyj powitania po numer poprawną wersję hello toofind tabeli.

   | Wersja klastra usługi HDInsight | Toouse wersji bazy danych HBase |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3, 3.4, 3.5 i 3,6 |1.1.2 |

    Aby uzyskać więcej informacji o wersji usługi HDInsight i składników, zobacz [co to są hello różne składniki platformy Hadoop dostępne z usługą HDInsight](hdinsight-component-versioning.md).

3. Dodaj hello następującego kodu toohello **pom.xml** pliku. Ten tekst musi znajdować się wewnątrz hello `<project>...</project>` tagów w hello plików, na przykład między `</dependencies>` i `</project>`.

   ```xml
    <build>
        <sourceDirectory>src</sourceDirectory>
        <resources>
        <resource>
            <directory>${basedir}/conf</directory>
            <filtering>false</filtering>
            <includes>
            <include>hbase-site.xml</include>
            </includes>
        </resource>
        </resources>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
            </configuration>
            <executions>
            <execution>
                <phase>package</phase>
                <goals>
                <goal>shade</goal>
                </goals>
            </execution>
            </executions>
        </plugin>
        </plugins>
    </build>
   ```

    W tej sekcji konfiguruje zasobu (`conf/hbase-site.xml`) zawiera informacje o konfiguracji dla bazy danych HBase.

   > [!NOTE]
   > Można również ustawić wartości konfiguracji za pomocą kodu. Zobacz komentarze hello w hello `CreateTable` przykład.

    W tej sekcji konfiguruje również hello [wtyczki kompilatora Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) i [Maven cień wtyczki](http://maven.apache.org/plugins/maven-shade-plugin/). wtyczki kompilatora Hello jest używane toocompile hello topologii. Wtyczka cień Hello jest duplikatów licencji tooprevent używane w pakiecie JAR hello jest konstruowany przez Maven. Ten dodatek jest używane tooprevent "duplikatów plików licencji" Błąd w czasie wykonywania w klastrze usługi HDInsight hello. Przy użyciu maven cień wtyczki z hello `ApacheLicenseResourceTransformer` hello błąd uniemożliwia implementacji.

    Witaj maven cień wtyczki tworzy również jar pełny, który zawiera wszystkie zależności hello wymagane przez aplikację hello.

4. Zapisz hello `pom.xml` pliku.

5. Utwórz katalog o nazwie `conf` w hello `hbaseapp` katalogu. Informacje o konfiguracji toohold używane do łączenia tooHBase jest to katalog.

6. Użyj hello następujące polecenie toocopy hello HBase konfigurację z toohello klastra HBase hello `conf` katalogu. Zastąp `USERNAME` o nazwie hello logowanie SSH. Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight:

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   Aby uzyskać więcej informacji na temat używania `ssh` i `scp`, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-hello-application"></a>Tworzenie aplikacji hello

1. Przejdź toohello `hbaseapp/src/main/java/com/microsoft/examples` katalogu i Zmień nazwę hello pliku app.java zbyt`CreateTable.java`.

2. Otwórz hello `CreateTable.java` plików i zastąpić istniejącą zawartość hello hello następującego tekstu:

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.TableName;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.util.Bytes;

    public class CreateTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Example of setting zookeeper values for HDInsight
        // in code instead of an hbase-site.xml file
        //
        // config.set("hbase.zookeeper.quorum",
        //            "zookeepernode0,zookeepernode1,zookeepernode2");
        //config.set("hbase.zookeeper.property.clientPort", "2181");
        //config.set("hbase.cluster.distributed", "true");
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as hello znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create hello table...
        HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
        // ... with two column families
        tableDescriptor.addFamily(new HColumnDescriptor("name"));
        tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
        admin.createTable(tableDescriptor);

        // define some people
        String[][] people = {
            { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
            { "2", "Franklin", "Holtz", "franklin@contoso.com" },
            { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
            { "4", "Rae", "Schroeder", "rae@contoso.com" },
            { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
            { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

        HTable table = new HTable(config, "people");

        // Add each person toohello table
        //   Use hello `name` column family for hello name
        //   Use hello `contactinfo` column family for hello email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close hello table
        table.flushCommits();
        table.close();
        }
    }
   ```

    Ten kod jest hello **CreateTable** klasy, która tworzy tabelę o nazwie **osób** i wypełnić ją w przypadku niektórych użytkowników wstępnie zdefiniowane.

3. Zapisz hello `CreateTable.java` pliku.

4. W hello `hbaseapp/src/main/java/com/microsoft/examples` katalogu, Utwórz plik o nazwie `SearchByEmail.java`. Użyj hello następującego tekstu jako hello zawartość tego pliku:

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
    import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
    import org.apache.hadoop.hbase.util.Bytes;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class SearchByEmail {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Use GenericOptionsParser tooget only hello parameters toohello class
        // and not all hello parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open hello table
        HTable table = new HTable(config, "people");

        // Define hello family and qualifiers toobe used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach hello regex filter tooa filter
        //   for hello email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set hello filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get hello results
        ResultScanner results = table.getScanner(scan);
        // Iterate over results and print  values
        for (Result result : results ) {
            String id = new String(result.getRow());
            byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
            String firstName = new String(firstNameObj);
            byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
            String lastName = new String(lastNameObj);
            System.out.println(firstName + " " + lastName + " - ID: " + id);
            byte[] emailObj = result.getValue(contactFamily, emailQualifier);
            String email = new String(emailObj);
            System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
        }
        results.close();
        table.close();
        }
    }
   ```

    Witaj **SearchByEmail** klasa może być używana tooquery wierszy za pomocą adresu e-mail. Ponieważ używa filtra wyrażenia regularnego, musisz podać ciąg lub wyrażenie regularne używając hello klasy.

5. Zapisz hello `SearchByEmail.java` pliku.

6. W hello `hbaseapp/src/main/hava/com/microsoft/examples` katalogu, Utwórz plik o nazwie `DeleteTable.java`. Użyj hello następującego tekstu jako hello zawartość tego pliku:

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete hello table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    Ta klasa czyści hello tabel HBase utworzone w tym przykładzie, wyłączając i upuszczanie tabeli hello tworzone przez hello `CreateTable` klasy.

7. Zapisz hello `DeleteTable.java` pliku.

## <a name="build-and-package-hello-application"></a>Aplikacja hello kompilacji i pakietu

1. Z hello `hbaseapp` katalogu, użyj hello następujące polecenie toobuild plik JAR zawierający aplikacji hello:

    ```bash
    mvn clean package
    ```

    To polecenie tworzy i aplikacji do pliku JAR hello pakietów.

2. Po polecenie hello zakończeniu hello `hbaseapp/target` katalog zawiera plik o nazwie `hbaseapp-1.0-SNAPSHOT.jar`.

   > [!NOTE]
   > Witaj `hbaseapp-1.0-SNAPSHOT.jar` plik jest jar pełny. Zawiera wszystkie hello zależności wymagane toorun hello aplikacji.


## <a name="upload-hello-jar-and-run-jobs-ssh"></a>Przekaż hello JAR i uruchom zadania (SSH)

Witaj, użyj czynności po `scp` toocopy hello JAR toohello głównej węzła głównego hbase sieci w klastrze usługi HDInsight. Witaj `ssh` polecenie jest następnie używany tooconnect toohello klastra i uruchom przykład Witaj bezpośrednio na powitania węzła głównego.

1. tooupload hello jar toohello klaster, hello Użyj następującego polecenia:

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    Zastąp `USERNAME` o nazwie hello logowanie SSH. Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight.

2. klaster HBase toohello tooconnect, hello Użyj następującego polecenia:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Zastąp `USERNAME` hello nazwa logowania użytkownika SSH. Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight.

3. toocreate tabeli HBase przy użyciu hello aplikacji Java, hello Użyj następującego polecenia:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    To polecenie tworzy tabelę HBase o nazwie **osoby**i wypełnia danych.

4. toosearch adresów e-mail, przechowywane w tabeli hello, hello Użyj następującego polecenia:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    Pojawi się hello następujące wyniki:

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. toodelete hello tabeli hello Użyj następującego polecenia:

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a>Przekaż hello JAR i uruchom zadania (PowerShell)

Hello następujące kroki, użyj programu Azure PowerShell tooupload hello JAR toohello domyślny magazyn dla klastra HBase. Polecenia cmdlet usługi HDInsight są następnie używane toorun hello przykłady zdalnie.

1. Po zainstalowaniu i skonfigurowaniu programu Azure PowerShell Utwórz plik o nazwie `hbase-runner.psm1`. Użyj hello następującego tekstu jako hello zawartość tego pliku:

   ```powershell
    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.CreateTable"
    -clusterName "MyHDInsightCluster"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "contoso.com"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "^r" -showErr
    #>

    function Start-HBaseExample {
    [CmdletBinding(SupportsShouldProcess = $true)]
    param(
    #hello class toorun
    [Parameter(Mandatory = $true)]
    [String]$className,

    #hello name of hello HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want toosee stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is hello Azure module installed?
    FindAzure

    # Get hello login for hello HDInsight cluster
    $creds=Get-Credential -Message "Enter hello login for hello cluster" -UserName "admin"

    # hello JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # hello job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get hello job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds
    if($showErr)
    {
    Write-Host "STDERR"
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds `
                -DisplayOutputType StandardError
    }
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    -Container "MyContainer"
    #>

    function Add-HDInsightFile {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
            #hello path toohello local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #hello destination path and file name, relative toohello root of hello container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #hello name of hello HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is hello Azure module installed?
        FindAzure

        # Get authentication for hello cluster
        $creds=Get-Credential

        # Does hello local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get hello primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file toostorage, overwriting existing files if -force was used.
        Set-AzureStorageBlobContent -File $localPath `
            -Blob $destinationPath `
            -force:$force `
            -Container $storage.container `
            -Context $storage.context
    }

    function FindAzure {
        # Is there an active Azure subscription?
        $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
        if(-not($sub))
        {
            throw "No active Azure subscription found! If you have a subscription, use hello Login-AzureRmAccount cmdlet toologin tooyour subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does hello cluster exist?
        if (!$hdi)
        {
            throw "HDInsight cluster '$clusterName' does not exist."
        }
        # Create a return object for context & container
        $return = @{}
        $storageAccounts = @{}

        # Get storage information
        $resourceGroup = $hdi.ResourceGroup
        $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
        $container=$hdi.DefaultStorageContainer
        $storageAccountKey=(Get-AzureRmStorageAccountKey `
            -Name $storageAccountName `
        -ResourceGroupName $resourceGroup)[0].Value
        # Get hello resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get hello storage context, as we can't depend
        # on using hello default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get hello container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts toosupport finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export hello verb-phrase things
    export-modulemember *-*
   ```

    Ten plik zawiera dwa moduły:

   * **Dodaj HDInsightFile** — używane tooupload pliki toohello klastra
   * **Start-HBaseExample** -używane klasy hello toorun utworzony wcześniej

2. Zapisz hello `hbase-runner.psm1` pliku.

3. Otwórz nowe okno programu Azure PowerShell, zmień katalogi toohello `hbaseapp` katalogu, a następnie hello uruchom następujące polecenie:

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    Zmienić lokalizację toohello ścieżka hello hello `hbase-runner.psm1` wcześniej utworzony plik. To polecenie rejestruje hello modułu przy użyciu programu Azure PowerShell.

4. Użyj hello następujące polecenie tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour klastra.

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    Zastąp `hdinsightclustername` o nazwie hello klastra. polecenie Hello przekazuje hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` lokalizacji w hello podstawowy magazyn dla klastra.

5. Witaj toocreate tabeli za pomocą `hbaseapp`, użyj następującego polecenia hello:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    Zastąp `hdinsightclustername` o nazwie hello klastra.

    To polecenie tworzy tabeli o nazwie **osób** w bazie danych HBase w klastrze usługi HDInsight. To polecenie nie wyświetla żadnych danych wyjściowych w oknie konsoli hello.

6. toosearch wpisy tabeli hello hello Użyj następującego polecenia:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    Zastąp `hdinsightclustername` o nazwie hello klastra.

    To polecenie używa hello `SearchByEmail` klasy toosearch wierszy, gdzie hello `contactinformation` rodziny kolumn i hello `email` kolumny zawiera ciąg hello `contoso.com`. Powinien zostać wyświetlony hello następujące wyniki:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Przy użyciu **fabrikam.com** dla hello `-emailRegex` wartość zwraca hello użytkowników, którzy mają **fabrikam.com** hello pola wiadomości e-mail. Można również używać wyrażeń regularnych jako hello wyszukiwanego terminu. Na przykład **^ r** zwraca e-mail adresów, które zaczynają się od litery hello "r".

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Nie wyników lub nieoczekiwane wyniki, korzystając z Start HBaseExample

Użyj hello `-showErr` tooview hello standardowy błąd parametru (STDERR) utworzonym podczas wykonywanym zadaniem hello.

## <a name="delete-hello-table"></a>Usuń tabelę hello

Po wykonaniu przykład Witaj, użyj następującego toodelete hello hello **osób** Tabela używana w tym przykładzie:

__Z `ssh` sesji__:

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

__Z programu Azure PowerShell__:

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a>Następne kroki

[Dowiedz się, jak toouse SQuirreL SQL z bazą danych HBase](hdinsight-hbase-phoenix-squirrel-linux.md)
