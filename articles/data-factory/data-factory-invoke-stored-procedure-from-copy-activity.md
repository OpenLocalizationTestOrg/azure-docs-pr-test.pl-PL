---
title: "aaaInvoke przechowywane procedury z działania kopiowania fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aktywność kopiowania tooinvoke procedurę przechowywaną w bazie danych SQL Azure lub programu SQL Server z fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="9449a-103">Wywołanie procedury składowanej z działania kopiowania w fabryce danych Azure</span><span class="sxs-lookup"><span data-stu-id="9449a-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="9449a-104">Podczas kopiowania danych do [programu SQL Server](data-factory-sqlserver-connector.md) lub [bazy danych SQL Azure](data-factory-azure-sql-connector.md), można skonfigurować hello **SqlSink** w tooinvoke działania kopiowania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="9449a-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure.</span></span> <span data-ttu-id="9449a-105">Możesz toouse hello przechowywane procedury tooperform dowolnego dodatkowego przetwarzania (Scalanie kolumn wyszukiwania wartości i wstawia go do wielu tabel, itp.) jest wymagana przed wstawieniem danych w tabeli docelowej toohello.</span><span class="sxs-lookup"><span data-stu-id="9449a-105">You may want toouse hello stored procedure tooperform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in toohello destination table.</span></span> <span data-ttu-id="9449a-106">Ta funkcja korzysta z [zwracającej tabelę parametrów](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="9449a-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="9449a-107">następujące przykładowe Hello pokazuje, jak tooinvoke procedury składowanej w programie SQL Server bazy danych z potoku fabryki danych (działanie kopiowania):</span><span class="sxs-lookup"><span data-stu-id="9449a-107">hello following sample shows how tooinvoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="9449a-108">Wyjściowy zestaw danych JSON</span><span class="sxs-lookup"><span data-stu-id="9449a-108">Output dataset JSON</span></span>
<span data-ttu-id="9449a-109">W zestawie danych wyjściowych hello JSON, ustaw hello **typu** do: **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="9449a-109">In hello output dataset JSON, set hello **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="9449a-110">Ustaw zbyt**AzureSqlTable** toouse z bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="9449a-110">Set it too**AzureSqlTable** toouse with an Azure SQL database.</span></span> <span data-ttu-id="9449a-111">Witaj wartość **tableName** właściwości musi odpowiadać nazwie hello pierwszy parametr hello przechowywane procedury.</span><span class="sxs-lookup"><span data-stu-id="9449a-111">hello value for **tableName** property must match hello name of first parameter of hello stored procedure.</span></span>  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="9449a-112">Sekcja SqlSink w przypadku działania kopiowania JSON</span><span class="sxs-lookup"><span data-stu-id="9449a-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="9449a-113">Zdefiniuj hello **SqlSink** sekcji w przypadku działania kopiowania hello JSON w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="9449a-113">Define hello **SqlSink** section in hello copy activity JSON as follows.</span></span> <span data-ttu-id="9449a-114">tooinvoke procedury składowanej podczas wstawiania danych do hello odbioru/docelowej bazy danych, określ wartości dla obu **SqlWriterStoredProcedureName** i **SqlWriterTableType** właściwości.</span><span class="sxs-lookup"><span data-stu-id="9449a-114">tooinvoke a stored procedure while inserting data into hello sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="9449a-115">Aby uzyskać opis tych właściwości, zobacz [SqlSink części artykułu łącznika programu SQL Server hello](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="9449a-115">For descriptions of these properties, see [SqlSink section in hello SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a><span data-ttu-id="9449a-116">Definicja procedury składowanej</span><span class="sxs-lookup"><span data-stu-id="9449a-116">Stored procedure definition</span></span> 
<span data-ttu-id="9449a-117">W bazie danych, należy zdefiniować hello przechowywane procedury hello sama nazwa jak **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="9449a-117">In your database, define hello stored procedure with hello same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="9449a-118">Witaj przechowywane procedury obsługi danych wejściowych z magazynu danych źródła hello i wstawia dane do tabeli hello docelowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9449a-118">hello stored procedure handles input data from hello source data store, and inserts data into a table in hello destination database.</span></span> <span data-ttu-id="9449a-119">Nazwa Hello hello pierwszy parametr procedury składowanej musi odpowiadać tableName hello zdefiniowany w zestawie danych hello JSON (Marketing).</span><span class="sxs-lookup"><span data-stu-id="9449a-119">hello name of hello first parameter of stored procedure must match hello tableName defined in hello dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="9449a-120">Definicja typu tabeli</span><span class="sxs-lookup"><span data-stu-id="9449a-120">Table type definition</span></span>
<span data-ttu-id="9449a-121">W bazie danych, określ typ tabeli hello z hello sama nazwa jak **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="9449a-121">In your database, define hello table type with hello same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="9449a-122">Schemat Hello hello typu tabeli muszą być zgodne hello schemat zestawu danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="9449a-122">hello schema of hello table type must match hello schema of hello input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="9449a-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9449a-123">Next steps</span></span>
<span data-ttu-id="9449a-124">Przejrzyj następujące artykuły łącznika, które dla ukończyć przykłady JSON hello:</span><span class="sxs-lookup"><span data-stu-id="9449a-124">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="9449a-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9449a-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="9449a-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9449a-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
