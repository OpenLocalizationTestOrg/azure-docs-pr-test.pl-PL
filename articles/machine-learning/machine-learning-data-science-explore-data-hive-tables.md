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
# <a name="explore-data-in-hive-tables-with-hive-queries"></a>Eksplorowanie danych tabel programu Hive za pomocą zapytań Hive
Ten dokument zawiera przykładowe skrypty Hive dane tooexplore używane w tabelach gałęzi w klastrze usługi HDInsight Hadoop.

następujące Hello **menu** łączy tootopics opisujące, jak toouse narzędzia tooexplore danych z różnych środowiskach magazynu.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że masz:

* Utworzone konto magazynu platformy Azure. Aby uzyskać instrukcje, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Zainicjowano obsługę administracyjną dostosowane klastra usługi Hadoop z hello usługi HDInsight. Aby uzyskać instrukcje, zobacz [dostosować Azure klastrów usługi HDInsight Hadoop zaawansowane analizy](machine-learning-data-science-customize-hadoop-cluster.md).
* Witaj dane zostały przekazane tooHive tabel w klastrach usługi Azure HDInsight Hadoop. Jeśli nie, postępuj zgodnie z instrukcjami hello [tworzenie i obciążenia tabel tooHive danych](machine-learning-data-science-move-hive-tables.md) tooHive danych tooupload najpierw tabel.
* Włączono klaster toohello dostępu zdalnego. Aby uzyskać instrukcje, zobacz [hello dostępu Head węzeł z klastra usługi Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).
* Aby uzyskać instrukcje na temat toosubmit zapytań programu Hive, zobacz [jak tooSubmit zapytań Hive](machine-learning-data-science-move-hive-tables.md#submit)

## <a name="example-hive-query-scripts-for-data-exploration"></a>Przykładowe skrypty służące zapytania Hive do Eksploracja danych
1. Zliczanie hello uwagi dla każdej partycji`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`
2. Zliczanie hello uwagi na dzień`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`
3. Pobierz poziomy hello w kolumnie podzielone na kategorie  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. Pobierz hello podaną liczbę poziomów w połączeniu z dwóch kolumn podzielone na kategorie`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`
5. Pobierz dystrybucji hello kolumn wartości liczbowych  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. Wyodrębnij rekordy z Sprzęganie dwóch tabel
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a>Skrypty zapytania dodatkowe scenariusze danych podróży taksówki
Przykłady zapytań, które są określone za[danych podróży taksówki NYC](http://chriswhong.com/open-data/foil_nyc_taxi/) scenariuszy znajdują się również w [repozytorium GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Te zapytania już mieć określony schemat danych i są gotowe toobe przesłane toorun.

