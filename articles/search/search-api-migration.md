---
title: "toohello aaaUpgrading interfejsu API REST usługi wyszukiwanie Azure w wersji 2016-09-01 | Dokumentacja firmy Microsoft"
description: "Uaktualnianie toohello interfejsu API REST usługi wyszukiwanie Azure w wersji 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="5b8c3-103">Uaktualnianie toohello interfejsu API REST usługi wyszukiwanie Azure w wersji 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="5b8c3-103">Upgrading toohello Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="5b8c3-104">Jeśli używasz wersji 2015-02-28 lub 2015-02-28-Podgląd hello [interfejsu API REST usługi Azure Search](https://msdn.microsoft.com/library/azure/dn798935.aspx), ten artykuł pomoże Ci uaktualnienie aplikacji toouse hello dalej ogólnie dostępna wersją interfejsu API, 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-104">If you're using version 2015-02-28 or 2015-02-28-Preview of hello [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application toouse hello next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="5b8c3-105">Wersja 2016-09-01 hello interfejsu API REST zawiera pewne zmiany z wcześniejszych wersji.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-105">Version 2016-09-01 of hello REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="5b8c3-106">Są to przede wszystkim zgodne z poprzednimi wersjami, tak więc zmiana kodu powinny wymagać tylko minimalnym wysiłku, w zależności od instalowanej wersji używanego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="5b8c3-107">Zobacz [tooupgrade kroki](#UpgradeSteps) instrukcje na temat toochange kodu toouse hello nowe wersją interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-107">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="5b8c3-108">Wystąpienia usługi Azure Search obsługuje kilka wersji interfejsu API REST, w tym hello najnowszy numer.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-108">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="5b8c3-109">Można kontynuować toouse wersji, gdy nie jest już hello najnowszego, ale zaleca się przeprowadzenie migracji kodu toouse hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-109">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="5b8c3-110">Nowości w wersji 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="5b8c3-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="5b8c3-111">Wersja 2016-09-01 jest hello drugi ogólnie dostępna wersja hello interfejsu API REST usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-111">Version 2016-09-01 is hello second generally available release of hello Azure Search Service REST API.</span></span> <span data-ttu-id="5b8c3-112">Nowe funkcje w tej wersji interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="5b8c3-112">New features in this API version include:</span></span>

