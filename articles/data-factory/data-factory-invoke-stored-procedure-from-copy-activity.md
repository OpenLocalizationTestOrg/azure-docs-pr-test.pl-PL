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
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a>Wywołanie procedury składowanej z działania kopiowania w fabryce danych Azure
Podczas kopiowania danych do [programu SQL Server](data-factory-sqlserver-connector.md) lub [bazy danych SQL Azure](data-factory-azure-sql-connector.md), można skonfigurować hello **SqlSink** w tooinvoke działania kopiowania procedury składowanej. Możesz toouse hello przechowywane procedury tooperform dowolnego dodatkowego przetwarzania (Scalanie kolumn wyszukiwania wartości i wstawia go do wielu tabel, itp.) jest wymagana przed wstawieniem danych w tabeli docelowej toohello. Ta funkcja korzysta z [zwracającej tabelę parametrów](https://msdn.microsoft.com/library/bb675163.aspx). 

następujące przykładowe Hello pokazuje, jak tooinvoke procedury składowanej w programie SQL Server bazy danych z potoku fabryki danych (działanie kopiowania):  

## <a name="output-dataset-json"></a>Wyjściowy zestaw danych JSON
W zestawie danych wyjściowych hello JSON, ustaw hello **typu** do: **SqlServerTable**. Ustaw zbyt**AzureSqlTable** toouse z bazy danych Azure SQL. Witaj wartość **tableName** właściwości musi odpowiadać nazwie hello pierwszy parametr hello przechowywane procedury.  

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

## <a name="sqlsink-section-in-copy-activity-json"></a>Sekcja SqlSink w przypadku działania kopiowania JSON
Zdefiniuj hello **SqlSink** sekcji w przypadku działania kopiowania hello JSON w następujący sposób. tooinvoke procedury składowanej podczas wstawiania danych do hello odbioru/docelowej bazy danych, określ wartości dla obu **SqlWriterStoredProcedureName** i **SqlWriterTableType** właściwości. Aby uzyskać opis tych właściwości, zobacz [SqlSink części artykułu łącznika programu SQL Server hello](data-factory-sqlserver-connector.md#sqlsink).

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

## <a name="stored-procedure-definition"></a>Definicja procedury składowanej 
W bazie danych, należy zdefiniować hello przechowywane procedury hello sama nazwa jak **SqlWriterStoredProcedureName**. Witaj przechowywane procedury obsługi danych wejściowych z magazynu danych źródła hello i wstawia dane do tabeli hello docelowej bazy danych. Nazwa Hello hello pierwszy parametr procedury składowanej musi odpowiadać tableName hello zdefiniowany w zestawie danych hello JSON (Marketing).

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a>Definicja typu tabeli
W bazie danych, określ typ tabeli hello z hello sama nazwa jak **SqlWriterTableType**. Schemat Hello hello typu tabeli muszą być zgodne hello schemat zestawu danych wejściowych hello.

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a>Następne kroki
Przejrzyj następujące artykuły łącznika, które dla ukończyć przykłady JSON hello: 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)
