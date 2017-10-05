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
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="75667-103">Zalecenia dotyczące usługi Azure Machine Learning — integracja JavaScript</span><span class="sxs-lookup"><span data-stu-id="75667-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="75667-104">Należy rozpocząć korzystanie z usługi kognitywnych interfejsu API zalecenia zamiast tej wersji.</span><span class="sxs-lookup"><span data-stu-id="75667-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="75667-105">Kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną nowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="75667-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="75667-106">Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.</span><span class="sxs-lookup"><span data-stu-id="75667-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="75667-107">Dowiedz się więcej o [migracji do nowej usługi kognitywnych](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="75667-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="75667-108">Ten dokument przedstawiać integrowanie witryny przy użyciu języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="75667-108">This document depict how to integrate your site using JavaScript.</span></span> <span data-ttu-id="75667-109">JavaScript umożliwia wysyłanie danych zdarzeń i zużywać zalecenia po utworzeniu modelu zalecenie.</span><span class="sxs-lookup"><span data-stu-id="75667-109">The JavaScript enables you to send Data Acquisition events and to consume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="75667-110">Wszystkie operacje wykonywane za pośrednictwem JS jest również możliwe po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="75667-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="75667-111">1. Ogólne omówienie</span><span class="sxs-lookup"><span data-stu-id="75667-111">1. General Overview</span></span>
<span data-ttu-id="75667-112">Integrowanie witryny z usługi Azure ML zalecenia składają się na fazy 2:</span><span class="sxs-lookup"><span data-stu-id="75667-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="75667-113">Wysyłanie zdarzeń do usługi Azure ML zalecenia.</span><span class="sxs-lookup"><span data-stu-id="75667-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="75667-114">Spowoduje to włączenie do tworzenia modelu zalecenia.</span><span class="sxs-lookup"><span data-stu-id="75667-114">This will enable to build a recommendation model.</span></span>
2. <span data-ttu-id="75667-115">Używać zalecenia.</span><span class="sxs-lookup"><span data-stu-id="75667-115">Consume the recommendations.</span></span> <span data-ttu-id="75667-116">Po utworzeniu modelu może wykorzystać zalecenia.</span><span class="sxs-lookup"><span data-stu-id="75667-116">After the model is built you can consume the recommendations.</span></span> <span data-ttu-id="75667-117">(Ten dokument nie wyjaśniono, jak do tworzenia modelu, przeczytaj Przewodnik Szybki start, aby uzyskać więcej informacji na temat).</span><span class="sxs-lookup"><span data-stu-id="75667-117">(This document does not explain how to build a model, read the quick start guide to get more information on how).</span></span>

<span data-ttu-id="75667-118"><ins>Faza I</ins></span><span class="sxs-lookup"><span data-stu-id="75667-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="75667-119">W pierwszej fazie należy wstawić na stronach html małych biblioteki JavaScript, która umożliwia stronę, aby wysyłać zdarzenia występujące na stronie html do serwerów usługi Azure ML zalecenia (za pośrednictwem rynku danych):</span><span class="sxs-lookup"><span data-stu-id="75667-119">In the first phase you insert into your html pages a small JavaScript library that enables the page to send events as they occur on the html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Drawing1][1]

<span data-ttu-id="75667-121"><ins>Faza II</ins></span><span class="sxs-lookup"><span data-stu-id="75667-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="75667-122">W drugim etapie, gdy chcesz pokazać zalecenia na stronie wybierz jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="75667-122">In the second phase when you want to show the recommendations on the page you select one of the following options:</span></span>

<span data-ttu-id="75667-123">1. serwera (na etapie renderowania stron) wywołuje Azure ML zalecenia dotyczące serwera (za pośrednictwem rynku danych) można uzyskać zalecenia.</span><span class="sxs-lookup"><span data-stu-id="75667-123">1.Your server (on the phase of page rendering) calls Azure ML Recommendations Server (via Data Market) to get recommendations.</span></span> <span data-ttu-id="75667-124">Wyniki obejmują listę elementów id.</span><span class="sxs-lookup"><span data-stu-id="75667-124">The results include a list of items id.</span></span> <span data-ttu-id="75667-125">Serwer musi wzbogacić wyników z elementami metadanych (np. obrazów, opis) i wysyłany do przeglądarki, utworzonej strony.</span><span class="sxs-lookup"><span data-stu-id="75667-125">Your server needs to enrich the results with the items Meta data (e.g. images, description) and send the created page to the browser.</span></span>

![Drawing2][2]

<span data-ttu-id="75667-127">2. druga opcja to na mały plik JavaScript z pierwszą fazę prosta lista elementów zalecane.</span><span class="sxs-lookup"><span data-stu-id="75667-127">2.The other option is to use the small JavaScript file from phase one to get a simple list of recommended items.</span></span> <span data-ttu-id="75667-128">Dane otrzymane w tym miejscu jest leaner niż ten, w pierwszej opcji.</span><span class="sxs-lookup"><span data-stu-id="75667-128">The data received here is leaner than the one in the first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="75667-130">2. Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="75667-130">2. Prerequisites</span></span>
1. <span data-ttu-id="75667-131">Utwórz nowy model przy użyciu interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="75667-131">Create a new model using the APIs.</span></span> <span data-ttu-id="75667-132">Jak to zrobić, zobacz Przewodnik Szybki start.</span><span class="sxs-lookup"><span data-stu-id="75667-132">See the Quick start guide on how to do it.</span></span>
2. <span data-ttu-id="75667-133">Kodowanie z &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; z formatu base64.</span><span class="sxs-lookup"><span data-stu-id="75667-133">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="75667-134">(Ten będzie służyć do uwierzytelniania podstawowego do włączenia kodu Javascript do wywołania interfejsów API).</span><span class="sxs-lookup"><span data-stu-id="75667-134">(This will be used for the basic authentication to enable the JS code to call the APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="75667-135">3. Wysyłanie zdarzeń danych przy użyciu języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="75667-135">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="75667-136">Poniższe kroki ułatwiają wysyłanie zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="75667-136">The following steps facilitate sending events:</span></span>

1. <span data-ttu-id="75667-137">Uwzględnij biblioteki JQuery w kodzie.</span><span class="sxs-lookup"><span data-stu-id="75667-137">Include JQuery library in your code.</span></span> <span data-ttu-id="75667-138">Można go pobrać z nuget następujący adres URL.</span><span class="sxs-lookup"><span data-stu-id="75667-138">You can download it from nuget in the following URL.</span></span>
   
     <span data-ttu-id="75667-139">http://www.nuget.org/Packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="75667-139">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="75667-140">Obejmują biblioteki skryptów Java zalecenia z następującego adresu URL: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="75667-140">Include the Recommendations Java Script library from the following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="75667-141">Zainicjowanie biblioteki Azure ML zalecenia z odpowiednimi parametrami.</span><span class="sxs-lookup"><span data-stu-id="75667-141">Initialize Azure ML Recommendations library with the appropriate parameters.</span></span>
   
     <span data-ttu-id="75667-142"><script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Wysłać odpowiednie zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="75667-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send the appropriate event.</span></span> <span data-ttu-id="75667-143">Zobacz poniższą sekcję szczegółowe na wszystkich typów zdarzeń (Zdarzenie kliknięcia przykład) <script> Jeśli (typeof AzureMLRecommendationsEvent == "undefined") {</span><span class="sxs-lookup"><span data-stu-id="75667-143">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="75667-144">AzureMLRecommendationsEvent =] } AzureMLRecommendationsEvent.push({event: "click", item: "18321116"});</script></span><span class="sxs-lookup"><span data-stu-id="75667-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="75667-145">3.1.</span><span class="sxs-lookup"><span data-stu-id="75667-145">3.1.</span></span>    <span data-ttu-id="75667-146">Ograniczenia i obsługa przeglądarek</span><span class="sxs-lookup"><span data-stu-id="75667-146">Limitations and Browser Support</span></span>
<span data-ttu-id="75667-147">Jest to implementacja odwołania i jest on podawany jest.</span><span class="sxs-lookup"><span data-stu-id="75667-147">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="75667-148">Należy go obsługuje wszystkie główne przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="75667-148">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="75667-149">3.2.</span><span class="sxs-lookup"><span data-stu-id="75667-149">3.2.</span></span>    <span data-ttu-id="75667-150">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="75667-150">Type of Events</span></span>
<span data-ttu-id="75667-151">Istnieje 5 typów zdarzeń, które obsługuje biblioteki: kliknij przycisk, kliknij zalecenie, Dodaj do koszyka sklep, Usuń z koszyka produkcyjny i zakupu.</span><span class="sxs-lookup"><span data-stu-id="75667-151">There are 5 types of event that the library supports: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="75667-152">Brak dodatkowych zdarzeń, która jest używana do ustawiania kontekstu użytkownika o nazwie logowania.</span><span class="sxs-lookup"><span data-stu-id="75667-152">There is an additional event that is used to set the user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="75667-153">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="75667-153">3.2.1.</span></span> <span data-ttu-id="75667-154">Zdarzenie kliknięcia</span><span class="sxs-lookup"><span data-stu-id="75667-154">Click Event</span></span>
<span data-ttu-id="75667-155">To zdarzenie powinny być używane w dowolnym momencie, a użytkownik kliknął element.</span><span class="sxs-lookup"><span data-stu-id="75667-155">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="75667-156">Zwykle, gdy użytkownik kliknie element Nowa strona zostanie otwarty z szczegóły elementu; na tej stronie to zdarzenie jest wyzwalane.</span><span class="sxs-lookup"><span data-stu-id="75667-156">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="75667-157">Parametry:</span><span class="sxs-lookup"><span data-stu-id="75667-157">Parameters:</span></span>

* <span data-ttu-id="75667-158">zdarzenia (ciąg, obowiązkowe) "kliknij"</span><span class="sxs-lookup"><span data-stu-id="75667-158">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="75667-159">Unikatowy identyfikator elementu (ciąg, obowiązkowe) — element</span><span class="sxs-lookup"><span data-stu-id="75667-159">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="75667-160">Nazwa elementu (ciąg, opcjonalnie) nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="75667-160">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="75667-161">itemDescription (ciąg, opcjonalny) - opis elementu</span><span class="sxs-lookup"><span data-stu-id="75667-161">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="75667-162">itemCategory (ciąg, opcjonalny) kategorii elementu</span><span class="sxs-lookup"><span data-stu-id="75667-162">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="75667-163">Lub z opcjonalnymi danymi:</span><span class="sxs-lookup"><span data-stu-id="75667-163">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="75667-164">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="75667-164">3.2.2.</span></span> <span data-ttu-id="75667-165">Zalecenie Zdarzenie kliknięcia</span><span class="sxs-lookup"><span data-stu-id="75667-165">Recommendation Click Event</span></span>
<span data-ttu-id="75667-166">To zdarzenie powinny być używane w dowolnym momencie, a użytkownik kliknął element otrzymanego od zaleceń uczenia Maszynowego Azure jako element zalecane.</span><span class="sxs-lookup"><span data-stu-id="75667-166">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="75667-167">Zwykle, gdy użytkownik kliknie element Nowa strona zostanie otwarty z szczegóły elementu; na tej stronie to zdarzenie jest wyzwalane.</span><span class="sxs-lookup"><span data-stu-id="75667-167">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="75667-168">Parametry:</span><span class="sxs-lookup"><span data-stu-id="75667-168">Parameters:</span></span>

* <span data-ttu-id="75667-169">zdarzenia (ciąg, obowiązkowe) "recommendationclick"</span><span class="sxs-lookup"><span data-stu-id="75667-169">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="75667-170">Unikatowy identyfikator elementu (ciąg, obowiązkowe) — element</span><span class="sxs-lookup"><span data-stu-id="75667-170">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="75667-171">Nazwa elementu (ciąg, opcjonalnie) nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="75667-171">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="75667-172">itemDescription (ciąg, opcjonalny) - opis elementu</span><span class="sxs-lookup"><span data-stu-id="75667-172">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="75667-173">itemCategory (ciąg, opcjonalny) kategorii elementu</span><span class="sxs-lookup"><span data-stu-id="75667-173">itemCategory (string, optional) - the category of the item</span></span>
* <span data-ttu-id="75667-174">nasiona (tablicy ciągów, opcjonalny) - ziarna wygenerowanych zapytania zalecenia.</span><span class="sxs-lookup"><span data-stu-id="75667-174">seeds (string array, optional) - the seeds that generated the recommendation query.</span></span>
* <span data-ttu-id="75667-175">recoList (tablicy ciągów, opcjonalny) - wynik żądania zalecenie, który wygenerował element, który został kliknięty.</span><span class="sxs-lookup"><span data-stu-id="75667-175">recoList (string array, optional) - the result of the recommendation request that generated the item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="75667-176">Lub z opcjonalnymi danymi:</span><span class="sxs-lookup"><span data-stu-id="75667-176">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="75667-177">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="75667-177">3.2.3.</span></span> <span data-ttu-id="75667-178">Dodawanie zdarzeń koszyka zakupów</span><span class="sxs-lookup"><span data-stu-id="75667-178">Add Shopping Cart Event</span></span>
<span data-ttu-id="75667-179">To zdarzenie powinna być używana podczas użytkownika dodania elementu do koszyka.</span><span class="sxs-lookup"><span data-stu-id="75667-179">This event should be used when the user add an item to the shopping cart.</span></span>
<span data-ttu-id="75667-180">Parametry:</span><span class="sxs-lookup"><span data-stu-id="75667-180">Parameters:</span></span>

* <span data-ttu-id="75667-181">zdarzenia (ciąg, obowiązkowe) "addshopcart"</span><span class="sxs-lookup"><span data-stu-id="75667-181">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="75667-182">Unikatowy identyfikator elementu (ciąg, obowiązkowe) — element</span><span class="sxs-lookup"><span data-stu-id="75667-182">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="75667-183">Nazwa elementu (ciąg, opcjonalnie) nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="75667-183">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="75667-184">itemDescription (ciąg, opcjonalny) - opis elementu</span><span class="sxs-lookup"><span data-stu-id="75667-184">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="75667-185">itemCategory (ciąg, opcjonalny) kategorii elementu</span><span class="sxs-lookup"><span data-stu-id="75667-185">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="75667-186">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="75667-186">3.2.4.</span></span> <span data-ttu-id="75667-187">Usuń zdarzenia z koszyka zakupów</span><span class="sxs-lookup"><span data-stu-id="75667-187">Remove Shopping Cart Event</span></span>
<span data-ttu-id="75667-188">To zdarzenie powinien być używany, gdy użytkownik usuwa element do koszyka.</span><span class="sxs-lookup"><span data-stu-id="75667-188">This event should be used when the user removes an item to the shopping cart.</span></span>

<span data-ttu-id="75667-189">Parametry:</span><span class="sxs-lookup"><span data-stu-id="75667-189">Parameters:</span></span>

* <span data-ttu-id="75667-190">zdarzenia (ciąg, obowiązkowe) "removeshopcart"</span><span class="sxs-lookup"><span data-stu-id="75667-190">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="75667-191">Unikatowy identyfikator elementu (ciąg, obowiązkowe) — element</span><span class="sxs-lookup"><span data-stu-id="75667-191">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="75667-192">Nazwa elementu (ciąg, opcjonalnie) nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="75667-192">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="75667-193">itemDescription (ciąg, opcjonalny) - opis elementu</span><span class="sxs-lookup"><span data-stu-id="75667-193">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="75667-194">itemCategory (ciąg, opcjonalny) kategorii elementu</span><span class="sxs-lookup"><span data-stu-id="75667-194">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="75667-195">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="75667-195">3.2.5.</span></span> <span data-ttu-id="75667-196">Zdarzenie zakupu</span><span class="sxs-lookup"><span data-stu-id="75667-196">Purchase Event</span></span>
<span data-ttu-id="75667-197">To zdarzenie powinien być używany, gdy użytkownik zakupionych jego koszyk.</span><span class="sxs-lookup"><span data-stu-id="75667-197">This event should be used when the user purchased his shopping cart.</span></span>

<span data-ttu-id="75667-198">Parametry:</span><span class="sxs-lookup"><span data-stu-id="75667-198">Parameters:</span></span>

* <span data-ttu-id="75667-199">zdarzenia (ciąg) "Kup"</span><span class="sxs-lookup"><span data-stu-id="75667-199">event (string) - “purchase”</span></span>
* <span data-ttu-id="75667-200">elementy (zakupione []) - zawierający wpis dla każdego elementu zakupionych tablicy.</span><span class="sxs-lookup"><span data-stu-id="75667-200">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="75667-201">Format zakupionych:</span><span class="sxs-lookup"><span data-stu-id="75667-201">Purchased format:</span></span>
  * <span data-ttu-id="75667-202">element (string) — Unikatowy identyfikator elementu.</span><span class="sxs-lookup"><span data-stu-id="75667-202">item (string) - Unique identifier of the item.</span></span>
  * <span data-ttu-id="75667-203">Liczba (int lub string) — liczba elementów, które zostały zakupione.</span><span class="sxs-lookup"><span data-stu-id="75667-203">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="75667-204">Cena (float lub string) — pole opcjonalne - cen elementu.</span><span class="sxs-lookup"><span data-stu-id="75667-204">price (float or string) - optional field - the price of the item.</span></span>

<span data-ttu-id="75667-205">W poniższym przykładzie pokazano zakupu 3 elementy (33, 34, 35), dwa wszystkich pól (element, count, cena) oraz jedną (element 34) bez ceny.</span><span class="sxs-lookup"><span data-stu-id="75667-205">The example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="75667-206">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="75667-206">3.2.6.</span></span> <span data-ttu-id="75667-207">Zdarzenia logowania użytkownika</span><span class="sxs-lookup"><span data-stu-id="75667-207">User Login Event</span></span>
<span data-ttu-id="75667-208">Biblioteki zdarzeń zalecenia dotyczące uczenia Maszynowego Azure tworzy i korzystania z pliku cookie w celu identyfikacji zdarzenia, które pochodzą z tej samej przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="75667-208">Azure ML Recommendations Event library creates and use a cookie in order to identify events that came from the same browser.</span></span> <span data-ttu-id="75667-209">W celu ulepszania wyniki modelu zalecenia dotyczące uczenia Maszynowego Azure umożliwia ustalenie Unikatowy identyfikator użytkownika, który zastąpi użycia plików cookie.</span><span class="sxs-lookup"><span data-stu-id="75667-209">In order to improve the model results Azure ML Recommendations enables to set a user unique identification that will override the cookie usage.</span></span>

<span data-ttu-id="75667-210">To zdarzenie powinny być używane po logowaniu użytkownika do witryny.</span><span class="sxs-lookup"><span data-stu-id="75667-210">This event should be used after the user login to your site.</span></span>

<span data-ttu-id="75667-211">Parametry:</span><span class="sxs-lookup"><span data-stu-id="75667-211">Parameters:</span></span>

* <span data-ttu-id="75667-212">zdarzenia (ciąg) "userlogin"</span><span class="sxs-lookup"><span data-stu-id="75667-212">event (string) - “userlogin”</span></span>
* <span data-ttu-id="75667-213">Użytkownik (string) — Unikatowy identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75667-213">user (string) - unique identification of the user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="75667-214">4. Korzystanie z zalecenia za pośrednictwem kodu JavaScript</span><span class="sxs-lookup"><span data-stu-id="75667-214">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="75667-215">Kod, który wykorzystuje zalecenie jest wyzwalany przez zdarzenie JavaScript przez klienta strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="75667-215">The code that consumes the recommendation is triggered by some JavaScript event by the client’s webpage.</span></span> <span data-ttu-id="75667-216">Odpowiedź zalecenie zawiera identyfikatory elementów zalecane, ich nazwy i ich klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="75667-216">The recommendation response includes the recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="75667-217">Najlepiej użyć tej opcji tylko w przypadku wyświetlania listy elementów zalecane — Obsługa bardziej złożonych (takie jak dodanie metadanych elementu) ma się odbywać na integracji po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="75667-217">It’s best to use this option only for a list display of the recommended items - more complex handling (such as adding the item’s metadata) should be done on the server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="75667-218">4.1 korzystać zalecenia</span><span class="sxs-lookup"><span data-stu-id="75667-218">4.1 Consume Recommendations</span></span>
<span data-ttu-id="75667-219">Korzystać z zaleceń, które należy uwzględnić wymaganych bibliotek JavaScript na stronie oraz wywołanie AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="75667-219">To consume recommendations you need to include the required JavaScript libraries in your page and to call AzureMLRecommendationsStart.</span></span> <span data-ttu-id="75667-220">W sekcji 2.</span><span class="sxs-lookup"><span data-stu-id="75667-220">See section 2.</span></span>

<span data-ttu-id="75667-221">Użycie zalecenia dla jednego lub więcej elementów, należy wywołać metodę o nazwie: AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="75667-221">To consume recommendations for one or more items you need to call a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="75667-222">Parametry:</span><span class="sxs-lookup"><span data-stu-id="75667-222">Parameters:</span></span>

* <span data-ttu-id="75667-223">elementy (tablicę ciągów) — co najmniej jeden element, aby uzyskać zalecenia dotyczące.</span><span class="sxs-lookup"><span data-stu-id="75667-223">items (array of strings) - One or more items to get recommendations for.</span></span> <span data-ttu-id="75667-224">Jeśli zostaną zużyte na kompilację zmianie wysokości progów, można ustawić tutaj tylko jeden element.</span><span class="sxs-lookup"><span data-stu-id="75667-224">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="75667-225">numberOfResults (int) - liczba wymaganych wyników.</span><span class="sxs-lookup"><span data-stu-id="75667-225">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="75667-226">includeMetadata (wartość logiczna, opcjonalny) — Jeśli ma wartość "true" wskazuje, czy pole metadanych powinno zostać zapełnione w wyniku.</span><span class="sxs-lookup"><span data-stu-id="75667-226">includeMetadata (boolean, optional) - if set to ‘true’ indicates that the metadata field must be populated in the result.</span></span>
* <span data-ttu-id="75667-227">Funkcja przetwarzania — funkcja, która będzie obsługiwać zalecenia zwracane.</span><span class="sxs-lookup"><span data-stu-id="75667-227">Processing function - a function that will handle the recommendations returned.</span></span> <span data-ttu-id="75667-228">Dane są zwracane jako tablica:</span><span class="sxs-lookup"><span data-stu-id="75667-228">The data is returned as an array of:</span></span>
  * <span data-ttu-id="75667-229">Identyfikator unikatowy element — element</span><span class="sxs-lookup"><span data-stu-id="75667-229">Item - item unique id</span></span>
  * <span data-ttu-id="75667-230">Nazwa — Nazwa elementu (jeśli istnieje w katalogu)</span><span class="sxs-lookup"><span data-stu-id="75667-230">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="75667-231">Ocena — zaleceniem klasyfikacji</span><span class="sxs-lookup"><span data-stu-id="75667-231">rating - recommendation rating</span></span>
  * <span data-ttu-id="75667-232">metadane — ciąg reprezentujący metadanych elementu</span><span class="sxs-lookup"><span data-stu-id="75667-232">metadata - a string that represents the metadata of the item</span></span>

<span data-ttu-id="75667-233">Przykład: Następujący kod żądań 8 zalecenia dla elementu "64f6eb0d-947a-4c18-a16c-888da9e228ba" (bez określania includeMetadata - niejawnie wskazanego czy metadanych nie jest wymagane), następnie połącz wyniki do buforu.</span><span class="sxs-lookup"><span data-stu-id="75667-233">Example: The following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate the results into a buffer.</span></span>

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
