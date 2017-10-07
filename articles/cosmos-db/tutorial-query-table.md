---
title: "dane tabeli tooquery aaaHow w usłudze Azure DB rozwiązania Cosmos? | Microsoft Docs"
description: "Dowiedz się tooquery tabeli danych w usłudze Azure DB rozwiązania Cosmos"
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a>Azure DB rozwiązania Cosmos: Jak tooquery tabeli danych przy użyciu hello tabeli interfejsu API (wersja zapoznawcza)?

Hello Azure DB rozwiązania Cosmos [API tabeli](table-introduction.md) (wersja zapoznawcza) obsługuje OData i [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) zapytań dotyczących danych klucz wartość (tabeli).  

W tym artykule omówiono hello następujące zadania: 

> [!div class="checklist"]
> * Wykonywanie zapytania na danych z hello tabeli interfejsu API

Witaj zapytania w tym artykule Użyj hello następujące przykładowe `People` tabeli:

| PartitionKey | RowKey | Adres e-mail | Numer telefonu |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jan | Jeff@contoso.com| 425-555-0104 | 

Ponieważ bazy danych Azure rozwiązania Cosmos jest zgodny z hello interfejsów API magazynu tabel Azure, zobacz [badania tabel i jednostek] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) szczegółowe informacje na temat sposobu hello tooquery przy użyciu Tabela interfejsu API. 

Aby uzyskać więcej informacji na powitania premium możliwości, które oferuje bazy danych rozwiązania Cosmos Azure, zobacz [bazy danych Azure rozwiązania Cosmos: Tabela interfejsu API](table-introduction.md) i [opracowanie z hello tabeli interfejs API .NET](tutorial-develop-table-dotnet.md). 

## <a name="prerequisites"></a>Wymagania wstępne

Dla tych toowork zapytania musi mieć konto bazy danych Azure rozwiązania Cosmos i danych jednostki w kontenerze hello. Nie masz żadnego z tych? Zakończenie hello [szybkiego startu 5 minutową](https://aka.ms/acdbtnetqs) lub hello [samouczek developer](https://aka.ms/acdbtabletut) toocreate konta i wypełnić bazę danych.

## <a name="query-on-partitionkey-and-rowkey"></a>Zapytanie dotyczące PartitionKey i RowKey
Ponieważ właściwości PartitionKey i RowKey hello tworzą klucza podstawowego jednostki, można użyć powitania po jednostki hello tooidentify specjalnej składni: 

**Zapytanie**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**Wyniki**

| PartitionKey | RowKey | Adres e-mail | Numer telefonu |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

Alternatywnie można określić właściwości jako część hello `$filter` opcji, jak pokazano w hello następujących sekcji. Należy pamiętać, że hello nazw właściwości kluczy i wartości stałe jest rozróżniana wielkość liter. Zarówno hello PartitionKey i właściwości RowKey są typu ciąg. 

## <a name="query-by-using-an-odata-filter"></a>Zapytanie za pomocą filtru OData
Gdy w przypadku tworzenia ciąg filtru, pamiętać o tych reguł: 

* Operatory logiczne hello Użyj zdefiniowany przez toocompare Specyfikacja protokołu OData hello tooa wartości właściwości. Należy pamiętać, że nie można porównać wartości właściwości dynamicznych tooa. Po jednej stronie powitania wyrażenie musi być stałą. 
* Hello nazwę właściwości, operator i wartość stała muszą być oddzielone spacjami zakodowane w adresie URL. Odstęp jest zakodowane w adresie URL jako `%20`. 
* Wszystkie części hello ciąg filtru jest rozróżniana wielkość liter. 
* musi być wartością stałą Hello hello tych samych danych typu jako właściwość hello aby hello filtru tooreturn prawidłowe wyniki. Aby uzyskać więcej informacji na temat typów obsługiwanych właściwości zobacz [hello opis modelu danych usługi tabel](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model). 

Poniżej przedstawiono przykładowe zapytanie, które pokazuje, jak toofilter przez hello PartitionKey i E-mail właściwości przy użyciu OData `$filter`.

**Zapytanie**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

Aby uzyskać więcej informacji dotyczących sposobu tooconstruct filtru wyrażeń dla różnych typów danych, zobacz [badania tabel i jednostek](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).

**Wyniki**

| PartitionKey | RowKey | Adres e-mail | Numer telefonu |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>Zapytanie za pomocą LINQ 
Możesz także zbadać za pomocą LINQ, który tłumaczy toohello odpowiedniego wyrażenia zapytania OData. Poniżej przedstawiono przykład sposobu toobuild zapytania przy użyciu hello zestawu .NET SDK:

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności:

> [!div class="checklist"]
> * Przedstawiono sposób tooquery przy użyciu hello tabeli interfejsu API (wersja zapoznawcza) 

Można teraz kontynuować toohello następny samouczek toolearn jak toodistribute danych globalnie.

> [!div class="nextstepaction"]
> [Globalny dystrybucji danych](tutorial-global-distribution-documentdb.md)
