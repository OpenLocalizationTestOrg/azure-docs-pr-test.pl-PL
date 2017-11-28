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
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a><span data-ttu-id="b3a2a-104">Azure DB rozwiązania Cosmos: Jak tooquery tabeli danych przy użyciu hello tabeli interfejsu API (wersja zapoznawcza)?</span><span class="sxs-lookup"><span data-stu-id="b3a2a-104">Azure Cosmos DB: How tooquery table data by using hello Table API (preview)?</span></span>

<span data-ttu-id="b3a2a-105">Hello Azure DB rozwiązania Cosmos [API tabeli](table-introduction.md) (wersja zapoznawcza) obsługuje OData i [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) zapytań dotyczących danych klucz wartość (tabeli).</span><span class="sxs-lookup"><span data-stu-id="b3a2a-105">hello Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="b3a2a-106">W tym artykule omówiono hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="b3a2a-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="b3a2a-107">Wykonywanie zapytania na danych z hello tabeli interfejsu API</span><span class="sxs-lookup"><span data-stu-id="b3a2a-107">Querying data with hello Table API</span></span>

<span data-ttu-id="b3a2a-108">Witaj zapytania w tym artykule Użyj hello następujące przykładowe `People` tabeli:</span><span class="sxs-lookup"><span data-stu-id="b3a2a-108">hello queries in this article use hello following sample `People` table:</span></span>

| <span data-ttu-id="b3a2a-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="b3a2a-109">PartitionKey</span></span> | <span data-ttu-id="b3a2a-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="b3a2a-110">RowKey</span></span> | <span data-ttu-id="b3a2a-111">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="b3a2a-111">Email</span></span> | <span data-ttu-id="b3a2a-112">Numer telefonu</span><span class="sxs-lookup"><span data-stu-id="b3a2a-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b3a2a-113">Harp</span><span class="sxs-lookup"><span data-stu-id="b3a2a-113">Harp</span></span> | <span data-ttu-id="b3a2a-114">Walter</span><span class="sxs-lookup"><span data-stu-id="b3a2a-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="b3a2a-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="b3a2a-115">425-555-0101</span></span> |
| <span data-ttu-id="b3a2a-116">Smith</span><span class="sxs-lookup"><span data-stu-id="b3a2a-116">Smith</span></span> | <span data-ttu-id="b3a2a-117">Ben</span><span class="sxs-lookup"><span data-stu-id="b3a2a-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="b3a2a-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="b3a2a-118">425-555-0102</span></span> |
| <span data-ttu-id="b3a2a-119">Smith</span><span class="sxs-lookup"><span data-stu-id="b3a2a-119">Smith</span></span> | <span data-ttu-id="b3a2a-120">Jan</span><span class="sxs-lookup"><span data-stu-id="b3a2a-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="b3a2a-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="b3a2a-121">425-555-0104</span></span> | 

<span data-ttu-id="b3a2a-122">Ponieważ bazy danych Azure rozwiązania Cosmos jest zgodny z hello interfejsów API magazynu tabel Azure, zobacz [badania tabel i jednostek] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) szczegółowe informacje na temat sposobu hello tooquery przy użyciu Tabela interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-122">Because Azure Cosmos DB is compatible with hello Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how tooquery by using hello Table API.</span></span> 

