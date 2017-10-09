---
title: "Zapytanie aaaOptimize Hive w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toooptimize, zapytań programu Hive, dla platformy Hadoop w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a>Optymalizacja zapytań programu Hive w usłudze Azure HDInsight

Domyślnie klastry Hadoop nie są zoptymalizowane pod kątem wydajności. W tym artykule omówiono niektóre najbardziej typowe metody optymalizacji wydajności gałęzi, na stosowanie tooyour zapytania.

## <a name="scale-out-worker-nodes"></a>Skalowanie w poziomie węzłów procesu roboczego

Zwiększenie hello liczba węzłów procesu roboczego w klastrze można wykorzystać więcej toobe mapowań i reduktory uruchamiane równolegle. Istnieją dwa sposoby może zwiększyć skalowania w poziomie w usłudze HDInsight:

* Podczas udostępniania hello można określić hello liczba węzłów procesu roboczego przy użyciu hello portalu Azure, programu Azure PowerShell lub interfejsu wiersza polecenia i platform.  Więcej informacji można znaleźć w artykule [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md) (Tworzenie klastrów usługi HDInsight). Witaj Poniższy zrzut ekranu przedstawia proces roboczy hello konfiguracji węzła na powitania portalu Azure:
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* Na czas wykonywania hello użytkownik może również skalować klastra bez konieczności ponownego tworzenia jedną:

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

Aby uzyskać więcej informacji na temat hello różnych maszyn wirtualnych obsługiwanych przez usługi HDInsight, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="enable-tez"></a>Włączanie aplikacji Tez

