---
title: "Jak wykonać zapytanie dotyczące tabeli danych w usłudze Azure DB rozwiązania Cosmos? | Microsoft Docs"
description: "Dowiedz się, jak dane tabeli zapytania w usłudze Azure DB rozwiązania Cosmos"
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
ms.openlocfilehash: e59cfa85c6bf584e44bdc6e88cc19d67df390041
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a><span data-ttu-id="e2e23-104">Azure DB rozwiązania Cosmos: Jak wykonać zapytanie tabeli danych przy użyciu interfejsu API tabeli (wersja zapoznawcza)?</span><span class="sxs-lookup"><span data-stu-id="e2e23-104">Azure Cosmos DB: How to query table data by using the Table API (preview)?</span></span>

<span data-ttu-id="e2e23-105">Azure DB rozwiązania Cosmos [API tabeli](table-introduction.md) (wersja zapoznawcza) obsługuje OData i [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) zapytań dotyczących danych klucz wartość (tabeli).</span><span class="sxs-lookup"><span data-stu-id="e2e23-105">The Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="e2e23-106">W tym artykule opisano następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="e2e23-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e2e23-107">Wykonywanie zapytania na danych przy użyciu interfejsu API tabeli</span><span class="sxs-lookup"><span data-stu-id="e2e23-107">Querying data with the Table API</span></span>

<span data-ttu-id="e2e23-108">Zapytania w tym artykule, skorzystaj z poniższego przykładu `People` tabeli:</span><span class="sxs-lookup"><span data-stu-id="e2e23-108">The queries in this article use the following sample `People` table:</span></span>

| <span data-ttu-id="e2e23-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="e2e23-109">PartitionKey</span></span> | <span data-ttu-id="e2e23-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="e2e23-110">RowKey</span></span> | <span data-ttu-id="e2e23-111">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="e2e23-111">Email</span></span> | <span data-ttu-id="e2e23-112">Numer telefonu</span><span class="sxs-lookup"><span data-stu-id="e2e23-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e2e23-113">Harp</span><span class="sxs-lookup"><span data-stu-id="e2e23-113">Harp</span></span> | <span data-ttu-id="e2e23-114">Walter</span><span class="sxs-lookup"><span data-stu-id="e2e23-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="e2e23-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="e2e23-115">425-555-0101</span></span> |
| <span data-ttu-id="e2e23-116">Smith</span><span class="sxs-lookup"><span data-stu-id="e2e23-116">Smith</span></span> | <span data-ttu-id="e2e23-117">Ben</span><span class="sxs-lookup"><span data-stu-id="e2e23-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="e2e23-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="e2e23-118">425-555-0102</span></span> |
| <span data-ttu-id="e2e23-119">Smith</span><span class="sxs-lookup"><span data-stu-id="e2e23-119">Smith</span></span> | <span data-ttu-id="e2e23-120">Jan</span><span class="sxs-lookup"><span data-stu-id="e2e23-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="e2e23-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="e2e23-121">425-555-0104</span></span> | 

<span data-ttu-id="e2e23-122">Ponieważ bazy danych Azure rozwiązania Cosmos jest zgodny z interfejsami API magazynu tabel Azure, zobacz [badania tabel i jednostek] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) Aby uzyskać więcej informacji na temat sposobu zapytania przy użyciu tabeli INTERFEJS API.</span><span class="sxs-lookup"><span data-stu-id="e2e23-122">Because Azure Cosmos DB is compatible with the Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span></span> 

