---
title: Eksplorowanie danych w maszynie wirtualnej serwera SQL na platformie Azure | Dokumentacja firmy Microsoft
description: "Jak eksplorować dane przechowywane na maszynie Wirtualnej z programu SQL Server na platformie Azure."
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
ms.openlocfilehash: a2be21ef15b9209db1e97150e0297558fa69a7be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="5047b-103">Eksplorowanie danych maszyny wirtualnej programu SQL Server na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5047b-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="5047b-104">W tym dokumencie opisano sposób eksplorować dane przechowywane na maszynie Wirtualnej z programu SQL Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5047b-104">This document covers how to explore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="5047b-105">Można to zrobić przy użyciu języka programowania, takich jak Python lub wrangling danych przy użyciu programu SQL.</span><span class="sxs-lookup"><span data-stu-id="5047b-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="5047b-106">Następujące **menu** linki do tematów opisujących sposób użycia narzędzia, aby eksplorować dane w różnych środowiskach magazynu.</span><span class="sxs-lookup"><span data-stu-id="5047b-106">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="5047b-107">To zadanie jest krokiem w procesie Analytics Cortana (CAP).</span><span class="sxs-lookup"><span data-stu-id="5047b-107">This task is a step in the Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="5047b-108">Instrukcje SQL próbki w tym dokumencie założono, że dane są w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5047b-108">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="5047b-109">Jeśli nie, zajrzyj do mapy procesu chmury danych nauki, aby dowiedzieć się, jak przenieść dane do programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5047b-109">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="5047b-110"><a name="sql-dataexploration"></a>Eksplorowanie danych SQL za pomocą skryptów SQL</span><span class="sxs-lookup"><span data-stu-id="5047b-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="5047b-111">Poniżej przedstawiono kilka przykładowe skrypty SQL, które mogą służyć do eksplorowania magazyny danych w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5047b-111">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

1. <span data-ttu-id="5047b-112">Zliczanie uwagi na dzień</span><span class="sxs-lookup"><span data-stu-id="5047b-112">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="5047b-113">Pobierz poziomy w kolumnie podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="5047b-113">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="5047b-114">Pobierz liczbę poziomów w połączeniu z dwóch kolumn podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="5047b-114">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="5047b-115">Pobierz dystrybucji dla kolumn wartości liczbowych</span><span class="sxs-lookup"><span data-stu-id="5047b-115">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="5047b-116">Na przykład praktyczne, można użyć [dataset taksówki NYC](http://www.andresmh.com/nyctaxitrips/) i zapoznaj się z IPNB zatytułowany [wrangling NYC danych za pomocą notesu IPython i SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) dla przewodnika end-to-end.</span><span class="sxs-lookup"><span data-stu-id="5047b-116">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="5047b-117"><a name="python"></a>Eksplorowanie danych SQL za pomocą języka Python</span><span class="sxs-lookup"><span data-stu-id="5047b-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="5047b-118">Przy użyciu języka Python do Eksplorowanie danych oraz do generowania funkcji, jeśli dane są w programie SQL Server jest podobny do przetwarzania danych obiektów blob platformy Azure przy użyciu języka Python, zgodnie z opisem w [danych obiektów Blob platformy Azure procesu w danym środowisku nauki danych](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="5047b-118">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="5047b-119">Dane powinna być załadowana z bazy danych do pandas DataFrame, a następnie mogą być dalej przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="5047b-119">The data needs to be loaded from the database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="5047b-120">Proces łączenia z bazą danych i ładowania danych do DataFrame w tej sekcji możemy dokumentu.</span><span class="sxs-lookup"><span data-stu-id="5047b-120">We document the process of connecting to the database and loading the data into the DataFrame in this section.</span></span>

<span data-ttu-id="5047b-121">Następującego formatu ciągu połączenia może służyć do połączenia z bazą danych programu SQL Server w języku Python za pomocą pyodbc (Zastąp servername, dbname nazwy użytkownika i hasła o określonej wartości):</span><span class="sxs-lookup"><span data-stu-id="5047b-121">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="5047b-122">[Biblioteki Pandas](http://pandas.pydata.org/) w języku Python zawiera bogaty zestaw struktur danych i narzędzia do analizy danych do manipulowania danymi programowania Python.</span><span class="sxs-lookup"><span data-stu-id="5047b-122">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="5047b-123">Poniższy kod odczytuje wyniki zwracane z bazy danych programu SQL Server do ramki danych Pandas:</span><span class="sxs-lookup"><span data-stu-id="5047b-123">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="5047b-124">Teraz możesz pracować z Pandas DataFrame, jak to opisano w temacie [danych obiektów Blob platformy Azure procesu w danym środowisku nauki danych](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="5047b-124">Now you can work with the Pandas DataFrame as covered in the topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="5047b-125">Proces Cortana analityka w przykładzie akcji</span><span class="sxs-lookup"><span data-stu-id="5047b-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="5047b-126">Aby proces Analytics Cortana, przy użyciu publicznego zestawu danych, na przykład na trasie wskazówki, zobacz [zespołu danych nauki procesu w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5047b-126">For an end-to-end walkthrough example of the Cortana Analytics Process using a public dataset, see [The Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

