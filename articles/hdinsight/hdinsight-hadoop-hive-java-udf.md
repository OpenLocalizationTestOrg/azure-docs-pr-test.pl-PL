---
title: "aaaJava — funkcja zdefiniowana przez użytkownika (UDF) przy użyciu Hive w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate opartych na języku Java zdefiniowane przez użytkownika (UDF) funkcja, która współdziała z gałęzi. W tym przykładzie UDF Konwertuje tabelę toolowercase ciągów tekstowych."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="231d9-104">Użyj Java funkcji zdefiniowanej przez użytkownika przy użyciu Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="231d9-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="231d9-105">Dowiedz się, jak toocreate opartych na języku Java zdefiniowane przez użytkownika (UDF) funkcja, która współdziała z gałęzi.</span><span class="sxs-lookup"><span data-stu-id="231d9-105">Learn how toocreate a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="231d9-106">Witaj UDF języka Java w tym przykładzie Konwertuje tabelę małe tooall ciągów znaków.</span><span class="sxs-lookup"><span data-stu-id="231d9-106">hello Java UDF in this example converts a table of text strings tooall-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="231d9-107">Wymagania</span><span class="sxs-lookup"><span data-stu-id="231d9-107">Requirements</span></span>

* <span data-ttu-id="231d9-108">Klaster usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="231d9-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="231d9-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="231d9-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="231d9-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="231d9-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="231d9-111">Większość kroków w tym dokumencie działają w obu klastrach z systemem Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="231d9-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="231d9-112">Jednak hello krokami tooupload hello skompilować UDF toohello klastra i uruchom go są określone na podstawie tooLinux klastry.</span><span class="sxs-lookup"><span data-stu-id="231d9-112">However, hello steps used tooupload hello compiled UDF toohello cluster and run it are specific tooLinux-based clusters.</span></span> <span data-ttu-id="231d9-113">Łącza podano tooinformation, który może być używany z klastrów z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="231d9-113">Links are provided tooinformation that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="231d9-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 lub nowszy (lub odpowiednik, takie jak OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="231d9-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="231d9-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="231d9-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="231d9-116">Edytora tekstu lub IDE języka Java</span><span class="sxs-lookup"><span data-stu-id="231d9-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="231d9-117">Jeśli tworzysz hello pliki języka Python w kliencie systemu Windows, musisz użyć edytora, używającą LF jako zakończenia linii.</span><span class="sxs-lookup"><span data-stu-id="231d9-117">If you create hello Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="231d9-118">Jeśli nie masz pewności, czy edytor używa LF lub CRLF, zobacz hello [Rozwiązywanie problemów](#troubleshooting) sekcji dla kroki dotyczące usuwania hello CR znaków.</span><span class="sxs-lookup"><span data-stu-id="231d9-118">If you are not sure whether your editor uses LF or CRLF, see hello [Troubleshooting](#troubleshooting) section for steps on removing hello CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="231d9-119">Utwórz przykład UDF języka Java</span><span class="sxs-lookup"><span data-stu-id="231d9-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="231d9-120">Z wiersza polecenia użyj następującego toocreate nowy projekt Maven hello:</span><span class="sxs-lookup"><span data-stu-id="231d9-120">From a command line, use hello following toocreate a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="231d9-121">Jeśli używasz programu PowerShell, możesz umieścić stawiać cudzysłów wokół hello parametrów.</span><span class="sxs-lookup"><span data-stu-id="231d9-121">If you are using PowerShell, you must put quotes around hello parameters.</span></span> <span data-ttu-id="231d9-122">Na przykład `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="231d9-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="231d9-123">To polecenie tworzy katalog o nazwie **exampleudf**, który zawiera projekt Maven hello.</span><span class="sxs-lookup"><span data-stu-id="231d9-123">This command creates a directory named **exampleudf**, which contains hello Maven project.</span></span>

2. <span data-ttu-id="231d9-124">Po utworzeniu projektu hello usunąć hello **exampleudf/src/testowanie** katalogu, który został utworzony jako część hello projektu.</span><span class="sxs-lookup"><span data-stu-id="231d9-124">Once hello project has been created, delete hello **exampleudf/src/test** directory that was created as part of hello project.</span></span>

3. <span data-ttu-id="231d9-125">Otwórz hello **exampleudf/pom.xml**i Zastąp istniejące hello `<dependencies>` wpis o powitania po XML:</span><span class="sxs-lookup"><span data-stu-id="231d9-125">Open hello **exampleudf/pom.xml**, and replace hello existing `<dependencies>` entry with hello following XML:</span></span>

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    <span data-ttu-id="231d9-126">Te wpisy Określ wersję hello Hadoop i Hive dołączonego HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="231d9-126">These entries specify hello version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="231d9-127">Można znaleźć informacji o wersjach hello Hadoop i Hive dostarczone z usługą HDInsight z hello [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="231d9-127">You can find information on hello versions of Hadoop and Hive provided with HDInsight from hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="231d9-128">Dodaj `<build>` sekcji przed hello `</project>` wiersz na końcu hello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="231d9-128">Add a `<build>` section before hello `</project>` line at hello end of hello file.</span></span> <span data-ttu-id="231d9-129">W tej sekcji, powinny zawierać następujące XML hello:</span><span class="sxs-lookup"><span data-stu-id="231d9-129">This section should contain hello following XML:</span></span>

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
                        </transformer>
                    </transformers>
                    <!-- Keep us from getting a bad signature error -->
                    <filters>
                        <filter>
                            <artifact>*:*</artifact>
                            <excludes>
                                <exclude>META-INF/*.SF</exclude>
                                <exclude>META-INF/*.DSA</exclude>
                                <exclude>META-INF/*.RSA</exclude>
                            </excludes>
                        </filter>
                    </filters>
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

    <span data-ttu-id="231d9-130">Te wpisy zdefiniuj, jak toobuild hello projektu.</span><span class="sxs-lookup"><span data-stu-id="231d9-130">These entries define how toobuild hello project.</span></span> <span data-ttu-id="231d9-131">W szczególności hello wersja programu Java, która hello projekt używa i w jaki sposób toobuild uberjar wdrożenia toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="231d9-131">Specifically, hello version of Java that hello project uses and how toobuild an uberjar for deployment toohello cluster.</span></span>

    <span data-ttu-id="231d9-132">Zapisz plik hello, gdy hello zostały zmienione.</span><span class="sxs-lookup"><span data-stu-id="231d9-132">Save hello file once hello changes have been made.</span></span>

4. <span data-ttu-id="231d9-133">Zmień nazwę **exampleudf/src/main/java/com/microsoft/examples/App.java** za**ExampleUDF.java**, a następnie otwórz plik hello w edytorze.</span><span class="sxs-lookup"><span data-stu-id="231d9-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** too**ExampleUDF.java**, and then open hello file in your editor.</span></span>

5. <span data-ttu-id="231d9-134">Zamień zawartość hello hello **ExampleUDF.java** następujący hello, a następnie zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="231d9-134">Replace hello contents of hello **ExampleUDF.java** file with hello following, then save hello file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="231d9-135">Ten kod implementuje UDF, akceptuje wartości ciągu, która zwraca ciąg hello wersję małe litery.</span><span class="sxs-lookup"><span data-stu-id="231d9-135">This code implements a UDF that accepts a string value, and returns a lowercase version of hello string.</span></span>

## <a name="build-and-install-hello-udf"></a><span data-ttu-id="231d9-136">Tworzenie i zainstalować hello funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="231d9-136">Build and install hello UDF</span></span>

1. <span data-ttu-id="231d9-137">Użyj następującego polecenia toocompile hello i pakietów hello funkcji zdefiniowanej przez użytkownika:</span><span class="sxs-lookup"><span data-stu-id="231d9-137">Use hello following command toocompile and package hello UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="231d9-138">To polecenie tworzy i pakietów hello UDF w hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` pliku.</span><span class="sxs-lookup"><span data-stu-id="231d9-138">This command builds and packages hello UDF into hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="231d9-139">Użyj hello `scp` klastra usługi HDInsight toohello polecenia toocopy hello pliku.</span><span class="sxs-lookup"><span data-stu-id="231d9-139">Use hello `scp` command toocopy hello file toohello HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="231d9-140">Zastąp `myuser` z hello konta użytkownika SSH dla klastra.</span><span class="sxs-lookup"><span data-stu-id="231d9-140">Replace `myuser` with hello SSH user account for your cluster.</span></span> <span data-ttu-id="231d9-141">Zastąp `mycluster` hello nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="231d9-141">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="231d9-142">Jeśli używasz hello toosecure hasło konta SSH, to tooenter zostanie wyświetlony monit o hasło hello.</span><span class="sxs-lookup"><span data-stu-id="231d9-142">If you used a password toosecure hello SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="231d9-143">Jeśli używasz certyfikatu może być konieczne toouse hello `-i` parametru toospecify hello pliku klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="231d9-143">If you used a certificate, you may need toouse hello `-i` parameter toospecify hello private key file.</span></span>

