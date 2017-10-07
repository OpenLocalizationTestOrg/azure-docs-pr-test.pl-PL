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
# <a name="heading"></a>Przetwarzanie danych obiektów blob platformy Azure za pomocą zaawansowana analityka
W tym dokumencie opisano masowej danych i funkcji generowania z danych przechowywanych w magazynie obiektów Blob Azure. 

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Ładowanie danych hello do ramki danych Pandas
W kolejności tooexplore i manipulowania zestawu danych, musi zostać pobrana z hello blob źródła tooa pliku lokalnego, która może zostać załadowana w ramce Pandas danych. Poniżej przedstawiono hello toofollow kroki do wykonania tej procedury:

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

## <a name="blob-dataexploration"></a>Eksploracja danych
Oto kilka przykładów tooexplore danych przy użyciu Pandas:

1. Sprawdź hello liczby wierszy i kolumn 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. Najpierw sprawdź hello lub ostatni kilka wierszy w elemencie dataset hello, jak pokazano poniżej:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Sprawdź typ danych hello każdej kolumny zostało zaimportowane jako przy użyciu hello następującego przykładowego kodu
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Sprawdź hello podstawowe statystyki hello kolumn w zestawie danych hello w następujący sposób
   
        dataframe_blobdata.describe()
5. Obejrzyj hello liczbę wpisów dla każdej wartości w kolumnie w następujący sposób
   
        dataframe_blobdata['<column_name>'].value_counts()
6. Liczba brakujących wartości w zależności od rzeczywistej liczby wpisów w każdej kolumnie, za pomocą następującego przykładowego kodu hello hello
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Jeśli brakuje wartości dla określonej kolumny w danych hello, musisz porzucić je w następujący sposób:
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape
   
   Inny sposób tooreplace brakujące wartości jest funkcją tryb hello:
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna ({< nazwa_kolumny >: .mode()[0]}) dataframe_blobdata ["< nazwa_kolumny >"]        
8. Utwórz wykres histogramu przy użyciu zmiennej liczby bins tooplot hello dystrybucji zmiennej    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Przyjrzyj się korelacji między zmienne przy użyciu scatterplot lub hello korelacji wbudowanych funkcji
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <a name="blob-featuregen"></a>Funkcja generowania
Firma Microsoft może wygenerować funkcji za pomocą języka Python w następujący sposób:

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
3. Teraz hello dane mogą zostać odczytane z hello obiektów blob za pomocą usługi Azure Machine Learning hello [i zaimportuj dane] [ import-data] modułu, jak pokazano na poniższym zrzucie ekranu hello:

![Czytnik obiektów blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

