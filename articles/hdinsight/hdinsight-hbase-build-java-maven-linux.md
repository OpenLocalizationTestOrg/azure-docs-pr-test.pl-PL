---
title: Klient Java HBase - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak używać Apache Maven do tworzenia aplikacji opartych na języku Java bazy danych Apache HBase, a następnie wdrożyć ją do bazy danych HBase w usłudze Azure HDInsight."
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
ms.openlocfilehash: 03c88397e36c0fc7f19410e49f6b6f1a607659f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="build-java-applications-for-apache-hbase"></a>Tworzenie aplikacji Java dla bazy danych Apache HBase

Dowiedz się, jak utworzyć [bazy danych Apache HBase](http://hbase.apache.org/) aplikacji w języku Java. Następnie należy użyć aplikacji z bazy danych HBase w usłudze Azure HDInsight.

Użyj dokumentów z krokami w tym [Maven](http://maven.apache.org/) do tworzenia i skompilować projekt. Zarządzanie projektami oprogramowania i zrozumienia narzędzia, która pozwala na tworzenie oprogramowania, dokumentacji i raporty dla projektów języka Java będzie maven.

> [!NOTE]
> Kroki opisane w tym dokumencie zostały ostatnio przetestowana 3,6 HDInsight.

> [!IMPORTANT]
> Kroki opisane w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="requirements"></a>Wymagania

* [Platformy Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 lub nowszy.

    > [!NOTE]
    > HDInsight w wersji 3.5 lub nowszej wymaga Java 8. Wcześniejszych wersji usługi hdinsight wymagają Java 7.

* [Maven](http://maven.apache.org/)

* [Klaster HDInsight Azure opartej na systemie Linux z bazy danych HBase](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > Kroki opisane w tym dokumencie zostały przetestowane w wersjach klastra usługi HDInsight 3.4 i 3.5. Wartości domyślnych w przykładach są dla klastra usługi HDInsight 3.5.

## <a name="create-the-project"></a>Tworzenie projektu

1. Z poziomu wiersza polecenia w środowisku projektowania, przejdź do lokalizacji, w której chcesz utworzyć projekt, na przykład `cd code\hbase`.

2. Użyj **mvn** polecenia, które jest instalowany z Maven, aby wygenerować funkcją szkieletów dla projektu.

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > Jeśli używasz programu PowerShell, należy ująć `-D` parametrów w podwójny cudzysłów.
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    To polecenie tworzy katalog o tej samej nazwie jako **artifactID** parametr (**hbaseapp** w tym przykładzie.) Ten katalog zawiera następujące elementy:

   * **pom.XML**: projektu Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) zawiera informacje i szczegóły konfiguracji używany do tworzenia projektu.
   * **SRC**: katalog, który zawiera **main/java/com/microsoft/przykłady** katalogu, w którym autor aplikacji.

3. Usuń `src/test/java/com/microsoft/examples/apptest.java` pliku. Nie można użyć w tym przykładzie.

## <a name="update-the-project-object-model"></a>Aktualizacja modelu obiektowego projektu

1. Edytuj `pom.xml` i Dodaj następujący kod w `<dependencies>` sekcji:

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

    W tej sekcji wskazuje, że projekt wymaga **klienta hbase** i **phoenix core** składników. W czasie kompilacji te zależności są pobierane z repozytorium Maven domyślne. Można użyć [Maven centralnym repozytorium wyszukiwania](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) Aby dowiedzieć się więcej na temat tej zależności.

   > [!IMPORTANT]
   > Numer wersji klienta hbase musi odpowiadać wersji bazy danych HBase, która jest dostarczana z klastrem usługi HDInsight. Skorzystaj z poniższej tabeli, aby znaleźć poprawnej wersji numer.

   | Wersja klastra usługi HDInsight | Wersja bazy danych HBase do użycia |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3, 3.4, 3.5 i 3,6 |1.1.2 |

    Aby uzyskać więcej informacji o wersji usługi HDInsight i składników, zobacz [co to są dostępne z usługą HDInsight różnych składników Hadoop](hdinsight-component-versioning.md).

3. Dodaj następujący kod do **pom.xml** pliku. Ten tekst musi znajdować się wewnątrz `<project>...</project>` tagów w pliku, na przykład między `</dependencies>` i `</project>`.

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
   > Można również ustawić wartości konfiguracji za pomocą kodu. Zobacz komentarze w `CreateTable` przykład.

    W tej sekcji konfiguruje również [wtyczki kompilatora Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) i [Maven cień wtyczki](http://maven.apache.org/plugins/maven-shade-plugin/). Kompilator wtyczka jest używana do kompilowania topologii. Wtyczka cień jest używany do chronienia duplikatów licencji w pakiecie JAR, który jest konstruowany przez Maven. Ten dodatek jest używany do chronienia błąd "licencji duplikatów plików" w czasie wykonywania w klastrze usługi HDInsight. Przy użyciu narzędzia maven cień wtyczki o `ApacheLicenseResourceTransformer` błąd uniemożliwia implementacji.

    Wtyczka cień maven tworzy również jar pełny, który zawiera wszystkie zależności wymagane przez aplikację.

4. Zapisz `pom.xml` pliku.

5. Utwórz katalog o nazwie `conf` w `hbaseapp` katalogu. Ten katalog jest używany do przechowywania informacji o konfiguracji w celu nawiązania HBase.

6. Użyj następującego polecenia umożliwia kopiowanie konfiguracji bazy danych HBase z klastra HBase `conf` katalogu. Zastąp `USERNAME` o nazwie logowanie SSH. Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight:

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   Aby uzyskać więcej informacji na temat używania `ssh` i `scp`, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-the-application"></a>Tworzenie aplikacji

1. Przejdź do `hbaseapp/src/main/java/com/microsoft/examples` katalogu i app.java Zmień nazwę pliku na `CreateTable.java`.

2. Otwórz `CreateTable.java` plików i zastąpić istniejącą zawartość z następującym tekstem:

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

        //Linux-based HDInsight clusters use /hbase-unsecure as the znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create the table...
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

        // Add each person to the table
        //   Use the `name` column family for the name
        //   Use the `contactinfo` column family for the email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close the table
        table.flushCommits();
        table.close();
        }
    }
   ```

    Ten kod jest **CreateTable** klasy, która tworzy tabelę o nazwie **osób** i wypełnić ją w przypadku niektórych użytkowników wstępnie zdefiniowane.

3. Zapisz `CreateTable.java` pliku.

4. W `hbaseapp/src/main/java/com/microsoft/examples` katalogu, Utwórz plik o nazwie `SearchByEmail.java`. Zawartość tego pliku, należy użyć następującego tekstu:

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

        // Use GenericOptionsParser to get only the parameters to the class
        // and not all the parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open the table
        HTable table = new HTable(config, "people");

        // Define the family and qualifiers to be used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach the regex filter to a filter
        //   for the email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set the filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get the results
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

    **SearchByEmail** klasa może być używana do zapytania dla wierszy za pomocą adresu e-mail. Ponieważ używa filtra wyrażenia regularnego, musisz podać ciąg lub wyrażenie regularne, przy użyciu klasy.

5. Zapisz `SearchByEmail.java` pliku.

6. W `hbaseapp/src/main/hava/com/microsoft/examples` katalogu, Utwórz plik o nazwie `DeleteTable.java`. Zawartość tego pliku, należy użyć następującego tekstu:

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete the table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    Ta klasa czyści tabele bazy danych HBase utworzone w tym przykładzie, wyłączając i upuszczanie tabeli utworzone przez `CreateTable` klasy.

7. Zapisz `DeleteTable.java` pliku.

## <a name="build-and-package-the-application"></a>Tworzenie i pakiet aplikacji

1. Z `hbaseapp` katalogu, użyj następującego polecenia, aby utworzyć plik JAR zawierający aplikację:

    ```bash
    mvn clean package
    ```

    To polecenie tworzy i pakiety aplikacji do pliku JAR.

2. Po zakończeniu wykonywania polecenia `hbaseapp/target` katalog zawiera plik o nazwie `hbaseapp-1.0-SNAPSHOT.jar`.

   > [!NOTE]
   > `hbaseapp-1.0-SNAPSHOT.jar` Plik jest jar pełny. Zawiera wszystkie zależności wymagane do uruchomienia aplikacji.


## <a name="upload-the-jar-and-run-jobs-ssh"></a>Przekaż JAR i uruchom zadania (SSH)

Następujące kroki użyj `scp` do skopiowania JAR do głównej węzła głównego hbase sieci w klastrze usługi HDInsight. `ssh` Polecenia jest następnie używany do nawiązania połączenia klastra i uruchomić przykład bezpośrednio w węźle głównym.

1. Aby przekazać jar do klastra, użyj następującego polecenia:

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    Zastąp `USERNAME` o nazwie logowanie SSH. Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight.

2. Aby połączyć się klastra HBase, użyj następującego polecenia:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Zastąp `USERNAME` nazwę użytkownika logowania SSH. Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight.

3. Do tworzenia tabel HBase przy użyciu aplikacji Java, użyj następującego polecenia:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    To polecenie tworzy tabelę HBase o nazwie **osoby**i wypełnia danych.

4. Aby wyszukać adresy e-mail przechowywane w tabeli, użyj następującego polecenia:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    Pojawi się następujące wyniki:

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. Aby usunąć tabeli, użyj następującego polecenia:

    

## <a name="upload-the-jar-and-run-jobs-powershell"></a>Przekaż JAR i uruchom zadania (PowerShell)

Poniższe kroki przekazać JAR do magazynu domyślnego dla klastra HBase przy użyciu programu Azure PowerShell. Polecenia cmdlet usługi HDInsight są następnie używane do uruchamiania w przykładach zdalnie.

1. Po zainstalowaniu i skonfigurowaniu programu Azure PowerShell Utwórz plik o nazwie `hbase-runner.psm1`. Zawartość tego pliku, należy użyć następującego tekstu:

   ```powershell
    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
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
    #The class to run
    [Parameter(Mandatory = $true)]
    [String]$className,

    #The name of the HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want to see stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is the Azure module installed?
    FindAzure

    # Get the login for the HDInsight cluster
    $creds=Get-Credential -Message "Enter the login for the cluster" -UserName "admin"

    # The JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # The job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get the job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
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
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
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
            #The path to the local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #The destination path and file name, relative to the root of the container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #The name of the HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is the Azure module installed?
        FindAzure

        # Get authentication for the cluster
        $creds=Get-Credential

        # Does the local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get the primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file to storage, overwriting existing files if -force was used.
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
            throw "No active Azure subscription found! If you have a subscription, use the Login-AzureRmAccount cmdlet to login to your subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does the cluster exist?
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
        # Get the resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get the storage context, as we can't depend
        # on using the default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get the container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts to support finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export the verb-phrase things
    export-modulemember *-*
   ```

    Ten plik zawiera dwa moduły:

   * **Dodaj HDInsightFile** — umożliwia przekazywanie plików do klastra
   * **Początek HBaseExample** — używany do uruchamiania klasy utworzony wcześniej

2. Zapisz `hbase-runner.psm1` pliku.

3. Otwórz nowe okno programu Azure PowerShell, przejdź do `hbaseapp` katalogu, a następnie uruchom następujące polecenie:

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    Zmień ścieżkę do lokalizacji `hbase-runner.psm1` wcześniej utworzony plik. To polecenie rejestruje moduł przy użyciu programu Azure PowerShell.

4. Użyj następującego polecenia do przekazania `hbaseapp-1.0-SNAPSHOT.jar` do klastra.

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    Zastąp ciąg `hdinsightclustername` nazwą klastra. Polecenie przekazuje `hbaseapp-1.0-SNAPSHOT.jar` do `example/jars` lokalizacji w pamięci głównej dla klastra.

5. Aby utworzyć tabelę przy użyciu `hbaseapp`, użyj następującego polecenia:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    Zastąp ciąg `hdinsightclustername` nazwą klastra.

    To polecenie tworzy tabeli o nazwie **osób** w bazie danych HBase w klastrze usługi HDInsight. To polecenie nie wyświetla żadnych danych wyjściowych w oknie konsoli.

6. Aby wyszukać wpisów w tabeli, użyj następującego polecenia:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    Zastąp ciąg `hdinsightclustername` nazwą klastra.

    To polecenie używa `SearchByEmail` klasę, aby wyszukać wszystkie wiersze gdzie `contactinformation` rodziny kolumn i `email` kolumny zawiera ciąg `contoso.com`. Powinien zostać wyświetlony następujące wyniki:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Przy użyciu **fabrikam.com** dla `-emailRegex` użytkowników, którzy mają zwraca wartość **fabrikam.com** w pole adresu e-mail. Można również używać wyrażeń regularnych jako terminu wyszukiwania. Na przykład **^ r** zwraca e-mail adresów, które zaczynają się od litery "r".

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Nie wyników lub nieoczekiwane wyniki, korzystając z Start HBaseExample

Użyj `-showErr` parametr, aby wyświetlić błąd standardowy (STDERR) jest tworzony podczas uruchamiania zadania.

## <a name="delete-the-table"></a>Usuwanie tabeli

Gdy wszystko będzie gotowe do przykładu, aby usunąć należy użyć następującego **osób** Tabela używana w tym przykładzie:

__Z `ssh` sesji__:

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

__Z programu Azure PowerShell__:

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a>Następne kroki

[Dowiedz się, jak korzystać z SQuirreL SQL z bazy danych HBase](hdinsight-hbase-phoenix-squirrel-linux.md)
