---
title: "aaaInteract z raportów za pomocą hello JavaScript API | Dokumentacja firmy Microsoft"
description: "Power BI Embedded, interakcji z raportów za pomocą hello JavaScript API"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a><span data-ttu-id="26d1d-103">Interakcje z raportów usługi Power BI za pomocą hello JavaScript API</span><span class="sxs-lookup"><span data-stu-id="26d1d-103">Interact with Power BI reports using hello JavaScript API</span></span>
<span data-ttu-id="26d1d-104">Umożliwia Power BI JavaScript API Hello tooeasily możesz osadzić raportów usługi Power BI w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="26d1d-104">hello Power BI JavaScript API enables you tooeasily embed Power BI reports into your applications.</span></span> <span data-ttu-id="26d1d-105">Z hello interfejsu API aplikacji programowo zakłócają elementów raportów, takich jak strony i filtry.</span><span class="sxs-lookup"><span data-stu-id="26d1d-105">With hello API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="26d1d-106">W sposób interaktywny sprawia to, że raporty usługi Power BI są bardziej zintegrowaną częścią aplikacji.</span><span class="sxs-lookup"><span data-stu-id="26d1d-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="26d1d-107">Osadzanie raportu usługi Power BI w aplikacji odbywa się przy użyciu elementu iframe, która jest obsługiwana w ramach aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="26d1d-107">You embed a Power BI report in your application by using an iframe that is hosted as part of hello application.</span></span> <span data-ttu-id="26d1d-108">Hello iframe pełni funkcję granicy między aplikacji i hello raport, jak widać w powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="26d1d-108">hello iframe acts as a boundary between your application and hello report, as you can see in hello following image.</span></span> 

