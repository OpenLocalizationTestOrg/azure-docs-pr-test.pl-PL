---
title: "aaaUse C# z Hive i Pig na platformie Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse C# zdefiniowane przez użytkownika (UDF) funkcje za pomocą technologii Hive i Pig przesyłania strumieniowego w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a>C# zdefiniowane przez użytkownika funkcji za pomocą technologii Hive i Pig przesyłania strumieniowego na platformie Hadoop w usłudze HDInsight

Dowiedz się, jak toouse C# funkcje zdefiniowane przez użytkownika (UDF) z Apache Hive i Pig w usłudze HDInsight.

> [!IMPORTANT]
> Hello kroków w tym dokumencie pracy z klastrami usługi HDInsight opartych na systemie Linux, a także z systemem Windows. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md).

Zarówno Hive i Pig można przekazać danych tooexternal aplikacje do przetworzenia. Ten proces jest nazywany _przesyłania strumieniowego_. Podczas korzystania z aplikacji .NET, hello przekazywania danych aplikacji toohello STDIN, a aplikacja hello zwraca wyniki hello ze strumienia STDOUT. tooread i zapisu z STDIN i STDOUT, można użyć `Console.ReadLine()` i `Console.WriteLine()` z aplikacji konsoli.

## <a name="prerequisites"></a>Wymagania wstępne

