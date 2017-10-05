---
title: "Przepływność udostępniania dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak ustawić udostępnionej przepływności dla containsers bazy danych Azure rozwiązania Cosmos, kolekcje, wykresów i tabel."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: d541bb19ba7e5ecb44c9fe91b1e232d4d9c2170e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="54d3b-103">Ustaw przepustowość dla kontenerów bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="54d3b-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="54d3b-104">Przepływność można ustawić dla kontenerów bazy danych Azure rozwiązania Cosmos w portalu Azure lub za pomocą zestawów SDK klienta.</span><span class="sxs-lookup"><span data-stu-id="54d3b-104">You can set throughput for your Azure Cosmos DB containers in the Azure portal or by using the client SDKs.</span></span> 

<span data-ttu-id="54d3b-105">W poniższej tabeli wymieniono dostępne dla kontenerów przepływności:</span><span class="sxs-lookup"><span data-stu-id="54d3b-105">The following table lists the throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="54d3b-106"><strong>Kontener jednej partycji</strong></span><span class="sxs-lookup"><span data-stu-id="54d3b-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="54d3b-107"><strong>Kontener podzielonym na partycje</strong></span><span class="sxs-lookup"><span data-stu-id="54d3b-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="54d3b-108">Przepustowość minimalna</span><span class="sxs-lookup"><span data-stu-id="54d3b-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="54d3b-109">400 jednostek żądań na sekundę</span><span class="sxs-lookup"><span data-stu-id="54d3b-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="54d3b-110">2500 jednostki żądania na sekundę</span><span class="sxs-lookup"><span data-stu-id="54d3b-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="54d3b-111">Maksymalna przepustowość</span><span class="sxs-lookup"><span data-stu-id="54d3b-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="54d3b-112">10 000 jednostek żądań na sekundę</span><span class="sxs-lookup"><span data-stu-id="54d3b-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="54d3b-113">Nieograniczona liczba</span><span class="sxs-lookup"><span data-stu-id="54d3b-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="to-set-the-throughput-by-using-the-azure-portal"></a><span data-ttu-id="54d3b-114">Aby ustawić przepływność przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="54d3b-114">To set the throughput by using the Azure portal</span></span>

1. <span data-ttu-id="54d3b-115">Otwórz w nowym oknie, [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="54d3b-115">In a new window, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="54d3b-116">Na pasku po lewej stronie kliknij **bazy danych Azure rozwiązania Cosmos**, lub kliknij przycisk **więcej usług** u dołu, następnie przewiń do **baz danych**, a następnie kliknij przycisk **bazy danych Azure rozwiązania Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="54d3b-116">On the left bar, click **Azure Cosmos DB**, or click **More Services** at the bottom, then scroll to **Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="54d3b-117">Wybierz konto DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="54d3b-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="54d3b-118">W nowym oknie kliknij **Eksploratora danych (wersja zapoznawcza)** w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="54d3b-118">In the new window, click **Data Explorer (Preview)** in the navigation menu.</span></span>
5. <span data-ttu-id="54d3b-119">W nowym oknie, rozwiń węzeł bazy danych i kontener, a następnie kliknij przycisk **& Ustawienia skalowania**.</span><span class="sxs-lookup"><span data-stu-id="54d3b-119">In the new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="54d3b-120">W nowym oknie, wpisz nową wartość przepływności w **przepływności** , a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="54d3b-120">In the new window, type the new throughput value in the **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="to-set-the-throughput-by-using-the-documentdb-api-for-net"></a><span data-ttu-id="54d3b-121">Aby ustawić przepływność przy użyciu interfejsu API usługi DocumentDB dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="54d3b-121">To set the throughput by using the DocumentDB API for .NET</span></span>

```C#
//Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to the new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="54d3b-122">Przepływność — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="54d3b-122">Throughput FAQ</span></span>

<span data-ttu-id="54d3b-123">**Można ustawić Moje przepływności na mniej niż 400 RU/s?**</span><span class="sxs-lookup"><span data-stu-id="54d3b-123">**Can I set my throughput to less than 400 RU/s?**</span></span>

<span data-ttu-id="54d3b-124">400 RU/s jest minimalna przepływność dostępne na kolekcje z jedną partycją DB rozwiązania Cosmos (minimum dla kolekcji partycjonowanych to 2500 RU/s).</span><span class="sxs-lookup"><span data-stu-id="54d3b-124">400 RU/s is the minimum throughput available on Cosmos DB single partition collections (2500 RU/s is the minimum for partitioned collections).</span></span> <span data-ttu-id="54d3b-125">Żądanie jednostki są ustawiane w 100 RU/s odstępach czasu, ale przepływności nie można ustawić na 100 RU/s lub dowolną wartość mniejszą niż 400 RU/s.</span><span class="sxs-lookup"><span data-stu-id="54d3b-125">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="54d3b-126">Jeśli szukasz ekonomiczne metody umożliwiające opracowanie i przetestowanie rozwiązania Cosmos DB mogą korzystać z BEZPŁATNEJ [Azure rozwiązania Cosmos DB emulatora](local-emulator.md), które można wdrożyć lokalnie bez ponoszenia kosztów.</span><span class="sxs-lookup"><span data-stu-id="54d3b-126">If you're looking for a cost effective method to develop and test Cosmos DB, you can use the free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="54d3b-127">**Jak ustawić througput przy użyciu interfejsu API bazy danych MongoDB?**</span><span class="sxs-lookup"><span data-stu-id="54d3b-127">**How do I set througput using the MongoDB API?**</span></span>

<span data-ttu-id="54d3b-128">Brak bez rozszerzenia interfejsu API bazy danych MongoDB, można ustawić przepływności.</span><span class="sxs-lookup"><span data-stu-id="54d3b-128">There's no MongoDB API extension to set throughput.</span></span> <span data-ttu-id="54d3b-129">Zalecane jest używanie interfejsu API usługi DocumentDB, jak pokazano w [można ustawić przepływność przy użyciu interfejsu API usługi DocumentDB dla platformy .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="54d3b-129">The recommendation is to use the DocumentDB API, as shown in [To set the throughput by using the DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54d3b-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54d3b-130">Next steps</span></span>

<span data-ttu-id="54d3b-131">Aby dowiedzieć się więcej o zasięgu planety będzie DB rozwiązania Cosmos i udostępniania, zobacz [dzielenia na partycje i skalowania rozwiązania Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="54d3b-131">To learn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
