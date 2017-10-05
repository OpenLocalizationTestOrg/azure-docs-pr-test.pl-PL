---
title: "Tworzenie funkcji danych klastra platformy Hadoop za pomocą zapytań Hive | Dokumentacja firmy Microsoft"
description: "Przykłady zapytań Hive, które generują funkcje w danych przechowywanych w klastrze usługi Azure HDInsight Hadoop."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e027a6ffcb63868be13432870e484c5cbf2eef4b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="0fd9c-103">Tworzenie funkcji dla danych w klastrze usługi Hadoop przy użyciu zapytań Hive</span><span class="sxs-lookup"><span data-stu-id="0fd9c-103">Create features for data in an Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="0fd9c-104">Ten dokument przedstawia sposób tworzenia funkcji danych przechowywanych w klastrze usługi Azure HDInsight Hadoop za pomocą zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-104">This document shows how to create features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="0fd9c-105">Te zapytania Hive Użyj osadzonych Hive funkcje zdefiniowane przez użytkownika (UDF), skryptów, dla której są dostarczane.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-105">These Hive queries use embedded Hive User Defined Functions (UDFs), the scripts for which are provided.</span></span>

<span data-ttu-id="0fd9c-106">Operacje potrzebne do utworzenia funkcje mogą być pamięci.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-106">The operations needed to create features can be memory intensive.</span></span> <span data-ttu-id="0fd9c-107">Wydajność zapytań programu Hive staje się ważniejsze w takich przypadkach i można zwiększyć przez dostrajanie określonych parametrów.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-107">The performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="0fd9c-108">Dostrajanie parametrów została szczegółowo opisana w sekcji końcowego.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-108">The tuning of these parameters is discussed in the final section.</span></span>

