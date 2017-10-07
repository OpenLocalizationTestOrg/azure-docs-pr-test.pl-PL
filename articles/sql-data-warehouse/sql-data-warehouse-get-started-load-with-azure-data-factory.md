---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "aaaLoad dane z fabryką danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooload dane z fabryką danych Azure"
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a>Ładowanie danych przy użyciu usługi Azure Data Factory
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)  
> 
> 

W tym samouczku przedstawiono sposób toocreate potok w fabryce danych Azure toomove danych z tooAzure obiektu Blob magazynu Azure SQL Data Warehouse. Następujące kroki hello umożliwi:

* Konfigurowanie przykładowych danych w rozszerzeniu Azure Storage Blob.
* Łączenie zasobów tooAzure fabryki danych.
* Utwórz dane toomove potoku tooSQL magazynu obiektów blob magazynu danych.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>Przed rozpoczęciem
toofamiliarize sobie z fabryką danych Azure, zobacz [tooAzure wprowadzenie fabryki danych][Introduction tooAzure Data Factory].

### <a name="create-or-identify-resources"></a>Tworzenie lub identyfikowanie zasobów
Przed rozpoczęciem tego samouczka potrzebne hello toohave następujące zasoby:

* **Obiekt Blob magazynu Azure**: w tym samouczku korzysta z obiektu Blob magazynu Azure jako źródła danych hello hello potoku fabryki danych Azure, a zatem potrzebny będzie toohave jeden dostępny toostore hello przykładowych danych. Jeśli nie masz już, Dowiedz się, jak za[Utwórz konto magazynu][Create a storage account].
* **Usługa SQL Data Warehouse**: ten samouczek przenosi dane hello z obiektu Blob magazynu Azure zbyt SQL Data Warehouse i dlatego należy toohave magazyn danych online, który jest ładowany z hello przykładowe dane AdventureWorksDW. Jeśli nie masz już magazyn danych, Dowiedz się, jak za[je udostępnić][Create a SQL Data Warehouse]. Jeśli masz magazyn danych, ale bez hello przykładowych danych, możesz [ręcznie załadować][Load sample data into SQL Data Warehouse].
* **Fabryka danych Azure**: fabryki danych Azure kończy hello rzeczywiste obciążenie i dlatego należy toohave jeden służy potoku przepływu danych hello toobuild. Dowiedz się, jeśli nie masz już, jak toocreate co w kroku 1 z [Rozpoczynanie pracy z fabryką danych Azure (Edytor fabryki danych)][Get started with Azure Data Factory (Data Factory Editor)].
* **Narzędzie AZCopy**: należy AZCopy toocopy hello przykładowych danych z lokalnego klienta tooyour obiektu Blob magazynu Azure. Aby uzyskać instrukcje instalacji, zobacz hello [dokumentację programu AZCopy][AZCopy documentation].

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a>Krok 1: Kopiowanie przykładowych danych tooAzure obiektu Blob magazynu
Gdy wszystkie elementy hello są gotowe, jest gotowy toocopy przykładowych danych tooyour obiektu Blob magazynu Azure.

1. [Pobierz przykładowe dane][Download sample data]. Te dane dodaje innego trzech lat od danych sprzedaży tooyour przykładowe dane AdventureWorksDW.
2. Użyj tego narzędzia AZCopy polecenia toocopy hello trzech lat tooyour danych obiektu Blob magazynu Azure.
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a>Krok 2: Łączenie zasobów tooAzure fabryki danych
Teraz, dane hello znajdują się w miejscu, możemy utworzyć hello fabryki danych Azure potoku toomove hello danych z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse.

tooget uruchomiony, otwórz hello [portalu Azure] [ Azure portal] i wybierz fabrykę danych z menu po lewej stronie powitania.

### <a name="step-21-create-linked-service"></a>Krok 2.1: tworzenie usługi połączonej
Połącz z kontem magazynu platformy Azure i fabryki danych tooyour SQL Data Warehouse.  

