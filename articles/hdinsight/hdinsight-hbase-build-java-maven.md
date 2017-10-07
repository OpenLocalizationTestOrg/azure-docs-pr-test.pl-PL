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
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="d5be0-103">Użyj aplikacji Java toobuild Maven, które używają bazy danych HBase z systemem Windows HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="d5be0-103">Use Maven toobuild Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="d5be0-104">Dowiedz się, jak toocreate i kompilacji [bazy danych Apache HBase](http://hbase.apache.org/) aplikacji w języku Java za pomocą Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="d5be0-104">Learn how toocreate and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="d5be0-105">Następnie za pomocą aplikacji hello Azure HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="d5be0-105">Then use hello application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="d5be0-106">[Maven](http://maven.apache.org/) to oprogramowanie projektu zarządzania i zrozumienia narzędzie, które pozwala toobuild oprogramowania, dokumentacji i raporty dla projektów języka Java.</span><span class="sxs-lookup"><span data-stu-id="d5be0-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="d5be0-107">W tym artykule dowiesz się, jak toouse on toocreate podstawowe aplikacji Java, która tworzy, wysyła zapytanie, które usuwa HBase tabeli w klastrze usługi HDInsight Azure.</span><span class="sxs-lookup"><span data-stu-id="d5be0-107">In this article, you learn how toouse it toocreate a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5be0-108">kroki Hello w tym dokumencie wymagają klastra usługi HDInsight z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="d5be0-108">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="d5be0-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d5be0-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d5be0-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="d5be0-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="d5be0-111">Wymagania</span><span class="sxs-lookup"><span data-stu-id="d5be0-111">Requirements</span></span>
* <span data-ttu-id="d5be0-112">[Platformy Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="d5be0-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="d5be0-113">Maven</span><span class="sxs-lookup"><span data-stu-id="d5be0-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="d5be0-114">Klaster usługi HDInsight opartej na systemie Windows z bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="d5be0-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="d5be0-115">kroki Hello w tym dokumencie zostały przetestowane w wersjach klastra usługi HDInsight 3.2 i 3.3.</span><span class="sxs-lookup"><span data-stu-id="d5be0-115">hello steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="d5be0-116">wartości domyślnych Hello w przykładach są dla klastra usługi HDInsight 3.3.</span><span class="sxs-lookup"><span data-stu-id="d5be0-116">hello default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="d5be0-117">Utwórz projekt hello</span><span class="sxs-lookup"><span data-stu-id="d5be0-117">Create hello project</span></span>
1. <span data-ttu-id="d5be0-118">W wierszu polecenia hello w środowisku projektowania Zmień katalogi toohello lokalizację toocreate hello projektu, na przykład `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="d5be0-118">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="d5be0-119">Użyj hello **mvn** polecenia, który jest instalowany z Maven, hello toogenerate tworzenia szkieletu do projektu hello.</span><span class="sxs-lookup"><span data-stu-id="d5be0-119">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="d5be0-120">To polecenie tworzy katalog w bieżącej lokalizacji hello o nazwie hello określony przez hello **artifactID** parametr (**hbaseapp** w tym przykładzie.) Ten katalog zawiera hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d5be0-120">This command creates a directory in hello current location, with hello name specified by hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="d5be0-121">**pom.XML**: hello projektu Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) zawiera informacje i konfiguracji projektu hello toobuild szczegóły używanego.</span><span class="sxs-lookup"><span data-stu-id="d5be0-121">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="d5be0-122">**SRC**: hello katalog, który zawiera hello **main\java\com\microsoft\examples** katalogu, w którym będzie Autor aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d5be0-122">**src**: hello directory that contains hello **main\java\com\microsoft\examples** directory, where you will author hello application.</span></span>
3. <span data-ttu-id="d5be0-123">Usuń hello **src\test\java\com\microsoft\examples\apptest.java** pliku, ponieważ nie jest on używany w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d5be0-123">Delete hello **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="d5be0-124">Aktualizacja hello modelu obiektowego projektu</span><span class="sxs-lookup"><span data-stu-id="d5be0-124">Update hello Project Object Model</span></span>
1. <span data-ttu-id="d5be0-125">Edytuj hello **pom.xml** plik i dodać hello następującego kodu wewnątrz hello `<dependencies>` sekcji:</span><span class="sxs-lookup"><span data-stu-id="d5be0-125">Edit hello **pom.xml** file and add hello following code inside hello `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="d5be0-126">W tej sekcji opisano Maven, który hello projektu wymaga **klienta hbase** wersji **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="d5be0-126">This section tells Maven that hello project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="d5be0-127">W czasie kompilacji tę zależność jest pobierana z hello domyślne Maven repozytorium.</span><span class="sxs-lookup"><span data-stu-id="d5be0-127">At compile time, this dependency is downloaded from hello default Maven repository.</span></span> <span data-ttu-id="d5be0-128">Można użyć hello [Maven centralnym repozytorium wyszukiwania](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn więcej informacji na temat tej zależności.</span><span class="sxs-lookup"><span data-stu-id="d5be0-128">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d5be0-129">Witaj, numer wersji musi odpowiadać wersji hello HBase, która jest dostarczana z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5be0-129">hello version number must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="d5be0-130">Użyj powitania po numer poprawną wersję hello toofind tabeli.</span><span class="sxs-lookup"><span data-stu-id="d5be0-130">Use hello following table toofind hello correct version number.</span></span>
   >
   >

   | <span data-ttu-id="d5be0-131">Wersja klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="d5be0-131">HDInsight cluster version</span></span> | <span data-ttu-id="d5be0-132">Toouse wersji bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="d5be0-132">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="d5be0-133">3.2</span><span class="sxs-lookup"><span data-stu-id="d5be0-133">3.2</span></span> |<span data-ttu-id="d5be0-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="d5be0-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="d5be0-135">3.3</span><span class="sxs-lookup"><span data-stu-id="d5be0-135">3.3</span></span> |<span data-ttu-id="d5be0-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="d5be0-136">1.1.2</span></span> |

    <span data-ttu-id="d5be0-137">Aby uzyskać więcej informacji o wersji usługi HDInsight i składników, zobacz [co to są hello różne składniki platformy Hadoop dostępne z usługą HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d5be0-137">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="d5be0-138">Jeśli korzystasz z klastra usługi HDInsight 3.3, należy dodać następujące toohello hello `<dependencies>` sekcji:</span><span class="sxs-lookup"><span data-stu-id="d5be0-138">If you are using an HDInsight 3.3 cluster, you must also add hello following toohello `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="d5be0-139">Ta zależność załaduje hello phoenix — podstawowe składniki, które są używane przez wersję bazy danych Hbase 1.1.x.</span><span class="sxs-lookup"><span data-stu-id="d5be0-139">This dependency will load hello phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="d5be0-140">Dodaj hello następującego kodu toohello **pom.xml** pliku.</span><span class="sxs-lookup"><span data-stu-id="d5be0-140">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="d5be0-141">W tej sekcji musi znajdować się wewnątrz hello `<project>...</project>` tagów w hello plików, na przykład między `</dependencies>` i `</project>`.</span><span class="sxs-lookup"><span data-stu-id="d5be0-141">This section must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="d5be0-142">Witaj `<resources>` sekcji konfiguruje zasobu (**conf\hbase-site.xml**) zawiera informacje o konfiguracji dla bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="d5be0-142">hello `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d5be0-143">Można również ustawić wartości konfiguracji za pomocą kodu.</span><span class="sxs-lookup"><span data-stu-id="d5be0-143">You can also set configuration values via code.</span></span> <span data-ttu-id="d5be0-144">Zobacz komentarze hello w hello **CreateTable** przykład znajdujący się na temat toodo to.</span><span class="sxs-lookup"><span data-stu-id="d5be0-144">See hello comments in hello **CreateTable** example that follows for how toodo this.</span></span>
   >
   >

    <span data-ttu-id="d5be0-145">To `<plugins>` sekcji konfiguruje hello [wtyczki kompilatora Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) i [Maven cień wtyczki](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="d5be0-145">This `<plugins>` section configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="d5be0-146">wtyczki kompilatora Hello jest używane toocompile hello topologii.</span><span class="sxs-lookup"><span data-stu-id="d5be0-146">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="d5be0-147">Wtyczka cień Hello jest duplikatów licencji tooprevent używane w pakiecie JAR hello jest konstruowany przez Maven.</span><span class="sxs-lookup"><span data-stu-id="d5be0-147">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="d5be0-148">Przyczyna Hello, używana jest czy plików licencji zduplikowane hello spowodować błąd w czasie wykonywania w klastrze usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d5be0-148">hello reason this is used is that hello duplicate license files cause an error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="d5be0-149">Przy użyciu maven cień wtyczki z hello `ApacheLicenseResourceTransformer` ten błąd uniemożliwia implementacji.</span><span class="sxs-lookup"><span data-stu-id="d5be0-149">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="d5be0-150">Witaj maven cień — dodatek również daje pełny jar (lub fat jar) zawierający wszystkie zależności hello wymagane przez aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="d5be0-150">hello maven-shade-plugin also produces an uber jar (or fat jar) that contains all hello dependencies required by hello application.</span></span>
4. <span data-ttu-id="d5be0-151">Zapisz hello **pom.xml** pliku.</span><span class="sxs-lookup"><span data-stu-id="d5be0-151">Save hello **pom.xml** file.</span></span>
5. <span data-ttu-id="d5be0-152">Utwórz nowy katalog o nazwie **conf** w hello **hbaseapp** katalogu.</span><span class="sxs-lookup"><span data-stu-id="d5be0-152">Create a new directory named **conf** in hello **hbaseapp** directory.</span></span> <span data-ttu-id="d5be0-153">W hello **conf** katalogu, Utwórz plik o nazwie **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="d5be0-153">In hello **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="d5be0-154">Użyj następujących hello jako hello zawartość pliku hello:</span><span class="sxs-lookup"><span data-stu-id="d5be0-154">Use hello following as hello contents of hello file:</span></span>

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

    <span data-ttu-id="d5be0-155">Ten plik będzie konfiguracji bazy danych HBase hello tooload używane dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5be0-155">This file will be used tooload hello HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d5be0-156">Jest to plik minimalnego hbase-site.xml, i zawiera hello systemu od zera minimalne ustawienia hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5be0-156">This is a minimal hbase-site.xml file, and it contains hello bare minimum settings for hello HDInsight cluster.</span></span>

6. <span data-ttu-id="d5be0-157">Zapisz hello **hbase-site.xml** pliku.</span><span class="sxs-lookup"><span data-stu-id="d5be0-157">Save hello **hbase-site.xml** file.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="d5be0-158">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="d5be0-158">Create hello application</span></span>
1. <span data-ttu-id="d5be0-159">Przejdź toohello **hbaseapp\src\main\java\com\microsoft\examples** katalogu i Zmień nazwę hello pliku app.java zbyt**CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="d5be0-159">Go toohello **hbaseapp\src\main\java\com\microsoft\examples** directory and rename hello app.java file too**CreateTable.java**.</span></span>
2. <span data-ttu-id="d5be0-160">Otwórz hello **CreateTable.java** plików i zastąpić istniejącą zawartość hello hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="d5be0-160">Open hello **CreateTable.java** file and replace hello existing contents with hello following code:</span></span>

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

    <span data-ttu-id="d5be0-161">Jest to hello **CreateTable** klasy, która zostanie utworzona tabela o nazwie **osób** i wypełnić ją w przypadku niektórych użytkowników wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="d5be0-161">This is hello **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="d5be0-162">Zapisz hello **CreateTable.java** pliku.</span><span class="sxs-lookup"><span data-stu-id="d5be0-162">Save hello **CreateTable.java** file.</span></span>
4. <span data-ttu-id="d5be0-163">W hello **hbaseapp\src\main\java\com\microsoft\examples** katalogu, Utwórz nowy plik o nazwie **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="d5be0-163">In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="d5be0-164">Użyj hello następującego kodu jako hello zawartość tego pliku:</span><span class="sxs-lookup"><span data-stu-id="d5be0-164">Use hello following code as hello contents of this file:</span></span>

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

    <span data-ttu-id="d5be0-165">Witaj **SearchByEmail** klasa może być używana tooquery wierszy za pomocą adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="d5be0-165">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="d5be0-166">Ponieważ używa filtra wyrażenia regularnego, musisz podać ciąg lub wyrażenie regularne używając hello klasy.</span><span class="sxs-lookup"><span data-stu-id="d5be0-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>
5. <span data-ttu-id="d5be0-167">Zapisz hello **SearchByEmail.java** pliku.</span><span class="sxs-lookup"><span data-stu-id="d5be0-167">Save hello **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="d5be0-168">W hello **hbaseapp\src\main\hava\com\microsoft\examples** katalogu, Utwórz nowy plik o nazwie **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="d5be0-168">In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="d5be0-169">Użyj hello następującego kodu jako hello zawartość tego pliku:</span><span class="sxs-lookup"><span data-stu-id="d5be0-169">Use hello following code as hello contents of this file:</span></span>

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

    <span data-ttu-id="d5be0-170">Ta klasa jest oczyszczania w tym przykładzie, wyłączając i upuszczanie tabeli hello tworzone przez hello **CreateTable** klasy.</span><span class="sxs-lookup"><span data-stu-id="d5be0-170">This class is for cleaning up this example by disabling and dropping hello table created by hello **CreateTable** class.</span></span>
7. <span data-ttu-id="d5be0-171">Zapisz hello **DeleteTable.java** pliku.</span><span class="sxs-lookup"><span data-stu-id="d5be0-171">Save hello **DeleteTable.java** file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="d5be0-172">Aplikacja hello kompilacji i pakietu</span><span class="sxs-lookup"><span data-stu-id="d5be0-172">Build and package hello application</span></span>
1. <span data-ttu-id="d5be0-173">Otwórz wiersz polecenia i zmień katalogi toohello **hbaseapp** katalogu.</span><span class="sxs-lookup"><span data-stu-id="d5be0-173">Open a command prompt and change directories toohello **hbaseapp** directory.</span></span>
2. <span data-ttu-id="d5be0-174">Użyj następującego polecenia toobuild plik JAR zawierający aplikacji hello hello:</span><span class="sxs-lookup"><span data-stu-id="d5be0-174">Use hello following command toobuild a JAR file that contains hello application:</span></span>

        mvn clean package

    <span data-ttu-id="d5be0-175">To czyści wszystkie poprzednie artefaktów kompilacji, pobierze wszelkie zależności, które nie są jeszcze zainstalowane, następnie kompilacje i pakiety aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d5be0-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages hello application.</span></span>
3. <span data-ttu-id="d5be0-176">Po polecenie hello zakończeniu hello **hbaseapp\target** katalog zawiera plik o nazwie **hbaseapp-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="d5be0-176">When hello command completes, hello **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d5be0-177">Witaj **hbaseapp-1.0-SNAPSHOT.jar** plików jest pełny jar (nazywane również fat jar), który zawiera wszystkie zależności hello wymaganych aplikacji hello toorun.</span><span class="sxs-lookup"><span data-stu-id="d5be0-177">hello **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all hello dependencies required toorun hello application.</span></span>

## <a name="upload-hello-jar-file-and-start-a-job"></a><span data-ttu-id="d5be0-178">Przekaż plik JAR hello i uruchomić zadanie</span><span class="sxs-lookup"><span data-stu-id="d5be0-178">Upload hello JAR file and start a job</span></span>
<span data-ttu-id="d5be0-179">Istnieje wiele sposobów tooupload klastra usługi HDInsight tooyour pliku, zgodnie z opisem w [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="d5be0-179">There are many ways tooupload a file tooyour HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="d5be0-180">Witaj następujące kroki użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5be0-180">hello following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="d5be0-181">Po zainstalowaniu i skonfigurowaniu programu Azure PowerShell, Utwórz nowy plik o nazwie **hbase runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="d5be0-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="d5be0-182">Użyj następujących hello jako hello zawartość tego pliku:</span><span class="sxs-lookup"><span data-stu-id="d5be0-182">Use hello following as hello contents of this file:</span></span>

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

    <span data-ttu-id="d5be0-183">Ten plik zawiera dwa moduły:</span><span class="sxs-lookup"><span data-stu-id="d5be0-183">This file contains two modules:</span></span>

   * <span data-ttu-id="d5be0-184">**Dodaj HDInsightFile** — używane tooupload tooHDInsight plików</span><span class="sxs-lookup"><span data-stu-id="d5be0-184">**Add-HDInsightFile** - used tooupload files tooHDInsight</span></span>
   * <span data-ttu-id="d5be0-185">**Start-HBaseExample** -używane klasy hello toorun utworzony wcześniej</span><span class="sxs-lookup"><span data-stu-id="d5be0-185">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>
2. <span data-ttu-id="d5be0-186">Zapisz hello **hbase runner.psm1** pliku.</span><span class="sxs-lookup"><span data-stu-id="d5be0-186">Save hello **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="d5be0-187">Otwórz nowe okno programu Azure PowerShell, zmień katalogi toohello **hbaseapp** katalogu, a następnie hello uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="d5be0-187">Open a new Azure PowerShell window, change directories toohello **hbaseapp** directory, and then run hello following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="d5be0-188">Zmienić lokalizację toohello ścieżka hello hello **hbase runner.psm1** wcześniej utworzony plik.</span><span class="sxs-lookup"><span data-stu-id="d5be0-188">Change hello path toohello location of hello **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="d5be0-189">Rejestruje moduł hello tej sesji programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5be0-189">This registers hello module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="d5be0-190">Użyj hello następujące polecenie tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5be0-190">Use hello following command tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="d5be0-191">Zastąp **hdinsightclustername** o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5be0-191">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="d5be0-192">polecenie Hello przekazuje hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **przykład/słoików** lokalizacji w hello podstawowy magazyn dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5be0-192">hello command uploads hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **example/jars** location in hello primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="d5be0-193">Po przekazaniu plików hello Użyj hello poniższy kod toocreate tabeli za pomocą hello **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="d5be0-193">After hello files are uploaded, use hello following code toocreate a table using hello **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="d5be0-194">Zastąp **hdinsightclustername** o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5be0-194">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="d5be0-195">To polecenie tworzy nową tabelę o nazwie **osób** w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5be0-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="d5be0-196">To polecenie nie wyświetla żadnych danych wyjściowych w oknie konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="d5be0-196">This command does not show any output in hello console window.</span></span>
6. <span data-ttu-id="d5be0-197">toosearch wpisy tabeli hello hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d5be0-197">toosearch for entries in hello table, use hello following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="d5be0-198">Zastąp **hdinsightclustername** o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5be0-198">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="d5be0-199">To polecenie używa hello **SearchByEmail** klasy toosearch wierszy, gdzie hello **contactinformation** rodziny kolumn i hello **e-mail** kolumny zawiera ciąg hello **contoso.com**. Powinien zostać wyświetlony hello następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="d5be0-199">This command uses hello **SearchByEmail** class toosearch for any rows where hello **contactinformation** column family and hello **email** column, contains hello string **contoso.com**. You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="d5be0-200">Przy użyciu **fabrikam.com** dla hello `-emailRegex` wartość zwraca hello użytkowników, którzy mają **fabrikam.com** hello pola wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="d5be0-200">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="d5be0-201">Ponieważ to wyszukiwanie jest implementowane za pomocą regularnego oparte na wyrażeniach filtru, możesz też wprowadzić wyrażeń regularnych, takich jak **^ r**, które zwraca zapisy, gdzie hello e-mail zaczyna się od hello litery "r".</span><span class="sxs-lookup"><span data-stu-id="d5be0-201">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where hello email begins with hello letter 'r'.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="d5be0-202">Usuń tabelę hello</span><span class="sxs-lookup"><span data-stu-id="d5be0-202">Delete hello table</span></span>
<span data-ttu-id="d5be0-203">Po wykonaniu przykład Witaj, następujące hello Użyj polecenie z hello Azure PowerShell sesji toodelete hello **osób** Tabela używana w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d5be0-203">When you are done with hello example, use hello following command from hello Azure PowerShell session toodelete hello **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="d5be0-204">Zastąp **hdinsightclustername** o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5be0-204">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d5be0-205">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="d5be0-205">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="d5be0-206">Nie wyników lub nieoczekiwane wyniki, korzystając z Start HBaseExample</span><span class="sxs-lookup"><span data-stu-id="d5be0-206">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="d5be0-207">Użyj hello `-showErr` tooview hello standardowy błąd parametru (STDERR) utworzonym podczas wykonywanym zadaniem hello.</span><span class="sxs-lookup"><span data-stu-id="d5be0-207">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>
