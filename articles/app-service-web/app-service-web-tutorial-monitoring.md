---
title: Monitorowanie aplikacji sieci Web | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak skonfigurować monitorowanie w aplikacji sieci Web"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="e153a-103">Monitor usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="e153a-103">Monitor App Service</span></span>
<span data-ttu-id="e153a-104">W tym samouczku przedstawiono sposób monitorowania aplikacji i za pomocą narzędzi wbudowanych platformy do rozwiązywania problemów w momencie wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="e153a-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span></span>

<span data-ttu-id="e153a-105">Każdej sekcji tego dokumentu przechodzi przez określoną funkcję.</span><span class="sxs-lookup"><span data-stu-id="e153a-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="e153a-106">Przy użyciu funkcji razem umożliwiają:</span><span class="sxs-lookup"><span data-stu-id="e153a-106">Using the features together let you:</span></span>
- <span data-ttu-id="e153a-107">Identyfikowanie problemu w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="e153a-108">Określanie, kiedy problem spowodowany kodu lub platformy.</span><span class="sxs-lookup"><span data-stu-id="e153a-108">Determining when the issue is caused by your code or the platform.</span></span>
- <span data-ttu-id="e153a-109">Zawęź źródłem problemu w kodzie.</span><span class="sxs-lookup"><span data-stu-id="e153a-109">Narrow down the source of the problem in your code.</span></span>
- <span data-ttu-id="e153a-110">Debugowanie i rozwiązywania problemu.</span><span class="sxs-lookup"><span data-stu-id="e153a-110">Debugging and fixing the issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e153a-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e153a-111">Before you begin</span></span>
- <span data-ttu-id="e153a-112">Należy aplikacji sieci Web w taki sposób, aby monitorować i wykonaj kroki obramowane.</span><span class="sxs-lookup"><span data-stu-id="e153a-112">You need a Web App to monitor and follow the outlined steps.</span></span>
    - <span data-ttu-id="e153a-113">Wykonanie kroków opisanych w aplikacji można utworzyć [tworzenie aplikacji ASP.NET na platformie Azure z bazy danych SQL](app-service-web-tutorial-dotnet-sqldatabase.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="e153a-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="e153a-114">Jeśli chcesz wypróbować **zdalnego debugowania** aplikacji, potrzebujesz programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e153a-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="e153a-115">Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i korzystać z BEZPŁATNEJ [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e153a-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="e153a-116">Podczas instalacji programu Visual Studio upewnij się, że jest włączona opcja **Programowanie na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="e153a-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

## <span data-ttu-id="e153a-117"><a name="metrics"></a>Krok 1 — widok metryk</span><span class="sxs-lookup"><span data-stu-id="e153a-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="e153a-118">**Metryki** są przydatne do zrozumienia:</span><span class="sxs-lookup"><span data-stu-id="e153a-118">**Metrics** are useful to understand:</span></span>
- <span data-ttu-id="e153a-119">Kondycja aplikacji</span><span class="sxs-lookup"><span data-stu-id="e153a-119">Application health</span></span>
- <span data-ttu-id="e153a-120">Wydajność aplikacji</span><span class="sxs-lookup"><span data-stu-id="e153a-120">App performance</span></span>
- <span data-ttu-id="e153a-121">Użycie zasobów</span><span class="sxs-lookup"><span data-stu-id="e153a-121">Resource consumption</span></span>

<span data-ttu-id="e153a-122">Po zbadaniu problemu z aplikacją, przeglądanie metryki jest dobrym miejscem do rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="e153a-122">When investigating an application issue, reviewing metrics is a good place to start.</span></span> <span data-ttu-id="e153a-123">Azure portal ma szybkie wizualnie Sprawdź swoją aplikację przy użyciu metryk **Azure Monitor**.</span><span class="sxs-lookup"><span data-stu-id="e153a-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="e153a-124">Metryki udostępnianie widok historycznych w kilku agregacjach klucza dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="e153a-125">Dla dowolnej aplikacji hostowanej w usłudze app service należy monitorować zarówno aplikacji sieci Web i plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="e153a-126">Plan usługi App Service reprezentuje kolekcję zasobów fizycznych służących do hostowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-126">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="e153a-127">Wszystkie aplikacje przypisane do planu usługi App Service współdzielą zasoby przez niego zdefiniowane, ograniczając koszt hostowania wielu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="e153a-128">Plany usługi App Service definiują następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e153a-128">App Service plans define:</span></span>
> * <span data-ttu-id="e153a-129">Region: Europa Północna, wschodnie stany USA, Azja południowo-wschodnia,... itd.</span><span class="sxs-lookup"><span data-stu-id="e153a-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="e153a-130">Rozmiar wystąpienia: Mały, Średni, duża itp.</span><span class="sxs-lookup"><span data-stu-id="e153a-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="e153a-131">Liczba skali: jedną, dwie lub trzy wystąpienia, itp.</span><span class="sxs-lookup"><span data-stu-id="e153a-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="e153a-132">Jednostka SKU: Wolne Shared Basic, Standard, Premium, itp.</span><span class="sxs-lookup"><span data-stu-id="e153a-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="e153a-133">Aby przejrzeć metryki dla aplikacji sieci Web, przejdź do **omówienie** bloku aplikacji, którą chcesz monitorować.</span><span class="sxs-lookup"><span data-stu-id="e153a-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span></span> <span data-ttu-id="e153a-134">W tym miejscu można wyświetlić wykresu dla metryki aplikacji jako **Kafelek monitorowanie**.</span><span class="sxs-lookup"><span data-stu-id="e153a-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="e153a-135">Kliknij Kafelek, aby edytowanie i konfigurowanie jakie metryk umożliwiają wyświetlenie i zakres czasu do wyświetlenia.</span><span class="sxs-lookup"><span data-stu-id="e153a-135">Click the tile to edit and configure what metrics to view and the time range to display.</span></span>

<span data-ttu-id="e153a-136">Domyślnie bloku zasobów zawiera widok dla żądań aplikacji i błędy w ciągu ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="e153a-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span></span>
<span data-ttu-id="e153a-137">![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="e153a-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="e153a-138">Jak widać w tym przykładzie mamy aplikacji, która generuje wiele **błędy serwera HTTP**.</span><span class="sxs-lookup"><span data-stu-id="e153a-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="e153a-139">Duża liczba błędów jest pierwsze wskazanie potrzebne w celu zbadania tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-139">The high volume of errors is the first indication we need to investigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="e153a-140">Więcej informacji na temat Monitora Azure z następujących łączy:</span><span class="sxs-lookup"><span data-stu-id="e153a-140">Learn more about Azure Monitor with the following links:</span></span>
> - [<span data-ttu-id="e153a-141">Rozpoczynanie pracy z monitorem Azure</span><span class="sxs-lookup"><span data-stu-id="e153a-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="e153a-142">Metryki Azure</span><span class="sxs-lookup"><span data-stu-id="e153a-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="e153a-143">Obsługiwane metryki z monitorem Azure</span><span class="sxs-lookup"><span data-stu-id="e153a-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="e153a-144">Azure pulpity nawigacyjne</span><span class="sxs-lookup"><span data-stu-id="e153a-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="e153a-145"><a name="alerts"></a>Krok 2 — Konfigurowanie alertów</span><span class="sxs-lookup"><span data-stu-id="e153a-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="e153a-146">**Alerty** można skonfigurować do wyzwalania określonych warunków dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-146">**Alerts** can be configured to trigger on specific conditions for your app.</span></span>

<span data-ttu-id="e153a-147">W [krok 1 — widok metryki](#metrics), widzieliśmy, że aplikacja będzie miała dużą liczbę błędów.</span><span class="sxs-lookup"><span data-stu-id="e153a-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span></span>

<span data-ttu-id="e153a-148">Umożliwia konfigurowanie alert, aby automatycznie Otrzymuj powiadomienia w przypadku błędów.</span><span class="sxs-lookup"><span data-stu-id="e153a-148">Lets configure an alert to automatically get notified when errors occur.</span></span> <span data-ttu-id="e153a-149">W takim przypadku chcemy alert do wysyłania i wiadomości e-mail za każdym razem, gdy liczba błędów HTTP 50 X przechodzi przez określony próg.</span><span class="sxs-lookup"><span data-stu-id="e153a-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="e153a-150">Aby utworzyć alert, przejdź do **monitorowanie** > **alerty** i kliknij przycisk **[+] Dodaj Alert**.</span><span class="sxs-lookup"><span data-stu-id="e153a-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Alerty](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="e153a-152">Podaj wartości w konfiguracji alertu:</span><span class="sxs-lookup"><span data-stu-id="e153a-152">Provide values for the Alert configuration:</span></span>
- <span data-ttu-id="e153a-153">**Zasób:** lokacji do monitorowania z alertem.</span><span class="sxs-lookup"><span data-stu-id="e153a-153">**Resource:** The site to monitor with the alert.</span></span>
- <span data-ttu-id="e153a-154">**Nazwa:** nazwę alertu, w tym przypadku: *wysokiej HTTP 50 X*.</span><span class="sxs-lookup"><span data-stu-id="e153a-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="e153a-155">**Opis:** wyjaśnienie ten alert spojrzenie na zwykły tekst.</span><span class="sxs-lookup"><span data-stu-id="e153a-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="e153a-156">**Alert dotyczący:** alerty można przeglądać metryki lub zdarzeń, w tym przykładzie czekamy na metryki.</span><span class="sxs-lookup"><span data-stu-id="e153a-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="e153a-157">**Metryka:** jakie Metryka do monitorowania, w tym przypadku: *błędy serwera HTTP*.</span><span class="sxs-lookup"><span data-stu-id="e153a-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="e153a-158">**Warunek:** kiedy alertu, w tym przypadku wybierz *większe* opcji.</span><span class="sxs-lookup"><span data-stu-id="e153a-158">**Condition:** When to alert, in this case select the *greater than* option.</span></span>
- <span data-ttu-id="e153a-159">**Próg:** co to jest wartość do wyszukania w takim przypadku: *400*.</span><span class="sxs-lookup"><span data-stu-id="e153a-159">**Threshold:** What is value to look for, in this case: *400*.</span></span>
- <span data-ttu-id="e153a-160">**Okres:** alerty działają na średnia wartość metryki.</span><span class="sxs-lookup"><span data-stu-id="e153a-160">**Period:** Alerts operate over the average value of a metric.</span></span> <span data-ttu-id="e153a-161">Mniejsze okresów uzyskanie bardziej poufnego alerty.</span><span class="sxs-lookup"><span data-stu-id="e153a-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="e153a-162">w takim przypadku czekamy na *5 minut*.</span><span class="sxs-lookup"><span data-stu-id="e153a-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="e153a-163">**Wyślij wiadomość e-mail właściciele i Współautorzy:** w takim przypadku: *włączone*.</span><span class="sxs-lookup"><span data-stu-id="e153a-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="e153a-164">Teraz, gdy alert jest tworzony za każdym razem, gdy aplikacja przechodzi przez skonfigurowany próg zostanie wysłana wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="e153a-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span></span> <span data-ttu-id="e153a-165">Aktywne alerty można wyświetlić w taki sposób, w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e153a-165">Active alerts can also be reviewed in the Azure portal.</span></span>

![Wyzwalanie alertów](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="e153a-167">Dowiedz się więcej o alertach Azure z następujących łączy:</span><span class="sxs-lookup"><span data-stu-id="e153a-167">Learn more about Azure Alerts with the following links:</span></span>
> - [<span data-ttu-id="e153a-168">Co to są alerty na platformie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e153a-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="e153a-169">Podejmij działanie metryk</span><span class="sxs-lookup"><span data-stu-id="e153a-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="e153a-170">Tworzenie metryk alertów</span><span class="sxs-lookup"><span data-stu-id="e153a-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="e153a-171"><a name="companion"></a>Krok 3 — Pomocnik usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="e153a-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="e153a-172">**Pomocnik usługi aplikacji** oferuje wygodny sposób monitorowania aplikacji z natywnym środowiskiem urządzenia przenośnego (z systemem iOS lub Android).</span><span class="sxs-lookup"><span data-stu-id="e153a-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="e153a-173">Użyj Pomocnik usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="e153a-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="e153a-174">Przejrzyj metryki aplikacji</span><span class="sxs-lookup"><span data-stu-id="e153a-174">Review application metrics</span></span>
- <span data-ttu-id="e153a-175">Przejrzyj i korzystania z aplikacji, alertów i zalecenia</span><span class="sxs-lookup"><span data-stu-id="e153a-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="e153a-176">Rozwiązywania problemów z podstawowego (Przeglądaj, uruchamianie, zatrzymywanie, ponownie uruchom aplikację)</span><span class="sxs-lookup"><span data-stu-id="e153a-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span></span>
- <span data-ttu-id="e153a-177">Uzyskiwanie powiadomień wypychanych dla zdarzeń krytycznych.</span><span class="sxs-lookup"><span data-stu-id="e153a-177">Get push notifications for critical events.</span></span>

![Pomocnik usługi aplikacji](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="e153a-179">[![Aplikacja usługi pomocnika sklepu](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Google Play pomocniczy usługi aplikacji](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="e153a-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="e153a-180">Pomocnik usługi aplikacji z można zainstalować [sklepu z aplikacjami](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) lub [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="e153a-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="e153a-181"><a name="diagnose"></a>Krok 4 — diagnozowanie i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="e153a-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="e153a-182">**Diagnozowanie i rozwiązywanie problemów** pomaga oddzielić problemy aplikacji tworzą problemy platformy.</span><span class="sxs-lookup"><span data-stu-id="e153a-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="e153a-183">On również zasugerować możliwe ograniczenie jego skutków można pobrać aplikacji sieci Web do dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="e153a-183">It can also suggest possible mitigations to get your Web App back to healthy.</span></span>

![Diagnozowanie i rozwiązywanie problemów](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="e153a-185">Kontynuowaniem przykład formularz poprzednie kroki, zobaczysz, że aplikacja ma zostać problemy dostępności.</span><span class="sxs-lookup"><span data-stu-id="e153a-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span></span> <span data-ttu-id="e153a-186">Natomiast dostępność platformy nie zostały przeniesione od 100%.</span><span class="sxs-lookup"><span data-stu-id="e153a-186">In contrast, the platform availability has not moved from 100%.</span></span>

<span data-ttu-id="e153a-187">Gdy aplikacja ma problem i pozostaje platformy w górę, jest jasne wskazanie, że firma Microsoft ma do czynienia z problemu z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="e153a-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="e153a-188"><a name="logging"></a>Krok 5 — rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="e153a-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="e153a-189">Teraz, gdy będziemy mieć zawęzić błędów, aby problemu z aplikacją, możemy obejrzeć Dzienniki aplikacji i serwera, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span></span>

<span data-ttu-id="e153a-190">Rejestrowanie umożliwia zbieranie zarówno **programu Application Diagnostics** i **diagnostyki serwera sieci Web** dzienników aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e153a-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="e153a-191">Usługa Application Diagnostics</span><span class="sxs-lookup"><span data-stu-id="e153a-191">Application Diagnostics</span></span>
<span data-ttu-id="e153a-192">Diagnostyki aplikacji umożliwia przechwytywanie śladów utworzonego przez aplikację w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="e153a-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span></span>

<span data-ttu-id="e153a-193">Dodawanie, śledzenie, aby aplikacja znacznie zwiększa możliwość debugowania i numer pin punktu problemy.</span><span class="sxs-lookup"><span data-stu-id="e153a-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span></span>

<span data-ttu-id="e153a-194">W programie ASP.NET, możesz zalogować się przy użyciu śladów aplikacji [System.Diagnostics.Trace — klasa](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) generowanie zdarzeń, które są przechwytywane przez infrastrukturę dziennika.</span><span class="sxs-lookup"><span data-stu-id="e153a-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span></span> <span data-ttu-id="e153a-195">Można również określić ważność śledzenia łatwiejsze filtrowania.</span><span class="sxs-lookup"><span data-stu-id="e153a-195">You can also specify the severity of the trace for easier filtering.</span></span>

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
<span data-ttu-id="e153a-196">Aby włączyć rejestrowanie aplikacji przejdź do **monitorowanie** > **dzienników diagnostycznych** i włączyć rejestrowania aplikacji za pomocą przełączników.</span><span class="sxs-lookup"><span data-stu-id="e153a-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span></span>

![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="e153a-198">Dzienniki aplikacji mogą być przechowywane do aplikacji sieci Web systemu plików lub wypchnięty do magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e153a-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span></span> <span data-ttu-id="e153a-199">W scenariuszach produkcyjnym zaleca się używać magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e153a-199">For production scenarios, it's recommended to use blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e153a-200">Włączanie rejestrowania ma wpływ na wykorzystanie wydajności i zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="e153a-201">W scenariuszach produkcji zaleca się w dzienniku błędów.</span><span class="sxs-lookup"><span data-stu-id="e153a-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="e153a-202">Pełniejsze rejestrowanie należy włączyć tylko podczas badania problemów.</span><span class="sxs-lookup"><span data-stu-id="e153a-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="e153a-203">Diagnostyka serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="e153a-203">Web Server Diagnostics</span></span>
<span data-ttu-id="e153a-204">Dzienniki serwera sieci Web są generowane, nawet jeśli aplikacja nie została zinstrumentowana.</span><span class="sxs-lookup"><span data-stu-id="e153a-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="e153a-205">Usługi aplikacji może zbierać trzy różne typy dzienników serwera:</span><span class="sxs-lookup"><span data-stu-id="e153a-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="e153a-206">**Rejestrowanie pracy serwera sieci Web**</span><span class="sxs-lookup"><span data-stu-id="e153a-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="e153a-207">Informacje o transakcjach HTTP przy użyciu [rozszerzonym formacie W3C dziennika pliku](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="e153a-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="e153a-208">Przydatne podczas określania ogólnego metryki lokacji, takie jak liczba żądań obsłużonych lub liczbę żądań pochodzą z określonego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="e153a-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="e153a-209">**Szczegółowe informacje o błędzie logowania**</span><span class="sxs-lookup"><span data-stu-id="e153a-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="e153a-210">Szczegółowe informacje o błędzie kodów stanu HTTP, które wskazania błędu (kod stanu 400 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="e153a-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="e153a-211">Dowiedz się więcej na temat rejestrowania szczegółowe informacje o błędzie</span><span class="sxs-lookup"><span data-stu-id="e153a-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="e153a-212">**Śledzenie niepomyślnych żądań**</span><span class="sxs-lookup"><span data-stu-id="e153a-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="e153a-213">Szczegółowe informacje dotyczące żądań zakończonych niepowodzeniem, w tym śladu używane do przetwarzania żądania oraz godzinę w poszczególnych składników składników usług IIS.</span><span class="sxs-lookup"><span data-stu-id="e153a-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span>
    - <span data-ttu-id="e153a-214">Nie powiodło się żądanie, które dzienniki są przydatne podczas próby izolowania, co powoduje określonego błędu HTTP.</span><span class="sxs-lookup"><span data-stu-id="e153a-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="e153a-215">Dowiedz się więcej na temat śledzenia nieudanych żądań</span><span class="sxs-lookup"><span data-stu-id="e153a-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="e153a-216">Aby włączyć rejestrowanie pracy serwera:</span><span class="sxs-lookup"><span data-stu-id="e153a-216">To enable Server logging:</span></span>
- <span data-ttu-id="e153a-217">Przejdź do **monitorowanie** > **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="e153a-217">go to **Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="e153a-218">Włącz różnego rodzaju diagnostyki serwera sieci Web za pomocą przełączników.</span><span class="sxs-lookup"><span data-stu-id="e153a-218">Enable the different types of Web Server Diagnostics using the toggles.</span></span>

![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="e153a-220">Włączanie rejestrowania ma wpływ na wykorzystanie wydajności i zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="e153a-221">W przypadku scenariuszy produkcji dzienniki błędów są zalecane, włączyć tylko pełniejsze rejestrowanie podczas badania problemów.</span><span class="sxs-lookup"><span data-stu-id="e153a-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="e153a-222">Uzyskiwanie dostępu do dzienników</span><span class="sxs-lookup"><span data-stu-id="e153a-222">Accessing Logs</span></span>
<span data-ttu-id="e153a-223">Dzienników przechowywanych w magazynie obiektów blob są dostępne za pomocą Eksploratora usługi Storage platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e153a-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="e153a-224">Dzienników przechowywanych w aplikacji sieci Web systemu plików są dostępne za pośrednictwem FTP w następujących ścieżkach:</span><span class="sxs-lookup"><span data-stu-id="e153a-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span></span>

- <span data-ttu-id="e153a-225">**Dzienniki aplikacji** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="e153a-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="e153a-226">Ten folder zawiera jeden lub więcej plików tekstowych, zawierający informacje o wygenerowane przez rejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="e153a-227">**Nie powiodło się żądanie śladów** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="e153a-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="e153a-228">Ten folder zawiera plik XSL i co najmniej jeden plik XML.</span><span class="sxs-lookup"><span data-stu-id="e153a-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="e153a-229">**Szczegółowe dzienniki błędów** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="e153a-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="e153a-230">Ten folder zawiera co najmniej jeden plik .htm o wiele informacji dotyczących błędów HTTP wygenerowany przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="e153a-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="e153a-231">**Dzienniki serwera w sieci Web** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="e153a-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="e153a-232">Ten folder zawiera jeden lub więcej plików tekst sformatowany przy użyciu rozszerzonym formacie W3C dziennika pliku.</span><span class="sxs-lookup"><span data-stu-id="e153a-232">This folder contains one or more text files formatted using the W3C extended log file format.</span></span>

## <span data-ttu-id="e153a-233"><a name="streaming"></a>Krok 6 - dzienników przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="e153a-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="e153a-234">Dzienniki przesyłania strumieniowego są wygodne podczas debugowania aplikacji, ponieważ zaoszczędzić czas, w porównaniu do [podczas uzyskiwania dostępu do dzienników](#Accessing-Logs) za pośrednictwem FTP.</span><span class="sxs-lookup"><span data-stu-id="e153a-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="e153a-235">Usługi aplikacji może być przesyłany strumieniowo **Dzienniki aplikacji** i **dzienniki serwera sieci Web** zgodnie z ich wygenerowaniu.</span><span class="sxs-lookup"><span data-stu-id="e153a-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="e153a-236">Przed podjęciem próby strumienia dzienniki, upewnij się, że włączono zbieranie dzienników zgodnie z opisem w [rejestrowanie](#logging) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e153a-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span></span>

<span data-ttu-id="e153a-237">Dzienniki strumieniowo, przejdź do **monitorowanie**> **strumienia dziennika**.</span><span class="sxs-lookup"><span data-stu-id="e153a-237">To stream logs, go to **Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="e153a-238">Wybierz **Dzienniki aplikacji** lub **dzienniki serwera w sieci Web** zależności informacjach szukasz.</span><span class="sxs-lookup"><span data-stu-id="e153a-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="e153a-239">W tym miejscu mogą również wstrzymać, uruchom ponownie i wyczyść bufor.</span><span class="sxs-lookup"><span data-stu-id="e153a-239">From here, you can also pause, restart, and clear the buffer.</span></span>

![Dzienniki przesyłania strumieniowego](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="e153a-241">Dzienniki są generowane tylko, gdy ruchu w aplikacji, można również zwiększyć poziom szczegółowości dzienniki, aby uzyskać więcej zdarzeń lub informacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span></span>

## <span data-ttu-id="e153a-242"><a name="remote"></a>Krok 7. debugowanie zdalne</span><span class="sxs-lookup"><span data-stu-id="e153a-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="e153a-243">Kiedy użytkownik ma numer pin — wskazywanej źródło problemów aplikacji, za pomocą **zdalnego debugowania** przechodzenia przez kod.</span><span class="sxs-lookup"><span data-stu-id="e153a-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span></span>

<span data-ttu-id="e153a-244">Zdalne debugowanie umożliwia możesz dołączyć do aplikacji sieci Web uruchomioną w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e153a-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span></span> <span data-ttu-id="e153a-245">Można ustawić punktów przerwania, manipulowanie nimi pamięci bezpośrednio, krokowo kodu oraz nawet zmienić ścieżkę kodu, podobnie jak w przypadku aplikacji uruchomionej na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="e153a-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span></span>

<span data-ttu-id="e153a-246">Aby dołączyć debuger do aplikacji uruchomionej w chmurze:</span><span class="sxs-lookup"><span data-stu-id="e153a-246">To attach the debugger to your app running in the cloud:</span></span>

- <span data-ttu-id="e153a-247">Za pomocą programu Visual Studio 2017 Otwórz rozwiązanie dla aplikacji, którą chcesz debugować</span><span class="sxs-lookup"><span data-stu-id="e153a-247">Using Visual Studio 2017, open the solution for the app you want to debug</span></span>
- <span data-ttu-id="e153a-248">Ustaw niektórych punktach hamulca, tak jak dla rozwoju lokalnych.</span><span class="sxs-lookup"><span data-stu-id="e153a-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="e153a-249">Otwórz **Eksplorator chmury** (kont. + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="e153a-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="e153a-250">Zaloguj się przy użyciu poświadczeń platformy azure, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="e153a-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="e153a-251">Znajdź aplikację, której chcesz debugować</span><span class="sxs-lookup"><span data-stu-id="e153a-251">Find the app you want to debug</span></span>
- <span data-ttu-id="e153a-252">Wybierz **dołączyć debuger** formularza **akcje** okienka.</span><span class="sxs-lookup"><span data-stu-id="e153a-252">Select **Attach Debugger** form the **Actions** pane.</span></span>

![Debugowanie zdalne](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="e153a-254">Visual Studio konfiguruje aplikację do zdalnego debugowania i uruchamia okno przeglądarki, który nawiguje do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span></span> <span data-ttu-id="e153a-255">Przeglądaj wyzwolenia punktów przerwania i kroku przez kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-255">Browse through your app to trigger break points and step through the code.</span></span>

> [!WARNING]
> <span data-ttu-id="e153a-256">Nie zaleca się uruchamiania w trybie debugowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e153a-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="e153a-257">Dla wielu wystąpień serwera nie jest skalowanie aplikacji produkcyjnych, debugowanie uniemożliwi serwera sieci web odpowiada na żądania innych.</span><span class="sxs-lookup"><span data-stu-id="e153a-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span></span> <span data-ttu-id="e153a-258">Podczas rozwiązywania problemów w środowisku produkcyjnym, jest najlepszym zasobu [skonfigurować rejestrowanie](#logging) i [usługi Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="e153a-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="e153a-259"><a name="explorer"></a>Krok 8 - Eksploratora procesów</span><span class="sxs-lookup"><span data-stu-id="e153a-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="e153a-260">Gdy aplikacja jest skalowana w poziomie do więcej niż jedno wystąpienie **Eksploratora procesów** mogą ułatwić identyfikację wystąpienia określonych problemów.</span><span class="sxs-lookup"><span data-stu-id="e153a-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="e153a-261">Użyj **przetworzyć Explorer** do:</span><span class="sxs-lookup"><span data-stu-id="e153a-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="e153a-262">Wylicza wszystkie procesy w różnych wystąpieniach planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-262">Enumerate all the processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="e153a-263">Przechodzenie i wyświetlić dojścia i moduły skojarzone z każdym procesie.</span><span class="sxs-lookup"><span data-stu-id="e153a-263">Drill down and view the handles and modules associated with each process.</span></span>
- <span data-ttu-id="e153a-264">Wyświetlanie procesora CPU, zestaw roboczy i liczba na poziomie procesu pomoże zidentyfikować wyczerpania procesów wątków</span><span class="sxs-lookup"><span data-stu-id="e153a-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span></span>
- <span data-ttu-id="e153a-265">Znajdź dojść otwartych plików, a nawet kill wystąpienia określonego procesu.</span><span class="sxs-lookup"><span data-stu-id="e153a-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="e153a-266">Eksploratora procesów można znaleźć w **monitorowanie** > **Eksploratora procesów**.</span><span class="sxs-lookup"><span data-stu-id="e153a-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Eksplorator procesów](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="e153a-268"><a name="insights"></a>Krok 9 - usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="e153a-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="e153a-269">**Usługa Application Insights** zapewnia profilowania aplikacji i zaawansowanych możliwości monitorowania dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="e153a-270">Usługa Application Insights umożliwia wykrywanie i diagnozowanie wyjątków i problemy z wydajnością w aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e153a-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="e153a-271">Można włączyć usługi Application Insights dla aplikacji sieci Web, w obszarze **monitorowanie** > **usługi Application Insights**</span><span class="sxs-lookup"><span data-stu-id="e153a-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="e153a-272">Usługa Application Insights może monit o zainstalowanie rozszerzenia lokacji usługi Application Insights, aby rozpocząć zbieranie danych.</span><span class="sxs-lookup"><span data-stu-id="e153a-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span></span> <span data-ttu-id="e153a-273">Instalowanie rozszerzenia lokacji powoduje ponowne uruchomienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e153a-273">Installing the site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="e153a-275">Usługa Application Insights ma zaawansowanych funkcji, ustawić, aby dowiedzieć się więcej, skorzystaj z łączy zawarte w [następne kroki](#next) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e153a-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span></span>

## <span data-ttu-id="e153a-276"><a name="next"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e153a-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="e153a-277">Co to jest usługa Application Insights</span><span class="sxs-lookup"><span data-stu-id="e153a-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="e153a-278">Monitorowanie wydajności aplikacji sieci web platformy Azure przy użyciu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="e153a-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="e153a-279">Monitorowanie dostępności i szybkość reakcji każdej witrynie sieci web z usługą Application Insights</span><span class="sxs-lookup"><span data-stu-id="e153a-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
