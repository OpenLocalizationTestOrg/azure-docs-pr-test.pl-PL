---
title: "dane aaaExplore w tabele programu Hive z zapytań programu Hive | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="ba2e1-103">Eksplorowanie danych tabel programu Hive za pomocą zapytań Hive</span><span class="sxs-lookup"><span data-stu-id="ba2e1-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="ba2e1-104">Ten dokument zawiera przykładowe skrypty Hive dane tooexplore używane w tabelach gałęzi w klastrze usługi HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="ba2e1-104">This document provides sample Hive scripts that are used tooexplore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="ba2e1-105">następujące Hello **menu** łączy tootopics opisujące, jak toouse narzędzia tooexplore danych z różnych środowiskach magazynu.</span><span class="sxs-lookup"><span data-stu-id="ba2e1-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="ba2e1-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ba2e1-106">Prerequisites</span></span>
<span data-ttu-id="ba2e1-107">W tym artykule przyjęto założenie, że masz:</span><span class="sxs-lookup"><span data-stu-id="ba2e1-107">This article assumes that you have:</span></span>

* <span data-ttu-id="ba2e1-108">Utworzone konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ba2e1-108">Created an Azure storage account.</span></span> <span data-ttu-id="ba2e1-109">Aby uzyskać instrukcje, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="ba2e1-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="ba2e1-110">Zainicjowano obsługę administracyjną dostosowane klastra usługi Hadoop z hello usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ba2e1-110">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span> <span data-ttu-id="ba2e1-111">Aby uzyskać instrukcje, zobacz [dostosować Azure klastrów usługi HDInsight Hadoop zaawansowane analizy](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ba2e1-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="ba2e1-112">Witaj dane zostały przekazane tooHive tabel w klastrach usługi Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="ba2e1-112">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="ba2e1-113">Jeśli nie, postępuj zgodnie z instrukcjami hello [tworzenie i obciążenia tabel tooHive danych](machine-learning-data-science-move-hive-tables.md) tooHive danych tooupload najpierw tabel.</span><span class="sxs-lookup"><span data-stu-id="ba2e1-113">If it has not, follow hello instructions in [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="ba2e1-114">Włączono klaster toohello dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="ba2e1-114">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="ba2e1-115">Aby uzyskać instrukcje, zobacz [hello dostępu Head węzeł z klastra usługi Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="ba2e1-115">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="ba2e1-116">Aby uzyskać instrukcje na temat toosubmit zapytań programu Hive, zobacz [jak tooSubmit zapytań Hive](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="ba2e1-116">If you need instructions on how toosubmit Hive queries, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="ba2e1-117">Przykładowe skrypty służące zapytania Hive do Eksploracja danych</span><span class="sxs-lookup"><span data-stu-id="ba2e1-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="ba2e1-118">Zliczanie hello uwagi dla każdej partycji`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="ba2e1-118">Get hello count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="ba2e1-119">Zliczanie hello uwagi na dzień`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="ba2e1-119">Get hello count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="ba2e1-120">Pobierz poziomy hello w kolumnie podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="ba2e1-120">Get hello levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="ba2e1-121">Pobierz hello podaną liczbę poziomów w połączeniu z dwóch kolumn podzielone na kategorie`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="ba2e1-121">Get hello number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="ba2e1-122">Pobierz dystrybucji hello kolumn wartości liczbowych</span><span class="sxs-lookup"><span data-stu-id="ba2e1-122">Get hello distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="ba2e1-123">Wyodrębnij rekordy z Sprzęganie dwóch tabel</span><span class="sxs-lookup"><span data-stu-id="ba2e1-123">Extract records from joining two tables</span></span>
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="ba2e1-124">Skrypty zapytania dodatkowe scenariusze danych podróży taksówki</span><span class="sxs-lookup"><span data-stu-id="ba2e1-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="ba2e1-125">Przykłady zapytań, które są określone za[danych podróży taksówki NYC](http://chriswhong.com/open-data/foil_nyc_taxi/) scenariuszy znajdują się również w [repozytorium GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="ba2e1-125">Examples of queries that are specific too[NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="ba2e1-126">Te zapytania już mieć określony schemat danych i są gotowe toobe przesłane toorun.</span><span class="sxs-lookup"><span data-stu-id="ba2e1-126">These queries already have data schema specified and are ready toobe submitted toorun.</span></span>

