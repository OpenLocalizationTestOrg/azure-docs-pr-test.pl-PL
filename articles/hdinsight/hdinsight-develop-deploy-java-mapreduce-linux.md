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
# <a name="develop-java-mapreduce-programs-for-hadoop-on-hdinsight"></a>Tworzenie programów Java MapReduce dla platformy Hadoop w usłudze HDInsight

Dowiedz się, jak toouse aplikacji MapReduce toocreate opartych na języku Java Apache Maven, następnie uruchom go z platformą Hadoop w usłudze Azure HDInsight.

> [!NOTE]
> W tym przykładzie ostatnio zbadano 3,6 HDInsight.

## <a name="prerequisites"></a>Wymagania wstępne

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 lub nowszy (lub odpowiednik, takie jak OpenJDK).
    
    > [!NOTE]
    > HDInsight w wersji 3.4 i wcześniejszych Użyj Java 7. HDInsight w wersji 3.5 lub nowszej używa języka Java 8.

* [Apache Maven](http://maven.apache.org/)

## <a name="configure-development-environment"></a>Konfigurowanie środowiska programowania

Witaj następujące zmienne środowiskowe mogą zostać ustawione podczas instalacji języka Java i hello JDK. Jednak należy sprawdzić, czy istnieją i że zawierają one hello poprawne wartości dla systemu.

* `JAVA_HOME`— powinna wskazywać katalog toohello zainstalowanym hello środowiska uruchomieniowego (JRE). Na przykład w systemie OS X, Unix lub Linux, powinien on wartość podobną zbyt`/usr/lib/jvm/java-7-oracle`. W systemie Windows czy ma on wartość podobną zbyt`c:\Program Files (x86)\Java\jre1.7`

* `PATH`— powinna zawierać hello następującej ścieżki:
  
  * `JAVA_HOME`(lub równoważne ścieżki hello)

  * `JAVA_HOME\bin`(lub równoważne ścieżki hello)

  * katalog Hello zainstalowanym Maven

## <a name="create-a-maven-project"></a>Utwórz projekt Maven

1. W sesji terminalowej lub wiersza polecenia w środowisku projektowania Zmień katalogi toohello lokalizację toostore tego projektu.

2. Użyj hello `mvn` polecenia, który jest instalowany z Maven, hello toogenerate tworzenia szkieletu do projektu hello.

   ```bash
   mvn archetype:generate -DgroupId=org.apache.hadoop.examples -DartifactId=wordcountjava -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```

    > [!NOTE]
    > Jeśli używasz programu PowerShell, należy ująć hello `-D` parametrów w podwójny cudzysłów.
    >
    > `mvn archetype:generate "-DgroupId=org.apache.hadoop.examples" "-DartifactId=wordcountjava" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    To polecenie tworzy katalog o nazwie hello określony przez hello `artifactID` parametr (**wordcountjava** w tym przykładzie.) Ten katalog zawiera hello następujące elementy:

   * `pom.xml`-hello [projektu Object Model (POM)](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html) zawierająca informacje i szczegóły konfiguracji używane toobuild hello projektu.

   * `src`-hello katalog, który zawiera hello aplikacji.

3. Usuń hello `src/test/java/org/apache/hadoop/examples/apptest.java` pliku. Nie jest on używany w tym przykładzie.

## <a name="add-dependencies"></a>Dodaj zależności

1. Edytuj hello `pom.xml` i dodaj następujące tekst wewnątrz hello hello `<dependencies>` sekcji:
   
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

    Definiuje wymaganych bibliotek (wymienione w &lt;artifactId\>) z określoną wersją (wymienione w &lt;wersji\>). W czasie kompilacji te zależności są pobierane z hello domyślne Maven repozytorium. Można użyć hello [Maven repozytorium wyszukiwania](http://search.maven.org/#artifactdetails%7Corg.apache.hadoop%7Chadoop-mapreduce-examples%7C2.5.1%7Cjar) tooview więcej.
   
    Witaj `<scope>provided</scope>` informuje Maven te zależności nie powinny być pakowane z aplikacji hello określone hello klastra usługi HDInsight w czasie wykonywania.

    > [!IMPORTANT]
    > używana wersja Hello powinna być zgodna wersja hello Hadoop istnieje w klastrze. Aby uzyskać więcej informacji o wersji, zobacz hello [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md) dokumentu.

2. Dodaj następujące toohello hello `pom.xml` pliku. Ten tekst musi znajdować się wewnątrz hello `<project>...</project>` tagów w pliku hello, na przykład między `</dependencies>` i `</project>`.

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

    Hello pierwszy wtyczki konfiguruje hello [Maven cień wtyczki](http://maven.apache.org/plugins/maven-shade-plugin/), która jest używana toobuild uberjar (nazywane również fatjar), która zawiera zależności wymagane przez aplikację hello. Uniemożliwia także dublowania licencji w pakiecie jar hello, co może spowodować problemy w niektórych systemach.

    druga wtyczka Hello konfiguruje hello docelową wersję języka Java.

    > [!NOTE]
    > HDInsight 3.4 i używanie wcześniejszych Java 7. HDInsight w wersji 3.5 lub nowszej używa języka Java 8.

3. Zapisz hello `pom.xml` pliku.

## <a name="create-hello-mapreduce-application"></a>Tworzenie aplikacji MapReduce hello

1. Przejdź toohello `wordcountjava/src/main/java/org/apache/hadoop/examples` hello katalogu i Zmień nazwę `App.java` pliku zbyt`WordCount.java`.

2. Otwórz hello `WordCount.java` plik w edytorze tekstów i Zastąp zawartość hello hello następującego tekstu:
   
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
   
    Nazwa pakietu hello powiadomienie jest `org.apache.hadoop.examples` i nazwa klasy hello jest `WordCount`. Za pomocą tych nazw można przesłać zadania MapReduce hello.

3. Zapisz plik hello.

## <a name="build-hello-application"></a>Tworzenie aplikacji hello

1. Zmień toohello `wordcountjava` katalogu, jeśli nie masz już istnieje.

2. Użyj następującego polecenia toobuild JAR pliku zawierającego aplikacji hello hello:

   ```
   mvn clean package
   ```

    To polecenie czyści wszystkie poprzednie artefaktów kompilacji, pobiera wszystkie zależności, które nie został jeszcze zainstalowany, a następnie kompilacje i pakietu aplikacji hello.

3. Po hello zakończeniu działania polecenia hello `wordcountjava/target` katalog zawiera plik o nazwie `wordcountjava-1.0-SNAPSHOT.jar`.
   
   > [!NOTE]
   > Witaj `wordcountjava-1.0-SNAPSHOT.jar` pliku jest uberjar, która zawiera nie tylko zadania WordCount hello, ale także zależności, które hello zadania wymaga w czasie wykonywania.

## <a id="upload"></a>Przekaż hello jar

Użyj następującego polecenia tooupload hello jar pliku toohello HDInsight headnode hello:

   ```bash
   scp target/wordcountjava-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
   ```

    Replace __USERNAME__ with your SSH user name for hello cluster. Replace __CLUSTERNAME__ with hello HDInsight cluster name.

To polecenie kopiuje pliki hello z węzłem głównym toohello hello systemu lokalnego. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="run"></a>Uruchomienie zadania MapReduce hello na platformie Hadoop

1. Połącz tooHDInsight przy użyciu protokołu SSH. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. W sesji SSH hello Użyj następującego polecenia toorun hello MapReduce aplikacji hello:
   
   ```bash
   yarn jar wordcountjava-1.0-SNAPSHOT.jar org.apache.hadoop.examples.WordCount /example/data/gutenberg/davinci.txt /example/data/wordcountout
   ```
   
    To polecenie uruchamia hello aplikacji WordCount MapReduce. Plik wejściowy Hello jest `/example/data/gutenberg/davinci.txt`, i katalog wyjściowy hello jest `/example/data/wordcountout`. Zarówno hello plik wejściowy i wyjściowy są przechowywane toohello domyślny magazyn dla klastra hello.

3. Po zakończeniu zadania hello, użyj hello następujące wyniki hello tooview poleceń:
   
   ```bash
   hdfs dfs -cat /example/data/wordcountout/*
   ```

    Listę słów i liczb, powinien zostać wyświetlony z wartości toohello podobne następującego tekstu:
   
        zeal    1
        zelus   1
        zenith  2

## <a id="nextsteps"></a>Następne kroki

W tym dokumencie wiesz już, jak toodevelop zadania Java MapReduce. Zobacz hello następujące dokumenty dla innych sposobów toowork z usługą HDInsight.

* [Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]
* [Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]
* [Korzystać z usługi MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)

Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/).

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

