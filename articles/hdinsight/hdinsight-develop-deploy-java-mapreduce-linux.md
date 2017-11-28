---
title: aaaCreate MapReduce Java dla platformy Hadoop - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse aplikacji MapReduce toocreate opartych na języku Java Apache Maven, następnie uruchom go z platformą Hadoop w usłudze Azure HDInsight."
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
ms.openlocfilehash: 903a57a482395f7da79002188399a4d6288ff0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a><span data-ttu-id="961d3-103">Tworzenie programów Java MapReduce dla platformy Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="961d3-103">Develop Java MapReduce programs for Hadoop on HDInsight</span></span>

<span data-ttu-id="961d3-104">Dowiedz się, jak toouse aplikacji MapReduce toocreate opartych na języku Java Apache Maven, następnie uruchom go z platformą Hadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="961d3-104">Learn how toouse Apache Maven toocreate a Java-based MapReduce application, then run it with Hadoop on Azure HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="961d3-105">W tym przykładzie ostatnio zbadano 3,6 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="961d3-105">This example was most recently tested on HDInsight 3.6.</span></span>

## <span data-ttu-id="961d3-106"><a name="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="961d3-106"><a name="prerequisites"></a>Prerequisites</span></span>

* <span data-ttu-id="961d3-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 lub nowszy (lub odpowiednik, takie jak OpenJDK).</span><span class="sxs-lookup"><span data-stu-id="961d3-107">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="961d3-108">HDInsight w wersji 3.4 i wcześniejszych Użyj Java 7.</span><span class="sxs-lookup"><span data-stu-id="961d3-108">HDInsight versions 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="961d3-109">HDInsight w wersji 3.5 lub nowszej używa języka Java 8.</span><span class="sxs-lookup"><span data-stu-id="961d3-109">HDInsight 3.5 and greater uses Java 8.</span></span>

