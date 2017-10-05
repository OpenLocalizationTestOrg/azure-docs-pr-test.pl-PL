---
title: "Java — funkcja zdefiniowana przez użytkownika (UDF) przy użyciu Hive w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia opartych na języku Java — funkcja zdefiniowana przez użytkownika (UDF) współpracujące z gałęzi. W tym przykładzie UDF Konwertuje tabelę ciągów tekst na małe litery."
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
ms.openlocfilehash: 481d234eaf88bdb210821084ee4154159470eda0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="e5380-104">Użyj Java funkcji zdefiniowanej przez użytkownika przy użyciu Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5380-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="e5380-105">Informacje o sposobie tworzenia opartych na języku Java — funkcja zdefiniowana przez użytkownika (UDF) współpracujące z gałęzi.</span><span class="sxs-lookup"><span data-stu-id="e5380-105">Learn how to create a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="e5380-106">UDF języka Java w tym przykładzie konwertuje wszystkie małe znaki tabeli ciągów tekstowych.</span><span class="sxs-lookup"><span data-stu-id="e5380-106">The Java UDF in this example converts a table of text strings to all-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="e5380-107">Wymagania</span><span class="sxs-lookup"><span data-stu-id="e5380-107">Requirements</span></span>

* <span data-ttu-id="e5380-108">Klaster usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5380-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="e5380-109">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="e5380-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e5380-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="e5380-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="e5380-111">Większość kroków w tym dokumencie działają w obu klastrach z systemem Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="e5380-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="e5380-112">Jednak kroki do przekazywania skompilowanych UDF w klastrze i uruchom go są specyficzne dla opartych na systemie Linux klastrów.</span><span class="sxs-lookup"><span data-stu-id="e5380-112">However, the steps used to upload the compiled UDF to the cluster and run it are specific to Linux-based clusters.</span></span> <span data-ttu-id="e5380-113">Zostały podane linki do informacji, które mogą być używane z klastrów z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="e5380-113">Links are provided to information that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="e5380-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 lub nowszy (lub odpowiednik, takie jak OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="e5380-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="e5380-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="e5380-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="e5380-116">Edytora tekstu lub IDE języka Java</span><span class="sxs-lookup"><span data-stu-id="e5380-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e5380-117">Jeśli tworzysz pliki języka Python w kliencie systemu Windows, musisz użyć edytora, używającą LF jako zakończenia linii.</span><span class="sxs-lookup"><span data-stu-id="e5380-117">If you create the Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="e5380-118">Jeśli nie masz pewności, czy edytor używa LF lub CRLF, zobacz [Rozwiązywanie problemów](#troubleshooting) sekcji instrukcje dotyczące usuwania znak CR.</span><span class="sxs-lookup"><span data-stu-id="e5380-118">If you are not sure whether your editor uses LF or CRLF, see the [Troubleshooting](#troubleshooting) section for steps on removing the CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="e5380-119">Utwórz przykład UDF języka Java</span><span class="sxs-lookup"><span data-stu-id="e5380-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="e5380-120">Z wiersza polecenia aby utworzyć nowy projekt Maven skorzystaj z następujących:</span><span class="sxs-lookup"><span data-stu-id="e5380-120">From a command line, use the following to create a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="e5380-121">Jeśli używasz programu PowerShell, możesz umieścić stawiać cudzysłów wokół parametrów.</span><span class="sxs-lookup"><span data-stu-id="e5380-121">If you are using PowerShell, you must put quotes around the parameters.</span></span> <span data-ttu-id="e5380-122">Na przykład `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="e5380-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="e5380-123">To polecenie tworzy katalog o nazwie **exampleudf**, który zawiera projekt Maven.</span><span class="sxs-lookup"><span data-stu-id="e5380-123">This command creates a directory named **exampleudf**, which contains the Maven project.</span></span>

2. <span data-ttu-id="e5380-124">Po utworzeniu projektu, należy usunąć **exampleudf/src/testowanie** katalogu, który został utworzony jako część projektu.</span><span class="sxs-lookup"><span data-stu-id="e5380-124">Once the project has been created, delete the **exampleudf/src/test** directory that was created as part of the project.</span></span>

3. <span data-ttu-id="e5380-125">Otwórz **exampleudf/pom.xml**i Zastąp istniejące `<dependencies>` wpis o następujących XML:</span><span class="sxs-lookup"><span data-stu-id="e5380-125">Open the **exampleudf/pom.xml**, and replace the existing `<dependencies>` entry with the following XML:</span></span>

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

    <span data-ttu-id="e5380-126">Te wpisy Określ wersję usług Hadoop i Hive dołączonego HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="e5380-126">These entries specify the version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="e5380-127">Można znaleźć informacje o wersjach usług Hadoop i Hive wyposażone w usłudze HDInsight z [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5380-127">You can find information on the versions of Hadoop and Hive provided with HDInsight from the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="e5380-128">Dodaj `<build>` sekcji przed `</project>` wiersz na końcu pliku.</span><span class="sxs-lookup"><span data-stu-id="e5380-128">Add a `<build>` section before the `</project>` line at the end of the file.</span></span> <span data-ttu-id="e5380-129">W tej sekcji, powinny zawierać następujące XML:</span><span class="sxs-lookup"><span data-stu-id="e5380-129">This section should contain the following XML:</span></span>

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

    <span data-ttu-id="e5380-130">Te wpisy definiują sposób tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="e5380-130">These entries define how to build the project.</span></span> <span data-ttu-id="e5380-131">W szczególności wersja języka Java, która używa projektu i sposobu tworzenia uberjar wdrożenia do klastra.</span><span class="sxs-lookup"><span data-stu-id="e5380-131">Specifically, the version of Java that the project uses and how to build an uberjar for deployment to the cluster.</span></span>

    <span data-ttu-id="e5380-132">Zapisz plik po dokonaniu zmian.</span><span class="sxs-lookup"><span data-stu-id="e5380-132">Save the file once the changes have been made.</span></span>

4. <span data-ttu-id="e5380-133">Zmień nazwę **exampleudf/src/main/java/com/microsoft/examples/App.java** do **ExampleUDF.java**, a następnie otwórz plik w edytorze.</span><span class="sxs-lookup"><span data-stu-id="e5380-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** to **ExampleUDF.java**, and then open the file in your editor.</span></span>

5. <span data-ttu-id="e5380-134">Zastąp zawartość **ExampleUDF.java** pliku następującym kodem, a następnie zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="e5380-134">Replace the contents of the **ExampleUDF.java** file with the following, then save the file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of the UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of the input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If the value is null, return a null
            if(input == null)
                return null;
            // Lowercase the input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="e5380-135">Ten kod implementuje UDF, akceptuje wartości ciągu, która zwraca wersję małe litery w ciągu.</span><span class="sxs-lookup"><span data-stu-id="e5380-135">This code implements a UDF that accepts a string value, and returns a lowercase version of the string.</span></span>

## <a name="build-and-install-the-udf"></a><span data-ttu-id="e5380-136">Tworzenie i zainstalować funkcję zdefiniowaną przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="e5380-136">Build and install the UDF</span></span>

1. <span data-ttu-id="e5380-137">Użyj następującego polecenia, aby skompilować i pakiet funkcji zdefiniowanej przez użytkownika:</span><span class="sxs-lookup"><span data-stu-id="e5380-137">Use the following command to compile and package the UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="e5380-138">To polecenie tworzy, a następnie umieszcza UDF w `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` pliku.</span><span class="sxs-lookup"><span data-stu-id="e5380-138">This command builds and packages the UDF into the `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="e5380-139">Użyj `scp` polecenie, aby skopiować plik do klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5380-139">Use the `scp` command to copy the file to the HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="e5380-140">Zastąp `myuser` przy użyciu konta użytkownika SSH dla klastra.</span><span class="sxs-lookup"><span data-stu-id="e5380-140">Replace `myuser` with the SSH user account for your cluster.</span></span> <span data-ttu-id="e5380-141">Zastąp `mycluster` z nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="e5380-141">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="e5380-142">Aby zabezpieczyć konto SSH użyto hasła, monit o wprowadzenie hasła.</span><span class="sxs-lookup"><span data-stu-id="e5380-142">If you used a password to secure the SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="e5380-143">Jeśli używasz certyfikatu może być konieczne użycie `-i` parametr, aby określić plik klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="e5380-143">If you used a certificate, you may need to use the `-i` parameter to specify the private key file.</span></span>

3. <span data-ttu-id="e5380-144">Połącz z klastrem przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="e5380-144">Connect to the cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="e5380-145">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e5380-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="e5380-146">W sesji SSH skopiuj plik jar w magazynie usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5380-146">From the SSH session, copy the jar file to HDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-the-udf-from-hive"></a><span data-ttu-id="e5380-147">Użyj funkcji zdefiniowanej przez użytkownika z gałęzi</span><span class="sxs-lookup"><span data-stu-id="e5380-147">Use the UDF from Hive</span></span>

1. <span data-ttu-id="e5380-148">Aby uruchomić klienta Beeline w sesji SSH, należy użyć następującego.</span><span class="sxs-lookup"><span data-stu-id="e5380-148">Use the following to start the Beeline client from the SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="e5380-149">Tym poleceniu założono, że używana jest domyślna **admin** konta logowania dla klastra.</span><span class="sxs-lookup"><span data-stu-id="e5380-149">This command assumes that you used the default of **admin** for the login account for your cluster.</span></span>

2. <span data-ttu-id="e5380-150">Po przyjeździe `jdbc:hive2://localhost:10001/>` monit, wprowadź następujące polecenie, aby dodać funkcję zdefiniowaną przez użytkownika do gałęzi i pozostawić ją jako funkcję.</span><span class="sxs-lookup"><span data-stu-id="e5380-150">Once you arrive at the `jdbc:hive2://localhost:10001/>` prompt, enter the following to add the UDF to Hive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="e5380-151">W tym przykładzie zakłada, że magazyn Azure domyślny magazyn dla klastra.</span><span class="sxs-lookup"><span data-stu-id="e5380-151">This example assumes that Azure Storage is default storage for the cluster.</span></span> <span data-ttu-id="e5380-152">Jeśli klaster używa zamiast tego Data Lake Store, zmień `wasb:///` do wartości `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="e5380-152">If your cluster uses Data Lake Store instead, change the `wasb:///` value to `adl:///`.</span></span>

3. <span data-ttu-id="e5380-153">Do konwersji wartości pobierane z tabeli ciągów małe litery, należy użyć funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e5380-153">Use the UDF to convert values retrieved from a table to lower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="e5380-154">To zapytanie wybiera platformy urządzenia (Android, Windows, iOS, itp.) z tabeli, należy przekonwertować ciąg do niższych wielkość liter, a następnie wyświetlić je.</span><span class="sxs-lookup"><span data-stu-id="e5380-154">This query selects the device platform (Android, Windows, iOS, etc.) from the table, convert the string to lower case, and then display them.</span></span> <span data-ttu-id="e5380-155">Wynik jest podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="e5380-155">The output appears similar to the following text:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e5380-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5380-156">Next steps</span></span>

<span data-ttu-id="e5380-157">Aby uzyskać inne sposoby pracy z Hive, zobacz [używanie Hive z usługą HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="e5380-157">For other ways to work with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="e5380-158">Aby uzyskać więcej informacji na temat funkcji Hive User-Defined, zobacz [operatorów Hive i funkcje zdefiniowane przez użytkownika](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) sekcji Wiki gałęzi w serwisie apache.org.</span><span class="sxs-lookup"><span data-stu-id="e5380-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of the Hive wiki at apache.org.</span></span>