[Apache Tez](http://hortonworks.com/hadoop/tez/) jest wykonanie alternatywnych MapReduce toohello silnik:

![tez_1][image-hdi-optimize-hive-tez_1]

Tez przebiega szybciej, ponieważ:

* **Wykonanie skierowane acykliczne Graph (DAG) jako pojedyncze zadanie w aparacie MapReduce hello**. Witaj DAG wymaga każdego zestawu następuje jeden zestaw reduktory toobe mapowań. Powoduje to wiele toobe zadań MapReduce wykonana dla każdego zapytania Hive. Tez nie ma takiego ograniczenia i może przetwarzać DAG złożonego jako jedno zadanie w związku z tym zminimalizować koszty uruchomienia zadania.
* **Pozwala uniknąć niepotrzebnego zapisy**. Ukończenia zadania toomultiple zostanie wykonana dla hello samo zapytanie Hive hello MapReduce aparatu, hello dane wyjściowe każdego zadania są zapisywane tooHDFS dla pośrednich danych. Ponieważ Tez minimalizuje liczbę zadań dla każdego zapytania Hive jest niepotrzebne zapisu tooavoid stanie.
* **Minimalizuje opóźnień uruchamiania**. Tez jest lepsze opóźnienia rozruchu stanie toominimize dzięki zmniejszeniu liczby hello mapowań potrzebuje toostart, a także ulepszanie optymalizacji w całej.
* **Ponownie używa kontenerów**. Zawsze, gdy Tez możliwe jest możliwe tooreuse kontenery tooensure tego opóźnienia powodu toostarting się kontenery jest ograniczona.
* **Techniki optymalizacji ciągłego**. Tradycyjnie optymalizacji została wykonana podczas fazy kompilacji. Więcej informacji na temat danych wejściowych hello jest dostępne umożliwiające lepsze optymalizacji w czasie wykonywania. Tez używa techniki ciągłego optymalizacji, które umożliwia dalsze planu hello toooptimize w fazie środowiska uruchomieniowego hello.

Aby uzyskać więcej informacji dotyczących tych pojęć, zobacz [Apache TEZ](http://hortonworks.com/hadoop/tez/).

Można wprowadzić żadnych zapytań Hive Tez włączane przez prefiksu hello zapytanie z poniższych ustawień hello:

    set hive.execution.engine=tez;

Klastry usługi HDInsight opartej na systemie Linux ma domyślnie włączona w aplikacji Tez.


## <a name="hive-partitioning"></a>Gałąź rejestru partycjonowania

Operacja We/Wy jest hello głównych wąskie gardło do uruchamiania zapytań Hive. Jeśli hello ilość danych, który wymaga toobe odczytać, może być można poprawić wydajność Hello mniejsze. Domyślnie zapytań programu Hive skanowania całego tabele programu Hive. Jest to doskonałe rozwiązanie dla zapytania, takie jak skanowanie tabeli. Jednak dla zapytań, które potrzebują tylko tooscan niewielką ilość danych (na przykład zapytania z filtrowania), to zachowanie tworzy niepotrzebne obciążenie. Partycjonowanie hive umożliwia Hive zapytania tooaccess tylko hello niezbędnej ilości danych w tabele programu Hive.

Partycjonowanie hive jest implementowany przez reorganizacja hello nieprzetworzone dane do nowych katalogów z każdej partycji o własny katalog - gdzie partycji hello jest zdefiniowane przez użytkownika hello. Witaj poniższym diagramie przedstawiono partycjonowania tabeli programu Hive według kolumny hello *roku*. Nowy katalog jest tworzony dla każdego roku.

![Podział na partycje][image-hdi-optimize-hive-partitioning_1]

Niektóre kwestie partycjonowania:

* **Czy nie w partycji** -partycjonowania dla kolumn mających tylko kilka wartości może spowodować kilka partycji. Na przykład tylko partycjonowania na płci tworzy dwa toobe partycje utworzone (męskiego i żeńskiego), w związku z tym tylko zmniejszenia opóźnienia hello maksymalnie o połowę.
* **Nie przez partycję** — na hello y., tworzenie partycji kolumn o unikatowe wartości (na przykład nazwa użytkownika) powoduje, że wiele partycji. W partycji powoduje, że wiele akcent na powitania namenode klastra została ona toohandle hello dużej liczby katalogów.
* **Unikaj danych pochylenia** -rozsądny sposób wybrać opcję kluczem partycjonowania, tak aby wszystkie partycje są nawet rozmiar. Przykładem jest partycjonowania na *stanu* może spowodować hello liczby rekordów w obszarze toobe Kalifornijskiej prawie 30 x z Vermont powodu różnicy toohello w populacji.

toocreate tabeli partycji, użyj hello *podzielona na partycje według* klauzuli:

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

Po utworzeniu tabeli partycjonowanej hello, możesz utworzyć partycjonowania statyczne lub dynamiczne partycjonowanie.

* **Partycjonowania statycznego** oznacza, że masz już podzielonej danych w hello odpowiednich katalogów i poproś ręcznie oparte na lokalizację katalogu hello partycje Hive. Przykładem jest Hello następującego fragmentu kodu.
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* **Dynamiczne partycjonowanie** oznacza, że ma partycje toocreate Hive automatycznie dla Ciebie. Ponieważ został już utworzony hello partycjonowania tabeli na podstawie hello Tabela przemieszczania, potrzebujemy toodo jest wstawiania danych toohello podzielona na partycje tabeli:
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

Aby uzyskać więcej informacji, zobacz [partycjonowane tabele](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).

## <a name="use-hello-orcfile-format"></a>Użyj formatu ORCFile hello
Hive obsługuje różnych formatach plików. Na przykład:

* **Tekst**: to jest domyślny format pliku hello i współdziała z większości scenariuszy
* **Avro**: sprawdza się w przypadku scenariuszy współdziałanie
* **ORC/Parquet**: najbardziej odpowiednie dla wydajności

Format ORC (zoptymalizowanych pod kątem wiersza kolumnowy) jest bardzo wydajny sposób toostore danych gałęzi. Formaty porównaniu tooother, ORC ma hello następujące korzyści:

* Obsługa typów złożonych tym DateTime i typy złożone i częściowo ustrukturyzowanych
* zapasowej too70% kompresji
* indeksy co 10 000 wierszy, co umożliwia pomijanie wierszy
* znaczny spadek wykonywania środowiska wykonawczego

tooenable ORC format, należy najpierw utworzyć tabelę z klauzulą hello *przechowywane jako ORC*:

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

Następnie Wstaw tabeli ORC toohello danych z hello tabeli przemieszczania. Na przykład:

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

Więcej o formacie ORC hello [tutaj](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).

## <a name="vectorization"></a>Vectorization

Vectorization umożliwia Hive tooprocess partii 1024 wiersze razem zamiast przetwarzania jeden wiersz jednocześnie. Oznacza to, że proste operacje są wykonywane szybciej ponieważ toorun wymaga mniej wewnętrznego kodu.

tooenable vectorization prefiks zapytanie Hive z hello następujące ustawienia:

    set hive.vectorized.execution.enabled = true;

Aby uzyskać więcej informacji, zobacz [Przekształcono wykonywania zapytania](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).

## <a name="other-optimization-methods"></a>Inne metody optymalizacji
Dostępnych jest więcej metod optymalizacji można rozważyć, na przykład:

* **Gałąź rejestru bucketing:** technika, która umożliwia toocluster lub segmentu dużych zestawów danych toooptimize kwerendy wydajności.
* **Dołącz do optymalizacji:** optymalizacji wykonanie zapytania gałęzi planowania tooimprove hello wydajność sprzężenia i ograniczyć potrzebę hello wskazówek użytkownika. Aby uzyskać więcej informacji, zobacz [Join optymalizacji](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).
* **Zwiększ reduktory**.

## <a name="next-steps"></a>Następne kroki
W tym artykule uzyskanych kilka typowych metody optymalizacji zapytań Hive. toolearn więcej, zobacz następujące artykuły hello:

* [Use Apache Hive w usłudze HDInsight](hdinsight-use-hive.md)
* [Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Analizowanie danych Twitter przy użyciu Hive w usłudze HDInsight](hdinsight-analyze-twitter-data.md)
* [Analizowanie danych czujnika przy użyciu konsoli zapytania Hive hello na platformie Hadoop w usłudze HDInsight](hdinsight-hive-analyze-sensor-data.md)
* [Korzystanie z programu Hive z HDInsight tooanalyze dzienników witryn sieci Web](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
