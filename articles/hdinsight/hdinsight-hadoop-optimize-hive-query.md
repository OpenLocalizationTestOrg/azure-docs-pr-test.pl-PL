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
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="47263-103">Optymalizacja zapytań programu Hive w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="47263-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="47263-104">Domyślnie klastry Hadoop nie są zoptymalizowane pod kątem wydajności.</span><span class="sxs-lookup"><span data-stu-id="47263-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="47263-105">W tym artykule omówiono niektóre najbardziej typowe metody optymalizacji wydajności gałęzi, na stosowanie tooyour zapytania.</span><span class="sxs-lookup"><span data-stu-id="47263-105">This article covers some most common Hive performance optimization methods that you can apply tooyour queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="47263-106">Skalowanie w poziomie węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="47263-106">Scale out worker nodes</span></span>

<span data-ttu-id="47263-107">Zwiększenie hello liczba węzłów procesu roboczego w klastrze można wykorzystać więcej toobe mapowań i reduktory uruchamiane równolegle.</span><span class="sxs-lookup"><span data-stu-id="47263-107">Increasing hello number of worker nodes in a cluster can leverage more mappers and reducers toobe run in parallel.</span></span> <span data-ttu-id="47263-108">Istnieją dwa sposoby może zwiększyć skalowania w poziomie w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="47263-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="47263-109">Podczas udostępniania hello można określić hello liczba węzłów procesu roboczego przy użyciu hello portalu Azure, programu Azure PowerShell lub interfejsu wiersza polecenia i platform.</span><span class="sxs-lookup"><span data-stu-id="47263-109">At hello provision time, you can specify hello number of worker nodes using hello Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="47263-110">Więcej informacji można znaleźć w artykule [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md) (Tworzenie klastrów usługi HDInsight).</span><span class="sxs-lookup"><span data-stu-id="47263-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="47263-111">Witaj Poniższy zrzut ekranu przedstawia proces roboczy hello konfiguracji węzła na powitania portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="47263-111">hello following screenshot shows hello worker node configuration on hello Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="47263-113">Na czas wykonywania hello użytkownik może również skalować klastra bez konieczności ponownego tworzenia jedną:</span><span class="sxs-lookup"><span data-stu-id="47263-113">At hello run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="47263-115">Aby uzyskać więcej informacji na temat hello różnych maszyn wirtualnych obsługiwanych przez usługi HDInsight, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="47263-115">For more information about hello different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="47263-116">Włączanie aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="47263-116">Enable Tez</span></span>

<span data-ttu-id="47263-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) jest wykonanie alternatywnych MapReduce toohello silnik:</span><span class="sxs-lookup"><span data-stu-id="47263-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine toohello MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="47263-119">Tez przebiega szybciej, ponieważ:</span><span class="sxs-lookup"><span data-stu-id="47263-119">Tez is faster because:</span></span>

* <span data-ttu-id="47263-120">**Wykonanie skierowane acykliczne Graph (DAG) jako pojedyncze zadanie w aparacie MapReduce hello**.</span><span class="sxs-lookup"><span data-stu-id="47263-120">**Execute Directed Acyclic Graph (DAG) as a single job in hello MapReduce engine**.</span></span> <span data-ttu-id="47263-121">Witaj DAG wymaga każdego zestawu następuje jeden zestaw reduktory toobe mapowań.</span><span class="sxs-lookup"><span data-stu-id="47263-121">hello DAG requires each set of mappers toobe followed by one set of reducers.</span></span> <span data-ttu-id="47263-122">Powoduje to wiele toobe zadań MapReduce wykonana dla każdego zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="47263-122">This causes multiple MapReduce jobs toobe spun off for each Hive query.</span></span> <span data-ttu-id="47263-123">Tez nie ma takiego ograniczenia i może przetwarzać DAG złożonego jako jedno zadanie w związku z tym zminimalizować koszty uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="47263-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="47263-124">**Pozwala uniknąć niepotrzebnego zapisy**.</span><span class="sxs-lookup"><span data-stu-id="47263-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="47263-125">Ukończenia zadania toomultiple zostanie wykonana dla hello samo zapytanie Hive hello MapReduce aparatu, hello dane wyjściowe każdego zadania są zapisywane tooHDFS dla pośrednich danych.</span><span class="sxs-lookup"><span data-stu-id="47263-125">Due toomultiple jobs being spun for hello same Hive query in hello MapReduce engine, hello output of each job is written tooHDFS for intermediate data.</span></span> <span data-ttu-id="47263-126">Ponieważ Tez minimalizuje liczbę zadań dla każdego zapytania Hive jest niepotrzebne zapisu tooavoid stanie.</span><span class="sxs-lookup"><span data-stu-id="47263-126">Since Tez minimizes number of jobs for each Hive query it is able tooavoid unnecessary write.</span></span>
* <span data-ttu-id="47263-127">**Minimalizuje opóźnień uruchamiania**.</span><span class="sxs-lookup"><span data-stu-id="47263-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="47263-128">Tez jest lepsze opóźnienia rozruchu stanie toominimize dzięki zmniejszeniu liczby hello mapowań potrzebuje toostart, a także ulepszanie optymalizacji w całej.</span><span class="sxs-lookup"><span data-stu-id="47263-128">Tez is better able toominimize start-up delay by reducing hello number of mappers it needs toostart and also improving optimization throughout.</span></span>
* <span data-ttu-id="47263-129">**Ponownie używa kontenerów**.</span><span class="sxs-lookup"><span data-stu-id="47263-129">**Reuses containers**.</span></span> <span data-ttu-id="47263-130">Zawsze, gdy Tez możliwe jest możliwe tooreuse kontenery tooensure tego opóźnienia powodu toostarting się kontenery jest ograniczona.</span><span class="sxs-lookup"><span data-stu-id="47263-130">Whenever possible Tez is able tooreuse containers tooensure that latency due toostarting up containers is reduced.</span></span>
* <span data-ttu-id="47263-131">**Techniki optymalizacji ciągłego**.</span><span class="sxs-lookup"><span data-stu-id="47263-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="47263-132">Tradycyjnie optymalizacji została wykonana podczas fazy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="47263-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="47263-133">Więcej informacji na temat danych wejściowych hello jest dostępne umożliwiające lepsze optymalizacji w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="47263-133">However more information about hello inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="47263-134">Tez używa techniki ciągłego optymalizacji, które umożliwia dalsze planu hello toooptimize w fazie środowiska uruchomieniowego hello.</span><span class="sxs-lookup"><span data-stu-id="47263-134">Tez uses continuous optimization techniques that allows it toooptimize hello plan further into hello runtime phase.</span></span>

