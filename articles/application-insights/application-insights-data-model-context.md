---
title: "Modelu danych Telemetrii wgląd aplikacji Azure — kontekstu Telemetrii | Dokumentacja firmy Microsoft"
description: Model danych kontekstu aplikacji Insights telemetrii
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: d6a0cad8bda6ca68aa691867e84f540c5ac9f6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="498fb-103">Kontekst danych telemetrii: model danych usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="498fb-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="498fb-104">Każdy element danych telemetrycznych może mieć pól jednoznacznie kontekstu.</span><span class="sxs-lookup"><span data-stu-id="498fb-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="498fb-105">Każde pole umożliwia scenariusza monitorowania.</span><span class="sxs-lookup"><span data-stu-id="498fb-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="498fb-106">Przechowywać informacje kontekstowe niestandardowych lub specyficznych dla aplikacji, należy użyć kolekcji właściwości niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="498fb-106">Use the custom properties collection to store custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="498fb-107">Wersja aplikacji</span><span class="sxs-lookup"><span data-stu-id="498fb-107">Application version</span></span>

<span data-ttu-id="498fb-108">Informacje w polach kontekstu aplikacji jest zawsze o aplikacji, który wysyła dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="498fb-108">Information in the application context fields is always about the application that is sending the telemetry.</span></span> <span data-ttu-id="498fb-109">Wersja aplikacji jest używany do analizowania trend zmiany zachowania aplikacji i jej korelacji do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="498fb-109">Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.</span></span>

<span data-ttu-id="498fb-110">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="498fb-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="498fb-111">Adres IP klienta</span><span class="sxs-lookup"><span data-stu-id="498fb-111">Client IP address</span></span>

<span data-ttu-id="498fb-112">Adres IP urządzenia klienckiego.</span><span class="sxs-lookup"><span data-stu-id="498fb-112">The IP address of the client device.</span></span> <span data-ttu-id="498fb-113">IPv4 i IPv6 są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="498fb-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="498fb-114">Podczas wysyłania danych telemetrycznych z usługą, kontekst lokalizacji jest dotyczące użytkownika, który zainicjował operację usługi.</span><span class="sxs-lookup"><span data-stu-id="498fb-114">When telemetry is sent from a service, the location context is about the user that initiated the operation in the service.</span></span> <span data-ttu-id="498fb-115">Usługa Application Insights wyodrębnienia informacji o lokalizacji geograficznej z adresu IP klienta i następnie obcięcie go.</span><span class="sxs-lookup"><span data-stu-id="498fb-115">Application Insights extract the geo-location information from the client IP and then truncate it.</span></span> <span data-ttu-id="498fb-116">Dlatego IP klienta samodzielnie nie można użyć jako informacje umożliwiające identyfikację użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="498fb-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="498fb-117">Maksymalna długość: 46</span><span class="sxs-lookup"><span data-stu-id="498fb-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="498fb-118">Typ urządzenia</span><span class="sxs-lookup"><span data-stu-id="498fb-118">Device type</span></span>

<span data-ttu-id="498fb-119">Pierwotnie to pole zostało służy do wskazania typu urządzenia, które jest używane przez użytkownika końcowego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="498fb-119">Originally this field was used to indicate the type of the device the end user of the application is using.</span></span> <span data-ttu-id="498fb-120">Obecnie jest używany głównie w celu odróżnienia telemetrii JavaScript z typem urządzenia telemetrii po stronie serwera z urządzeniem "Browser" typu "Komputer".</span><span class="sxs-lookup"><span data-stu-id="498fb-120">Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.</span></span>

<span data-ttu-id="498fb-121">Maksymalna długość: 64</span><span class="sxs-lookup"><span data-stu-id="498fb-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="498fb-122">Identyfikator operacji</span><span class="sxs-lookup"><span data-stu-id="498fb-122">Operation id</span></span>

