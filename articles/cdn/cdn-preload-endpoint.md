---
title: "Wstępne ładowanie zasobów dla punktu końcowego usługi Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wstępne ładowanie pamięci podręcznej zawartości dla punktu końcowego usługi Azure CDN."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 1f2dcd9a91bb6e883cbef06373c1acd98bf8d45f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="2a3be-103">Wstępne ładowanie zasobów w punkcie końcowym usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="2a3be-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="2a3be-104">Domyślnie zasoby najpierw są buforowane, ponieważ są one wymagane.</span><span class="sxs-lookup"><span data-stu-id="2a3be-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="2a3be-105">Oznacza to, że pierwsze żądanie z każdego regionu może trwać dłużej, ponieważ serwery krawędzi nie będą mieć zawartość w pamięci podręcznej i będzie musiał przesyła żądanie do serwera pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="2a3be-105">This means that the first request from each region may take longer, since the edge servers will not have the content cached and will need to forward the request to the origin server.</span></span> <span data-ttu-id="2a3be-106">Wstępnego ładowania zawartości pozwala uniknąć ten pierwszy opóźnienia trafień.</span><span class="sxs-lookup"><span data-stu-id="2a3be-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="2a3be-107">Oprócz zapewnienia lepszej obsługi klienta, wstępne ładowanie pamięci podręcznej zasobów można również zmniejszenie ruchu w sieci na serwerze źródłowym.</span><span class="sxs-lookup"><span data-stu-id="2a3be-107">In addition to providing a better customer experience, pre-loading your cached assets can also reduce network traffic on the origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="2a3be-108">Wstępne ładowanie zasobów jest przydatna przy dużych zdarzenia lub zawartości, która staje się dostępna jednocześnie do wielu użytkowników, takich jak nowe wydanie filmu lub aktualizacji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="2a3be-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available to a large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="2a3be-109">W tym samouczku przedstawiono wstępnego ładowania zawartości w pamięci podręcznej na wszystkich węzłach krawędzi Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="2a3be-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="2a3be-110">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="2a3be-110">Walkthrough</span></span>
1. <span data-ttu-id="2a3be-111">W [Azure Portal](https://portal.azure.com), przejdź do profilu CDN zawierający punkt końcowy do wstępnego załadowania.</span><span class="sxs-lookup"><span data-stu-id="2a3be-111">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span></span>  <span data-ttu-id="2a3be-112">Zostanie otwarty blok profilu.</span><span class="sxs-lookup"><span data-stu-id="2a3be-112">The profile blade opens.</span></span>
2. <span data-ttu-id="2a3be-113">Kliknij punkt końcowy na liście.</span><span class="sxs-lookup"><span data-stu-id="2a3be-113">Click the endpoint in the list.</span></span>  <span data-ttu-id="2a3be-114">Zostanie otwarty blok końcowy.</span><span class="sxs-lookup"><span data-stu-id="2a3be-114">The endpoint blade opens.</span></span>
3. <span data-ttu-id="2a3be-115">W bloku punktu końcowego usługi CDN kliknij przycisk obciążenia.</span><span class="sxs-lookup"><span data-stu-id="2a3be-115">From the CDN endpoint blade, click the load button.</span></span>
   
    ![Blok punktu końcowego CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="2a3be-117">Zostanie otwarty blok obciążenia.</span><span class="sxs-lookup"><span data-stu-id="2a3be-117">The Load blade opens.</span></span>
   
    ![Blok obciążenia CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="2a3be-119">Wprowadź pełną ścieżkę każdego zasobu do załadowania (np. `/pictures/kitten.png`) w **ścieżki** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="2a3be-119">Enter the full path of each asset you wish to load (e.g., `/pictures/kitten.png`) in the **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="2a3be-120">Więcej **ścieżki** pola tekstowe pojawią się po wprowadź tekst, który pozwala na utworzenie listy wiele zasobów.</span><span class="sxs-lookup"><span data-stu-id="2a3be-120">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="2a3be-121">Zasoby można usunąć z listy, klikając przycisk wielokropka (...).</span><span class="sxs-lookup"><span data-stu-id="2a3be-121">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="2a3be-122">Ścieżki musi być względnym adresem URL, który pasuje do następujących [wyrażenia regularnego](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="2a3be-122">Paths must be a relative URL that fits the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="2a3be-123">Załadować ścieżki pojedynczy plik `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="2a3be-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="2a3be-124">Załaduj pojedynczy plik z ciągu zapytania`@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="2a3be-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="2a3be-125">Każdego zasobu musi mieć własny ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="2a3be-125">Each asset must have its own path.</span></span>  <span data-ttu-id="2a3be-126">Nie ma żadnych funkcji symboli wieloznacznych dla wstępnego ładowania zasobów.</span><span class="sxs-lookup"><span data-stu-id="2a3be-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Przycisk obciążenia](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="2a3be-128">Kliknij przycisk **obciążenia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2a3be-128">Click the **Load** button.</span></span>
   
    ![Przycisk obciążenia](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="2a3be-130">Istnieje ograniczenie 10 obciążenia żądań na minutę na profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="2a3be-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="2a3be-131">50 ścieżek są dozwolone na żądanie.</span><span class="sxs-lookup"><span data-stu-id="2a3be-131">50 paths are allowed per request.</span></span> <span data-ttu-id="2a3be-132">Każda ścieżka ma limit długość ścieżki 1024 znaków.</span><span class="sxs-lookup"><span data-stu-id="2a3be-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="2a3be-133">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2a3be-133">See also</span></span>
* [<span data-ttu-id="2a3be-134">Przeczyszczanie punktu końcowego usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="2a3be-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="2a3be-135">Azure dokumentacji interfejsu API REST usługi CDN - przeczyścić lub wstępnie załadować punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="2a3be-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

