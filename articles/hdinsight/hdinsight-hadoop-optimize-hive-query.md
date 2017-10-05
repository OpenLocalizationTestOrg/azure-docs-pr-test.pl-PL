---
title: "Optymalizacja zapytań programu Hive w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zoptymalizować zapytania Hive dla platformy Hadoop w usłudze HDInsight."
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
ms.openlocfilehash: edbf797e6277a65b5311e4939f5ab72776b11557
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="36522-103">Optymalizacja zapytań programu Hive w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="36522-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="36522-104">Domyślnie klastry Hadoop nie są zoptymalizowane pod kątem wydajności.</span><span class="sxs-lookup"><span data-stu-id="36522-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="36522-105">W tym artykule omówiono niektóre najczęściej stosowane do zapytania metody optymalizacji wydajności Hive.</span><span class="sxs-lookup"><span data-stu-id="36522-105">This article covers some most common Hive performance optimization methods that you can apply to your queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="36522-106">Skalowanie w poziomie węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="36522-106">Scale out worker nodes</span></span>

<span data-ttu-id="36522-107">Zwiększenie liczby węzłów procesu roboczego w klastrze, można wykorzystać więcej mapowań i reduktory do uruchomienia równoległego.</span><span class="sxs-lookup"><span data-stu-id="36522-107">Increasing the number of worker nodes in a cluster can leverage more mappers and reducers to be run in parallel.</span></span> <span data-ttu-id="36522-108">Istnieją dwa sposoby może zwiększyć skalowania w poziomie w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="36522-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="36522-109">Podczas udostępniania można określić liczbę węzłów procesu roboczego przy użyciu portalu Azure, programu Azure PowerShell lub interfejsu wiersza polecenia i platform.</span><span class="sxs-lookup"><span data-stu-id="36522-109">At the provision time, you can specify the number of worker nodes using the Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="36522-110">Więcej informacji można znaleźć w artykule [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md) (Tworzenie klastrów usługi HDInsight).</span><span class="sxs-lookup"><span data-stu-id="36522-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="36522-111">Poniższy zrzut ekranu przedstawia proces roboczy konfiguracji węzła w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="36522-111">The following screenshot shows the worker node configuration on the Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="36522-113">W czasie wykonywania użytkownik może również skalować klastra bez konieczności ponownego tworzenia jedną:</span><span class="sxs-lookup"><span data-stu-id="36522-113">At the run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="36522-115">Aby uzyskać więcej informacji o różnych maszyn wirtualnych obsługiwanych przez usługi HDInsight, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="36522-115">For more information about the different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="36522-116">Włączanie aplikacji Tez</span><span class="sxs-lookup"><span data-stu-id="36522-116">Enable Tez</span></span>

<span data-ttu-id="36522-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) jest aparatowi wykonywania alternatywnych aparat MapReduce:</span><span class="sxs-lookup"><span data-stu-id="36522-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine to the MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="36522-119">Tez przebiega szybciej, ponieważ:</span><span class="sxs-lookup"><span data-stu-id="36522-119">Tez is faster because:</span></span>

