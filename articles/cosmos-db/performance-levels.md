---
title: "poziomy wydajności aaaDocumentDB interfejsu API | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu poziomy wydajności usługi DocumentDB interfejsu API umożliwiają tooreserve przepływności na podstawie kontenera na."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a><span data-ttu-id="6a283-103">Wycofanie hello poziomy wydajności S1, S2 i S3</span><span class="sxs-lookup"><span data-stu-id="6a283-103">Retiring hello S1, S2, and S3 performance levels</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="6a283-104">Witaj S1, S2 i S3 poziomy wydajności omówione w tym artykule jest wycofana i nie będą już dostępne dla nowych kont usługi DocumentDB interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6a283-104">hello S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB API accounts.</span></span>
>

<span data-ttu-id="6a283-105">Ten artykuł zawiera omówienie poziomów wydajności S1, S2 i S3 i omówiono, jak kolekcje hello, korzystających z tych poziomów wydajności będzie toosingle zmigrowane kolekcje partycji na 1 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6a283-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how hello collections that use these performance levels will be migrated toosingle partition collections on August 1st, 2017.</span></span> <span data-ttu-id="6a283-106">Po przeczytaniu tego artykułu, będziesz w stanie tooanswer hello następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="6a283-106">After reading this article, you'll be able tooanswer hello following questions:</span></span>