1. Najpierw Rozpocznij proces rejestracji hello, klikając sekcję "Połączone usługi" hello fabrykę danych, a następnie kliknij przycisk "Nowy magazyn danych". Wybierz magazyn azure w obszarze, wybierz magazyn Azure jako typ tooregister nazwę, a następnie wprowadź nazwę konta i klucz konta.
2. tooregister SQL Data Warehouse przejdź do sekcji "Utwórz i wdróż" toohello, wybierz pozycję "Nowy magazyn danych", a następnie "Azure SQL Data Warehouse". Skopiuj dane i wklej w tym szablonie, a następnie uzupełnij go swoimi danymi.
   
    ```JSON
    {
        "name": "<Linked Service Name>",
        "properties": {
            "description": "",
            "type": "AzureSqlDW",
            "typeProperties": {
                 "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
             }
        }
    }
    ```

### <a name="step-22-define-hello-dataset"></a>Krok 2.2: Definiowanie hello zestawu danych
Po utworzenia hello połączone usługi, mamy zestawów danych hello toodefine.  W tym miejscu oznacza to, definiowania struktury hello hello danych, które są przenoszone z magazynu danych tooyour magazynu.  Więcej informacji na temat tworzenia

1. Uruchom ten proces, przechodząc toohello sekcji "Utwórz i wdróż" w fabryce danych.
2. Kliknij nowy zestaw danych, a następnie "Azure Blob storage" toolink fabrykę danych tooyour magazynu.  Program hello poniżej toodefine skryptu danych w magazynie obiektów Blob platformy Azure:
   
    ```JSON
    {
        "name": "<Dataset Name>",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "<linked storage name>",
            "typeProperties": {
                "folderPath": "<containter name>",
                "fileName": "FactInternetSales.csv",
                "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }
    ```
3. Teraz zdefiniujemy także zestaw danych dla usługi SQL Data Warehouse. Rozpoczynamy w hello tak samo, klikając nowy zestaw danych, a następnie "Azure SQL Data Warehouse".
   
    ```JSON
    {
        "name": "DWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": "AzureSqlDWLinkedService",
            "typeProperties": {
                "tableName": "FactInternetSales"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

## <a name="step-3-create-and-run-your-pipeline"></a>Krok 3: tworzenie i uruchamianie potoku
Na koniec mamy ustawiania i uruchom hello potok w fabryce danych Azure.  Jest to operacja hello, która kończy hello rzeczywiste przeniesienie danych.  Pełny wgląd hello operacje, które można wykonać przy użyciu usługi SQL Data Warehouse i fabryki danych Azure można znaleźć [tutaj][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].

W sekcji "Utwórz i wdróż" hello kliknij przycisk "Więcej poleceń", a następnie klikając przycisk "Nowy potok".  Po utworzeniu potoku hello program hello poniżej kod tootransfer hello danych tooyour danych magazynu:

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
              }
            ],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a>Następne kroki
toolearn, Rozpocznij od wyświetlenia:

* [Ścieżka szkoleniowa usługi Azure Data Factory][Azure Data Factory learning path].
* [Łącznik usługi Azure SQL Data Warehouse][Azure SQL Data Warehouse Connector]. Jest to podstawy temat referencyjny hello korzystania z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure.

Te tematy zawierają szczegółowe informacje na temat usługi Azure Data Factory. Omówiono w nich usługi Azure SQL Database lub HDInsight, ale informacje hello mają zastosowanie również tooAzure SQL Data Warehouse.

* [Samouczek: Rozpoczynanie pracy z fabryką danych Azure] [ Tutorial: Get started with Azure Data Factory] to hello podstawowy samouczek dotyczący przetwarzania danych przy użyciu fabryki danych Azure. W tym samouczku możesz utworzyć swój pierwszy potok, który używa HDInsight tootransform i analizy dzienników sieci web co miesiąc. Zauważ, że w tym samouczku nie ma czynności kopiowania.
* [Samouczek: Kopiowanie danych z obiektu Blob magazynu Azure tooAzure bazy danych SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]. W tym samouczku utworzysz potok w fabryce danych Azure toocopy danych z obiektu Blob magazynu Azure tooAzure bazy danych SQL.

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