3. <span data-ttu-id="231d9-144">Połącz toohello klastra przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="231d9-144">Connect toohello cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="231d9-145">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="231d9-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="231d9-146">W sesji SSH hello skopiuj magazyn tooHDInsight plików jar hello.</span><span class="sxs-lookup"><span data-stu-id="231d9-146">From hello SSH session, copy hello jar file tooHDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a><span data-ttu-id="231d9-147">Użyj hello funkcji zdefiniowanej przez użytkownika z gałęzi</span><span class="sxs-lookup"><span data-stu-id="231d9-147">Use hello UDF from Hive</span></span>

1. <span data-ttu-id="231d9-148">Użyj następującego toostart hello Beeline klienta z sesji SSH hello hello.</span><span class="sxs-lookup"><span data-stu-id="231d9-148">Use hello following toostart hello Beeline client from hello SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="231d9-149">To polecenie przy założeniu, że użytkownik domyślną hello **admin** hello konta logowania dla klastra.</span><span class="sxs-lookup"><span data-stu-id="231d9-149">This command assumes that you used hello default of **admin** for hello login account for your cluster.</span></span>

2. <span data-ttu-id="231d9-150">Po przyjeździe hello `jdbc:hive2://localhost:10001/>` monit, wprowadź następujące tooadd hello UDF tooHive hello i uwidacznia go jako funkcję.</span><span class="sxs-lookup"><span data-stu-id="231d9-150">Once you arrive at hello `jdbc:hive2://localhost:10001/>` prompt, enter hello following tooadd hello UDF tooHive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="231d9-151">W tym przykładzie zakłada, że magazyn Azure domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="231d9-151">This example assumes that Azure Storage is default storage for hello cluster.</span></span> <span data-ttu-id="231d9-152">Jeśli klaster używa zamiast tego Data Lake Store, zmień hello `wasb:///` wartość zbyt`adl:///`.</span><span class="sxs-lookup"><span data-stu-id="231d9-152">If your cluster uses Data Lake Store instead, change hello `wasb:///` value too`adl:///`.</span></span>