* Znajomość pisania i kompilowania kodu C#, przeznaczonego dla programu .NET Framework 4.5.

    * Użyj dowolnej IDE ma. Firma Microsoft zaleca [programu Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, lub [Visual Studio Code](https://code.visualstudio.com/). Witaj kroków w tym dokumencie Visual Studio 2017 r.

* .Exe tooupload sposób pliki toohello klastra i wykonywania zadań Pig i Hive. Zalecamy hello Data Lake Tools dla programu Visual Studio, programu Azure PowerShell i interfejsu wiersza polecenia Azure. Witaj kroki opisane w tym dokumencie użycia hello Data Lake Tools dla Visual Studio tooupload hello plików i uruchom hello przykładowe zapytanie Hive.

    Informacji na temat innych sposobów zapytań programu Hive toorun i zadań Pig Zobacz hello w następujących dokumentach:

    * [Use Apache Hive z usługą HDInsight](hdinsight-use-hive.md)

    * [Use Apache Pig z usługą HDInsight](hdinsight-use-pig.md)

* Hadoop w klastrze usługi HDInsight. Aby uzyskać więcej informacji na temat tworzenia klastra, zobacz [tworzenia klastra usługi HDInsight](hdinsight-provision-clusters.md).

## <a name="net-on-hdinsight"></a>.NET w usłudze HDInsight

* __HDInsight opartych na systemie Linux__ klastrów za pomocą [Mono (https://mono-project.com)](https://mono-project.com) toorun aplikacji .NET. Wersja mono 4.2.1 jest uwzględniona w usłudze HDInsight w wersji 3.5.

    Aby uzyskać więcej informacji na Mono zgodność z wersji systemu .NET Framework, zobacz [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/).

    toouse określonej wersji Mono, zobacz hello [instalacji lub aktualizacji Mono](hdinsight-hadoop-install-mono.md) dokumentu.

* __HDInsight opartych na systemie Windows__ klastrom aplikacji .NET toorun Microsoft .NET CLR hello.

Aby uzyskać więcej informacji o wersji hello hello .NET framework i Mono dołączone do wersji usługi HDInsight, zobacz [wersji składnika usługi HDInsight](hdinsight-component-versioning.md).

## <a name="create-hello-c-projects"></a>Utwórz hello C\# projektów

### <a name="hive-udf"></a>Hive funkcji zdefiniowanej przez użytkownika

1. Otwórz program Visual Studio i utworzyć rozwiązanie. Typ projektu hello wybierz **aplikacji konsoli (.NET Framework)**i nazwę hello nowy projekt **HiveCSharp**.

    > [!IMPORTANT]
    > Wybierz __.NET Framework 4.5__ korzystania z klastra usługi HDInsight opartej na systemie Linux. Aby uzyskać więcej informacji na Mono zgodność z wersji systemu .NET Framework, zobacz [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/).

2. Zamień zawartość hello **Program.cs** hello następujący:

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. Tworzenie projektu hello.

### <a name="pig-udf"></a>Pig funkcji zdefiniowanej przez użytkownika

1. Otwórz program Visual Studio i utworzyć rozwiązanie. Typ projektu hello wybierz **aplikacji konsoli**i nowy projekt hello nazwa **PigUDF**.

2. Zamień zawartość hello hello **Program.cs** pliku z hello następującego kodu:

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    Ta aplikacja analizuje wierszy hello wysłanych z Pig i ponownego formatowania wierszy, które zaczynają się od `java.lang.Exception`.

3. Zapisz **Program.cs**i późniejszego kompilowania hello projektu.

## <a name="upload-toostorage"></a>Przekaż toostorage

1. W programie Visual Studio Otwórz **Eksploratora serwera**.

2. Rozwiń węzeł **Azure**, a następnie rozwiń węzeł **HDInsight**.

3. Jeśli zostanie wyświetlony monit, wprowadź swoje poświadczenia subskrypcji platformy Azure, a następnie kliknij przycisk **logowania**.

4. Rozwiń węzeł klastra usługi HDInsight hello, która ma toodeploy tej aplikacji w celu. Wpis tekstem hello __(domyślne konto magazynu)__ ma na liście.

    ![Wyświetlanie hello konta magazynu dla klastra hello Eksploratora serwera](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Jeśli tego wpisu można rozszerzać, używasz __konta magazynu Azure__ jako domyślny magazyn dla klastra hello. Rozwiń pozycję hello tooview hello pliki hello domyślny magazyn dla klastra hello, a następnie kliknij dwukrotnie hello __(domyślny kontener)__.

    * Jeśli tego wpisu nie można rozwijać, używasz __Azure Data Lake Store__ jako hello domyślny magazyn dla klastra hello. pliki hello tooview hello domyślny magazyn dla klastra hello, kliknij dwukrotnie hello __(domyślne konto magazynu)__ wpisu.

6. pliki .exe hello tooupload, użyj jednej z hello następujące metody:

    * Jeśli przy użyciu __konta magazynu Azure__, kliknij ikonę przekazywania hello, a następnie wyszukaj toohello **bin\debug** folder hello **HiveCSharp** projektu. Na koniec wybierz hello **HiveCSharp.exe** plik i kliknij przycisk **Ok**.

        ![Przekaż ikonę](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Jeśli przy użyciu __Azure Data Lake Store__, kliknij prawym przyciskiem myszy pusty obszar liście hello zawartości pliku, a następnie wybierz __przekazać__. Na koniec wybierz hello **HiveCSharp.exe** plik i kliknij przycisk **Otwórz**.

    Raz hello __HiveCSharp.exe__ przekazywania zakończył proces przekazywania powtarzania hello hello __PigUDF.exe__ pliku.

## <a name="run-a-hive-query"></a>Uruchomienie zapytania programu Hive

1. W programie Visual Studio Otwórz **Eksploratora serwera**.

2. Rozwiń węzeł **Azure**, a następnie rozwiń węzeł **HDInsight**.

3. Kliknij prawym przyciskiem myszy klaster hello wdrożonymi hello **HiveCSharp** do aplikacji, a następnie wybierz **Napisz zapytanie Hive**.

4. Użyj następującego tekstu dla zapytania Hive hello hello:

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > Usuń znaczniki komentarza hello `add file` instrukcji, która odpowiada hello typu magazyny domyślne używane dla klastra.

    To zapytanie wybiera hello `clientid`, `devicemake`, i `devicemodel` pola z `hivesampletable`i przekazuje pola hello toohello HiveCSharp.exe aplikacji. Zapytanie Hello oczekuje hello aplikacji tooreturn trzy pola, które są przechowywane jako `clientid`, `phoneLabel`, i `phoneHash`. Zapytanie Hello oczekuje również toofind HiveCSharp.exe w katalogu głównym hello hello domyślnego kontenera magazynu.

5. Kliknij przycisk **przesyłania** klastra usługi HDInsight toohello toosubmit hello zadania. Witaj **Podsumowanie zadania Hive** zostanie otwarte okno.

6. Kliknij przycisk **Odśwież** toorefresh hello podsumowania do **stan zadania** zmiany zbyt**Ukończono**. dane wyjściowe zadania hello tooview, kliknij przycisk **dane wyjściowe zadania**.

## <a name="run-a-pig-job"></a>Uruchom zadanie Pig

1. Użyj jednej z powitania po klastra usługi HDInsight tooyour tooconnect metod:

    * Jeśli używasz __opartych na systemie Linux__ HDInsight klastra, należy użyć protokołu SSH. Na przykład `ssh sshuser@mycluster-ssh.azurehdinsight.net`. Aby uzyskać więcej informacji, zobacz [withHDInsight używanie protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md)
    
    * Jeśli używasz __opartych na systemie Windows__ klastra usługi HDInsight [Connect toohello klastra przy użyciu pulpitu zdalnego](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)

2. Użyj hello jednym następującego wiersza polecenia Pig hello toostart polecenia:

        pig

    > [!IMPORTANT]
    > Jeśli korzystasz z klastra z systemem Windows, należy użyć hello zamiast tego następujące polecenia:
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    A `grunt>` zostanie wyświetlony monit.

3. Wprowadź następujące toorun zadanie Pig, które korzysta z aplikacji .NET Framework hello hello:

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    Witaj `DEFINE` instrukcja tworzy alias `streamer` w przypadku aplikacji hello pigudf.exe i `CACHE` ładuje go z domyślny magazyn dla klastra hello. Później `streamer` jest używany z hello `STREAM` operator tooprocess hello pojedynczych wierszy zawartych w DZIENNIKÓW i danych hello zwracany jako serię kolumn.

    > [!NOTE]
    > Nazwa aplikacji Hello, który służy do przesyłania strumieniowego musi być ujęte w hello \` (backtick) gdy znak, ponieważ i ' (pojedynczy cudzysłów) w przypadku użycia z `SHIP`.

4. Po wprowadzeniu hello ostatni wiersz, należy zacząć hello zadania. Zwraca dane wyjściowe toohello podobne następującego tekstu:

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a>Następne kroki

W tym dokumencie wiesz już, jak toouse aplikacji .NET Framework, Hive i Pig w usłudze HDInsight. Jeśli chcesz toolearn toouse Python z Hive i Pig, zobacz temat [Użyj Python z Hive i Pig w usłudze HDInsight](hdinsight-python.md).

Inne sposoby toouse Pig i Hive i toolearn o korzystaniu z MapReduce Zobacz hello w następujących dokumentach:

* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystać z usługi MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)
