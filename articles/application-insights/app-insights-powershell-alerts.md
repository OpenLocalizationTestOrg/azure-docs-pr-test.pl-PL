---
title: "aaaUse Powershell tooset alertów w usłudze Application Insights | Dokumentacja firmy Microsoft"
description: "Zautomatyzować konfigurację usługi Application Insights tooget powiadomienia dotyczące zmiany metryki."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a><span data-ttu-id="8fb32-103">Użyj programu PowerShell tooset alertów w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="8fb32-103">Use PowerShell tooset alerts in Application Insights</span></span>
<span data-ttu-id="8fb32-104">Można zautomatyzować konfigurację hello [alerty](app-insights-alerts.md) w [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8fb32-104">You can automate hello configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="8fb32-105">Ponadto można [ustawić tooautomate elementów webhook alertu tooan odpowiedzi](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8fb32-105">In addition, you can [set webhooks tooautomate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8fb32-106">Jeśli chcesz toocreate zasobów i alerty o hello takie same czasu, należy wziąć pod uwagę [przy użyciu szablonu usługi Azure Resource Manager](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8fb32-106">If you want toocreate resources and alerts at hello same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="8fb32-107">Jednorazowej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="8fb32-107">One-time setup</span></span>
<span data-ttu-id="8fb32-108">Jeśli nie użyto programu PowerShell z subskrypcją platformy Azure przed:</span><span class="sxs-lookup"><span data-stu-id="8fb32-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="8fb32-109">Instalowanie modułu Azure Powershell hello na maszynie hello miejscu toorun hello skryptów.</span><span class="sxs-lookup"><span data-stu-id="8fb32-109">Install hello Azure Powershell module on hello machine where you want toorun hello scripts.</span></span>

* <span data-ttu-id="8fb32-110">Zainstaluj [Instalatora platformy sieci Web firmy Microsoft (w wersji 5 lub nowszej)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fb32-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="8fb32-111">Użyj go tooinstall Microsoft Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="8fb32-111">Use it tooinstall Microsoft Azure Powershell</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="8fb32-112">Połącz tooAzure</span><span class="sxs-lookup"><span data-stu-id="8fb32-112">Connect tooAzure</span></span>
<span data-ttu-id="8fb32-113">Uruchom program Azure PowerShell i [połączenia subskrypcji tooyour](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="8fb32-113">Start Azure PowerShell and [connect tooyour subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="8fb32-114">Uzyskiwanie alertów</span><span class="sxs-lookup"><span data-stu-id="8fb32-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="8fb32-115">Dodawanie alertu</span><span class="sxs-lookup"><span data-stu-id="8fb32-115">Add alert</span></span>
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a><span data-ttu-id="8fb32-116">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="8fb32-116">Example 1</span></span>
<span data-ttu-id="8fb32-117">Wyślij mi wiadomość e-mail, jeśli żądania tooHTTP odpowiedzi serwera hello, średnio ponad 5 minut, jest mniejsza niż 1 sekunda.</span><span class="sxs-lookup"><span data-stu-id="8fb32-117">Email me if hello server's response tooHTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="8fb32-118">Moje zasobu usługi Application Insights jest nazywany IceCreamWebApp i jest w grupie zasobów firmy Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="8fb32-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="8fb32-119">Jestem właścicielem hello hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fb32-119">I am hello owner of hello Azure subscription.</span></span>

<span data-ttu-id="8fb32-120">Witaj identyfikator GUID jest Identyfikatorem subskrypcji hello (nie hello klucza instrumentacji aplikacji hello).</span><span class="sxs-lookup"><span data-stu-id="8fb32-120">hello GUID is hello subscription ID (not hello instrumentation key of hello application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="8fb32-121">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="8fb32-121">Example 2</span></span>
<span data-ttu-id="8fb32-122">Używana aplikacja, I użyj [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport metrykę o nazwie "salesPerHour."</span><span class="sxs-lookup"><span data-stu-id="8fb32-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport a metric named "salesPerHour."</span></span> <span data-ttu-id="8fb32-123">Wyślij wiadomość e-mail toomy współpracowników, jeśli "salesPerHour" spadnie poniżej 100, średnio ponad 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="8fb32-123">Send an email toomy colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

<span data-ttu-id="8fb32-124">zasada może służyć do Metryka hello Hello zgłosił za pomocą hello [parametru pomiaru](app-insights-api-custom-events-metrics.md#properties) wywołania innego śledzenia, takie jak TrackEvent lub trackPageView.</span><span class="sxs-lookup"><span data-stu-id="8fb32-124">hello same rule can be used for hello metric reported by using hello [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="8fb32-125">Nazwy metryki</span><span class="sxs-lookup"><span data-stu-id="8fb32-125">Metric names</span></span>
| <span data-ttu-id="8fb32-126">Nazwa metryki</span><span class="sxs-lookup"><span data-stu-id="8fb32-126">Metric name</span></span> | <span data-ttu-id="8fb32-127">Nazwa ekranu</span><span class="sxs-lookup"><span data-stu-id="8fb32-127">Screen name</span></span> | <span data-ttu-id="8fb32-128">Opis</span><span class="sxs-lookup"><span data-stu-id="8fb32-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="8fb32-129">Wyjątki przeglądarki</span><span class="sxs-lookup"><span data-stu-id="8fb32-129">Browser exceptions</span></span> |<span data-ttu-id="8fb32-130">Liczba nieprzechwyconych wyjątków zgłoszonych w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="8fb32-130">Count of uncaught exceptions thrown in hello browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="8fb32-131">Wyjątki serwera</span><span class="sxs-lookup"><span data-stu-id="8fb32-131">Server exceptions</span></span> |<span data-ttu-id="8fb32-132">Liczba nieobsługiwanych wyjątków zgłoszonych przez aplikację hello</span><span class="sxs-lookup"><span data-stu-id="8fb32-132">Count of unhandled exceptions thrown by hello app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="8fb32-133">Czas przetwarzania klienta</span><span class="sxs-lookup"><span data-stu-id="8fb32-133">Client processing time</span></span> |<span data-ttu-id="8fb32-134">Czas między odebraniem ostatniego bajtu hello dokumentu do momentu załadowania modelu DOM hello.</span><span class="sxs-lookup"><span data-stu-id="8fb32-134">Time between receiving hello last byte of a document until hello DOM is loaded.</span></span> <span data-ttu-id="8fb32-135">Żądania asynchroniczne mogą nadal być przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="8fb32-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="8fb32-136">Czas połączenia sieciowego podczas ładowania strony</span><span class="sxs-lookup"><span data-stu-id="8fb32-136">Page load network connect time</span></span> |<span data-ttu-id="8fb32-137">Czas hello przeglądarki przyjmuje tooconnect toohello sieci.</span><span class="sxs-lookup"><span data-stu-id="8fb32-137">Time hello browser takes tooconnect toohello network.</span></span> <span data-ttu-id="8fb32-138">Może być równa 0, jeśli w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="8fb32-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="8fb32-139">Odbieranie czas odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8fb32-139">Receiving response time</span></span> |<span data-ttu-id="8fb32-140">Czas między przeglądarki wysyłania żądania toostarting tooreceive odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="8fb32-140">Time between browser sending request toostarting tooreceive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="8fb32-141">Wyślij czas żądania</span><span class="sxs-lookup"><span data-stu-id="8fb32-141">Send request time</span></span> |<span data-ttu-id="8fb32-142">Czas trwania żądania toosend przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="8fb32-142">Time taken by browser toosend request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="8fb32-143">Czas ładowania strony przeglądarki</span><span class="sxs-lookup"><span data-stu-id="8fb32-143">Browser page load time</span></span> |<span data-ttu-id="8fb32-144">Czas od wysłania żądania użytkownika do modelu DOM, arkuszy stylów, skryptów i obrazów są ładowane.</span><span class="sxs-lookup"><span data-stu-id="8fb32-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="8fb32-145">Dostępna pamięć</span><span class="sxs-lookup"><span data-stu-id="8fb32-145">Available memory</span></span> |<span data-ttu-id="8fb32-146">Pamięć fizyczna dostępna natychmiast dla procesów lub do wykorzystania przez system.</span><span class="sxs-lookup"><span data-stu-id="8fb32-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="8fb32-147">Szybkość przetwarzania We/Wy</span><span class="sxs-lookup"><span data-stu-id="8fb32-147">Process IO Rate</span></span> |<span data-ttu-id="8fb32-148">Całkowita liczba bajtów na drugi odczytu i zapisywane toofiles, sieci i urządzeń.</span><span class="sxs-lookup"><span data-stu-id="8fb32-148">Total bytes per second read and written toofiles, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="8fb32-149">szybkość wyjątku</span><span class="sxs-lookup"><span data-stu-id="8fb32-149">exception rate</span></span> |<span data-ttu-id="8fb32-150">Wyjątków zgłaszanych na sekundę.</span><span class="sxs-lookup"><span data-stu-id="8fb32-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="8fb32-151">Proces Procesora</span><span class="sxs-lookup"><span data-stu-id="8fb32-151">Process CPU</span></span> |<span data-ttu-id="8fb32-152">Procent Hello wszystkich wątków procesów używanych przez hello procesora tooexecution instrukcje dla procesu aplikacji hello czas, który upłynął.</span><span class="sxs-lookup"><span data-stu-id="8fb32-152">hello percentage of elapsed time of all process threads used by hello processor tooexecution instructions for hello applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="8fb32-153">Czas procesora</span><span class="sxs-lookup"><span data-stu-id="8fb32-153">Processor time</span></span> |<span data-ttu-id="8fb32-154">Hello wartość procentową czasu hello procesor spędza w Aktywne wątki.</span><span class="sxs-lookup"><span data-stu-id="8fb32-154">hello percentage of time that hello processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="8fb32-155">Bajtów prywatnych procesu</span><span class="sxs-lookup"><span data-stu-id="8fb32-155">Process private bytes</span></span> |<span data-ttu-id="8fb32-156">Pamięć przypisana wyłącznie toohello monitorowane procesów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8fb32-156">Memory exclusively assigned toohello monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="8fb32-157">Czas wykonania żądania programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8fb32-157">ASP.NET request execution time</span></span> |<span data-ttu-id="8fb32-158">Czas wykonywania hello ostatniego żądania.</span><span class="sxs-lookup"><span data-stu-id="8fb32-158">Execution time of hello most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="8fb32-159">ASP.NET żądań w kolejce wykonywania</span><span class="sxs-lookup"><span data-stu-id="8fb32-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="8fb32-160">Długość kolejki żądań aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8fb32-160">Length of hello application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="8fb32-161">Współczynnik żądań ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8fb32-161">ASP.NET request rate</span></span> |<span data-ttu-id="8fb32-162">Częstotliwość wszystkich żądań aplikacji toohello na sekundę z platformy ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8fb32-162">Rate of all requests toohello application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="8fb32-163">Błędy zależności</span><span class="sxs-lookup"><span data-stu-id="8fb32-163">Dependency failures</span></span> |<span data-ttu-id="8fb32-164">Liczba nieudanych wywołań powitania serwera aplikacji tooexternal zasobów.</span><span class="sxs-lookup"><span data-stu-id="8fb32-164">Count of failed calls made by hello server application tooexternal resources.</span></span> |
| `request.duration` |<span data-ttu-id="8fb32-165">Czas odpowiedzi serwera</span><span class="sxs-lookup"><span data-stu-id="8fb32-165">Server response time</span></span> |<span data-ttu-id="8fb32-166">Czas między odebraniem żądania HTTP i zakończeniem wysyłania odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="8fb32-166">Time between receiving an HTTP request and finishing sending hello response.</span></span> |
| `request.rate` |<span data-ttu-id="8fb32-167">Współczynnik żądań</span><span class="sxs-lookup"><span data-stu-id="8fb32-167">Request rate</span></span> |<span data-ttu-id="8fb32-168">Częstotliwość wszystkich żądań aplikacji toohello na sekundę.</span><span class="sxs-lookup"><span data-stu-id="8fb32-168">Rate of all requests toohello application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="8fb32-169">Żądań zakończonych niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="8fb32-169">Failed requests</span></span> |<span data-ttu-id="8fb32-170">Liczba żądań HTTP które wywołały kod odpowiedzi > = 400</span><span class="sxs-lookup"><span data-stu-id="8fb32-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="8fb32-171">Liczba wyświetleń strony</span><span class="sxs-lookup"><span data-stu-id="8fb32-171">Page views</span></span> |<span data-ttu-id="8fb32-172">Liczba żądań użytkowników klientów dla strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="8fb32-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="8fb32-173">Ruchu syntetycznego jest odfiltrowana.</span><span class="sxs-lookup"><span data-stu-id="8fb32-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="8fb32-174">{niestandardowe metryki nazwę}</span><span class="sxs-lookup"><span data-stu-id="8fb32-174">{your custom metric name}</span></span> |<span data-ttu-id="8fb32-175">{Nazwa metryki}</span><span class="sxs-lookup"><span data-stu-id="8fb32-175">{Your metric name}</span></span> |<span data-ttu-id="8fb32-176">Wartość metryki zgłoszone przez [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) lub hello [pomiarów parametru wywołania śledzenia](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="8fb32-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in hello [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="8fb32-177">metryki Hello są wysyłane przez moduły różnych telemetrii:</span><span class="sxs-lookup"><span data-stu-id="8fb32-177">hello metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="8fb32-178">Metryki grupy</span><span class="sxs-lookup"><span data-stu-id="8fb32-178">Metric group</span></span> | <span data-ttu-id="8fb32-179">Moduł zbierający</span><span class="sxs-lookup"><span data-stu-id="8fb32-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="8fb32-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="8fb32-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="8fb32-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="8fb32-181">clientPerformance,</span></span><br/><span data-ttu-id="8fb32-182">wyświetl</span><span class="sxs-lookup"><span data-stu-id="8fb32-182">view</span></span> |[<span data-ttu-id="8fb32-183">Kod JavaScript przeglądarki</span><span class="sxs-lookup"><span data-stu-id="8fb32-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="8fb32-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="8fb32-184">performanceCounter</span></span> |[<span data-ttu-id="8fb32-185">Wydajność</span><span class="sxs-lookup"><span data-stu-id="8fb32-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="8fb32-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="8fb32-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="8fb32-187">Zależność</span><span class="sxs-lookup"><span data-stu-id="8fb32-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="8fb32-188">żądanie,</span><span class="sxs-lookup"><span data-stu-id="8fb32-188">request,</span></span><br/><span data-ttu-id="8fb32-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="8fb32-189">requestFailed</span></span> |[<span data-ttu-id="8fb32-190">Żądanie serwera</span><span class="sxs-lookup"><span data-stu-id="8fb32-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="8fb32-191">elementów webhook</span><span class="sxs-lookup"><span data-stu-id="8fb32-191">Webhooks</span></span>
<span data-ttu-id="8fb32-192">Możesz [zautomatyzować alertu tooan odpowiedzi](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8fb32-192">You can [automate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="8fb32-193">Azure będzie wywoływać adres sieci web wybranych przez użytkownika, gdy zostanie zgłoszony alert.</span><span class="sxs-lookup"><span data-stu-id="8fb32-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="8fb32-194">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="8fb32-194">See also</span></span>
* [<span data-ttu-id="8fb32-195">Skrypt tooconfigure usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="8fb32-195">Script tooconfigure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="8fb32-196">Tworzenie usługi Application Insights i zasobów testu sieci web za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="8fb32-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="8fb32-197">Automatyzowanie sprzężenia Insights tooApplication Diagnostyka pakietu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8fb32-197">Automate coupling Microsoft Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="8fb32-198">Automatyzowanie alertu tooan odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="8fb32-198">Automate your response tooan alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
