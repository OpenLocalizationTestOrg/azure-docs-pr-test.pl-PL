---
title: "Utwórz Java MapReduce dla platformy Hadoop — usługa Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać Apache Maven do tworzenia aplikacji opartych na języku Java MapReduce, a następnie uruchom go z platformą Hadoop w usłudze Azure HDInsight."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
ms.assetid: 9ee6384c-cb61-4087-8273-fb53fa27c1c3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 11d63f22204eb2acb530378f53ac72f16a35a4f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="95c6f-103">Tworzenie programów Java MapReduce dla platformy Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="95c6f-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="95c6f-104">Dowiedz się, jak używać Apache Maven do tworzenia aplikacji opartych na języku Java MapReduce, a następnie uruchom go z platformą Hadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="95c6f-104">Learn how to use Apache Maven to create a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="95c6f-105">W tym przykładzie ostatnio zbadano 3,6 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="95c6f-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="95c6f-106"><a name="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="95c6f-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="95c6f-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 lub nowszy (lub odpowiednik, takie jak OpenJDK).</span><span class="sxs-lookup"><span data-stu-id="95c6f-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="95c6f-108">HDInsight w wersji 3.4 i wcześniejszych Użyj Java 7.</span><span class="sxs-lookup"><span data-stu-id="95c6f-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="95c6f-109">HDInsight w wersji 3.5 lub nowszej używa języka Java 8.</span><span class="sxs-lookup"><span data-stu-id="95c6f-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="95c6f-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="95c6f-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="95c6f-111">Konfigurowanie środowiska programowania</span><span class="sxs-lookup"><span data-stu-id="95c6f-111">Configure development environment</span></span>

<span data-ttu-id="95c6f-112">Po zainstalowaniu Java i zestaw JDK, który można konfigurować następujące zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="95c6f-112">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="95c6f-113">Jednak należy sprawdzić, czy istnieją i że zawierają one poprawne wartości dla systemu.</span><span class="sxs-lookup"><span data-stu-id="95c6f-113">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="95c6f-114">`JAVA_HOME`-powinny wskazywać na katalog, w którym zainstalowano środowiska wykonawczego języka Java (JRE).</span><span class="sxs-lookup"><span data-stu-id="95c6f-114">`JAVA_HOME` - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="95c6f-115">Na przykład w systemie OS X, Unix lub Linux, powinien on wartość podobną do `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="95c6f-115">For example, on an OS X, Unix or Linux system, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="95c6f-116">W systemie Windows będzie mieć wartość podobną do`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="95c6f-116">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="95c6f-117">`PATH`— powinna zawierać następujących ścieżkach:</span><span class="sxs-lookup"><span data-stu-id="95c6f-117">`PATH` - should contain the following paths:</span></span>
  
  * <span data-ttu-id="95c6f-118">`JAVA_HOME`(lub równoważne ścieżki)</span><span class="sxs-lookup"><span data-stu-id="95c6f-118">`JAVA_HOME` (or the equivalent path)</span></span>

  * <span data-ttu-id="95c6f-119">`JAVA_HOME\bin`(lub równoważne ścieżki)</span><span class="sxs-lookup"><span data-stu-id="95c6f-119">`JAVA_HOME\bin` (or the equivalent path)</span></span>

  * <span data-ttu-id="95c6f-120">Katalogu, w którym zainstalowano Maven</span><span class="sxs-lookup"><span data-stu-id="95c6f-120">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="95c6f-121">Utwórz projekt Maven</span><span class="sxs-lookup"><span data-stu-id="95c6f-121">Create a Maven project</span></span>

1. <span data-ttu-id="95c6f-122">W sesji terminalowej lub wiersza polecenia w środowisku projektowania przejdź do lokalizacji przechowywania tego projektu.</span><span class="sxs-lookup"><span data-stu-id="95c6f-122">From a terminal session, or command line in your development environment, change directories to the location you want to store this project.</span></span>