![Element iframe usługi Power BI Embedded bez interfejsu API języka Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="26d1d-110">Hello iframe powoduje osadzanie procesu znacznie łatwiejsze hello, ale bez hello JavaScript API hello raportu i aplikacji nie mogą oddziaływać na siebie.</span><span class="sxs-lookup"><span data-stu-id="26d1d-110">hello iframe makes hello embedding process a lot easier, but without hello JavaScript API hello report and your application can't interact with each other.</span></span> <span data-ttu-id="26d1d-111">Ten brak interakcji można tworzyć wrażenie hello raportu nie jest częścią aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="26d1d-111">This lack of interaction can make it feel like hello report is not really part of hello application.</span></span> <span data-ttu-id="26d1d-112">Raport Hello i aplikacji są naprawdę potrzebne toocommunicate i z powrotem, tak jak powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="26d1d-112">hello report and application really need toocommunicate back and forth, as in hello following image.</span></span>

![Element iframe usługi Power BI Embedded z interfejsem API języka Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="26d1d-114">Witaj Power BI JavaScript API umożliwia toowrite kod, który można bezpiecznie przekazywane hello iframe granic.</span><span class="sxs-lookup"><span data-stu-id="26d1d-114">hello Power BI JavaScript API enables you toowrite code that can securely pass through hello iframe boundary.</span></span> <span data-ttu-id="26d1d-115">Ta umożliwia tooprogrammatically Twojej aplikacji wykonywania akcji w raporcie i toolisten zdarzeń z akcji, które użytkownicy wykonują w raporcie hello.</span><span class="sxs-lookup"><span data-stu-id="26d1d-115">This enables your application tooprogrammatically perform an action in a report, and toolisten for events from actions that users make within hello report.</span></span>

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a><span data-ttu-id="26d1d-116">Co należy zrobić z hello Power BI JavaScript API?</span><span class="sxs-lookup"><span data-stu-id="26d1d-116">What can you do with hello Power BI JavaScript API?</span></span>
<span data-ttu-id="26d1d-117">Z hello JavaScript API można Zarządzanie raportami, przejdź toopages w raporcie, filtrowanie raportu i obsługi osadzanie zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="26d1d-117">With hello JavaScript API you can manage reports, navigate toopages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="26d1d-118">Witaj Poniższy diagram przedstawia hello struktury hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="26d1d-118">hello following diagram shows hello structure of hello API.</span></span>

![Diagram interfejsu API języka JavaScript usługi Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="26d1d-120">Zarządzanie raportami</span><span class="sxs-lookup"><span data-stu-id="26d1d-120">Manage reports</span></span>
<span data-ttu-id="26d1d-121">Witaj Javascript API umożliwia zachowanie toomanage na poziomie raportu i strony hello:</span><span class="sxs-lookup"><span data-stu-id="26d1d-121">hello Javascript API enables you toomanage behavior at hello report and page level:</span></span>

* <span data-ttu-id="26d1d-122">Bezpieczne osadzanie określonego raportu Power BI w aplikacji - spróbuj hello [osadzić pokaz aplikacji](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="26d1d-122">Embed a specific Power BI Report securely in your application - try hello [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="26d1d-123">Określanie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="26d1d-123">Set access token</span></span>
* <span data-ttu-id="26d1d-124">Skonfiguruj raport hello</span><span class="sxs-lookup"><span data-stu-id="26d1d-124">Configure hello report</span></span>
  * <span data-ttu-id="26d1d-125">Włącz i Wyłącz okienko filtru hello i okienko nawigacji strony - spróbuj hello [aktualizowanie ustawień aplikacji demonstracyjnej](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="26d1d-125">Enable and disable hello filter pane and page navigation pane - try hello [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="26d1d-126">Określ ustawienia domyślne dla stron i filtry - spróbuj hello [zestaw wartości domyślnych pokaz](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="26d1d-126">Set defaults for pages and filters - try hello [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="26d1d-127">Włączanie i zamykanie trybu pełnoekranowego</span><span class="sxs-lookup"><span data-stu-id="26d1d-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="26d1d-128">Więcej informacji na temat osadzania raportu</span><span class="sxs-lookup"><span data-stu-id="26d1d-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a><span data-ttu-id="26d1d-129">Przejdź toopages w raporcie</span><span class="sxs-lookup"><span data-stu-id="26d1d-129">Navigate toopages in a report</span></span>
<span data-ttu-id="26d1d-130">enbales JavaScript API Hello możesz toodiscover wszystkie strony raportu i tooset hello bieżącej strony.</span><span class="sxs-lookup"><span data-stu-id="26d1d-130">hello JavaScript API enbales you toodiscover all pages in a report and tooset hello current page.</span></span> <span data-ttu-id="26d1d-131">Spróbuj hello [aplikacji demonstracyjnej nawigacji](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="26d1d-131">Try hello [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="26d1d-132">Więcej informacji o nawigacji na stronie</span><span class="sxs-lookup"><span data-stu-id="26d1d-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="26d1d-133">Filtrowanie raportu</span><span class="sxs-lookup"><span data-stu-id="26d1d-133">Filter a report</span></span>
<span data-ttu-id="26d1d-134">Witaj JavaScript API udostępnia podstawowe i zaawansowane filtrowanie możliwości dla osadzonych raporty i strony raportu.</span><span class="sxs-lookup"><span data-stu-id="26d1d-134">hello JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="26d1d-135">Spróbuj hello [filtrowania aplikacji demonstracyjnej](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)i przejrzyj niektórych wprowadzenia kodu.</span><span class="sxs-lookup"><span data-stu-id="26d1d-135">Try hello [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="26d1d-136">Filtry podstawowe</span><span class="sxs-lookup"><span data-stu-id="26d1d-136">Basic filters</span></span>
<span data-ttu-id="26d1d-137">Filtr podstawowe znajduje się na poziomie kolumny lub hierarchii i zawiera listę wartości tooinclude lub wykluczania.</span><span class="sxs-lookup"><span data-stu-id="26d1d-137">A basic filter is placed on a column or hierarchy level and contains a list of values tooinclude or exclude.</span></span>

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a><span data-ttu-id="26d1d-138">Filtry zaawansowane</span><span class="sxs-lookup"><span data-stu-id="26d1d-138">Advanced filters</span></span>
<span data-ttu-id="26d1d-139">Filtry zaawansowane użycie operatora logicznego hello i lub OR i zaakceptuj warunki jeden lub dwa, każdy z własnych operator i wartość.</span><span class="sxs-lookup"><span data-stu-id="26d1d-139">Advanced filters use hello logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="26d1d-140">Obsługiwane warunki to:</span><span class="sxs-lookup"><span data-stu-id="26d1d-140">Supported conditions are:</span></span>

* <span data-ttu-id="26d1d-141">None</span><span class="sxs-lookup"><span data-stu-id="26d1d-141">None</span></span>
* <span data-ttu-id="26d1d-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="26d1d-142">LessThan</span></span>
* <span data-ttu-id="26d1d-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="26d1d-143">LessThanOrEqual</span></span>
* <span data-ttu-id="26d1d-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="26d1d-144">GreaterThan</span></span>
* <span data-ttu-id="26d1d-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="26d1d-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="26d1d-146">Contains</span><span class="sxs-lookup"><span data-stu-id="26d1d-146">Contains</span></span>
* <span data-ttu-id="26d1d-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="26d1d-147">DoesNotContain</span></span>
* <span data-ttu-id="26d1d-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="26d1d-148">StartsWith</span></span>
* <span data-ttu-id="26d1d-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="26d1d-149">DoesNotStartWith</span></span>
* <span data-ttu-id="26d1d-150">Is</span><span class="sxs-lookup"><span data-stu-id="26d1d-150">Is</span></span>
* <span data-ttu-id="26d1d-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="26d1d-151">IsNot</span></span>
* <span data-ttu-id="26d1d-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="26d1d-152">IsBlank</span></span>
* <span data-ttu-id="26d1d-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="26d1d-153">IsNotBlank</span></span>

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[<span data-ttu-id="26d1d-154">Więcej informacji na temat filtrowania</span><span class="sxs-lookup"><span data-stu-id="26d1d-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="26d1d-155">Obsługa zdarzeń</span><span class="sxs-lookup"><span data-stu-id="26d1d-155">Handling events</span></span>
<span data-ttu-id="26d1d-156">Ponadto toosending informacji do hello iframe, aplikację można również odbierać informacji na temat hello następujące zdarzenia pochodzące z elementu iframe hello:</span><span class="sxs-lookup"><span data-stu-id="26d1d-156">In addition toosending information into hello iframe, your application can also receive information on hello following events coming from hello iframe:</span></span>

* <span data-ttu-id="26d1d-157">Embed</span><span class="sxs-lookup"><span data-stu-id="26d1d-157">Embed</span></span>
  * <span data-ttu-id="26d1d-158">loaded</span><span class="sxs-lookup"><span data-stu-id="26d1d-158">loaded</span></span>
  * <span data-ttu-id="26d1d-159">error</span><span class="sxs-lookup"><span data-stu-id="26d1d-159">error</span></span>
* <span data-ttu-id="26d1d-160">Reports</span><span class="sxs-lookup"><span data-stu-id="26d1d-160">Reports</span></span>
  * <span data-ttu-id="26d1d-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="26d1d-161">pageChanged</span></span>
  * <span data-ttu-id="26d1d-162">dataSelected (wkrótce)</span><span class="sxs-lookup"><span data-stu-id="26d1d-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="26d1d-163">Więcej informacji na temat obsługi zdarzeń</span><span class="sxs-lookup"><span data-stu-id="26d1d-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="26d1d-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="26d1d-164">Next steps</span></span>
<span data-ttu-id="26d1d-165">Aby uzyskać więcej informacji na temat hello Power BI JavaScript API wyewidencjonować hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="26d1d-165">For more information about hello Power BI JavaScript API, check out hello following links:</span></span>

* [<span data-ttu-id="26d1d-166">Strona typu Wiki interfejsu API języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="26d1d-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="26d1d-167">Dokumentacja modelu obiektów</span><span class="sxs-lookup"><span data-stu-id="26d1d-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="26d1d-168">Przykłady</span><span class="sxs-lookup"><span data-stu-id="26d1d-168">Samples</span></span>
  * [<span data-ttu-id="26d1d-169">Angular</span><span class="sxs-lookup"><span data-stu-id="26d1d-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="26d1d-170">Ember</span><span class="sxs-lookup"><span data-stu-id="26d1d-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="26d1d-171">Pokaz na żywo</span><span class="sxs-lookup"><span data-stu-id="26d1d-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

