---
title: Eksplorowanie danych maszyny wirtualnej programu SQL Server na platformie Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 16fabb29bdc8ec770efd843e18e9016e338a8f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="755ed-103"><a name="heading"></a>Dane procesu w maszynie wirtualnej serwera SQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="755ed-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="755ed-104">W tym dokumencie opisano sposób eksplorować dane i generowanie funkcji danych przechowywanych na maszynie Wirtualnej z programu SQL Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="755ed-104">This document covers how to explore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="755ed-105">Można to zrobić przy użyciu języka programowania, takich jak Python lub wrangling danych przy użyciu programu SQL.</span><span class="sxs-lookup"><span data-stu-id="755ed-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="755ed-106">Instrukcje SQL próbki w tym dokumencie założono, że dane są w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="755ed-106">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="755ed-107">Jeśli nie, zajrzyj do mapy procesu chmury danych nauki, aby dowiedzieć się, jak przenieść dane do programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="755ed-107">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="755ed-108"><a name="SQL"></a>Przy użyciu programu SQL</span><span class="sxs-lookup"><span data-stu-id="755ed-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="755ed-109">Opisano następujące zadania wrangling danych w tej sekcji przy użyciu programu SQL:</span><span class="sxs-lookup"><span data-stu-id="755ed-109">We describe the following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="755ed-110">Eksploracja danych</span><span class="sxs-lookup"><span data-stu-id="755ed-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="755ed-111">Funkcja generowania</span><span class="sxs-lookup"><span data-stu-id="755ed-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="755ed-112"><a name="sql-dataexploration"></a>Eksploracja danych</span><span class="sxs-lookup"><span data-stu-id="755ed-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="755ed-113">Poniżej przedstawiono kilka przykładowe skrypty SQL, które mogą służyć do eksplorowania magazyny danych w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="755ed-113">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="755ed-114">Na przykład praktyczne, można użyć [dataset taksówki NYC](http://www.andresmh.com/nyctaxitrips/) i zapoznaj się z IPNB zatytułowany [wrangling NYC danych za pomocą notesu IPython i SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) dla przewodnika end-to-end.</span><span class="sxs-lookup"><span data-stu-id="755ed-114">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="755ed-115">Zliczanie uwagi na dzień</span><span class="sxs-lookup"><span data-stu-id="755ed-115">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="755ed-116">Pobierz poziomy w kolumnie podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="755ed-116">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="755ed-117">Pobierz liczbę poziomów w połączeniu z dwóch kolumn podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="755ed-117">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="755ed-118">Pobierz dystrybucji dla kolumn wartości liczbowych</span><span class="sxs-lookup"><span data-stu-id="755ed-118">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="755ed-119"><a name="sql-featuregen"></a>Funkcja generowania</span><span class="sxs-lookup"><span data-stu-id="755ed-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="755ed-120">W tej sekcji opisano sposób generowania funkcji za pomocą programu SQL:</span><span class="sxs-lookup"><span data-stu-id="755ed-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="755ed-121">Funkcja generowania na podstawie liczby</span><span class="sxs-lookup"><span data-stu-id="755ed-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="755ed-122">Funkcja generowania binning</span><span class="sxs-lookup"><span data-stu-id="755ed-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="755ed-123">Wprowadza funkcji z jedną kolumną</span><span class="sxs-lookup"><span data-stu-id="755ed-123">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="755ed-124">Po wygenerowaniu dodatkowe funkcje, możesz dodać je jako kolumny do istniejącej tabeli lub Utwórz nową tabelę z dodatkowych funkcji i klucz podstawowy, który może być połączony z oryginalnej tabeli.</span><span class="sxs-lookup"><span data-stu-id="755ed-124">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span> 
> 
> 

### <span data-ttu-id="755ed-125"><a name="sql-countfeature"></a>Funkcja generowania na podstawie liczby</span><span class="sxs-lookup"><span data-stu-id="755ed-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="755ed-126">W poniższych przykładach pokazano dwa sposoby generowania funkcji count.</span><span class="sxs-lookup"><span data-stu-id="755ed-126">The following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="755ed-127">Pierwsza metoda korzysta sum warunkowych, a druga metoda klauzula "where".</span><span class="sxs-lookup"><span data-stu-id="755ed-127">The first method uses conditional sum and the second method uses the 'where' clause.</span></span> <span data-ttu-id="755ed-128">Te można następnie być połączony z oryginalnej tabeli (przy użyciu kolumn klucza podstawowego) ma funkcje liczby równolegle z oryginalnych danych.</span><span class="sxs-lookup"><span data-stu-id="755ed-128">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="755ed-129"><a name="sql-binningfeature"></a>Funkcja generowania binning</span><span class="sxs-lookup"><span data-stu-id="755ed-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="755ed-130">Poniższy przykład przedstawia wygenerować funkcji binned przez binning (za pomocą pięciu bins) kolumny liczbowe, która może służyć jako funkcja zamiast tego:</span><span class="sxs-lookup"><span data-stu-id="755ed-130">The following example shows how to generate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="755ed-131"><a name="sql-featurerollout"></a>Wprowadza funkcji z jedną kolumną</span><span class="sxs-lookup"><span data-stu-id="755ed-131"><a name="sql-featurerollout"></a>Rolling out the features from a single column</span></span>
<span data-ttu-id="755ed-132">W tej sekcji pokażemy, jak korzystać z jednej kolumny w tabeli, aby wygenerować dodatkowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="755ed-132">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span></span> <span data-ttu-id="755ed-133">W przykładzie założono, że w tabeli, z którego chcesz wygenerować funkcji jest kolumną szerokości geograficznej lub długość geograficzną.</span><span class="sxs-lookup"><span data-stu-id="755ed-133">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="755ed-134">Oto krótkie Elementarz na współrzędne/geograficznej lokalizacji danych (planować z stackoverflow [sposób mierzenia dokładność współrzędne geograficzne?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="755ed-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="755ed-135">Jest to przydatne zrozumieć przed featurizing pole lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="755ed-135">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="755ed-136">Znak informuje NAS czy możemy się północ lub Południowa, wschód lub zachód na całym świecie.</span><span class="sxs-lookup"><span data-stu-id="755ed-136">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="755ed-137">Niezerowe setki cyfrę informuje, nam używamy długości, nie szerokości geograficznej!</span><span class="sxs-lookup"><span data-stu-id="755ed-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="755ed-138">Dziesiątki cyfrę daje możliwość około 1000 kilometrach.</span><span class="sxs-lookup"><span data-stu-id="755ed-138">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="755ed-139">Udostępnia nam przydatnych informacji o jakie kontynencie lub Oceanu jesteśmy w.</span><span class="sxs-lookup"><span data-stu-id="755ed-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="755ed-140">Cyfra jednostki (jeden stopień decimal) zapewnia pozycji do 111 kilometrach (60 mil, około 69 mil).</span><span class="sxs-lookup"><span data-stu-id="755ed-140">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="755ed-141">Go nam powiedzieć około jakim stanie dużych lub kraju, w którym możemy w.</span><span class="sxs-lookup"><span data-stu-id="755ed-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="755ed-142">Pierwszy przecinka warto do 11.1 km: można odróżnić pozycja dużych miast z sąsiednich Miasto duże.</span><span class="sxs-lookup"><span data-stu-id="755ed-142">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="755ed-143">Drugi przecinka warto do 1.1 km: go oddzielić wieś jednego z następnej.</span><span class="sxs-lookup"><span data-stu-id="755ed-143">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="755ed-144">Trzecia cyfra dziesiętna jest wartości do 110 m: zidentyfikuje dużych rolnych pola lub instytucjonalnych firmy.</span><span class="sxs-lookup"><span data-stu-id="755ed-144">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="755ed-145">Warto m: do 11 można zidentyfikować zbiorczym ziemi jest czwarty miejsc dziesiętnych.</span><span class="sxs-lookup"><span data-stu-id="755ed-145">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="755ed-146">Nie jest porównywalny typowe dokładność Niepoprawione jednostki GPS bez zakłóceń.</span><span class="sxs-lookup"><span data-stu-id="755ed-146">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="755ed-147">Warto do 1.1 m: go odróżnia drzewa od siebie nawzajem jest piąty przecinka.</span><span class="sxs-lookup"><span data-stu-id="755ed-147">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="755ed-148">Dokładność na ten poziom z komercyjnego jednostki GPS tylko może zostać osiągnięty przy różnicowej korekty.</span><span class="sxs-lookup"><span data-stu-id="755ed-148">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="755ed-149">Warto do uwzględnieniu wartości 0,11 m: możesz użyć tej funkcji do układania struktury szczegółowo projektowania krajobrazów, tworzenie drogi jest szóstego miejsc dziesiętnych.</span><span class="sxs-lookup"><span data-stu-id="755ed-149">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="755ed-150">Powinna ona więcej niż wystarczy do śledzenia przemieszczania glaciers i rzek.</span><span class="sxs-lookup"><span data-stu-id="755ed-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="755ed-151">Można to osiągnąć, wykonując painstaking środków GPS, takich jak differentially poprawiony GPS.</span><span class="sxs-lookup"><span data-stu-id="755ed-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="755ed-152">Informacje o lokalizacji można featurized następujące oddzielanie regionu, lokalizacji i Miasto informacji.</span><span class="sxs-lookup"><span data-stu-id="755ed-152">The location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="755ed-153">Należy pamiętać, można również wywołać punkt końcowy REST, np. interfejsu API map Bing dostępne pod adresem [znaleźć lokalizacji przez punkt](https://msdn.microsoft.com/library/ff701710.aspx) można pobrać informacji o regionie/okręgu.</span><span class="sxs-lookup"><span data-stu-id="755ed-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) to get the region/district information.</span></span>

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

<span data-ttu-id="755ed-154">Te funkcje oparte na lokalizacji dalsze umożliwia generowanie liczby dodatkowych funkcji zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="755ed-154">These location-based features can be further used to generate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="755ed-155">Można programowane Wstawianie rekordów przy użyciu języka wybór.</span><span class="sxs-lookup"><span data-stu-id="755ed-155">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="755ed-156">Konieczne może być wstawić fragmentów, aby zwiększyć wydajność zapisu danych (na przykład jak to zrobić przy użyciu pyodbc zobacz [próby A HelloWorld do uzyskiwania dostępu do SQLServer python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="755ed-156">You may need to insert the data in chunks to improve write efficiency (for an example of how to do this using pyodbc, see [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="755ed-157">Alternatywą jest do wstawiania danych w bazie danych przy użyciu [narzędzia BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="755ed-157">Another alternative is to insert data in the database using the [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="755ed-158"><a name="sql-aml"></a>Nawiązywanie połączenia z usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="755ed-158"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="755ed-159">Funkcja wygenerowanym możliwość dodania jako kolumny do istniejącej tabeli lub przechowywane w nowej tabeli i połączony z oryginalnej tabeli do uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="755ed-159">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="755ed-160">Funkcje mogą być generowane lub dostęp, jeśli już utworzone za pomocą [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="755ed-160">Features can be generated or accessed if already created, using the [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![czytniki uczenie maszynowe Azure][1] 

## <span data-ttu-id="755ed-162"><a name="python"></a>Przy użyciu języka programowania, takich jak Python</span><span class="sxs-lookup"><span data-stu-id="755ed-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="755ed-163">Przy użyciu języka Python do Eksplorowanie danych oraz do generowania funkcji, jeśli dane są w programie SQL Server jest podobny do przetwarzania danych obiektów blob platformy Azure przy użyciu języka Python, zgodnie z opisem w [danych obiektów Blob platformy Azure procesu w danym środowisku nauki danych](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="755ed-163">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="755ed-164">Dane powinna być załadowana z bazy danych do ramki pandas danych, a następnie mogą być dalej przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="755ed-164">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="755ed-165">Proces łączenia z bazą danych i ładowania danych do ramki danych w tej sekcji możemy dokumentu.</span><span class="sxs-lookup"><span data-stu-id="755ed-165">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="755ed-166">Następującego formatu ciągu połączenia może służyć do połączenia z bazą danych programu SQL Server w języku Python za pomocą pyodbc (Zastąp servername, dbname nazwy użytkownika i hasła o określonej wartości):</span><span class="sxs-lookup"><span data-stu-id="755ed-166">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="755ed-167">[Biblioteki Pandas](http://pandas.pydata.org/) w języku Python zawiera bogaty zestaw struktur danych i narzędzia do analizy danych do manipulowania danymi programowania Python.</span><span class="sxs-lookup"><span data-stu-id="755ed-167">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="755ed-168">Poniższy kod odczytuje wyniki zwracane z bazy danych programu SQL Server do ramki danych Pandas:</span><span class="sxs-lookup"><span data-stu-id="755ed-168">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="755ed-169">Teraz możesz pracować z Pandas ramki danych, co opisano w artykule [danych obiektów Blob platformy Azure procesu w danym środowisku nauki danych](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="755ed-169">Now you can work with the Pandas data frame as covered in the article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="755ed-170">Nauki danych Azure w przykładzie akcji</span><span class="sxs-lookup"><span data-stu-id="755ed-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="755ed-171">Na przykład wskazówki end-to-end procesu nauki danych Azure przy użyciu publicznego zestawu danych, zobacz [proces nauki danych Azure, w akcji](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="755ed-171">For an end-to-end walkthrough example of the Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

