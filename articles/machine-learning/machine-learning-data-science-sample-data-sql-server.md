---
title: aaaSample danych w programie SQL Server na platformie Azure | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="77e99-103"><a name="heading"></a>Przykładowe dane w programie SQL Server na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="77e99-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="77e99-104">Tym dokumencie przedstawiono sposób przechowywania danych toosample w programie SQL Server na platformie Azure przy użyciu SQL lub hello język programowania Python.</span><span class="sxs-lookup"><span data-stu-id="77e99-104">This document shows how toosample data stored in SQL Server on Azure using either SQL or hello Python programming language.</span></span> <span data-ttu-id="77e99-105">Pokazuje też, jak toomove próbce danych do usługi Azure Machine Learning przez zapisanie go w pliku tooa, przekazać go tooan obiektów blob platformy Azure, a następnie odczytanie go do usługi Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="77e99-105">It also shows how toomove sampled data into Azure Machine Learning by saving it tooa file, uploading it tooan Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="77e99-106">próbkowanie Python Hello używa hello [pyodbc](https://code.google.com/p/pyodbc/) tooSQL tooconnect biblioteki ODBC serwera na platformie Azure i hello [Pandas](http://pandas.pydata.org/) biblioteki toodo hello próbkowania.</span><span class="sxs-lookup"><span data-stu-id="77e99-106">hello Python sampling uses hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC library tooconnect tooSQL Server on Azure and hello [Pandas](http://pandas.pydata.org/) library toodo hello sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="77e99-107">Hello przykładowy SQL kod w tym dokumencie przyjęto założenie, że hello jest danych w programie SQL Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="77e99-107">hello sample SQL code in this document assumes that hello data is in a SQL Server on Azure.</span></span> <span data-ttu-id="77e99-108">Jeśli nie jest dostępne, można znaleźć za[przenoszenia danych tooSQL Server na platformie Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) tematu, aby uzyskać instrukcje dotyczące toomove Twojego tooSQL danych serwera na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="77e99-108">If it is not, please refer too[Move data tooSQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how toomove your data tooSQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="77e99-109">następujące Hello **menu** łączy tootopics, które opisują sposób toosample danych z różnych środowiskach magazynu.</span><span class="sxs-lookup"><span data-stu-id="77e99-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="77e99-110">**Dlaczego przykładowe dane?**</span><span class="sxs-lookup"><span data-stu-id="77e99-110">**Why sample your data?**</span></span>
<span data-ttu-id="77e99-111">Jeśli planujesz tooanalyze dataset hello jest duży, zazwyczaj jest to dobrze hello toodown przykładowych danych tooreduce jego rozmiar tooa mniejsze, ale reprezentatywny i łatwiejsze w zarządzaniu.</span><span class="sxs-lookup"><span data-stu-id="77e99-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="77e99-112">To ułatwia zrozumienie danych, badanie i inżynieria funkcji.</span><span class="sxs-lookup"><span data-stu-id="77e99-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="77e99-113">Swoją rolę w hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) jest szybkie tworzenie prototypów tooenable hello przetwarzania danych funkcji i modeli uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="77e99-113">Its role in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="77e99-114">To zadanie próbkowania jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="77e99-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="77e99-115"><a name="SQL"></a>Przy użyciu programu SQL</span><span class="sxs-lookup"><span data-stu-id="77e99-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="77e99-116">W tej sekcji opisano kilka metod za pomocą tooperform SQL pobieranie próbek losowych hello danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="77e99-116">This section describes several methods using SQL tooperform simple random sampling against hello data in hello database.</span></span> <span data-ttu-id="77e99-117">Wybierz metodę, w oparciu o rozmiar danych i jego dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="77e99-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="77e99-118">Poniższe elementy dwóch Hello pokazują, jak newid toouse w tooperform programu SQL Server hello próbkowania.</span><span class="sxs-lookup"><span data-stu-id="77e99-118">hello two items below show how toouse newid in SQL Server tooperform hello sampling.</span></span> <span data-ttu-id="77e99-119">Hello metody zależy od sposobu losowe hello próbki toobe (pk_id w hello przykładowy kod poniżej przyjęto toobe automatycznego generowania klucza podstawowego).</span><span class="sxs-lookup"><span data-stu-id="77e99-119">hello method you choose depends on how random you want hello sample toobe (pk_id in hello sample code below is assumed toobe an auto-generated primary key).</span></span>

