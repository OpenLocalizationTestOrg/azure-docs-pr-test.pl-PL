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
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a><span data-ttu-id="78570-103">Mapowanie kolumn toodestination kolumn źródło zestawu danych w zestawie danych</span><span class="sxs-lookup"><span data-stu-id="78570-103">Map source dataset columns toodestination dataset columns</span></span>
<span data-ttu-id="78570-104">Mapowanie kolumny może być używane toospecify jak kolumn określonych w hello toocolumns mapy tabeli źródłowej "strukturę" określony w hello "structure" tabeli ujścia.</span><span class="sxs-lookup"><span data-stu-id="78570-104">Column mapping can be used toospecify how columns specified in hello “structure” of source table map toocolumns specified in hello “structure” of sink table.</span></span> <span data-ttu-id="78570-105">Witaj **columnMapping** właściwość jest dostępna w hello **typeProperties** sekcji hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="78570-105">hello **columnMapping** property is available in hello **typeProperties** section of hello Copy activity.</span></span>

<span data-ttu-id="78570-106">Mapowanie kolumny obsługuje hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="78570-106">Column mapping supports hello following scenarios:</span></span>

* <span data-ttu-id="78570-107">Wszystkie kolumny w strukturze zestawu danych źródła hello są mapowane tooall kolumn w strukturze zestawu danych obiektu sink hello.</span><span class="sxs-lookup"><span data-stu-id="78570-107">All columns in hello source dataset structure are mapped tooall columns in hello sink dataset structure.</span></span>
* <span data-ttu-id="78570-108">Podzbiór hello kolumn w strukturze zestawu danych źródła hello jest mapowanych tooall kolumn w strukturze zestawu danych obiektu sink hello.</span><span class="sxs-lookup"><span data-stu-id="78570-108">A subset of hello columns in hello source dataset structure is mapped tooall columns in hello sink dataset structure.</span></span>

<span data-ttu-id="78570-109">Oto Hello warunki błędów, które powodują powstanie wyjątku:</span><span class="sxs-lookup"><span data-stu-id="78570-109">hello following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="78570-110">Mniejszą liczbę kolumn lub większą liczbę kolumn w hello "structure" tabeli ujścia niż określona w mapowaniu hello.</span><span class="sxs-lookup"><span data-stu-id="78570-110">Either fewer columns or more columns in hello “structure” of sink table than specified in hello mapping.</span></span>
* <span data-ttu-id="78570-111">Zduplikowane mapowania.</span><span class="sxs-lookup"><span data-stu-id="78570-111">Duplicate mapping.</span></span>
* <span data-ttu-id="78570-112">Wynik kwerendy SQL nie ma nazwę kolumny, która jest określona w mapowaniu hello.</span><span class="sxs-lookup"><span data-stu-id="78570-112">SQL query result does not have a column name that is specified in hello mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="78570-113">Witaj następujące przykłady są Azure SQL i obiektów Blob platformy Azure, ale są odpowiednie tooany magazynem danych, który obsługuje prostokątne zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="78570-113">hello following samples are for Azure SQL and Azure Blob but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="78570-114">Dostosuj zestawu danych i definicje połączonej usługi w toodata toopoint przykłady hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="78570-114">Adjust dataset and linked service definitions in examples toopoint toodata in hello relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a><span data-ttu-id="78570-115">Przykład 1 — z obiektu blob tooAzure Azure SQL w mapowaniu kolumn</span><span class="sxs-lookup"><span data-stu-id="78570-115">Sample 1 – column mapping from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="78570-116">W tym przykładzie Tabela wejściowa hello ma strukturę i wskazuje tooa tabeli SQL w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="78570-116">In this sample, hello input table has a structure and it points tooa SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="78570-117">W tym przykładzie tabela wyjściowa hello ma strukturę i wskazuje tooa obiektów blob w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="78570-117">In this sample, hello output table has a structure and it points tooa blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="78570-118">powitania po JSON definiuje działanie kopiowania w potoku.</span><span class="sxs-lookup"><span data-stu-id="78570-118">hello following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="78570-119">toocolumns w ujściu zamapować kolumn Hello ze źródła (**columnMappings**) przy użyciu hello **Translator** właściwości.</span><span class="sxs-lookup"><span data-stu-id="78570-119">hello columns from source mapped toocolumns in sink (**columnMappings**) by using hello **Translator** property.</span></span>

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
<span data-ttu-id="78570-120">**Przepływ mapowanie kolumn:**</span><span class="sxs-lookup"><span data-stu-id="78570-120">**Column mapping flow:**</span></span>

![Przepływ mapowania kolumn](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a><span data-ttu-id="78570-122">Przykład 2 — z zapytania SQL z obiektu blob tooAzure Azure SQL w mapowaniu kolumn</span><span class="sxs-lookup"><span data-stu-id="78570-122">Sample 2 – column mapping with SQL query from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="78570-123">W tym przykładzie zapytanie SQL jest używane tooextract danych z bazy danych SQL Azure zamiast określania po prostu hello nazwę tabeli i hello nazwy kolumn w sekcji "structure".</span><span class="sxs-lookup"><span data-stu-id="78570-123">In this sample, a SQL query is used tooextract data from Azure SQL instead of simply specifying hello table name and hello column names in “structure” section.</span></span> 

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
<span data-ttu-id="78570-124">W takim przypadku hello wyniki zapytania są pierwszy toocolumns zamapowanych określony w "structure" źródła.</span><span class="sxs-lookup"><span data-stu-id="78570-124">In this case, hello query results are first mapped toocolumns specified in “structure” of source.</span></span> <span data-ttu-id="78570-125">Następnie kolumny hello ze źródła "structure" są mapowane toocolumns w sink "structure" z regułami określonymi w columnMappings.</span><span class="sxs-lookup"><span data-stu-id="78570-125">Next, hello columns from source “structure” are mapped toocolumns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="78570-126">Załóżmy, że hello zapytanie zwraca 5 kolumn, dwóch kolumn niż określone w hello "structure" źródła.</span><span class="sxs-lookup"><span data-stu-id="78570-126">Suppose hello query returns 5 columns, two more columns than those specified in hello “structure” of source.</span></span>

<span data-ttu-id="78570-127">**Przepływ mapowania kolumn**</span><span class="sxs-lookup"><span data-stu-id="78570-127">**Column mapping flow**</span></span>

![Mapowanie kolumny przepływu-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="78570-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="78570-129">Next steps</span></span>
<span data-ttu-id="78570-130">Zobacz artykuł hello samouczek dotyczący używania działania kopiowania:</span><span class="sxs-lookup"><span data-stu-id="78570-130">See hello article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="78570-131">Kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych</span><span class="sxs-lookup"><span data-stu-id="78570-131">Copy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