* <span data-ttu-id="36522-120">**Wykonanie skierowane acykliczne Graph (DAG) jako pojedyncze zadanie w aparacie MapReduce**.</span><span class="sxs-lookup"><span data-stu-id="36522-120">**Execute Directed Acyclic Graph (DAG) as a single job in the MapReduce engine**.</span></span> <span data-ttu-id="36522-121">DAG wymaga każdy zestaw mapowań przez jeden zestaw reduktory.</span><span class="sxs-lookup"><span data-stu-id="36522-121">The DAG requires each set of mappers to be followed by one set of reducers.</span></span> <span data-ttu-id="36522-122">Powoduje to wiele zadań MapReduce być wykonana dla każdego zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="36522-122">This causes multiple MapReduce jobs to be spun off for each Hive query.</span></span> <span data-ttu-id="36522-123">Tez nie ma takiego ograniczenia i może przetwarzać DAG złożonego jako jedno zadanie w związku z tym zminimalizować koszty uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="36522-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="36522-124">**Pozwala uniknąć niepotrzebnego zapisy**.</span><span class="sxs-lookup"><span data-stu-id="36522-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="36522-125">Ze względu na wiele zadań jest wykonana dla tego samego zapytania Hive w aparacie MapReduce dane wyjściowe każdego zadania są zapisywane w systemie plików HDFS dla pośrednich danych.</span><span class="sxs-lookup"><span data-stu-id="36522-125">Due to multiple jobs being spun for the same Hive query in the MapReduce engine, the output of each job is written to HDFS for intermediate data.</span></span> <span data-ttu-id="36522-126">Ponieważ Tez minimalizuje liczbę zadań dla każdego zapytania Hive jest w stanie uniknąć niepotrzebnych zapisu.</span><span class="sxs-lookup"><span data-stu-id="36522-126">Since Tez minimizes number of jobs for each Hive query it is able to avoid unnecessary write.</span></span>
* <span data-ttu-id="36522-127">**Minimalizuje opóźnień uruchamiania**.</span><span class="sxs-lookup"><span data-stu-id="36522-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="36522-128">Tez lepiej jest w stanie zminimalizować opóźnienie rozpoczęcia zmniejszenie liczby mapowań niezbędne do uruchomienia, a także zwiększanie optymalizacji w całej.</span><span class="sxs-lookup"><span data-stu-id="36522-128">Tez is better able to minimize start-up delay by reducing the number of mappers it needs to start and also improving optimization throughout.</span></span>
* <span data-ttu-id="36522-129">**Ponownie używa kontenerów**.</span><span class="sxs-lookup"><span data-stu-id="36522-129">**Reuses containers**.</span></span> <span data-ttu-id="36522-130">Po każdej zmianie Tez możliwe jest ponowne użycie kontenerów, aby upewnić się, zmniejsza opóźnienia z powodu uruchamiania kontenerów.</span><span class="sxs-lookup"><span data-stu-id="36522-130">Whenever possible Tez is able to reuse containers to ensure that latency due to starting up containers is reduced.</span></span>
* <span data-ttu-id="36522-131">**Techniki optymalizacji ciągłego**.</span><span class="sxs-lookup"><span data-stu-id="36522-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="36522-132">Tradycyjnie optymalizacji została wykonana podczas fazy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="36522-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="36522-133">Więcej informacji na temat danych wejściowych jest dostępne umożliwiające lepsze optymalizacji w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="36522-133">However more information about the inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="36522-134">Tez używa techniki ciągłego optymalizacji, które umożliwia Optymalizowanie planu dalsze w fazie środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="36522-134">Tez uses continuous optimization techniques that allows it to optimize the plan further into the runtime phase.</span></span>