<span data-ttu-id="b3a2a-123">Aby uzyskać więcej informacji na powitania premium możliwości, które oferuje bazy danych rozwiązania Cosmos Azure, zobacz [bazy danych Azure rozwiązania Cosmos: Tabela interfejsu API](table-introduction.md) i [opracowanie z hello tabeli interfejs API .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b3a2a-123">For more information on hello premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with hello Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b3a2a-124">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b3a2a-124">Prerequisites</span></span>

<span data-ttu-id="b3a2a-125">Dla tych toowork zapytania musi mieć konto bazy danych Azure rozwiązania Cosmos i danych jednostki w kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-125">For these queries toowork, you must have an Azure Cosmos DB account and have entity data in hello container.</span></span> <span data-ttu-id="b3a2a-126">Nie masz żadnego z tych?</span><span class="sxs-lookup"><span data-stu-id="b3a2a-126">Don't have any of those?</span></span> <span data-ttu-id="b3a2a-127">Zakończenie hello [szybkiego startu 5 minutową](https://aka.ms/acdbtnetqs) lub hello [samouczek developer](https://aka.ms/acdbtabletut) toocreate konta i wypełnić bazę danych.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-127">Complete hello [five-minute quickstart](https://aka.ms/acdbtnetqs) or hello [developer tutorial](https://aka.ms/acdbtabletut) toocreate an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="b3a2a-128">Zapytanie dotyczące PartitionKey i RowKey</span><span class="sxs-lookup"><span data-stu-id="b3a2a-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="b3a2a-129">Ponieważ właściwości PartitionKey i RowKey hello tworzą klucza podstawowego jednostki, można użyć powitania po jednostki hello tooidentify specjalnej składni:</span><span class="sxs-lookup"><span data-stu-id="b3a2a-129">Because hello PartitionKey and RowKey properties form an entity's primary key, you can use hello following special syntax tooidentify hello entity:</span></span> 

<span data-ttu-id="b3a2a-130">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="b3a2a-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="b3a2a-131">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="b3a2a-131">**Results**</span></span>

| <span data-ttu-id="b3a2a-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="b3a2a-132">PartitionKey</span></span> | <span data-ttu-id="b3a2a-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="b3a2a-133">RowKey</span></span> | <span data-ttu-id="b3a2a-134">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="b3a2a-134">Email</span></span> | <span data-ttu-id="b3a2a-135">Numer telefonu</span><span class="sxs-lookup"><span data-stu-id="b3a2a-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b3a2a-136">Harp</span><span class="sxs-lookup"><span data-stu-id="b3a2a-136">Harp</span></span> | <span data-ttu-id="b3a2a-137">Walter</span><span class="sxs-lookup"><span data-stu-id="b3a2a-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="b3a2a-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="b3a2a-138">425-555-0104</span></span> |

<span data-ttu-id="b3a2a-139">Alternatywnie można określić właściwości jako część hello `$filter` opcji, jak pokazano w hello następujących sekcji.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-139">Alternatively, you can specify these properties as part of hello `$filter` option, as shown in hello following section.</span></span> <span data-ttu-id="b3a2a-140">Należy pamiętać, że hello nazw właściwości kluczy i wartości stałe jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-140">Note that hello key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="b3a2a-141">Zarówno hello PartitionKey i właściwości RowKey są typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-141">Both hello PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="b3a2a-142">Zapytanie za pomocą filtru OData</span><span class="sxs-lookup"><span data-stu-id="b3a2a-142">Query by using an OData filter</span></span>
<span data-ttu-id="b3a2a-143">Gdy w przypadku tworzenia ciąg filtru, pamiętać o tych reguł:</span><span class="sxs-lookup"><span data-stu-id="b3a2a-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="b3a2a-144">Operatory logiczne hello Użyj zdefiniowany przez toocompare Specyfikacja protokołu OData hello tooa wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-144">Use hello logical operators defined by hello OData Protocol Specification toocompare a property tooa value.</span></span> <span data-ttu-id="b3a2a-145">Należy pamiętać, że nie można porównać wartości właściwości dynamicznych tooa.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-145">Note that you can't compare a property tooa dynamic value.</span></span> <span data-ttu-id="b3a2a-146">Po jednej stronie powitania wyrażenie musi być stałą.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-146">One side of hello expression must be a constant.</span></span> 
* <span data-ttu-id="b3a2a-147">Hello nazwę właściwości, operator i wartość stała muszą być oddzielone spacjami zakodowane w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-147">hello property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="b3a2a-148">Odstęp jest zakodowane w adresie URL jako `%20`.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="b3a2a-149">Wszystkie części hello ciąg filtru jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-149">All parts of hello filter string are case-sensitive.</span></span> 
* <span data-ttu-id="b3a2a-150">musi być wartością stałą Hello hello tych samych danych typu jako właściwość hello aby hello filtru tooreturn prawidłowe wyniki.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-150">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="b3a2a-151">Aby uzyskać więcej informacji na temat typów obsługiwanych właściwości zobacz [hello opis modelu danych usługi tabel](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="b3a2a-151">For more information about supported property types, see [Understanding hello Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="b3a2a-152">Poniżej przedstawiono przykładowe zapytanie, które pokazuje, jak toofilter przez hello PartitionKey i E-mail właściwości przy użyciu OData `$filter`.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-152">Here's an example query that shows how toofilter by hello PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="b3a2a-153">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="b3a2a-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="b3a2a-154">Aby uzyskać więcej informacji dotyczących sposobu tooconstruct filtru wyrażeń dla różnych typów danych, zobacz [badania tabel i jednostek](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="b3a2a-154">For more information on how tooconstruct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="b3a2a-155">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="b3a2a-155">**Results**</span></span>

| <span data-ttu-id="b3a2a-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="b3a2a-156">PartitionKey</span></span> | <span data-ttu-id="b3a2a-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="b3a2a-157">RowKey</span></span> | <span data-ttu-id="b3a2a-158">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="b3a2a-158">Email</span></span> | <span data-ttu-id="b3a2a-159">Numer telefonu</span><span class="sxs-lookup"><span data-stu-id="b3a2a-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b3a2a-160">Ben</span><span class="sxs-lookup"><span data-stu-id="b3a2a-160">Ben</span></span> |<span data-ttu-id="b3a2a-161">Smith</span><span class="sxs-lookup"><span data-stu-id="b3a2a-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="b3a2a-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="b3a2a-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="b3a2a-163">Zapytanie za pomocą LINQ</span><span class="sxs-lookup"><span data-stu-id="b3a2a-163">Query by using LINQ</span></span> 
<span data-ttu-id="b3a2a-164">Możesz także zbadać za pomocą LINQ, który tłumaczy toohello odpowiedniego wyrażenia zapytania OData.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-164">You can also query by using LINQ, which translates toohello corresponding OData query expressions.</span></span> <span data-ttu-id="b3a2a-165">Poniżej przedstawiono przykład sposobu toobuild zapytania przy użyciu hello zestawu .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="b3a2a-165">Here's an example of how toobuild queries by using hello .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b3a2a-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3a2a-166">Next steps</span></span>

<span data-ttu-id="b3a2a-167">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b3a2a-167">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b3a2a-168">Przedstawiono sposób tooquery przy użyciu hello tabeli interfejsu API (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="b3a2a-168">Learned how tooquery by using hello Table API (preview)</span></span> 

<span data-ttu-id="b3a2a-169">Można teraz kontynuować toohello następny samouczek toolearn jak toodistribute danych globalnie.</span><span class="sxs-lookup"><span data-stu-id="b3a2a-169">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b3a2a-170">Globalny dystrybucji danych</span><span class="sxs-lookup"><span data-stu-id="b3a2a-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
