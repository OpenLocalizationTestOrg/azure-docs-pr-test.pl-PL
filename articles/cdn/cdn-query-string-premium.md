---
title: "zachowanie buforowania Azure CDN z ciągami zapytań - Premium aaaControl | Dokumentacja firmy Microsoft"
description: "Ciąg zapytania Azure CDN buforowanie kontroli, jak pliki są toobe, które zawierają ciągi zapytań w pamięci podręcznej."
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
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="6c57c-103">Formant Azure CDN buforowanie z ciągami zapytań - Premium</span><span class="sxs-lookup"><span data-stu-id="6c57c-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c57c-104">Standardowa</span><span class="sxs-lookup"><span data-stu-id="6c57c-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="6c57c-105">Azure CDN Premium from Verizon</span><span class="sxs-lookup"><span data-stu-id="6c57c-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="6c57c-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6c57c-106">Overview</span></span>
<span data-ttu-id="6c57c-107">Buforowanie kontroli, jak pliki są toobe, które zawierają ciągi zapytań w pamięci podręcznej ciągów zapytań.</span><span class="sxs-lookup"><span data-stu-id="6c57c-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c57c-108">Witaj Standard i Premium CDN produkty zawierają hello zapytania takie same parametry funkcji buforowania, ale hello interfejs użytkownika różni się.</span><span class="sxs-lookup"><span data-stu-id="6c57c-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="6c57c-109">W tym dokumencie opisano interfejs hello **Azure CDN Premium from Verizon**.</span><span class="sxs-lookup"><span data-stu-id="6c57c-109">This document describes hello interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="6c57c-110">Dla zapytania z buforowania ciągu **Azure CDN Standard from Akamai** i **Azure CDN Standard from Verizon**, zobacz [kontrolowanie zachowania buforowania CDN żądań z ciągami zapytań](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="6c57c-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="6c57c-111">Dostępne są trzy tryby:</span><span class="sxs-lookup"><span data-stu-id="6c57c-111">Three modes are available:</span></span>

* <span data-ttu-id="6c57c-112">**pamięć podręczna standard**: jest to tryb domyślny hello.</span><span class="sxs-lookup"><span data-stu-id="6c57c-112">**standard-cache**:  This is hello default mode.</span></span>  <span data-ttu-id="6c57c-113">węzeł brzegowy CDN Hello przechodzą ciągu zapytania hello pochodzenia toohello obiektu żądającego hello na pierwsze Żądanie hello i zasobów hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6c57c-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="6c57c-114">Wszystkie kolejne żądania dla tego zasobu, które są obsługiwane z węzłem krawędzi hello zignoruje hello ciąg zapytania do momentu wygaśnięcia hello zasobów pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6c57c-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="6c57c-115">**pamięć podręczna nie**: W tym trybie żądań z ciągami zapytań nie są buforowane na węzeł brzegowy hello CDN.</span><span class="sxs-lookup"><span data-stu-id="6c57c-115">**no-cache**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="6c57c-116">węzeł brzegowy Hello pobiera hello zasobów bezpośrednio ze źródła hello i przekazuje ją obiektu żądającego toohello z każdym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="6c57c-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="6c57c-117">**Unikatowy pamięci podręcznej**: w tym trybie traktuje każde żądanie zawierające ciąg zapytania jako unikatowy zasób ze swojej własnej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="6c57c-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="6c57c-118">Na przykład Witaj odpowiedzi pochodzenia hello na żądanie dla *foo.ashx?q=bar* będą buforowane na węzeł brzegowy hello i zwrócony dla kolejnych pamięci podręcznych z tym samym ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="6c57c-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="6c57c-119">Żądanie *foo.ashx?q=somethingelse* będzie buforowana jako zasób oddzielne ze swoim toolive czasie.</span><span class="sxs-lookup"><span data-stu-id="6c57c-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="6c57c-120">Zmiana ustawienia profilów sieci CDN w warstwie premium buforowanie ciągów zapytań</span><span class="sxs-lookup"><span data-stu-id="6c57c-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="6c57c-121">Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c57c-121">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="6c57c-123">Otwiera portalu zarządzania Hello CDN.</span><span class="sxs-lookup"><span data-stu-id="6c57c-123">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="6c57c-124">Przesuń kursor myszy hello **HTTP dużych** kartę, a następnie przesuń kursor myszy hello **ustawienia pamięci podręcznej** wysuwane okno.</span><span class="sxs-lookup"><span data-stu-id="6c57c-124">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="6c57c-125">Polecenie **buforowania ciągu kwerendy**.</span><span class="sxs-lookup"><span data-stu-id="6c57c-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="6c57c-126">Opcje buforowania ciągu kwerendy są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="6c57c-126">Query string caching options are displayed.</span></span>
   
    ![Opcje buforowania ciągu kwerendy CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="6c57c-128">Po dokonaniu wyboru kliknij przycisk hello **aktualizacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c57c-128">After making your selection, click hello **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c57c-129">zmiany ustawień Hello mogą nie być od razu widoczne, zajmuje trochę czasu hello toopropagate rejestracji za pomocą hello CDN.</span><span class="sxs-lookup"><span data-stu-id="6c57c-129">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="6c57c-130">W przypadku profilów usługi <b>Azure CDN from Verizon</b> propagacja zwykle zostanie ukończona w ciągu 90 minut, ale niekiedy może to zająć więcej czasu.</span><span class="sxs-lookup"><span data-stu-id="6c57c-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

