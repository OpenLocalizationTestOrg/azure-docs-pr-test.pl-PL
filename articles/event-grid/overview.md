---
title: "Przegląd zdarzeń siatki aaaAzure"
description: "Opisuje Azure zdarzeń siatki i jego pojęcia."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a><span data-ttu-id="f5421-103">Wprowadzenie tooAzure siatki zdarzeń</span><span class="sxs-lookup"><span data-stu-id="f5421-103">An introduction tooAzure Event Grid</span></span>

<span data-ttu-id="f5421-104">Azure siatki zdarzeń umożliwia tooeasily kompilacji aplikacji za pomocą architektury oparty na zdarzeniach.</span><span class="sxs-lookup"><span data-stu-id="f5421-104">Azure Event Grid allows you tooeasily build applications with event-based architectures.</span></span> <span data-ttu-id="f5421-105">Możesz wybrać hello zasobów platformy Azure chcesz toosubscribe do i program obsługi zdarzeń hello lub elementu WebHook punktu końcowego toosend hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f5421-105">You select hello Azure resource you would like toosubscribe to, and give hello event handler or WebHook endpoint toosend hello event to.</span></span> <span data-ttu-id="f5421-106">Siatka zdarzeń ma wbudowaną obsługę zdarzenia pochodzące z usług Azure, takich jak magazynu obiektów blob i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="f5421-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="f5421-107">Siatka zdarzeń ma również obsługę niestandardowych aplikacji i innych zdarzeń, przy użyciu niestandardowych tematów i niestandardowych elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="f5421-107">Event Grid also has custom support for application and third-party events, using custom topics and custom webhooks.</span></span> 

<span data-ttu-id="f5421-108">Można użyć filtrów tooroute określonych zdarzeń toodifferent punkty końcowe multiemisji toomultiple punktów końcowych i upewnij się, że niezawodnie dostarczania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="f5421-108">You can use filters tooroute specific events toodifferent endpoints, multicast toomultiple endpoints, and make sure your events are reliably delivered.</span></span> <span data-ttu-id="f5421-109">Siatki zdarzeń również ma wbudowaną obsługą dla firm i niestandardowych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="f5421-109">Event Grid also has built in support for custom and third-party events.</span></span>

<span data-ttu-id="f5421-110">Dla wersji zapoznawczej hello obsługuje zdarzenia siatki **westus2** i **westcentralus** lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="f5421-110">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span> <span data-ttu-id="f5421-111">Zostanie dodany innych regionów.</span><span class="sxs-lookup"><span data-stu-id="f5421-111">Other regions will be added.</span></span>

