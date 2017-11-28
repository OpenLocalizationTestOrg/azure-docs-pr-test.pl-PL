---
title: "zasoby aaaPre obciążenia dla punktu końcowego usługi Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak obciążenia toopre buforowanej zawartości dla punktu końcowego usługi Azure CDN."
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
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="9bb95-103">Wstępne ładowanie zasobów w punkcie końcowym usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="9bb95-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="9bb95-104">Domyślnie zasoby najpierw są buforowane, ponieważ są one wymagane.</span><span class="sxs-lookup"><span data-stu-id="9bb95-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="9bb95-105">Oznacza to, że hello pierwsze żądanie z każdego regionu może trwać dłużej, ponieważ serwery krawędzi hello nie będą mieć hello zawartość w pamięci podręcznej i będzie konieczne serwera pochodzenia toohello tooforward hello żądania.</span><span class="sxs-lookup"><span data-stu-id="9bb95-105">This means that hello first request from each region may take longer, since hello edge servers will not have hello content cached and will need tooforward hello request toohello origin server.</span></span> <span data-ttu-id="9bb95-106">Wstępnego ładowania zawartości pozwala uniknąć ten pierwszy opóźnienia trafień.</span><span class="sxs-lookup"><span data-stu-id="9bb95-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="9bb95-107">Ponadto tooproviding lepsze środowisko klienta wstępne ładowanie pamięci podręcznej zasobów pomaga również zmniejszyć ruch sieciowy na powitania serwera źródłowego.</span><span class="sxs-lookup"><span data-stu-id="9bb95-107">In addition tooproviding a better customer experience, pre-loading your cached assets can also reduce network traffic on hello origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="9bb95-108">Wstępne ładowanie zasobów jest przydatne w przypadku dużych zdarzenia lub zawartości, która staje się jednocześnie dostępne tooa dużą liczbę użytkowników, takich jak nowe wydanie filmu lub aktualizacji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="9bb95-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available tooa large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="9bb95-109">W tym samouczku przedstawiono wstępnego ładowania zawartości w pamięci podręcznej na wszystkich węzłach krawędzi Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="9bb95-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="9bb95-110">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="9bb95-110">Walkthrough</span></span>
1. <span data-ttu-id="9bb95-111">W hello [Azure Portal](https://portal.azure.com), Przeglądaj profil CDN toohello zawierający punkt końcowy hello mają toopre obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9bb95-111">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopre-load.</span></span>  <span data-ttu-id="9bb95-112">zostanie otwarty blok profilu Hello.</span><span class="sxs-lookup"><span data-stu-id="9bb95-112">hello profile blade opens.</span></span>
2. <span data-ttu-id="9bb95-113">Kliknij punkt końcowy hello hello na liście.</span><span class="sxs-lookup"><span data-stu-id="9bb95-113">Click hello endpoint in hello list.</span></span>  <span data-ttu-id="9bb95-114">zostanie otwarty blok końcowy Hello.</span><span class="sxs-lookup"><span data-stu-id="9bb95-114">hello endpoint blade opens.</span></span>
3. <span data-ttu-id="9bb95-115">W bloku punktu końcowego CDN hello przycisk hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9bb95-115">From hello CDN endpoint blade, click hello load button.</span></span>
   
    ![Blok punktu końcowego CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="9bb95-117">zostanie otwarty blok obciążenia Hello.</span><span class="sxs-lookup"><span data-stu-id="9bb95-117">hello Load blade opens.</span></span>
   
    ![Blok obciążenia CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="9bb95-119">Wprowadź pełną ścieżkę hello każdego trwałego mają tooload (np. `/pictures/kitten.png`) w hello **ścieżki** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9bb95-119">Enter hello full path of each asset you wish tooload (e.g., `/pictures/kitten.png`) in hello **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="9bb95-120">Więcej **ścieżki** pola tekstowe pojawią się po wprowadzeniu tooallow tekst toobuild lista wiele zasobów.</span><span class="sxs-lookup"><span data-stu-id="9bb95-120">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="9bb95-121">Zasoby można usunąć z listy hello, klikając przycisk wielokropka (...) hello.</span><span class="sxs-lookup"><span data-stu-id="9bb95-121">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="9bb95-122">Ścieżki musi być względnym adresem URL, która pasuje do następujących hello [wyrażenia regularnego](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="9bb95-122">Paths must be a relative URL that fits hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="9bb95-123">Załadować ścieżki pojedynczy plik `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="9bb95-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="9bb95-124">Załaduj pojedynczy plik z ciągu zapytania`@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="9bb95-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="9bb95-125">Każdego zasobu musi mieć własny ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="9bb95-125">Each asset must have its own path.</span></span>  <span data-ttu-id="9bb95-126">Nie ma żadnych funkcji symboli wieloznacznych dla wstępnego ładowania zasobów.</span><span class="sxs-lookup"><span data-stu-id="9bb95-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Przycisk obciążenia](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="9bb95-128">Kliknij przycisk hello **obciążenia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9bb95-128">Click hello **Load** button.</span></span>
   
    ![Przycisk obciążenia](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="9bb95-130">Istnieje ograniczenie 10 obciążenia żądań na minutę na profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="9bb95-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="9bb95-131">50 ścieżek są dozwolone na żądanie.</span><span class="sxs-lookup"><span data-stu-id="9bb95-131">50 paths are allowed per request.</span></span> <span data-ttu-id="9bb95-132">Każda ścieżka ma limit długość ścieżki 1024 znaków.</span><span class="sxs-lookup"><span data-stu-id="9bb95-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="9bb95-133">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9bb95-133">See also</span></span>
* [<span data-ttu-id="9bb95-134">Przeczyszczanie punktu końcowego usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="9bb95-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="9bb95-135">Azure dokumentacji interfejsu API REST usługi CDN - przeczyścić lub wstępnie załadować punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="9bb95-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

