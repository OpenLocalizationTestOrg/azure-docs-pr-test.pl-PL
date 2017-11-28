---
title: aaaExplore danych maszyny wirtualnej w programu SQL Server na platformie Azure | Dokumentacja firmy Microsoft
description: Jak tooexplore dane przechowywane na maszynie Wirtualnej z programu SQL Server na platformie Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="54902-103">Eksplorowanie danych maszyny wirtualnej programu SQL Server na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="54902-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="54902-104">W tym dokumencie opisano sposób tooexplore dane przechowywane na maszynie Wirtualnej z programu SQL Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="54902-104">This document covers how tooexplore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="54902-105">Można to zrobić przy użyciu języka programowania, takich jak Python lub wrangling danych przy użyciu programu SQL.</span><span class="sxs-lookup"><span data-stu-id="54902-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="54902-106">następujące Hello **menu** łączy tootopics opisujące, jak toouse narzędzia tooexplore danych z różnych środowiskach magazynu.</span><span class="sxs-lookup"><span data-stu-id="54902-106">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="54902-107">To zadanie jest etapem hello Cortana Analytics procesu (CAP).</span><span class="sxs-lookup"><span data-stu-id="54902-107">This task is a step in hello Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="54902-108">instrukcje SQL próbki Hello w tym dokumencie założono, że dane są w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54902-108">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="54902-109">Jeśli nie, zobacz toohello chmury danych nauki procesu mapy toolearn jak toomove Twojego tooSQL danych serwera.</span><span class="sxs-lookup"><span data-stu-id="54902-109">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="54902-110"><a name="sql-dataexploration"></a>Eksplorowanie danych SQL za pomocą skryptów SQL</span><span class="sxs-lookup"><span data-stu-id="54902-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="54902-111">Poniżej przedstawiono kilka przykładowe skrypty SQL, które mogą być używane tooexplore magazyny danych w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54902-111">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

1. <span data-ttu-id="54902-112">Zliczanie hello uwagi na dzień</span><span class="sxs-lookup"><span data-stu-id="54902-112">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="54902-113">Pobierz poziomy hello w kolumnie podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="54902-113">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="54902-114">Pobierz hello podaną liczbę poziomów w połączeniu z dwóch kolumn podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="54902-114">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="54902-115">Pobierz dystrybucji hello kolumn wartości liczbowych</span><span class="sxs-lookup"><span data-stu-id="54902-115">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="54902-116">Na przykład praktyczne, można użyć hello [dataset taksówki NYC](http://www.andresmh.com/nyctaxitrips/) i odwoływać się toohello IPNB zatytułowany [wrangling NYC danych za pomocą notesu IPython i SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) dla przewodnika end-to-end.</span><span class="sxs-lookup"><span data-stu-id="54902-116">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="54902-117"><a name="python"></a>Eksplorowanie danych SQL za pomocą języka Python</span><span class="sxs-lookup"><span data-stu-id="54902-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="54902-118">Przy użyciu języka Python tooexplore danych i funkcji generowania hello danych jest w programie SQL Server jest podobne tooprocessing dane obiektów blob platformy Azure przy użyciu języka Python, zgodnie z opisem w [danych obiektów Blob platformy Azure procesu w danym środowisku nauki danych](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="54902-118">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="54902-119">dane Hello musi załadować z bazy danych hello do pandas DataFrame toobe i następnie mogą być dalej przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="54902-119">hello data needs toobe loaded from hello database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="54902-120">Firma Microsoft dokumentu hello proces łączenia toohello bazy danych i ładowania danych hello do hello DataFrame w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="54902-120">We document hello process of connecting toohello database and loading hello data into hello DataFrame in this section.</span></span>

<span data-ttu-id="54902-121">Witaj następującego formatu ciągu połączenia może być bazy danych programu SQL Server tooa tooconnect używanych w języku Python za pomocą pyodbc (Zastąp servername, dbname nazwy użytkownika i hasła o określonej wartości):</span><span class="sxs-lookup"><span data-stu-id="54902-121">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="54902-122">Witaj [biblioteki Pandas](http://pandas.pydata.org/) w języku Python zawiera bogaty zestaw struktur danych i narzędzia do analizy danych do manipulowania danymi programowania Python.</span><span class="sxs-lookup"><span data-stu-id="54902-122">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="54902-123">Witaj następujący kod odczytuje hello wyników zwrócony z bazy danych programu SQL Server do ramki danych Pandas:</span><span class="sxs-lookup"><span data-stu-id="54902-123">hello following code reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="54902-124">Teraz możesz pracować z hello Pandas DataFrame, jak to opisano w temacie hello [danych obiektów Blob platformy Azure procesu w danym środowisku nauki danych](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="54902-124">Now you can work with hello Pandas DataFrame as covered in hello topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="54902-125">Proces Cortana analityka w przykładzie akcji</span><span class="sxs-lookup"><span data-stu-id="54902-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="54902-126">Przykład wskazówki na trasie hello Cortana Analytics procesu przy użyciu publicznego zestawu danych, zobacz [hello proces nauki danych zespołu w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="54902-126">For an end-to-end walkthrough example of hello Cortana Analytics Process using a public dataset, see [hello Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