<span data-ttu-id="47263-135">Aby uzyskać więcej informacji dotyczących tych pojęć, zobacz [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="47263-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="47263-136">Można wprowadzić żadnych zapytań Hive Tez włączane przez prefiksu hello zapytanie z poniższych ustawień hello:</span><span class="sxs-lookup"><span data-stu-id="47263-136">You can make any Hive query Tez enabled by prefixing hello query with hello setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="47263-137">Klastry usługi HDInsight opartej na systemie Linux ma domyślnie włączona w aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="47263-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="47263-138">Gałąź rejestru partycjonowania</span><span class="sxs-lookup"><span data-stu-id="47263-138">Hive partitioning</span></span>

<span data-ttu-id="47263-139">Operacja We/Wy jest hello głównych wąskie gardło do uruchamiania zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="47263-139">I/O operation is hello major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="47263-140">Jeśli hello ilość danych, który wymaga toobe odczytać, może być można poprawić wydajność Hello mniejsze.</span><span class="sxs-lookup"><span data-stu-id="47263-140">hello performance can be improved if hello amount of data that needs toobe read can be reduced.</span></span> <span data-ttu-id="47263-141">Domyślnie zapytań programu Hive skanowania całego tabele programu Hive.</span><span class="sxs-lookup"><span data-stu-id="47263-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="47263-142">Jest to doskonałe rozwiązanie dla zapytania, takie jak skanowanie tabeli.</span><span class="sxs-lookup"><span data-stu-id="47263-142">This is great for queries like table scans.</span></span> <span data-ttu-id="47263-143">Jednak dla zapytań, które potrzebują tylko tooscan niewielką ilość danych (na przykład zapytania z filtrowania), to zachowanie tworzy niepotrzebne obciążenie.</span><span class="sxs-lookup"><span data-stu-id="47263-143">However for queries that only need tooscan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="47263-144">Partycjonowanie hive umożliwia Hive zapytania tooaccess tylko hello niezbędnej ilości danych w tabele programu Hive.</span><span class="sxs-lookup"><span data-stu-id="47263-144">Hive partitioning allows Hive queries tooaccess only hello necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="47263-145">Partycjonowanie hive jest implementowany przez reorganizacja hello nieprzetworzone dane do nowych katalogów z każdej partycji o własny katalog - gdzie partycji hello jest zdefiniowane przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="47263-145">Hive partitioning is implemented by reorganizing hello raw data into new directories with each partition having its own directory - where hello partition is defined by hello user.</span></span> <span data-ttu-id="47263-146">Witaj poniższym diagramie przedstawiono partycjonowania tabeli programu Hive według kolumny hello *roku*.</span><span class="sxs-lookup"><span data-stu-id="47263-146">hello following diagram illustrates partitioning a Hive table by hello column *Year*.</span></span> <span data-ttu-id="47263-147">Nowy katalog jest tworzony dla każdego roku.</span><span class="sxs-lookup"><span data-stu-id="47263-147">A new directory is created for each year.</span></span>

![Podział na partycje][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="47263-149">Niektóre kwestie partycjonowania:</span><span class="sxs-lookup"><span data-stu-id="47263-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="47263-150">**Czy nie w partycji** -partycjonowania dla kolumn mających tylko kilka wartości może spowodować kilka partycji.</span><span class="sxs-lookup"><span data-stu-id="47263-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="47263-151">Na przykład tylko partycjonowania na płci tworzy dwa toobe partycje utworzone (męskiego i żeńskiego), w związku z tym tylko zmniejszenia opóźnienia hello maksymalnie o połowę.</span><span class="sxs-lookup"><span data-stu-id="47263-151">For example, partitioning on gender only creates two partitions toobe created (male and female), thus only reduce hello latency by a maximum of half.</span></span>
* <span data-ttu-id="47263-152">**Nie przez partycję** — na hello y., tworzenie partycji kolumn o unikatowe wartości (na przykład nazwa użytkownika) powoduje, że wiele partycji.</span><span class="sxs-lookup"><span data-stu-id="47263-152">**Do not over partition** - On hello other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="47263-153">W partycji powoduje, że wiele akcent na powitania namenode klastra została ona toohandle hello dużej liczby katalogów.</span><span class="sxs-lookup"><span data-stu-id="47263-153">Over partition causes much stress on hello cluster namenode as it has toohandle hello large number of directories.</span></span>
* <span data-ttu-id="47263-154">**Unikaj danych pochylenia** -rozsądny sposób wybrać opcję kluczem partycjonowania, tak aby wszystkie partycje są nawet rozmiar.</span><span class="sxs-lookup"><span data-stu-id="47263-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="47263-155">Przykładem jest partycjonowania na *stanu* może spowodować hello liczby rekordów w obszarze toobe Kalifornijskiej prawie 30 x z Vermont powodu różnicy toohello w populacji.</span><span class="sxs-lookup"><span data-stu-id="47263-155">An example is partitioning on *State* may cause hello number of records under California toobe almost 30x that of Vermont due toohello difference in population.</span></span>

<span data-ttu-id="47263-156">toocreate tabeli partycji, użyj hello *podzielona na partycje według* klauzuli:</span><span class="sxs-lookup"><span data-stu-id="47263-156">toocreate a partition table, use hello *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="47263-157">Po utworzeniu tabeli partycjonowanej hello, możesz utworzyć partycjonowania statyczne lub dynamiczne partycjonowanie.</span><span class="sxs-lookup"><span data-stu-id="47263-157">Once hello partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="47263-158">**Partycjonowania statycznego** oznacza, że masz już podzielonej danych w hello odpowiednich katalogów i poproś ręcznie oparte na lokalizację katalogu hello partycje Hive.</span><span class="sxs-lookup"><span data-stu-id="47263-158">**Static partitioning** means that you have already sharded data in hello appropriate directories and you can ask Hive partitions manually based on hello directory location.</span></span> <span data-ttu-id="47263-159">Przykładem jest Hello następującego fragmentu kodu.</span><span class="sxs-lookup"><span data-stu-id="47263-159">hello following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="47263-160">**Dynamiczne partycjonowanie** oznacza, że ma partycje toocreate Hive automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="47263-160">**Dynamic partitioning** means that you want Hive toocreate partitions automatically for you.</span></span> <span data-ttu-id="47263-161">Ponieważ został już utworzony hello partycjonowania tabeli na podstawie hello Tabela przemieszczania, potrzebujemy toodo jest wstawiania danych toohello podzielona na partycje tabeli:</span><span class="sxs-lookup"><span data-stu-id="47263-161">Since we have already created hello partitioning table from hello staging table, all we need toodo is insert data toohello partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="47263-162">Aby uzyskać więcej informacji, zobacz [partycjonowane tabele](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="47263-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-hello-orcfile-format"></a><span data-ttu-id="47263-163">Użyj formatu ORCFile hello</span><span class="sxs-lookup"><span data-stu-id="47263-163">Use hello ORCFile format</span></span>
<span data-ttu-id="47263-164">Hive obsługuje różnych formatach plików.</span><span class="sxs-lookup"><span data-stu-id="47263-164">Hive supports different file formats.</span></span> <span data-ttu-id="47263-165">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="47263-165">For example:</span></span>

* <span data-ttu-id="47263-166">**Tekst**: to jest domyślny format pliku hello i współdziała z większości scenariuszy</span><span class="sxs-lookup"><span data-stu-id="47263-166">**Text**: this is hello default file format and works with most scenarios</span></span>
* <span data-ttu-id="47263-167">**Avro**: sprawdza się w przypadku scenariuszy współdziałanie</span><span class="sxs-lookup"><span data-stu-id="47263-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="47263-168">**ORC/Parquet**: najbardziej odpowiednie dla wydajności</span><span class="sxs-lookup"><span data-stu-id="47263-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="47263-169">Format ORC (zoptymalizowanych pod kątem wiersza kolumnowy) jest bardzo wydajny sposób toostore danych gałęzi.</span><span class="sxs-lookup"><span data-stu-id="47263-169">ORC (Optimized Row Columnar) format is a highly efficient way toostore Hive data.</span></span> <span data-ttu-id="47263-170">Formaty porównaniu tooother, ORC ma hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="47263-170">Compared tooother formats, ORC has hello following advantages:</span></span>

* <span data-ttu-id="47263-171">Obsługa typów złożonych tym DateTime i typy złożone i częściowo ustrukturyzowanych</span><span class="sxs-lookup"><span data-stu-id="47263-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="47263-172">zapasowej too70% kompresji</span><span class="sxs-lookup"><span data-stu-id="47263-172">up too70% compression</span></span>
* <span data-ttu-id="47263-173">indeksy co 10 000 wierszy, co umożliwia pomijanie wierszy</span><span class="sxs-lookup"><span data-stu-id="47263-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="47263-174">znaczny spadek wykonywania środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="47263-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="47263-175">tooenable ORC format, należy najpierw utworzyć tabelę z klauzulą hello *przechowywane jako ORC*:</span><span class="sxs-lookup"><span data-stu-id="47263-175">tooenable ORC format, you first create a table with hello clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="47263-176">Następnie Wstaw tabeli ORC toohello danych z hello tabeli przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="47263-176">Next, you insert data toohello ORC table from hello staging table.</span></span> <span data-ttu-id="47263-177">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="47263-177">For example:</span></span>

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

<span data-ttu-id="47263-178">Więcej o formacie ORC hello [tutaj](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="47263-178">You can read more on hello ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="47263-179">Vectorization</span><span class="sxs-lookup"><span data-stu-id="47263-179">Vectorization</span></span>

<span data-ttu-id="47263-180">Vectorization umożliwia Hive tooprocess partii 1024 wiersze razem zamiast przetwarzania jeden wiersz jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="47263-180">Vectorization allows Hive tooprocess a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="47263-181">Oznacza to, że proste operacje są wykonywane szybciej ponieważ toorun wymaga mniej wewnętrznego kodu.</span><span class="sxs-lookup"><span data-stu-id="47263-181">It means that simple operations are done faster because less internal code needs toorun.</span></span>

<span data-ttu-id="47263-182">tooenable vectorization prefiks zapytanie Hive z hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="47263-182">tooenable vectorization prefix your Hive query with hello following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="47263-183">Aby uzyskać więcej informacji, zobacz [Przekształcono wykonywania zapytania](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="47263-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="47263-184">Inne metody optymalizacji</span><span class="sxs-lookup"><span data-stu-id="47263-184">Other optimization methods</span></span>
<span data-ttu-id="47263-185">Dostępnych jest więcej metod optymalizacji można rozważyć, na przykład:</span><span class="sxs-lookup"><span data-stu-id="47263-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="47263-186">**Gałąź rejestru bucketing:** technika, która umożliwia toocluster lub segmentu dużych zestawów danych toooptimize kwerendy wydajności.</span><span class="sxs-lookup"><span data-stu-id="47263-186">**Hive bucketing:** a technique that allows toocluster or segment large sets of data toooptimize query performance.</span></span>
* <span data-ttu-id="47263-187">**Dołącz do optymalizacji:** optymalizacji wykonanie zapytania gałęzi planowania tooimprove hello wydajność sprzężenia i ograniczyć potrzebę hello wskazówek użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47263-187">**Join optimization:** optimization of Hive's query execution planning tooimprove hello efficiency of joins and reduce hello need for user hints.</span></span> <span data-ttu-id="47263-188">Aby uzyskać więcej informacji, zobacz [Join optymalizacji](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="47263-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="47263-189">**Zwiększ reduktory**.</span><span class="sxs-lookup"><span data-stu-id="47263-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47263-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="47263-190">Next steps</span></span>
<span data-ttu-id="47263-191">W tym artykule uzyskanych kilka typowych metody optymalizacji zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="47263-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="47263-192">toolearn więcej, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="47263-192">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="47263-193">Use Apache Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="47263-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="47263-194">Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="47263-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="47263-195">Analizowanie danych Twitter przy użyciu Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="47263-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="47263-196">Analizowanie danych czujnika przy użyciu konsoli zapytania Hive hello na platformie Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="47263-196">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="47263-197">Korzystanie z programu Hive z HDInsight tooanalyze dzienników witryn sieci Web</span><span class="sxs-lookup"><span data-stu-id="47263-197">Use Hive with HDInsight tooanalyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
