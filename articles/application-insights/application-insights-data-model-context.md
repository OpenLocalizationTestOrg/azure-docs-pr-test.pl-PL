---
title: aaaAzure aplikacji modelu danych Telemetrii Insights - kontekstu Telemetrii | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="6a5d1-103">Kontekst danych telemetrii: model danych usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="6a5d1-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="6a5d1-104">Każdy element danych telemetrycznych może mieć pól jednoznacznie kontekstu.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="6a5d1-105">Każde pole umożliwia scenariusza monitorowania.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="6a5d1-106">Użyj hello niestandardowe właściwości z kolekcji toostore niestandardowych lub specyficznych dla aplikacji informacje kontekstowe.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-106">Use hello custom properties collection toostore custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="6a5d1-107">Wersja aplikacji</span><span class="sxs-lookup"><span data-stu-id="6a5d1-107">Application version</span></span>

<span data-ttu-id="6a5d1-108">Informacje w polach kontekstu aplikacji hello jest zawsze o aplikacji hello, który wysyła dane telemetryczne hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-108">Information in hello application context fields is always about hello application that is sending hello telemetry.</span></span> <span data-ttu-id="6a5d1-109">Wersja aplikacji jest używany tooanalyze trend zmiany w zachowanie aplikacji hello i jej wdrożenia toohello korelacji.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-109">Application version is used tooanalyze trend changes in hello application behavior and its correlation toohello deployments.</span></span>

<span data-ttu-id="6a5d1-110">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="6a5d1-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="6a5d1-111">Adres IP klienta</span><span class="sxs-lookup"><span data-stu-id="6a5d1-111">Client IP address</span></span>

<span data-ttu-id="6a5d1-112">adres IP Hello powitania klienta urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-112">hello IP address of hello client device.</span></span> <span data-ttu-id="6a5d1-113">IPv4 i IPv6 są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="6a5d1-114">Po wysłaniu danych telemetrycznych z usługi kontekstu lokalizacji hello jest o hello użytkownika, który zainicjował operację hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-114">When telemetry is sent from a service, hello location context is about hello user that initiated hello operation in hello service.</span></span> <span data-ttu-id="6a5d1-115">Usługi Application Insights wyodrębnienia informacji o lokalizacji geograficznej hello z hello IP klienta, a następnie instrukcja truncate.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-115">Application Insights extract hello geo-location information from hello client IP and then truncate it.</span></span> <span data-ttu-id="6a5d1-116">Dlatego IP klienta samodzielnie nie można użyć jako informacje umożliwiające identyfikację użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="6a5d1-117">Maksymalna długość: 46</span><span class="sxs-lookup"><span data-stu-id="6a5d1-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="6a5d1-118">Typ urządzenia</span><span class="sxs-lookup"><span data-stu-id="6a5d1-118">Device type</span></span>

<span data-ttu-id="6a5d1-119">Pierwotnie został użyty w tym polu tooindicate hello typ użytkownika końcowego hello urządzenia hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-119">Originally this field was used tooindicate hello type of hello device hello end user of hello application is using.</span></span> <span data-ttu-id="6a5d1-120">Dzisiaj hello urządzenia typu "Przeglądarki" z telemetrii po stronie serwera z typem urządzenia hello 'Komputera' użyć głównie toodistinguish JavaScript telemetrii.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-120">Today used primarily toodistinguish JavaScript telemetry with hello device type 'Browser' from server-side telemetry with hello device type 'PC'.</span></span>

<span data-ttu-id="6a5d1-121">Maksymalna długość: 64</span><span class="sxs-lookup"><span data-stu-id="6a5d1-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="6a5d1-122">Identyfikator operacji</span><span class="sxs-lookup"><span data-stu-id="6a5d1-122">Operation id</span></span>

