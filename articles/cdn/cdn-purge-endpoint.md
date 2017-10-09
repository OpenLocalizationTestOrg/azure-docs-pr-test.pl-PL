---
title: "punkt końcowy usługi Azure CDN aaaPurge | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toopurge wszystkie buforowane zawartości z punktu końcowego usługi Azure CDN."
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
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="3b85c-103">Przeczyszczanie punktu końcowego usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="3b85c-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="3b85c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3b85c-104">Overview</span></span>
<span data-ttu-id="3b85c-105">Azure CDN krawędzi węzły będą buforowane zasoby, do momentu wygaśnięcia hello zasobu czas wygaśnięcia (TTL).</span><span class="sxs-lookup"><span data-stu-id="3b85c-105">Azure CDN edge nodes will cache assets until hello asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="3b85c-106">Po wygaśnięciu TTL hello zasobów, gdy klient żąda zawartości hello z węzłem krawędzi hello, węzłem krawędzi hello pobiera zaktualizowane nową kopię żądania hello zasobów tooserve powitania klienta i przechowywać odświeżania hello w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3b85c-106">After hello asset's TTL expires, when a client requests hello asset from hello edge node, hello edge node will retrieve a new updated copy of hello asset tooserve hello client request and store refresh hello cache.</span></span>

<span data-ttu-id="3b85c-107">Witaj najlepsze praktyki toomake się, że użytkownicy zawsze uzyskać najnowszą kopię zasobów hello jest tooversion zasobów dla każdej aktualizacji i opublikujesz je jako nowego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="3b85c-107">hello best practice toomake sure your users always obtain hello latest copy of your assets is tooversion your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="3b85c-108">CDN natychmiast pobierze hello nowych zasobów hello dalej żądań klientów.</span><span class="sxs-lookup"><span data-stu-id="3b85c-108">CDN will immediately retrieve hello new assets for hello next client requests.</span></span>  <span data-ttu-id="3b85c-109">Czasami warto zapoznać się z toopurge buforowanej zawartości z dowolnych węzłów edge i wymusić wszystkie tooretrieve nowe zasoby zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="3b85c-109">Sometimes you may wish toopurge cached content from all edge nodes and force them all tooretrieve new updated assets.</span></span>  <span data-ttu-id="3b85c-110">Może to być aplikacji sieci web tooyour tooupdates lub tooquickly aktualizacji zasobów, które zawierają nieprawidłowe informacje.</span><span class="sxs-lookup"><span data-stu-id="3b85c-110">This might be due tooupdates tooyour web application, or tooquickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="3b85c-111">Należy pamiętać, że tylko przeczyszczanie czyści hello w pamięci podręcznej zawartości na serwerach krawędzi CDN hello.</span><span class="sxs-lookup"><span data-stu-id="3b85c-111">Note that purging only clears hello cached content on hello CDN edge servers.</span></span>  <span data-ttu-id="3b85c-112">Wszystkie podrzędne pamięci podręcznych, takich jak serwery proxy i pamięci podręcznej przeglądarki lokalnego, może nadal posiadają pamięci podręcznej kopię pliku hello.</span><span class="sxs-lookup"><span data-stu-id="3b85c-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of hello file.</span></span>  <span data-ttu-id="3b85c-113">Jest ważne tooremember to podczas ustawiania pliku time-to-live.</span><span class="sxs-lookup"><span data-stu-id="3b85c-113">It's important tooremember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="3b85c-114">Możesz wymusić podrzędne klienta toorequest hello najnowszej wersji pliku przez nadanie mu unikatową nazwę za każdym razem, należy zaktualizować lub korzystając z [buforowanie ciągu zapytania](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="3b85c-114">You can force a downstream client toorequest hello latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="3b85c-115">W tym samouczku przedstawiono przeczyszczanie zasoby ze wszystkich węzłów krawędzi punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="3b85c-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="3b85c-116">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="3b85c-116">Walkthrough</span></span>
1. <span data-ttu-id="3b85c-117">W hello [Azure Portal](https://portal.azure.com), Przeglądaj profil CDN toohello zawierający punkt końcowy hello mają toopurge.</span><span class="sxs-lookup"><span data-stu-id="3b85c-117">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopurge.</span></span>
2. <span data-ttu-id="3b85c-118">Z blok profilu CDN hello kliknij przycisk Wyczyść hello.</span><span class="sxs-lookup"><span data-stu-id="3b85c-118">From hello CDN profile blade, click hello purge button.</span></span>
   
    ![Blok profilu CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="3b85c-120">zostanie otwarty blok przeczyszczania Hello.</span><span class="sxs-lookup"><span data-stu-id="3b85c-120">hello Purge blade opens.</span></span>
   
    ![Blok przeczyszczania CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="3b85c-122">Na powitania przeczyścić bloku, zaznacz adres usługi hello mają toopurge z hello adres URL z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="3b85c-122">On hello Purge blade, select hello service address you wish toopurge from hello URL dropdown.</span></span>
   
    ![Przeczyść formularza](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="3b85c-124">Toohello przeczyszczania bloku można także uzyskać, klikając hello **przeczyścić** przycisk na blok punktu końcowego CDN hello.</span><span class="sxs-lookup"><span data-stu-id="3b85c-124">You can also get toohello Purge blade by clicking hello **Purge** button on hello CDN endpoint blade.</span></span>  <span data-ttu-id="3b85c-125">W takim przypadku hello **adres URL** pole będzie wstępnie wypełniane adres usługi hello tego określonego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="3b85c-125">In that case, hello **URL** field will be pre-populated with hello service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="3b85c-126">Wybierz, jakie zasoby mają toopurge z hello węzłów krawędzi.</span><span class="sxs-lookup"><span data-stu-id="3b85c-126">Select what assets you wish toopurge from hello edge nodes.</span></span>  <span data-ttu-id="3b85c-127">Tooclear wszystkie zasoby, kliknij przycisk hello **Przeczyść wszystko** wyboru.</span><span class="sxs-lookup"><span data-stu-id="3b85c-127">If you wish tooclear all assets, click hello **Purge all** checkbox.</span></span>  <span data-ttu-id="3b85c-128">W przeciwnym razie wpisz ścieżkę hello każdego trwałego mają toopurge w hello **ścieżki** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="3b85c-128">Otherwise, type hello path of each asset you wish toopurge in hello **Path** textbox.</span></span> <span data-ttu-id="3b85c-129">Poniżej formaty są obsługiwane w ścieżce hello.</span><span class="sxs-lookup"><span data-stu-id="3b85c-129">Below formats are supported in hello path.</span></span>
    1. <span data-ttu-id="3b85c-130">**Pojedynczy adres URL przeczyszczania**: czyszczenie poszczególnych zasobów, określając hello pełny adres URL, z lub bez hello rozszerzenie, np.`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="3b85c-130">**Single URL purge**: Purge individual asset by specifying hello full URL, with or without hello file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="3b85c-131">**Symbol wieloznaczny przeczyszczania**: gwiazdki (\*) może być używany jako symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="3b85c-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="3b85c-132">Wyczyść wszystkie foldery, podfoldery i pliki w obszarze punkt końcowy z `/*` w hello ścieżki lub przeczyścić wszystkie podfoldery i pliki w określonym folderze, określając folder hello następuje `/*`, np.`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="3b85c-132">Purge all folders, sub-folders and files under an endpoint with `/*` in hello path or purge all sub-folders and files under a specific folder by specifying hello folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="3b85c-133">Należy pamiętać, czyszczenie tego symbolu wieloznacznego nie jest obsługiwany przez usługi Azure CDN from Akamai obecnie.</span><span class="sxs-lookup"><span data-stu-id="3b85c-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="3b85c-134">**Przeczyszczanie domeny katalogu głównego**: główny hello przeczyszczenia punktu końcowego Witaj, "/" w ścieżce hello.</span><span class="sxs-lookup"><span data-stu-id="3b85c-134">**Root domain purge**: Purge hello root of hello endpoint with "/" in hello path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="3b85c-135">Ścieżki musi być określona dla przeczyszczania i musi być względnym adresem URL, który mieści się następujące hello [wyrażenie regularne](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b85c-135">Paths must be specified for purge and must be a relative URL that fit hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="3b85c-136">**Przeczyść wszystko** i **przeczyszczania symbolu wieloznacznego** nie są obsługiwane przez **Azure CDN from Akamai** obecnie.</span><span class="sxs-lookup"><span data-stu-id="3b85c-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="3b85c-137">Pojedynczy adres URL przeczyszczenia`@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="3b85c-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="3b85c-138">Ciąg zapytania`@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="3b85c-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="3b85c-139">Symbol wieloznaczny przeczyszczania `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="3b85c-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="3b85c-140">Więcej **ścieżki** pola tekstowe pojawią się po wprowadzeniu tooallow tekst toobuild lista wiele zasobów.</span><span class="sxs-lookup"><span data-stu-id="3b85c-140">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="3b85c-141">Zasoby można usunąć z listy hello, klikając przycisk wielokropka (...) hello.</span><span class="sxs-lookup"><span data-stu-id="3b85c-141">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="3b85c-142">Kliknij przycisk hello **przeczyścić** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3b85c-142">Click hello **Purge** button.</span></span>
   
    ![Przeczyść przycisku](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="3b85c-144">Przeczyść żądań zająć około 2 – 3 minuty tooprocess z **Azure CDN from Verizon** (Standard i Premium), a około 7 minut z **Azure CDN from Akamai**.</span><span class="sxs-lookup"><span data-stu-id="3b85c-144">Purge requests take approximately 2-3 minutes tooprocess with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="3b85c-145">Usługi Azure CDN ma limit współbieżnych 50 przeczyścić żądań w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="3b85c-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="3b85c-146">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3b85c-146">See also</span></span>
* [<span data-ttu-id="3b85c-147">Wstępne ładowanie zasobów w punkcie końcowym usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="3b85c-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="3b85c-148">Azure dokumentacji interfejsu API REST usługi CDN - przeczyścić lub wstępnie załadować punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="3b85c-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

