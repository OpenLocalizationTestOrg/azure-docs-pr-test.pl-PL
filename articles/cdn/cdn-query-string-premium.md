---
title: "Kontrolowanie Azure CDN buforowanie z ciągami zapytań - Premium | Dokumentacja firmy Microsoft"
description: "Ciąg zapytania usługi Azure CDN buforowanie kontroli, jak pliki mają być buforowane, które zawierają ciągi zapytań."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 145067c2ce50b41c4783f4de4052c0e7cb529fc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="c6f57-103">Formant Azure CDN buforowanie z ciągami zapytań - Premium</span><span class="sxs-lookup"><span data-stu-id="c6f57-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6f57-104">Standardowa</span><span class="sxs-lookup"><span data-stu-id="c6f57-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="c6f57-105">Azure CDN Premium from Verizon</span><span class="sxs-lookup"><span data-stu-id="c6f57-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c6f57-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c6f57-106">Overview</span></span>
<span data-ttu-id="c6f57-107">Ciąg zapytania buforowanie kontroli, jak pliki mają być buforowane, które zawierają ciągi zapytań.</span><span class="sxs-lookup"><span data-stu-id="c6f57-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6f57-108">Produkty Standard i Premium CDN zawierają ten sam ciąg zapytania buforowanie funkcji, ale różni się w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6f57-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="c6f57-109">W tym dokumencie opisano interfejs dla **Azure CDN Premium from Verizon**.</span><span class="sxs-lookup"><span data-stu-id="c6f57-109">This document describes the interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="c6f57-110">Dla zapytania z buforowania ciągu **Azure CDN Standard from Akamai** i **Azure CDN Standard from Verizon**, zobacz [kontrolowanie zachowania buforowania CDN żądań z ciągami zapytań](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="c6f57-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="c6f57-111">Dostępne są trzy tryby:</span><span class="sxs-lookup"><span data-stu-id="c6f57-111">Three modes are available:</span></span>

* <span data-ttu-id="c6f57-112">**pamięć podręczna standard**: jest to tryb domyślny.</span><span class="sxs-lookup"><span data-stu-id="c6f57-112">**standard-cache**:  This is the default mode.</span></span>  <span data-ttu-id="c6f57-113">Węzeł brzegowy CDN zostaną spełnione ciąg zapytania z żądającego do źródła na pierwsze żądanie i pamięci podręcznej elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="c6f57-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="c6f57-114">Wszystkie kolejne żądania dla tego zasobu, które są obsługiwane z węzłem krawędzi zignoruje ciąg zapytania do momentu wygaśnięcia elementu pamięci podręcznej zawartości.</span><span class="sxs-lookup"><span data-stu-id="c6f57-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="c6f57-115">**pamięć podręczna nie**: W tym trybie żądań z ciągami zapytań nie są buforowane w sieci CDN węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="c6f57-115">**no-cache**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="c6f57-116">Węzeł brzegowy pobiera zasobu bezpośrednio ze źródła i przekazuje je do obiektu żądającego z każdym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="c6f57-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="c6f57-117">**Unikatowy pamięci podręcznej**: w tym trybie traktuje każde żądanie zawierające ciąg zapytania jako unikatowy zasób ze swojej własnej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c6f57-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="c6f57-118">Na przykład odpowiedzi ze źródła dla żądania *foo.ashx?q=bar* będą buforowane w węźle krawędzi i zwrócony dla kolejnych pamięci podręcznych z tym samym ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="c6f57-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="c6f57-119">Żądanie *foo.ashx?q=somethingelse* będzie buforowana jako osobne zasobów własny czas wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="c6f57-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="c6f57-120">Zmiana ustawienia profilów sieci CDN w warstwie premium buforowanie ciągów zapytań</span><span class="sxs-lookup"><span data-stu-id="c6f57-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="c6f57-121">Blok profilu CDN, kliknij **Zarządzaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6f57-121">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="c6f57-123">Zostanie otwarty w portalu zarządzania usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="c6f57-123">The CDN management portal opens.</span></span>
2. <span data-ttu-id="c6f57-124">Umieść kursor nad **HTTP dużych** , a następnie umieść kursor nad **ustawienia pamięci podręcznej** wysuwane okno.</span><span class="sxs-lookup"><span data-stu-id="c6f57-124">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="c6f57-125">Polecenie **buforowania ciągu kwerendy**.</span><span class="sxs-lookup"><span data-stu-id="c6f57-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="c6f57-126">Opcje buforowania ciągu kwerendy są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="c6f57-126">Query string caching options are displayed.</span></span>
   
    ![Opcje buforowania ciągu kwerendy CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="c6f57-128">Po dokonaniu wyboru kliknij przycisk **aktualizacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6f57-128">After making your selection, click the **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6f57-129">Zmiany ustawienia mogą nie być od razu widoczne, czas rejestracji propagację za pośrednictwem sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="c6f57-129">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="c6f57-130">W przypadku profilów usługi <b>Azure CDN from Verizon</b> propagacja zwykle zostanie ukończona w ciągu 90 minut, ale niekiedy może to zająć więcej czasu.</span><span class="sxs-lookup"><span data-stu-id="c6f57-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

