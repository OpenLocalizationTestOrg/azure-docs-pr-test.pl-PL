---
title: "Funkcje aaaCreate danych w programie SQL Server przy użyciu programu SQL i Python | Dokumentacja firmy Microsoft"
description: "Przetwarzania danych z usługi SQL Azure"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="36fdd-103">Tworzenie funkcji dla danych w programie SQL Server przy użyciu języka SQL i Python</span><span class="sxs-lookup"><span data-stu-id="36fdd-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="36fdd-104">Ten dokument przedstawia sposób funkcji toogenerate dla danych przechowywanych w Maszynę wirtualną SQL Server na platformie Azure, które pomagają algorytmów wydajniej nauki hello danych.</span><span class="sxs-lookup"><span data-stu-id="36fdd-104">This document shows how toogenerate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from hello data.</span></span> <span data-ttu-id="36fdd-105">Można to zrobić przy użyciu języka SQL lub przy użyciu języka programowania, takich jak Python, które przedstawiono w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="36fdd-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="36fdd-106">To **menu** łączy tootopics, które opisują sposób toocreate funkcji dla danych w różnych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="36fdd-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="36fdd-107">To zadanie jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="36fdd-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="36fdd-108">Na przykład praktyczne, zalecamy skonsultowanie hello [dataset taksówki NYC](http://www.andresmh.com/nyctaxitrips/) i odwoływać się toohello IPNB zatytułowany [wrangling NYC danych za pomocą notesu IPython i SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) dla przewodnika end-to-end.</span><span class="sxs-lookup"><span data-stu-id="36fdd-108">For a practical example, you can consult hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="36fdd-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="36fdd-109">Prerequisites</span></span>
<span data-ttu-id="36fdd-110">W tym artykule przyjęto założenie, że masz:</span><span class="sxs-lookup"><span data-stu-id="36fdd-110">This article assumes that you have:</span></span>

* <span data-ttu-id="36fdd-111">Utworzone konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36fdd-111">Created an Azure storage account.</span></span> <span data-ttu-id="36fdd-112">Aby uzyskać instrukcje, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="36fdd-112">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="36fdd-113">Przechowywane dane w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="36fdd-113">Stored your data in SQL Server.</span></span> <span data-ttu-id="36fdd-114">Jeśli nie masz, zobacz [Przenieś tooan danych bazy danych SQL Azure dla usługi Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) instrukcje dotyczące sposobu toomove hello dane za pomocą.</span><span class="sxs-lookup"><span data-stu-id="36fdd-114">If you have not, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how toomove hello data there.</span></span>

## <span data-ttu-id="36fdd-115"><a name="sql-featuregen"></a>Funkcja generowania z SQL</span><span class="sxs-lookup"><span data-stu-id="36fdd-115"><a name="sql-featuregen"></a>Feature Generation with SQL</span></span>
<span data-ttu-id="36fdd-116">W tej sekcji opisano sposób generowania funkcji za pomocą programu SQL:</span><span class="sxs-lookup"><span data-stu-id="36fdd-116">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="36fdd-117">Funkcja generowania na podstawie liczby</span><span class="sxs-lookup"><span data-stu-id="36fdd-117">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="36fdd-118">Funkcja generowania binning</span><span class="sxs-lookup"><span data-stu-id="36fdd-118">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="36fdd-119">Wprowadza hello funkcji z jedną kolumną</span><span class="sxs-lookup"><span data-stu-id="36fdd-119">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="36fdd-120">Po wygenerowaniu dodatkowe funkcje, możesz dodać je jako kolumny toohello istniejącej tabeli lub Utwórz nową tabelę z dodatkowych funkcji hello i klucz podstawowy, który może być połączony z hello oryginalnej tabeli.</span><span class="sxs-lookup"><span data-stu-id="36fdd-120">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span>
> 
> 

### <span data-ttu-id="36fdd-121"><a name="sql-countfeature"></a>Funkcja generowania na podstawie liczby</span><span class="sxs-lookup"><span data-stu-id="36fdd-121"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="36fdd-122">W tym dokumencie przedstawiono dwa sposoby generowania funkcji count.</span><span class="sxs-lookup"><span data-stu-id="36fdd-122">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="36fdd-123">Pierwsza metoda Hello używa warunkowego sum i drugi używa metody hello hello klauzuli 'where'.</span><span class="sxs-lookup"><span data-stu-id="36fdd-123">hello first method uses conditional sum and hello second method uses hello 'where\` clause.</span></span> <span data-ttu-id="36fdd-124">Następnie te mogą być dołączane funkcjami hello oryginalnej tabeli (przy użyciu kolumn klucza podstawowego) toohave liczba obok hello oryginalnych danych.</span><span class="sxs-lookup"><span data-stu-id="36fdd-124">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <span data-ttu-id="36fdd-125"><a name="sql-binningfeature"></a>Funkcja generowania binning</span><span class="sxs-lookup"><span data-stu-id="36fdd-125"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="36fdd-126">Witaj poniższy przykład przedstawia sposób toogenerate binned funkcje przez binning (przy użyciu 5 bins) kolumny liczbowe, która może służyć jako funkcja zamiast tego:</span><span class="sxs-lookup"><span data-stu-id="36fdd-126">hello following example shows how toogenerate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="36fdd-127"><a name="sql-featurerollout"></a>Wprowadza hello funkcji z jedną kolumną</span><span class="sxs-lookup"><span data-stu-id="36fdd-127"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="36fdd-128">W tej sekcji przedstawiony sposób tooroll poza pojedyncza kolumna w tabeli toogenerate dodatkowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="36fdd-128">In this section, we demonstrate how tooroll-out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="36fdd-129">przykład Witaj zakłada, że istnieje szerokości geograficznej lub długość geograficzną kolumny w tabeli hello, z którym próbujesz toogenerate funkcji.</span><span class="sxs-lookup"><span data-stu-id="36fdd-129">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="36fdd-130">Oto krótkie Elementarz na współrzędne/geograficznej lokalizacji danych (planować z stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span><span class="sxs-lookup"><span data-stu-id="36fdd-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="36fdd-131">Jest to przydatne toounderstand przed pole lokalizacji hello featurizing:</span><span class="sxs-lookup"><span data-stu-id="36fdd-131">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="36fdd-132">znak Hello informuje NAS czy pracujemy północ lub południe, wschód lub zachód na Witaj świecie.</span><span class="sxs-lookup"><span data-stu-id="36fdd-132">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="36fdd-133">Niezerowe setki cyfrę informuje, nam używamy długości, nie szerokości geograficznej!</span><span class="sxs-lookup"><span data-stu-id="36fdd-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span></span>
* <span data-ttu-id="36fdd-134">cyfra Hello dziesiątki daje tooabout pozycji kilometrach 1000.</span><span class="sxs-lookup"><span data-stu-id="36fdd-134">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="36fdd-135">Udostępnia nam przydatnych informacji o jakie kontynencie lub Oceanu jesteśmy w.</span><span class="sxs-lookup"><span data-stu-id="36fdd-135">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="36fdd-136">cyfra jednostki Hello (jeden stopień decimal) zapewnia stanie się kilometrach too111 (60 mil, około 69 mil).</span><span class="sxs-lookup"><span data-stu-id="36fdd-136">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="36fdd-137">Go nam powiedzieć około jakim stanie dużych lub kraju, w którym możemy w.</span><span class="sxs-lookup"><span data-stu-id="36fdd-137">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="36fdd-138">Witaj przecinku warto się too11.1 km: można odróżnić hello położenie dużych miast z sąsiednich Miasto duże.</span><span class="sxs-lookup"><span data-stu-id="36fdd-138">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="36fdd-139">drugi po przecinku Hello warto się too1.1 km: go dalej oddzielić wieś jeden od hello.</span><span class="sxs-lookup"><span data-stu-id="36fdd-139">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="36fdd-140">trzeci po przecinku Hello jest warto się too110 m: zidentyfikuje dużych rolnych pola lub instytucjonalnych firmy.</span><span class="sxs-lookup"><span data-stu-id="36fdd-140">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="36fdd-141">czwarty po przecinku Hello jest warto się too11 m: można zidentyfikować zbiorczym ziemi.</span><span class="sxs-lookup"><span data-stu-id="36fdd-141">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="36fdd-142">To typowy dokładność toohello można porównywać pod względem jednostki GPS Niepoprawione bez zakłóceń.</span><span class="sxs-lookup"><span data-stu-id="36fdd-142">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="36fdd-143">Hello piątej po przecinku warto się too1.1 m: go odróżnić od siebie drzewa.</span><span class="sxs-lookup"><span data-stu-id="36fdd-143">hello fifth decimal place is worth up too1.1 m: it distinguish trees from each other.</span></span> <span data-ttu-id="36fdd-144">Poziom toothis dokładność z komercyjnego jednostki GPS można uzyskać tylko z różnicowej korekty.</span><span class="sxs-lookup"><span data-stu-id="36fdd-144">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="36fdd-145">szóstego po przecinku Hello warto się m: too0.11, możesz użyć tej funkcji do układania struktury szczegółowo projektowania krajobrazów, tworzenie drogi.</span><span class="sxs-lookup"><span data-stu-id="36fdd-145">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="36fdd-146">Powinna ona więcej niż wystarczy do śledzenia przemieszczania glaciers i rzek.</span><span class="sxs-lookup"><span data-stu-id="36fdd-146">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="36fdd-147">Można to osiągnąć, wykonując painstaking środków GPS, takich jak differentially poprawiony GPS.</span><span class="sxs-lookup"><span data-stu-id="36fdd-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="36fdd-148">informacje o lokalizacji Hello można można featurized następujące oddzielanie regionu, lokalizacji i miejscowości.</span><span class="sxs-lookup"><span data-stu-id="36fdd-148">hello location information can can be featurized as follows, separating out region, location and city information.</span></span> <span data-ttu-id="36fdd-149">Należy pamiętać, że raz także wywołać punkt końcowy REST, np. interfejsu API map Bing dostępne pod adresem `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello region/regionalnego informacji.</span><span class="sxs-lookup"><span data-stu-id="36fdd-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello region/district information.</span></span>

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

<span data-ttu-id="36fdd-150">Hello w powyższej lokalizacji, na podstawie funkcje można dodatkowo korzysta z funkcji count dodatkowe toogenerate zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="36fdd-150">hello above location based features can be further used toogenerate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="36fdd-151">Można programowo wstawić hello rekordów przy użyciu języka wybór.</span><span class="sxs-lookup"><span data-stu-id="36fdd-151">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="36fdd-152">Może być konieczne danych hello tooinsert efektywności zapisu tooimprove fragmentów [zapoznaj się z przykładem hello toodo to w tym miejscu przy użyciu pyodbc](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span><span class="sxs-lookup"><span data-stu-id="36fdd-152">You may need tooinsert hello data in chunks tooimprove write efficiency [Check out hello example of how toodo this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="36fdd-153">Alternatywą jest tooinsert danych przy użyciu bazy danych hello [narzędzia BCP](https://msdn.microsoft.com/library/ms162802.aspx)</span><span class="sxs-lookup"><span data-stu-id="36fdd-153">Another alternative is tooinsert data in hello database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <span data-ttu-id="36fdd-154"><a name="sql-aml"></a>Łączenie tooAzure uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="36fdd-154"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="36fdd-155">Funkcja Hello nowo wygenerowane mogą być dodawane jako kolumny tabeli istniejącej tooan lub przechowywane w nowej tabeli lub połączony z oryginalnej tabeli hello do uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="36fdd-155">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="36fdd-156">Funkcje mogą być generowane lub niemożliwy, jeśli już utworzone przy użyciu hello [i zaimportuj dane](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) modułu w uczenie Maszynowe Azure, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="36fdd-156">Features can be generated or accessed if already created, using hello [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![czytniki uczenie maszynowe Azure](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <span data-ttu-id="36fdd-158"><a name="python"></a>Przy użyciu języka programowania, takich jak Python</span><span class="sxs-lookup"><span data-stu-id="36fdd-158"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="36fdd-159">Za pomocą funkcji toogenerate Python, gdy dane hello jest w programie SQL Server jest podobne tooprocessing dane obiektów blob platformy Azure przy użyciu języka Python, zgodnie z opisem w [danych obiektów Blob platformy Azure proces w przypadku danych nauki środowisku](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="36fdd-159">Using Python toogenerate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="36fdd-160">dane Hello musi załadować z bazy danych hello do ramki danych pandas toobe i następnie mogą być dalej przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="36fdd-160">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="36fdd-161">Firma Microsoft dokumentu hello proces łączenia toohello bazy danych i ładowania danych hello do ramki danych hello w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="36fdd-161">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="36fdd-162">Witaj następującego formatu ciągu połączenia może być bazy danych programu SQL Server tooa tooconnect używanych w języku Python za pomocą pyodbc (Zastąp servername, dbname, nazwę użytkownika i hasła o określonej wartości):</span><span class="sxs-lookup"><span data-stu-id="36fdd-162">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="36fdd-163">Witaj [biblioteki Pandas](http://pandas.pydata.org/) w języku Python zawiera bogaty zestaw struktur danych i narzędzia do analizy danych do manipulowania danymi programowania Python.</span><span class="sxs-lookup"><span data-stu-id="36fdd-163">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="36fdd-164">Poniższy kod Hello odczytuje hello wyników zwrócony z bazy danych programu SQL Server do ramki danych Pandas:</span><span class="sxs-lookup"><span data-stu-id="36fdd-164">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="36fdd-165">Teraz możesz pracować z hello Pandas danych ramki, co opisano w tematach [Tworzenie funkcji dla danych magazynu obiektów blob platformy Azure przy użyciu Panda](machine-learning-data-science-create-features-blob.md).</span><span class="sxs-lookup"><span data-stu-id="36fdd-165">Now you can work with hello Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span></span>