2. <span data-ttu-id="95c6f-123">Użyj `mvn` polecenia, które jest instalowany z Maven, aby wygenerować funkcją szkieletów dla projektu.</span><span class="sxs-lookup"><span data-stu-id="95c6f-123">Use the `mvn` command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="95c6f-124">Jeśli używasz programu PowerShell, należy ująć `-D` parametrów w podwójny cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="95c6f-124">If you are using PowerShell, you must enclose the `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="95c6f-125">To polecenie tworzy katalog o nazwie określonej przez `artifactID` parametr (**wordcountjava** w tym przykładzie.) Ten katalog zawiera następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="95c6f-125">This command creates a directory with the name specified by the `artifactID` parameter (**wordcountjava** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="95c6f-126">`pom.xml`- [Projektu Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) zawiera informacje i szczegóły konfiguracji używany do tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="95c6f-126">`pom.xml` - The [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used to build the project.</span></span>

   * <span data-ttu-id="95c6f-127">`src`-Katalog zawierający aplikację.</span><span class="sxs-lookup"><span data-stu-id="95c6f-127">`src` - The directory that contains the application.</span></span>

3. <span data-ttu-id="95c6f-128">Usuń `src/test/java/org/apache/hadoop/examples/apptest.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="95c6f-128">Delete the `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="95c6f-129">Nie jest on używany w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="95c6f-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="95c6f-130">Dodaj zależności</span><span class="sxs-lookup"><span data-stu-id="95c6f-130">Add dependencies</span></span>

1. <span data-ttu-id="95c6f-131">Edytuj `pom.xml` i Dodaj następujący tekst wewnątrz `<dependencies>` sekcji:</span><span class="sxs-lookup"><span data-stu-id="95c6f-131">Edit the `pom.xml` file and add the following text inside the `<dependencies>` section:</span></span>
   
   ```xml
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-examples</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-mapreduce-client-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.hadoop</groupId>
        <artifactId>hadoop-common</artifactId>
        <version>2.7.3</version>
        <scope>provided</scope>
    </dependency>
   ```

    <span data-ttu-id="95c6f-132">Definiuje wymaganych bibliotek (wymienione w &lt;artifactId\>) z określoną wersją (wymienione w &lt;wersji\>).</span><span class="sxs-lookup"><span data-stu-id="95c6f-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="95c6f-133">W czasie kompilacji te zależności są pobierane z repozytorium Maven domyślne.</span><span class="sxs-lookup"><span data-stu-id="95c6f-133">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="95c6f-134">Można użyć [Maven repozytorium wyszukiwania](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) Aby wyświetlić więcej.</span><span class="sxs-lookup"><span data-stu-id="95c6f-134">You can use the [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) to view more.</span></span>
   
    <span data-ttu-id="95c6f-135">`<scope>provided</scope>` Informuje Maven te zależności nie powinny być pakowane z aplikacją, jak są one udostępniane przez klaster usługi HDInsight w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="95c6f-135">The `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with the application, as they are provided by the HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="95c6f-136">Wersja użyta powinna być zgodna wersja platformy Hadoop w klastrze.</span><span class="sxs-lookup"><span data-stu-id="95c6f-136">The version used should match the version of Hadoop present on your cluster.</span></span> <span data-ttu-id="95c6f-137">Aby uzyskać więcej informacji o wersji, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="95c6f-137">For more information on versions, see the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="95c6f-138">Dodaj następujący kod do `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="95c6f-138">Add the following to the `pom.xml` file.</span></span> <span data-ttu-id="95c6f-139">Ten tekst musi znajdować się wewnątrz `<project>...</project>` tagów w pliku, na przykład między `</dependencies>` i `</project>`.</span><span class="sxs-lookup"><span data-stu-id="95c6f-139">This text must be inside the `<project>...</project>` tags in the file; for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <plugins>
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
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
            <source>1.8</source>
            <target>1.8</target>
            </configuration>
        </plugin>
        </plugins>
    </build>
   ```

    <span data-ttu-id="95c6f-140">Konfiguruje pierwszy wtyczki [Maven cień wtyczki](http://maven.apache.org/plugins/maven-shade-plugin/), który jest używany do tworzenia uberjar (nazywane również fatjar), która zawiera zależności wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="95c6f-140">The first plugin configures the [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used to build an uberjar (sometimes called a fatjar), which contains dependencies required by the application.</span></span> <span data-ttu-id="95c6f-141">Uniemożliwia także dublowania licencji w pakiecie jar, co może spowodować problemy w niektórych systemach.</span><span class="sxs-lookup"><span data-stu-id="95c6f-141">It also prevents duplication of licenses within the jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="95c6f-142">Druga wtyczka konfiguruje docelową wersję języka Java.</span><span class="sxs-lookup"><span data-stu-id="95c6f-142">The second plugin configures the target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="95c6f-143">HDInsight 3.4 i używanie wcześniejszych Java 7.</span><span class="sxs-lookup"><span data-stu-id="95c6f-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="95c6f-144">HDInsight w wersji 3.5 lub nowszej używa języka Java 8.</span><span class="sxs-lookup"><span data-stu-id="95c6f-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="95c6f-145">Zapisz `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="95c6f-145">Save the `pom.xml` file.</span></span>

## <a name="create-the-mapreduce-application"></a><span data-ttu-id="95c6f-146">Tworzenie aplikacji MapReduce</span><span class="sxs-lookup"><span data-stu-id="95c6f-146">Create the MapReduce application</span></span>

1. <span data-ttu-id="95c6f-147">Przejdź do `wordcountjava/src/main/java/org/apache/hadoop/examples` katalogu i Zmień nazwę `App.java` pliku `WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="95c6f-147">Go to the `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename the `App.java` file to `WordCount.java`.</span></span>

2. <span data-ttu-id="95c6f-148">Otwórz `WordCount.java` plik w edytorze tekstów i Zastąp zawartość następującym tekstem:</span><span class="sxs-lookup"><span data-stu-id="95c6f-148">Open the `WordCount.java` file in a text editor and replace the contents with the following text:</span></span>
   
    ```java
    package org.apache.hadoop.examples;

    import java.io.IOException;
    import java.util.StringTokenizer;
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.fs.Path;
    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Job;
    import org.apache.hadoop.mapreduce.Mapper;
    import org.apache.hadoop.mapreduce.Reducer;
    import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
    import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class WordCount {

        public static class TokenizerMapper
            extends Mapper<Object, Text, Text, IntWritable>{

        private final static IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Context context
                        ) throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
            word.set(itr.nextToken());
            context.write(word, one);
            }
        }
    }

    public static class IntSumReducer
            extends Reducer<Text,IntWritable,Text,IntWritable> {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values,
                            Context context
                            ) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable val : values) {
            sum += val.get();
            }
            result.set(sum);
            context.write(key, result);
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
        if (otherArgs.length != 2) {
            System.err.println("Usage: wordcount <in> <out>");
            System.exit(2);
        }
        Job job = new Job(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
        FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
        System.exit(job.waitForCompletion(true) ? 0 : 1);
        }
    }
    ```
   
    <span data-ttu-id="95c6f-149">Zwróć uwagę, nazwa pakietu jest `org.apache.hadoop.examples` i nazwa klasy jest `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="95c6f-149">Notice the package name is `org.apache.hadoop.examples` and the class name is `WordCount`.</span></span> <span data-ttu-id="95c6f-150">Za pomocą tych nazw można przesłać zadania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="95c6f-150">You use these names when you submit the MapReduce job.</span></span>

3. <span data-ttu-id="95c6f-151">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="95c6f-151">Save the file.</span></span>

## <a name="build-the-application"></a><span data-ttu-id="95c6f-152">Kompilowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="95c6f-152">Build the application</span></span>

1. <span data-ttu-id="95c6f-153">Zmień na `wordcountjava` katalogu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="95c6f-153">Change to the `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="95c6f-154">Aby utworzyć plik JAR zawierający aplikację, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="95c6f-154">Use the following command to build a JAR file containing the application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="95c6f-155">To polecenie czyści wszystkie poprzednie artefaktów kompilacji, pobierze wszelkie zależności, które nie został jeszcze zainstalowany, a następnie kompilacji i pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="95c6f-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package the application.</span></span>

3. <span data-ttu-id="95c6f-156">Po zakończeniu działania polecenia `wordcountjava/target` katalog zawiera plik o nazwie `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="95c6f-156">Once the command finishes, the `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="95c6f-157">`wordcountjava-1.0-SNAPSHOT.jar` Plik jest uberjar, która zawiera nie tylko zadania WordCount, ale także zależności, które wymaga zadanie w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="95c6f-157">The `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only the WordCount job, but also dependencies that the job requires at runtime.</span></span>

## <span data-ttu-id="95c6f-158"><a id="upload"></a>Przekaż jar</span><span class="sxs-lookup"><span data-stu-id="95c6f-158"><a id="upload"></a>Upload the jar</span></span>

<span data-ttu-id="95c6f-159">Użyj następującego polecenia, aby przekazać plik jar do HDInsight headnode:</span><span class="sxs-lookup"><span data-stu-id="95c6f-159">Use the following command to upload the jar file to the HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for the cluster. Replace __CLUSTERNAME__ with the HDInsight cluster name.

<span data-ttu-id="95c6f-160">To polecenie kopiuje pliki z systemu lokalnego do węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="95c6f-160">This command copies the files from the local system to the head node.</span></span> <span data-ttu-id="95c6f-161">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="95c6f-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="95c6f-162"><a name="run"></a>Uruchom zadanie MapReduce na platformie Hadoop</span><span class="sxs-lookup"><span data-stu-id="95c6f-162"><a name="run"></a>Run the MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="95c6f-163">Połączenie do usługi HDInsight przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="95c6f-163">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="95c6f-164">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="95c6f-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="95c6f-165">W sesji SSH wpisz następujące polecenie do uruchomienia aplikacji MapReduce:</span><span class="sxs-lookup"><span data-stu-id="95c6f-165">From the SSH session, use the following command to run the MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="95c6f-166">To polecenie uruchamia aplikację WordCount MapReduce.</span><span class="sxs-lookup"><span data-stu-id="95c6f-166">This command starts the WordCount MapReduce application.</span></span> <span data-ttu-id="95c6f-167">Plik wejściowy jest `/example/data/gutenberg/davinci.txt`, i katalog wyjściowy jest `/example/data/wordcountout`.</span><span class="sxs-lookup"><span data-stu-id="95c6f-167">The input file is `/example/data/gutenberg/davinci.txt`, and the output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="95c6f-168">Plik wejściowy i wyjściowy są przechowywane do magazynu domyślnego dla klastra.</span><span class="sxs-lookup"><span data-stu-id="95c6f-168">Both the input file and output are stored to the default storage for the cluster.</span></span>

3. <span data-ttu-id="95c6f-169">Po zakończeniu zadania, użyj następującego polecenia, aby wyświetlić wyniki:</span><span class="sxs-lookup"><span data-stu-id="95c6f-169">Once the job completes, use the following command to view the results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="95c6f-170">Powinien zostać wyświetlony listę słów i liczb, wartości podobnie do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="95c6f-170">You should receive a list of words and counts, with values similar to the following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="95c6f-171"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95c6f-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="95c6f-172">W tym dokumencie mają przedstawiono sposób rozwijać zadania Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="95c6f-172">In this document, you have learned how to develop a Java MapReduce job.</span></span> <span data-ttu-id="95c6f-173">Można znaleźć w następujących dokumentach inne sposoby pracy z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="95c6f-173">See the following documents for other ways to work with HDInsight.</span></span>

* <span data-ttu-id="95c6f-174">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="95c6f-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="95c6f-175">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="95c6f-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="95c6f-176">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="95c6f-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="95c6f-177">Aby uzyskać więcej informacji, zobacz też [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="95c6f-177">For more information, see also the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md

[powershell-PSCredential]: http://social.technet.microsoft.com/wiki/contents/articles/4546.working-with-passwords-secure-strings-and-credentials-in-windows-powershell.aspx

