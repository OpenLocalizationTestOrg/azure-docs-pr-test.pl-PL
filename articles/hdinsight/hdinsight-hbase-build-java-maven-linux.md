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
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="10910-103">Tworzenie aplikacji Java dla bazy danych Apache HBase</span><span class="sxs-lookup"><span data-stu-id="10910-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="10910-104">Dowiedz się, jak toocreate [bazy danych Apache HBase](http://hbase.apache.org/) aplikacji w języku Java.</span><span class="sxs-lookup"><span data-stu-id="10910-104">Learn how toocreate an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="10910-105">Z bazy danych HBase w usłudze Azure HDInsight za pomocą aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="10910-105">Then use hello application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="10910-106">Witaj kroków w tym dokumencie [Maven](http://maven.apache.org/) toocreate i kompilacji projektu hello.</span><span class="sxs-lookup"><span data-stu-id="10910-106">hello steps in this document use [Maven](http://maven.apache.org/) toocreate and build hello project.</span></span> <span data-ttu-id="10910-107">Zarządzanie projektami oprogramowania i zrozumienia narzędzie, które umożliwia toobuild oprogramowania, dokumentacji i raporty dla projektów języka Java będzie maven.</span><span class="sxs-lookup"><span data-stu-id="10910-107">Maven is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="10910-108">Witaj kroki opisane w tym dokumencie zostały ostatnio przetestowana 3,6 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10910-108">hello steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10910-109">kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="10910-109">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="10910-110">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="10910-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="10910-111">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="10910-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="10910-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="10910-112">Requirements</span></span>