<span data-ttu-id="498fb-123">Unikatowy identyfikator działania głównego.</span><span class="sxs-lookup"><span data-stu-id="498fb-123">A unique identifier of the root operation.</span></span> <span data-ttu-id="498fb-124">Ten identyfikator umożliwia telemetrii grupy między kilka składników.</span><span class="sxs-lookup"><span data-stu-id="498fb-124">This identifier allows to group telemetry across multiple components.</span></span> <span data-ttu-id="498fb-125">Zobacz [korelacji telemetrii](application-insights-correlation.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="498fb-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="498fb-126">Identyfikator operacji jest tworzony przez żądanie lub widok strony.</span><span class="sxs-lookup"><span data-stu-id="498fb-126">The operation id is created by either a request or a page view.</span></span> <span data-ttu-id="498fb-127">Wszystkie inne dane telemetryczne ustawia tego pola wartość dla widoku zawierającego żądanie lub strony.</span><span class="sxs-lookup"><span data-stu-id="498fb-127">All other telemetry sets this field to the value for the containing request or page view.</span></span> 

<span data-ttu-id="498fb-128">Maksymalna długość: 128</span><span class="sxs-lookup"><span data-stu-id="498fb-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="498fb-129">Identyfikator działania nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="498fb-129">Parent operation ID</span></span>

<span data-ttu-id="498fb-130">Unikatowy identyfikator elementu telemetrii natychmiastowego nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="498fb-130">The unique identifier of the telemetry item's immediate parent.</span></span> <span data-ttu-id="498fb-131">Zobacz [korelacji telemetrii](application-insights-correlation.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="498fb-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="498fb-132">Maksymalna długość: 128</span><span class="sxs-lookup"><span data-stu-id="498fb-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="498fb-133">Nazwa operacji</span><span class="sxs-lookup"><span data-stu-id="498fb-133">Operation name</span></span>

<span data-ttu-id="498fb-134">Nazwa (grupa) operacji.</span><span class="sxs-lookup"><span data-stu-id="498fb-134">The name (group) of the operation.</span></span> <span data-ttu-id="498fb-135">Nazwa operacji jest tworzony przez żądanie lub widok strony.</span><span class="sxs-lookup"><span data-stu-id="498fb-135">The operation name is created by either a request or a page view.</span></span> <span data-ttu-id="498fb-136">Wszystkie pozostałe elementy danych telemetrycznych ustawioną wartość dla widoku zawierającego żądanie lub strony w tym polu.</span><span class="sxs-lookup"><span data-stu-id="498fb-136">All other telemetry items set this field to the value for the containing request or page view.</span></span> <span data-ttu-id="498fb-137">Nazwa operacji służy do znajdowania wszystkie elementy danych telemetrycznych dla grupy działań (na przykład "GET głównej/Index").</span><span class="sxs-lookup"><span data-stu-id="498fb-137">Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="498fb-138">Ta właściwość kontekstu jest używana w odpowiedzi na pytania, takich jak "jakie są typowe wyjątki wyrzucane na tej stronie."</span><span class="sxs-lookup"><span data-stu-id="498fb-138">This context property is used to answer questions like "what are the typical exceptions thrown on this page."</span></span>

<span data-ttu-id="498fb-139">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="498fb-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-the-operation"></a><span data-ttu-id="498fb-140">Syntetyczne źródło operacji</span><span class="sxs-lookup"><span data-stu-id="498fb-140">Synthetic source of the operation</span></span>

<span data-ttu-id="498fb-141">Nazwa źródła syntetycznych.</span><span class="sxs-lookup"><span data-stu-id="498fb-141">Name of synthetic source.</span></span> <span data-ttu-id="498fb-142">Niektóre dane telemetryczne z aplikacji może reprezentować ruchu syntetycznego.</span><span class="sxs-lookup"><span data-stu-id="498fb-142">Some telemetry from the application may represent synthetic traffic.</span></span> <span data-ttu-id="498fb-143">Może to być indeksowania witryny sieci web, testy dostępności lokacji lub śladów z diagnostycznych bibliotek, takich jak Insights zestaw SDK usługi Application sam przeszukiwarkę sieci web.</span><span class="sxs-lookup"><span data-stu-id="498fb-143">It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="498fb-144">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="498fb-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="498fb-145">Identyfikator sesji</span><span class="sxs-lookup"><span data-stu-id="498fb-145">Session id</span></span>

<span data-ttu-id="498fb-146">Identyfikator sesji - wystąpienie interakcji z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="498fb-146">Session ID - the instance of the user's interaction with the app.</span></span> <span data-ttu-id="498fb-147">Informacje w polach kontekstu sesji jest zawsze o użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="498fb-147">Information in the session context fields is always about the end user.</span></span> <span data-ttu-id="498fb-148">Po wysłaniu danych telemetrycznych z usługą kontekstu sesji dotyczy użytkownika, który zainicjował operację usługi.</span><span class="sxs-lookup"><span data-stu-id="498fb-148">When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="498fb-149">Maksymalna długość: 64</span><span class="sxs-lookup"><span data-stu-id="498fb-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="498fb-150">Identyfikator użytkownika anonimowego</span><span class="sxs-lookup"><span data-stu-id="498fb-150">Anonymous user id</span></span>

<span data-ttu-id="498fb-151">Identyfikator użytkownika anonimowego.</span><span class="sxs-lookup"><span data-stu-id="498fb-151">Anonymous user id.</span></span> <span data-ttu-id="498fb-152">Reprezentuje użytkownika końcowego w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="498fb-152">Represents the end user of the application.</span></span> <span data-ttu-id="498fb-153">Po wysłaniu danych telemetrycznych z usługą kontekstu użytkownika dotyczy użytkownika, który zainicjował operację usługi.</span><span class="sxs-lookup"><span data-stu-id="498fb-153">When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="498fb-154">[Próbkowanie](app-insights-sampling.md) jest jedną z metod, aby zminimalizować ilość zbieranych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="498fb-154">[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry.</span></span> <span data-ttu-id="498fb-155">Algorytm próbkowania podejmuje próbę albo próbki przychodzący lub wychodzący wszystkie dane telemetryczne skorelowane.</span><span class="sxs-lookup"><span data-stu-id="498fb-155">Sampling algorithm attempts to either sample in or out all the correlated telemetry.</span></span> <span data-ttu-id="498fb-156">Identyfikator użytkownika anonimowego jest używana do próbkowania generowania oceny.</span><span class="sxs-lookup"><span data-stu-id="498fb-156">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="498fb-157">Dlatego użytkownik anonimowy identyfikator powinien być wystarczająco losowych wartości.</span><span class="sxs-lookup"><span data-stu-id="498fb-157">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="498fb-158">Za pomocą identyfikatora użytkownika anonimowego do przechowywania nazwy użytkownika jest nieprawidłowe użycie pola.</span><span class="sxs-lookup"><span data-stu-id="498fb-158">Using anonymous user id to store user name is a misuse of the field.</span></span> <span data-ttu-id="498fb-159">Za pomocą identyfikatora użytkownika uwierzytelnione.</span><span class="sxs-lookup"><span data-stu-id="498fb-159">Use Authenticated user id.</span></span>

<span data-ttu-id="498fb-160">Maksymalna długość: 128</span><span class="sxs-lookup"><span data-stu-id="498fb-160">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="498fb-161">Identyfikator użytkownika uwierzytelnionego</span><span class="sxs-lookup"><span data-stu-id="498fb-161">Authenticated user id</span></span>

<span data-ttu-id="498fb-162">Identyfikator uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="498fb-162">Authenticated user id.</span></span> <span data-ttu-id="498fb-163">Identyfikator użytkownika anonimowego i na odwrót to pole reprezentuje użytkownika o przyjaznej nazwie.</span><span class="sxs-lookup"><span data-stu-id="498fb-163">The opposite of anonymous user id, this field represents the user with a friendly name.</span></span> <span data-ttu-id="498fb-164">Od momentu jego osobowe go nie są zbierane domyślnie przez większość zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="498fb-164">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="498fb-165">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="498fb-165">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="498fb-166">Identyfikator konta</span><span class="sxs-lookup"><span data-stu-id="498fb-166">Account id</span></span>

<span data-ttu-id="498fb-167">W aplikacjach wielodostępne jest identyfikator konta lub nazwa użytkownika jest działające z.</span><span class="sxs-lookup"><span data-stu-id="498fb-167">In multi-tenant applications this is the account ID or name, which the user is acting with.</span></span> <span data-ttu-id="498fb-168">Przykładami mogą być identyfikator subskrypcji platformy Azure portalu lub blogu nazwa obsługi blogów.</span><span class="sxs-lookup"><span data-stu-id="498fb-168">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="498fb-169">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="498fb-169">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="498fb-170">Rola w chmurze</span><span class="sxs-lookup"><span data-stu-id="498fb-170">Cloud role</span></span>

<span data-ttu-id="498fb-171">Nazwa roli aplikacji jest częścią.</span><span class="sxs-lookup"><span data-stu-id="498fb-171">Name of the role the application is a part of.</span></span> <span data-ttu-id="498fb-172">Mapy bezpośrednio do nazw ról na platformie azure.</span><span class="sxs-lookup"><span data-stu-id="498fb-172">Maps directly to the role name in azure.</span></span> <span data-ttu-id="498fb-173">Można również odróżnienie micro usług, które są częścią pojedynczej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="498fb-173">Can also be used to distinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="498fb-174">Maksymalna długość: 256</span><span class="sxs-lookup"><span data-stu-id="498fb-174">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="498fb-175">Wystąpienie roli w chmurze</span><span class="sxs-lookup"><span data-stu-id="498fb-175">Cloud role instance</span></span>

<span data-ttu-id="498fb-176">Nazwa wystąpienia, w którym aplikacja jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="498fb-176">Name of the instance where the application is running.</span></span> <span data-ttu-id="498fb-177">Nazwa komputera lokalnego, aby uzyskać nazwę wystąpienia dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="498fb-177">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="498fb-178">Maksymalna długość: 256</span><span class="sxs-lookup"><span data-stu-id="498fb-178">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="498fb-179">Wewnętrzne: Wersja zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="498fb-179">Internal: SDK version</span></span>

<span data-ttu-id="498fb-180">Wersja zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="498fb-180">SDK version.</span></span> <span data-ttu-id="498fb-181">Zobacz https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification informacji.</span><span class="sxs-lookup"><span data-stu-id="498fb-181">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="498fb-182">Maksymalna długość: 64</span><span class="sxs-lookup"><span data-stu-id="498fb-182">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="498fb-183">Wewnętrzne: Nazwa węzła</span><span class="sxs-lookup"><span data-stu-id="498fb-183">Internal: Node name</span></span>

<span data-ttu-id="498fb-184">To pole reprezentuje nazwę węzła używana do celów rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="498fb-184">This field represents the node name used for billing purposes.</span></span> <span data-ttu-id="498fb-185">Użyj go, aby przesłonić standardowe wykrywanie węzłów.</span><span class="sxs-lookup"><span data-stu-id="498fb-185">Use it to override the standard detection of nodes.</span></span>

<span data-ttu-id="498fb-186">Maksymalna długość: 256</span><span class="sxs-lookup"><span data-stu-id="498fb-186">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="498fb-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="498fb-187">Next steps</span></span>

- <span data-ttu-id="498fb-188">Dowiedz się, jak [rozszerzanie i filtrować dane telemetryczne](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="498fb-188">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="498fb-189">Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="498fb-189">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="498fb-190">Zapoznaj się z kolekcji właściwości kontekstu standardowe [konfiguracji](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span><span class="sxs-lookup"><span data-stu-id="498fb-190">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
