---
title: 'Machine Learning zalecenia: Integracja JavaScript | Dokumentacja firmy Microsoft'
description: "Dokumentację platformy Azure zalecenia dotyczące — integracja JavaScript - Learning maszyny"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="8d31f-103">Zalecenia dotyczące usługi Azure Machine Learning — integracja JavaScript</span><span class="sxs-lookup"><span data-stu-id="8d31f-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="8d31f-104">Należy rozpocząć za pomocą hello usługi kognitywnych zalecenia dotyczące interfejsu API, zamiast tej wersji.</span><span class="sxs-lookup"><span data-stu-id="8d31f-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="8d31f-105">Hello kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną wszystkie hello nowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="8d31f-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="8d31f-106">Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.</span><span class="sxs-lookup"><span data-stu-id="8d31f-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="8d31f-107">Dowiedz się więcej o [toohello Migrowanie nową usługę kognitywnych](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="8d31f-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="8d31f-108">Ten dokument przedstawiać jak toointegrate witryny przy użyciu języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8d31f-108">This document depict how toointegrate your site using JavaScript.</span></span> <span data-ttu-id="8d31f-109">Hello JavaScript umożliwia toosend pozyskiwania danych zdarzeń i zalecenia tooconsume po utworzeniu modelu zalecenia.</span><span class="sxs-lookup"><span data-stu-id="8d31f-109">hello JavaScript enables you toosend Data Acquisition events and tooconsume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="8d31f-110">Wszystkie operacje wykonywane za pośrednictwem JS jest również możliwe po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="8d31f-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="8d31f-111">1. Ogólne omówienie</span><span class="sxs-lookup"><span data-stu-id="8d31f-111">1. General Overview</span></span>
<span data-ttu-id="8d31f-112">Integrowanie witryny z usługi Azure ML zalecenia składają się na fazy 2:</span><span class="sxs-lookup"><span data-stu-id="8d31f-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="8d31f-113">Wysyłanie zdarzeń do usługi Azure ML zalecenia.</span><span class="sxs-lookup"><span data-stu-id="8d31f-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="8d31f-114">Spowoduje to włączenie toobuild modelu zalecenia.</span><span class="sxs-lookup"><span data-stu-id="8d31f-114">This will enable toobuild a recommendation model.</span></span>
2. <span data-ttu-id="8d31f-115">Używać hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="8d31f-115">Consume hello recommendations.</span></span> <span data-ttu-id="8d31f-116">Po utworzeniu modelu hello mogą zużywać hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="8d31f-116">After hello model is built you can consume hello recommendations.</span></span> <span data-ttu-id="8d31f-117">(Ten dokument nie wyjaśniono, jak toobuild modelu, przeczytaj hello tooget Przewodnik Szybki start więcej informacji na temat).</span><span class="sxs-lookup"><span data-stu-id="8d31f-117">(This document does not explain how toobuild a model, read hello quick start guide tooget more information on how).</span></span>

<span data-ttu-id="8d31f-118"><ins>Faza I</ins></span><span class="sxs-lookup"><span data-stu-id="8d31f-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="8d31f-119">Hello pierwszą fazę wstawić na stronach html małych biblioteka języka JavaScript, która umożliwia hello strony toosend zdarzenia występujące na stronie html hello na serwerach Azure ML zalecenia (za pośrednictwem rynku danych):</span><span class="sxs-lookup"><span data-stu-id="8d31f-119">In hello first phase you insert into your html pages a small JavaScript library that enables hello page toosend events as they occur on hello html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Drawing1][1]

<span data-ttu-id="8d31f-121"><ins>Faza II</ins></span><span class="sxs-lookup"><span data-stu-id="8d31f-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="8d31f-122">W hello drugiej fazy, kiedy zechcesz zalecenia hello tooshow na stronie powitania wybraniu jednej z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="8d31f-122">In hello second phase when you want tooshow hello recommendations on hello page you select one of hello following options:</span></span>

<span data-ttu-id="8d31f-123">1. serwer (na etapie hello renderowania stron) wywołuje zalecenia tooget Azure ML zalecenia serwera (za pośrednictwem rynku danych).</span><span class="sxs-lookup"><span data-stu-id="8d31f-123">1.Your server (on hello phase of page rendering) calls Azure ML Recommendations Server (via Data Market) tooget recommendations.</span></span> <span data-ttu-id="8d31f-124">Witaj wyniki obejmują listę elementów id. Serwer musi tooenrich hello wyników z elementami hello metadanych (np. obrazów, opis) i wysłać hello utworzona strona toohello przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="8d31f-124">hello results include a list of items id. Your server needs tooenrich hello results with hello items Meta data (e.g. images, description) and send hello created page toohello browser.</span></span>

![Drawing2][2]

<span data-ttu-id="8d31f-126">2. Witaj druga opcja to toouse hello mały plik JavaScript z fazy jeden tooget to prosta lista elementów zalecane.</span><span class="sxs-lookup"><span data-stu-id="8d31f-126">2.hello other option is toouse hello small JavaScript file from phase one tooget a simple list of recommended items.</span></span> <span data-ttu-id="8d31f-127">w tym miejscu odebrane dane Hello jest leaner niż jeden hello w pierwszej opcji hello.</span><span class="sxs-lookup"><span data-stu-id="8d31f-127">hello data received here is leaner than hello one in hello first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="8d31f-129">2. Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8d31f-129">2. Prerequisites</span></span>
1. <span data-ttu-id="8d31f-130">Utwórz nowy model przy użyciu hello interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="8d31f-130">Create a new model using hello APIs.</span></span> <span data-ttu-id="8d31f-131">Zobacz Przewodnik Szybki start hello na temat toodo go.</span><span class="sxs-lookup"><span data-stu-id="8d31f-131">See hello Quick start guide on how toodo it.</span></span>
2. <span data-ttu-id="8d31f-132">Kodowanie z &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; z formatu base64.</span><span class="sxs-lookup"><span data-stu-id="8d31f-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="8d31f-133">(Ten będzie służyć do hello uwierzytelnianie podstawowe tooenable hello JS kodu toocall hello interfejsów API).</span><span class="sxs-lookup"><span data-stu-id="8d31f-133">(This will be used for hello basic authentication tooenable hello JS code toocall hello APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="8d31f-134">3. Wysyłanie zdarzeń danych przy użyciu języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="8d31f-134">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="8d31f-135">Witaj następujące kroki ułatwiają wysyłanie zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="8d31f-135">hello following steps facilitate sending events:</span></span>

1. <span data-ttu-id="8d31f-136">Uwzględnij biblioteki JQuery w kodzie.</span><span class="sxs-lookup"><span data-stu-id="8d31f-136">Include JQuery library in your code.</span></span> <span data-ttu-id="8d31f-137">Można go pobrać z nuget w hello następującego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="8d31f-137">You can download it from nuget in hello following URL.</span></span>
   
     <span data-ttu-id="8d31f-138">http://www.nuget.org/Packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="8d31f-138">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="8d31f-139">Zawierają hello skryptów Java zalecenia biblioteki z następującego adresu URL hello: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="8d31f-139">Include hello Recommendations Java Script library from hello following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="8d31f-140">Zainicjowanie biblioteki Azure ML zalecenia z odpowiednimi parametrami hello.</span><span class="sxs-lookup"><span data-stu-id="8d31f-140">Initialize Azure ML Recommendations library with hello appropriate parameters.</span></span>
   
     <span data-ttu-id="8d31f-141"><script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Odpowiednie zdarzenie hello wysyłania.</span><span class="sxs-lookup"><span data-stu-id="8d31f-141"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send hello appropriate event.</span></span> <span data-ttu-id="8d31f-142">Zobacz poniższą sekcję szczegółowe na wszystkich typów zdarzeń (Zdarzenie kliknięcia przykład) <script> Jeśli (typeof AzureMLRecommendationsEvent == "undefined") {</span><span class="sxs-lookup"><span data-stu-id="8d31f-142">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="8d31f-143">AzureMLRecommendationsEvent =] } AzureMLRecommendationsEvent.push({event: "click", item: "18321116"});</script></span><span class="sxs-lookup"><span data-stu-id="8d31f-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="8d31f-144">3.1.</span><span class="sxs-lookup"><span data-stu-id="8d31f-144">3.1.</span></span>    <span data-ttu-id="8d31f-145">Ograniczenia i obsługa przeglądarek</span><span class="sxs-lookup"><span data-stu-id="8d31f-145">Limitations and Browser Support</span></span>
