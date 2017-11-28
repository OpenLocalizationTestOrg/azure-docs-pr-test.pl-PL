---
title: "Przepływność aaaProvision dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset elastycznie przepływności containsers bazy danych Azure rozwiązania Cosmos, kolekcje, wykresów i tabel."
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
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="3cf43-103">Ustaw przepustowość dla kontenerów bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="3cf43-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="3cf43-104">Można określić przepustowość dla kontenerów bazy danych Azure rozwiązania Cosmos w hello portalu Azure lub za pomocą hello zestawy SDK klientów.</span><span class="sxs-lookup"><span data-stu-id="3cf43-104">You can set throughput for your Azure Cosmos DB containers in hello Azure portal or by using hello client SDKs.</span></span> 

<span data-ttu-id="3cf43-105">Witaj w poniższej tabeli wymieniono hello przepustowości dostępnej dla kontenerów:</span><span class="sxs-lookup"><span data-stu-id="3cf43-105">hello following table lists hello throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="3cf43-106"><strong>Kontener jednej partycji</strong></span><span class="sxs-lookup"><span data-stu-id="3cf43-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3cf43-107"><strong>Kontener podzielonym na partycje</strong></span><span class="sxs-lookup"><span data-stu-id="3cf43-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="3cf43-108">Przepustowość minimalna</span><span class="sxs-lookup"><span data-stu-id="3cf43-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3cf43-109">400 jednostek żądań na sekundę</span><span class="sxs-lookup"><span data-stu-id="3cf43-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3cf43-110">2500 jednostki żądania na sekundę</span><span class="sxs-lookup"><span data-stu-id="3cf43-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="3cf43-111">Maksymalna przepustowość</span><span class="sxs-lookup"><span data-stu-id="3cf43-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3cf43-112">10 000 jednostek żądań na sekundę</span><span class="sxs-lookup"><span data-stu-id="3cf43-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="3cf43-113">Nieograniczona liczba</span><span class="sxs-lookup"><span data-stu-id="3cf43-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a><span data-ttu-id="3cf43-114">Przepływność hello tooset przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3cf43-114">tooset hello throughput by using hello Azure portal</span></span>

1. <span data-ttu-id="3cf43-115">W nowym oknie, otwórz hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3cf43-115">In a new window, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3cf43-116">Na pasku po lewej stronie powitania kliknij **bazy danych Azure rozwiązania Cosmos**, lub kliknij przycisk **więcej usług** u dołu hello następnie przewiń zbyt**baz danych**, a następnie kliknij przycisk **bazy danych Azure rozwiązania Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="3cf43-116">On hello left bar, click **Azure Cosmos DB**, or click **More Services** at hello bottom, then scroll too**Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="3cf43-117">Wybierz konto DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3cf43-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="3cf43-118">W nowym oknie powitania kliknij **Eksploratora danych (wersja zapoznawcza)** w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="3cf43-118">In hello new window, click **Data Explorer (Preview)** in hello navigation menu.</span></span>
5. <span data-ttu-id="3cf43-119">W nowym oknie hello, rozwiń węzeł bazy danych i kontener, a następnie kliknij przycisk **& Ustawienia skalowania**.</span><span class="sxs-lookup"><span data-stu-id="3cf43-119">In hello new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="3cf43-120">W nowym oknie hello, wpisz nową wartość przepływności hello w hello **przepływności** , a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3cf43-120">In hello new window, type hello new throughput value in hello **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a><span data-ttu-id="3cf43-121">Przepływność hello tooset przy użyciu hello interfejsu API usługi DocumentDB dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="3cf43-121">tooset hello throughput by using hello DocumentDB API for .NET</span></span>

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="3cf43-122">Przepływność — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="3cf43-122">Throughput FAQ</span></span>

<span data-ttu-id="3cf43-123">**Można ustawić Mój tooless przepływności niż 400 RU/s?**</span><span class="sxs-lookup"><span data-stu-id="3cf43-123">**Can I set my throughput tooless than 400 RU/s?**</span></span>

<span data-ttu-id="3cf43-124">400 RU/s jest hello minimalną przepustowość na kolekcje z jedną partycją DB rozwiązania Cosmos (minimum dla kolekcji partycjonowanych hello jest 2500 RU/s).</span><span class="sxs-lookup"><span data-stu-id="3cf43-124">400 RU/s is hello minimum throughput available on Cosmos DB single partition collections (2500 RU/s is hello minimum for partitioned collections).</span></span> <span data-ttu-id="3cf43-125">Żądanie jednostki są ustawiane w 100 RU/s odstępach czasu, ale przepływności nie można ustawić too100 RU/s lub dowolna wartość mniejszą niż 400 RU/s.</span><span class="sxs-lookup"><span data-stu-id="3cf43-125">Request units are set in 100 RU/s intervals, but throughput cannot be set too100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="3cf43-126">Jeśli szukasz toodevelop ekonomiczne — metoda i przetestować rozwiązania Cosmos bazy danych, możesz użyć hello wolnego [Azure rozwiązania Cosmos DB emulatora](local-emulator.md), które można wdrożyć lokalnie bez ponoszenia kosztów.</span><span class="sxs-lookup"><span data-stu-id="3cf43-126">If you're looking for a cost effective method toodevelop and test Cosmos DB, you can use hello free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="3cf43-127">**Jak ustawić througput przy użyciu hello bazy danych MongoDB interfejsu API?**</span><span class="sxs-lookup"><span data-stu-id="3cf43-127">**How do I set througput using hello MongoDB API?**</span></span>

<span data-ttu-id="3cf43-128">Nie ma żadnych przepływności tooset rozszerzenia interfejsu API bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="3cf43-128">There's no MongoDB API extension tooset throughput.</span></span> <span data-ttu-id="3cf43-129">Witaj zalecane jest hello toouse interfejsu API usługi DocumentDB, jak pokazano w [tooset hello przepływność przy użyciu hello interfejsu API usługi DocumentDB dla platformy .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="3cf43-129">hello recommendation is toouse hello DocumentDB API, as shown in [tooset hello throughput by using hello DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cf43-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3cf43-130">Next steps</span></span>

<span data-ttu-id="3cf43-131">Zobacz toolearn więcej informacji na temat udostępniania i skali planety będzie DB rozwiązania Cosmos [dzielenia na partycje i skalowania rozwiązania Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="3cf43-131">toolearn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