<span data-ttu-id="6a5d1-123">Unikatowy identyfikator hello działania głównego.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-123">A unique identifier of hello root operation.</span></span> <span data-ttu-id="6a5d1-124">Ten identyfikator umożliwia telemetrii toogroup przez kilka składników.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-124">This identifier allows toogroup telemetry across multiple components.</span></span> <span data-ttu-id="6a5d1-125">Zobacz [korelacji telemetrii](application-insights-correlation.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="6a5d1-126">Identyfikator operacji Hello jest tworzony przez żądanie lub widok strony.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-126">hello operation id is created by either a request or a page view.</span></span> <span data-ttu-id="6a5d1-127">Wszystkie inne dane telemetryczne ustawia tego pola wartość toohello hello zawierające żądania lub widoku strony.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-127">All other telemetry sets this field toohello value for hello containing request or page view.</span></span> 

<span data-ttu-id="6a5d1-128">Maksymalna długość: 128</span><span class="sxs-lookup"><span data-stu-id="6a5d1-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="6a5d1-129">Identyfikator działania nadrzędnego</span><span class="sxs-lookup"><span data-stu-id="6a5d1-129">Parent operation ID</span></span>

<span data-ttu-id="6a5d1-130">Witaj Unikatowy identyfikator hello telemetrii bezpośrednim elementem nadrzędnym składnika.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-130">hello unique identifier of hello telemetry item's immediate parent.</span></span> <span data-ttu-id="6a5d1-131">Zobacz [korelacji telemetrii](application-insights-correlation.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="6a5d1-132">Maksymalna długość: 128</span><span class="sxs-lookup"><span data-stu-id="6a5d1-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="6a5d1-133">Nazwa operacji</span><span class="sxs-lookup"><span data-stu-id="6a5d1-133">Operation name</span></span>

<span data-ttu-id="6a5d1-134">Nazwa Hello (grupa) hello operacji.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-134">hello name (group) of hello operation.</span></span> <span data-ttu-id="6a5d1-135">Nazwa operacji Hello jest tworzony przez żądanie lub widok strony.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-135">hello operation name is created by either a request or a page view.</span></span> <span data-ttu-id="6a5d1-136">Wszystkie pozostałe elementy danych telemetrycznych ta wartość pola toohello dla hello zawierające żądania lub strony widoku.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-136">All other telemetry items set this field toohello value for hello containing request or page view.</span></span> <span data-ttu-id="6a5d1-137">Nazwa operacji służy do znajdowania wszystkie elementy telemetrii hello grupy operacji (na przykład "GET głównej/Index").</span><span class="sxs-lookup"><span data-stu-id="6a5d1-137">Operation name is used for finding all hello telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="6a5d1-138">Ta właściwość kontekst jest używany tooanswer, które pytania, takich jak "co to są hello wyjątków typowe zgłaszanych na tej stronie."</span><span class="sxs-lookup"><span data-stu-id="6a5d1-138">This context property is used tooanswer questions like "what are hello typical exceptions thrown on this page."</span></span>

<span data-ttu-id="6a5d1-139">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="6a5d1-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-hello-operation"></a><span data-ttu-id="6a5d1-140">Syntetyczne źródło hello operacji</span><span class="sxs-lookup"><span data-stu-id="6a5d1-140">Synthetic source of hello operation</span></span>

<span data-ttu-id="6a5d1-141">Nazwa źródła syntetycznych.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-141">Name of synthetic source.</span></span> <span data-ttu-id="6a5d1-142">Niektóre dane telemetryczne z aplikacji hello może reprezentować ruchu syntetycznego.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-142">Some telemetry from hello application may represent synthetic traffic.</span></span> <span data-ttu-id="6a5d1-143">Może być witryny sieci web hello indeksowania przez przeszukiwarkę sieci web, testy dostępności lokacji lub śladów z diagnostycznych bibliotek, takich jak Insights zestaw SDK usługi Application sam.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-143">It may be web crawler indexing hello web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="6a5d1-144">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="6a5d1-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="6a5d1-145">Identyfikator sesji</span><span class="sxs-lookup"><span data-stu-id="6a5d1-145">Session id</span></span>

<span data-ttu-id="6a5d1-146">Identyfikator sesji - hello wystąpienia użytkownika hello interakcji z aplikacją hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-146">Session ID - hello instance of hello user's interaction with hello app.</span></span> <span data-ttu-id="6a5d1-147">Informacje w polach kontekstu sesji hello jest zawsze o hello użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-147">Information in hello session context fields is always about hello end user.</span></span> <span data-ttu-id="6a5d1-148">Po wysłaniu danych telemetrycznych z usługi kontekstu sesji hello jest o hello użytkownika, który zainicjował operację hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-148">When telemetry is sent from a service, hello session context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="6a5d1-149">Maksymalna długość: 64</span><span class="sxs-lookup"><span data-stu-id="6a5d1-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="6a5d1-150">Identyfikator użytkownika anonimowego</span><span class="sxs-lookup"><span data-stu-id="6a5d1-150">Anonymous user id</span></span>

<span data-ttu-id="6a5d1-151">Identyfikator użytkownika anonimowego. Reprezentuje użytkownika końcowego hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-151">Anonymous user id. Represents hello end user of hello application.</span></span> <span data-ttu-id="6a5d1-152">Po wysłaniu danych telemetrycznych z usługi kontekstu użytkownika hello jest o hello użytkownika, który zainicjował operację hello hello usługi.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-152">When telemetry is sent from a service, hello user context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="6a5d1-153">[Próbkowanie](app-insights-sampling.md) jest jednym z hello techniki toominimize hello ilość zbieranych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-153">[Sampling](app-insights-sampling.md) is one of hello techniques toominimize hello amount of collected telemetry.</span></span> <span data-ttu-id="6a5d1-154">Próbkowanie tooeither prób algorytm próbki przychodzący lub wychodzący wszystkich hello skorelowane telemetrii.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-154">Sampling algorithm attempts tooeither sample in or out all hello correlated telemetry.</span></span> <span data-ttu-id="6a5d1-155">Identyfikator użytkownika anonimowego jest używana do próbkowania generowania oceny.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-155">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="6a5d1-156">Dlatego użytkownik anonimowy identyfikator powinien być wystarczająco losowych wartości.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-156">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="6a5d1-157">Przy użyciu nazwy użytkownika toostore identyfikatora użytkownika anonimowego jest nieprawidłowe użycie pola hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-157">Using anonymous user id toostore user name is a misuse of hello field.</span></span> <span data-ttu-id="6a5d1-158">Za pomocą identyfikatora użytkownika uwierzytelnione.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-158">Use Authenticated user id.</span></span>

<span data-ttu-id="6a5d1-159">Maksymalna długość: 128</span><span class="sxs-lookup"><span data-stu-id="6a5d1-159">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="6a5d1-160">Identyfikator użytkownika uwierzytelnionego</span><span class="sxs-lookup"><span data-stu-id="6a5d1-160">Authenticated user id</span></span>

<span data-ttu-id="6a5d1-161">Identyfikator uwierzytelnionego użytkownika. Witaj przeciwne identyfikatora użytkownika anonimowego, to pole reprezentuje użytkownika hello o przyjaznej nazwie.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-161">Authenticated user id. hello opposite of anonymous user id, this field represents hello user with a friendly name.</span></span> <span data-ttu-id="6a5d1-162">Od momentu jego osobowe go nie są zbierane domyślnie przez większość zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-162">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="6a5d1-163">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="6a5d1-163">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="6a5d1-164">Identyfikator konta</span><span class="sxs-lookup"><span data-stu-id="6a5d1-164">Account id</span></span>

<span data-ttu-id="6a5d1-165">W aplikacjach wielodostępnej jest identyfikator konta hello lub nazwę użytkownika, który hello działa z.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-165">In multi-tenant applications this is hello account ID or name, which hello user is acting with.</span></span> <span data-ttu-id="6a5d1-166">Przykładami mogą być identyfikator subskrypcji platformy Azure portalu lub blogu nazwa obsługi blogów.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="6a5d1-167">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="6a5d1-167">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="6a5d1-168">Rola w chmurze</span><span class="sxs-lookup"><span data-stu-id="6a5d1-168">Cloud role</span></span>

<span data-ttu-id="6a5d1-169">Nazwa aplikacji hello roli hello jest częścią.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-169">Name of hello role hello application is a part of.</span></span> <span data-ttu-id="6a5d1-170">Mapuje bezpośrednio toohello nazwy roli na platformie azure.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-170">Maps directly toohello role name in azure.</span></span> <span data-ttu-id="6a5d1-171">Może być również używane toodistinguish micro usług, które są częścią pojedynczej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-171">Can also be used toodistinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="6a5d1-172">Maksymalna długość: 256</span><span class="sxs-lookup"><span data-stu-id="6a5d1-172">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="6a5d1-173">Wystąpienie roli w chmurze</span><span class="sxs-lookup"><span data-stu-id="6a5d1-173">Cloud role instance</span></span>

<span data-ttu-id="6a5d1-174">Nazwa wystąpienia hello, w którym jest uruchomiona aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-174">Name of hello instance where hello application is running.</span></span> <span data-ttu-id="6a5d1-175">Nazwa komputera lokalnego, aby uzyskać nazwę wystąpienia dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-175">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="6a5d1-176">Maksymalna długość: 256</span><span class="sxs-lookup"><span data-stu-id="6a5d1-176">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="6a5d1-177">Wewnętrzne: Wersja zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="6a5d1-177">Internal: SDK version</span></span>

<span data-ttu-id="6a5d1-178">Wersja zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-178">SDK version.</span></span> <span data-ttu-id="6a5d1-179">Zobacz https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification informacji.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="6a5d1-180">Maksymalna długość: 64</span><span class="sxs-lookup"><span data-stu-id="6a5d1-180">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="6a5d1-181">Wewnętrzne: Nazwa węzła</span><span class="sxs-lookup"><span data-stu-id="6a5d1-181">Internal: Node name</span></span>

<span data-ttu-id="6a5d1-182">To pole reprezentuje nazwę węzła hello używana do celów rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-182">This field represents hello node name used for billing purposes.</span></span> <span data-ttu-id="6a5d1-183">Użyj toooverride hello standardowe wykrywanie węzłów.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-183">Use it toooverride hello standard detection of nodes.</span></span>

<span data-ttu-id="6a5d1-184">Maksymalna długość: 256</span><span class="sxs-lookup"><span data-stu-id="6a5d1-184">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="6a5d1-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a5d1-185">Next steps</span></span>

- <span data-ttu-id="6a5d1-186">Dowiedz się, jak za[rozszerzanie i filtrować dane telemetryczne](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="6a5d1-186">Learn how too[extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="6a5d1-187">Zobacz [modelu danych](application-insights-data-model.md) dla modelu danych i typów usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6a5d1-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="6a5d1-188">Zapoznaj się z kolekcji właściwości kontekstu standardowe [konfiguracji](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span><span class="sxs-lookup"><span data-stu-id="6a5d1-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
