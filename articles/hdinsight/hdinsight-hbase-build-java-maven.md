---
title: "aaaBuild aplikację Java HBase dla systemu Windows Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse aplikacji bazy danych Apache HBase opartych na języku Java toobuild Apache Maven, następnie wdrożyć ją tooa klastrów HDInsight opartych na systemie Windows Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 33c2f3d12cb6a17b5406817e8bcd3accff239517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a>Użyj aplikacji Java toobuild Maven, które używają bazy danych HBase z systemem Windows HDInsight (Hadoop)
Dowiedz się, jak toocreate i kompilacji [bazy danych Apache HBase](http://hbase.apache.org/) aplikacji w języku Java za pomocą Apache Maven. Następnie za pomocą aplikacji hello Azure HDInsight (Hadoop).

[Maven](http://maven.apache.org/) to oprogramowanie projektu zarządzania i zrozumienia narzędzie, które pozwala toobuild oprogramowania, dokumentacji i raporty dla projektów języka Java. W tym artykule dowiesz się, jak toouse on toocreate podstawowe aplikacji Java, która tworzy, wysyła zapytanie, które usuwa HBase tabeli w klastrze usługi HDInsight Azure.

> [!IMPORTANT]
> kroki Hello w tym dokumencie wymagają klastra usługi HDInsight z systemem Windows. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="requirements"></a>Wymagania
* [Platformy Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 lub nowszy
* [Maven](http://maven.apache.org/)
* Klaster usługi HDInsight opartej na systemie Windows z bazy danych HBase

    > [!NOTE]
    > kroki Hello w tym dokumencie zostały przetestowane w wersjach klastra usługi HDInsight 3.2 i 3.3. wartości domyślnych Hello w przykładach są dla klastra usługi HDInsight 3.3.

## <a name="create-hello-project"></a>Utwórz projekt hello
1. W wierszu polecenia hello w środowisku projektowania Zmień katalogi toohello lokalizację toocreate hello projektu, na przykład `cd code\hdinsight`.
2. Użyj hello **mvn** polecenia, który jest instalowany z Maven, hello toogenerate tworzenia szkieletu do projektu hello.

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    To polecenie tworzy katalog w bieżącej lokalizacji hello o nazwie hello określony przez hello **artifactID** parametr (**hbaseapp** w tym przykładzie.) Ten katalog zawiera hello następujące elementy:

   * **pom.XML**: hello projektu Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) zawiera informacje i konfiguracji projektu hello toobuild szczegóły używanego.
   * **SRC**: hello katalog, który zawiera hello **main\java\com\microsoft\examples** katalogu, w którym będzie Autor aplikacji hello.
3. Usuń hello **src\test\java\com\microsoft\examples\apptest.java** pliku, ponieważ nie jest on używany w tym przykładzie.

## <a name="update-hello-project-object-model"></a>Aktualizacja hello modelu obiektowego projektu
1. Edytuj hello **pom.xml** plik i dodać hello następującego kodu wewnątrz hello `<dependencies>` sekcji:

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    W tej sekcji opisano Maven, który hello projektu wymaga **klienta hbase** wersji **1.1.2**. W czasie kompilacji tę zależność jest pobierana z hello domyślne Maven repozytorium. Można użyć hello [Maven centralnym repozytorium wyszukiwania](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn więcej informacji na temat tej zależności.

   > [!IMPORTANT]
   > Witaj, numer wersji musi odpowiadać wersji hello HBase, która jest dostarczana z klastrem usługi HDInsight. Użyj powitania po numer poprawną wersję hello toofind tabeli.
   >
   >

   | Wersja klastra usługi HDInsight | Toouse wersji bazy danych HBase |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3 |1.1.2 |

    Aby uzyskać więcej informacji o wersji usługi HDInsight i składników, zobacz [co to są hello różne składniki platformy Hadoop dostępne z usługą HDInsight](hdinsight-component-versioning.md).
2. Jeśli korzystasz z klastra usługi HDInsight 3.3, należy dodać następujące toohello hello `<dependencies>` sekcji:

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    Ta zależność załaduje hello phoenix — podstawowe składniki, które są używane przez wersję bazy danych Hbase 1.1.x.
3. Dodaj hello następującego kodu toohello **pom.xml** pliku. W tej sekcji musi znajdować się wewnątrz hello `<project>...</project>` tagów w hello plików, na przykład między `</dependencies>` i `</project>`.

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
                    <source>1.7</source>
                    <target>1.7</target>
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

    Witaj `<resources>` sekcji konfiguruje zasobu (**conf\hbase-site.xml**) zawiera informacje o konfiguracji dla bazy danych HBase.

   > [!NOTE]
   > Można również ustawić wartości konfiguracji za pomocą kodu. Zobacz komentarze hello w hello **CreateTable** przykład znajdujący się na temat toodo to.
   >
   >

    To `<plugins>` sekcji konfiguruje hello [wtyczki kompilatora Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) i [Maven cień wtyczki](http://maven.apache.org/plugins/maven-shade-plugin/). wtyczki kompilatora Hello jest używane toocompile hello topologii. Wtyczka cień Hello jest duplikatów licencji tooprevent używane w pakiecie JAR hello jest konstruowany przez Maven. Przyczyna Hello, używana jest czy plików licencji zduplikowane hello spowodować błąd w czasie wykonywania w klastrze usługi HDInsight hello. Przy użyciu maven cień wtyczki z hello `ApacheLicenseResourceTransformer` ten błąd uniemożliwia implementacji.

    Witaj maven cień — dodatek również daje pełny jar (lub fat jar) zawierający wszystkie zależności hello wymagane przez aplikację hello.
4. Zapisz hello **pom.xml** pliku.
5. Utwórz nowy katalog o nazwie **conf** w hello **hbaseapp** katalogu. W hello **conf** katalogu, Utwórz plik o nazwie **hbase-site.xml**. Użyj następujących hello jako hello zawartość pliku hello:

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 hello Apache Software Foundation
          *
          * Licensed toohello Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See hello NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  hello ASF licenses this file
          * tooyou under hello Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with hello License.  You may obtain a copy of hello License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed tooin writing, software
          * distributed under hello License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See hello License for hello specific language governing permissions and
          * limitations under hello License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    Ten plik będzie konfiguracji bazy danych HBase hello tooload używane dla klastra usługi HDInsight.

   > [!NOTE]
   > Jest to plik minimalnego hbase-site.xml, i zawiera hello systemu od zera minimalne ustawienia hello klastra usługi HDInsight.

6. Zapisz hello **hbase-site.xml** pliku.

## <a name="create-hello-application"></a>Tworzenie aplikacji hello
1. Przejdź toohello **hbaseapp\src\main\java\com\microsoft\examples** katalogu i Zmień nazwę hello pliku app.java zbyt**CreateTable.java**.
2. Otwórz hello **CreateTable.java** plików i zastąpić istniejącą zawartość hello hello następującego kodu:

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
            // hello following sets hello znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

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

    Jest to hello **CreateTable** klasy, która zostanie utworzona tabela o nazwie **osób** i wypełnić ją w przypadku niektórych użytkowników wstępnie zdefiniowane.
3. Zapisz hello **CreateTable.java** pliku.
4. W hello **hbaseapp\src\main\java\com\microsoft\examples** katalogu, Utwórz nowy plik o nazwie **SearchByEmail.java**. Użyj hello następującego kodu jako hello zawartość tego pliku:

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

            // Create a new regex filter
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

    Witaj **SearchByEmail** klasa może być używana tooquery wierszy za pomocą adresu e-mail. Ponieważ używa filtra wyrażenia regularnego, musisz podać ciąg lub wyrażenie regularne używając hello klasy.
5. Zapisz hello **SearchByEmail.java** pliku.
6. W hello **hbaseapp\src\main\hava\com\microsoft\examples** katalogu, Utwórz nowy plik o nazwie **DeleteTable.java**. Użyj hello następującego kodu jako hello zawartość tego pliku:

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

    Ta klasa jest oczyszczania w tym przykładzie, wyłączając i upuszczanie tabeli hello tworzone przez hello **CreateTable** klasy.
7. Zapisz hello **DeleteTable.java** pliku.

## <a name="build-and-package-hello-application"></a>Aplikacja hello kompilacji i pakietu
1. Otwórz wiersz polecenia i zmień katalogi toohello **hbaseapp** katalogu.
2. Użyj następującego polecenia toobuild plik JAR zawierający aplikacji hello hello:

        mvn clean package

    To czyści wszystkie poprzednie artefaktów kompilacji, pobierze wszelkie zależności, które nie są jeszcze zainstalowane, następnie kompilacje i pakiety aplikacji hello.
3. Po polecenie hello zakończeniu hello **hbaseapp\target** katalog zawiera plik o nazwie **hbaseapp-1.0-SNAPSHOT.jar**.

   > [!NOTE]
   > Witaj **hbaseapp-1.0-SNAPSHOT.jar** plików jest pełny jar (nazywane również fat jar), który zawiera wszystkie zależności hello wymaganych aplikacji hello toorun.

## <a name="upload-hello-jar-file-and-start-a-job"></a>Przekaż plik JAR hello i uruchomić zadanie
Istnieje wiele sposobów tooupload klastra usługi HDInsight tooyour pliku, zgodnie z opisem w [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md). Witaj następujące kroki użyciu programu Azure PowerShell.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. Po zainstalowaniu i skonfigurowaniu programu Azure PowerShell, Utwórz nowy plik o nazwie **hbase runner.psm1**. Użyj następujących hello jako hello zawartość tego pliku:

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

    Ten plik zawiera dwa moduły:

   * **Dodaj HDInsightFile** — używane tooupload tooHDInsight plików
   * **Start-HBaseExample** -używane klasy hello toorun utworzony wcześniej
2. Zapisz hello **hbase runner.psm1** pliku.
3. Otwórz nowe okno programu Azure PowerShell, zmień katalogi toohello **hbaseapp** katalogu, a następnie hello uruchom następujące polecenie.

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    Zmienić lokalizację toohello ścieżka hello hello **hbase runner.psm1** wcześniej utworzony plik. Rejestruje moduł hello tej sesji programu Azure PowerShell.
4. Użyj hello następujące polecenie tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour klastra usługi HDInsight.

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    Zastąp **hdinsightclustername** o nazwie hello klastra usługi HDInsight. polecenie Hello przekazuje hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **przykład/słoików** lokalizacji w hello podstawowy magazyn dla klastra usługi HDInsight.
5. Po przekazaniu plików hello Użyj hello poniższy kod toocreate tabeli za pomocą hello **hbaseapp**:

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    Zastąp **hdinsightclustername** o nazwie hello klastra usługi HDInsight.

    To polecenie tworzy nową tabelę o nazwie **osób** w klastrze usługi HDInsight. To polecenie nie wyświetla żadnych danych wyjściowych w oknie konsoli hello.
6. toosearch wpisy tabeli hello hello Użyj następującego polecenia:

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    Zastąp **hdinsightclustername** o nazwie hello klastra usługi HDInsight.

    To polecenie używa hello **SearchByEmail** klasy toosearch wierszy, gdzie hello **contactinformation** rodziny kolumn i hello **e-mail** kolumny zawiera ciąg hello **contoso.com**. Powinien zostać wyświetlony hello następujące wyniki:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Przy użyciu **fabrikam.com** dla hello `-emailRegex` wartość zwraca hello użytkowników, którzy mają **fabrikam.com** hello pola wiadomości e-mail. Ponieważ to wyszukiwanie jest implementowane za pomocą regularnego oparte na wyrażeniach filtru, możesz też wprowadzić wyrażeń regularnych, takich jak **^ r**, które zwraca zapisy, gdzie hello e-mail zaczyna się od hello litery "r".

## <a name="delete-hello-table"></a>Usuń tabelę hello
Po wykonaniu przykład Witaj, następujące hello Użyj polecenie z hello Azure PowerShell sesji toodelete hello **osób** Tabela używana w tym przykładzie:

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

Zastąp **hdinsightclustername** o nazwie hello klastra usługi HDInsight.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Nie wyników lub nieoczekiwane wyniki, korzystając z Start HBaseExample
Użyj hello `-showErr` tooview hello standardowy błąd parametru (STDERR) utworzonym podczas wykonywanym zadaniem hello.
