---
title: "Funkcje aaaCreate danych klastra platformy Hadoop za pomocą zapytań Hive | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a><span data-ttu-id="5ffb3-103">Tworzenie funkcji dla danych w klastrze usługi Hadoop przy użyciu zapytań Hive</span><span class="sxs-lookup"><span data-stu-id="5ffb3-103">Create features for data in an Hadoop cluster using Hive queries</span></span>
<span data-ttu-id="5ffb3-104">Ten dokument przedstawia sposób przechowywania funkcje toocreate danych w klastrze usługi Azure HDInsight Hadoop za pomocą zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-104">This document shows how toocreate features for data stored in an Azure HDInsight Hadoop cluster using Hive queries.</span></span> <span data-ttu-id="5ffb3-105">Tych zapytań programu Hive użyć osadzonego Hive funkcje zdefiniowane przez użytkownika (UDF), skrypty hello, dla której są udostępniane.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-105">These Hive queries use embedded Hive User Defined Functions (UDFs), hello scripts for which are provided.</span></span>

<span data-ttu-id="5ffb3-106">Funkcje toocreate potrzebnych operacji Hello można pamięci.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-106">hello operations needed toocreate features can be memory intensive.</span></span> <span data-ttu-id="5ffb3-107">Witaj wydajność zapytań programu Hive staje się ważniejsze w takich przypadkach i można zwiększyć przez dostrajanie niektórych parametrów.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-107">hello performance of Hive queries becomes more critical in such cases and can be improved by tuning certain parameters.</span></span> <span data-ttu-id="5ffb3-108">Hello dostrajanie z tych parametrów została szczegółowo opisana w sekcji końcowego hello.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-108">hello tuning of these parameters is discussed in hello final section.</span></span>

