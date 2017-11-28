---
title: "aaaProcess Azure blob danych za pomocą zaawansowana analityka | Dokumentacja firmy Microsoft"
description: "Przetwarzania danych w magazynie obiektów Blob Azure."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5911d4211c4135680555a8cdd99e745499a24215
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="cd20d-103"><a name="heading"></a>Przetwarzanie danych obiektów blob platformy Azure za pomocą zaawansowana analityka</span><span class="sxs-lookup"><span data-stu-id="cd20d-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="cd20d-104">W tym dokumencie opisano masowej danych i funkcji generowania z danych przechowywanych w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="cd20d-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="cd20d-105">Ładowanie danych hello do ramki danych Pandas</span><span class="sxs-lookup"><span data-stu-id="cd20d-105">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="cd20d-106">W kolejności tooexplore i manipulowania zestawu danych, musi zostać pobrana z hello blob źródła tooa pliku lokalnego, która może zostać załadowana w ramce Pandas danych.</span><span class="sxs-lookup"><span data-stu-id="cd20d-106">In order tooexplore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="cd20d-107">Poniżej przedstawiono hello toofollow kroki do wykonania tej procedury:</span><span class="sxs-lookup"><span data-stu-id="cd20d-107">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="cd20d-108">Pobierz dane hello z platformy Azure blob z hello następującego przykładowego kodu Python za pomocą usługi blob.</span><span class="sxs-lookup"><span data-stu-id="cd20d-108">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="cd20d-109">Zastąp zmienną hello w kodzie hello poniżej określonej wartości:</span><span class="sxs-lookup"><span data-stu-id="cd20d-109">Replace hello variable in hello code below with your specific values:</span></span> 
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. <span data-ttu-id="cd20d-110">Odczyt danych hello w Pandas danych ramkę z hello pobrany plik.</span><span class="sxs-lookup"><span data-stu-id="cd20d-110">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="cd20d-111">Teraz są gotowe tooexplore hello danych i generowanie funkcji dla tego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="cd20d-111">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="cd20d-112"><a name="blob-dataexploration"></a>Eksploracja danych</span><span class="sxs-lookup"><span data-stu-id="cd20d-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="cd20d-113">Oto kilka przykładów tooexplore danych przy użyciu Pandas:</span><span class="sxs-lookup"><span data-stu-id="cd20d-113">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="cd20d-114">Sprawdź hello liczby wierszy i kolumn</span><span class="sxs-lookup"><span data-stu-id="cd20d-114">Inspect hello number of rows and columns</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="cd20d-115">Najpierw sprawdź hello lub ostatni kilka wierszy w elemencie dataset hello, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="cd20d-115">Inspect hello first or last few rows in hello dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="cd20d-116">Sprawdź typ danych hello każdej kolumny zostało zaimportowane jako przy użyciu hello następującego przykładowego kodu</span><span class="sxs-lookup"><span data-stu-id="cd20d-116">Check hello data type each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="cd20d-117">Sprawdź hello podstawowe statystyki hello kolumn w zestawie danych hello w następujący sposób</span><span class="sxs-lookup"><span data-stu-id="cd20d-117">Check hello basic stats for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="cd20d-118">Obejrzyj hello liczbę wpisów dla każdej wartości w kolumnie w następujący sposób</span><span class="sxs-lookup"><span data-stu-id="cd20d-118">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="cd20d-119">Liczba brakujących wartości w zależności od rzeczywistej liczby wpisów w każdej kolumnie, za pomocą następującego przykładowego kodu hello hello</span><span class="sxs-lookup"><span data-stu-id="cd20d-119">Count missing values versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="cd20d-120">Jeśli brakuje wartości dla określonej kolumny w danych hello, musisz porzucić je w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cd20d-120">If you have missing values for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="cd20d-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="cd20d-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="cd20d-122">Inny sposób tooreplace brakujące wartości jest funkcją tryb hello:</span><span class="sxs-lookup"><span data-stu-id="cd20d-122">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="cd20d-123">dataframe_blobdata_mode = dataframe_blobdata.fillna ({< nazwa_kolumny >: .mode()[0]}) dataframe_blobdata ["< nazwa_kolumny >"]</span><span class="sxs-lookup"><span data-stu-id="cd20d-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="cd20d-124">Utwórz wykres histogramu przy użyciu zmiennej liczby bins tooplot hello dystrybucji zmiennej</span><span class="sxs-lookup"><span data-stu-id="cd20d-124">Create a histogram plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="cd20d-125">Przyjrzyj się korelacji między zmienne przy użyciu scatterplot lub hello korelacji wbudowanych funkcji</span><span class="sxs-lookup"><span data-stu-id="cd20d-125">Look at correlations between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="cd20d-126"><a name="blob-featuregen"></a>Funkcja generowania</span><span class="sxs-lookup"><span data-stu-id="cd20d-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="cd20d-127">Firma Microsoft może wygenerować funkcji za pomocą języka Python w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cd20d-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="cd20d-128"><a name="blob-countfeature"></a>Funkcja generowania na podstawie wartości wskaźnika</span><span class="sxs-lookup"><span data-stu-id="cd20d-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="cd20d-129">Podzielone na kategorie funkcji można utworzyć w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cd20d-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="cd20d-130">Sprawdź dystrybucji hello hello kolumny podzielone na kategorie:</span><span class="sxs-lookup"><span data-stu-id="cd20d-130">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="cd20d-131">Generowanie wartości wskaźnika dla każdej wartości w kolumnie hello</span><span class="sxs-lookup"><span data-stu-id="cd20d-131">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="cd20d-132">Dołącz kolumny wskaźnik hello hello oryginalne dane ramki</span><span class="sxs-lookup"><span data-stu-id="cd20d-132">Join hello indicator column with hello original data frame</span></span> 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="cd20d-133">Usuń samej zmiennej hello oryginalnego:</span><span class="sxs-lookup"><span data-stu-id="cd20d-133">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="cd20d-134"><a name="blob-binningfeature"></a>Funkcja generowania binning</span><span class="sxs-lookup"><span data-stu-id="cd20d-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="cd20d-135">Podczas generowania binned funkcje, możemy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cd20d-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="cd20d-136">Dodaj sekwencję toobin kolumny liczbowej</span><span class="sxs-lookup"><span data-stu-id="cd20d-136">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="cd20d-137">Konwertuj binning sekwencji tooa logiczna zmiennych</span><span class="sxs-lookup"><span data-stu-id="cd20d-137">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="cd20d-138">Na koniec sprzężenia hello fikcyjny zmienne kopii toohello oryginalne dane ramki</span><span class="sxs-lookup"><span data-stu-id="cd20d-138">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="cd20d-139"><a name="sql-featuregen"></a>Zapisywanie danych kopii tooAzure obiektów blob i korzystanie z usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cd20d-139"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="cd20d-140">Po przedstawione hello danych i utworzyć hello funkcji niezbędnych możesz przekazać dane hello (próbkowany lub featurized) tooan Azure blob i używać go w usłudze Azure Machine Learning przy użyciu hello następujące kroki: należy pamiętać, że można tworzyć dodatkowe funkcje w hello Azure Machine Learning Studio również.</span><span class="sxs-lookup"><span data-stu-id="cd20d-140">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="cd20d-141">Zapisać hello danych ramki toolocal pliku</span><span class="sxs-lookup"><span data-stu-id="cd20d-141">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="cd20d-142">Przekaż obiekt blob tooAzure danych hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cd20d-142">Upload hello data tooAzure blob as follows:</span></span>
   
        from azure.storage.blob import BlobService
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
3. <span data-ttu-id="cd20d-143">Teraz hello dane mogą zostać odczytane z hello obiektów blob za pomocą usługi Azure Machine Learning hello [i zaimportuj dane] [ import-data] modułu, jak pokazano na poniższym zrzucie ekranu hello:</span><span class="sxs-lookup"><span data-stu-id="cd20d-143">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data][import-data] module as shown in hello screen below:</span></span>

![Czytnik obiektów blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