<span data-ttu-id="f5421-112">Ten artykuł zawiera omówienie Azure zdarzeń siatki.</span><span class="sxs-lookup"><span data-stu-id="f5421-112">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="f5421-113">Tooget wprowadzenie siatki zdarzeń, zobacz [tworzenie i tras niestandardowych zdarzeń siatki zdarzeń Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="f5421-113">If you want tooget started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>

![Model funkcjonalności siatki zdarzeń](./media/overview/event-grid-functional-model.png)

<span data-ttu-id="f5421-115">Magazyn obiektów Blob nie jest obecnie publicznie dostępna jako wydawca.</span><span class="sxs-lookup"><span data-stu-id="f5421-115">Currently, Blob Storage is not publicly available as a publisher.</span></span>

## <a name="concepts"></a><span data-ttu-id="f5421-116">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="f5421-116">Concepts</span></span>

<span data-ttu-id="f5421-117">Istnieje pięć pojęcia w siatce zdarzeń platformy Azure, które umożliwiają zacząć:</span><span class="sxs-lookup"><span data-stu-id="f5421-117">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="f5421-118">**Zdarzenia** -co się stało.</span><span class="sxs-lookup"><span data-stu-id="f5421-118">**Events** - What happened.</span></span>
* <span data-ttu-id="f5421-119">**Wydawcy źródeł zdarzeń** — w przypadku, gdy zdarzenie hello miało miejsce.</span><span class="sxs-lookup"><span data-stu-id="f5421-119">**Event sources/publishers** - Where hello event took place.</span></span>
* <span data-ttu-id="f5421-120">**Tematy** — Witaj punktu końcowego, gdzie wydawców wysłać zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f5421-120">**Topics** - hello endpoint where publishers send events.</span></span>
* <span data-ttu-id="f5421-121">**Subskrypcja zdarzeń** -hello punktu końcowego lub wbudowany mechanizm tooroute zdarzeń, a czasami toomultiple obsługi.</span><span class="sxs-lookup"><span data-stu-id="f5421-121">**Event subscriptions** - hello endpoint or built-in mechanism tooroute events, sometimes toomultiple handlers.</span></span> <span data-ttu-id="f5421-122">Subskrypcje są również używane przez programy obsługi zdarzenia przychodzące filtru toointelligently.</span><span class="sxs-lookup"><span data-stu-id="f5421-122">Subscriptions are also used by handlers toointelligently filter incoming events.</span></span>
* <span data-ttu-id="f5421-123">**Programy obsługi zdarzeń** — Witaj aplikacji lub usługi dające dodatnią reakcję toohello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="f5421-123">**Event handlers** - hello app or service reacting toohello event.</span></span>

<span data-ttu-id="f5421-124">Aby uzyskać więcej informacji dotyczących tych pojęć, zobacz [pojęcia w siatce zdarzeń Azure](concepts.md).</span><span class="sxs-lookup"><span data-stu-id="f5421-124">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="f5421-125">Możliwości</span><span class="sxs-lookup"><span data-stu-id="f5421-125">Capabilities</span></span>

<span data-ttu-id="f5421-126">Oto niektóre najważniejsze funkcje hello Azure siatki zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="f5421-126">Here are some of hello key features of Azure Event Grid:</span></span>

* <span data-ttu-id="f5421-127">**Prostota** -zdarzenia tooaim punktu i kliknij przycisk z obsługi zdarzeń tooany zasobów platformy Azure lub punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="f5421-127">**Simplicity** - Point and click tooaim events from your Azure resource tooany event handler or endpoint.</span></span>
* <span data-ttu-id="f5421-128">**Zaawansowane filtrowanie** -filtr na zdarzenie typu lub zdarzenia publikowania tooensure ścieżka procedury obsługi zdarzeń odbierać istotne zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f5421-128">**Advanced filtering** - Filter on event type or event publish path tooensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="f5421-129">**Rozdysponowywania** -wiele punktów końcowych toohello subskrypcji tego samego zdarzenia toosend kopie tooas zdarzeń hello wielu miejscach zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="f5421-129">**Fan-out** - Subscribe multiple endpoints toohello same event toosend copies of hello event tooas many places as needed.</span></span>
* <span data-ttu-id="f5421-130">**Niezawodność** — korzystanie z 24-godzinnym ponownie za pomocą tooensure wykładniczego wycofywania zdarzenia są dostarczane.</span><span class="sxs-lookup"><span data-stu-id="f5421-130">**Reliability** - Utilize 24-hour retry with exponential backoff tooensure events are delivered.</span></span>
* <span data-ttu-id="f5421-131">**Płatności na zdarzenie** — płać tylko dla kwoty hello Użyj siatki zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="f5421-131">**Pay-per-event** - Pay only for hello amount you use Event Grid.</span></span>
* <span data-ttu-id="f5421-132">**Wysokiej przepływności** — Tworzenie dużych obciążeń w siatce zdarzeń z obsługą miliony zdarzeń na sekundę.</span><span class="sxs-lookup"><span data-stu-id="f5421-132">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="f5421-133">**Wbudowane zdarzenia** — Uzyskaj i szybko uruchomić zdefiniowany zasób wbudowanych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f5421-133">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="f5421-134">**Niestandardowe zdarzenia** -Użyj siatki zdarzeń trasy, filtr i niezawodnie dostarczyć zdarzeń niestandardowych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f5421-134">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

## <a name="built-in-publisher-and-handler-integration"></a><span data-ttu-id="f5421-135">Wbudowane funkcje integracji wydawcy i obsługi</span><span class="sxs-lookup"><span data-stu-id="f5421-135">Built-in publisher and handler integration</span></span>

<span data-ttu-id="f5421-136">Azure oferuje obsługę wbudowanych zdarzeń przy użyciu wielu usług, w tym zarówno i obsługi.</span><span class="sxs-lookup"><span data-stu-id="f5421-136">Azure offers built-in event support using numerous services, including both publishers and handlers.</span></span>

### <a name="publishers"></a><span data-ttu-id="f5421-137">Wydawcy</span><span class="sxs-lookup"><span data-stu-id="f5421-137">Publishers</span></span>

<span data-ttu-id="f5421-138">Obecnie hello następujących usług platformy Azure są wbudowane wydawcy obsługę zdarzeń siatki:</span><span class="sxs-lookup"><span data-stu-id="f5421-138">Currently, hello following Azure services have built-in publisher support for event grid:</span></span>

* <span data-ttu-id="f5421-139">Grupy zasobów (operacje zarządzania)</span><span class="sxs-lookup"><span data-stu-id="f5421-139">Resource Groups (management operations)</span></span>
* <span data-ttu-id="f5421-140">Subskrypcje platformy Azure (operacje zarządzania)</span><span class="sxs-lookup"><span data-stu-id="f5421-140">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="f5421-141">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f5421-141">Event Hubs</span></span>
* <span data-ttu-id="f5421-142">Niestandardowe — tematy</span><span class="sxs-lookup"><span data-stu-id="f5421-142">Custom Topics</span></span>

<span data-ttu-id="f5421-143">Innymi usługami Azure zostaną dodane tego roku.</span><span class="sxs-lookup"><span data-stu-id="f5421-143">Other Azure services will be added this year.</span></span>

### <a name="handlers"></a><span data-ttu-id="f5421-144">Programy obsługi</span><span class="sxs-lookup"><span data-stu-id="f5421-144">Handlers</span></span>

<span data-ttu-id="f5421-145">Obecnie hello następujących usług platformy Azure są wbudowana obsługa siatki zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="f5421-145">Currently, hello following Azure services have built-in handler support for Event Grid:</span></span> 

* <span data-ttu-id="f5421-146">Stan usługi Funkcje Azure</span><span class="sxs-lookup"><span data-stu-id="f5421-146">Azure Functions</span></span>
* <span data-ttu-id="f5421-147">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f5421-147">Logic Apps</span></span>
* <span data-ttu-id="f5421-148">Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f5421-148">Azure Automation</span></span>
* <span data-ttu-id="f5421-149">Elementów Webhook</span><span class="sxs-lookup"><span data-stu-id="f5421-149">WebHooks</span></span>

<span data-ttu-id="f5421-150">Innymi usługami Azure zostaną dodane tego roku.</span><span class="sxs-lookup"><span data-stu-id="f5421-150">Other Azure services will be added this year.</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="f5421-151">Co można zrobić siatki zdarzenia?</span><span class="sxs-lookup"><span data-stu-id="f5421-151">What can I do with Event Grid?</span></span>

<span data-ttu-id="f5421-152">Siatki zdarzeń Azure oferuje kilka możliwości, które znacząco poprawić niekorzystającą, ops automatyzacji i pracy integracji:</span><span class="sxs-lookup"><span data-stu-id="f5421-152">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="f5421-153">Architektury aplikacji bez użycia serwera</span><span class="sxs-lookup"><span data-stu-id="f5421-153">Serverless application architectures</span></span>

![Aplikację niekorzystającą](./media/overview/serverless_web_app.png)

<span data-ttu-id="f5421-155">Usługa Event Grid łączy źródła danych i programy obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="f5421-155">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="f5421-156">Na przykład użyć wyzwalacza tooinstantly siatki zdarzeń niekorzystającą funkcja analizy obrazu toorun każdym razem, gdy jest nowe zdjęcie dodać kontener magazynu obiektów blob tooa.</span><span class="sxs-lookup"><span data-stu-id="f5421-156">For example, use Event Grid tooinstantly trigger a serverless function toorun image analysis each time a new photo is added tooa blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="f5421-157">Automatyzacja OPS</span><span class="sxs-lookup"><span data-stu-id="f5421-157">Ops Automation</span></span>

![Automatyzacja operacji](./media/overview/Ops_automation.png)

<span data-ttu-id="f5421-159">Siatka zdarzeń umożliwia automatyzację toospeed i uprościć wymuszanie zasad.</span><span class="sxs-lookup"><span data-stu-id="f5421-159">Event Grid allows you toospeed automation and simplify policy enforcement.</span></span> <span data-ttu-id="f5421-160">Przykładowo usługa Event Grid może powiadamiać usługę Azure Automation, gdy maszyna wirtualna zostanie utworzona lub usługa SQL Database zostanie rozszerzona.</span><span class="sxs-lookup"><span data-stu-id="f5421-160">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="f5421-161">Zdarzenia te mogą służyć tooautomatically Sprawdź, czy konfiguracja usługi są zgodne, poddane metadanych narzędzia operacje, tag maszyn wirtualnych lub pliku elementów roboczych.</span><span class="sxs-lookup"><span data-stu-id="f5421-161">These events can be used tooautomatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="f5421-162">Integracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="f5421-162">Application integration</span></span>

![Integracja aplikacji](./media/overview/app_integration.png)

<span data-ttu-id="f5421-164">Usługa Event Grid łączy aplikację z innymi usługami.</span><span class="sxs-lookup"><span data-stu-id="f5421-164">Event Grid connects your app with other services.</span></span> <span data-ttu-id="f5421-165">Na przykład utworzyć toosend niestandardowego tematu tooEvent danych zdarzeń aplikacji siatki i wykorzystać jej wiarygodnych dostarczania zaawansowane routingu i bezpośrednia Integracja z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="f5421-165">For example, create a custom topic toosend your app's event data tooEvent Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="f5421-166">Alternatywnie można użyć siatki zdarzeń z dane tooprocess Logic Apps w dowolnym miejscu, bez pisania kodu.</span><span class="sxs-lookup"><span data-stu-id="f5421-166">Alternatively, you can use Event Grid with Logic Apps tooprocess data anywhere, without writing code.</span></span> 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a><span data-ttu-id="f5421-167">Czym różni się siatki zdarzeń od innych usług integracji Azure?</span><span class="sxs-lookup"><span data-stu-id="f5421-167">How is Event Grid different from other Azure integration services?</span></span>

<span data-ttu-id="f5421-168">Siatka zdarzeń jest płyty montażowej obsługi zdarzeń, która umożliwia programowanie sterowane zdarzeniami, reaktywne.</span><span class="sxs-lookup"><span data-stu-id="f5421-168">Event Grid is an eventing backplane that enables event-driven, reactive programming.</span></span> <span data-ttu-id="f5421-169">Jest ściśle zintegrowana z usługami Azure, a może być zintegrowana z usługami innych firm.</span><span class="sxs-lookup"><span data-stu-id="f5421-169">It is deeply integrated with Azure services and can be integrated with third-party services.</span></span> <span data-ttu-id="f5421-170">wiadomości powitania zdarzenia zawiera informacje hello potrzebne toochanges tooreact w usług i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f5421-170">hello event message contains hello information you need tooreact toochanges in services and applications.</span></span> <span data-ttu-id="f5421-171">Siatka zdarzeń nie jest potoku danych i nie dostarcza hello rzeczywistego obiektu, który został zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="f5421-171">Event Grid is not a data pipeline, and does not deliver hello actual object that was updated.</span></span>

<span data-ttu-id="f5421-172">Usługa Service Bus jest odpowiednia dla przedsiębiorstwa tradycyjnej aplikacji, które wymagają transakcji, porządkowanie, wykrywania duplikatów i natychmiastowe spójności.</span><span class="sxs-lookup"><span data-stu-id="f5421-172">Service Bus is well suited for traditional enterprise applications that require transactions, ordering, duplicate detection, and instantaneous consistency.</span></span> <span data-ttu-id="f5421-173">Siatka zdarzeń jest pod kątem szybkości, skala, szerokość i niedrogiej reaktywne modelu.</span><span class="sxs-lookup"><span data-stu-id="f5421-173">Event Grid is designed for speed, scale, breadth, and low cost in a reactive model.</span></span> <span data-ttu-id="f5421-174">Należy dobrze nadają się tooserverless architektury.</span><span class="sxs-lookup"><span data-stu-id="f5421-174">It is well suited tooserverless architecture.</span></span>

<span data-ttu-id="f5421-175">Zdarzenie siatki uzupełnia innymi usługami Azure, takich jak aplikacje logiki i usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="f5421-175">Event Grid complements other Azure services like Logic Apps and Event Hubs.</span></span> <span data-ttu-id="f5421-176">Wyzwalacze zdarzeń siatki hello toobegin aplikacji logiki jego przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="f5421-176">Event Grid triggers hello logic app toobegin its workflow.</span></span> <span data-ttu-id="f5421-177">Centra zdarzeń współpracuje z siatki zdarzeń włączając tooevents tooreact przechwytywania centra zdarzeń i potoki przychodzące i przekształcania danych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f5421-177">Event Hubs works with Event Grid by enabling you tooreact tooevents from Event Hubs Capture, and build data ingress and transformation pipelines.</span></span>

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="f5421-178">Ile kosztuje siatki zdarzeń</span><span class="sxs-lookup"><span data-stu-id="f5421-178">How much does Event Grid cost?</span></span>

<span data-ttu-id="f5421-179">Azure siatki zdarzeń używa modelu cenowego płatności na zdarzenie, więc płacisz tylko za można użyć.</span><span class="sxs-lookup"><span data-stu-id="f5421-179">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span>

<span data-ttu-id="f5421-180">Zdarzenia siatki koszty: 0,60 $ operacje milionów ($0.30 wersji zapoznawczej) i mogą hello pierwszych 100 000 operacji w ciągu miesiąca.</span><span class="sxs-lookup"><span data-stu-id="f5421-180">Event Grid costs $0.60 per million operations ($0.30 during preview) and hello first 100,000 operation per month are free.</span></span> <span data-ttu-id="f5421-181">Operacje są definiowane jako zdarzeń wejściowych, zaawansowane dopasowania, próba dostarczania i zarządzania wywołania.</span><span class="sxs-lookup"><span data-stu-id="f5421-181">Operations are defined as event ingress, advanced match, delivery attempt, and management calls.</span></span>  <span data-ttu-id="f5421-182">Więcej informacji można znaleźć na powitania [cennikiem](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="f5421-182">More details can be found on hello [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5421-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f5421-183">Next steps</span></span>

* <span data-ttu-id="f5421-184">[Tworzyć i subskrybować zdarzenia toocustom](custom-event-quickstart.md) od razu i Rozpocznij wysyłanie własnych punktu końcowego tooany zdarzeń niestandardowych za pomocą hello Azure zdarzeń siatki — Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="f5421-184">[Create and subscribe toocustom events](custom-event-quickstart.md) Jump right in and start sending your own custom events tooany endpoint using hello Azure Event Grid quickstart.</span></span>
* <span data-ttu-id="f5421-185">[Przy użyciu logiki aplikacji jako program obsługi zdarzeń](monitor-virtual-machine-changes-event-grid-logic-app.md) samouczek dotyczący tworzenia aplikacji za pomocą tooevents tooreact Logic Apps wypychana przez zdarzenie siatki.</span><span class="sxs-lookup"><span data-stu-id="f5421-185">[Using Logic Apps as an Event Handler](monitor-virtual-machine-changes-event-grid-logic-app.md) A tutorial on building an app using Logic Apps tooreact tooevents pushed by Event Grid.</span></span>
* [<span data-ttu-id="f5421-186">Dokumentacja interfejsu API REST siatki zdarzeń</span><span class="sxs-lookup"><span data-stu-id="f5421-186">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="f5421-187">Zawiera więcej informacji technicznych dotyczących hello Azure zdarzeń siatki i odwołanie zarządzania subskrypcji zdarzeń routingu i filtrowania.</span><span class="sxs-lookup"><span data-stu-id="f5421-187">Provides more technical information about hello Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>