* <span data-ttu-id="5b8c3-113">[Niestandardowe analizatorów](https://aka.ms/customanalyzers), co pozwala użytkownikowi tootake kontrolę nad hello proces konwersji tekstu na tokeny można indeksować i wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you tootake control over hello process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="5b8c3-114">[Magazyn obiektów Blob Azure](search-howto-indexing-azure-blob-storage.md) i [Azure Table Storage](search-howto-indexing-azure-tables.md) indeksatorów, które pozwalają tooeasily importowanie danych z magazynu Azure do usługi Azure Search na harmonogram lub na żądanie.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you tooeasily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="5b8c3-115">[Pole — mapowanie](search-indexer-field-mappings.md), co pozwala użytkownikowi toocustomize jak indeksatory importowania danych do usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-115">[Field mappings](search-indexer-field-mappings.md), which allow you toocustomize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="5b8c3-116">Elementy etag, pozwalają tooupdate hello definicje indeksów, indeksatorów i źródeł danych w sposób bezpieczny współbieżności.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-116">ETags, which allow you tooupdate hello definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="5b8c3-117">Kroki tooupgrade</span><span class="sxs-lookup"><span data-stu-id="5b8c3-117">Steps tooupgrade</span></span>
<span data-ttu-id="5b8c3-118">Jeśli uaktualniasz z wersji 2015-02-28, prawdopodobnie nie będziesz mieć toomake żadnego kodu tooyour zmiany, innego niż numer wersji hello toochange.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-118">If you are upgrading from version 2015-02-28, you probably won't have toomake any changes tooyour code, other than toochange hello version number.</span></span> <span data-ttu-id="5b8c3-119">Hello tylko sytuacji, w których może być konieczne toochange kodu są:</span><span class="sxs-lookup"><span data-stu-id="5b8c3-119">hello only situations in which you may need toochange code are when:</span></span>

* <span data-ttu-id="5b8c3-120">Kod kończy się niepowodzeniem, nierozpoznany właściwości są zwracane w odpowiedzi interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="5b8c3-121">Domyślnie aplikacja ignorować właściwości, których nie zna.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="5b8c3-122">Kod będzie się powtarzał żądania interfejsu API i próbuje tooresend ich toohello nowej wersji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-122">Your code persists API requests and tries tooresend them toohello new API version.</span></span> <span data-ttu-id="5b8c3-123">Na przykład może się zdarzyć, aplikacja będzie nadal występował tokeny kontynuacji zwrócony z interfejsu API Search hello (Aby uzyskać więcej informacji, poszukaj `@search.nextPageParameters` w hello [odwołanie wyszukiwania do interfejsu API](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="5b8c3-123">For example, this might happen if your application persists continuation tokens returned from hello Search API (for more information, look for `@search.nextPageParameters` in hello [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="5b8c3-124">Jeśli jeden z tych sytuacji zastosować tooyou, może wymagać toochange kodu odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-124">If either of these situations apply tooyou, then you may need toochange your code accordingly.</span></span> <span data-ttu-id="5b8c3-125">W przeciwnym razie żadne zmiany jeśli są niezbędne, chyba że chcesz toostart przy użyciu hello [nowe funkcje](#WhatsNew) wersji 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-125">Otherwise, no changes should be necessary unless you want toostart using hello [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="5b8c3-126">Uaktualniania z wersji 2015-02-28-Preview hello powyżej ma również zastosowanie, ale należy wziąć pod uwagę, że niektóre funkcje wersji zapoznawczej nie są dostępne w wersji 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="5b8c3-126">If you are upgrading from version 2015-02-28-Preview, hello above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="5b8c3-127">Magazyn obiektów Blob indeksatora pomocy technicznej platformy Azure dla plików CSV i obiektów blob zawierający tablice notacji JSON.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="5b8c3-128">Synonimy</span><span class="sxs-lookup"><span data-stu-id="5b8c3-128">Synonyms</span></span>
* <span data-ttu-id="5b8c3-129">Zapytania "Więcej postać"</span><span class="sxs-lookup"><span data-stu-id="5b8c3-129">"More like this" queries</span></span>

<span data-ttu-id="5b8c3-130">Jeśli kod korzysta z tych funkcji, nie będzie możliwe tooupgrade too2016-09-01 bez usuwania użycie ich.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-130">If your code uses these features, you will not be able tooupgrade too2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b8c3-131">Należy pamiętać, Podgląd interfejsy API są przeznaczone do testowania i ocenie, a nie powinna być używana w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="5b8c3-132">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5b8c3-132">Conclusion</span></span>
<span data-ttu-id="5b8c3-133">Aby uzyskać więcej informacji na temat używania hello interfejsu API REST usługi Azure Search, zobacz hello niedawno aktualizowana [dokumentacja interfejsu API](https://msdn.microsoft.com/library/azure/dn798935.aspx) w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-133">If you need more details on using hello Azure Search Service REST API, see hello recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="5b8c3-134">Chętnie poznamy Twoją opinię w usłudze Azure Search.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="5b8c3-135">Jeśli wystąpią problemy, możesz wolnego tooask nam Aby uzyskać pomoc dotyczącą hello [forum usługi Azure Search w witrynie MSDN](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) lub [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="5b8c3-135">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="5b8c3-136">Jeśli pytanie o Azure będzie wyszukiwać w witrynie StackOverflow, upewnij się, że tootag z `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="5b8c3-136">If you're asking a question about Azure Search on StackOverflow, make sure tootag it with `azure-search`.</span></span>

<span data-ttu-id="5b8c3-137">Dziękujemy za skorzystanie z usługi Azure Search!</span><span class="sxs-lookup"><span data-stu-id="5b8c3-137">Thank you for using Azure Search!</span></span>

