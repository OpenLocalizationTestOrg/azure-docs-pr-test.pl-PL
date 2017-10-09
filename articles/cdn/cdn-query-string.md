---
title: "zachowanie buforowania Azure CDN z ciągami zapytań aaaControl | Dokumentacja firmy Microsoft"
description: "Ciąg zapytania Azure CDN buforowanie kontroli, jak pliki są toobe, które zawierają ciągi zapytań w pamięci podręcznej."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="3d28a-103">Formant Azure CDN buforowanie z ciągami zapytań</span><span class="sxs-lookup"><span data-stu-id="3d28a-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d28a-104">Standardowa</span><span class="sxs-lookup"><span data-stu-id="3d28a-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="3d28a-105">Azure CDN Premium from Verizon</span><span class="sxs-lookup"><span data-stu-id="3d28a-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="3d28a-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3d28a-106">Overview</span></span>
<span data-ttu-id="3d28a-107">Buforowanie kontroli, jak pliki są toobe, które zawierają ciągi zapytań w pamięci podręcznej ciągów zapytań.</span><span class="sxs-lookup"><span data-stu-id="3d28a-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d28a-108">Witaj Standard i Premium CDN produkty zawierają hello zapytania takie same parametry funkcji buforowania, ale hello interfejs użytkownika różni się.</span><span class="sxs-lookup"><span data-stu-id="3d28a-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="3d28a-109">W tym dokumencie opisano interfejs hello **Azure CDN Standard from Akamai** i **Azure CDN Standard from Verizon**.</span><span class="sxs-lookup"><span data-stu-id="3d28a-109">This document describes hello interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="3d28a-110">Dla zapytania z buforowania ciągu **Azure CDN Premium from Verizon**, zobacz [kontrolowanie zachowania buforowania CDN żądań z ciągami zapytań - Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="3d28a-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="3d28a-111">Dostępne są trzy tryby:</span><span class="sxs-lookup"><span data-stu-id="3d28a-111">Three modes are available:</span></span>

* <span data-ttu-id="3d28a-112">**Ignorować ciągi kwerendy**: jest to tryb domyślny hello.</span><span class="sxs-lookup"><span data-stu-id="3d28a-112">**Ignore query strings**:  This is hello default mode.</span></span>  <span data-ttu-id="3d28a-113">węzeł brzegowy CDN Hello przechodzą ciągu zapytania hello pochodzenia toohello obiektu żądającego hello na pierwsze Żądanie hello i zasobów hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3d28a-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="3d28a-114">Wszystkie kolejne żądania dla tego zasobu, które są obsługiwane z węzłem krawędzi hello zignoruje hello ciąg zapytania do momentu wygaśnięcia hello zasobów pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3d28a-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="3d28a-115">**Pomiń buforowanie adresu URL z ciągami zapytań**: W tym trybie żądań z ciągami zapytań nie są buforowane na węzeł brzegowy hello CDN.</span><span class="sxs-lookup"><span data-stu-id="3d28a-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="3d28a-116">węzeł brzegowy Hello pobiera hello zasobów bezpośrednio ze źródła hello i przekazuje ją obiektu żądającego toohello z każdym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="3d28a-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="3d28a-117">**Buforuj każdy unikatowy adres URL**: w tym trybie traktuje każde żądanie zawierające ciąg zapytania jako unikatowy zasób ze swojej własnej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3d28a-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="3d28a-118">Na przykład Witaj odpowiedzi pochodzenia hello na żądanie dla *foo.ashx?q=bar* będą buforowane na węzeł brzegowy hello i zwrócony dla kolejnych pamięci podręcznych z tym samym ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="3d28a-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="3d28a-119">Żądanie *foo.ashx?q=somethingelse* będzie buforowana jako zasób oddzielne ze swoim toolive czasie.</span><span class="sxs-lookup"><span data-stu-id="3d28a-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="3d28a-120">Zmiana ustawienia profilów sieci CDN w warstwie standardowa buforowanie ciągów zapytań</span><span class="sxs-lookup"><span data-stu-id="3d28a-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="3d28a-121">Blok profilu CDN hello kliknij punkt końcowy CDN hello mają toomanage.</span><span class="sxs-lookup"><span data-stu-id="3d28a-121">From hello CDN profile blade, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Punkty końcowe blok profilu CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="3d28a-123">zostanie otwarty blok punktu końcowego CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="3d28a-123">hello CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="3d28a-124">Kliknij przycisk hello **Konfiguruj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3d28a-124">Click hello **Configure** button.</span></span>
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="3d28a-126">zostanie otwarty blok konfiguracji CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="3d28a-126">hello CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="3d28a-127">Wybierz ustawienie z hello **zachowanie buforowania ciągu kwerendy** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="3d28a-127">Select a setting from hello **Query string caching behavior** dropdown.</span></span>
   
    ![Opcje buforowania ciągu kwerendy CDN](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="3d28a-129">Po dokonaniu wyboru kliknij przycisk hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3d28a-129">After making your selection, click hello **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d28a-130">zmiany ustawień Hello mogą nie być od razu widoczne, zajmuje trochę czasu hello toopropagate rejestracji za pomocą hello CDN.</span><span class="sxs-lookup"><span data-stu-id="3d28a-130">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="3d28a-131">W przypadku profilów usługi <b>Azure CDN from Akamai</b> propagacja zwykle zostanie ukończona w ciągu minuty.</span><span class="sxs-lookup"><span data-stu-id="3d28a-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="3d28a-132">W przypadku profilów usługi <b>Azure CDN from Verizon</b> propagacja zwykle zostanie ukończona w ciągu 90 minut, ale niekiedy może to zająć więcej czasu.</span><span class="sxs-lookup"><span data-stu-id="3d28a-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

