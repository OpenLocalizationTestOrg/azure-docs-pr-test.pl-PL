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
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a>Eksplorowanie danych usługi Azure Blob Storage za pomocą usług Panda
W tym dokumencie opisano, jak tooexplore dane przechowywane na platformie Azure blob przy użyciu kontenera [Pandas](http://pandas.pydata.org/) pakiet języka Python.

następujące Hello **menu** łączy tootopics opisujące, jak toouse narzędzia tooexplore danych z różnych środowiskach magazynu. To zadanie jest etapem hello [proces nauki danych]().

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że masz:

* Utworzone konto magazynu platformy Azure. Aby uzyskać instrukcje, zobacz [Tworzenie konta usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Przechowywane dane na koncie magazynu obiektów blob platformy Azure. Aby uzyskać instrukcje, zobacz [przenoszenie tooand danych z magazynu Azure](../storage/common/storage-moving-data.md)

## <a name="load-hello-data-into-a-pandas-dataframe"></a>Ładowanie danych hello do Pandas DataFrame
tooexplore i manipulowania zestawu danych, najpierw musi zostać pobrana z hello obiektów blob tooa lokalny plik źródłowy, który następnie będzie można załadować Pandas DataFrame. Poniżej przedstawiono hello toofollow kroki do wykonania tej procedury:

1. Pobierz dane hello z platformy Azure blob z powitania po przykładowy kod języka Python za pomocą usługi blob. Zastąp zmienną hello w hello następującego kodu przy użyciu określonych wartości: 
   
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

## <a name="blob-dataexploration"></a>Przykłady Eksploracja danych przy użyciu Pandas
Oto kilka przykładów tooexplore danych przy użyciu Pandas:

1. Sprawdź hello **liczba wierszy i kolumn** 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. **Sprawdź** hello kilka pierwszego lub ostatniego **wierszy** w hello następującego zestawu danych:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Sprawdź hello **— typ danych** każda kolumna została zaimportowana jako przy użyciu hello następującego przykładowego kodu
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Sprawdź hello **podstawowe statystyki** dla kolumn hello w hello następujący zestaw danych
   
        dataframe_blobdata.describe()
5. Obejrzyj hello liczbę wpisów dla każdej wartości w kolumnie w następujący sposób
   
        dataframe_blobdata['<column_name>'].value_counts()
6. **Liczba brakujących wartości** i hello rzeczywista liczba wpisów w każdej kolumnie, za pomocą następującego przykładowego kodu hello
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Jeśli masz **brakujące wartości** dla określonej kolumny w danych hello, można umieszczać je w następujący sposób:
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape
   
   Inny sposób tooreplace brakujące wartości jest funkcją tryb hello:
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna ({< nazwa_kolumny >: .mode()[0]}) dataframe_blobdata ["< nazwa_kolumny >"]        
8. Utwórz **histogram** wykreślenia przy użyciu zmiennej liczby bins tooplot hello dystrybucji zmiennej    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Przyjrzyj się **korelacji** między zmienne przy użyciu scatterplot lub hello korelacji wbudowanych funkcji
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

