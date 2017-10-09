---
title: "Funkcje aaaCreate dla usługi Azure blob magazynu danych przy użyciu Panda | Dokumentacja firmy Microsoft"
description: "Jak toocreate funkcji dla danych przechowywanych w kontenerze obiektów blob platformy Azure z pakietem Panda Python hello."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 676b5fb0-4c89-4516-b3a8-e78ae3ca078d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: 8594046c5d76a36ad87fc77e407752489d30afcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="5b079-103">Tworzenie funkcji dla danych usługi Azure Blob Storage za pomocą usługi Panda</span><span class="sxs-lookup"><span data-stu-id="5b079-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="5b079-104">Ten dokument przedstawia sposób toocreate funkcji dla danych przechowywanych w kontenerze obiektów blob platformy Azure przy użyciu hello [Pandas](http://pandas.pydata.org/) pakiet języka Python.</span><span class="sxs-lookup"><span data-stu-id="5b079-104">This document shows how toocreate features for data that is stored in Azure blob container using hello [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="5b079-105">Po zwijania jak tooload hello danych do ramki danych Panda, widoczny jest sposób toogenerate podzielone na kategorie funkcji za pomocą skryptów języka Python z wartościami wskaźnik i binning funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b079-105">After outlining how tooload hello data into a Panda data frame, it shows how toogenerate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="5b079-106">To **menu** łączy tootopics, które opisują sposób toocreate funkcji dla danych w różnych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="5b079-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="5b079-107">To zadanie jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="5b079-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b079-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5b079-108">Prerequisites</span></span>
<span data-ttu-id="5b079-109">W tym artykule założono, że utworzono konto magazynu obiektów blob platformy Azure i przechowywanych danych istnieje.</span><span class="sxs-lookup"><span data-stu-id="5b079-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="5b079-110">Aby uzyskać instrukcje tooset konta, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="5b079-110">If you need instructions tooset up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="5b079-111">Ładowanie danych hello do ramki danych Pandas</span><span class="sxs-lookup"><span data-stu-id="5b079-111">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="5b079-112">W kolejności toodo Eksploruj i manipulowania zestawu danych, musi zostać pobrana z hello blob źródła tooa pliku lokalnego, która może zostać załadowana w ramce Pandas danych.</span><span class="sxs-lookup"><span data-stu-id="5b079-112">In order toodo explore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="5b079-113">Poniżej przedstawiono hello toofollow kroki do wykonania tej procedury:</span><span class="sxs-lookup"><span data-stu-id="5b079-113">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="5b079-114">Pobierz dane hello z platformy Azure blob z hello następującego przykładowego kodu Python za pomocą usługi blob.</span><span class="sxs-lookup"><span data-stu-id="5b079-114">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="5b079-115">Zastąp zmienną hello w kodzie hello poniżej określonej wartości:</span><span class="sxs-lookup"><span data-stu-id="5b079-115">Replace hello variable in hello code below with your specific values:</span></span>
   
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
2. <span data-ttu-id="5b079-116">Odczyt danych hello w Pandas danych ramkę z hello pobrany plik.</span><span class="sxs-lookup"><span data-stu-id="5b079-116">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="5b079-117">Teraz są gotowe tooexplore hello danych i generowanie funkcji dla tego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="5b079-117">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="5b079-118"><a name="blob-featuregen"></a>Funkcja generowania</span><span class="sxs-lookup"><span data-stu-id="5b079-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="5b079-119">Witaj w dwóch następnych sekcjach pokazują, jak toogenerate podzielone na kategorie funkcji z wartościami wskaźnik i binning funkcji za pomocą skryptów języka Python.</span><span class="sxs-lookup"><span data-stu-id="5b079-119">hello next two sections show how toogenerate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="5b079-120"><a name="blob-countfeature"></a>Funkcja generowania na podstawie wartości wskaźnika</span><span class="sxs-lookup"><span data-stu-id="5b079-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="5b079-121">Podzielone na kategorie funkcji można utworzyć w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5b079-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="5b079-122">Sprawdź dystrybucji hello hello kolumny podzielone na kategorie:</span><span class="sxs-lookup"><span data-stu-id="5b079-122">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="5b079-123">Generowanie wartości wskaźnika dla każdej wartości w kolumnie hello</span><span class="sxs-lookup"><span data-stu-id="5b079-123">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="5b079-124">Dołącz kolumny wskaźnik hello hello oryginalne dane ramki</span><span class="sxs-lookup"><span data-stu-id="5b079-124">Join hello indicator column with hello original data frame</span></span>
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="5b079-125">Usuń samej zmiennej hello oryginalnego:</span><span class="sxs-lookup"><span data-stu-id="5b079-125">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="5b079-126"><a name="blob-binningfeature"></a>Funkcja generowania binning</span><span class="sxs-lookup"><span data-stu-id="5b079-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="5b079-127">Podczas generowania binned funkcje, możemy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5b079-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="5b079-128">Dodaj sekwencję toobin kolumny liczbowej</span><span class="sxs-lookup"><span data-stu-id="5b079-128">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="5b079-129">Konwertuj binning sekwencji tooa logiczna zmiennych</span><span class="sxs-lookup"><span data-stu-id="5b079-129">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="5b079-130">Na koniec sprzężenia hello fikcyjny zmienne kopii toohello oryginalne dane ramki</span><span class="sxs-lookup"><span data-stu-id="5b079-130">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="5b079-131"><a name="sql-featuregen"></a>Zapisywanie danych kopii tooAzure obiektów blob i korzystanie z usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5b079-131"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="5b079-132">Po przedstawione hello danych i utworzyć hello funkcji niezbędnych możesz przekazać dane hello (próbkowany lub featurized) tooan Azure blob i używać go w usłudze Azure Machine Learning przy użyciu hello następujące kroki: należy pamiętać, że można tworzyć dodatkowe funkcje w hello Azure Machine Learning Studio również.</span><span class="sxs-lookup"><span data-stu-id="5b079-132">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="5b079-133">Zapisać hello danych ramki toolocal pliku</span><span class="sxs-lookup"><span data-stu-id="5b079-133">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="5b079-134">Przekaż obiekt blob tooAzure danych hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5b079-134">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="5b079-135">Teraz hello dane mogą zostać odczytane z hello obiektów blob za pomocą usługi Azure Machine Learning hello [i zaimportuj dane](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) modułu, jak pokazano na poniższym zrzucie ekranu hello:</span><span class="sxs-lookup"><span data-stu-id="5b079-135">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in hello screen below:</span></span>

![Czytnik obiektów blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