* [<span data-ttu-id="961d3-110">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="961d3-110">Apache Maven</span></span>](http://maven.apache.org/)

## <a name="configure-development-environment"></a><span data-ttu-id="961d3-111">Konfigurowanie środowiska programowania</span><span class="sxs-lookup"><span data-stu-id="961d3-111">Configure development environment</span></span>

<span data-ttu-id="961d3-112">Witaj następujące zmienne środowiskowe mogą zostać ustawione podczas instalacji języka Java i hello JDK.</span><span class="sxs-lookup"><span data-stu-id="961d3-112">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="961d3-113">Jednak należy sprawdzić, czy istnieją i że zawierają one hello poprawne wartości dla systemu.</span><span class="sxs-lookup"><span data-stu-id="961d3-113">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="961d3-114">`JAVA_HOME`— powinna wskazywać katalog toohello zainstalowanym hello środowiska uruchomieniowego (JRE).</span><span class="sxs-lookup"><span data-stu-id="961d3-114">`JAVA_HOME` - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="961d3-115">Na przykład w systemie OS X, Unix lub Linux, powinien on wartość podobną zbyt`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="961d3-115">For example, on an OS X, Unix or Linux system, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="961d3-116">W systemie Windows czy ma on wartość podobną zbyt`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="961d3-116">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="961d3-117">`PATH`— powinna zawierać hello następującej ścieżki:</span><span class="sxs-lookup"><span data-stu-id="961d3-117">`PATH` - should contain hello following paths:</span></span>
  
  * <span data-ttu-id="961d3-118">`JAVA_HOME`(lub równoważne ścieżki hello)</span><span class="sxs-lookup"><span data-stu-id="961d3-118">`JAVA_HOME` (or hello equivalent path)</span></span>

  * <span data-ttu-id="961d3-119">`JAVA_HOME\bin`(lub równoważne ścieżki hello)</span><span class="sxs-lookup"><span data-stu-id="961d3-119">`JAVA_HOME\bin` (or hello equivalent path)</span></span>

  * <span data-ttu-id="961d3-120">katalog Hello zainstalowanym Maven</span><span class="sxs-lookup"><span data-stu-id="961d3-120">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="961d3-121">Utwórz projekt Maven</span><span class="sxs-lookup"><span data-stu-id="961d3-121">Create a Maven project</span></span>

1. <span data-ttu-id="961d3-122">W sesji terminalowej lub wiersza polecenia w środowisku projektowania Zmień katalogi toohello lokalizację toostore tego projektu.</span><span class="sxs-lookup"><span data-stu-id="961d3-122">From a terminal session, or command line in your development environment, change directories toohello location you want toostore this project.</span></span>

2. <span data-ttu-id="961d3-123">Użyj hello `mvn` polecenia, który jest instalowany z Maven, hello toogenerate tworzenia szkieletu do projektu hello.</span><span class="sxs-lookup"><span data-stu-id="961d3-123">Use hello `mvn` command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > <span data-ttu-id="961d3-124">Jeśli używasz programu PowerShell, należy ująć hello `-D` parametrów w podwójny cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="961d3-124">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="961d3-125">To polecenie tworzy katalog o nazwie hello określony przez hello `artifactID` parametr (**wordcountjava** w tym przykładzie.) Ten katalog zawiera hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="961d3-125">This command creates a directory with hello name specified by hello `artifactID` parameter (**wordcountjava** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="961d3-126">`pom.xml`-hello [projektu Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) zawierająca informacje i szczegóły konfiguracji używane toobuild hello projektu.</span><span class="sxs-lookup"><span data-stu-id="961d3-126">`pom.xml` - hello [Project Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) that contains information and configuration details used toobuild hello project.</span></span>

   * <span data-ttu-id="961d3-127">`src`-hello katalog, który zawiera hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="961d3-127">`src` - hello directory that contains hello application.</span></span>

3. <span data-ttu-id="961d3-128">Usuń hello `src/test/java/org/apache/hadoop/examples/apptest.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="961d3-128">Delete hello `src/test/java/org/apache/hadoop/examples/apptest.java` file.</span></span> <span data-ttu-id="961d3-129">Nie jest on używany w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="961d3-129">It is not used in this example.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="961d3-130">Dodaj zależności</span><span class="sxs-lookup"><span data-stu-id="961d3-130">Add dependencies</span></span>

1. <span data-ttu-id="961d3-131">Edytuj hello `pom.xml` i dodaj następujące tekst wewnątrz hello hello `<dependencies>` sekcji:</span><span class="sxs-lookup"><span data-stu-id="961d3-131">Edit hello `pom.xml` file and add hello following text inside hello `<dependencies>` section:</span></span>
   
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

    <span data-ttu-id="961d3-132">Definiuje wymaganych bibliotek (wymienione w &lt;artifactId\>) z określoną wersją (wymienione w &lt;wersji\>).</span><span class="sxs-lookup"><span data-stu-id="961d3-132">This defines required libraries (listed within &lt;artifactId\>) with a specific version (listed within &lt;version\>).</span></span> <span data-ttu-id="961d3-133">W czasie kompilacji te zależności są pobierane z hello domyślne Maven repozytorium.</span><span class="sxs-lookup"><span data-stu-id="961d3-133">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="961d3-134">Można użyć hello [Maven repozytorium wyszukiwania](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview więcej.</span><span class="sxs-lookup"><span data-stu-id="961d3-134">You can use hello [Maven repository search](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview more.</span></span>
   
    <span data-ttu-id="961d3-135">Witaj `<scope>provided</scope>` informuje Maven te zależności nie powinny być pakowane z aplikacji hello określone hello klastra usługi HDInsight w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="961d3-135">hello `<scope>provided</scope>` tells Maven that these dependencies should not be packaged with hello application, as they are provided by hello HDInsight cluster at run-time.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="961d3-136">używana wersja Hello powinna być zgodna wersja hello Hadoop istnieje w klastrze.</span><span class="sxs-lookup"><span data-stu-id="961d3-136">hello version used should match hello version of Hadoop present on your cluster.</span></span> <span data-ttu-id="961d3-137">Aby uzyskać więcej informacji o wersji, zobacz hello [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="961d3-137">For more information on versions, see hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

2. <span data-ttu-id="961d3-138">Dodaj następujące toohello hello `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="961d3-138">Add hello following toohello `pom.xml` file.</span></span> <span data-ttu-id="961d3-139">Ten tekst musi znajdować się wewnątrz hello `<project>...</project>` tagów w pliku hello, na przykład między `</dependencies>` i `</project>`.</span><span class="sxs-lookup"><span data-stu-id="961d3-139">This text must be inside hello `<project>...</project>` tags in hello file; for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="961d3-140">Hello pierwszy wtyczki konfiguruje hello [Maven cień wtyczki](http://maven.apache.org/plugins/maven-shade-plugin/), która jest używana toobuild uberjar (nazywane również fatjar), która zawiera zależności wymagane przez aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="961d3-140">hello first plugin configures hello [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/), which is used toobuild an uberjar (sometimes called a fatjar), which contains dependencies required by hello application.</span></span> <span data-ttu-id="961d3-141">Uniemożliwia także dublowania licencji w pakiecie jar hello, co może spowodować problemy w niektórych systemach.</span><span class="sxs-lookup"><span data-stu-id="961d3-141">It also prevents duplication of licenses within hello jar package, which can cause problems on some systems.</span></span>

    <span data-ttu-id="961d3-142">druga wtyczka Hello konfiguruje hello docelową wersję języka Java.</span><span class="sxs-lookup"><span data-stu-id="961d3-142">hello second plugin configures hello target Java version.</span></span>

    > [!NOTE]
    > <span data-ttu-id="961d3-143">HDInsight 3.4 i używanie wcześniejszych Java 7.</span><span class="sxs-lookup"><span data-stu-id="961d3-143">HDInsight 3.4 and earlier use Java 7.</span></span> <span data-ttu-id="961d3-144">HDInsight w wersji 3.5 lub nowszej używa języka Java 8.</span><span class="sxs-lookup"><span data-stu-id="961d3-144">HDInsight 3.5 and greater uses Java 8.</span></span>

3. <span data-ttu-id="961d3-145">Zapisz hello `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="961d3-145">Save hello `pom.xml` file.</span></span>

## <a name="create-hello-mapreduce-application"></a><span data-ttu-id="961d3-146">Tworzenie aplikacji MapReduce hello</span><span class="sxs-lookup"><span data-stu-id="961d3-146">Create hello MapReduce application</span></span>

1. <span data-ttu-id="961d3-147">Przejdź toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` hello katalogu i Zmień nazwę `App.java` pliku zbyt`WordCount.java`.</span><span class="sxs-lookup"><span data-stu-id="961d3-147">Go toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` directory and rename hello `App.java` file too`WordCount.java`.</span></span>

2. <span data-ttu-id="961d3-148">Otwórz hello `WordCount.java` plik w edytorze tekstów i Zastąp zawartość hello hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="961d3-148">Open hello `WordCount.java` file in a text editor and replace hello contents with hello following text:</span></span>
   
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
   
    <span data-ttu-id="961d3-149">Nazwa pakietu hello powiadomienie jest `org.apache.hadoop.examples` i nazwa klasy hello jest `WordCount`.</span><span class="sxs-lookup"><span data-stu-id="961d3-149">Notice hello package name is `org.apache.hadoop.examples` and hello class name is `WordCount`.</span></span> <span data-ttu-id="961d3-150">Za pomocą tych nazw można przesłać zadania MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="961d3-150">You use these names when you submit hello MapReduce job.</span></span>

3. <span data-ttu-id="961d3-151">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="961d3-151">Save hello file.</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="961d3-152">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="961d3-152">Build hello application</span></span>

1. <span data-ttu-id="961d3-153">Zmień toohello `wordcountjava` katalogu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="961d3-153">Change toohello `wordcountjava` directory, if you are not already there.</span></span>

2. <span data-ttu-id="961d3-154">Użyj następującego polecenia toobuild JAR pliku zawierającego aplikacji hello hello:</span><span class="sxs-lookup"><span data-stu-id="961d3-154">Use hello following command toobuild a JAR file containing hello application:</span></span>

   ```
   mvn clean package
   ```

    <span data-ttu-id="961d3-155">To polecenie czyści wszystkie poprzednie artefaktów kompilacji, pobiera wszystkie zależności, które nie został jeszcze zainstalowany, a następnie kompilacje i pakietu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="961d3-155">This command cleans any previous build artifacts, downloads any dependencies that have not already been installed, and then builds and package hello application.</span></span>

3. <span data-ttu-id="961d3-156">Po hello zakończeniu działania polecenia hello `wordcountjava/target` katalog zawiera plik o nazwie `wordcountjava-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="961d3-156">Once hello command finishes, hello `wordcountjava/target` directory contains a file named `wordcountjava-1.0-SNAPSHOT.jar`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="961d3-157">Witaj `wordcountjava-1.0-SNAPSHOT.jar` pliku jest uberjar, która zawiera nie tylko zadania WordCount hello, ale także zależności, które hello zadania wymaga w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="961d3-157">hello `wordcountjava-1.0-SNAPSHOT.jar` file is an uberjar, which contains not only hello WordCount job, but also dependencies that hello job requires at runtime.</span></span>

## <span data-ttu-id="961d3-158"><a id="upload"></a>Przekaż hello jar</span><span class="sxs-lookup"><span data-stu-id="961d3-158"><a id="upload"></a>Upload hello jar</span></span>

<span data-ttu-id="961d3-159">Użyj następującego polecenia tooupload hello jar pliku toohello HDInsight headnode hello:</span><span class="sxs-lookup"><span data-stu-id="961d3-159">Use hello following command tooupload hello jar file toohello HDInsight headnode:</span></span>

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

<span data-ttu-id="961d3-160">To polecenie kopiuje pliki hello z węzłem głównym toohello hello systemu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="961d3-160">This command copies hello files from hello local system toohello head node.</span></span> <span data-ttu-id="961d3-161">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="961d3-161">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="961d3-162"><a name="run"></a>Uruchomienie zadania MapReduce hello na platformie Hadoop</span><span class="sxs-lookup"><span data-stu-id="961d3-162"><a name="run"></a>Run hello MapReduce job on Hadoop</span></span>

1. <span data-ttu-id="961d3-163">Połącz tooHDInsight przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="961d3-163">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="961d3-164">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="961d3-164">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="961d3-165">W sesji SSH hello Użyj następującego polecenia toorun hello MapReduce aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="961d3-165">From hello SSH session, use hello following command toorun hello MapReduce application:</span></span>
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    <span data-ttu-id="961d3-166">To polecenie uruchamia hello aplikacji WordCount MapReduce.</span><span class="sxs-lookup"><span data-stu-id="961d3-166">This command starts hello WordCount MapReduce application.</span></span> <span data-ttu-id="961d3-167">Plik wejściowy Hello jest `/example/data/gutenberg/davinci.txt`, i katalog wyjściowy hello jest `/example/data/wordcountout`.</span><span class="sxs-lookup"><span data-stu-id="961d3-167">hello input file is `/example/data/gutenberg/davinci.txt`, and hello output directory is `/example/data/wordcountout`.</span></span> <span data-ttu-id="961d3-168">Zarówno hello plik wejściowy i wyjściowy są przechowywane toohello domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="961d3-168">Both hello input file and output are stored toohello default storage for hello cluster.</span></span>

3. <span data-ttu-id="961d3-169">Po zakończeniu zadania hello, użyj hello następujące wyniki hello tooview poleceń:</span><span class="sxs-lookup"><span data-stu-id="961d3-169">Once hello job completes, use hello following command tooview hello results:</span></span>
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    <span data-ttu-id="961d3-170">Listę słów i liczb, powinien zostać wyświetlony z wartości toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="961d3-170">You should receive a list of words and counts, with values similar toohello following text:</span></span>
   
        zeal    1
        zelus   1
        zenith  2

## <span data-ttu-id="961d3-171"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="961d3-171"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="961d3-172">W tym dokumencie wiesz już, jak toodevelop zadania Java MapReduce.</span><span class="sxs-lookup"><span data-stu-id="961d3-172">In this document, you have learned how toodevelop a Java MapReduce job.</span></span> <span data-ttu-id="961d3-173">Zobacz hello następujące dokumenty dla innych sposobów toowork z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="961d3-173">See hello following documents for other ways toowork with HDInsight.</span></span>

* <span data-ttu-id="961d3-174">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="961d3-174">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="961d3-175">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="961d3-175">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* [<span data-ttu-id="961d3-176">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="961d3-176">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="961d3-177">Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="961d3-177">For more information, see also hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

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

