---
title: "aaaUse DataFu z Pig w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "DataFu to kolekcja bibliotek do użycia z usługą Hadoop. Dowiedz się, jak używasz DataFu z Pig w klastrze usługi HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 0016721a-82be-4773-88ad-91e6b2c21cbb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 357ad8f9694cc590115289877e752bdd242bdadc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-datafu-with-pig-on-hdinsight"></a>DataFu za pomocą pig w usłudze HDInsight

Dowiedz się, jak toouse DataFu z usługą HDInsight. DataFu to kolekcja bibliotek typu Open Source do użycia z Pig na platformie Hadoop.

## <a name="prerequisites"></a>Wymagania wstępne

* Subskrypcja platformy Azure.

* Klaster Azure HDInsight (Linux lub systemem Windows)

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* Podstawowa znajomość [w usłudze HDInsight przy użyciu Pig](hdinsight-use-pig.md)

## <a name="install-datafu-on-linux-based-hdinsight"></a>Zainstaluj DataFu na HDInsight opartych na systemie Linux

> [!IMPORTANT]
> DataFu jest zainstalowany w wersji opartej na systemie Linux klastrów 3.3 lub nowszej, a w klastrach opartych na systemie Windows. Go nie jest zainstalowany w klastrach opartych na systemie Linux starszych niż 3.3.
>
> Jeśli korzystasz z klastra z systemem Windows lub wyższa niż wersja 3.3 opartych na systemie Linux klastrów, Pomiń tę sekcję.

DataFu może zostać pobrana i zainstalowana z hello Maven repozytorium. Użyj powitania po klastra usługi HDInsight tooyour DataFu tooadd kroki:

1. Połącz tooyour opartych na systemie Linux klaster usługi HDInsight przy użyciu protokołu SSH. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Użyj hello poniższe polecenie toodownload hello DataFu jar plik przy użyciu narzędzia wget hello, lub skopiuj i Wklej hello link do pobierania hello toobegin przeglądarki.

    ```
    wget http://central.maven.org/maven2/com/linkedin/datafu/datafu/1.2.0/datafu-1.2.0.jar
    ```

3. Następnie przekaż hello pliku toodefault magazynu dla klastra usługi HDInsight. Umieszczenie w domyślnym pliku hello magazyn umożliwia tooall dostępne węzły w klastrze hello.

    ```
    hdfs dfs -put datafu-1.2.0.jar /example/jars
    ```

    > [!NOTE]
    > poprzednie polecenie Hello przechowuje hello jar w `/example/jars` ponieważ ten katalog już istnieje w magazynie klastra hello. Możesz użyć dowolnej lokalizacji, która ma w magazynie klastra usługi HDInsight.

## <a name="use-datafu-with-pig"></a>DataFu za pomocą Pig

kroki Hello w tej sekcji założono, że czytelnik zna używanie Pig na HDInsight. Aby uzyskać więcej informacji o korzystaniu z języka Pig z usługą HDInsight, zobacz [Use Pig z usługą HDInsight](hdinsight-use-pig.md).

> [!IMPORTANT]
> Jeśli zainstalowano ręcznie przy użyciu kroków hello w poprzedniej sekcji hello DataFu, musi być zarejestrowany przed jego użyciem.
>
> * Jeśli klaster używa magazynu Azure, użyj `wasb://` ścieżki. Na przykład `register wasb:///example/jars/datafu-1.2.0.jar`.
>
> * Jeśli klaster używa usługi Azure Data Lake Store, użyj `adl://` ścieżki. Na przykład `register adl://home/example/jars/datafu-1.2.0.jar`.

Często Definiowanie aliasu dla funkcji DataFu. Witaj poniższym przykładzie zdefiniowano alias `SHA`:

```piglatin
DEFINE SHA datafu.pig.hash.SHA();
```

Następnie można użyć tego aliasu w toogenerate skryptu Pig Latin skrót hello danych wejściowych. Na przykład hello następujący kod zastępuje hello lokalizacji w danych wejściowych hello wartość skrótu:

```piglatin
raw = LOAD '/HdiSamples/HdiSamples/SensorSampleData/building/building.csv' USING
    org.apache.pig.piggybank.storage.CSVExcelStorage(',', 'NO_MULTILINE', 'UNIX', 'SKIP_INPUT_HEADER') AS
    (int1:int,
     id1:chararray,
     int2:int,
     id2:chararray,
     location:chararray);
mask = FOREACH raw GENERATE int1, id1, int2, id2, SHA(location);
DUMP mask;
```

Generuje hello następujące dane wyjściowe:

    (1,M1,25,AC1000,aa5ab35a9174c2062b7f7697b33fafe5ce404cf5fecf6bfbbf0dc96ba0d90046)
    (2,M2,27,FN39TG,7a1ca4ef7515f7276bae7230545829c27810c9d9e98ab2c06066bee6270d5153)
    (3,M3,28,JDNS77,07f62b021771d3cf67e2e1faf18769cc5e5c119ad7d4d1847a11e11d6d5a7ecb)
    (4,M4,17,GG1919,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (5,M5,3,ACMAX22,1ed8c7e56c947bebc0cfcf88c4ea0f02c944568f71df893a99970e4f0c78cddc)
    (6,M6,9,AC1000,c96dd81db196cca5f57bd4270bbb9d9e9d1b242d67f9364005ee1dfdc2632523)
    (7,M7,13,FN39TG,3e049d78d958038ac6bd5dcf038075cc73362b4956aaf7308c3a69c8eca76297)
    (8,M8,25,JDNS77,c1ef40ce0484c698eb4bd27fe56c1e7b68d74f9780ed674210d0e5013dae45e9)
    (9,M9,11,GG1919,a7d355b26bda6bf1196ccffead0b2cf2b81f0a9de5b4876b44407f1dc07e51e6)
    (10,M10,23,ACMAX22,10436829032f361a3de50048de41755140e581467bc1895e6c1a17f423e42d10)
    (11,M11,14,AC1000,348841ef53dbd5a64008a86be432973db790774fb28b59b0d99702a3188b3705)
    (12,M12,26,FN39TG,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (13,M13,25,JDNS77,ed9ad13611d7164839dd3feaf9a7f6a75a4138f389e0d45f8e07fa38da1116a2)
    (14,M14,17,GG1919,80db4ccdca106d37b920206331fcfe3e9e50a9e763d89b54ce3ad5ac8cf30f03)
    (15,M15,19,ACMAX22,3552ac0c032467fbf592cb4d10c5c9267800c01e343ad8ca557256d882ae9327)
    (16,M16,23,AC1000,07c67d76ef92ac9853588e098983fefba4ba5965f8fec95f42ab0d04c27865ba)
    (17,M17,11,FN39TG,557c1599d9a04895d3817d293e0806a4419a14de31958386182798d0d2ed3a56)
    (18,M18,25,JDNS77,dbc74a36d8e7439c45c64d856388506cc9b1218619cef979c3d605115a7a4546)
    (19,M19,14,GG1919,be55ef3f4c4e6c2d9c2afe2a33ac90ad0f50d4de7f9163999877e2a9ca5a54f8)
    (20,M20,19,ACMAX22,ea0b937ea317101ee2c26b03a4843a19ceced8a2b9673c3cf409a726ca2b0fd8)

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących DataFu lub Pig Zobacz hello w następujących dokumentach:

* [Apache DataFu Pig przewodnik](http://datafu.incubator.apache.org/docs/datafu/guide.html).
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
