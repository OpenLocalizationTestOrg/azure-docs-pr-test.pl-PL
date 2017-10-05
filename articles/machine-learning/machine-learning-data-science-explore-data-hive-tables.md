---
title: "Eksploruj dane w tabelach gałąź z zapytań programu Hive | Dokumentacja firmy Microsoft"
description: "Eksploruj dane w tabelach Hive za pomocą zapytań Hive."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 67a33a9abc3d3dcdd2fc7205e11feff97e3582a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="03298-103">Eksplorowanie danych tabel programu Hive za pomocą zapytań Hive</span><span class="sxs-lookup"><span data-stu-id="03298-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="03298-104">Ten dokument zawiera przykładowe skrypty Hive, które są używane, aby eksplorować dane w tabelach gałęzi w klastrze usługi HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="03298-104">This document provides sample Hive scripts that are used to explore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="03298-105">Następujące **menu** linki do tematów opisujących sposób użycia narzędzia, aby eksplorować dane w różnych środowiskach magazynu.</span><span class="sxs-lookup"><span data-stu-id="03298-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="03298-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="03298-106">Prerequisites</span></span>
<span data-ttu-id="03298-107">W tym artykule przyjęto założenie, że masz:</span><span class="sxs-lookup"><span data-stu-id="03298-107">This article assumes that you have:</span></span>

* <span data-ttu-id="03298-108">Utworzone konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="03298-108">Created an Azure storage account.</span></span> <span data-ttu-id="03298-109">Aby uzyskać instrukcje, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="03298-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="03298-110">Zainicjowano obsługę administracyjną dostosowane klastra usługi Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="03298-110">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span> <span data-ttu-id="03298-111">Aby uzyskać instrukcje, zobacz [dostosować Azure klastrów usługi HDInsight Hadoop zaawansowane analizy](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="03298-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="03298-112">Dane przekazane do tabele programu Hive w klastrach usługi Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="03298-112">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="03298-113">Jeśli nie, postępuj zgodnie z instrukcjami [tworzenie i ładowanie danych do tabel Hive](machine-learning-data-science-move-hive-tables.md) najpierw przekazywać dane do tabele programu Hive.</span><span class="sxs-lookup"><span data-stu-id="03298-113">If it has not, follow the instructions in [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="03298-114">Włączyć dostęp zdalny do klastra.</span><span class="sxs-lookup"><span data-stu-id="03298-114">Enabled remote access to the cluster.</span></span> <span data-ttu-id="03298-115">Aby uzyskać instrukcje, zobacz [dostęp węzła Head klastra usługi Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="03298-115">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="03298-116">Aby uzyskać instrukcje dotyczące sposobu przesyłania zapytań programu Hive, zobacz [sposobu przesyłania zapytań Hive](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="03298-116">If you need instructions on how to submit Hive queries, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="03298-117">Przykładowe skrypty służące zapytania Hive do Eksploracja danych</span><span class="sxs-lookup"><span data-stu-id="03298-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="03298-118">Zliczanie uwagi dla każdej partycji`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="03298-118">Get the count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="03298-119">Zliczanie uwagi na dzień`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="03298-119">Get the count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="03298-120">Pobierz poziomy w kolumnie podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="03298-120">Get the levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="03298-121">Pobierz liczbę poziomów w połączeniu z dwóch kolumn podzielone na kategorie`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="03298-121">Get the number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="03298-122">Pobierz dystrybucji dla kolumn wartości liczbowych</span><span class="sxs-lookup"><span data-stu-id="03298-122">Get the distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="03298-123">Wyodrębnij rekordy z Sprzęganie dwóch tabel</span><span class="sxs-lookup"><span data-stu-id="03298-123">Extract records from joining two tables</span></span>
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="03298-124">Skrypty zapytania dodatkowe scenariusze danych podróży taksówki</span><span class="sxs-lookup"><span data-stu-id="03298-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="03298-125">Przykłady zapytań, które są specyficzne dla [danych podróży taksówki NYC](http://chriswhong.com/open-data/foil_nyc_taxi/) scenariuszy znajdują się również w [repozytorium GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="03298-125">Examples of queries that are specific to [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="03298-126">Te zapytania już mieć określony schemat danych i jest gotowe do przesłania do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="03298-126">These queries already have data schema specified and are ready to be submitted to run.</span></span>

