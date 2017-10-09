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
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a>Użyj Java funkcji zdefiniowanej przez użytkownika przy użyciu Hive w usłudze HDInsight

Dowiedz się, jak toocreate opartych na języku Java zdefiniowane przez użytkownika (UDF) funkcja, która współdziała z gałęzi. Witaj UDF języka Java w tym przykładzie Konwertuje tabelę małe tooall ciągów znaków.

## <a name="requirements"></a>Wymagania

* Klaster usługi HDInsight 

    > [!IMPORTANT]
    > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

    Większość kroków w tym dokumencie działają w obu klastrach z systemem Windows i Linux. Jednak hello krokami tooupload hello skompilować UDF toohello klastra i uruchom go są określone na podstawie tooLinux klastry. Łącza podano tooinformation, który może być używany z klastrów z systemem Windows.

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 lub nowszy (lub odpowiednik, takie jak OpenJDK)

* [Apache Maven](http://maven.apache.org/)

* Edytora tekstu lub IDE języka Java

    > [!IMPORTANT]
    > Jeśli tworzysz hello pliki języka Python w kliencie systemu Windows, musisz użyć edytora, używającą LF jako zakończenia linii. Jeśli nie masz pewności, czy edytor używa LF lub CRLF, zobacz hello [Rozwiązywanie problemów](#troubleshooting) sekcji dla kroki dotyczące usuwania hello CR znaków.

## <a name="create-an-example-java-udf"></a>Utwórz przykład UDF języka Java 

1. Z wiersza polecenia użyj następującego toocreate nowy projekt Maven hello:

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > Jeśli używasz programu PowerShell, możesz umieścić stawiać cudzysłów wokół hello parametrów. Na przykład `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.

    To polecenie tworzy katalog o nazwie **exampleudf**, który zawiera projekt Maven hello.

2. Po utworzeniu projektu hello usunąć hello **exampleudf/src/testowanie** katalogu, który został utworzony jako część hello projektu.

3. Otwórz hello **exampleudf/pom.xml**i Zastąp istniejące hello `<dependencies>` wpis o powitania po XML:

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

    Te wpisy Określ wersję hello Hadoop i Hive dołączonego HDInsight 3.5. Można znaleźć informacji o wersjach hello Hadoop i Hive dostarczone z usługą HDInsight z hello [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md) dokumentu.

    Dodaj `<build>` sekcji przed hello `</project>` wiersz na końcu hello hello pliku. W tej sekcji, powinny zawierać następujące XML hello:

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

    Te wpisy zdefiniuj, jak toobuild hello projektu. W szczególności hello wersja programu Java, która hello projekt używa i w jaki sposób toobuild uberjar wdrożenia toohello klastra.

    Zapisz plik hello, gdy hello zostały zmienione.

4. Zmień nazwę **exampleudf/src/main/java/com/microsoft/examples/App.java** za**ExampleUDF.java**, a następnie otwórz plik hello w edytorze.

5. Zamień zawartość hello hello **ExampleUDF.java** następujący hello, a następnie zapisz plik hello.

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

    Ten kod implementuje UDF, akceptuje wartości ciągu, która zwraca ciąg hello wersję małe litery.

## <a name="build-and-install-hello-udf"></a>Tworzenie i zainstalować hello funkcji zdefiniowanej przez użytkownika

1. Użyj następującego polecenia toocompile hello i pakietów hello funkcji zdefiniowanej przez użytkownika:

    ```bash
    mvn compile package
    ```

    To polecenie tworzy i pakietów hello UDF w hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` pliku.

2. Użyj hello `scp` klastra usługi HDInsight toohello polecenia toocopy hello pliku.

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    Zastąp `myuser` z hello konta użytkownika SSH dla klastra. Zastąp `mycluster` hello nazwą klastra. Jeśli używasz hello toosecure hasło konta SSH, to tooenter zostanie wyświetlony monit o hasło hello. Jeśli używasz certyfikatu może być konieczne toouse hello `-i` parametru toospecify hello pliku klucza prywatnego.

3. Połącz toohello klastra przy użyciu protokołu SSH.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

4. W sesji SSH hello skopiuj magazyn tooHDInsight plików jar hello.

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a>Użyj hello funkcji zdefiniowanej przez użytkownika z gałęzi

1. Użyj następującego toostart hello Beeline klienta z sesji SSH hello hello.

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    To polecenie przy założeniu, że użytkownik domyślną hello **admin** hello konta logowania dla klastra.

2. Po przyjeździe hello `jdbc:hive2://localhost:10001/>` monit, wprowadź następujące tooadd hello UDF tooHive hello i uwidacznia go jako funkcję.

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > W tym przykładzie zakłada, że magazyn Azure domyślny magazyn dla klastra hello. Jeśli klaster używa zamiast tego Data Lake Store, zmień hello `wasb:///` wartość zbyt`adl:///`.

3. Użyj wartości tooconvert UDF hello pobierane z ciągów wielkość toolower tabeli.

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    To zapytanie, wybiera hello platformy urządzenia (Android, Windows, iOS, itp.) z tabeli hello przekonwertować przypadku toolower ciąg hello i wyświetl je. dane wyjściowe Hello zostaną wyświetlone podobne toohello następującego tekstu:

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

## <a name="next-steps"></a>Następne kroki

Aby uzyskać inne sposoby toowork przy użyciu Hive, zobacz [używanie Hive z usługą HDInsight](hdinsight-use-hive.md).

Aby uzyskać więcej informacji na temat funkcji Hive User-Defined, zobacz [operatorów Hive i funkcje zdefiniowane przez użytkownika](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) sekcji hello Hive stron typu wiki w serwisie apache.org.
