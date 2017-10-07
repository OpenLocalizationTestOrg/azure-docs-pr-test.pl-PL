---
title: "Magazyn obiektów blob aaaSample danych na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przykładowe dane w magazynie obiektów Blob Azure"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: cceadf1fb1fb4804fc5b5a3da55c82854651026e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="54fdd-103"><a name="heading"></a>Magazyn obiektów blob przykładowych danych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="54fdd-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="54fdd-104">W tym dokumencie opisano próbkowania danych przechowywanych w magazynie obiektów blob platformy Azure programowo ją pobrać, a następnie próbkowania przy użyciu procedury napisane w języku Python.</span><span class="sxs-lookup"><span data-stu-id="54fdd-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="54fdd-105">następujące Hello **menu** łączy tootopics, które opisują sposób toosample danych z różnych środowiskach magazynu.</span><span class="sxs-lookup"><span data-stu-id="54fdd-105">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="54fdd-106">**Dlaczego przykładowe dane?**</span><span class="sxs-lookup"><span data-stu-id="54fdd-106">**Why sample your data?**</span></span>
<span data-ttu-id="54fdd-107">Jeśli planujesz tooanalyze dataset hello jest duży, zazwyczaj jest to dobrze hello toodown przykładowych danych tooreduce jego rozmiar tooa mniejsze, ale reprezentatywny i łatwiejsze w zarządzaniu.</span><span class="sxs-lookup"><span data-stu-id="54fdd-107">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="54fdd-108">To ułatwia zrozumienie danych, badanie i inżynieria funkcji.</span><span class="sxs-lookup"><span data-stu-id="54fdd-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="54fdd-109">Swoją rolę w hello Cortana Analytics procesu jest szybkie tworzenie prototypów tooenable hello przetwarzania danych funkcji i modeli uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="54fdd-109">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="54fdd-110">To zadanie próbkowania jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="54fdd-110">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="54fdd-111">Pobieranie i w dół przykładowe dane</span><span class="sxs-lookup"><span data-stu-id="54fdd-111">Download and down-sample data</span></span>
1. <span data-ttu-id="54fdd-112">Pobierz hello danych z magazynu obiektów blob platformy Azure przy użyciu usługi blob hello z następującego przykładowego kodu Python hello:</span><span class="sxs-lookup"><span data-stu-id="54fdd-112">Download hello data from Azure blob storage using hello blob service from hello following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="54fdd-113">Odczytywanie danych w Pandas danych ramkę z pliku hello pobrane powyżej.</span><span class="sxs-lookup"><span data-stu-id="54fdd-113">Read data into a Pandas data-frame from hello file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="54fdd-114">Dół sample hello danych przy użyciu hello `numpy`w `random.choice` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="54fdd-114">Down-sample hello data using hello `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="54fdd-115">Teraz możesz pracować z hello powyżej ramki danych próbki 1 procent hello dalszych badań i generowanie funkcji.</span><span class="sxs-lookup"><span data-stu-id="54fdd-115">Now you can work with hello above data frame with hello 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="54fdd-116"><a name="heading"></a>Przekazywanie danych i przeczytaj go do usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="54fdd-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="54fdd-117">Można użyć hello następujące przykładowe dane hello toodown przykładowy kod i używać go bezpośrednio w usłudze Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="54fdd-117">You can use hello following sample code toodown-sample hello data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="54fdd-118">Zapis pliku lokalnego tooa hello danych ramki</span><span class="sxs-lookup"><span data-stu-id="54fdd-118">Write hello data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="54fdd-119">Przekaż tooan pliku lokalnego hello Azure blob przy użyciu następującego przykładowego kodu hello:</span><span class="sxs-lookup"><span data-stu-id="54fdd-119">Upload hello local file tooan Azure blob using hello following sample code:</span></span>
   
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
            print ("Something went wrong with uploading toohello blob:"+ BLOBNAME)

3. <span data-ttu-id="54fdd-120">Odczytywanie danych hello z hello obiektów blob platformy Azure przy użyciu usługi Azure Machine Learning [i zaimportuj dane](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) pokazane na poniższym obrazie hello:</span><span class="sxs-lookup"><span data-stu-id="54fdd-120">Read hello data from hello Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in hello image below:</span></span>

![Czytnik obiektów blob](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