<span data-ttu-id="8d31f-146">Jest to implementacja odwołania i jest on podawany jest.</span><span class="sxs-lookup"><span data-stu-id="8d31f-146">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="8d31f-147">Należy go obsługuje wszystkie główne przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="8d31f-147">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="8d31f-148">3.2.</span><span class="sxs-lookup"><span data-stu-id="8d31f-148">3.2.</span></span>    <span data-ttu-id="8d31f-149">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="8d31f-149">Type of Events</span></span>
<span data-ttu-id="8d31f-150">Istnieje 5 typy zdarzeń, które obsługuje biblioteki hello: kliknij pozycję zalecenie, Dodaj tooShop koszyka, Usuń z koszyka produkcyjny i zakupu.</span><span class="sxs-lookup"><span data-stu-id="8d31f-150">There are 5 types of event that hello library supports: Click, Recommendation Click, Add tooShop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="8d31f-151">Brak dodatkowych zdarzenie kontekstu użytkownika hello używane tooset o nazwie logowania.</span><span class="sxs-lookup"><span data-stu-id="8d31f-151">There is an additional event that is used tooset hello user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="8d31f-152">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="8d31f-152">3.2.1.</span></span> <span data-ttu-id="8d31f-153">Zdarzenie kliknięcia</span><span class="sxs-lookup"><span data-stu-id="8d31f-153">Click Event</span></span>
<span data-ttu-id="8d31f-154">To zdarzenie powinny być używane w dowolnym momencie, a użytkownik kliknął element.</span><span class="sxs-lookup"><span data-stu-id="8d31f-154">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="8d31f-155">Zwykle, gdy użytkownik kliknie element Nowa strona zostanie otwarty z szczegóły elementu hello; na tej stronie to zdarzenie jest wyzwalane.</span><span class="sxs-lookup"><span data-stu-id="8d31f-155">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="8d31f-156">Parametry:</span><span class="sxs-lookup"><span data-stu-id="8d31f-156">Parameters:</span></span>

