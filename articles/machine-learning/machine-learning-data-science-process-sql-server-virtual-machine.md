---
title: aaaExplore danych maszyny wirtualnej programu SQL Server na platformie Azure | Dokumentacja firmy Microsoft
description: Eksploruj dane i generowania funkcje w maszyny wirtualnej programu SQL Server na platformie Azure
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="01531-103"><a name="heading"></a>Dane procesu w maszynie wirtualnej serwera SQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="01531-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="01531-104">W tym dokumencie opisano sposób tooexplore danych oraz do generowania funkcje danych przechowywanych na maszynie Wirtualnej z programu SQL Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="01531-104">This document covers how tooexplore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="01531-105">Można to zrobić przy użyciu języka programowania, takich jak Python lub wrangling danych przy użyciu programu SQL.</span><span class="sxs-lookup"><span data-stu-id="01531-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="01531-106">instrukcje SQL próbki Hello w tym dokumencie założono, że dane są w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="01531-106">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="01531-107">Jeśli nie, zobacz toohello chmury danych nauki procesu mapy toolearn jak toomove Twojego tooSQL danych serwera.</span><span class="sxs-lookup"><span data-stu-id="01531-107">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="01531-108"><a name="SQL"></a>Przy użyciu programu SQL</span><span class="sxs-lookup"><span data-stu-id="01531-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="01531-109">Przedstawione hello następujące zadania wrangling danych w tej sekcji przy użyciu programu SQL:</span><span class="sxs-lookup"><span data-stu-id="01531-109">We describe hello following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="01531-110">Eksploracja danych</span><span class="sxs-lookup"><span data-stu-id="01531-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="01531-111">Funkcja generowania</span><span class="sxs-lookup"><span data-stu-id="01531-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="01531-112"><a name="sql-dataexploration"></a>Eksploracja danych</span><span class="sxs-lookup"><span data-stu-id="01531-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="01531-113">Poniżej przedstawiono kilka przykładowe skrypty SQL, które mogą być używane tooexplore magazyny danych w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="01531-113">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="01531-114">Na przykład praktyczne, można użyć hello [dataset taksówki NYC](http://www.andresmh.com/nyctaxitrips/) i odwoływać się toohello IPNB zatytułowany [wrangling NYC danych za pomocą notesu IPython i SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) dla przewodnika end-to-end.</span><span class="sxs-lookup"><span data-stu-id="01531-114">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="01531-115">Zliczanie hello uwagi na dzień</span><span class="sxs-lookup"><span data-stu-id="01531-115">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="01531-116">Pobierz poziomy hello w kolumnie podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="01531-116">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="01531-117">Pobierz hello podaną liczbę poziomów w połączeniu z dwóch kolumn podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="01531-117">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="01531-118">Pobierz dystrybucji hello kolumn wartości liczbowych</span><span class="sxs-lookup"><span data-stu-id="01531-118">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="01531-119"><a name="sql-featuregen"></a>Funkcja generowania</span><span class="sxs-lookup"><span data-stu-id="01531-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="01531-120">W tej sekcji opisano sposób generowania funkcji za pomocą programu SQL:</span><span class="sxs-lookup"><span data-stu-id="01531-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="01531-121">Funkcja generowania na podstawie liczby</span><span class="sxs-lookup"><span data-stu-id="01531-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="01531-122">Funkcja generowania binning</span><span class="sxs-lookup"><span data-stu-id="01531-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="01531-123">Wprowadza hello funkcji z jedną kolumną</span><span class="sxs-lookup"><span data-stu-id="01531-123">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="01531-124">Po wygenerowaniu dodatkowe funkcje, możesz dodać je jako kolumny toohello istniejącej tabeli lub Utwórz nową tabelę z dodatkowych funkcji hello i klucz podstawowy, który może być połączony z hello oryginalnej tabeli.</span><span class="sxs-lookup"><span data-stu-id="01531-124">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span> 
> 
> 

### <span data-ttu-id="01531-125"><a name="sql-countfeature"></a>Funkcja generowania na podstawie liczby</span><span class="sxs-lookup"><span data-stu-id="01531-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="01531-126">Witaj poniższych przykładach pokazano dwa sposoby generowania funkcji count.</span><span class="sxs-lookup"><span data-stu-id="01531-126">hello following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="01531-127">Pierwsza metoda Hello używa warunkowego sum i drugi używa metody hello hello klauzuli 'where'.</span><span class="sxs-lookup"><span data-stu-id="01531-127">hello first method uses conditional sum and hello second method uses hello 'where' clause.</span></span> <span data-ttu-id="01531-128">Następnie te mogą być dołączane funkcjami hello oryginalnej tabeli (przy użyciu kolumn klucza podstawowego) toohave liczba obok hello oryginalnych danych.</span><span class="sxs-lookup"><span data-stu-id="01531-128">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="01531-129"><a name="sql-binningfeature"></a>Funkcja generowania binning</span><span class="sxs-lookup"><span data-stu-id="01531-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="01531-130">Witaj poniższy przykład przedstawia sposób toogenerate binned funkcje przez binning (za pomocą pięciu bins) kolumny liczbowe, która może służyć jako funkcja zamiast tego:</span><span class="sxs-lookup"><span data-stu-id="01531-130">hello following example shows how toogenerate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="01531-131"><a name="sql-featurerollout"></a>Wprowadza hello funkcji z jedną kolumną</span><span class="sxs-lookup"><span data-stu-id="01531-131"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="01531-132">W tej sekcji przedstawiony sposób tooroll limit pojedynczej kolumny w tabeli toogenerate dodatkowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="01531-132">In this section, we demonstrate how tooroll out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="01531-133">przykład Witaj zakłada, że istnieje szerokości geograficznej lub długość geograficzną kolumny w tabeli hello, z którym próbujesz toogenerate funkcji.</span><span class="sxs-lookup"><span data-stu-id="01531-133">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="01531-134">Oto krótkie Elementarz na współrzędne/geograficznej lokalizacji danych (planować z stackoverflow [jak toomeasure hello dokładność współrzędne geograficzne?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="01531-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How toomeasure hello accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="01531-135">Jest to przydatne toounderstand przed pole lokalizacji hello featurizing:</span><span class="sxs-lookup"><span data-stu-id="01531-135">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="01531-136">znak Hello informuje NAS czy pracujemy północ lub południe, wschód lub zachód na Witaj świecie.</span><span class="sxs-lookup"><span data-stu-id="01531-136">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="01531-137">Niezerowe setki cyfrę informuje, nam używamy długości, nie szerokości geograficznej!</span><span class="sxs-lookup"><span data-stu-id="01531-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="01531-138">cyfra Hello dziesiątki daje tooabout pozycji kilometrach 1000.</span><span class="sxs-lookup"><span data-stu-id="01531-138">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="01531-139">Udostępnia nam przydatnych informacji o jakie kontynencie lub Oceanu jesteśmy w.</span><span class="sxs-lookup"><span data-stu-id="01531-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="01531-140">cyfra jednostki Hello (jeden stopień decimal) zapewnia stanie się kilometrach too111 (60 mil, około 69 mil).</span><span class="sxs-lookup"><span data-stu-id="01531-140">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="01531-141">Go nam powiedzieć około jakim stanie dużych lub kraju, w którym możemy w.</span><span class="sxs-lookup"><span data-stu-id="01531-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="01531-142">Witaj przecinku warto się too11.1 km: można odróżnić hello położenie dużych miast z sąsiednich Miasto duże.</span><span class="sxs-lookup"><span data-stu-id="01531-142">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="01531-143">drugi po przecinku Hello warto się too1.1 km: go dalej oddzielić wieś jeden od hello.</span><span class="sxs-lookup"><span data-stu-id="01531-143">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="01531-144">trzeci po przecinku Hello jest warto się too110 m: zidentyfikuje dużych rolnych pola lub instytucjonalnych firmy.</span><span class="sxs-lookup"><span data-stu-id="01531-144">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="01531-145">czwarty po przecinku Hello jest warto się too11 m: można zidentyfikować zbiorczym ziemi.</span><span class="sxs-lookup"><span data-stu-id="01531-145">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="01531-146">To typowy dokładność toohello można porównywać pod względem jednostki GPS Niepoprawione bez zakłóceń.</span><span class="sxs-lookup"><span data-stu-id="01531-146">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="01531-147">dziesiętnego piątym powitania jest warto się too1.1 m: go odróżnia drzewa od siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="01531-147">hello fifth decimal place is worth up too1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="01531-148">Poziom toothis dokładność z komercyjnego jednostki GPS można uzyskać tylko z różnicowej korekty.</span><span class="sxs-lookup"><span data-stu-id="01531-148">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="01531-149">szóstego po przecinku Hello warto się m: too0.11, możesz użyć tej funkcji do układania struktury szczegółowo projektowania krajobrazów, tworzenie drogi.</span><span class="sxs-lookup"><span data-stu-id="01531-149">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="01531-150">Powinna ona więcej niż wystarczy do śledzenia przemieszczania glaciers i rzek.</span><span class="sxs-lookup"><span data-stu-id="01531-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="01531-151">Można to osiągnąć, wykonując painstaking środków GPS, takich jak differentially poprawiony GPS.</span><span class="sxs-lookup"><span data-stu-id="01531-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="01531-152">informacje o lokalizacji Hello można featurized następujące oddzielanie regionu, lokalizacji i Miasto informacji.</span><span class="sxs-lookup"><span data-stu-id="01531-152">hello location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="01531-153">Należy pamiętać, można również wywołać punkt końcowy REST, np. interfejsu API map Bing dostępne pod adresem [znaleźć lokalizacji przez punkt](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello region/regionalnego informacji.</span><span class="sxs-lookup"><span data-stu-id="01531-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello region/district information.</span></span>

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

<span data-ttu-id="01531-154">Te funkcje na podstawie lokalizacji może być dalsze używane toogenerate liczba dodatkowe funkcje, zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="01531-154">These location-based features can be further used toogenerate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="01531-155">Można programowo wstawić hello rekordów przy użyciu języka wybór.</span><span class="sxs-lookup"><span data-stu-id="01531-155">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="01531-156">Może być konieczne danych hello tooinsert efektywności zapisu tooimprove fragmentów (na przykład jak toodo tego przy użyciu pyodbc, zobacz [A HelloWorld próbki tooaccess SQLServer języka Python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="01531-156">You may need tooinsert hello data in chunks tooimprove write efficiency (for an example of how toodo this using pyodbc, see [A HelloWorld sample tooaccess SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="01531-157">Alternatywą jest tooinsert danych w bazie danych hello przy użyciu hello [narzędzia BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="01531-157">Another alternative is tooinsert data in hello database using hello [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="01531-158"><a name="sql-aml"></a>Łączenie tooAzure uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="01531-158"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="01531-159">Funkcja Hello nowo wygenerowane mogą być dodawane jako kolumny tabeli istniejącej tooan lub przechowywane w nowej tabeli lub połączony z oryginalnej tabeli hello do uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="01531-159">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="01531-160">Funkcje mogą być generowane lub niemożliwy, jeśli już utworzone przy użyciu hello [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="01531-160">Features can be generated or accessed if already created, using hello [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![czytniki uczenie maszynowe Azure][1] 

## <span data-ttu-id="01531-162"><a name="python"></a>Przy użyciu języka programowania, takich jak Python</span><span class="sxs-lookup"><span data-stu-id="01531-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="01531-163">Przy użyciu języka Python tooexplore danych i funkcji generowania hello danych jest w programie SQL Server jest podobne tooprocessing dane obiektów blob platformy Azure przy użyciu języka Python, zgodnie z opisem w [danych obiektów Blob platformy Azure procesu w danym środowisku nauki danych](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="01531-163">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="01531-164">dane Hello musi załadować z bazy danych hello do ramki danych pandas toobe i następnie mogą być dalej przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="01531-164">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="01531-165">Firma Microsoft dokumentu hello proces łączenia toohello bazy danych i ładowania danych hello do ramki danych hello w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="01531-165">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="01531-166">Witaj następującego formatu ciągu połączenia może być bazy danych programu SQL Server tooa tooconnect używanych w języku Python za pomocą pyodbc (Zastąp servername, dbname nazwy użytkownika i hasła o określonej wartości):</span><span class="sxs-lookup"><span data-stu-id="01531-166">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="01531-167">Witaj [biblioteki Pandas](http://pandas.pydata.org/) w języku Python zawiera bogaty zestaw struktur danych i narzędzia do analizy danych do manipulowania danymi programowania Python.</span><span class="sxs-lookup"><span data-stu-id="01531-167">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="01531-168">Poniższy kod Hello odczytuje hello wyników zwrócony z bazy danych programu SQL Server do ramki danych Pandas:</span><span class="sxs-lookup"><span data-stu-id="01531-168">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="01531-169">Teraz możesz pracować z hello Pandas danych ramki, co opisano w artykule hello [danych obiektów Blob platformy Azure procesu w danym środowisku nauki danych](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="01531-169">Now you can work with hello Pandas data frame as covered in hello article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="01531-170">Nauki danych Azure w przykładzie akcji</span><span class="sxs-lookup"><span data-stu-id="01531-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="01531-171">Przykład wskazówki na trasie hello proces nauki danych Azure przy użyciu publicznego zestawu danych, zobacz [proces nauki danych Azure, w akcji](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="01531-171">For an end-to-end walkthrough example of hello Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