* <span data-ttu-id="10910-113">[Platformy Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="10910-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="10910-114">HDInsight w wersji 3.5 lub nowszej wymaga Java 8.</span><span class="sxs-lookup"><span data-stu-id="10910-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="10910-115">Wcześniejszych wersji usługi hdinsight wymagają Java 7.</span><span class="sxs-lookup"><span data-stu-id="10910-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="10910-116">Maven</span><span class="sxs-lookup"><span data-stu-id="10910-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="10910-117">Klaster HDInsight Azure opartej na systemie Linux z bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="10910-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="10910-118">kroki Hello w tym dokumencie zostały przetestowane w wersjach klastra usługi HDInsight 3.4 i 3.5.</span><span class="sxs-lookup"><span data-stu-id="10910-118">hello steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="10910-119">wartości domyślnych Hello w przykładach są dla klastra usługi HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="10910-119">hello default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="10910-120">Utwórz projekt hello</span><span class="sxs-lookup"><span data-stu-id="10910-120">Create hello project</span></span>

1. <span data-ttu-id="10910-121">W wierszu polecenia hello w środowisku projektowania Zmień katalogi toohello lokalizację toocreate hello projektu, na przykład `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="10910-121">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="10910-122">Użyj hello **mvn** polecenia, który jest instalowany z Maven, hello toogenerate tworzenia szkieletu do projektu hello.</span><span class="sxs-lookup"><span data-stu-id="10910-122">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="10910-123">Jeśli używasz programu PowerShell, należy ująć hello `-D` parametrów w podwójny cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="10910-123">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="10910-124">To polecenie tworzy katalog z hello sama nazwa jak hello **artifactID** parametr (**hbaseapp** w tym przykładzie.) Ten katalog zawiera hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="10910-124">This command creates a directory with hello same name as hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="10910-125">**pom.XML**: hello projektu Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) zawiera informacje i konfiguracji projektu hello toobuild szczegóły używanego.</span><span class="sxs-lookup"><span data-stu-id="10910-125">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="10910-126">**SRC**: hello katalog, który zawiera hello **main/java/com/microsoft/przykłady** katalogu, w którym autor aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="10910-126">**src**: hello directory that contains hello **main/java/com/microsoft/examples** directory, where you author hello application.</span></span>

3. <span data-ttu-id="10910-127">Usuń hello `src/test/java/com/microsoft/examples/apptest.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="10910-127">Delete hello `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="10910-128">Nie można użyć w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="10910-128">It is not be used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="10910-129">Aktualizacja hello modelu obiektowego projektu</span><span class="sxs-lookup"><span data-stu-id="10910-129">Update hello Project Object Model</span></span>

1. <span data-ttu-id="10910-130">Edytuj hello `pom.xml` plik i dodać hello następującego kodu wewnątrz hello `<dependencies>` sekcji:</span><span class="sxs-lookup"><span data-stu-id="10910-130">Edit hello `pom.xml` file and add hello following code inside hello `<dependencies>` section:</span></span>

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

    <span data-ttu-id="10910-131">W tej sekcji wskazuje projekt hello musi **klienta hbase** i **phoenix core** składników.</span><span class="sxs-lookup"><span data-stu-id="10910-131">This section indicates that hello project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="10910-132">W czasie kompilacji te zależności są pobierane z hello domyślne Maven repozytorium.</span><span class="sxs-lookup"><span data-stu-id="10910-132">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="10910-133">Można użyć hello [Maven centralnym repozytorium wyszukiwania](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn więcej informacji na temat tej zależności.</span><span class="sxs-lookup"><span data-stu-id="10910-133">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="10910-134">numer wersji Hello hello hbase klient musi odpowiadać wersji hello HBase, która jest dostarczana z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10910-134">hello version number of hello hbase-client must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="10910-135">Użyj powitania po numer poprawną wersję hello toofind tabeli.</span><span class="sxs-lookup"><span data-stu-id="10910-135">Use hello following table toofind hello correct version number.</span></span>

   | <span data-ttu-id="10910-136">Wersja klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="10910-136">HDInsight cluster version</span></span> | <span data-ttu-id="10910-137">Toouse wersji bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="10910-137">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="10910-138">3.2</span><span class="sxs-lookup"><span data-stu-id="10910-138">3.2</span></span> |<span data-ttu-id="10910-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="10910-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="10910-140">3.3, 3.4, 3.5 i 3,6</span><span class="sxs-lookup"><span data-stu-id="10910-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="10910-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="10910-141">1.1.2</span></span> |

    <span data-ttu-id="10910-142">Aby uzyskać więcej informacji o wersji usługi HDInsight i składników, zobacz [co to są hello różne składniki platformy Hadoop dostępne z usługą HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="10910-142">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="10910-143">Dodaj hello następującego kodu toohello **pom.xml** pliku.</span><span class="sxs-lookup"><span data-stu-id="10910-143">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="10910-144">Ten tekst musi znajdować się wewnątrz hello `<project>...</project>` tagów w hello plików, na przykład między `</dependencies>` i `</project>`.</span><span class="sxs-lookup"><span data-stu-id="10910-144">This text must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="10910-145">W tej sekcji konfiguruje zasobu (`conf/hbase-site.xml`) zawiera informacje o konfiguracji dla bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="10910-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="10910-146">Można również ustawić wartości konfiguracji za pomocą kodu.</span><span class="sxs-lookup"><span data-stu-id="10910-146">You can also set configuration values via code.</span></span> <span data-ttu-id="10910-147">Zobacz komentarze hello w hello `CreateTable` przykład.</span><span class="sxs-lookup"><span data-stu-id="10910-147">See hello comments in hello `CreateTable` example.</span></span>

    <span data-ttu-id="10910-148">W tej sekcji konfiguruje również hello [wtyczki kompilatora Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) i [Maven cień wtyczki](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="10910-148">This section also configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="10910-149">wtyczki kompilatora Hello jest używane toocompile hello topologii.</span><span class="sxs-lookup"><span data-stu-id="10910-149">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="10910-150">Wtyczka cień Hello jest duplikatów licencji tooprevent używane w pakiecie JAR hello jest konstruowany przez Maven.</span><span class="sxs-lookup"><span data-stu-id="10910-150">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="10910-151">Ten dodatek jest używane tooprevent "duplikatów plików licencji" Błąd w czasie wykonywania w klastrze usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="10910-151">This plugin is used tooprevent a "duplicate license files" error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="10910-152">Przy użyciu maven cień wtyczki z hello `ApacheLicenseResourceTransformer` hello błąd uniemożliwia implementacji.</span><span class="sxs-lookup"><span data-stu-id="10910-152">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents hello error.</span></span>

    <span data-ttu-id="10910-153">Witaj maven cień wtyczki tworzy również jar pełny, który zawiera wszystkie zależności hello wymagane przez aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="10910-153">hello maven-shade-plugin also produces an uber jar that contains all hello dependencies required by hello application.</span></span>

4. <span data-ttu-id="10910-154">Zapisz hello `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="10910-154">Save hello `pom.xml` file.</span></span>

5. <span data-ttu-id="10910-155">Utwórz katalog o nazwie `conf` w hello `hbaseapp` katalogu.</span><span class="sxs-lookup"><span data-stu-id="10910-155">Create a directory named `conf` in hello `hbaseapp` directory.</span></span> <span data-ttu-id="10910-156">Informacje o konfiguracji toohold używane do łączenia tooHBase jest to katalog.</span><span class="sxs-lookup"><span data-stu-id="10910-156">This directory is used toohold configuration information for connecting tooHBase.</span></span>

6. <span data-ttu-id="10910-157">Użyj hello następujące polecenie toocopy hello HBase konfigurację z toohello klastra HBase hello `conf` katalogu.</span><span class="sxs-lookup"><span data-stu-id="10910-157">Use hello following command toocopy hello HBase configuration from hello HBase cluster toohello `conf` directory.</span></span> <span data-ttu-id="10910-158">Zastąp `USERNAME` o nazwie hello logowanie SSH.</span><span class="sxs-lookup"><span data-stu-id="10910-158">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="10910-159">Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="10910-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="10910-160">Aby uzyskać więcej informacji na temat używania `ssh` i `scp`, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="10910-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="10910-161">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="10910-161">Create hello application</span></span>

1. <span data-ttu-id="10910-162">Przejdź toohello `hbaseapp/src/main/java/com/microsoft/examples` katalogu i Zmień nazwę hello pliku app.java zbyt`CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="10910-162">Go toohello `hbaseapp/src/main/java/com/microsoft/examples` directory and rename hello app.java file too`CreateTable.java`.</span></span>

2. <span data-ttu-id="10910-163">Otwórz hello `CreateTable.java` plików i zastąpić istniejącą zawartość hello hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="10910-163">Open hello `CreateTable.java` file and replace hello existing contents with hello following text:</span></span>

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

    <span data-ttu-id="10910-164">Ten kod jest hello **CreateTable** klasy, która tworzy tabelę o nazwie **osób** i wypełnić ją w przypadku niektórych użytkowników wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="10910-164">This code is hello **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="10910-165">Zapisz hello `CreateTable.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="10910-165">Save hello `CreateTable.java` file.</span></span>

4. <span data-ttu-id="10910-166">W hello `hbaseapp/src/main/java/com/microsoft/examples` katalogu, Utwórz plik o nazwie `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="10910-166">In hello `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="10910-167">Użyj hello następującego tekstu jako hello zawartość tego pliku:</span><span class="sxs-lookup"><span data-stu-id="10910-167">Use hello following text as hello contents of this file:</span></span>

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

    <span data-ttu-id="10910-168">Witaj **SearchByEmail** klasa może być używana tooquery wierszy za pomocą adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="10910-168">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="10910-169">Ponieważ używa filtra wyrażenia regularnego, musisz podać ciąg lub wyrażenie regularne używając hello klasy.</span><span class="sxs-lookup"><span data-stu-id="10910-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>

5. <span data-ttu-id="10910-170">Zapisz hello `SearchByEmail.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="10910-170">Save hello `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="10910-171">W hello `hbaseapp/src/main/hava/com/microsoft/examples` katalogu, Utwórz plik o nazwie `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="10910-171">In hello `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="10910-172">Użyj hello następującego tekstu jako hello zawartość tego pliku:</span><span class="sxs-lookup"><span data-stu-id="10910-172">Use hello following text as hello contents of this file:</span></span>

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

    <span data-ttu-id="10910-173">Ta klasa czyści hello tabel HBase utworzone w tym przykładzie, wyłączając i upuszczanie tabeli hello tworzone przez hello `CreateTable` klasy.</span><span class="sxs-lookup"><span data-stu-id="10910-173">This class cleans up hello HBase tables created in this example by disabling and dropping hello table created by hello `CreateTable` class.</span></span>

7. <span data-ttu-id="10910-174">Zapisz hello `DeleteTable.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="10910-174">Save hello `DeleteTable.java` file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="10910-175">Aplikacja hello kompilacji i pakietu</span><span class="sxs-lookup"><span data-stu-id="10910-175">Build and package hello application</span></span>

1. <span data-ttu-id="10910-176">Z hello `hbaseapp` katalogu, użyj hello następujące polecenie toobuild plik JAR zawierający aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="10910-176">From hello `hbaseapp` directory, use hello following command toobuild a JAR file that contains hello application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="10910-177">To polecenie tworzy i aplikacji do pliku JAR hello pakietów.</span><span class="sxs-lookup"><span data-stu-id="10910-177">This command builds and packages hello application into a .jar file.</span></span>

2. <span data-ttu-id="10910-178">Po polecenie hello zakończeniu hello `hbaseapp/target` katalog zawiera plik o nazwie `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="10910-178">When hello command completes, hello `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="10910-179">Witaj `hbaseapp-1.0-SNAPSHOT.jar` plik jest jar pełny.</span><span class="sxs-lookup"><span data-stu-id="10910-179">hello `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="10910-180">Zawiera wszystkie hello zależności wymagane toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10910-180">It contains all hello dependencies required toorun hello application.</span></span>


## <a name="upload-hello-jar-and-run-jobs-ssh"></a><span data-ttu-id="10910-181">Przekaż hello JAR i uruchom zadania (SSH)</span><span class="sxs-lookup"><span data-stu-id="10910-181">Upload hello JAR and run jobs (SSH)</span></span>

<span data-ttu-id="10910-182">Witaj, użyj czynności po `scp` toocopy hello JAR toohello głównej węzła głównego hbase sieci w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10910-182">hello following steps use `scp` toocopy hello JAR toohello primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="10910-183">Witaj `ssh` polecenie jest następnie używany tooconnect toohello klastra i uruchom przykład Witaj bezpośrednio na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="10910-183">hello `ssh` command is then used tooconnect toohello cluster and run hello example directly on hello head node.</span></span>

1. <span data-ttu-id="10910-184">tooupload hello jar toohello klaster, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="10910-184">tooupload hello jar toohello cluster, use hello following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="10910-185">Zastąp `USERNAME` o nazwie hello logowanie SSH.</span><span class="sxs-lookup"><span data-stu-id="10910-185">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="10910-186">Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10910-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="10910-187">klaster HBase toohello tooconnect, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="10910-187">tooconnect toohello HBase cluster, use hello following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="10910-188">Zastąp `USERNAME` hello nazwa logowania użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="10910-188">Replace `USERNAME` hello name of your SSH login.</span></span> <span data-ttu-id="10910-189">Zastąp `CLUSTERNAME` nazwą klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10910-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="10910-190">toocreate tabeli HBase przy użyciu hello aplikacji Java, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="10910-190">toocreate an HBase table using hello Java application, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="10910-191">To polecenie tworzy tabelę HBase o nazwie **osoby**i wypełnia danych.</span><span class="sxs-lookup"><span data-stu-id="10910-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="10910-192">toosearch adresów e-mail, przechowywane w tabeli hello, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="10910-192">toosearch for email addresses stored in hello table, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="10910-193">Pojawi się hello następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="10910-193">You receive hello following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="10910-194">toodelete hello tabeli hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="10910-194">toodelete hello table, use hello following command:</span></span>

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a><span data-ttu-id="10910-195">Przekaż hello JAR i uruchom zadania (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="10910-195">Upload hello JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="10910-196">Hello następujące kroki, użyj programu Azure PowerShell tooupload hello JAR toohello domyślny magazyn dla klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="10910-196">hello following steps use Azure PowerShell tooupload hello JAR toohello default storage for your HBase cluster.</span></span> <span data-ttu-id="10910-197">Polecenia cmdlet usługi HDInsight są następnie używane toorun hello przykłady zdalnie.</span><span class="sxs-lookup"><span data-stu-id="10910-197">HDInsight cmdlets are then used toorun hello examples remotely.</span></span>

1. <span data-ttu-id="10910-198">Po zainstalowaniu i skonfigurowaniu programu Azure PowerShell Utwórz plik o nazwie `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="10910-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="10910-199">Użyj hello następującego tekstu jako hello zawartość tego pliku:</span><span class="sxs-lookup"><span data-stu-id="10910-199">Use hello following text as hello contents of this file:</span></span>

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

    <span data-ttu-id="10910-200">Ten plik zawiera dwa moduły:</span><span class="sxs-lookup"><span data-stu-id="10910-200">This file contains two modules:</span></span>

   * <span data-ttu-id="10910-201">**Dodaj HDInsightFile** — używane tooupload pliki toohello klastra</span><span class="sxs-lookup"><span data-stu-id="10910-201">**Add-HDInsightFile** - used tooupload files toohello cluster</span></span>
   * <span data-ttu-id="10910-202">**Start-HBaseExample** -używane klasy hello toorun utworzony wcześniej</span><span class="sxs-lookup"><span data-stu-id="10910-202">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>

2. <span data-ttu-id="10910-203">Zapisz hello `hbase-runner.psm1` pliku.</span><span class="sxs-lookup"><span data-stu-id="10910-203">Save hello `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="10910-204">Otwórz nowe okno programu Azure PowerShell, zmień katalogi toohello `hbaseapp` katalogu, a następnie hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="10910-204">Open a new Azure PowerShell window, change directories toohello `hbaseapp` directory, and then run hello following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="10910-205">Zmienić lokalizację toohello ścieżka hello hello `hbase-runner.psm1` wcześniej utworzony plik.</span><span class="sxs-lookup"><span data-stu-id="10910-205">Change hello path toohello location of hello `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="10910-206">To polecenie rejestruje hello modułu przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10910-206">This command registers hello module with Azure PowerShell.</span></span>

4. <span data-ttu-id="10910-207">Użyj hello następujące polecenie tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour klastra.</span><span class="sxs-lookup"><span data-stu-id="10910-207">Use hello following command tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="10910-208">Zastąp `hdinsightclustername` o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="10910-208">Replace `hdinsightclustername` with hello name of your cluster.</span></span> <span data-ttu-id="10910-209">polecenie Hello przekazuje hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` lokalizacji w hello podstawowy magazyn dla klastra.</span><span class="sxs-lookup"><span data-stu-id="10910-209">hello command uploads hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` location in hello primary storage for your cluster.</span></span>

5. <span data-ttu-id="10910-210">Witaj toocreate tabeli za pomocą `hbaseapp`, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="10910-210">toocreate a table using hello `hbaseapp`, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="10910-211">Zastąp `hdinsightclustername` o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="10910-211">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="10910-212">To polecenie tworzy tabeli o nazwie **osób** w bazie danych HBase w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="10910-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="10910-213">To polecenie nie wyświetla żadnych danych wyjściowych w oknie konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="10910-213">This command does not show any output in hello console window.</span></span>

6. <span data-ttu-id="10910-214">toosearch wpisy tabeli hello hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="10910-214">toosearch for entries in hello table, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="10910-215">Zastąp `hdinsightclustername` o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="10910-215">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="10910-216">To polecenie używa hello `SearchByEmail` klasy toosearch wierszy, gdzie hello `contactinformation` rodziny kolumn i hello `email` kolumny zawiera ciąg hello `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="10910-216">This command uses hello `SearchByEmail` class toosearch for any rows where hello `contactinformation` column family and hello `email` column, contains hello string `contoso.com`.</span></span> <span data-ttu-id="10910-217">Powinien zostać wyświetlony hello następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="10910-217">You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="10910-218">Przy użyciu **fabrikam.com** dla hello `-emailRegex` wartość zwraca hello użytkowników, którzy mają **fabrikam.com** hello pola wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="10910-218">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="10910-219">Można również używać wyrażeń regularnych jako hello wyszukiwanego terminu.</span><span class="sxs-lookup"><span data-stu-id="10910-219">You can also use regular expressions as hello search term.</span></span> <span data-ttu-id="10910-220">Na przykład **^ r** zwraca e-mail adresów, które zaczynają się od litery hello "r".</span><span class="sxs-lookup"><span data-stu-id="10910-220">For example, **^r** returns email addresses that begin with hello letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="10910-221">Nie wyników lub nieoczekiwane wyniki, korzystając z Start HBaseExample</span><span class="sxs-lookup"><span data-stu-id="10910-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="10910-222">Użyj hello `-showErr` tooview hello standardowy błąd parametru (STDERR) utworzonym podczas wykonywanym zadaniem hello.</span><span class="sxs-lookup"><span data-stu-id="10910-222">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="10910-223">Usuń tabelę hello</span><span class="sxs-lookup"><span data-stu-id="10910-223">Delete hello table</span></span>

<span data-ttu-id="10910-224">Po wykonaniu przykład Witaj, użyj następującego toodelete hello hello **osób** Tabela używana w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="10910-224">When you are done with hello example, use hello following toodelete hello **people** table used in this example:</span></span>

<span data-ttu-id="10910-225">__Z `ssh` sesji__:</span><span class="sxs-lookup"><span data-stu-id="10910-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="10910-226">__Z programu Azure PowerShell__:</span><span class="sxs-lookup"><span data-stu-id="10910-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="10910-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10910-227">Next steps</span></span>

[<span data-ttu-id="10910-228">Dowiedz się, jak toouse SQuirreL SQL z bazą danych HBase</span><span class="sxs-lookup"><span data-stu-id="10910-228">Learn how toouse SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
