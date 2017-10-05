---
title: "Kontrolowanie Azure CDN buforowanie z ciągami zapytań | Dokumentacja firmy Microsoft"
description: "Ciąg zapytania usługi Azure CDN buforowanie kontroli, jak pliki mają być buforowane, które zawierają ciągi zapytań."
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
ms.openlocfilehash: 8d79626fa8516f226a82d3dac693c2033904c91d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="98f8c-103">Formant Azure CDN buforowanie z ciągami zapytań</span><span class="sxs-lookup"><span data-stu-id="98f8c-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="98f8c-104">Standardowa</span><span class="sxs-lookup"><span data-stu-id="98f8c-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="98f8c-105">Azure CDN Premium from Verizon</span><span class="sxs-lookup"><span data-stu-id="98f8c-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="98f8c-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="98f8c-106">Overview</span></span>
<span data-ttu-id="98f8c-107">Ciąg zapytania buforowanie kontroli, jak pliki mają być buforowane, które zawierają ciągi zapytań.</span><span class="sxs-lookup"><span data-stu-id="98f8c-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98f8c-108">Produkty Standard i Premium CDN zawierają ten sam ciąg zapytania buforowanie funkcji, ale różni się w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="98f8c-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="98f8c-109">W tym dokumencie opisano interfejs dla **Azure CDN Standard from Akamai** i **Azure CDN Standard from Verizon**.</span><span class="sxs-lookup"><span data-stu-id="98f8c-109">This document describes the interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="98f8c-110">Dla zapytania z buforowania ciągu **Azure CDN Premium from Verizon**, zobacz [kontrolowanie zachowania buforowania CDN żądań z ciągami zapytań - Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="98f8c-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="98f8c-111">Dostępne są trzy tryby:</span><span class="sxs-lookup"><span data-stu-id="98f8c-111">Three modes are available:</span></span>

* <span data-ttu-id="98f8c-112">**Ignorować ciągi kwerendy**: jest to tryb domyślny.</span><span class="sxs-lookup"><span data-stu-id="98f8c-112">**Ignore query strings**:  This is the default mode.</span></span>  <span data-ttu-id="98f8c-113">Węzeł brzegowy CDN zostaną spełnione ciąg zapytania z żądającego do źródła na pierwsze żądanie i pamięci podręcznej elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="98f8c-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="98f8c-114">Wszystkie kolejne żądania dla tego zasobu, które są obsługiwane z węzłem krawędzi zignoruje ciąg zapytania do momentu wygaśnięcia elementu pamięci podręcznej zawartości.</span><span class="sxs-lookup"><span data-stu-id="98f8c-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="98f8c-115">**Pomiń buforowanie adresu URL z ciągami zapytań**: W tym trybie żądań z ciągami zapytań nie są buforowane w sieci CDN węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="98f8c-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="98f8c-116">Węzeł brzegowy pobiera zasobu bezpośrednio ze źródła i przekazuje je do obiektu żądającego z każdym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="98f8c-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="98f8c-117">**Buforuj każdy unikatowy adres URL**: w tym trybie traktuje każde żądanie zawierające ciąg zapytania jako unikatowy zasób ze swojej własnej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="98f8c-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="98f8c-118">Na przykład odpowiedzi ze źródła dla żądania *foo.ashx?q=bar* będą buforowane w węźle krawędzi i zwrócony dla kolejnych pamięci podręcznych z tym samym ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="98f8c-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="98f8c-119">Żądanie *foo.ashx?q=somethingelse* będzie buforowana jako osobne zasobów własny czas wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="98f8c-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="98f8c-120">Zmiana ustawienia profilów sieci CDN w warstwie standardowa buforowanie ciągów zapytań</span><span class="sxs-lookup"><span data-stu-id="98f8c-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="98f8c-121">Blok profilu CDN kliknij punkt końcowy CDN, którą chcesz zarządzać.</span><span class="sxs-lookup"><span data-stu-id="98f8c-121">From the CDN profile blade, click the CDN endpoint you wish to manage.</span></span>
   
    ![Punkty końcowe blok profilu CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="98f8c-123">Zostanie otwarty blok punktu końcowego CDN.</span><span class="sxs-lookup"><span data-stu-id="98f8c-123">The CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="98f8c-124">Kliknij przycisk **Konfiguruj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="98f8c-124">Click the **Configure** button.</span></span>
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="98f8c-126">Zostanie otwarty blok konfiguracji sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="98f8c-126">The CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="98f8c-127">Wybierz ustawienie z **zachowanie buforowania ciągu kwerendy** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="98f8c-127">Select a setting from the **Query string caching behavior** dropdown.</span></span>
   
    ![Opcje buforowania ciągu kwerendy CDN](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="98f8c-129">Po dokonaniu wyboru kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="98f8c-129">After making your selection, click the **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98f8c-130">Zmiany ustawienia mogą nie być od razu widoczne, czas rejestracji propagację za pośrednictwem sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="98f8c-130">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="98f8c-131">W przypadku profilów usługi <b>Azure CDN from Akamai</b> propagacja zwykle zostanie ukończona w ciągu minuty.</span><span class="sxs-lookup"><span data-stu-id="98f8c-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="98f8c-132">W przypadku profilów usługi <b>Azure CDN from Verizon</b> propagacja zwykle zostanie ukończona w ciągu 90 minut, ale niekiedy może to zająć więcej czasu.</span><span class="sxs-lookup"><span data-stu-id="98f8c-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