<span data-ttu-id="36522-135">Aby uzyskać więcej informacji dotyczących tych pojęć, zobacz [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="36522-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="36522-136">Można wprowadzić żadnych zapytań Hive Tez włączane przez prefiksu zapytanie z poniższych ustawień:</span><span class="sxs-lookup"><span data-stu-id="36522-136">You can make any Hive query Tez enabled by prefixing the query with the setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="36522-137">Klastry usługi HDInsight opartej na systemie Linux ma domyślnie włączona w aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="36522-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="36522-138">Gałąź rejestru partycjonowania</span><span class="sxs-lookup"><span data-stu-id="36522-138">Hive partitioning</span></span>

<span data-ttu-id="36522-139">Operacja We/Wy jest głównych wąskie gardło do uruchamiania zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="36522-139">I/O operation is the major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="36522-140">Wydajność można poprawić, jeśli można zmniejszyć ilość danych, który musi być do odczytu.</span><span class="sxs-lookup"><span data-stu-id="36522-140">The performance can be improved if the amount of data that needs to be read can be reduced.</span></span> <span data-ttu-id="36522-141">Domyślnie zapytań programu Hive skanowania całego tabele programu Hive.</span><span class="sxs-lookup"><span data-stu-id="36522-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="36522-142">Jest to doskonałe rozwiązanie dla zapytania, takie jak skanowanie tabeli.</span><span class="sxs-lookup"><span data-stu-id="36522-142">This is great for queries like table scans.</span></span> <span data-ttu-id="36522-143">Jednak dla zapytań, które należy tylko skanowanie niewielką ilość danych (na przykład zapytania z filtrowania), to zachowanie tworzy niepotrzebne obciążenie.</span><span class="sxs-lookup"><span data-stu-id="36522-143">However for queries that only need to scan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="36522-144">Partycjonowanie hive umożliwia zapytań programu Hive dostępu niezbędnej ilości danych w tabelach gałęzi do.</span><span class="sxs-lookup"><span data-stu-id="36522-144">Hive partitioning allows Hive queries to access only the necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="36522-145">Partycjonowanie hive jest implementowany przez reorganizacja nieprzetworzone dane do nowych katalogów z każdej partycji o własny katalog — gdy partycja jest zdefiniowany przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="36522-145">Hive partitioning is implemented by reorganizing the raw data into new directories with each partition having its own directory - where the partition is defined by the user.</span></span> <span data-ttu-id="36522-146">Na poniższym diagramie przedstawiono partycjonowania tabeli programu Hive w kolumnie *roku*.</span><span class="sxs-lookup"><span data-stu-id="36522-146">The following diagram illustrates partitioning a Hive table by the column *Year*.</span></span> <span data-ttu-id="36522-147">Nowy katalog jest tworzony dla każdego roku.</span><span class="sxs-lookup"><span data-stu-id="36522-147">A new directory is created for each year.</span></span>

![Podział na partycje][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="36522-149">Niektóre kwestie partycjonowania:</span><span class="sxs-lookup"><span data-stu-id="36522-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="36522-150">**Czy nie w partycji** -partycjonowania dla kolumn mających tylko kilka wartości może spowodować kilka partycji.</span><span class="sxs-lookup"><span data-stu-id="36522-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="36522-151">Na przykład partycjonowania na płci tylko tworzy dwie partycje można utworzyć (męskiego i żeńskiego), w związku z tym tylko zmniejszyć opóźnienia maksymalnie o połowę.</span><span class="sxs-lookup"><span data-stu-id="36522-151">For example, partitioning on gender only creates two partitions to be created (male and female), thus only reduce the latency by a maximum of half.</span></span>
* <span data-ttu-id="36522-152">**Nie przez partycję** — na y. utworzeniu partycji dla kolumny zawierającej unikatowe wartości (na przykład nazwa użytkownika) powoduje, że wiele partycji.</span><span class="sxs-lookup"><span data-stu-id="36522-152">**Do not over partition** - On the other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="36522-153">W partycji powoduje dużo akcent namenode klastra, musi do obsługi dużej liczby katalogów.</span><span class="sxs-lookup"><span data-stu-id="36522-153">Over partition causes much stress on the cluster namenode as it has to handle the large number of directories.</span></span>
* <span data-ttu-id="36522-154">**Unikaj danych pochylenia** -rozsądny sposób wybrać opcję kluczem partycjonowania, tak aby wszystkie partycje są nawet rozmiar.</span><span class="sxs-lookup"><span data-stu-id="36522-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="36522-155">Przykładem jest partycjonowania na *stanu* może spowodować to liczba rekordów w obszarze Kalifornijskiej być prawie 30 x z Vermont z powodu różnic w populacji.</span><span class="sxs-lookup"><span data-stu-id="36522-155">An example is partitioning on *State* may cause the number of records under California to be almost 30x that of Vermont due to the difference in population.</span></span>

<span data-ttu-id="36522-156">Aby utworzyć tabelę partycji, użyj *podzielona na partycje według* klauzuli:</span><span class="sxs-lookup"><span data-stu-id="36522-156">To create a partition table, use the *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="36522-157">Po utworzeniu tabeli partycjonowanej, możesz utworzyć partycjonowania statyczne lub dynamiczne partycjonowanie.</span><span class="sxs-lookup"><span data-stu-id="36522-157">Once the partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="36522-158">**Partycjonowania statycznego** oznacza, że masz już podzielonej danych w odpowiednich katalogów i poproś partycje Hive ręcznie oparte na lokalizację katalogu.</span><span class="sxs-lookup"><span data-stu-id="36522-158">**Static partitioning** means that you have already sharded data in the appropriate directories and you can ask Hive partitions manually based on the directory location.</span></span> <span data-ttu-id="36522-159">Poniższy fragment kodu jest wartością przykładową.</span><span class="sxs-lookup"><span data-stu-id="36522-159">The following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="36522-160">**Dynamiczne partycjonowanie** oznacza, że chcesz gałąź, aby automatycznie utworzyć partycji dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="36522-160">**Dynamic partitioning** means that you want Hive to create partitions automatically for you.</span></span> <span data-ttu-id="36522-161">Ponieważ został już utworzony partycjonowania tabeli z tabeli tymczasowej, konieczne będzie wstawiania danych do tabeli partycjonowanej:</span><span class="sxs-lookup"><span data-stu-id="36522-161">Since we have already created the partitioning table from the staging table, all we need to do is insert data to the partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="36522-162">Aby uzyskać więcej informacji, zobacz [partycjonowane tabele](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="36522-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-the-orcfile-format"></a><span data-ttu-id="36522-163">Użyj formatu ORCFile</span><span class="sxs-lookup"><span data-stu-id="36522-163">Use the ORCFile format</span></span>
<span data-ttu-id="36522-164">Hive obsługuje różnych formatach plików.</span><span class="sxs-lookup"><span data-stu-id="36522-164">Hive supports different file formats.</span></span> <span data-ttu-id="36522-165">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36522-165">For example:</span></span>

* <span data-ttu-id="36522-166">**Tekst**: to jest domyślny format pliku i współdziała z większości scenariuszy</span><span class="sxs-lookup"><span data-stu-id="36522-166">**Text**: this is the default file format and works with most scenarios</span></span>
* <span data-ttu-id="36522-167">**Avro**: sprawdza się w przypadku scenariuszy współdziałanie</span><span class="sxs-lookup"><span data-stu-id="36522-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="36522-168">**ORC/Parquet**: najbardziej odpowiednie dla wydajności</span><span class="sxs-lookup"><span data-stu-id="36522-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="36522-169">Format ORC (zoptymalizowanych pod kątem wiersza kolumnowy) jest bardzo wydajny sposób przechowywania danych Hive.</span><span class="sxs-lookup"><span data-stu-id="36522-169">ORC (Optimized Row Columnar) format is a highly efficient way to store Hive data.</span></span> <span data-ttu-id="36522-170">W porównaniu do innych formatów ORC ma następujące zalety:</span><span class="sxs-lookup"><span data-stu-id="36522-170">Compared to other formats, ORC has the following advantages:</span></span>

* <span data-ttu-id="36522-171">Obsługa typów złożonych tym DateTime i typy złożone i częściowo ustrukturyzowanych</span><span class="sxs-lookup"><span data-stu-id="36522-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="36522-172">maksymalnie 70% kompresji</span><span class="sxs-lookup"><span data-stu-id="36522-172">up to 70% compression</span></span>
* <span data-ttu-id="36522-173">indeksy co 10 000 wierszy, co umożliwia pomijanie wierszy</span><span class="sxs-lookup"><span data-stu-id="36522-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="36522-174">znaczny spadek wykonywania środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="36522-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="36522-175">Aby włączyć ORC format, należy najpierw utworzyć tabelę z klauzulą *przechowywane jako ORC*:</span><span class="sxs-lookup"><span data-stu-id="36522-175">To enable ORC format, you first create a table with the clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="36522-176">Następnie możesz wstawiania danych do tabeli ORC z tabeli tymczasowej.</span><span class="sxs-lookup"><span data-stu-id="36522-176">Next, you insert data to the ORC table from the staging table.</span></span> <span data-ttu-id="36522-177">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36522-177">For example:</span></span>

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

<span data-ttu-id="36522-178">Więcej na temat formatu ORC [tutaj](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="36522-178">You can read more on the ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="36522-179">Vectorization</span><span class="sxs-lookup"><span data-stu-id="36522-179">Vectorization</span></span>

<span data-ttu-id="36522-180">Vectorization umożliwia Hive można przetworzyć partii wierszy 1024 razem zamiast przetwarzania jeden wiersz jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="36522-180">Vectorization allows Hive to process a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="36522-181">Oznacza to, że proste operacje są wykonywane szybciej ponieważ mniej wewnętrzny kod musi być uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="36522-181">It means that simple operations are done faster because less internal code needs to run.</span></span>

<span data-ttu-id="36522-182">Aby włączyć vectorization prefiksu zapytanie Hive z następującymi ustawieniami:</span><span class="sxs-lookup"><span data-stu-id="36522-182">To enable vectorization prefix your Hive query with the following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="36522-183">Aby uzyskać więcej informacji, zobacz [Przekształcono wykonywania zapytania](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="36522-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="36522-184">Inne metody optymalizacji</span><span class="sxs-lookup"><span data-stu-id="36522-184">Other optimization methods</span></span>
<span data-ttu-id="36522-185">Dostępnych jest więcej metod optymalizacji można rozważyć, na przykład:</span><span class="sxs-lookup"><span data-stu-id="36522-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="36522-186">**Gałąź rejestru bucketing:** technika, która umożliwia klastra lub segment dużych zestawów danych w celu zoptymalizowania wydajności zapytania.</span><span class="sxs-lookup"><span data-stu-id="36522-186">**Hive bucketing:** a technique that allows to cluster or segment large sets of data to optimize query performance.</span></span>
* <span data-ttu-id="36522-187">**Dołącz do optymalizacji:** optymalizacji wykonywania zapytania gałęzi planowania podnieść wydajność sprzężenia i zmniejsza potrzebę wskazówek użytkownika.</span><span class="sxs-lookup"><span data-stu-id="36522-187">**Join optimization:** optimization of Hive's query execution planning to improve the efficiency of joins and reduce the need for user hints.</span></span> <span data-ttu-id="36522-188">Aby uzyskać więcej informacji, zobacz [Join optymalizacji](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="36522-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="36522-189">**Zwiększ reduktory**.</span><span class="sxs-lookup"><span data-stu-id="36522-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36522-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36522-190">Next steps</span></span>
<span data-ttu-id="36522-191">W tym artykule uzyskanych kilka typowych metody optymalizacji zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="36522-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="36522-192">Aby dowiedzieć się więcej, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="36522-192">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="36522-193">Use Apache Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="36522-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="36522-194">Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="36522-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="36522-195">Analizowanie danych Twitter przy użyciu Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="36522-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="36522-196">Analizowanie danych czujnika przy użyciu konsoli zapytania Hive na platformie Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="36522-196">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="36522-197">Korzystanie z programu Hive z usługą HDInsight do analizy dzienników witryn sieci Web</span><span class="sxs-lookup"><span data-stu-id="36522-197">Use Hive with HDInsight to analyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