- [<span data-ttu-id="6a283-107">Dlaczego są wydajności S1, S2 i S3 hello poziomy wycofana?</span><span class="sxs-lookup"><span data-stu-id="6a283-107">Why are hello S1, S2, and S3 performance levels being retired?</span></span>](#why-retired)
- [<span data-ttu-id="6a283-108">Kolekcje z jedną partycją i kolekcji partycjonowanych porównanie toohello S1, S2, poziomy wydajności S3?</span><span class="sxs-lookup"><span data-stu-id="6a283-108">How do single partition collections and partitioned collections compare toohello S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="6a283-109">Co mogę zrobić muszą tooensure toodo nieprzerwany dostęp do danych toomy?</span><span class="sxs-lookup"><span data-stu-id="6a283-109">What do I need toodo tooensure uninterrupted access toomy data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="6a283-110">Jak mojej kolekcji ulegnie zmianie po migracji hello?</span><span class="sxs-lookup"><span data-stu-id="6a283-110">How will my collection change after hello migration?</span></span>](#collection-change)
- [<span data-ttu-id="6a283-111">Jak Moje rozliczeń ulegnie zmianie po jestem toosingle zmigrowane kolekcje partycji?</span><span class="sxs-lookup"><span data-stu-id="6a283-111">How will my billing change after I’m migrated toosingle partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="6a283-112">Co zrobić, jeśli potrzebna jest więcej niż 10 GB przestrzeni dyskowej?</span><span class="sxs-lookup"><span data-stu-id="6a283-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="6a283-113">Można zmienić między hello poziomy wydajności S1, S2 i S3 przed 1 sierpnia 2017 r?</span><span class="sxs-lookup"><span data-stu-id="6a283-113">Can I change between hello S1, S2, and S3 performance levels before August 1, 2017?</span></span>](#change-before)
- [<span data-ttu-id="6a283-114">Jak wiedzą, gdy został zmigrowany mojej kolekcji?</span><span class="sxs-lookup"><span data-stu-id="6a283-114">How will I know when my collection has migrated?</span></span>](#when-migrated)
- [<span data-ttu-id="6a283-115">Jak przeprowadzić migrację z hello S1, S2, S3 kolekcjami partycji toosingle poziomów wydajności na własną?</span><span class="sxs-lookup"><span data-stu-id="6a283-115">How do I migrate from hello S1, S2, S3 performance levels toosingle partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="6a283-116">Jak m wpływ mam EA klienta?</span><span class="sxs-lookup"><span data-stu-id="6a283-116">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="6a283-117">Dlaczego są wydajności S1, S2 i S3 hello poziomy wycofana?</span><span class="sxs-lookup"><span data-stu-id="6a283-117">Why are hello S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="6a283-118">poziomy wydajności S1, S2 i S3 Hello nie nie elastyczność hello oferty, która oferuje kolekcje interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6a283-118">hello S1, S2, and S3 performance levels do not offer hello flexibility that DocumentDB API collections offers.</span></span> <span data-ttu-id="6a283-119">Hello S1, S2, poziomy wydajności S3, zarówno hello przepływności i pojemność pamięci masowej zostały wstępnie ustawiony i nie zaproponował elastyczność.</span><span class="sxs-lookup"><span data-stu-id="6a283-119">With hello S1, S2, S3 performance levels, both hello throughput and storage capacity were pre-set and did not offer elasticity.</span></span> <span data-ttu-id="6a283-120">Azure DB rozwiązania Cosmos oferuje teraz hello możliwości toocustomize Twojego przepływność i Magazyn, oferty, można znacznie większą elastyczność tooscale Twojego możliwości stosownie do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="6a283-120">Azure Cosmos DB now offers hello ability toocustomize your throughput and storage, offering you much more flexibility in your ability tooscale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a><span data-ttu-id="6a283-121">Kolekcje z jedną partycją i kolekcji partycjonowanych porównanie toohello S1, S2, poziomy wydajności S3?</span><span class="sxs-lookup"><span data-stu-id="6a283-121">How do single partition collections and partitioned collections compare toohello S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="6a283-122">Witaj w poniższej tabeli porównano hello przepływność i Magazyn opcje dostępne w kolekcji partycjonowanych i S1, S2, S3 poziomy wydajności w kolekcje z jedną partycją.</span><span class="sxs-lookup"><span data-stu-id="6a283-122">hello following table compares hello throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="6a283-123">Oto przykład dla regionu nam wschodnie 2:</span><span class="sxs-lookup"><span data-stu-id="6a283-123">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="6a283-124">Kolekcja podzielonym na partycje</span><span class="sxs-lookup"><span data-stu-id="6a283-124">Partitioned collection</span></span>|<span data-ttu-id="6a283-125">Kolekcja jednej partycji</span><span class="sxs-lookup"><span data-stu-id="6a283-125">Single partition collection</span></span>|<span data-ttu-id="6a283-126">S1</span><span class="sxs-lookup"><span data-stu-id="6a283-126">S1</span></span>|<span data-ttu-id="6a283-127">S2</span><span class="sxs-lookup"><span data-stu-id="6a283-127">S2</span></span>|<span data-ttu-id="6a283-128">S3</span><span class="sxs-lookup"><span data-stu-id="6a283-128">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="6a283-129">Maksymalna przepustowość</span><span class="sxs-lookup"><span data-stu-id="6a283-129">Maximum throughput</span></span>|<span data-ttu-id="6a283-130">Nieograniczona liczba</span><span class="sxs-lookup"><span data-stu-id="6a283-130">Unlimited</span></span>|<span data-ttu-id="6a283-131">10 K RU/s</span><span class="sxs-lookup"><span data-stu-id="6a283-131">10K RU/s</span></span>|<span data-ttu-id="6a283-132">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="6a283-132">250 RU/s</span></span>|<span data-ttu-id="6a283-133">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="6a283-133">1 K RU/s</span></span>|<span data-ttu-id="6a283-134">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="6a283-134">2.5 K RU/s</span></span>|
|<span data-ttu-id="6a283-135">Przepustowość minimalna</span><span class="sxs-lookup"><span data-stu-id="6a283-135">Minimum throughput</span></span>|<span data-ttu-id="6a283-136">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="6a283-136">2.5K RU/s</span></span>|<span data-ttu-id="6a283-137">400 RU/s</span><span class="sxs-lookup"><span data-stu-id="6a283-137">400 RU/s</span></span>|<span data-ttu-id="6a283-138">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="6a283-138">250 RU/s</span></span>|<span data-ttu-id="6a283-139">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="6a283-139">1 K RU/s</span></span>|<span data-ttu-id="6a283-140">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="6a283-140">2.5 K RU/s</span></span>|
|<span data-ttu-id="6a283-141">Maksymalna przestrzeń magazynowa</span><span class="sxs-lookup"><span data-stu-id="6a283-141">Maximum storage</span></span>|<span data-ttu-id="6a283-142">Nieograniczona liczba</span><span class="sxs-lookup"><span data-stu-id="6a283-142">Unlimited</span></span>|<span data-ttu-id="6a283-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="6a283-143">10 GB</span></span>|<span data-ttu-id="6a283-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="6a283-144">10 GB</span></span>|<span data-ttu-id="6a283-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="6a283-145">10 GB</span></span>|<span data-ttu-id="6a283-146">10 GB</span><span class="sxs-lookup"><span data-stu-id="6a283-146">10 GB</span></span>|
|<span data-ttu-id="6a283-147">Cena (co miesiąc)</span><span class="sxs-lookup"><span data-stu-id="6a283-147">Price (monthly)</span></span>|<span data-ttu-id="6a283-148">Przepływność: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="6a283-148">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="6a283-149">Magazyn: 0,25 USD/GB</span><span class="sxs-lookup"><span data-stu-id="6a283-149">Storage: $0.25/GB</span></span>|<span data-ttu-id="6a283-150">Przepływność: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="6a283-150">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="6a283-151">Magazyn: 0,25 USD/GB</span><span class="sxs-lookup"><span data-stu-id="6a283-151">Storage: $0.25/GB</span></span>|<span data-ttu-id="6a283-152">$25 USD</span><span class="sxs-lookup"><span data-stu-id="6a283-152">$25 USD</span></span>|<span data-ttu-id="6a283-153">$50 USD</span><span class="sxs-lookup"><span data-stu-id="6a283-153">$50 USD</span></span>|<span data-ttu-id="6a283-154">$100 USD</span><span class="sxs-lookup"><span data-stu-id="6a283-154">$100 USD</span></span>|

<span data-ttu-id="6a283-155">Czy klient EA?</span><span class="sxs-lookup"><span data-stu-id="6a283-155">Are you an EA customer?</span></span> <span data-ttu-id="6a283-156">Jeśli tak, zobacz [am I wpływ mam EA klienta?](#ea-customer)</span><span class="sxs-lookup"><span data-stu-id="6a283-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a><span data-ttu-id="6a283-157">Co mogę zrobić muszą tooensure toodo nieprzerwany dostęp do danych toomy?</span><span class="sxs-lookup"><span data-stu-id="6a283-157">What do I need toodo tooensure uninterrupted access toomy data?</span></span>

<span data-ttu-id="6a283-158">Nothing, DB rozwiązania Cosmos obsługuje migrację hello za Ciebie.</span><span class="sxs-lookup"><span data-stu-id="6a283-158">Nothing, Cosmos DB handles hello migration for you.</span></span> <span data-ttu-id="6a283-159">Jeśli masz kolekcję S1, S2 lub S3 bieżącej kolekcji będą tooa migrowanych kolekcji jednej partycji na 31 lipca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6a283-159">If you have an S1, S2, or S3 collection, your current collection will be migrated tooa single partition collection on July 31, 2017.</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a><span data-ttu-id="6a283-160">Jak mojej kolekcji ulegnie zmianie po migracji hello?</span><span class="sxs-lookup"><span data-stu-id="6a283-160">How will my collection change after hello migration?</span></span>

<span data-ttu-id="6a283-161">Jeśli masz kolekcji S1 będzie tooa migrowanych kolekcji jednej partycji o 400 RU/s przepustowości.</span><span class="sxs-lookup"><span data-stu-id="6a283-161">If you have an S1 collection, you will be migrated tooa single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="6a283-162">400 RU/s jest hello najniższy przepływności dostępne kolekcje z jedną partycją.</span><span class="sxs-lookup"><span data-stu-id="6a283-162">400 RU/s is hello lowest throughput available with single partition collections.</span></span> <span data-ttu-id="6a283-163">Jednak koszt hello 400 RU/s w hello jest Kolekcja jednej partycji w przybliżeniu hello takie same, jak zostały płatność za pomocą kolekcji S1 i 250 RU/s — dzięki nie płatność za hello bardzo 150 tooyou dostępne RU/s.</span><span class="sxs-lookup"><span data-stu-id="6a283-163">However, hello cost for 400 RU/s in hello a single partition collection is approximately hello same as you were paying with your S1 collection and 250 RU/s – so you are not paying for hello extra 150 RU/s available tooyou.</span></span>

<span data-ttu-id="6a283-164">Jeśli masz kolekcji S2 będzie tooa migrowanych kolekcji jednej partycji o 1 K RU/s.</span><span class="sxs-lookup"><span data-stu-id="6a283-164">If you have an S2 collection, you will be migrated tooa single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="6a283-165">Zostanie wyświetlone nie Zmień poziom przepływności tooyour.</span><span class="sxs-lookup"><span data-stu-id="6a283-165">You will see no change tooyour throughput level.</span></span>

<span data-ttu-id="6a283-166">Jeśli masz kolekcji S3 będzie tooa migrowanych kolekcji jednej partycji z 2,5 K RU/s.</span><span class="sxs-lookup"><span data-stu-id="6a283-166">If you have an S3 collection, you will be migrated tooa single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="6a283-167">Zostanie wyświetlone nie Zmień poziom przepływności tooyour.</span><span class="sxs-lookup"><span data-stu-id="6a283-167">You will see no change tooyour throughput level.</span></span>

<span data-ttu-id="6a283-168">W każdym z tych przypadków po migracji kolekcji użytkownik będzie być może toocustomize poziom przepływności lub skalować go w górę i w dół jako wymagane tooprovide małych opóźnieniach dostępu tooyour użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6a283-168">In each of these cases, after your collection is migrated, you will be able toocustomize your throughput level, or scale it up and down as needed tooprovide low-latency access tooyour users.</span></span> <span data-ttu-id="6a283-169">toochange poziomu przepływności powitania po migracji ma kolekcji po prostu otwórz konto DB rozwiązania Cosmos w hello portalu Azure kliknij skali, wybierz kolekcję, a następnie Dostosuj poziom przepływności hello, jak pokazano w powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="6a283-169">toochange hello throughput level after your collection has migrated, simply open your Cosmos DB account in hello Azure portal, click Scale, choose your collection, and then adjust hello throughput level, as shown in hello following screenshot:</span></span>

![Jak tooscale przepływność w hello portalu Azure](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a><span data-ttu-id="6a283-171">Jak Moje rozliczeń ulegnie zmianie po jestem toohello zmigrowane kolekcje z jedną partycją?</span><span class="sxs-lookup"><span data-stu-id="6a283-171">How will my billing change after I’m migrated toohello single partition collections?</span></span>

<span data-ttu-id="6a283-172">Wykonując zawiera 10 kolekcji S1, 1 GB pamięci masowej dla każdego regionu nam wschodnie hello, i migracji tych 10 S1 kolekcje too10 kolekcje z jedną partycją na 400 RU/s (minimalny poziom hello).</span><span class="sxs-lookup"><span data-stu-id="6a283-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in hello US East region, and you migrate these 10 S1 collections too10 single partition collections at 400 RU/sec (hello minimum level).</span></span> <span data-ttu-id="6a283-173">Jeśli zachowasz hello kolekcje 10 jednej partycji dla całego miesiąca, rachunku będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="6a283-173">Your bill will look as follows if you keep hello 10 single partition collections for a full month:</span></span>

![Jak S1 ceny 10 kolekcje porównuje too10 kolekcji przy użyciu ceny Kolekcja jednej partycji](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="6a283-175">Co zrobić, jeśli potrzebna jest więcej niż 10 GB przestrzeni dyskowej?</span><span class="sxs-lookup"><span data-stu-id="6a283-175">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="6a283-176">Czy masz kolekcję o poziomie wydajności S1, S2 lub S3 lub mieć Kolekcja jednej partycji, które mają 10 GB dostępnego miejsca, można użyć toomigrate narzędzia migracji danych DB rozwiązania Cosmos hello tooa Twojego danych praktycznie na partycje kolekcji nieograniczony magazyn.</span><span class="sxs-lookup"><span data-stu-id="6a283-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use hello Cosmos DB Data Migration tool toomigrate your data tooa partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="6a283-177">Aby uzyskać informacje dotyczące korzyści hello kolekcję partycjonowaną, zobacz [dzielenia na partycje i skalowania w usłudze Azure DB rozwiązania Cosmos](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="6a283-177">For information about hello benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="6a283-178">Aby uzyskać informacje dotyczące toomigrate można znaleźć S1, S2, S3 lub kolekcji tooa podzielona na partycje Kolekcja jednej partycji, [migracji z jednej partycji toopartitioned kolekcji](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="6a283-178">For information about how toomigrate your S1, S2, S3, or single partition collection tooa partitioned collection, see [Migrating from single-partition toopartitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a><span data-ttu-id="6a283-179">Można zmienić między hello poziomy wydajności S1, S2 i S3 przed 1 sierpnia 2017 r?</span><span class="sxs-lookup"><span data-stu-id="6a283-179">Can I change between hello S1, S2, and S3 performance levels before August 1, 2017?</span></span>

<span data-ttu-id="6a283-180">Istniejące konta tylko z wydajnością S1, S2 i S3 zostanie stanie toochange i zmieniać warstwy poziomu wydajności za pośrednictwem portalu hello lub programowo.</span><span class="sxs-lookup"><span data-stu-id="6a283-180">Only existing accounts with S1, S2, and S3 performance will be able toochange and alter performance level tiers through hello portal or programmatically.</span></span> <span data-ttu-id="6a283-181">1 sierpnia 2017 hello S1, S2, i poziomy wydajności S3 nie będą już dostępne.</span><span class="sxs-lookup"><span data-stu-id="6a283-181">By August 1, 2017, hello S1, S2, and S3 performance levels will no longer be available.</span></span> <span data-ttu-id="6a283-182">W przypadku zmiany z kolekcji jednej partycji tooa S1 S3 i S3 nie może zwracać toohello poziomy wydajności S1, S2 lub S3.</span><span class="sxs-lookup"><span data-stu-id="6a283-182">If you change from S1, S3, or S3 tooa single partition collection, you cannot return toohello S1, S2, or S3 performance levels.</span></span>

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a><span data-ttu-id="6a283-183">Jak wiedzą, gdy został zmigrowany mojej kolekcji?</span><span class="sxs-lookup"><span data-stu-id="6a283-183">How will I know when my collection has migrated?</span></span>

<span data-ttu-id="6a283-184">Witaj migracji nastąpi na 31 lipca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6a283-184">hello migration will occur on July 31, 2017.</span></span> <span data-ttu-id="6a283-185">Jeśli masz kolekcję używającą hello S1, S2 lub poziomy wydajności S3, zespołu DB rozwiązania Cosmos hello skontaktuje się z Tobą za pośrednictwem poczty e-mail przed dokonaniem migracji hello.</span><span class="sxs-lookup"><span data-stu-id="6a283-185">If you have a collection that uses hello S1, S2 or S3 performance levels, hello Cosmos DB team will contact you by email before hello migration takes place.</span></span> <span data-ttu-id="6a283-186">Po zakończeniu migracji hello, na 1 sierpnia 2017 hello portalu Azure zostaną wyświetlone kolekcji używany cen warstwy standardowa.</span><span class="sxs-lookup"><span data-stu-id="6a283-186">Once hello migration is complete, on August 1, 2017, hello Azure portal will show that your collection uses Standard pricing.</span></span>

![Jak tooconfirm kolekcji ma warstwy cenowej standardowa toohello migracji](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a><span data-ttu-id="6a283-188">Jak przeprowadzić migrację z hello S1, S2, S3 kolekcjami partycji toosingle poziomów wydajności na własną?</span><span class="sxs-lookup"><span data-stu-id="6a283-188">How do I migrate from hello S1, S2, S3 performance levels toosingle partition collections on my own?</span></span>

<span data-ttu-id="6a283-189">Można migrować z hello S1, S2, a kolekcje partycji toosingle przy użyciu portalu Azure hello poziomy wydajności S3 lub programowo.</span><span class="sxs-lookup"><span data-stu-id="6a283-189">You can migrate from hello S1, S2, and S3 performance levels toosingle partition collections using hello Azure portal or programmatically.</span></span> <span data-ttu-id="6a283-190">Można to zrobić na własnych przed 1 sierpnia toobenefit z hello przepływności elastyczne opcje kolekcje z jedną partycją lub będziemy kolekcji można migrować na 31 lipca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6a283-190">You can do this on your own before August 1 toobenefit from hello flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span></span>

<span data-ttu-id="6a283-191">**kolekcje z partycją toosingle toomigrate przy użyciu hello portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="6a283-191">**toomigrate toosingle partition collections using hello Azure portal**</span></span>

1. <span data-ttu-id="6a283-192">W hello [ **portalu Azure**](https://portal.azure.com), kliknij przycisk **bazy danych Azure rozwiązania Cosmos**, następnie wybierz hello DB rozwiązania Cosmos konta toomodify.</span><span class="sxs-lookup"><span data-stu-id="6a283-192">In hello [**Azure portal**](https://portal.azure.com), click **Azure Cosmos DB**, then select hello Cosmos DB account toomodify.</span></span> 
 
    <span data-ttu-id="6a283-193">Jeśli **bazy danych Azure rozwiązania Cosmos** nie jest na hello przechodzenia kliknij pozycję >, przewiń zbyt**baz danych**, wybierz pozycję **bazy danych Azure rozwiązania Cosmos**, a następnie wybierz konto usługi DocumentDB hello.</span><span class="sxs-lookup"><span data-stu-id="6a283-193">If **Azure Cosmos DB** is not on hello Jumpbar, click >, scroll too**Databases**, select **Azure Cosmos DB**, and then select hello DocumentDB account.</span></span>  

2. <span data-ttu-id="6a283-194">W menu zasobów hello w obszarze **kontenery**, kliknij przycisk **skali**, wybierz z listy rozwijanej hello hello toomodify kolekcji, a następnie kliknij przycisk **warstwy cenowej**.</span><span class="sxs-lookup"><span data-stu-id="6a283-194">On hello resource menu, under **Containers**, click **Scale**, select hello collection toomodify from hello drop-down list, and then click **Pricing Tier**.</span></span> <span data-ttu-id="6a283-195">Konta przy użyciu wstępnie zdefiniowanych przepływności mają warstwy cenowej S1, S2 lub S3.</span><span class="sxs-lookup"><span data-stu-id="6a283-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span></span>  <span data-ttu-id="6a283-196">W hello **wybierz warstwę cenową** bloku, kliknij przycisk **standardowe** toochange zdefiniowane toouser przepływności, a następnie kliknij przycisk **wybierz** toosave zmiany.</span><span class="sxs-lookup"><span data-stu-id="6a283-196">In hello **Choose your pricing tier** blade, click **Standard** toochange toouser-defined throughput, and then click **Select** toosave your change.</span></span>

    ![Zrzut ekranu przedstawiający blok ustawień hello pokazujący, gdzie toochange hello wartość przepływności](./media/performance-levels/change-performance-set-thoughput.png)

3. <span data-ttu-id="6a283-198">Po powrocie do hello **skali** bloku, hello **warstwy cenowej** zostanie zmieniona zbyt**standardowe** i hello **przepływności (RU/s)** zostanie wyświetlone okno z Wartość domyślna 400.</span><span class="sxs-lookup"><span data-stu-id="6a283-198">Back in hello **Scale** blade, hello **Pricing Tier** is changed too**Standard** and hello **Throughput (RU/s)** box is displayed with a default value of 400.</span></span> <span data-ttu-id="6a283-199">Zestaw hello przepływności od 400 do 10 000 [jednostek żądania](request-units.md)/second (RU/s).</span><span class="sxs-lookup"><span data-stu-id="6a283-199">Set hello throughput between 400 and 10,000 [Request units](request-units.md)/second (RU/s).</span></span> <span data-ttu-id="6a283-200">Witaj **Szacowana kwota rachunku miesięczne** u dołu hello hello strony automatycznie aktualizuje tooprovide szacunkową hello koszt co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="6a283-200">hello **Estimated Monthly Bill** at hello bottom of hello page updates automatically tooprovide an estimate of hello monthly cost.</span></span> 

    >[!IMPORTANT] 
    > <span data-ttu-id="6a283-201">Po zapisaniu zmian i przenieść toohello warstwy cenowej standardowa, nie można wycofać toohello poziomy wydajności S1, S2 lub S3.</span><span class="sxs-lookup"><span data-stu-id="6a283-201">Once you save your changes and move toohello Standard pricing tier, you cannot roll back toohello S1, S2, or S3 performance levels.</span></span>

4. <span data-ttu-id="6a283-202">Kliknij przycisk **zapisać** toosave zmiany.</span><span class="sxs-lookup"><span data-stu-id="6a283-202">Click **Save** toosave your changes.</span></span>

    <span data-ttu-id="6a283-203">Jeśli okaże się, że potrzebujesz więcej przepływności (większe niż 10 000 RU/s) lub więcej pamięci masowej (większe niż 10GB) można utworzyć kolekcję partycjonowaną.</span><span class="sxs-lookup"><span data-stu-id="6a283-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span></span> <span data-ttu-id="6a283-204">toomigrate kolekcji tooa podzielona na partycje Kolekcja jednej partycji, zobacz [migracji z jednej partycji toopartitioned kolekcji](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="6a283-204">toomigrate a single partition collection tooa partitioned collection, see [Migrating from single-partition toopartitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span>

    > [!NOTE]
    > <span data-ttu-id="6a283-205">Zmiana z tooStandard S1, S2 lub S3 może trwać too2 minut.</span><span class="sxs-lookup"><span data-stu-id="6a283-205">Changing from S1, S2, or S3 tooStandard may take up too2 minutes.</span></span>
    > 
    > 

<span data-ttu-id="6a283-206">**kolekcje z partycją toosingle toomigrate przy użyciu zestawu .NET SDK hello**</span><span class="sxs-lookup"><span data-stu-id="6a283-206">**toomigrate toosingle partition collections using hello .NET SDK**</span></span>

<span data-ttu-id="6a283-207">Inną opcją w przypadku zmiany poziomów wydajności z kolekcji jest przez nasze zestawy SDK.</span><span class="sxs-lookup"><span data-stu-id="6a283-207">Another option for changing your collections' performance levels is through our SDKs.</span></span> <span data-ttu-id="6a283-208">W tej sekcji opisano tylko zmiana wydajności kolekcji poziomu przy użyciu naszych [interfejsu API platformy .NET usługi DocumentDB](documentdb-sdk-dotnet.md), ale hello proces jest podobny do naszych innych zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="6a283-208">This section only covers changing a collection's performance level using our [DocumentDB .NET API](documentdb-sdk-dotnet.md), but hello process is similar for our other SDKs.</span></span>

<span data-ttu-id="6a283-209">Oto fragment kodu dla zmiana too5 przepływność kolekcji hello, 000 jednostek żądań na sekundę:</span><span class="sxs-lookup"><span data-stu-id="6a283-209">Here is a code snippet for changing hello collection throughput too5,000 request units per second:</span></span>
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="6a283-210">Odwiedź stronę [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview dodatkowe przykłady i Dowiedz się więcej o naszym metody oferta:</span><span class="sxs-lookup"><span data-stu-id="6a283-210">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="6a283-211">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="6a283-211">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="6a283-212">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="6a283-212">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="6a283-213">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="6a283-213">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="6a283-214">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="6a283-214">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="6a283-215">Jak m wpływ mam EA klienta?</span><span class="sxs-lookup"><span data-stu-id="6a283-215">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="6a283-216">Umowa EA klienci będą cen chronione do końca hello Umowa.</span><span class="sxs-lookup"><span data-stu-id="6a283-216">EA customers will be price protected until hello end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a283-217">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a283-217">Next steps</span></span>
<span data-ttu-id="6a283-218">toolearn więcej informacji o cenach i zarządzanie danymi za pomocą usługi Azure rozwiązania Cosmos bazy danych, zapoznaj się z tymi zasobami:</span><span class="sxs-lookup"><span data-stu-id="6a283-218">toolearn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span></span>

1.  <span data-ttu-id="6a283-219">[Partycjonowanie danych w bazie danych rozwiązania Cosmos](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="6a283-219">[Partitioning data in Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="6a283-220">Zrozumieć różnicę hello kontenera jednej partycji i kontenery podzielonym na partycje, a także wskazówki dotyczące implementowania bezproblemowo partycjonowania tooscale strategii.</span><span class="sxs-lookup"><span data-stu-id="6a283-220">Understand hello difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy tooscale seamlessly.</span></span>
2.  <span data-ttu-id="6a283-221">[Cennik rozwiązania cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="6a283-221">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> <span data-ttu-id="6a283-222">Więcej informacji na temat hello koszt obsługi przepływności i korzystanie z magazynu.</span><span class="sxs-lookup"><span data-stu-id="6a283-222">Learn about hello cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="6a283-223">[Jednostek żądania](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="6a283-223">[Request units](request-units.md).</span></span> <span data-ttu-id="6a283-224">Zrozumienie hello zużycie przepustowości dla różnych operacji typów, na przykład Odczyt, zapis zapytania.</span><span class="sxs-lookup"><span data-stu-id="6a283-224">Understand hello consumption of throughput for different operation types, for example Read, Write, Query.</span></span>