<span data-ttu-id="0fd9c-109">Przykłady zapytań, które są przedstawiane są specyficzne dla [danych podróży taksówki NYC](http://chriswhong.com/open-data/foil_nyc_taxi/) scenariuszy znajdują się również w [repozytorium GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="0fd9c-109">Examples of the queries that are presented are specific to the [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="0fd9c-110">Te zapytania już mieć określony schemat danych i jest gotowe do przesłania do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-110">These queries already have data schema specified and are ready to be submitted to run.</span></span> <span data-ttu-id="0fd9c-111">W końcowej sekcji omówiono również parametry, które użytkownicy można dostosować tak, aby ulepszyć wydajność zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-111">In the final section, parameters that users can tune so that the performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="0fd9c-112">To **menu** linki do tematów opisujących sposób tworzenia funkcji dla danych w różnych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-112">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="0fd9c-113">To zadanie jest krokiem w [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="0fd9c-113">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fd9c-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0fd9c-114">Prerequisites</span></span>
<span data-ttu-id="0fd9c-115">W tym artykule przyjęto założenie, że masz:</span><span class="sxs-lookup"><span data-stu-id="0fd9c-115">This article assumes that you have:</span></span>

* <span data-ttu-id="0fd9c-116">Utworzone konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-116">Created an Azure storage account.</span></span> <span data-ttu-id="0fd9c-117">Aby uzyskać instrukcje, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="0fd9c-117">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="0fd9c-118">Zainicjowano obsługę administracyjną dostosowane klastra usługi Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-118">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span>  <span data-ttu-id="0fd9c-119">Aby uzyskać instrukcje, zobacz [dostosować Azure klastrów usługi HDInsight Hadoop zaawansowane analizy](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="0fd9c-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="0fd9c-120">Dane przekazane do tabele programu Hive w klastrach usługi Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-120">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="0fd9c-121">Jeśli nie, wykonaj [tworzenie i ładowanie danych do tabel Hive](machine-learning-data-science-move-hive-tables.md) najpierw przekazywać dane do tabele programu Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-121">If it has not, please follow [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="0fd9c-122">Włączyć dostęp zdalny do klastra.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-122">Enabled remote access to the cluster.</span></span> <span data-ttu-id="0fd9c-123">Aby uzyskać instrukcje, zobacz [dostęp węzła Head klastra usługi Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="0fd9c-123">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <span data-ttu-id="0fd9c-124"><a name="hive-featureengineering"></a>Funkcja generowania</span><span class="sxs-lookup"><span data-stu-id="0fd9c-124"><a name="hive-featureengineering"></a>Feature Generation</span></span>
<span data-ttu-id="0fd9c-125">W tej sekcji opisano kilka przykładów sposoby, w którym można generowania funkcji za pomocą zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-125">In this section, several examples of the ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="0fd9c-126">Po wygenerowaniu dodatkowe funkcje, możesz dodać je jako kolumny do istniejącej tabeli lub Utwórz nową tabelę z dodatkowych funkcji i klucza podstawowego, który następnie może być połączony z oryginalnej tabeli.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-126">Once you have generated additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, which can then be joined with the original table.</span></span> <span data-ttu-id="0fd9c-127">Poniżej przedstawiono w przykładach przedstawionych:</span><span class="sxs-lookup"><span data-stu-id="0fd9c-127">Here are the examples presented:</span></span>

1. [<span data-ttu-id="0fd9c-128">Funkcja generowania na podstawie częstotliwości</span><span class="sxs-lookup"><span data-stu-id="0fd9c-128">Frequency based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="0fd9c-129">Ryzyko podzielone na kategorie zmiennych w klasyfikacji binarnej</span><span class="sxs-lookup"><span data-stu-id="0fd9c-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="0fd9c-130">Wyodrębnij funkcji z pola daty/godziny</span><span class="sxs-lookup"><span data-stu-id="0fd9c-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="0fd9c-131">Wyodrębnij funkcji z pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="0fd9c-132">Oblicz odległość między współrzędne GPS</span><span class="sxs-lookup"><span data-stu-id="0fd9c-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <span data-ttu-id="0fd9c-133"><a name="hive-frequencyfeature"></a>Funkcja generowania na podstawie częstotliwości</span><span class="sxs-lookup"><span data-stu-id="0fd9c-133"><a name="hive-frequencyfeature"></a>Frequency based Feature Generation</span></span>
<span data-ttu-id="0fd9c-134">Często jest przydatne do obliczania częstotliwości poziomów podzielone na kategorie zmiennej lub częstotliwości niektórych kombinacji poziomy wiele zmiennych podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-134">It is often useful to calculate the frequencies of the levels of a categorical variable, or the frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="0fd9c-135">Użytkownicy mogą używać poniższy skrypt, aby obliczyć częstotliwości te:</span><span class="sxs-lookup"><span data-stu-id="0fd9c-135">Users can use the following script to calculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <span data-ttu-id="0fd9c-136"><a name="hive-riskfeature"></a>Ryzyko podzielone na kategorie zmiennych w klasyfikacji binarnej</span><span class="sxs-lookup"><span data-stu-id="0fd9c-136"><a name="hive-riskfeature"></a>Risks of Categorical Variables in Binary Classification</span></span>
<span data-ttu-id="0fd9c-137">W klasyfikacji binarnej musimy przekształcania nieliczbowy podzielone na kategorie zmiennych w funkcje numeryczne modeli używany tylko zająć funkcje numeryczne.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-137">In binary classification, we need to convert non-numeric categorical variables into numeric features when the models being used only take numeric features.</span></span> <span data-ttu-id="0fd9c-138">Jest to realizowane przez zamianę każdy poziom nieliczbowy zagrożenie liczbowych.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-138">This is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="0fd9c-139">W tej sekcji zostanie przedstawiony niektórych ogólnego zapytań Hive, które obliczania wartości ryzyka (dziennika prawdopodobieństwo) podzielone na kategorie zmiennej.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-139">In this section, we show some generic Hive queries that calculate the risk values (log odds) of a categorical variable.</span></span>

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

<span data-ttu-id="0fd9c-140">W tym przykładzie zmienne `smooth_param1` i `smooth_param2` ustawioną smooth wartości ryzyka obliczana na podstawie danych.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-140">In this example, variables `smooth_param1` and `smooth_param2` are set to smooth the risk values calculated from the data.</span></span> <span data-ttu-id="0fd9c-141">Ryzyko ma zakresie -Inf Inf.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="0fd9c-142">Zagrożenia > 0 wskazuje, że prawdopodobieństwo, że element docelowy jest równa 1, jest większa niż 0,5.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-142">A risks > 0 indicates that the probability that the target is equal to 1 is greater than 0.5.</span></span>

<span data-ttu-id="0fd9c-143">Po ryzyko jest obliczana tabeli, użytkownicy mogą przypisywać wartości ryzyka do tabeli przez dołączenie go do tabeli ryzyka.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-143">After the risk table is calculated, users can assign risk values to a table by joining it with the risk table.</span></span> <span data-ttu-id="0fd9c-144">Zapytanie łącząca Hive została dostarczona w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-144">The Hive joining query was provided in previous section.</span></span>

### <span data-ttu-id="0fd9c-145"><a name="hive-datefeatures"></a>Wyodrębnij funkcji z pól daty i godziny</span><span class="sxs-lookup"><span data-stu-id="0fd9c-145"><a name="hive-datefeatures"></a>Extract features from Datetime Fields</span></span>
<span data-ttu-id="0fd9c-146">Gałąź jest dostarczany z zestawem funkcji UDF przetwarzania pól daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="0fd9c-147">W gałęzi, domyślny format daty/godziny jest "RRRR MM-dd 00:00:00" ("1970-01-01-12:21:32" na przykład).</span><span class="sxs-lookup"><span data-stu-id="0fd9c-147">In Hive, the default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="0fd9c-148">W tej sekcji zostanie przedstawiony przykłady, które wyodrębnianie dnia miesiąca, miesiąc z polem datetime i inne przykłady, które konwertowanie ciągu daty i godziny w formacie innym niż domyślny format ciąg daty i godziny w domyślnym formacie.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-148">In this section, we show examples that extract the day of a month, the month from a datetime field, and other examples that convert a datetime string in a format other than the default format to a datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="0fd9c-149">To zapytanie Hive przy założeniu, że *&#60; pole Data i godzina >* jest w formacie daty/godziny domyślne.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-149">This Hive query assumes that the *&#60;datetime field>* is in the default datetime format.</span></span>

<span data-ttu-id="0fd9c-150">Pole daty i godziny nie ma domyślnego formatu, należy najpierw przekonwertuj pole daty/godziny na sygnatury czasowej systemu Unix, a następnie wykonać konwersję sygnaturę czasową Unix ciąg daty i godziny w formacie domyślne.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-150">If a datetime field is not in the default format, you need to convert the datetime field into Unix time stamp first, and then convert the Unix time stamp to a datetime string that is in the default format.</span></span> <span data-ttu-id="0fd9c-151">W przypadku datę i godzinę w domyślnym formacie, użytkownicy mogą stosować osadzonych funkcji UDF, aby wyodrębnić funkcji daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-151">When the datetime is in default format, users can apply the embedded datetime UDFs to extract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of the datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="0fd9c-152">W tym zapytaniu Jeśli *&#60; pole daty/godziny >* ma wzorzec, takich jak *2015-03-26 12:04:39*, *"&#60; wzorzec pola datetime >"* powinien być `'MM/dd/yyyy HH:mm:ss'`.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-152">In this query, if the *&#60;datetime field>* has the pattern like *03/26/2015 12:04:39*, the *'&#60;pattern of the datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="0fd9c-153">Aby ją przetestować, użytkownicy mogą uruchamiać</span><span class="sxs-lookup"><span data-stu-id="0fd9c-153">To test it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="0fd9c-154">*Hivesampletable* w tym zapytaniu preinstalowane na wszystkich klastrach Azure HDInsight Hadoop domyślnie podczas przydzielania klastrów.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-154">The *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when the clusters are provisioned.</span></span>

### <span data-ttu-id="0fd9c-155"><a name="hive-textfeatures"></a>Wyodrębnij funkcji z pola tekstowe</span><span class="sxs-lookup"><span data-stu-id="0fd9c-155"><a name="hive-textfeatures"></a>Extract features from Text Fields</span></span>
<span data-ttu-id="0fd9c-156">Jeśli w tabeli Hive pola tekstowego, który zawiera ciąg słowa, które są rozdzielone spacjami, następujące zapytanie wyodrębnia długość ciągu i liczbę słów w ciągu.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-156">When the Hive table has a text field that contains a string of words that are delimited by spaces, the following query extracts the length of the string, and the number of words in the string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <span data-ttu-id="0fd9c-157"><a name="hive-gpsdistance"></a>Obliczanie odległości między zestawami współrzędne GPS</span><span class="sxs-lookup"><span data-stu-id="0fd9c-157"><a name="hive-gpsdistance"></a>Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="0fd9c-158">Zapytanie podane w tej sekcji można bezpośrednio odnosić się do danych podróży taksówki NYC.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-158">The query given in this section can be directly applied to the NYC Taxi Trip Data.</span></span> <span data-ttu-id="0fd9c-159">To zapytanie ma na celu pokazują, jak zastosować osadzonych funkcji matematycznych w gałęzi do generowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-159">The purpose of this query is to show how to apply an embedded mathematical functions in Hive to generate features.</span></span>

<span data-ttu-id="0fd9c-160">Pola, które są używane w tym zapytaniu są współrzędne GPS odbiór i dropoff lokalizacji o nazwie *podnoszenia\_geograficzne*, *podnoszenia\_szerokości geograficznej*,  *dropoff\_geograficzne*, i *dropoff\_szerokości geograficznej*.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-160">The fields that are used in this query are the GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="0fd9c-161">Zapytania obliczające bezpośrednie odległość między współrzędne odbiór i dropoff są:</span><span class="sxs-lookup"><span data-stu-id="0fd9c-161">The queries that calculate the direct distance between the pickup and dropoff coordinates are:</span></span>

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

<span data-ttu-id="0fd9c-162">Równania matematyczne, które obliczyć odległość między dwoma współrzędne GPS można znaleźć w <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">skryptów typu ruchome</a> lokacji utworzone przez Lapisu Peterowi.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-162">The mathematical equations that calculate the distance between two GPS coordinates can be found on the <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="0fd9c-163">W języku Javascript, jego funkcji `toRad()` jest po prostu *lat_or_lon*pi/180 *, który Konwertuje stopnie na radiany.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-163">In his Javascript, the function `toRad()` is just *lat_or_lon*pi/180*, which converts degrees to radians.</span></span> <span data-ttu-id="0fd9c-164">W tym miejscu *lat_or_lon* jest zakres lub długość geograficzną.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-164">Here, *lat_or_lon* is the latitude or longitude.</span></span> <span data-ttu-id="0fd9c-165">Ponieważ gałąź nie zawiera funkcji `atan2`, ale udostępnia funkcję `atan`, `atan2` funkcji jest implementowany przez `atan` funkcji w powyższym zapytaniu gałęzi przy użyciu definicji w <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-165">Since Hive does not provide the function `atan2`, but provides the function `atan`, the `atan2` function is implemented by `atan` function in the above Hive query using the definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-create-features-hive/atan2new.png)

<span data-ttu-id="0fd9c-167">Pełną listę gałęzi funkcji UDF embedded znajdują się w **wbudowanych funkcji** sekcji na <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span><span class="sxs-lookup"><span data-stu-id="0fd9c-167">A full list of Hive embedded UDFs can be found in the **Built-in Functions** section on the <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <span data-ttu-id="0fd9c-168"><a name="tuning"></a>Tematy zaawansowane: parametry Hive strojenia poprawy szybkości zapytania</span><span class="sxs-lookup"><span data-stu-id="0fd9c-168"><a name="tuning"></a> Advanced topics: Tune Hive Parameters to Improve Query Speed</span></span>
<span data-ttu-id="0fd9c-169">Domyślne ustawienia parametru gałęzi klastra może nie być odpowiednie dla zapytań Hive i dane, które są przetwarzania zapytania.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-169">The default parameter settings of Hive cluster might not be suitable for the Hive queries and the data that the queries are processing.</span></span> <span data-ttu-id="0fd9c-170">W tej sekcji omówiono niektóre parametry, które użytkownicy mogą dostosować które poprawić wydajność zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-170">In this section, we discuss some parameters that users can tune that improve the performance of Hive queries.</span></span> <span data-ttu-id="0fd9c-171">Użytkownicy muszą dodać parametr strojenia kwerendy przed zapytania przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-171">Users need to add the parameter tuning queries before the queries of processing data.</span></span>

1. <span data-ttu-id="0fd9c-172">**Miejsce na stercie Java**: dla zapytań obejmujących dołączenie dużych zestawów danych lub przetwarzania rekordów długi **kończy się wolne miejsce na stercie** jest jednym z typowych błędów.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of the common error.</span></span> <span data-ttu-id="0fd9c-173">Można to dostroić przez ustawienie parametrów *mapreduce.map.java.opts* i *mapreduce.task.io.sort.mb* do żądanej wartości.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-173">This can be tuned by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* to desired values.</span></span> <span data-ttu-id="0fd9c-174">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="0fd9c-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="0fd9c-175">Ten parametr przydziela 4GB pamięci, aby miejsce na stercie Java i powoduje sortowanie efektywniejsze przez przydzielanie większej ilości pamięci.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-175">This parameter allocates 4GB memory to Java heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="0fd9c-176">Należy dobrze gry z tych przydziałów, jeśli istnieją wszystkie zadania błędy związane z miejsca na stercie.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-176">It is a good idea to play with these allocations if there are any job failure errors related to heap space.</span></span>

1. <span data-ttu-id="0fd9c-177">**Rozmiaru bloku systemu plików DFS** : ten parametr określa najmniejsza jednostka danych przechowywanych w systemie plików.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-177">**DFS block size** : This parameter sets the smallest unit of data that the file system stores.</span></span> <span data-ttu-id="0fd9c-178">Na przykład jeśli rozmiar bloku systemu plików DFS jest 128MB, a następnie żadnych danych o rozmiarze mniejsza i maksymalnie 128MB są przechowywane w jeden blok danych, który jest większy niż 128MB przydzielony dodatkowe bloki.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-178">As an example, if the DFS block size is 128MB, then any data of size less than and up to 128MB is stored in a single block, while data that is larger than 128MB is allotted extra blocks.</span></span> <span data-ttu-id="0fd9c-179">Wybieranie rozmiaru bloku bardzo małych powoduje duże koszty Hadoop, ponieważ nazwa węzła ma przetwarzać wiele żądań więcej można znaleźć odpowiedniego bloku odnoszące się do pliku.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-179">Choosing a very small block size causes large overheads in Hadoop since the name node has to process many more requests to find the relevant block pertaining to the file.</span></span> <span data-ttu-id="0fd9c-180">Zalecane ustawienia po dotyczących gigabajty (lub więcej) danych jest:</span><span class="sxs-lookup"><span data-stu-id="0fd9c-180">A recommended setting when dealing with gigabytes (or larger) data is :</span></span>
   
        set dfs.block.size=128m;
2. <span data-ttu-id="0fd9c-181">**Optymalizacja operacji tworzenia sprzężenia w gałęzi** : podczas operacji łączenia w ramach mapy/Zmniejsz zazwyczaj miejsce w fazie Zmniejsz czasami znaczne zyski można osiągnąć poprzez zaplanowanie sprzężenia w fazie mapy (zwane również "mapjoins").</span><span class="sxs-lookup"><span data-stu-id="0fd9c-181">**Optimizing join operation in Hive** : While join operations in the map/reduce framework typically take place in the reduce phase, sometimes, enormous gains can be achieved by scheduling joins in the map phase (also called "mapjoins").</span></span> <span data-ttu-id="0fd9c-182">Aby skierować gałąź, aby to zrobić, jeśli to możliwe, możemy ustawić:</span><span class="sxs-lookup"><span data-stu-id="0fd9c-182">To direct Hive to do this whenever possible, we can set :</span></span>
   
        set hive.auto.convert.join=true;
3. <span data-ttu-id="0fd9c-183">**Określanie liczby mapowań do gałęzi** : podczas Hadoop zezwala użytkownikowi na określenie liczby reduktory, liczba mapowań jest zwykle nie jest ustawiony przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-183">**Specifying the number of mappers to Hive** : While Hadoop allows the user to set the number of reducers, the number of mappers is typically not be set by the user.</span></span> <span data-ttu-id="0fd9c-184">Lewy, umożliwiający pewien stopień kontroli tego numeru jest wybranie zmienne Hadoop *mapred.min.split.size* i *mapred.max.split.size* jako rozmiar map zadań zależy od:</span><span class="sxs-lookup"><span data-stu-id="0fd9c-184">A trick that allows some degree of control on this number is to choose the Hadoop variables, *mapred.min.split.size* and *mapred.max.split.size* as the size of each map task is determined by :</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="0fd9c-185">Zazwyczaj wartość domyślną *mapred.min.split.size* ma wartość 0, z *mapred.max.split.size* jest **Long.MAX** i *dfs.block.size* to 64MB.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-185">Typically, the default value of *mapred.min.split.size* is 0, that of *mapred.max.split.size* is **Long.MAX** and that of *dfs.block.size* is 64MB.</span></span> <span data-ttu-id="0fd9c-186">Jak możemy stwierdzić, podany rozmiar danych dostrajanie parametrów "ustawienia" ich pozwala nam dostosować liczbę mapowań używane.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-186">As we can see, given the data size, tuning these parameters by "setting" them allows us to tune the number of mappers used.</span></span>
4. <span data-ttu-id="0fd9c-187">Kilka innych kolejnych **zaawansowane opcje** Hive optymalizacji wydajności są wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-187">A few other more **advanced options** for optimizing Hive performance are mentioned below.</span></span> <span data-ttu-id="0fd9c-188">Te umożliwiają skonfigurowanie pamięć przydzielona do mapowania i zmniejszyć zadań i mogą być przydatne w Dostosowywanie wydajności.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-188">These allow you to set the memory allocated to map and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="0fd9c-189">Sprawdź należy pamiętać, że *mapreduce.reduce.memory.mb* nie może być większa niż rozmiar pamięci fizycznej w każdym węźle procesu roboczego klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0fd9c-189">Please keep in mind that the *mapreduce.reduce.memory.mb* cannot be greater than the physical memory size of each worker node in the Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

