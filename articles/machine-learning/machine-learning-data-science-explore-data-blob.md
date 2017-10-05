---
title: "Eksploruj dane w magazynie obiektów blob platformy Azure z Pandas | Dokumentacja firmy Microsoft"
description: "Jak Eksplorowanie danych przechowywanych w kontenerze obiektów blob platformy Azure przy użyciu Pandas."
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
ms.openlocfilehash: e1b33b17270122a38228484a56c8324c5b4505a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="e898f-103">Eksplorowanie danych usługi Azure Blob Storage za pomocą usług Panda</span><span class="sxs-lookup"><span data-stu-id="e898f-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="e898f-104">W tym dokumencie opisano sposób eksplorować dane przechowywane w użyciu kontenera obiektów blob platformy Azure [Pandas](http://pandas.pydata.org/) pakiet języka Python.</span><span class="sxs-lookup"><span data-stu-id="e898f-104">This document covers how to explore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="e898f-105">Następujące **menu** linki do tematów opisujących sposób użycia narzędzia, aby eksplorować dane w różnych środowiskach magazynu.</span><span class="sxs-lookup"><span data-stu-id="e898f-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="e898f-106">To zadanie jest krokiem w [proces nauki danych]().</span><span class="sxs-lookup"><span data-stu-id="e898f-106">This task is a step in the [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="e898f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e898f-107">Prerequisites</span></span>
<span data-ttu-id="e898f-108">W tym artykule przyjęto założenie, że masz:</span><span class="sxs-lookup"><span data-stu-id="e898f-108">This article assumes that you have:</span></span>

* <span data-ttu-id="e898f-109">Utworzone konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e898f-109">Created an Azure storage account.</span></span> <span data-ttu-id="e898f-110">Aby uzyskać instrukcje, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="e898f-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="e898f-111">Przechowywane dane na koncie magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e898f-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="e898f-112">Aby uzyskać instrukcje, zobacz [przenoszenie danych do i z usługi Azure Storage](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="e898f-112">If you need instructions, see [Moving data to and from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-the-data-into-a-pandas-dataframe"></a><span data-ttu-id="e898f-113">Ładowanie danych do Pandas DataFrame</span><span class="sxs-lookup"><span data-stu-id="e898f-113">Load the data into a Pandas DataFrame</span></span>
<span data-ttu-id="e898f-114">Aby eksplorować i manipulowania zestawu danych, musi najpierw zostać pobrana od źródła obiektu blob do pliku lokalnego, który następnie będzie można załadować Pandas DataFrame.</span><span class="sxs-lookup"><span data-stu-id="e898f-114">To explore and manipulate a dataset, it must first be downloaded from the blob source to a local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="e898f-115">Poniżej przedstawiono kroki do wykonania w przypadku tej procedury:</span><span class="sxs-lookup"><span data-stu-id="e898f-115">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="e898f-116">Pobieranie danych z usługi Azure blob z Poniższy przykładowy kod języka Python za pomocą usługi blob.</span><span class="sxs-lookup"><span data-stu-id="e898f-116">Download the data from Azure blob with the following Python code sample using blob service.</span></span> <span data-ttu-id="e898f-117">Zastąp zmienną w poniższym kodzie z określonymi wartościami:</span><span class="sxs-lookup"><span data-stu-id="e898f-117">Replace the variable in the following code with your specific values:</span></span> 
   
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
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))
2. <span data-ttu-id="e898f-118">Dane do odczytu do Pandas danych ramki z pobranego pliku.</span><span class="sxs-lookup"><span data-stu-id="e898f-118">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="e898f-119">Teraz można przystąpić do eksplorowania danych oraz do generowania funkcji dla tego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="e898f-119">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="e898f-120"><a name="blob-dataexploration"></a>Przykłady Eksploracja danych przy użyciu Pandas</span><span class="sxs-lookup"><span data-stu-id="e898f-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="e898f-121">Oto kilka przykładów sposobów, aby eksplorować dane przy użyciu Pandas:</span><span class="sxs-lookup"><span data-stu-id="e898f-121">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="e898f-122">Sprawdź **liczba wierszy i kolumn**</span><span class="sxs-lookup"><span data-stu-id="e898f-122">Inspect the **number of rows and columns**</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="e898f-123">**Sprawdź** kilka pierwszego lub ostatniego **wierszy** następujących danych:</span><span class="sxs-lookup"><span data-stu-id="e898f-123">**Inspect** the first or last few **rows** in the following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="e898f-124">Sprawdź **— typ danych** każda kolumna została zaimportowana jako przy użyciu następujący przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="e898f-124">Check the **data type** each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="e898f-125">Sprawdź **podstawowe statystyki** kolumn danych, ustaw następujący</span><span class="sxs-lookup"><span data-stu-id="e898f-125">Check the **basic stats** for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="e898f-126">Przyjrzyj się liczba wpisów dla każdej wartości w kolumnie w następujący sposób</span><span class="sxs-lookup"><span data-stu-id="e898f-126">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="e898f-127">**Liczba brakujących wartości** zależności od rzeczywistej liczby wpisów w każdej kolumnie, za pomocą następujący przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="e898f-127">**Count missing values** versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="e898f-128">Jeśli masz **brakujące wartości** dla określonej kolumny danych, można umieszczać je w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e898f-128">If you have **missing values** for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="e898f-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="e898f-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="e898f-130">Zastąp brakujące wartości w inny sposób jest funkcją trybu:</span><span class="sxs-lookup"><span data-stu-id="e898f-130">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="e898f-131">dataframe_blobdata_mode = dataframe_blobdata.fillna ({< nazwa_kolumny >: .mode()[0]}) dataframe_blobdata ["< nazwa_kolumny >"]</span><span class="sxs-lookup"><span data-stu-id="e898f-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="e898f-132">Utwórz **histogram** wykreślenia przy użyciu zmiennej liczby bins do wykreślenia dystrybucji zmiennej</span><span class="sxs-lookup"><span data-stu-id="e898f-132">Create a **histogram** plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="e898f-133">Przyjrzyj się **korelacji** między zmienne przy użyciu scatterplot lub funkcja wbudowana korelacji</span><span class="sxs-lookup"><span data-stu-id="e898f-133">Look at **correlations** between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

