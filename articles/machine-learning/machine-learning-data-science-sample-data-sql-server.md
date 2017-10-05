---
title: "Przykładowe dane w programie SQL Server na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przykładowe dane w programie SQL Server na platformie Azure"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 1bdcc7175dac325de1144d805e977264524b3fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="b8187-103"><a name="heading"></a>Przykładowe dane w programie SQL Server na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b8187-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="b8187-104">Ten dokument zamieszczono przykładowe dane przechowywane w programie SQL Server na platformie Azure przy użyciu SQL lub języka programowania Python.</span><span class="sxs-lookup"><span data-stu-id="b8187-104">This document shows how to sample data stored in SQL Server on Azure using either SQL or the Python programming language.</span></span> <span data-ttu-id="b8187-105">Ponadto jak przenieść próbki danych do usługi Azure Machine Learning przez zapisanie go w pliku, przekazać go do obiektów blob platformy Azure i odczytywania go do usługi Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="b8187-105">It also shows how to move sampled data into Azure Machine Learning by saving it to a file, uploading it to an Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="b8187-106">Używa języka Python próbkowania [pyodbc](https://code.google.com/p/pyodbc/) ODBC — Biblioteka nawiązać połączenia z programem SQL Server na platformie Azure i [Pandas](http://pandas.pydata.org/) biblioteki w celu pobierania próbek.</span><span class="sxs-lookup"><span data-stu-id="b8187-106">The Python sampling uses the [pyodbc](https://code.google.com/p/pyodbc/) ODBC library to connect to SQL Server on Azure and the [Pandas](http://pandas.pydata.org/) library to do the sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="b8187-107">Przykładowy kod SQL w tym dokumencie przyjęto założenie, że dane są w programie SQL Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b8187-107">The sample SQL code in this document assumes that the data is in a SQL Server on Azure.</span></span> <span data-ttu-id="b8187-108">Jeśli nie jest, zapoznaj się [przenoszenie danych do programu SQL Server na platformie Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) tematu, aby uzyskać instrukcje dotyczące sposobu przenoszenia danych do programu SQL Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b8187-108">If it is not, please refer to [Move data to SQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how to move your data to SQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="b8187-109">Następujące **menu** linki do tematów opisujących sposób przykładowe dane z różnych środowiskach magazynu.</span><span class="sxs-lookup"><span data-stu-id="b8187-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="b8187-110">**Dlaczego przykładowe dane?**</span><span class="sxs-lookup"><span data-stu-id="b8187-110">**Why sample your data?**</span></span>
<span data-ttu-id="b8187-111">Jeśli zestaw danych, które mają być analizowanie jest duży, zazwyczaj jest dobrym rozwiązaniem w dół przykładowych danych, aby zmniejszyć jego rozmiar mniejsze, ale reprezentatywny i łatwiejsze w zarządzaniu.</span><span class="sxs-lookup"><span data-stu-id="b8187-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="b8187-112">To ułatwia zrozumienie danych, badanie i inżynieria funkcji.</span><span class="sxs-lookup"><span data-stu-id="b8187-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="b8187-113">Swoją rolę w [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) jest umożliwienie szybkiego prototypy funkcji przetwarzania danych i modeli uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="b8187-113">Its role in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="b8187-114">To zadanie próbkowania jest krokiem w [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="b8187-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="b8187-115"><a name="SQL"></a>Przy użyciu programu SQL</span><span class="sxs-lookup"><span data-stu-id="b8187-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="b8187-116">W tej sekcji opisano kilka metod, aby wykonać pobieranie próbek losowych z danymi w bazie danych przy użyciu programu SQL.</span><span class="sxs-lookup"><span data-stu-id="b8187-116">This section describes several methods using SQL to perform simple random sampling against the data in the database.</span></span> <span data-ttu-id="b8187-117">Wybierz metodę, w oparciu o rozmiar danych i jego dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="b8187-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="b8187-118">Dwa poniższe elementy pokazują, jak używać newid w programie SQL Server do wykonywania próbki.</span><span class="sxs-lookup"><span data-stu-id="b8187-118">The two items below show how to use newid in SQL Server to perform the sampling.</span></span> <span data-ttu-id="b8187-119">Wybór metody zależy od sposobu losowej próbki w celu (pk_id w poniższym przykładowym kodzie zakłada się, że klucz podstawowy generowane automatycznie).</span><span class="sxs-lookup"><span data-stu-id="b8187-119">The method you choose depends on how random you want the sample to be (pk_id in the sample code below is assumed to be an auto-generated primary key).</span></span>

1. <span data-ttu-id="b8187-120">Mniej rygorystyczne losowej próbki</span><span class="sxs-lookup"><span data-stu-id="b8187-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="b8187-121">Więcej losowej próbki</span><span class="sxs-lookup"><span data-stu-id="b8187-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="b8187-122">Tablesample może być użyta do próbkowania także przedstawiona poniżej.</span><span class="sxs-lookup"><span data-stu-id="b8187-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="b8187-123">Może to być lepszym rozwiązaniem, jeśli rozmiar danych jest duży (przy założeniu, że nie jest skorelowany danych na różnych stronach) i dla zapytania do wykonania w odpowiednim czasie.</span><span class="sxs-lookup"><span data-stu-id="b8187-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for the query to complete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="b8187-124">Można eksplorować i generowanie funkcji z tej próbki danych przez zapisanie go w nowej tabeli</span><span class="sxs-lookup"><span data-stu-id="b8187-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="b8187-125"><a name="sql-aml"></a>Nawiązywanie połączenia z usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b8187-125"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="b8187-126">Przykładowe zapytania powyżej można używać bezpośrednio w usłudze Azure Machine Learning [i zaimportuj dane] [ import-data] moduł dół przykładowe dane na bieżąco i przełączyć go do eksperymentu uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="b8187-126">You can directly  use the sample queries above in the Azure Machine Learning [Import Data][import-data] module to down-sample the data on the fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="b8187-127">Poniżej przedstawiono zrzut ekranu przy użyciu modułu czytnik do odczytu próbki danych:</span><span class="sxs-lookup"><span data-stu-id="b8187-127">A screen shot of using the reader module to read the sampled data is shown below:</span></span>

![Czytnik sql][1]

## <span data-ttu-id="b8187-129"><a name="python"></a>Przy użyciu języka programowania Python</span><span class="sxs-lookup"><span data-stu-id="b8187-129"><a name="python"></a>Using the Python programming language</span></span>
<span data-ttu-id="b8187-130">W tej sekcji przedstawiono przy użyciu [biblioteki pyodbc](https://code.google.com/p/pyodbc/) do ustanawiania połączenia ODBC w bazie danych programu SQL server w języku Python.</span><span class="sxs-lookup"><span data-stu-id="b8187-130">This section demonstrates using the [pyodbc library](https://code.google.com/p/pyodbc/) to establish an ODBC connect to a SQL server database in Python.</span></span> <span data-ttu-id="b8187-131">Parametry połączenia bazy danych jest następujący: (zamiast servername, dbname, nazwę użytkownika i hasło z konfiguracją):</span><span class="sxs-lookup"><span data-stu-id="b8187-131">The database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="b8187-132">[Pandas](http://pandas.pydata.org/) biblioteki w języku Python zawiera bogaty zestaw struktur danych i narzędzia do analizy danych do manipulowania danymi programowania Python.</span><span class="sxs-lookup"><span data-stu-id="b8187-132">The [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="b8187-133">Poniższy kod odczytuje 0,1% próbkę danych z tabeli w bazie danych Azure SQL w danych Pandas:</span><span class="sxs-lookup"><span data-stu-id="b8187-133">The code below reads a 0.1% sample of the data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="b8187-134">Teraz możesz pracować z próbki danych w ramce Pandas danych.</span><span class="sxs-lookup"><span data-stu-id="b8187-134">You can now work with the sampled data in the Pandas data frame.</span></span> 

### <span data-ttu-id="b8187-135"><a name="python-aml"></a>Nawiązywanie połączenia z usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b8187-135"><a name="python-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="b8187-136">Następujący przykładowy kod umożliwia zapisują dane próbkowania w dół do pliku i przekaż go do obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b8187-136">You can use the following sample code to save the down-sampled data to a file and upload it to an Azure blob.</span></span> <span data-ttu-id="b8187-137">Dane w obiekcie blob mogą bezpośrednio odczytywać do eksperymentu Azure Machine Learning przy użyciu [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="b8187-137">The data in the blob can be directly read into an Azure Machine Learning Experiment using the [Import Data][import-data] module.</span></span> <span data-ttu-id="b8187-138">Dostępne są następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b8187-138">The steps are as follows:</span></span> 

1. <span data-ttu-id="b8187-139">Zapis pandas ramki danych do pliku lokalnego</span><span class="sxs-lookup"><span data-stu-id="b8187-139">Write the pandas data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="b8187-140">Przekazywanie pliku lokalnego do obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b8187-140">Upload local file to Azure blob</span></span>
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="b8187-141">Odczytywanie danych z obiektów blob platformy Azure przy użyciu usługi Azure Machine Learning [i zaimportuj dane] [ import-data] modułu, jak pokazano poniżej Przechwyć ekranu:</span><span class="sxs-lookup"><span data-stu-id="b8187-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in the screen grab below:</span></span>

![Czytnik obiektów blob][2]

## <a name="the-team-data-science-process-in-action-example"></a><span data-ttu-id="b8187-143">Proces nauki danych zespołu w przykładzie akcji</span><span class="sxs-lookup"><span data-stu-id="b8187-143">The Team Data Science Process in Action example</span></span>
<span data-ttu-id="b8187-144">Przykład end-to-end wskazówki procesu nauki danych Team publicznego zestawu danych, przy użyciu zobacz [proces nauki danych zespołu w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="b8187-144">For an end-to-end walkthrough example of the Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
