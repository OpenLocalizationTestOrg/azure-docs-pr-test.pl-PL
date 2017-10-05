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
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="ca4fe-103">Tworzenie aplikacji Java dla bazy danych Apache HBase</span><span class="sxs-lookup"><span data-stu-id="ca4fe-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="ca4fe-104">Dowiedz się, jak utworzyć [bazy danych Apache HBase](http://hbase.apache.org/) aplikacji w języku Java.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-104">Learn how to create an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="ca4fe-105">Następnie należy użyć aplikacji z bazy danych HBase w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-105">Then use the application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="ca4fe-106">Użyj dokumentów z krokami w tym [Maven](http://maven.apache.org/) do tworzenia i skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-106">The steps in this document use [Maven](http://maven.apache.org/) to create and build the project.</span></span> <span data-ttu-id="ca4fe-107">Zarządzanie projektami oprogramowania i zrozumienia narzędzia, która pozwala na tworzenie oprogramowania, dokumentacji i raporty dla projektów języka Java będzie maven.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-107">Maven is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="ca4fe-108">Kroki opisane w tym dokumencie zostały ostatnio przetestowana 3,6 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-108">The steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca4fe-109">Kroki opisane w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-109">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="ca4fe-110">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ca4fe-111">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="ca4fe-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="ca4fe-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="ca4fe-112">Requirements</span></span>

* <span data-ttu-id="ca4fe-113">[Platformy Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ca4fe-114">HDInsight w wersji 3.5 lub nowszej wymaga Java 8.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="ca4fe-115">Wcześniejszych wersji usługi hdinsight wymagają Java 7.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="ca4fe-116">Maven</span><span class="sxs-lookup"><span data-stu-id="ca4fe-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="ca4fe-117">Klaster HDInsight Azure opartej na systemie Linux z bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="ca4fe-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="ca4fe-118">Kroki opisane w tym dokumencie zostały przetestowane w wersjach klastra usługi HDInsight 3.4 i 3.5.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-118">The steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="ca4fe-119">Wartości domyślnych w przykładach są dla klastra usługi HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-119">The default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="ca4fe-120">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="ca4fe-120">Create the project</span></span>

1. <span data-ttu-id="ca4fe-121">Z poziomu wiersza polecenia w środowisku projektowania, przejdź do lokalizacji, w której chcesz utworzyć projekt, na przykład `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-121">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="ca4fe-122">Użyj **mvn** polecenia, które jest instalowany z Maven, aby wygenerować funkcją szkieletów dla projektu.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-122">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="ca4fe-123">Jeśli używasz programu PowerShell, należy ująć `-D` parametrów w podwójny cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-123">If you are using PowerShell, you must enclose the `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="ca4fe-124">To polecenie tworzy katalog o tej samej nazwie jako **artifactID** parametr (**hbaseapp** w tym przykładzie.) Ten katalog zawiera następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-124">This command creates a directory with the same name as the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="ca4fe-125">**pom.XML**: projektu Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) zawiera informacje i szczegóły konfiguracji używany do tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-125">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="ca4fe-126">**SRC**: katalog, który zawiera **main/java/com/microsoft/przykłady** katalogu, w którym autor aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-126">**src**: The directory that contains the **main/java/com/microsoft/examples** directory, where you author the application.</span></span>

3. <span data-ttu-id="ca4fe-127">Usuń `src/test/java/com/microsoft/examples/apptest.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-127">Delete the `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="ca4fe-128">Nie można użyć w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-128">It is not be used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="ca4fe-129">Aktualizacja modelu obiektowego projektu</span><span class="sxs-lookup"><span data-stu-id="ca4fe-129">Update the Project Object Model</span></span>

1. <span data-ttu-id="ca4fe-130">Edytuj `pom.xml` i Dodaj następujący kod w `<dependencies>` sekcji:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-130">Edit the `pom.xml` file and add the following code inside the `<dependencies>` section:</span></span>

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

    <span data-ttu-id="ca4fe-131">W tej sekcji wskazuje, że projekt wymaga **klienta hbase** i **phoenix core** składników.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-131">This section indicates that the project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="ca4fe-132">W czasie kompilacji te zależności są pobierane z repozytorium Maven domyślne.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-132">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="ca4fe-133">Można użyć [Maven centralnym repozytorium wyszukiwania](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) Aby dowiedzieć się więcej na temat tej zależności.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-133">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ca4fe-134">Numer wersji klienta hbase musi odpowiadać wersji bazy danych HBase, która jest dostarczana z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-134">The version number of the hbase-client must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="ca4fe-135">Skorzystaj z poniższej tabeli, aby znaleźć poprawnej wersji numer.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-135">Use the following table to find the correct version number.</span></span>

   | <span data-ttu-id="ca4fe-136">Wersja klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="ca4fe-136">HDInsight cluster version</span></span> | <span data-ttu-id="ca4fe-137">Wersja bazy danych HBase do użycia</span><span class="sxs-lookup"><span data-stu-id="ca4fe-137">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="ca4fe-138">3.2</span><span class="sxs-lookup"><span data-stu-id="ca4fe-138">3.2</span></span> |<span data-ttu-id="ca4fe-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="ca4fe-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="ca4fe-140">3.3, 3.4, 3.5 i 3,6</span><span class="sxs-lookup"><span data-stu-id="ca4fe-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="ca4fe-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="ca4fe-141">1.1.2</span></span> |

    <span data-ttu-id="ca4fe-142">Aby uzyskać więcej informacji o wersji usługi HDInsight i składników, zobacz [co to są dostępne z usługą HDInsight różnych składników Hadoop](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ca4fe-142">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="ca4fe-143">Dodaj następujący kod do **pom.xml** pliku.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-143">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="ca4fe-144">Ten tekst musi znajdować się wewnątrz `<project>...</project>` tagów w pliku, na przykład między `</dependencies>` i `</project>`.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-144">This text must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="ca4fe-145">W tej sekcji konfiguruje zasobu (`conf/hbase-site.xml`) zawiera informacje o konfiguracji dla bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ca4fe-146">Można również ustawić wartości konfiguracji za pomocą kodu.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-146">You can also set configuration values via code.</span></span> <span data-ttu-id="ca4fe-147">Zobacz komentarze w `CreateTable` przykład.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-147">See the comments in the `CreateTable` example.</span></span>

    <span data-ttu-id="ca4fe-148">W tej sekcji konfiguruje również [wtyczki kompilatora Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) i [Maven cień wtyczki](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="ca4fe-148">This section also configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="ca4fe-149">Kompilator wtyczka jest używana do kompilowania topologii.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-149">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="ca4fe-150">Wtyczka cień jest używany do chronienia duplikatów licencji w pakiecie JAR, który jest konstruowany przez Maven.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-150">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="ca4fe-151">Ten dodatek jest używany do chronienia błąd "licencji duplikatów plików" w czasie wykonywania w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-151">This plugin is used to prevent a "duplicate license files" error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="ca4fe-152">Przy użyciu narzędzia maven cień wtyczki o `ApacheLicenseResourceTransformer` błąd uniemożliwia implementacji.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-152">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents the error.</span></span>

    <span data-ttu-id="ca4fe-153">Wtyczka cień maven tworzy również jar pełny, który zawiera wszystkie zależności wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-153">The maven-shade-plugin also produces an uber jar that contains all the dependencies required by the application.</span></span>

4. <span data-ttu-id="ca4fe-154">Zapisz `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-154">Save the `pom.xml` file.</span></span>

5. <span data-ttu-id="ca4fe-155">Utwórz katalog o nazwie `conf` w `hbaseapp` katalogu.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-155">Create a directory named `conf` in the `hbaseapp` directory.</span></span> <span data-ttu-id="ca4fe-156">Ten katalog jest używany do przechowywania informacji o konfiguracji w celu nawiązania HBase.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-156">This directory is used to hold configuration information for connecting to HBase.</span></span>

6. <span data-ttu-id="ca4fe-157">Użyj następującego polecenia umożliwia kopiowanie konfiguracji bazy danych HBase z klastra HBase `conf` katalogu.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-157">Use the following command to copy the HBase configuration from the HBase cluster to the `conf` directory.</span></span> <span data-ttu-id="ca4fe-158">Zastąp `USERNAME` o nazwie logowanie SSH.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-158">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="ca4fe-159">Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="ca4fe-160">Aby uzyskać więcej informacji na temat używania `ssh` i `scp`, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ca4fe-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-the-application"></a><span data-ttu-id="ca4fe-161">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="ca4fe-161">Create the application</span></span>

1. <span data-ttu-id="ca4fe-162">Przejdź do `hbaseapp/src/main/java/com/microsoft/examples` katalogu i app.java Zmień nazwę pliku na `CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-162">Go to the `hbaseapp/src/main/java/com/microsoft/examples` directory and rename the app.java file to `CreateTable.java`.</span></span>

2. <span data-ttu-id="ca4fe-163">Otwórz `CreateTable.java` plików i zastąpić istniejącą zawartość z następującym tekstem:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-163">Open the `CreateTable.java` file and replace the existing contents with the following text:</span></span>

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

    <span data-ttu-id="ca4fe-164">Ten kod jest **CreateTable** klasy, która tworzy tabelę o nazwie **osób** i wypełnić ją w przypadku niektórych użytkowników wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-164">This code is the **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="ca4fe-165">Zapisz `CreateTable.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-165">Save the `CreateTable.java` file.</span></span>

4. <span data-ttu-id="ca4fe-166">W `hbaseapp/src/main/java/com/microsoft/examples` katalogu, Utwórz plik o nazwie `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-166">In the `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="ca4fe-167">Zawartość tego pliku, należy użyć następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-167">Use the following text as the contents of this file:</span></span>

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

    <span data-ttu-id="ca4fe-168">**SearchByEmail** klasa może być używana do zapytania dla wierszy za pomocą adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-168">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="ca4fe-169">Ponieważ używa filtra wyrażenia regularnego, musisz podać ciąg lub wyrażenie regularne, przy użyciu klasy.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>

5. <span data-ttu-id="ca4fe-170">Zapisz `SearchByEmail.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-170">Save the `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="ca4fe-171">W `hbaseapp/src/main/hava/com/microsoft/examples` katalogu, Utwórz plik o nazwie `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-171">In the `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="ca4fe-172">Zawartość tego pliku, należy użyć następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-172">Use the following text as the contents of this file:</span></span>

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

    <span data-ttu-id="ca4fe-173">Ta klasa czyści tabele bazy danych HBase utworzone w tym przykładzie, wyłączając i upuszczanie tabeli utworzone przez `CreateTable` klasy.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-173">This class cleans up the HBase tables created in this example by disabling and dropping the table created by the `CreateTable` class.</span></span>

7. <span data-ttu-id="ca4fe-174">Zapisz `DeleteTable.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-174">Save the `DeleteTable.java` file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="ca4fe-175">Tworzenie i pakiet aplikacji</span><span class="sxs-lookup"><span data-stu-id="ca4fe-175">Build and package the application</span></span>

1. <span data-ttu-id="ca4fe-176">Z `hbaseapp` katalogu, użyj następującego polecenia, aby utworzyć plik JAR zawierający aplikację:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-176">From the `hbaseapp` directory, use the following command to build a JAR file that contains the application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="ca4fe-177">To polecenie tworzy i pakiety aplikacji do pliku JAR.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-177">This command builds and packages the application into a .jar file.</span></span>

2. <span data-ttu-id="ca4fe-178">Po zakończeniu wykonywania polecenia `hbaseapp/target` katalog zawiera plik o nazwie `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-178">When the command completes, the `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ca4fe-179">`hbaseapp-1.0-SNAPSHOT.jar` Plik jest jar pełny.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-179">The `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="ca4fe-180">Zawiera wszystkie zależności wymagane do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-180">It contains all the dependencies required to run the application.</span></span>


## <a name="upload-the-jar-and-run-jobs-ssh"></a><span data-ttu-id="ca4fe-181">Przekaż JAR i uruchom zadania (SSH)</span><span class="sxs-lookup"><span data-stu-id="ca4fe-181">Upload the JAR and run jobs (SSH)</span></span>

<span data-ttu-id="ca4fe-182">Następujące kroki użyj `scp` do skopiowania JAR do głównej węzła głównego hbase sieci w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-182">The following steps use `scp` to copy the JAR to the primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="ca4fe-183">`ssh` Polecenia jest następnie używany do nawiązania połączenia klastra i uruchomić przykład bezpośrednio w węźle głównym.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-183">The `ssh` command is then used to connect to the cluster and run the example directly on the head node.</span></span>

1. <span data-ttu-id="ca4fe-184">Aby przekazać jar do klastra, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-184">To upload the jar to the cluster, use the following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="ca4fe-185">Zastąp `USERNAME` o nazwie logowanie SSH.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-185">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="ca4fe-186">Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="ca4fe-187">Aby połączyć się klastra HBase, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-187">To connect to the HBase cluster, use the following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="ca4fe-188">Zastąp `USERNAME` nazwę użytkownika logowania SSH.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-188">Replace `USERNAME` the name of your SSH login.</span></span> <span data-ttu-id="ca4fe-189">Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="ca4fe-190">Do tworzenia tabel HBase przy użyciu aplikacji Java, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-190">To create an HBase table using the Java application, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="ca4fe-191">To polecenie tworzy tabelę HBase o nazwie **osoby**i wypełnia danych.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="ca4fe-192">Aby wyszukać adresy e-mail przechowywane w tabeli, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-192">To search for email addresses stored in the table, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="ca4fe-193">Pojawi się następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-193">You receive the following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="ca4fe-194">Aby usunąć tabeli, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-194">To delete the table, use the following command:</span></span>

    

## <a name="upload-the-jar-and-run-jobs-powershell"></a><span data-ttu-id="ca4fe-195">Przekaż JAR i uruchom zadania (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="ca4fe-195">Upload the JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="ca4fe-196">Poniższe kroki przekazać JAR do magazynu domyślnego dla klastra HBase przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-196">The following steps use Azure PowerShell to upload the JAR to the default storage for your HBase cluster.</span></span> <span data-ttu-id="ca4fe-197">Polecenia cmdlet usługi HDInsight są następnie używane do uruchamiania w przykładach zdalnie.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-197">HDInsight cmdlets are then used to run the examples remotely.</span></span>

1. <span data-ttu-id="ca4fe-198">Po zainstalowaniu i skonfigurowaniu programu Azure PowerShell Utwórz plik o nazwie `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="ca4fe-199">Zawartość tego pliku, należy użyć następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-199">Use the following text as the contents of this file:</span></span>

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

    <span data-ttu-id="ca4fe-200">Ten plik zawiera dwa moduły:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-200">This file contains two modules:</span></span>

   * <span data-ttu-id="ca4fe-201">**Dodaj HDInsightFile** — umożliwia przekazywanie plików do klastra</span><span class="sxs-lookup"><span data-stu-id="ca4fe-201">**Add-HDInsightFile** - used to upload files to the cluster</span></span>
   * <span data-ttu-id="ca4fe-202">**Początek HBaseExample** — używany do uruchamiania klasy utworzony wcześniej</span><span class="sxs-lookup"><span data-stu-id="ca4fe-202">**Start-HBaseExample** - used to run the classes created earlier</span></span>

2. <span data-ttu-id="ca4fe-203">Zapisz `hbase-runner.psm1` pliku.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-203">Save the `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="ca4fe-204">Otwórz nowe okno programu Azure PowerShell, przejdź do `hbaseapp` katalogu, a następnie uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-204">Open a new Azure PowerShell window, change directories to the `hbaseapp` directory, and then run the following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="ca4fe-205">Zmień ścieżkę do lokalizacji `hbase-runner.psm1` wcześniej utworzony plik.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-205">Change the path to the location of the `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="ca4fe-206">To polecenie rejestruje moduł przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-206">This command registers the module with Azure PowerShell.</span></span>

4. <span data-ttu-id="ca4fe-207">Użyj następującego polecenia do przekazania `hbaseapp-1.0-SNAPSHOT.jar` do klastra.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-207">Use the following command to upload the `hbaseapp-1.0-SNAPSHOT.jar` to your cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="ca4fe-208">Zastąp ciąg `hdinsightclustername` nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-208">Replace `hdinsightclustername` with the name of your cluster.</span></span> <span data-ttu-id="ca4fe-209">Polecenie przekazuje `hbaseapp-1.0-SNAPSHOT.jar` do `example/jars` lokalizacji w pamięci głównej dla klastra.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-209">The command uploads the `hbaseapp-1.0-SNAPSHOT.jar` to the `example/jars` location in the primary storage for your cluster.</span></span>

5. <span data-ttu-id="ca4fe-210">Aby utworzyć tabelę przy użyciu `hbaseapp`, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-210">To create a table using the `hbaseapp`, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="ca4fe-211">Zastąp ciąg `hdinsightclustername` nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-211">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="ca4fe-212">To polecenie tworzy tabeli o nazwie **osób** w bazie danych HBase w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="ca4fe-213">To polecenie nie wyświetla żadnych danych wyjściowych w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-213">This command does not show any output in the console window.</span></span>

6. <span data-ttu-id="ca4fe-214">Aby wyszukać wpisów w tabeli, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-214">To search for entries in the table, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="ca4fe-215">Zastąp ciąg `hdinsightclustername` nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-215">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="ca4fe-216">To polecenie używa `SearchByEmail` klasę, aby wyszukać wszystkie wiersze gdzie `contactinformation` rodziny kolumn i `email` kolumny zawiera ciąg `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-216">This command uses the `SearchByEmail` class to search for any rows where the `contactinformation` column family and the `email` column, contains the string `contoso.com`.</span></span> <span data-ttu-id="ca4fe-217">Powinien zostać wyświetlony następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-217">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="ca4fe-218">Przy użyciu **fabrikam.com** dla `-emailRegex` użytkowników, którzy mają zwraca wartość **fabrikam.com** w pole adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-218">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="ca4fe-219">Można również używać wyrażeń regularnych jako terminu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-219">You can also use regular expressions as the search term.</span></span> <span data-ttu-id="ca4fe-220">Na przykład **^ r** zwraca e-mail adresów, które zaczynają się od litery "r".</span><span class="sxs-lookup"><span data-stu-id="ca4fe-220">For example, **^r** returns email addresses that begin with the letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="ca4fe-221">Nie wyników lub nieoczekiwane wyniki, korzystając z Start HBaseExample</span><span class="sxs-lookup"><span data-stu-id="ca4fe-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="ca4fe-222">Użyj `-showErr` parametr, aby wyświetlić błąd standardowy (STDERR) jest tworzony podczas uruchamiania zadania.</span><span class="sxs-lookup"><span data-stu-id="ca4fe-222">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="ca4fe-223">Usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="ca4fe-223">Delete the table</span></span>

<span data-ttu-id="ca4fe-224">Gdy wszystko będzie gotowe do przykładu, aby usunąć należy użyć następującego **osób** Tabela używana w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-224">When you are done with the example, use the following to delete the **people** table used in this example:</span></span>

<span data-ttu-id="ca4fe-225">__Z `ssh` sesji__:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="ca4fe-226">__Z programu Azure PowerShell__:</span><span class="sxs-lookup"><span data-stu-id="ca4fe-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="ca4fe-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ca4fe-227">Next steps</span></span>

[<span data-ttu-id="ca4fe-228">Dowiedz się, jak korzystać z SQuirreL SQL z bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="ca4fe-228">Learn how to use SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
