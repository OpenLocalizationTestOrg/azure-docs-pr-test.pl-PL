---
title: "Przeczyszczanie punktu końcowego usługi Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przeczyścić całej zawartości pamięci podręcznej z punktu końcowego usługi Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: b035c232bb58d653960190d4974cc3789d55a51d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="72a64-103">Przeczyszczanie punktu końcowego usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="72a64-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="72a64-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="72a64-104">Overview</span></span>
<span data-ttu-id="72a64-105">Azure CDN krawędzi węzły będą buforowane zasoby, do momentu wygaśnięcia zasobu czas wygaśnięcia (TTL).</span><span class="sxs-lookup"><span data-stu-id="72a64-105">Azure CDN edge nodes will cache assets until the asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="72a64-106">Po wygaśnięciu TTL elementu zawartości, gdy klient zażąda zawartości z węzłem krawędzi, węzłem krawędzi pobiera zaktualizowane nową kopię elementu zawartości do obsługi żądań klienta i Magazyn odświeżania pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="72a64-106">After the asset's TTL expires, when a client requests the asset from the edge node, the edge node will retrieve a new updated copy of the asset to serve the client request and store refresh the cache.</span></span>

<span data-ttu-id="72a64-107">Najlepszym rozwiązaniem jest upewnij się, że użytkownicy zawsze uzyskać najnowszą kopię zasobów jest wersja zasobów dla każdej aktualizacji i opublikujesz je jako nowe adresy URL.</span><span class="sxs-lookup"><span data-stu-id="72a64-107">The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="72a64-108">CDN zostanie natychmiast pobrać nowych zasobów dla następnego żądania klienta.</span><span class="sxs-lookup"><span data-stu-id="72a64-108">CDN will immediately retrieve the new assets for the next client requests.</span></span>  <span data-ttu-id="72a64-109">Czasami możesz przeczyścić zawartości w pamięci podręcznej ze wszystkich węzłów edge i wymuszanie je wszystkie do pobierania nowych, zaktualizowanych trwałych.</span><span class="sxs-lookup"><span data-stu-id="72a64-109">Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets.</span></span>  <span data-ttu-id="72a64-110">Może to być spowodowane aktualizacje do aplikacji sieci web lub aby szybko zasoby aktualizacji, które zawierają nieprawidłowe informacje.</span><span class="sxs-lookup"><span data-stu-id="72a64-110">This might be due to updates to your web application, or to quickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="72a64-111">Należy pamiętać, że przeczyszczanie tylko czyści zawartości w pamięci podręcznej na serwerze krawędzi CDN.</span><span class="sxs-lookup"><span data-stu-id="72a64-111">Note that purging only clears the cached content on the CDN edge servers.</span></span>  <span data-ttu-id="72a64-112">Wszystkie podrzędne pamięci podręcznych, takich jak serwery proxy i pamięci podręcznej przeglądarki lokalnego, może nadal posiadają pamięci podręcznej kopię pliku.</span><span class="sxs-lookup"><span data-stu-id="72a64-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of the file.</span></span>  <span data-ttu-id="72a64-113">Należy pamiętać o tym, gdy ustawiona pliku time-to-live.</span><span class="sxs-lookup"><span data-stu-id="72a64-113">It's important to remember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="72a64-114">Możesz wymusić podrzędne klientowi żądanie najnowszej wersji pliku, nadając jej unikatową nazwę za każdym razem, należy zaktualizować lub korzystając z [buforowanie ciągu zapytania](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="72a64-114">You can force a downstream client to request the latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="72a64-115">W tym samouczku przedstawiono przeczyszczanie zasoby ze wszystkich węzłów krawędzi punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="72a64-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="72a64-116">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="72a64-116">Walkthrough</span></span>
1. <span data-ttu-id="72a64-117">W [Azure Portal](https://portal.azure.com), przejdź do profilu CDN zawierający punktu końcowego, które chcesz wyczyścić.</span><span class="sxs-lookup"><span data-stu-id="72a64-117">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to purge.</span></span>
2. <span data-ttu-id="72a64-118">Z blok profilu CDN kliknij przycisk Wyczyść.</span><span class="sxs-lookup"><span data-stu-id="72a64-118">From the CDN profile blade, click the purge button.</span></span>
   
    ![Blok profilu CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="72a64-120">Zostanie otwarty blok przeczyszczenia.</span><span class="sxs-lookup"><span data-stu-id="72a64-120">The Purge blade opens.</span></span>
   
    ![Blok przeczyszczania CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="72a64-122">W bloku przeczyszczania wybierz adres usługi, które chcesz przeczyścić z listy rozwijanej adresu URL.</span><span class="sxs-lookup"><span data-stu-id="72a64-122">On the Purge blade, select the service address you wish to purge from the URL dropdown.</span></span>
   
    ![Przeczyść formularza](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="72a64-124">Można także uzyskać bloku przeczyszczania klikając **przeczyścić** przycisk w bloku punktu końcowego CDN.</span><span class="sxs-lookup"><span data-stu-id="72a64-124">You can also get to the Purge blade by clicking the **Purge** button on the CDN endpoint blade.</span></span>  <span data-ttu-id="72a64-125">W takim przypadku **adres URL** pole będzie wstępnie wypełniane przy użyciu adresu tego określonego punktu końcowego usługi.</span><span class="sxs-lookup"><span data-stu-id="72a64-125">In that case, the **URL** field will be pre-populated with the service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="72a64-126">Wybierz zasoby, jakie mają zostać przeczyszczone węzłów krawędzi.</span><span class="sxs-lookup"><span data-stu-id="72a64-126">Select what assets you wish to purge from the edge nodes.</span></span>  <span data-ttu-id="72a64-127">Jeśli chcesz wyczyścić wszystkie zasoby, kliknij przycisk **Przeczyść wszystko** wyboru.</span><span class="sxs-lookup"><span data-stu-id="72a64-127">If you wish to clear all assets, click the **Purge all** checkbox.</span></span>  <span data-ttu-id="72a64-128">W przeciwnym razie wpisz ścieżkę do każdego trwałego chcesz przeczyścić w **ścieżki** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="72a64-128">Otherwise, type the path of each asset you wish to purge in the **Path** textbox.</span></span> <span data-ttu-id="72a64-129">Poniżej formaty są obsługiwane w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="72a64-129">Below formats are supported in the path.</span></span>
    1. <span data-ttu-id="72a64-130">**Pojedynczy adres URL przeczyszczania**: czyszczenie poszczególnych zasobów, określając pełny adres URL z lub bez rozszerzenie pliku, np.`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="72a64-130">**Single URL purge**: Purge individual asset by specifying the full URL, with or without the file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="72a64-131">**Symbol wieloznaczny przeczyszczania**: gwiazdki (\*) może być używany jako symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="72a64-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="72a64-132">Wyczyść wszystkie foldery, podfoldery i pliki w obszarze punkt końcowy z `/*` przeczyszczania lub ścieżkę wszystkie podfoldery i pliki w określonym folderze, określając folder następuje `/*`, np.`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="72a64-132">Purge all folders, sub-folders and files under an endpoint with `/*` in the path or purge all sub-folders and files under a specific folder by specifying the folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="72a64-133">Należy pamiętać, czyszczenie tego symbolu wieloznacznego nie jest obsługiwany przez usługi Azure CDN from Akamai obecnie.</span><span class="sxs-lookup"><span data-stu-id="72a64-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="72a64-134">**Przeczyszczanie domeny katalogu głównego**: przeczyścić głównego punktu końcowego z "/" w ścieżce.</span><span class="sxs-lookup"><span data-stu-id="72a64-134">**Root domain purge**: Purge the root of the endpoint with "/" in the path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="72a64-135">Ścieżki musi być określona dla przeczyszczania i musi być względnym adresem URL, który mieści się następujące [wyrażenie regularne](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="72a64-135">Paths must be specified for purge and must be a relative URL that fit the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="72a64-136">**Przeczyść wszystko** i **przeczyszczania symbolu wieloznacznego** nie są obsługiwane przez **Azure CDN from Akamai** obecnie.</span><span class="sxs-lookup"><span data-stu-id="72a64-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="72a64-137">Pojedynczy adres URL przeczyszczenia`@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="72a64-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="72a64-138">Ciąg zapytania`@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="72a64-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="72a64-139">Symbol wieloznaczny przeczyszczania `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="72a64-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="72a64-140">Więcej **ścieżki** pola tekstowe pojawią się po wprowadź tekst, który pozwala na utworzenie listy wiele zasobów.</span><span class="sxs-lookup"><span data-stu-id="72a64-140">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="72a64-141">Zasoby można usunąć z listy, klikając przycisk wielokropka (...).</span><span class="sxs-lookup"><span data-stu-id="72a64-141">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="72a64-142">Kliknij przycisk **przeczyścić** przycisku.</span><span class="sxs-lookup"><span data-stu-id="72a64-142">Click the **Purge** button.</span></span>
   
    ![Przeczyść przycisku](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="72a64-144">Żądania przeczyszczenia zająć około 2 – 3 minuty do przetworzenia z **Azure CDN from Verizon** (Standard i Premium), a około 7 minut z **Azure CDN from Akamai**.</span><span class="sxs-lookup"><span data-stu-id="72a64-144">Purge requests take approximately 2-3 minutes to process with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="72a64-145">Usługi Azure CDN ma limit współbieżnych 50 przeczyścić żądań w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="72a64-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="72a64-146">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="72a64-146">See also</span></span>
* [<span data-ttu-id="72a64-147">Wstępne ładowanie zasobów w punkcie końcowym usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="72a64-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="72a64-148">Azure dokumentacji interfejsu API REST usługi CDN - przeczyścić lub wstępnie załadować punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="72a64-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