* <span data-ttu-id="8d31f-157">zdarzenia (ciąg, obowiązkowe) "kliknij"</span><span class="sxs-lookup"><span data-stu-id="8d31f-157">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="8d31f-158">Unikatowy identyfikator elementu hello (ciąg, obowiązkowe) — element</span><span class="sxs-lookup"><span data-stu-id="8d31f-158">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="8d31f-159">Nazwa elementu (ciąg, opcjonalnie) nazwa hello elementu hello</span><span class="sxs-lookup"><span data-stu-id="8d31f-159">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="8d31f-160">itemDescription (ciąg, opcjonalny) hello opis elementu hello</span><span class="sxs-lookup"><span data-stu-id="8d31f-160">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="8d31f-161">itemCategory (ciąg, opcjonalny) kategorii hello hello elementu</span><span class="sxs-lookup"><span data-stu-id="8d31f-161">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="8d31f-162">Lub z opcjonalnymi danymi:</span><span class="sxs-lookup"><span data-stu-id="8d31f-162">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="8d31f-163">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="8d31f-163">3.2.2.</span></span> <span data-ttu-id="8d31f-164">Zalecenie Zdarzenie kliknięcia</span><span class="sxs-lookup"><span data-stu-id="8d31f-164">Recommendation Click Event</span></span>
<span data-ttu-id="8d31f-165">To zdarzenie powinny być używane w dowolnym momencie, a użytkownik kliknął element otrzymanego od zaleceń uczenia Maszynowego Azure jako element zalecane.</span><span class="sxs-lookup"><span data-stu-id="8d31f-165">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="8d31f-166">Zwykle, gdy użytkownik kliknie element Nowa strona zostanie otwarty z szczegóły elementu hello; na tej stronie to zdarzenie jest wyzwalane.</span><span class="sxs-lookup"><span data-stu-id="8d31f-166">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="8d31f-167">Parametry:</span><span class="sxs-lookup"><span data-stu-id="8d31f-167">Parameters:</span></span>