<span data-ttu-id="5ffb3-109">Przykłady hello zapytań, które są przedstawiane są określone toohello [NYC taksówki podróży danych](http://chriswhong.com/open-data/foil_nyc_taxi/) scenariuszy znajdują się również w [repozytorium GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="5ffb3-109">Examples of hello queries that are presented are specific toohello [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="5ffb3-110">Te zapytania już mieć określony schemat danych i są gotowe toobe przesłane toorun.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-110">These queries already have data schema specified and are ready toobe submitted toorun.</span></span> <span data-ttu-id="5ffb3-111">W końcowej sekcji hello parametry, które użytkownicy można dostosować tak, aby ulepszyć wydajność zapytań programu Hive hello omówiono także.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-111">In hello final section, parameters that users can tune so that hello performance of Hive queries can be improved are  also discussed.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="5ffb3-112">To **menu** łączy tootopics, które opisują sposób toocreate funkcji dla danych w różnych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-112">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="5ffb3-113">To zadanie jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="5ffb3-113">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ffb3-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5ffb3-114">Prerequisites</span></span>
<span data-ttu-id="5ffb3-115">W tym artykule przyjęto założenie, że masz:</span><span class="sxs-lookup"><span data-stu-id="5ffb3-115">This article assumes that you have:</span></span>

* <span data-ttu-id="5ffb3-116">Utworzone konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-116">Created an Azure storage account.</span></span> <span data-ttu-id="5ffb3-117">Aby uzyskać instrukcje, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="5ffb3-117">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="5ffb3-118">Zainicjowano obsługę administracyjną dostosowane klastra usługi Hadoop z hello usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-118">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span>  <span data-ttu-id="5ffb3-119">Aby uzyskać instrukcje, zobacz [dostosować Azure klastrów usługi HDInsight Hadoop zaawansowane analizy](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5ffb3-119">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="5ffb3-120">Witaj dane zostały przekazane tooHive tabel w klastrach usługi Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-120">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="5ffb3-121">Jeśli nie, wykonaj [tworzenie i obciążenia tabel tooHive danych](machine-learning-data-science-move-hive-tables.md) tooHive danych tooupload najpierw tabel.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-121">If it has not, please follow [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="5ffb3-122">Włączono klaster toohello dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-122">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="5ffb3-123">Aby uzyskać instrukcje, zobacz [hello dostępu Head węzeł z klastra usługi Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="5ffb3-123">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

## <span data-ttu-id="5ffb3-124"><a name="hive-featureengineering"></a>Funkcja generowania</span><span class="sxs-lookup"><span data-stu-id="5ffb3-124"><a name="hive-featureengineering"></a>Feature Generation</span></span>
<span data-ttu-id="5ffb3-125">W tej sekcji opisano kilka przykładów hello sposoby, w którym można generowania funkcji za pomocą zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-125">In this section, several examples of hello ways in which features can be generating using Hive queries are described.</span></span> <span data-ttu-id="5ffb3-126">Po wygenerowaniu dodatkowe funkcje, możesz dodać je jako kolumny toohello istniejącej tabeli lub Utwórz nową tabelę z dodatkowych funkcji hello i klucza podstawowego, który następnie może być połączony z hello oryginalnej tabeli.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-126">Once you have generated additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, which can then be joined with hello original table.</span></span> <span data-ttu-id="5ffb3-127">W tym miejscu są przedstawione przykłady hello:</span><span class="sxs-lookup"><span data-stu-id="5ffb3-127">Here are hello examples presented:</span></span>

1. [<span data-ttu-id="5ffb3-128">Funkcja generowania na podstawie częstotliwości</span><span class="sxs-lookup"><span data-stu-id="5ffb3-128">Frequency based Feature Generation</span></span>](#hive-frequencyfeature)
2. [<span data-ttu-id="5ffb3-129">Ryzyko podzielone na kategorie zmiennych w klasyfikacji binarnej</span><span class="sxs-lookup"><span data-stu-id="5ffb3-129">Risks of Categorical Variables in Binary Classification</span></span>](#hive-riskfeature)
3. [<span data-ttu-id="5ffb3-130">Wyodrębnij funkcji z pola daty/godziny</span><span class="sxs-lookup"><span data-stu-id="5ffb3-130">Extract features from Datetime Field</span></span>](#hive-datefeatures)
4. [<span data-ttu-id="5ffb3-131">Wyodrębnij funkcji z pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-131">Extract features from Text Field</span></span>](#hive-textfeatures)
5. [<span data-ttu-id="5ffb3-132">Oblicz odległość między współrzędne GPS</span><span class="sxs-lookup"><span data-stu-id="5ffb3-132">Calculate distance between GPS coordinates</span></span>](#hive-gpsdistance)

### <span data-ttu-id="5ffb3-133"><a name="hive-frequencyfeature"></a>Funkcja generowania na podstawie częstotliwości</span><span class="sxs-lookup"><span data-stu-id="5ffb3-133"><a name="hive-frequencyfeature"></a>Frequency based Feature Generation</span></span>
<span data-ttu-id="5ffb3-134">Często jest przydatne toocalculate hello częstotliwości poziomy hello podzielone na kategorie zmiennej lub częstotliwości hello niektórych kombinacji poziomy wiele zmiennych podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-134">It is often useful toocalculate hello frequencies of hello levels of a categorical variable, or hello frequencies of certain combinations of levels from multiple categorical variables.</span></span> <span data-ttu-id="5ffb3-135">Użytkownicy mogą używać tych częstotliwości powitania po toocalculate skryptu:</span><span class="sxs-lookup"><span data-stu-id="5ffb3-135">Users can use hello following script toocalculate these frequencies:</span></span>

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <span data-ttu-id="5ffb3-136"><a name="hive-riskfeature"></a>Ryzyko podzielone na kategorie zmiennych w klasyfikacji binarnej</span><span class="sxs-lookup"><span data-stu-id="5ffb3-136"><a name="hive-riskfeature"></a>Risks of Categorical Variables in Binary Classification</span></span>
<span data-ttu-id="5ffb3-137">W klasyfikacji binarnej potrzebujemy tooconvert nieliczbowy podzielone na kategorie zmiennych w funkcje numeryczne po modeli hello jest używany tylko mieć funkcje numeryczne.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-137">In binary classification, we need tooconvert non-numeric categorical variables into numeric features when hello models being used only take numeric features.</span></span> <span data-ttu-id="5ffb3-138">Jest to realizowane przez zamianę każdy poziom nieliczbowy zagrożenie liczbowych.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-138">This is done by replacing each non-numeric level with a numeric risk.</span></span> <span data-ttu-id="5ffb3-139">W tej sekcji zostanie przedstawiony niektórych ogólnego zapytań programu Hive obliczające wartości ryzyka hello (dziennika prawdopodobieństwo) podzielone na kategorie zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-139">In this section, we show some generic Hive queries that calculate hello risk values (log odds) of a categorical variable.</span></span>

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

<span data-ttu-id="5ffb3-140">W tym przykładzie zmienne `smooth_param1` i `smooth_param2` są ustawione toosmooth hello ryzyka wartości obliczana na podstawie danych hello.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-140">In this example, variables `smooth_param1` and `smooth_param2` are set toosmooth hello risk values calculated from hello data.</span></span> <span data-ttu-id="5ffb3-141">Ryzyko ma zakresie -Inf Inf.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-141">Risks have a range between -Inf and Inf.</span></span> <span data-ttu-id="5ffb3-142">Ryzyko > 0 wskazuje, czy hello prawdopodobieństwo, że kierowanych hello jest równy too1 jest większa niż 0,5.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-142">A risks > 0 indicates that hello probability that hello target is equal too1 is greater than 0.5.</span></span>

<span data-ttu-id="5ffb3-143">Po obliczeniu hello ryzyka tabeli, użytkownicy mogą przypisywać Tabela tooa wartości ryzyka przez dołączenie go z tabelą ryzyka hello.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-143">After hello risk table is calculated, users can assign risk values tooa table by joining it with hello risk table.</span></span> <span data-ttu-id="5ffb3-144">Zapytanie łącząca Hive Hello została dostarczona w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-144">hello Hive joining query was provided in previous section.</span></span>

### <span data-ttu-id="5ffb3-145"><a name="hive-datefeatures"></a>Wyodrębnij funkcji z pól daty i godziny</span><span class="sxs-lookup"><span data-stu-id="5ffb3-145"><a name="hive-datefeatures"></a>Extract features from Datetime Fields</span></span>
<span data-ttu-id="5ffb3-146">Gałąź jest dostarczany z zestawem funkcji UDF przetwarzania pól daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-146">Hive comes with a set of UDFs for processing datetime fields.</span></span> <span data-ttu-id="5ffb3-147">W gałęzi, hello domyślny format daty/godziny jest "RRRR MM-dd 00:00:00" ("1970-01-01-12:21:32" na przykład).</span><span class="sxs-lookup"><span data-stu-id="5ffb3-147">In Hive, hello default datetime format is 'yyyy-MM-dd 00:00:00' ('1970-01-01 12:21:32' for example).</span></span> <span data-ttu-id="5ffb3-148">W tej sekcji zostanie przedstawiony przykłady, które wyodrębnić hello dnia miesiąca, miesiąc hello z polem datetime i inne przykłady, które konwertowanie ciągu daty/godziny w formacie inne niż w domyślnym formacie hello domyślny ciąg formatu w tooa daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-148">In this section, we show examples that extract hello day of a month, hello month from a datetime field, and other examples that convert a datetime string in a format other than hello default format tooa datetime string in default format.</span></span>

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

<span data-ttu-id="5ffb3-149">To zapytanie Hive przyjęto założenie, że hello *&#60; pole Data i godzina >* jest w formacie daty/godziny hello domyślne.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-149">This Hive query assumes that hello *&#60;datetime field>* is in hello default datetime format.</span></span>

<span data-ttu-id="5ffb3-150">Jeśli pól datetime nie jest hello domyślny format, do sygnatury czasowej Unix należy najpierw tooconvert hello datetime pola, a następnie czas Unix hello konwersji ciągu tooa sygnaturę daty/godziny, która jest domyślnej hello formatu.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-150">If a datetime field is not in hello default format, you need tooconvert hello datetime field into Unix time stamp first, and then convert hello Unix time stamp tooa datetime string that is in hello default format.</span></span> <span data-ttu-id="5ffb3-151">Po hello daty/godziny w domyślnym formacie, użytkownicy mogą stosować funkcje tooextract funkcji UDF datetime hello osadzonych.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-151">When hello datetime is in default format, users can apply hello embedded datetime UDFs tooextract features.</span></span>

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

<span data-ttu-id="5ffb3-152">W tym zapytaniu, jeśli hello *&#60; pole daty/godziny >* ma wzorzec hello, takich jak *2015-03-26 12:04:39*, hello *"&#60; wzorzec pola datetime hello >"* powinna być `'MM/dd/yyyy HH:mm:ss'`.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-152">In this query, if hello *&#60;datetime field>* has hello pattern like *03/26/2015 12:04:39*, hello *'&#60;pattern of hello datetime field>'* should be `'MM/dd/yyyy HH:mm:ss'`.</span></span> <span data-ttu-id="5ffb3-153">tootest, użytkownicy mogą uruchamiać</span><span class="sxs-lookup"><span data-stu-id="5ffb3-153">tootest it, users can run</span></span>

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

<span data-ttu-id="5ffb3-154">Witaj *hivesampletable* w tym zapytaniu preinstalowane na wszystkich klastrach Azure HDInsight Hadoop domyślnie podczas przydzielania hello klastrów.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-154">hello *hivesampletable* in this query comes preinstalled on all Azure HDInsight Hadoop clusters by default when hello clusters are provisioned.</span></span>

### <span data-ttu-id="5ffb3-155"><a name="hive-textfeatures"></a>Wyodrębnij funkcji z pola tekstowe</span><span class="sxs-lookup"><span data-stu-id="5ffb3-155"><a name="hive-textfeatures"></a>Extract features from Text Fields</span></span>
<span data-ttu-id="5ffb3-156">Jeśli tabelę programu Hive hello pola tekstowego, który zawiera ciąg słowa, które są rozdzielone spacjami, hello następujące zapytanie wyodrębnia hello długość ciągu hello i hello liczbę słów w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-156">When hello Hive table has a text field that contains a string of words that are delimited by spaces, hello following query extracts hello length of hello string, and hello number of words in hello string.</span></span>

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <span data-ttu-id="5ffb3-157"><a name="hive-gpsdistance"></a>Obliczanie odległości między zestawami współrzędne GPS</span><span class="sxs-lookup"><span data-stu-id="5ffb3-157"><a name="hive-gpsdistance"></a>Calculate distances between sets of GPS coordinates</span></span>
<span data-ttu-id="5ffb3-158">Zapytanie Hello podane w tej sekcji można bezpośrednio zastosowane toohello NYC taksówki podróży danych.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-158">hello query given in this section can be directly applied toohello NYC Taxi Trip Data.</span></span> <span data-ttu-id="5ffb3-159">Celem Hello to zapytanie jest tooshow jak tooapply osadzonych funkcji matematycznych w gałęzi toogenerate funkcji.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-159">hello purpose of this query is tooshow how tooapply an embedded mathematical functions in Hive toogenerate features.</span></span>

<span data-ttu-id="5ffb3-160">Witaj pola, które są używane w tym zapytaniu są współrzędne GPS hello odbiór i dropoff lokalizacji o nazwie *podnoszenia\_geograficzne*, *podnoszenia\_szerokości geograficznej*,  *dropoff\_geograficzne*, i *dropoff\_szerokości geograficznej*.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-160">hello fields that are used in this query are hello GPS coordinates of pickup and dropoff locations, named *pickup\_longitude*, *pickup\_latitude*, *dropoff\_longitude*, and *dropoff\_latitude*.</span></span> <span data-ttu-id="5ffb3-161">zapytania Hello, obliczające hello bezpośredniego odległość między współrzędne odbiór i dropoff hello są:</span><span class="sxs-lookup"><span data-stu-id="5ffb3-161">hello queries that calculate hello direct distance between hello pickup and dropoff coordinates are:</span></span>

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

<span data-ttu-id="5ffb3-162">równania matematyczne Hello obliczające hello odległość między dwoma współrzędne GPS znajduje się na powitania <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">skryptów typu ruchome</a> lokacji utworzone przez Lapisu Peterowi.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-162">hello mathematical equations that calculate hello distance between two GPS coordinates can be found on hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable Type Scripts</a> site, authored by Peter Lapisu.</span></span> <span data-ttu-id="5ffb3-163">W jego Javascript hello funkcja `toRad()` jest po prostu *lat_or_lon*pi/180 *, który konwertuje tooradians stopni.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-163">In his Javascript, hello function `toRad()` is just *lat_or_lon*pi/180*, which converts degrees tooradians.</span></span> <span data-ttu-id="5ffb3-164">W tym miejscu *lat_or_lon* jest szerokości geograficznej hello lub długość geograficzną.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-164">Here, *lat_or_lon* is hello latitude or longitude.</span></span> <span data-ttu-id="5ffb3-165">Ponieważ gałąź nie zawiera funkcji hello `atan2`, ale zawierają hello funkcja `atan`, hello `atan2` funkcji jest implementowany przez `atan` w hello powyżej zapytań Hive przy użyciu definicji hello w funkcji <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-165">Since Hive does not provide hello function `atan2`, but provides hello function `atan`, hello `atan2` function is implemented by `atan` function in hello above Hive query using hello definition provided in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank">Wikipedia</a>.</span></span>

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-create-features-hive/atan2new.png)

<span data-ttu-id="5ffb3-167">Pełną listę funkcji UDF embedded znajdują się w hello gałęzi **wbudowanych funkcji** sekcji na powitania <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span><span class="sxs-lookup"><span data-stu-id="5ffb3-167">A full list of Hive embedded UDFs can be found in hello **Built-in Functions** section on hello <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).</span></span>  

## <span data-ttu-id="5ffb3-168"><a name="tuning"></a>Tematy zaawansowane: parametry Hive strojenia tooImprove szybkości zapytania</span><span class="sxs-lookup"><span data-stu-id="5ffb3-168"><a name="tuning"></a> Advanced topics: Tune Hive Parameters tooImprove Query Speed</span></span>
<span data-ttu-id="5ffb3-169">Witaj domyślnego parametru, ustawienia klastra gałęzi nie może być odpowiednie dla zapytań programu Hive hello i danych hello przetwarzania kwerend hello.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-169">hello default parameter settings of Hive cluster might not be suitable for hello Hive queries and hello data that hello queries are processing.</span></span> <span data-ttu-id="5ffb3-170">W tej sekcji omówiono niektóre parametry, które użytkownicy można dostosować zwiększających hello wydajność zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-170">In this section, we discuss some parameters that users can tune that improve hello performance of Hive queries.</span></span> <span data-ttu-id="5ffb3-171">Użytkownicy muszą parametru hello tooadd strojenia kwerendy przed hello zapytania przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-171">Users need tooadd hello parameter tuning queries before hello queries of processing data.</span></span>

1. <span data-ttu-id="5ffb3-172">**Miejsce na stercie Java**: dla zapytań obejmujących dołączenie dużych zestawów danych lub przetwarzania rekordów długi **kończy się wolne miejsce na stercie** jest jednym z typowych błędów hello.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-172">**Java heap space**: For queries involving joining large datasets, or processing long records, **running out of heap space** is one of hello common error.</span></span> <span data-ttu-id="5ffb3-173">Można to dostroić przez ustawienie parametrów *mapreduce.map.java.opts* i *mapreduce.task.io.sort.mb* toodesired wartości.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-173">This can be tuned by setting parameters *mapreduce.map.java.opts* and *mapreduce.task.io.sort.mb* toodesired values.</span></span> <span data-ttu-id="5ffb3-174">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="5ffb3-174">Here is an example:</span></span>
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    <span data-ttu-id="5ffb3-175">Ten parametr przydziela miejsce na stercie tooJava 4GB pamięci i powoduje sortowanie efektywniejsze przez przydzielanie większej ilości pamięci.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-175">This parameter allocates 4GB memory tooJava heap space and also makes sorting more efficient by allocating more memory for it.</span></span> <span data-ttu-id="5ffb3-176">Jest dobrym rozwiązaniem tooplay z tych przydziałów, jeśli każde miejsce tooheap powiązane błędy niepowodzenia zadania.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-176">It is a good idea tooplay with these allocations if there are any job failure errors related tooheap space.</span></span>

1. <span data-ttu-id="5ffb3-177">**Rozmiaru bloku systemu plików DFS** : ten parametr określa hello najmniejsza jednostka danych hello magazynów systemu plików.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-177">**DFS block size** : This parameter sets hello smallest unit of data that hello file system stores.</span></span> <span data-ttu-id="5ffb3-178">Na przykład jeśli rozmiar bloku hello systemu plików DFS to 128MB, następnie żadnych danych o rozmiarze poniżej oraz too128MB są przechowywane w jeden blok danych, który jest większy niż 128MB przydzielony dodatkowe bloki.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-178">As an example, if hello DFS block size is 128MB, then any data of size less than and up too128MB is stored in a single block, while data that is larger than 128MB is allotted extra blocks.</span></span> <span data-ttu-id="5ffb3-179">Wybieranie rozmiaru bloku bardzo małych powoduje duże koszty Hadoop, ponieważ hello nazwa węzła ma tooprocess wiele więcej żądań toofind hello odpowiednich bloku dotyczących pliku toohello.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-179">Choosing a very small block size causes large overheads in Hadoop since hello name node has tooprocess many more requests toofind hello relevant block pertaining toohello file.</span></span> <span data-ttu-id="5ffb3-180">Zalecane ustawienia po dotyczących gigabajty (lub więcej) danych jest:</span><span class="sxs-lookup"><span data-stu-id="5ffb3-180">A recommended setting when dealing with gigabytes (or larger) data is :</span></span>
   
        set dfs.block.size=128m;
2. <span data-ttu-id="5ffb3-181">**Optymalizacja operacji tworzenia sprzężenia w gałęzi** : podczas operacji łączenia w ramach mapy/zmniejszyć hello zazwyczaj miejsce w hello zmniejszyć fazy, czasami, znaczne zyski uzyskuje się poprzez zaplanowanie sprzężenia w fazie mapy hello (zwane również "mapjoins").</span><span class="sxs-lookup"><span data-stu-id="5ffb3-181">**Optimizing join operation in Hive** : While join operations in hello map/reduce framework typically take place in hello reduce phase, sometimes, enormous gains can be achieved by scheduling joins in hello map phase (also called "mapjoins").</span></span> <span data-ttu-id="5ffb3-182">toodirect gałęzi toodo to o ile to możliwe, firma Microsoft może ustawić:</span><span class="sxs-lookup"><span data-stu-id="5ffb3-182">toodirect Hive toodo this whenever possible, we can set :</span></span>
   
        set hive.auto.convert.join=true;
3. <span data-ttu-id="5ffb3-183">**Określanie liczby hello tooHive mapowań** : podczas Hadoop pozwala hello użytkownika tooset hello liczba reduktory, hello liczby mapowań jest zwykle nie można ustawić hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-183">**Specifying hello number of mappers tooHive** : While Hadoop allows hello user tooset hello number of reducers, hello number of mappers is typically not be set by hello user.</span></span> <span data-ttu-id="5ffb3-184">Lewy, umożliwiający pewien stopień kontroli tego numeru jest toochoose hello Hadoop zmiennych, *mapred.min.split.size* i *mapred.max.split.size* jako rozmiar hello map zadań zależy od:</span><span class="sxs-lookup"><span data-stu-id="5ffb3-184">A trick that allows some degree of control on this number is toochoose hello Hadoop variables, *mapred.min.split.size* and *mapred.max.split.size* as hello size of each map task is determined by :</span></span>
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    <span data-ttu-id="5ffb3-185">Zazwyczaj hello wartość domyślną *mapred.min.split.size* ma wartość 0, z *mapred.max.split.size* jest **Long.MAX** i *dfs.block.size* to 64MB.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-185">Typically, hello default value of *mapred.min.split.size* is 0, that of *mapred.max.split.size* is **Long.MAX** and that of *dfs.block.size* is 64MB.</span></span> <span data-ttu-id="5ffb3-186">Jak widać, rozmiar danych danego hello, dostrajanie parametrów "ustawienia" ich pozwala nam tootune hello liczby mapowań używane.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-186">As we can see, given hello data size, tuning these parameters by "setting" them allows us tootune hello number of mappers used.</span></span>
4. <span data-ttu-id="5ffb3-187">Kilka innych kolejnych **zaawansowane opcje** Hive optymalizacji wydajności są wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-187">A few other more **advanced options** for optimizing Hive performance are mentioned below.</span></span> <span data-ttu-id="5ffb3-188">Te pozwalają tooset hello przydzielonej pamięci toomap i zmniejszyć zadań i mogą być przydatne w Dostosowywanie wydajności.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-188">These allow you tooset hello memory allocated toomap and reduce tasks, and can be useful in tweaking performance.</span></span> <span data-ttu-id="5ffb3-189">Należy pamiętać o tym hello *mapreduce.reduce.memory.mb* nie może być większy niż rozmiar pamięci fizycznej hello każdego węzła procesu roboczego w hello klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5ffb3-189">Please keep in mind that hello *mapreduce.reduce.memory.mb* cannot be greater than hello physical memory size of each worker node in hello Hadoop cluster.</span></span>
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