3. <span data-ttu-id="231d9-153">Użyj wartości tooconvert UDF hello pobierane z ciągów wielkość toolower tabeli.</span><span class="sxs-lookup"><span data-stu-id="231d9-153">Use hello UDF tooconvert values retrieved from a table toolower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="231d9-154">To zapytanie, wybiera hello platformy urządzenia (Android, Windows, iOS, itp.) z tabeli hello przekonwertować przypadku toolower ciąg hello i wyświetl je.</span><span class="sxs-lookup"><span data-stu-id="231d9-154">This query selects hello device platform (Android, Windows, iOS, etc.) from hello table, convert hello string toolower case, and then display them.</span></span> <span data-ttu-id="231d9-155">dane wyjściowe Hello zostaną wyświetlone podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="231d9-155">hello output appears similar toohello following text:</span></span>

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a><span data-ttu-id="231d9-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="231d9-156">Next steps</span></span>

<span data-ttu-id="231d9-157">Aby uzyskać inne sposoby toowork przy użyciu Hive, zobacz [używanie Hive z usługą HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="231d9-157">For other ways toowork with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="231d9-158">Aby uzyskać więcej informacji na temat funkcji Hive User-Defined, zobacz [operatorów Hive i funkcje zdefiniowane przez użytkownika](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) sekcji hello Hive stron typu wiki w serwisie apache.org.</span><span class="sxs-lookup"><span data-stu-id="231d9-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of hello Hive wiki at apache.org.</span></span>