* <span data-ttu-id="8d31f-168">zdarzenia (ciąg, obowiązkowe) "recommendationclick"</span><span class="sxs-lookup"><span data-stu-id="8d31f-168">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="8d31f-169">Unikatowy identyfikator elementu hello (ciąg, obowiązkowe) — element</span><span class="sxs-lookup"><span data-stu-id="8d31f-169">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="8d31f-170">Nazwa elementu (ciąg, opcjonalnie) nazwa hello elementu hello</span><span class="sxs-lookup"><span data-stu-id="8d31f-170">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="8d31f-171">itemDescription (ciąg, opcjonalny) hello opis elementu hello</span><span class="sxs-lookup"><span data-stu-id="8d31f-171">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="8d31f-172">itemCategory (ciąg, opcjonalny) kategorii hello hello elementu</span><span class="sxs-lookup"><span data-stu-id="8d31f-172">itemCategory (string, optional) - hello category of hello item</span></span>
* <span data-ttu-id="8d31f-173">ziarna (tablicy ciągów, opcjonalny) — Witaj ziarna wygenerowanych hello zalecenie zapytania.</span><span class="sxs-lookup"><span data-stu-id="8d31f-173">seeds (string array, optional) - hello seeds that generated hello recommendation query.</span></span>
* <span data-ttu-id="8d31f-174">recoList (tablicy ciągów, opcjonalny) — Witaj wynik żądania zalecenie hello, generowany hello elementu, który został kliknięty.</span><span class="sxs-lookup"><span data-stu-id="8d31f-174">recoList (string array, optional) - hello result of hello recommendation request that generated hello item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="8d31f-175">Lub z opcjonalnymi danymi:</span><span class="sxs-lookup"><span data-stu-id="8d31f-175">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="8d31f-176">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="8d31f-176">3.2.3.</span></span> <span data-ttu-id="8d31f-177">Dodawanie zdarzeń koszyka zakupów</span><span class="sxs-lookup"><span data-stu-id="8d31f-177">Add Shopping Cart Event</span></span>
<span data-ttu-id="8d31f-178">To zdarzenie powinna być używana podczas użytkownika hello dodać toohello elementu koszyka.</span><span class="sxs-lookup"><span data-stu-id="8d31f-178">This event should be used when hello user add an item toohello shopping cart.</span></span>
<span data-ttu-id="8d31f-179">Parametry:</span><span class="sxs-lookup"><span data-stu-id="8d31f-179">Parameters:</span></span>

* <span data-ttu-id="8d31f-180">zdarzenia (ciąg, obowiązkowe) "addshopcart"</span><span class="sxs-lookup"><span data-stu-id="8d31f-180">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="8d31f-181">Unikatowy identyfikator elementu hello (ciąg, obowiązkowe) — element</span><span class="sxs-lookup"><span data-stu-id="8d31f-181">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="8d31f-182">Nazwa elementu (ciąg, opcjonalnie) nazwa hello elementu hello</span><span class="sxs-lookup"><span data-stu-id="8d31f-182">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="8d31f-183">itemDescription (ciąg, opcjonalny) hello opis elementu hello</span><span class="sxs-lookup"><span data-stu-id="8d31f-183">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="8d31f-184">itemCategory (ciąg, opcjonalny) kategorii hello hello elementu</span><span class="sxs-lookup"><span data-stu-id="8d31f-184">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="8d31f-185">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="8d31f-185">3.2.4.</span></span> <span data-ttu-id="8d31f-186">Usuń zdarzenia z koszyka zakupów</span><span class="sxs-lookup"><span data-stu-id="8d31f-186">Remove Shopping Cart Event</span></span>
<span data-ttu-id="8d31f-187">To zdarzenie powinien być używany, gdy użytkownik hello usuwa element toohello koszyk.</span><span class="sxs-lookup"><span data-stu-id="8d31f-187">This event should be used when hello user removes an item toohello shopping cart.</span></span>

<span data-ttu-id="8d31f-188">Parametry:</span><span class="sxs-lookup"><span data-stu-id="8d31f-188">Parameters:</span></span>

* <span data-ttu-id="8d31f-189">zdarzenia (ciąg, obowiązkowe) "removeshopcart"</span><span class="sxs-lookup"><span data-stu-id="8d31f-189">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="8d31f-190">Unikatowy identyfikator elementu hello (ciąg, obowiązkowe) — element</span><span class="sxs-lookup"><span data-stu-id="8d31f-190">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="8d31f-191">Nazwa elementu (ciąg, opcjonalnie) nazwa hello elementu hello</span><span class="sxs-lookup"><span data-stu-id="8d31f-191">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="8d31f-192">itemDescription (ciąg, opcjonalny) hello opis elementu hello</span><span class="sxs-lookup"><span data-stu-id="8d31f-192">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="8d31f-193">itemCategory (ciąg, opcjonalny) kategorii hello hello elementu</span><span class="sxs-lookup"><span data-stu-id="8d31f-193">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="8d31f-194">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="8d31f-194">3.2.5.</span></span> <span data-ttu-id="8d31f-195">Zdarzenie zakupu</span><span class="sxs-lookup"><span data-stu-id="8d31f-195">Purchase Event</span></span>
<span data-ttu-id="8d31f-196">To zdarzenie powinien być używany, gdy użytkownik hello kupił jego koszyk.</span><span class="sxs-lookup"><span data-stu-id="8d31f-196">This event should be used when hello user purchased his shopping cart.</span></span>