<span data-ttu-id="e2e23-123">Aby uzyskać więcej informacji na możliwości premium, które oferuje bazy danych rozwiązania Cosmos Azure, zobacz [bazy danych Azure rozwiązania Cosmos: API tabeli](table-introduction.md) i [opracowanie przy użyciu interfejsu API tabeli w programie .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e2e23-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e2e23-124">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e2e23-124">Prerequisites</span></span>

<span data-ttu-id="e2e23-125">Dla tych zapytań do pracy musi mieć konto bazy danych Azure rozwiązania Cosmos i danych jednostki w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="e2e23-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span></span> <span data-ttu-id="e2e23-126">Nie masz żadnego z tych?</span><span class="sxs-lookup"><span data-stu-id="e2e23-126">Don't have any of those?</span></span> <span data-ttu-id="e2e23-127">Zakończenie [szybkiego startu 5 minutową](https://aka.ms/acdbtnetqs) lub [samouczek developer](https://aka.ms/acdbtabletut) Tworzenie konta usługi i umieścić w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="e2e23-127">Complete the [five-minute quickstart](https://aka.ms/acdbtnetqs) or the [developer tutorial](https://aka.ms/acdbtabletut) to create an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="e2e23-128">Zapytanie dotyczące PartitionKey i RowKey</span><span class="sxs-lookup"><span data-stu-id="e2e23-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="e2e23-129">Ponieważ właściwości PartitionKey i RowKey tworzą klucza podstawowego jednostki, aby zidentyfikować jednostki można użyć następującej składni specjalne:</span><span class="sxs-lookup"><span data-stu-id="e2e23-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span></span> 

<span data-ttu-id="e2e23-130">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="e2e23-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="e2e23-131">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="e2e23-131">**Results**</span></span>

| <span data-ttu-id="e2e23-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="e2e23-132">PartitionKey</span></span> | <span data-ttu-id="e2e23-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="e2e23-133">RowKey</span></span> | <span data-ttu-id="e2e23-134">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="e2e23-134">Email</span></span> | <span data-ttu-id="e2e23-135">Numer telefonu</span><span class="sxs-lookup"><span data-stu-id="e2e23-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e2e23-136">Harp</span><span class="sxs-lookup"><span data-stu-id="e2e23-136">Harp</span></span> | <span data-ttu-id="e2e23-137">Walter</span><span class="sxs-lookup"><span data-stu-id="e2e23-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="e2e23-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="e2e23-138">425-555-0104</span></span> |

<span data-ttu-id="e2e23-139">Alternatywnie można określić właściwości jako część `$filter` opcji, jak pokazano w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e2e23-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span></span> <span data-ttu-id="e2e23-140">Należy pamiętać, że nazw właściwości kluczy i wartości stałe jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="e2e23-140">Note that the key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="e2e23-141">Właściwości PartitionKey i RowKey są typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="e2e23-141">Both the PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="e2e23-142">Zapytanie za pomocą filtru OData</span><span class="sxs-lookup"><span data-stu-id="e2e23-142">Query by using an OData filter</span></span>
<span data-ttu-id="e2e23-143">Gdy w przypadku tworzenia ciąg filtru, pamiętać o tych reguł:</span><span class="sxs-lookup"><span data-stu-id="e2e23-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="e2e23-144">Aby porównać właściwości na wartość, należy użyć operatorów logicznych w specyfikacji protokołu OData.</span><span class="sxs-lookup"><span data-stu-id="e2e23-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span></span> <span data-ttu-id="e2e23-145">Należy pamiętać, że nie można porównać właściwości na wartość dynamiczną.</span><span class="sxs-lookup"><span data-stu-id="e2e23-145">Note that you can't compare a property to a dynamic value.</span></span> <span data-ttu-id="e2e23-146">Po jednej stronie wyrażenia musi być stałą.</span><span class="sxs-lookup"><span data-stu-id="e2e23-146">One side of the expression must be a constant.</span></span> 
* <span data-ttu-id="e2e23-147">Nazwa właściwości, operator i wartość stała muszą być oddzielone spacjami zakodowane w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="e2e23-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="e2e23-148">Odstęp jest zakodowane w adresie URL jako `%20`.</span><span class="sxs-lookup"><span data-stu-id="e2e23-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="e2e23-149">Wszystkie części ciąg filtru jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="e2e23-149">All parts of the filter string are case-sensitive.</span></span> 
* <span data-ttu-id="e2e23-150">Stała wartość musi być tego samego typu danych jako wartość właściwości w kolejności filtru do zwrócenia prawidłowe wyniki.</span><span class="sxs-lookup"><span data-stu-id="e2e23-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="e2e23-151">Aby uzyskać więcej informacji na temat typów obsługiwanych właściwości zobacz [opis modelu danych usługi tabel](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="e2e23-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="e2e23-152">Poniżej przedstawiono przykładowe zapytanie, które pokazuje, jak do filtrowania według właściwości PartitionKey i poczty E-mail przy użyciu OData `$filter`.</span><span class="sxs-lookup"><span data-stu-id="e2e23-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="e2e23-153">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="e2e23-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="e2e23-154">Aby uzyskać więcej informacji dotyczących sposobu tworzenia wyrażenia filtru dla różnych typów danych, zobacz [badania tabel i jednostek](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="e2e23-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="e2e23-155">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="e2e23-155">**Results**</span></span>

| <span data-ttu-id="e2e23-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="e2e23-156">PartitionKey</span></span> | <span data-ttu-id="e2e23-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="e2e23-157">RowKey</span></span> | <span data-ttu-id="e2e23-158">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="e2e23-158">Email</span></span> | <span data-ttu-id="e2e23-159">Numer telefonu</span><span class="sxs-lookup"><span data-stu-id="e2e23-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e2e23-160">Ben</span><span class="sxs-lookup"><span data-stu-id="e2e23-160">Ben</span></span> |<span data-ttu-id="e2e23-161">Smith</span><span class="sxs-lookup"><span data-stu-id="e2e23-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="e2e23-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="e2e23-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="e2e23-163">Zapytanie za pomocą LINQ</span><span class="sxs-lookup"><span data-stu-id="e2e23-163">Query by using LINQ</span></span> 
<span data-ttu-id="e2e23-164">Możesz także zbadać za pomocą LINQ, co oznacza odpowiedniego wyrażenia zapytania OData.</span><span class="sxs-lookup"><span data-stu-id="e2e23-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span></span> <span data-ttu-id="e2e23-165">Oto przykład sposobu tworzenia zapytań przy użyciu zestawu .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="e2e23-165">Here's an example of how to build queries by using the .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e2e23-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e2e23-166">Next steps</span></span>

<span data-ttu-id="e2e23-167">W tym samouczku wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="e2e23-167">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2e23-168">Przedstawiono sposób tworzenia zapytań przy użyciu interfejsu API tabeli (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="e2e23-168">Learned how to query by using the Table API (preview)</span></span> 

<span data-ttu-id="e2e23-169">Możesz teraz przejść do następnym samouczku informacje na temat dystrybucji danych globalnie.</span><span class="sxs-lookup"><span data-stu-id="e2e23-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e2e23-170">Globalny dystrybucji danych</span><span class="sxs-lookup"><span data-stu-id="e2e23-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
