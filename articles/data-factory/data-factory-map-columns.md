---
title: kolumny zestawu danych aaaMapping w fabryce danych Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toomap źródła kolumny toodestination kolumny."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8f78d4af675bec0a70e5f6e83ec1ffb511408b5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a>Mapowanie kolumn toodestination kolumn źródło zestawu danych w zestawie danych
Mapowanie kolumny może być używane toospecify jak kolumn określonych w hello toocolumns mapy tabeli źródłowej "strukturę" określony w hello "structure" tabeli ujścia. Witaj **columnMapping** właściwość jest dostępna w hello **typeProperties** sekcji hello działanie kopiowania.

Mapowanie kolumny obsługuje hello następujące scenariusze:

* Wszystkie kolumny w strukturze zestawu danych źródła hello są mapowane tooall kolumn w strukturze zestawu danych obiektu sink hello.
* Podzbiór hello kolumn w strukturze zestawu danych źródła hello jest mapowanych tooall kolumn w strukturze zestawu danych obiektu sink hello.

Oto Hello warunki błędów, które powodują powstanie wyjątku:

* Mniejszą liczbę kolumn lub większą liczbę kolumn w hello "structure" tabeli ujścia niż określona w mapowaniu hello.
* Zduplikowane mapowania.
* Wynik kwerendy SQL nie ma nazwę kolumny, która jest określona w mapowaniu hello.

> [!NOTE]
> Witaj następujące przykłady są Azure SQL i obiektów Blob platformy Azure, ale są odpowiednie tooany magazynem danych, który obsługuje prostokątne zestawów danych. Dostosuj zestawu danych i definicje połączonej usługi w toodata toopoint przykłady hello źródła danych.

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a>Przykład 1 — z obiektu blob tooAzure Azure SQL w mapowaniu kolumn
W tym przykładzie Tabela wejściowa hello ma strukturę i wskazuje tooa tabeli SQL w bazie danych Azure SQL.

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

W tym przykładzie tabela wyjściowa hello ma strukturę i wskazuje tooa obiektów blob w magazynie obiektów blob platformy Azure.

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

powitania po JSON definiuje działanie kopiowania w potoku. toocolumns w ujściu zamapować kolumn Hello ze źródła (**columnMappings**) przy użyciu hello **Translator** właściwości.

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
**Przepływ mapowanie kolumn:**

![Przepływ mapowania kolumn](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a>Przykład 2 — z zapytania SQL z obiektu blob tooAzure Azure SQL w mapowaniu kolumn
W tym przykładzie zapytanie SQL jest używane tooextract danych z bazy danych SQL Azure zamiast określania po prostu hello nazwę tabeli i hello nazwy kolumn w sekcji "structure". 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
W takim przypadku hello wyniki zapytania są pierwszy toocolumns zamapowanych określony w "structure" źródła. Następnie kolumny hello ze źródła "structure" są mapowane toocolumns w sink "structure" z regułami określonymi w columnMappings.  Załóżmy, że hello zapytanie zwraca 5 kolumn, dwóch kolumn niż określone w hello "structure" źródła.

**Przepływ mapowania kolumn**

![Mapowanie kolumny przepływu-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a>Następne kroki
Zobacz artykuł hello samouczek dotyczący używania działania kopiowania: 

- [Kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
