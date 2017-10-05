---
title: "Ustawianie alertów w usłudze Application Insights przy użyciu programu Powershell | Dokumentacja firmy Microsoft"
description: "Zautomatyzować konfigurację Application Insights, aby otrzymywać wiadomości e-mail o zmianach metryki."
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
ms.openlocfilehash: 64675c51abf80daa3a55220f910aa8fdee1042ca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-set-alerts-in-application-insights"></a><span data-ttu-id="11dbd-103">Ustawianie alertów w usłudze Application Insights przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="11dbd-103">Use PowerShell to set alerts in Application Insights</span></span>
<span data-ttu-id="11dbd-104">Można zautomatyzować konfigurowanie [alerty](app-insights-alerts.md) w [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11dbd-104">You can automate the configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="11dbd-105">Ponadto można [Ustaw elementów webhook można zautomatyzować Twojej odpowiedzi na alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="11dbd-105">In addition, you can [set webhooks to automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="11dbd-106">Jeśli chcesz utworzyć zasobów i alertów w tym samym czasie, należy wziąć pod uwagę [przy użyciu szablonu usługi Azure Resource Manager](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="11dbd-106">If you want to create resources and alerts at the same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="11dbd-107">Jednorazowej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="11dbd-107">One-time setup</span></span>
<span data-ttu-id="11dbd-108">Jeśli nie użyto programu PowerShell z subskrypcją platformy Azure przed:</span><span class="sxs-lookup"><span data-stu-id="11dbd-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="11dbd-109">Zainstaluj moduł Azure Powershell na komputerze, na którym chcesz uruchomić skrypty.</span><span class="sxs-lookup"><span data-stu-id="11dbd-109">Install the Azure Powershell module on the machine where you want to run the scripts.</span></span>

* <span data-ttu-id="11dbd-110">Zainstaluj [Instalatora platformy sieci Web firmy Microsoft (w wersji 5 lub nowszej)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="11dbd-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="11dbd-111">Użyć go do zainstalowania programu Microsoft Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="11dbd-111">Use it to install Microsoft Azure Powershell</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="11dbd-112">Nawiązywanie połączenia z usługą Azure</span><span class="sxs-lookup"><span data-stu-id="11dbd-112">Connect to Azure</span></span>
<span data-ttu-id="11dbd-113">Uruchom program Azure PowerShell i [nawiązać połączenia z subskrypcją](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="11dbd-113">Start Azure PowerShell and [connect to your subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="11dbd-114">Uzyskiwanie alertów</span><span class="sxs-lookup"><span data-stu-id="11dbd-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="11dbd-115">Dodawanie alertu</span><span class="sxs-lookup"><span data-stu-id="11dbd-115">Add alert</span></span>
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



## <a name="example-1"></a><span data-ttu-id="11dbd-116">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="11dbd-116">Example 1</span></span>
<span data-ttu-id="11dbd-117">Wyślij mi wiadomość e-mail, jeśli odpowiedzi serwera na żądania HTTP, średnio ponad 5 minut, jest mniejsza niż 1 sekunda.</span><span class="sxs-lookup"><span data-stu-id="11dbd-117">Email me if the server's response to HTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="11dbd-118">Moje zasobu usługi Application Insights jest nazywany IceCreamWebApp i jest w grupie zasobów firmy Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="11dbd-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="11dbd-119">Jestem właścicielem subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="11dbd-119">I am the owner of the Azure subscription.</span></span>

<span data-ttu-id="11dbd-120">Identyfikator GUID jest Identyfikatorem subskrypcji (nie klucza instrumentacji aplikacji).</span><span class="sxs-lookup"><span data-stu-id="11dbd-120">The GUID is the subscription ID (not the instrumentation key of the application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if the server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="11dbd-121">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="11dbd-121">Example 2</span></span>
<span data-ttu-id="11dbd-122">Używana aplikacja, I użyj [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) zgłoszenia metrykę o nazwie "salesPerHour."</span><span class="sxs-lookup"><span data-stu-id="11dbd-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to report a metric named "salesPerHour."</span></span> <span data-ttu-id="11dbd-123">Wyślij wiadomość e-mail do moich współpracowników, gdy "salesPerHour" spada poniżej 100, średnio ponad 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="11dbd-123">Send an email to my colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

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

<span data-ttu-id="11dbd-124">Ta zasada może służyć do metryki zgłoszone za pomocą [parametru pomiaru](app-insights-api-custom-events-metrics.md#properties) wywołania innego śledzenia, takie jak TrackEvent lub trackPageView.</span><span class="sxs-lookup"><span data-stu-id="11dbd-124">The same rule can be used for the metric reported by using the [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="11dbd-125">Nazwy metryki</span><span class="sxs-lookup"><span data-stu-id="11dbd-125">Metric names</span></span>
| <span data-ttu-id="11dbd-126">Nazwa metryki</span><span class="sxs-lookup"><span data-stu-id="11dbd-126">Metric name</span></span> | <span data-ttu-id="11dbd-127">Nazwa ekranu</span><span class="sxs-lookup"><span data-stu-id="11dbd-127">Screen name</span></span> | <span data-ttu-id="11dbd-128">Opis</span><span class="sxs-lookup"><span data-stu-id="11dbd-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="11dbd-129">Wyjątki przeglądarki</span><span class="sxs-lookup"><span data-stu-id="11dbd-129">Browser exceptions</span></span> |<span data-ttu-id="11dbd-130">Liczba nieprzechwyconych wyjątków zgłoszonych w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="11dbd-130">Count of uncaught exceptions thrown in the browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="11dbd-131">Wyjątki serwera</span><span class="sxs-lookup"><span data-stu-id="11dbd-131">Server exceptions</span></span> |<span data-ttu-id="11dbd-132">Liczba nieobsługiwanych wyjątków zgłoszonych przez aplikację</span><span class="sxs-lookup"><span data-stu-id="11dbd-132">Count of unhandled exceptions thrown by the app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="11dbd-133">Czas przetwarzania klienta</span><span class="sxs-lookup"><span data-stu-id="11dbd-133">Client processing time</span></span> |<span data-ttu-id="11dbd-134">Czas między odebraniem ostatniego bajtu dokumentu do momentu załadowania modelu DOM.</span><span class="sxs-lookup"><span data-stu-id="11dbd-134">Time between receiving the last byte of a document until the DOM is loaded.</span></span> <span data-ttu-id="11dbd-135">Żądania asynchroniczne mogą nadal być przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="11dbd-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="11dbd-136">Czas połączenia sieciowego podczas ładowania strony</span><span class="sxs-lookup"><span data-stu-id="11dbd-136">Page load network connect time</span></span> |<span data-ttu-id="11dbd-137">Czas przeglądarki do nawiązania połączenia z siecią.</span><span class="sxs-lookup"><span data-stu-id="11dbd-137">Time the browser takes to connect to the network.</span></span> <span data-ttu-id="11dbd-138">Może być równa 0, jeśli w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="11dbd-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="11dbd-139">Odbieranie czas odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="11dbd-139">Receiving response time</span></span> |<span data-ttu-id="11dbd-140">Czas między przeglądarki, wysyłając żądanie do uruchamiania odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="11dbd-140">Time between browser sending request to starting to receive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="11dbd-141">Wyślij czas żądania</span><span class="sxs-lookup"><span data-stu-id="11dbd-141">Send request time</span></span> |<span data-ttu-id="11dbd-142">Czas trwania przeglądarki można wysłać żądania.</span><span class="sxs-lookup"><span data-stu-id="11dbd-142">Time taken by browser to send request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="11dbd-143">Czas ładowania strony przeglądarki</span><span class="sxs-lookup"><span data-stu-id="11dbd-143">Browser page load time</span></span> |<span data-ttu-id="11dbd-144">Czas od wysłania żądania użytkownika do modelu DOM, arkuszy stylów, skryptów i obrazów są ładowane.</span><span class="sxs-lookup"><span data-stu-id="11dbd-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="11dbd-145">Dostępna pamięć</span><span class="sxs-lookup"><span data-stu-id="11dbd-145">Available memory</span></span> |<span data-ttu-id="11dbd-146">Pamięć fizyczna dostępna natychmiast dla procesów lub do wykorzystania przez system.</span><span class="sxs-lookup"><span data-stu-id="11dbd-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="11dbd-147">Szybkość przetwarzania We/Wy</span><span class="sxs-lookup"><span data-stu-id="11dbd-147">Process IO Rate</span></span> |<span data-ttu-id="11dbd-148">Całkowita liczba bajtów na sekundę, Odczyt i zapis do plików, sieci i urządzeń.</span><span class="sxs-lookup"><span data-stu-id="11dbd-148">Total bytes per second read and written to files, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="11dbd-149">szybkość wyjątku</span><span class="sxs-lookup"><span data-stu-id="11dbd-149">exception rate</span></span> |<span data-ttu-id="11dbd-150">Wyjątków zgłaszanych na sekundę.</span><span class="sxs-lookup"><span data-stu-id="11dbd-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="11dbd-151">Proces Procesora</span><span class="sxs-lookup"><span data-stu-id="11dbd-151">Process CPU</span></span> |<span data-ttu-id="11dbd-152">Procent czasu wykonywania wszystkich wątków procesów używanych przez procesor do wykonywania instrukcji dla procesu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11dbd-152">The percentage of elapsed time of all process threads used by the processor to execution instructions for the applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="11dbd-153">Czas procesora</span><span class="sxs-lookup"><span data-stu-id="11dbd-153">Processor time</span></span> |<span data-ttu-id="11dbd-154">Procent czasu, jaki procesor zużywa w Aktywne wątki.</span><span class="sxs-lookup"><span data-stu-id="11dbd-154">The percentage of time that the processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="11dbd-155">Bajtów prywatnych procesu</span><span class="sxs-lookup"><span data-stu-id="11dbd-155">Process private bytes</span></span> |<span data-ttu-id="11dbd-156">Pamięć przypisana wyłącznie do procesów monitorowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11dbd-156">Memory exclusively assigned to the monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="11dbd-157">Czas wykonania żądania programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="11dbd-157">ASP.NET request execution time</span></span> |<span data-ttu-id="11dbd-158">Czas wykonania ostatniego żądania.</span><span class="sxs-lookup"><span data-stu-id="11dbd-158">Execution time of the most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="11dbd-159">ASP.NET żądań w kolejce wykonywania</span><span class="sxs-lookup"><span data-stu-id="11dbd-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="11dbd-160">Długość kolejki żądań aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11dbd-160">Length of the application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="11dbd-161">Współczynnik żądań ASP.NET</span><span class="sxs-lookup"><span data-stu-id="11dbd-161">ASP.NET request rate</span></span> |<span data-ttu-id="11dbd-162">Częstotliwość wszystkich żądań do aplikacji w ciągu sekundy z platformy ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="11dbd-162">Rate of all requests to the application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="11dbd-163">Błędy zależności</span><span class="sxs-lookup"><span data-stu-id="11dbd-163">Dependency failures</span></span> |<span data-ttu-id="11dbd-164">Liczba nieudanych wywołań zasobów zewnętrznych aplikacji serwera.</span><span class="sxs-lookup"><span data-stu-id="11dbd-164">Count of failed calls made by the server application to external resources.</span></span> |
| `request.duration` |<span data-ttu-id="11dbd-165">Czas odpowiedzi serwera</span><span class="sxs-lookup"><span data-stu-id="11dbd-165">Server response time</span></span> |<span data-ttu-id="11dbd-166">Czas między odebraniem żądania HTTP i zakończeniem wysyłania odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="11dbd-166">Time between receiving an HTTP request and finishing sending the response.</span></span> |
| `request.rate` |<span data-ttu-id="11dbd-167">Współczynnik żądań</span><span class="sxs-lookup"><span data-stu-id="11dbd-167">Request rate</span></span> |<span data-ttu-id="11dbd-168">Częstotliwość wszystkich żądań do aplikacji na sekundę.</span><span class="sxs-lookup"><span data-stu-id="11dbd-168">Rate of all requests to the application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="11dbd-169">Żądań zakończonych niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="11dbd-169">Failed requests</span></span> |<span data-ttu-id="11dbd-170">Liczba żądań HTTP które wywołały kod odpowiedzi > = 400</span><span class="sxs-lookup"><span data-stu-id="11dbd-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="11dbd-171">Liczba wyświetleń strony</span><span class="sxs-lookup"><span data-stu-id="11dbd-171">Page views</span></span> |<span data-ttu-id="11dbd-172">Liczba żądań użytkowników klientów dla strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="11dbd-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="11dbd-173">Ruchu syntetycznego jest odfiltrowana.</span><span class="sxs-lookup"><span data-stu-id="11dbd-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="11dbd-174">{niestandardowe metryki nazwę}</span><span class="sxs-lookup"><span data-stu-id="11dbd-174">{your custom metric name}</span></span> |<span data-ttu-id="11dbd-175">{Nazwa metryki}</span><span class="sxs-lookup"><span data-stu-id="11dbd-175">{Your metric name}</span></span> |<span data-ttu-id="11dbd-176">Wartość metryki zgłoszone przez [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) lub [pomiarów parametru wywołania śledzenia](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="11dbd-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in the [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="11dbd-177">Metryki są przesyłane przez różnych telemetrii moduły:</span><span class="sxs-lookup"><span data-stu-id="11dbd-177">The metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="11dbd-178">Metryki grupy</span><span class="sxs-lookup"><span data-stu-id="11dbd-178">Metric group</span></span> | <span data-ttu-id="11dbd-179">Moduł zbierający</span><span class="sxs-lookup"><span data-stu-id="11dbd-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="11dbd-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="11dbd-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="11dbd-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="11dbd-181">clientPerformance,</span></span><br/><span data-ttu-id="11dbd-182">wyświetl</span><span class="sxs-lookup"><span data-stu-id="11dbd-182">view</span></span> |[<span data-ttu-id="11dbd-183">Kod JavaScript przeglądarki</span><span class="sxs-lookup"><span data-stu-id="11dbd-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="11dbd-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="11dbd-184">performanceCounter</span></span> |[<span data-ttu-id="11dbd-185">Wydajność</span><span class="sxs-lookup"><span data-stu-id="11dbd-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="11dbd-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="11dbd-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="11dbd-187">Zależność</span><span class="sxs-lookup"><span data-stu-id="11dbd-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="11dbd-188">żądanie,</span><span class="sxs-lookup"><span data-stu-id="11dbd-188">request,</span></span><br/><span data-ttu-id="11dbd-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="11dbd-189">requestFailed</span></span> |[<span data-ttu-id="11dbd-190">Żądanie serwera</span><span class="sxs-lookup"><span data-stu-id="11dbd-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="11dbd-191">elementów webhook</span><span class="sxs-lookup"><span data-stu-id="11dbd-191">Webhooks</span></span>
<span data-ttu-id="11dbd-192">Możesz [zautomatyzować Twojej odpowiedzi na alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="11dbd-192">You can [automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="11dbd-193">Azure będzie wywoływać adres sieci web wybranych przez użytkownika, gdy zostanie zgłoszony alert.</span><span class="sxs-lookup"><span data-stu-id="11dbd-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="11dbd-194">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="11dbd-194">See also</span></span>
* [<span data-ttu-id="11dbd-195">Skrypt w celu skonfigurowania usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="11dbd-195">Script to configure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="11dbd-196">Tworzenie usługi Application Insights i zasobów testu sieci web za pomocą szablonów</span><span class="sxs-lookup"><span data-stu-id="11dbd-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="11dbd-197">Automatyzowanie sprzężenia Diagnostyka pakietu Microsoft Azure do usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="11dbd-197">Automate coupling Microsoft Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="11dbd-198">Twoje odpowiedzi na alert automatyzacji</span><span class="sxs-lookup"><span data-stu-id="11dbd-198">Automate your response to an alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