1. <span data-ttu-id="77e99-120">Mniej rygorystyczne losowej próbki</span><span class="sxs-lookup"><span data-stu-id="77e99-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="77e99-121">Więcej losowej próbki</span><span class="sxs-lookup"><span data-stu-id="77e99-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="77e99-122">Tablesample może być użyta do próbkowania także przedstawiona poniżej.</span><span class="sxs-lookup"><span data-stu-id="77e99-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="77e99-123">Może to być lepszym rozwiązaniem Jeśli rozmiar danych jest duży (przy założeniu, że nie jest skorelowany danych na różnych stronach) i toocomplete zapytania hello w odpowiednim czasie.</span><span class="sxs-lookup"><span data-stu-id="77e99-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for hello query toocomplete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="77e99-124">Można eksplorować i generowanie funkcji z tej próbki danych przez zapisanie go w nowej tabeli</span><span class="sxs-lookup"><span data-stu-id="77e99-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="77e99-125"><a name="sql-aml"></a>Łączenie tooAzure uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="77e99-125"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="77e99-126">Możesz bezpośrednio użyć hello przykładowe zapytania powyżej w hello Azure Machine Learning [i zaimportuj dane] [ import-data] modułu hello toodown przykładowe dane na powitania udać i przełączyć go do eksperymentu uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="77e99-126">You can directly  use hello sample queries above in hello Azure Machine Learning [Import Data][import-data] module toodown-sample hello data on hello fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="77e99-127">Poniżej przedstawiono zrzut ekranu przy użyciu hello czytnika modułu tooread hello próbkowany danych:</span><span class="sxs-lookup"><span data-stu-id="77e99-127">A screen shot of using hello reader module tooread hello sampled data is shown below:</span></span>

![Czytnik sql][1]

## <span data-ttu-id="77e99-129"><a name="python"></a>Przy użyciu języka programowania Python hello</span><span class="sxs-lookup"><span data-stu-id="77e99-129"><a name="python"></a>Using hello Python programming language</span></span>
<span data-ttu-id="77e99-130">W tej sekcji przedstawiono przy użyciu hello [biblioteki pyodbc](https://code.google.com/p/pyodbc/) tooestablish ODBC połączyć tooa bazy danych serwera SQL w języku Python.</span><span class="sxs-lookup"><span data-stu-id="77e99-130">This section demonstrates using hello [pyodbc library](https://code.google.com/p/pyodbc/) tooestablish an ODBC connect tooa SQL server database in Python.</span></span> <span data-ttu-id="77e99-131">Parametry połączenia bazy danych Hello jest następująca: (zamiast servername, dbname, nazwę użytkownika i hasło z konfiguracją):</span><span class="sxs-lookup"><span data-stu-id="77e99-131">hello database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="77e99-132">Witaj [Pandas](http://pandas.pydata.org/) biblioteki w języku Python zawiera bogaty zestaw struktur danych i narzędzia do analizy danych do manipulowania danymi programowania Python.</span><span class="sxs-lookup"><span data-stu-id="77e99-132">hello [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="77e99-133">Poniższy kod Hello odczytuje próbkę 0,1% hello danych z tabeli w bazie danych Azure SQL w danych Pandas:</span><span class="sxs-lookup"><span data-stu-id="77e99-133">hello code below reads a 0.1% sample of hello data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="77e99-134">Teraz możesz pracować z danymi hello próbkowany hello Pandas danych ramki.</span><span class="sxs-lookup"><span data-stu-id="77e99-134">You can now work with hello sampled data in hello Pandas data frame.</span></span> 

### <span data-ttu-id="77e99-135"><a name="python-aml"></a>Łączenie tooAzure uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="77e99-135"><a name="python-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="77e99-136">Można użyć następującego przykładowego kodu toosave hello danych próbkowania w dół tooa pliku hello i przekaż go tooan obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77e99-136">You can use hello following sample code toosave hello down-sampled data tooa file and upload it tooan Azure blob.</span></span> <span data-ttu-id="77e99-137">Hello dane w obiekcie blob hello może być bezpośrednio odczytane do eksperymentu Azure Machine Learning przy użyciu hello [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="77e99-137">hello data in hello blob can be directly read into an Azure Machine Learning Experiment using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="77e99-138">Witaj obejmuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="77e99-138">hello steps are as follows:</span></span> 

1. <span data-ttu-id="77e99-139">Zapis hello pandas danych ramki tooa lokalnego pliku</span><span class="sxs-lookup"><span data-stu-id="77e99-139">Write hello pandas data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="77e99-140">Przekazywanie pliku lokalnego tooAzure blob</span><span class="sxs-lookup"><span data-stu-id="77e99-140">Upload local file tooAzure blob</span></span>
   
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
3. <span data-ttu-id="77e99-141">Odczytywanie danych z obiektów blob platformy Azure przy użyciu usługi Azure Machine Learning [i zaimportuj dane] [ import-data] modułu, jak pokazano poniżej Przechwyć ekranie powitania:</span><span class="sxs-lookup"><span data-stu-id="77e99-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in hello screen grab below:</span></span>

![Czytnik obiektów blob][2]

## <a name="hello-team-data-science-process-in-action-example"></a><span data-ttu-id="77e99-143">Witaj proces nauki danych zespołu w przykładzie akcji</span><span class="sxs-lookup"><span data-stu-id="77e99-143">hello Team Data Science Process in Action example</span></span>
<span data-ttu-id="77e99-144">Przykład wskazówki na trasie hello proces nauki danych Team publicznego zestawu danych, przy użyciu zobacz [proces nauki danych zespołu w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="77e99-144">For an end-to-end walkthrough example of hello Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
