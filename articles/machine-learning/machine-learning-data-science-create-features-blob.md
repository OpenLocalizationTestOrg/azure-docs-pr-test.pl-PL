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
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a>Tworzenie funkcji dla danych usługi Azure Blob Storage za pomocą usługi Panda
Ten dokument przedstawia sposób toocreate funkcji dla danych przechowywanych w kontenerze obiektów blob platformy Azure przy użyciu hello [Pandas](http://pandas.pydata.org/) pakiet języka Python. Po zwijania jak tooload hello danych do ramki danych Panda, widoczny jest sposób toogenerate podzielone na kategorie funkcji za pomocą skryptów języka Python z wartościami wskaźnik i binning funkcji.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

To **menu** łączy tootopics, które opisują sposób toocreate funkcji dla danych w różnych środowiskach. To zadanie jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule założono, że utworzono konto magazynu obiektów blob platformy Azure i przechowywanych danych istnieje. Aby uzyskać instrukcje tooset konta, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Ładowanie danych hello do ramki danych Pandas
W kolejności toodo Eksploruj i manipulowania zestawu danych, musi zostać pobrana z hello blob źródła tooa pliku lokalnego, która może zostać załadowana w ramce Pandas danych. Poniżej przedstawiono hello toofollow kroki do wykonania tej procedury:

1. Pobierz dane hello z platformy Azure blob z hello następującego przykładowego kodu Python za pomocą usługi blob. Zastąp zmienną hello w kodzie hello poniżej określonej wartości:
   
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
2. Odczyt danych hello w Pandas danych ramkę z hello pobrany plik.
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

Teraz są gotowe tooexplore hello danych i generowanie funkcji dla tego zestawu danych.

## <a name="blob-featuregen"></a>Funkcja generowania
Witaj w dwóch następnych sekcjach pokazują, jak toogenerate podzielone na kategorie funkcji z wartościami wskaźnik i binning funkcji za pomocą skryptów języka Python.

### <a name="blob-countfeature"></a>Funkcja generowania na podstawie wartości wskaźnika
Podzielone na kategorie funkcji można utworzyć w następujący sposób:

1. Sprawdź dystrybucji hello hello kolumny podzielone na kategorie:
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. Generowanie wartości wskaźnika dla każdej wartości w kolumnie hello
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. Dołącz kolumny wskaźnik hello hello oryginalne dane ramki
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. Usuń samej zmiennej hello oryginalnego:
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>Funkcja generowania binning
Podczas generowania binned funkcje, możemy wykonać następujące czynności:

1. Dodaj sekwencję toobin kolumny liczbowej
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. Konwertuj binning sekwencji tooa logiczna zmiennych
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. Na koniec sprzężenia hello fikcyjny zmienne kopii toohello oryginalne dane ramki
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <a name="sql-featuregen"></a>Zapisywanie danych kopii tooAzure obiektów blob i korzystanie z usługi Azure Machine Learning
Po przedstawione hello danych i utworzyć hello funkcji niezbędnych możesz przekazać dane hello (próbkowany lub featurized) tooan Azure blob i używać go w usłudze Azure Machine Learning przy użyciu hello następujące kroki: należy pamiętać, że można tworzyć dodatkowe funkcje w hello Azure Machine Learning Studio również.

1. Zapisać hello danych ramki toolocal pliku
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Przekaż obiekt blob tooAzure danych hello w następujący sposób:
   
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
3. Teraz hello dane mogą zostać odczytane z hello obiektów blob za pomocą usługi Azure Machine Learning hello [i zaimportuj dane](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) modułu, jak pokazano na poniższym zrzucie ekranu hello:

![Czytnik obiektów blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