<span data-ttu-id="8d31f-197">Parametry:</span><span class="sxs-lookup"><span data-stu-id="8d31f-197">Parameters:</span></span>

* <span data-ttu-id="8d31f-198">zdarzenia (ciąg) "Kup"</span><span class="sxs-lookup"><span data-stu-id="8d31f-198">event (string) - “purchase”</span></span>
* <span data-ttu-id="8d31f-199">elementy (zakupione []) - zawierający wpis dla każdego elementu zakupionych tablicy.</span><span class="sxs-lookup"><span data-stu-id="8d31f-199">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="8d31f-200">Format zakupionych:</span><span class="sxs-lookup"><span data-stu-id="8d31f-200">Purchased format:</span></span>
  * <span data-ttu-id="8d31f-201">element (string) — Unikatowy identyfikator elementu hello.</span><span class="sxs-lookup"><span data-stu-id="8d31f-201">item (string) - Unique identifier of hello item.</span></span>
  * <span data-ttu-id="8d31f-202">Liczba (int lub string) — liczba elementów, które zostały zakupione.</span><span class="sxs-lookup"><span data-stu-id="8d31f-202">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="8d31f-203">Cena (float lub string) — pole opcjonalne — hello cena elementu hello.</span><span class="sxs-lookup"><span data-stu-id="8d31f-203">price (float or string) - optional field - hello price of hello item.</span></span>

<span data-ttu-id="8d31f-204">przykład Witaj poniżej przedstawia zakupu 3 elementy (33, 34, 35), dwa wszystkich pól (element, count, cena) oraz jedną (element 34) bez ceny.</span><span class="sxs-lookup"><span data-stu-id="8d31f-204">hello example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="8d31f-205">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="8d31f-205">3.2.6.</span></span> <span data-ttu-id="8d31f-206">Zdarzenia logowania użytkownika</span><span class="sxs-lookup"><span data-stu-id="8d31f-206">User Login Event</span></span>
<span data-ttu-id="8d31f-207">Azure zdarzeń zalecenia dotyczące uczenia Maszynowego tworzy biblioteki i używanie plików cookie w kolejności tooidentify zdarzenia, które nadeszły z hello tę samą przeglądarkę.</span><span class="sxs-lookup"><span data-stu-id="8d31f-207">Azure ML Recommendations Event library creates and use a cookie in order tooidentify events that came from hello same browser.</span></span> <span data-ttu-id="8d31f-208">W modelu hello tooimprove kolejność wyników Azure ML zalecenia umożliwia tooset Unikatowy identyfikator użytkownika, który zastąpi hello użycia plików cookie.</span><span class="sxs-lookup"><span data-stu-id="8d31f-208">In order tooimprove hello model results Azure ML Recommendations enables tooset a user unique identification that will override hello cookie usage.</span></span>

<span data-ttu-id="8d31f-209">To zdarzenie powinny być używane po hello użytkownika logowania tooyour lokacji.</span><span class="sxs-lookup"><span data-stu-id="8d31f-209">This event should be used after hello user login tooyour site.</span></span>

<span data-ttu-id="8d31f-210">Parametry:</span><span class="sxs-lookup"><span data-stu-id="8d31f-210">Parameters:</span></span>

