---
title: aaaExplore danych na platformie Azure blob magazynu z Pandas | Dokumentacja firmy Microsoft
description: "Jak tooexplore dane przechowywane na platformie Azure kontenera obiektów blob przy użyciu Pandas."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="c2547-103">Eksplorowanie danych usługi Azure Blob Storage za pomocą usług Panda</span><span class="sxs-lookup"><span data-stu-id="c2547-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="c2547-104">W tym dokumencie opisano, jak tooexplore dane przechowywane na platformie Azure blob przy użyciu kontenera [Pandas](http://pandas.pydata.org/) pakiet języka Python.</span><span class="sxs-lookup"><span data-stu-id="c2547-104">This document covers how tooexplore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="c2547-105">następujące Hello **menu** łączy tootopics opisujące, jak toouse narzędzia tooexplore danych z różnych środowiskach magazynu.</span><span class="sxs-lookup"><span data-stu-id="c2547-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="c2547-106">To zadanie jest etapem hello [proces nauki danych]().</span><span class="sxs-lookup"><span data-stu-id="c2547-106">This task is a step in hello [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="c2547-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c2547-107">Prerequisites</span></span>
<span data-ttu-id="c2547-108">W tym artykule przyjęto założenie, że masz:</span><span class="sxs-lookup"><span data-stu-id="c2547-108">This article assumes that you have:</span></span>

* <span data-ttu-id="c2547-109">Utworzone konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c2547-109">Created an Azure storage account.</span></span> <span data-ttu-id="c2547-110">Aby uzyskać instrukcje, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="c2547-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="c2547-111">Przechowywane dane na koncie magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c2547-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="c2547-112">Aby uzyskać instrukcje, zobacz [przenoszenie tooand danych z magazynu Azure](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="c2547-112">If you need instructions, see [Moving data tooand from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-hello-data-into-a-pandas-dataframe"></a><span data-ttu-id="c2547-113">Ładowanie danych hello do Pandas DataFrame</span><span class="sxs-lookup"><span data-stu-id="c2547-113">Load hello data into a Pandas DataFrame</span></span>
<span data-ttu-id="c2547-114">tooexplore i manipulowania zestawu danych, najpierw musi zostać pobrana z hello obiektów blob tooa lokalny plik źródłowy, który następnie będzie można załadować Pandas DataFrame.</span><span class="sxs-lookup"><span data-stu-id="c2547-114">tooexplore and manipulate a dataset, it must first be downloaded from hello blob source tooa local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="c2547-115">Poniżej przedstawiono hello toofollow kroki do wykonania tej procedury:</span><span class="sxs-lookup"><span data-stu-id="c2547-115">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="c2547-116">Pobierz dane hello z platformy Azure blob z powitania po przykładowy kod języka Python za pomocą usługi blob.</span><span class="sxs-lookup"><span data-stu-id="c2547-116">Download hello data from Azure blob with hello following Python code sample using blob service.</span></span> <span data-ttu-id="c2547-117">Zastąp zmienną hello w hello następującego kodu przy użyciu określonych wartości:</span><span class="sxs-lookup"><span data-stu-id="c2547-117">Replace hello variable in hello following code with your specific values:</span></span> 
   
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
2. <span data-ttu-id="c2547-118">Odczyt danych hello w Pandas danych ramkę z hello pobrany plik.</span><span class="sxs-lookup"><span data-stu-id="c2547-118">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="c2547-119">Teraz są gotowe tooexplore hello danych i generowanie funkcji dla tego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="c2547-119">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="c2547-120"><a name="blob-dataexploration"></a>Przykłady Eksploracja danych przy użyciu Pandas</span><span class="sxs-lookup"><span data-stu-id="c2547-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="c2547-121">Oto kilka przykładów tooexplore danych przy użyciu Pandas:</span><span class="sxs-lookup"><span data-stu-id="c2547-121">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="c2547-122">Sprawdź hello **liczba wierszy i kolumn**</span><span class="sxs-lookup"><span data-stu-id="c2547-122">Inspect hello **number of rows and columns**</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="c2547-123">**Sprawdź** hello kilka pierwszego lub ostatniego **wierszy** w hello następującego zestawu danych:</span><span class="sxs-lookup"><span data-stu-id="c2547-123">**Inspect** hello first or last few **rows** in hello following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="c2547-124">Sprawdź hello **— typ danych** każda kolumna została zaimportowana jako przy użyciu hello następującego przykładowego kodu</span><span class="sxs-lookup"><span data-stu-id="c2547-124">Check hello **data type** each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="c2547-125">Sprawdź hello **podstawowe statystyki** dla kolumn hello w hello następujący zestaw danych</span><span class="sxs-lookup"><span data-stu-id="c2547-125">Check hello **basic stats** for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="c2547-126">Obejrzyj hello liczbę wpisów dla każdej wartości w kolumnie w następujący sposób</span><span class="sxs-lookup"><span data-stu-id="c2547-126">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="c2547-127">**Liczba brakujących wartości** i hello rzeczywista liczba wpisów w każdej kolumnie, za pomocą następującego przykładowego kodu hello</span><span class="sxs-lookup"><span data-stu-id="c2547-127">**Count missing values** versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="c2547-128">Jeśli masz **brakujące wartości** dla określonej kolumny w danych hello, można umieszczać je w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c2547-128">If you have **missing values** for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="c2547-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="c2547-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="c2547-130">Inny sposób tooreplace brakujące wartości jest funkcją tryb hello:</span><span class="sxs-lookup"><span data-stu-id="c2547-130">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="c2547-131">dataframe_blobdata_mode = dataframe_blobdata.fillna ({< nazwa_kolumny >: .mode()[0]}) dataframe_blobdata ["< nazwa_kolumny >"]</span><span class="sxs-lookup"><span data-stu-id="c2547-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="c2547-132">Utwórz **histogram** wykreślenia przy użyciu zmiennej liczby bins tooplot hello dystrybucji zmiennej</span><span class="sxs-lookup"><span data-stu-id="c2547-132">Create a **histogram** plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="c2547-133">Przyjrzyj się **korelacji** między zmienne przy użyciu scatterplot lub hello korelacji wbudowanych funkcji</span><span class="sxs-lookup"><span data-stu-id="c2547-133">Look at **correlations** between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

