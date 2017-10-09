---
title: "aaaUse Hadoop Pig w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse wieprzowe z platformą Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a>Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight

Dowiedz się, jak toouse [Apache Pig](http://pig.apache.org/) z usługą HDInsight...

Pig to platforma do tworzenia programów dla platformy Hadoop przy użyciu języka procedurach znany jako *Pig Latin*. Pig jest alternatywnych tooJava tworzenia *MapReduce* rozwiązania który znajduje się w usłudze Azure HDInsight. Użyj powitania po tabeli toodiscover hello różne sposoby, że Pig mogą być używane z usługą HDInsight:

| **Użyj tej** Jeśli chcesz... | .. .an **interakcyjne** powłoki | ... **partii** przetwarzania | .. zwykle to **systemu operacyjnego klastra** | .. .from to **system operacyjny klienta** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X lub systemu Windows |
| [Interfejs API REST](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux lub Windows |Linux, Unix, Mac OS X lub systemu Windows |
| [Zestaw SDK dla platformy .NET usługi Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux lub Windows |Systemu Windows (na razie) |
| [Środowisko Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux lub Windows |Windows |
| [Pulpit zdalny](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 i 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a id="why"></a>Dlaczego warto korzystać z języka Pig

Jednym z wyzwań hello przetwarzania danych przy użyciu MapReduce w Hadoop przy użyciu tylko mapy i funkcja Zmniejsz implementuje logika przetwarzania. Do złożonych obliczeń, często mają toobreak przetwarzania na wiele operacji MapReduce, które są połączone tooachieve hello żądanego wyniku.

Pig umożliwia toodefine przetwarzania jako serię transformacje, których hello przepływów danych za pośrednictwem tooproduce hello potrzebne w danych wyjściowych.

język Pig Latin Hello pozwala możesz toodescribe hello przepływu danych z nieprzetworzone dane wejściowe, przez co najmniej jeden przekształcenia, dane wyjściowe hello potrzeby tooproduce. Programy pig Latin wykonaj tego wzorca ogólne:

* **Obciążenia**: odczytu danych toobe modyfikowany w zakresie od hello systemu plików

* **Przekształć**: manipulować danymi hello

* **Zrzut lub przechowywać**: ekran toohello danych wyjściowych lub zapisać go do przetworzenia

### <a name="user-defined-functions"></a>Funkcje zdefiniowane przez użytkownika

Pig Latin obsługuje również funkcje zdefiniowane przez użytkownika (UDF), dzięki czemu można tooinvoke składników zewnętrznych, które implementują logikę, która jest trudne toomodel w Pig Latin.

Aby uzyskać więcej informacji na temat Pig Latin, zobacz [1 Ręczne odwołanie Pig Latin](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) i [2 ręczne odwołanie Pig Latin](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).

Przykład przy użyciu funkcji UDF z Pig Zobacz hello w następujących dokumentach:

* [DataFu za pomocą Pig w usłudze HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) -DataFu jest kolekcją przydatne funkcje UDF obsługiwanego przez Apache
* [Używanie języka Python za pomocą Pig i Hive w usłudze HDInsight](hdinsight-python.md)
* [Używanie języka C# z Hive i Pig w usłudze HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a>Przykładowe dane

Usługa HDInsight zapewnia różne przykład zestawów danych, które są przechowywane w hello `/example/data` i `/HdiSamples` katalogów. Te katalogi są hello domyślny magazyn dla klastra. przykład Witaj Pig w tym dokumencie używa hello *log4j* plik `/example/data/sample.log`.

Każdy dziennik wewnątrz pliku hello składa się z pól wiersz, który zawiera `[LOG LEVEL]` pola tooshow hello typu i hello ważność, na przykład:

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

W poprzednim przykładzie hello poziom dziennika hello jest błąd.

> [!NOTE]
> Można także wygenerować plik log4j przy użyciu hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) narzędzia rejestrowania, a następnie przekaż tego obiektu blob tooyour pliku. Zobacz [tooHDInsight przekazywanie danych](hdinsight-upload-data.md) instrukcje. Aby uzyskać więcej informacji o używaniu obiekty BLOB w magazynie Azure z usługą HDInsight, zobacz [Użyj magazynu obiektów Blob Azure z usługą HDInsight](hdinsight-hadoop-use-blob-storage.md).

## <a id="job"></a>Przykładowe zadania

Witaj zadanie Pig Latin ładuje hello `sample.log` plik z hello domyślnego magazynu dla klastra usługi HDInsight. Następnie wykonuje szereg przekształcenia prowadzących liczbę jak wiele razy każdego danych wejściowych hello wystąpił poziomu dziennika. wyniki Hello są zapisywane tooSTDOUT.

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

Witaj poniższej ilustracji przedstawiono podsumowanie jakie każdego transformacji jest toohello danych.

![Graficzna reprezentacja hello przekształcenia][image-hdi-pig-data-transformation]

## <a id="run"></a>Uruchom zadanie Pig Latin hello

HDInsight można uruchamiać zadania Pig Latin przy użyciu różnych metod. Użyj powitania po toodecide tabeli, która metoda jest odpowiednie dla Ciebie, a następnie wykonaj hello łącze, aby uzyskać wskazówki.

| **Użyj tej** Jeśli chcesz... | .. .an **interakcyjne** powłoki | ... **partii** przetwarzania | .. zwykle to **systemu operacyjnego klastra** | .. .from to **klienta** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X lub systemu Windows |
| [Narzędzie curl](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux lub Windows |Linux, Unix, Mac OS X lub systemu Windows |
| [Zestaw SDK dla platformy .NET usługi Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux lub Windows |Systemu Windows (na razie) |
| [Środowisko Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux lub Windows |Windows |
| [Pulpit zdalny](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 i 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="pig-and-sql-server-integration-services"></a>Pig i SQL Server Integration Services

Możesz użyć programu SQL Server Integration Services (SSIS) toorun zadania programu Pig. Hello Azure Feature Pack do SSIS zapewnia hello następujące składniki, które współpracują z zadań Pig w usłudze HDInsight.

* [Zadaniem Azure HDInsight Pig][pigtask]

* [Menedżer połączeń subskrypcji platformy Azure][connectionmanager]

Dowiedz się więcej o hello Azure Feature Pack SSIS [tutaj][ssispack].

## <a id="nextsteps"></a>Następne kroki
Teraz, kiedy znasz już jak toouse Pig z usługą HDInsight, hello Użyj następujących łączy tooexplore toowork inne sposoby z usługą Azure HDInsight.

* [Przekazywanie danych tooHDInsight][hdinsight-upload-data]
* [Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]
* [Korzystanie z usługą HDInsight Sqoop](hdinsight-use-sqoop.md)
* [Korzystanie z Oozie z usługą HDInsight](hdinsight-use-oozie.md)
* [Korzystanie z zadań MapReduce z usługą HDInsight][hdinsight-use-mapreduce]

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