* <span data-ttu-id="8d31f-211">zdarzenia (ciąg) "userlogin"</span><span class="sxs-lookup"><span data-stu-id="8d31f-211">event (string) - “userlogin”</span></span>
* <span data-ttu-id="8d31f-212">Użytkownik (string) — Unikatowy identyfikator hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8d31f-212">user (string) - unique identification of hello user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="8d31f-213">4. Korzystanie z zalecenia za pośrednictwem kodu JavaScript</span><span class="sxs-lookup"><span data-stu-id="8d31f-213">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="8d31f-214">Hello kod, który zużywa zalecenie hello jest wyzwalany przez zdarzenie JavaScript przez powitania klienta strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8d31f-214">hello code that consumes hello recommendation is triggered by some JavaScript event by hello client’s webpage.</span></span> <span data-ttu-id="8d31f-215">odpowiedź zalecenie Hello zawiera hello zalecane identyfikatory elementów, ich nazwy i ich klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="8d31f-215">hello recommendation response includes hello recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="8d31f-216">Jest najlepszym toouse, który tę opcję tylko w przypadku wyświetlania listy hello zalecane elementów - bardziej złożonej obsługi (takie jak dodanie metadanych elementu hello) ma się odbywać na powitania serwera po stronie integracji.</span><span class="sxs-lookup"><span data-stu-id="8d31f-216">It’s best toouse this option only for a list display of hello recommended items - more complex handling (such as adding hello item’s metadata) should be done on hello server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="8d31f-217">4.1 korzystać zalecenia</span><span class="sxs-lookup"><span data-stu-id="8d31f-217">4.1 Consume Recommendations</span></span>
<span data-ttu-id="8d31f-218">zalecenia tooconsume potrzebne tooinclude hello wymaganych bibliotek JavaScript na stronie i w toocall AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="8d31f-218">tooconsume recommendations you need tooinclude hello required JavaScript libraries in your page and toocall AzureMLRecommendationsStart.</span></span> <span data-ttu-id="8d31f-219">W sekcji 2.</span><span class="sxs-lookup"><span data-stu-id="8d31f-219">See section 2.</span></span>

<span data-ttu-id="8d31f-220">tooconsume zalecenia dla jednego lub więcej elementów należy wywołać metodę toocall: AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="8d31f-220">tooconsume recommendations for one or more items you need toocall a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="8d31f-221">Parametry:</span><span class="sxs-lookup"><span data-stu-id="8d31f-221">Parameters:</span></span>

* <span data-ttu-id="8d31f-222">elementy jeden lub więcej elementów tooget zalecenia dotyczące (Tablica ciągów -).</span><span class="sxs-lookup"><span data-stu-id="8d31f-222">items (array of strings) - One or more items tooget recommendations for.</span></span> <span data-ttu-id="8d31f-223">Jeśli zostaną zużyte na kompilację zmianie wysokości progów, można ustawić tutaj tylko jeden element.</span><span class="sxs-lookup"><span data-stu-id="8d31f-223">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="8d31f-224">numberOfResults (int) - liczba wymaganych wyników.</span><span class="sxs-lookup"><span data-stu-id="8d31f-224">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="8d31f-225">includeMetadata (wartość logiczna, opcjonalny) — Jeśli ustawić too'true "wskazuje tego pola metadanych hello powinno zostać zapełnione w wyniku hello.</span><span class="sxs-lookup"><span data-stu-id="8d31f-225">includeMetadata (boolean, optional) - if set too‘true’ indicates that hello metadata field must be populated in hello result.</span></span>
* <span data-ttu-id="8d31f-226">Funkcja przetwarzania — funkcja, która będzie obsługiwać zalecenia hello zwracane.</span><span class="sxs-lookup"><span data-stu-id="8d31f-226">Processing function - a function that will handle hello recommendations returned.</span></span> <span data-ttu-id="8d31f-227">Witaj, dane są zwracane jako tablica:</span><span class="sxs-lookup"><span data-stu-id="8d31f-227">hello data is returned as an array of:</span></span>
  * <span data-ttu-id="8d31f-228">Identyfikator unikatowy element — element</span><span class="sxs-lookup"><span data-stu-id="8d31f-228">Item - item unique id</span></span>
  * <span data-ttu-id="8d31f-229">Nazwa — Nazwa elementu (jeśli istnieje w katalogu)</span><span class="sxs-lookup"><span data-stu-id="8d31f-229">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="8d31f-230">Ocena — zaleceniem klasyfikacji</span><span class="sxs-lookup"><span data-stu-id="8d31f-230">rating - recommendation rating</span></span>
  * <span data-ttu-id="8d31f-231">metadane — ciąg reprezentujący hello metadanych elementu hello</span><span class="sxs-lookup"><span data-stu-id="8d31f-231">metadata - a string that represents hello metadata of hello item</span></span>

<span data-ttu-id="8d31f-232">Przykład: hello następującego kodu żądań 8 zalecenia dla elementu "64f6eb0d-947a-4c18-a16c-888da9e228ba" (bez określania includeMetadata - niejawnie wskazanego czy metadanych nie jest wymagane), następnie połącz hello wyniki do buforu.</span><span class="sxs-lookup"><span data-stu-id="8d31f-232">Example: hello following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate hello results into a buffer.</span></span>

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
