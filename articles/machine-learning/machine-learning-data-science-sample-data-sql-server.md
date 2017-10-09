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
# <a name="heading"></a>Przykładowe dane w programie SQL Server na platformie Azure
Tym dokumencie przedstawiono sposób przechowywania danych toosample w programie SQL Server na platformie Azure przy użyciu SQL lub hello język programowania Python. Pokazuje też, jak toomove próbce danych do usługi Azure Machine Learning przez zapisanie go w pliku tooa, przekazać go tooan obiektów blob platformy Azure, a następnie odczytanie go do usługi Azure Machine Learning Studio.

próbkowanie Python Hello używa hello [pyodbc](https://code.google.com/p/pyodbc/) tooSQL tooconnect biblioteki ODBC serwera na platformie Azure i hello [Pandas](http://pandas.pydata.org/) biblioteki toodo hello próbkowania.

> [!NOTE]
> Hello przykładowy SQL kod w tym dokumencie przyjęto założenie, że hello jest danych w programie SQL Server na platformie Azure. Jeśli nie jest dostępne, można znaleźć za[przenoszenia danych tooSQL Server na platformie Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) tematu, aby uzyskać instrukcje dotyczące toomove Twojego tooSQL danych serwera na platformie Azure.
> 
> 

następujące Hello **menu** łączy tootopics, które opisują sposób toosample danych z różnych środowiskach magazynu. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Dlaczego przykładowe dane?**
Jeśli planujesz tooanalyze dataset hello jest duży, zazwyczaj jest to dobrze hello toodown przykładowych danych tooreduce jego rozmiar tooa mniejsze, ale reprezentatywny i łatwiejsze w zarządzaniu. To ułatwia zrozumienie danych, badanie i inżynieria funkcji. Swoją rolę w hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) jest szybkie tworzenie prototypów tooenable hello przetwarzania danych funkcji i modeli uczenia maszynowego.

To zadanie próbkowania jest etapem hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="SQL"></a>Przy użyciu programu SQL
W tej sekcji opisano kilka metod za pomocą tooperform SQL pobieranie próbek losowych hello danych w bazie danych hello. Wybierz metodę, w oparciu o rozmiar danych i jego dystrybucji.

Poniższe elementy dwóch Hello pokazują, jak newid toouse w tooperform programu SQL Server hello próbkowania. Hello metody zależy od sposobu losowe hello próbki toobe (pk_id w hello przykładowy kod poniżej przyjęto toobe automatycznego generowania klucza podstawowego).

1. Mniej rygorystyczne losowej próbki
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. Więcej losowej próbki 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

Tablesample może być użyta do próbkowania także przedstawiona poniżej. Może to być lepszym rozwiązaniem Jeśli rozmiar danych jest duży (przy założeniu, że nie jest skorelowany danych na różnych stronach) i toocomplete zapytania hello w odpowiednim czasie.

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> Można eksplorować i generowanie funkcji z tej próbki danych przez zapisanie go w nowej tabeli
> 
> 

### <a name="sql-aml"></a>Łączenie tooAzure uczenia maszynowego
Możesz bezpośrednio użyć hello przykładowe zapytania powyżej w hello Azure Machine Learning [i zaimportuj dane] [ import-data] modułu hello toodown przykładowe dane na powitania udać i przełączyć go do eksperymentu uczenia maszynowego Azure. Poniżej przedstawiono zrzut ekranu przy użyciu hello czytnika modułu tooread hello próbkowany danych:

![Czytnik sql][1]

## <a name="python"></a>Przy użyciu języka programowania Python hello
W tej sekcji przedstawiono przy użyciu hello [biblioteki pyodbc](https://code.google.com/p/pyodbc/) tooestablish ODBC połączyć tooa bazy danych serwera SQL w języku Python. Parametry połączenia bazy danych Hello jest następująca: (zamiast servername, dbname, nazwę użytkownika i hasło z konfiguracją):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Witaj [Pandas](http://pandas.pydata.org/) biblioteki w języku Python zawiera bogaty zestaw struktur danych i narzędzia do analizy danych do manipulowania danymi programowania Python. Poniższy kod Hello odczytuje próbkę 0,1% hello danych z tabeli w bazie danych Azure SQL w danych Pandas:

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

Teraz możesz pracować z danymi hello próbkowany hello Pandas danych ramki. 

### <a name="python-aml"></a>Łączenie tooAzure uczenia maszynowego
Można użyć następującego przykładowego kodu toosave hello danych próbkowania w dół tooa pliku hello i przekaż go tooan obiektów blob platformy Azure. Hello dane w obiekcie blob hello może być bezpośrednio odczytane do eksperymentu Azure Machine Learning przy użyciu hello [i zaimportuj dane] [ import-data] modułu. Witaj obejmuje następujące czynności: 

1. Zapis hello pandas danych ramki tooa lokalnego pliku
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Przekazywanie pliku lokalnego tooAzure blob
   
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
3. Odczytywanie danych z obiektów blob platformy Azure przy użyciu usługi Azure Machine Learning [i zaimportuj dane] [ import-data] modułu, jak pokazano poniżej Przechwyć ekranie powitania:

![Czytnik obiektów blob][2]

## <a name="hello-team-data-science-process-in-action-example"></a>Witaj proces nauki danych zespołu w przykładzie akcji
Przykład wskazówki na trasie hello proces nauki danych Team publicznego zestawu danych, przy użyciu zobacz [proces nauki danych zespołu w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
