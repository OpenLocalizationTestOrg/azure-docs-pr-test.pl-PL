---
title: aaaMonitor aplikacji sieci Web | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooset się monitorowania na aplikację sieci Web"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="8ab2c-103">Monitor usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="8ab2c-103">Monitor App Service</span></span>
<span data-ttu-id="8ab2c-104">W tym samouczku przedstawiono sposób monitorowania aplikacji i przy użyciu hello platformy wbudowane narzędzia toosolve problemów, jeśli występują.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-104">This tutorial walks you through monitoring your app and using hello built-in platform tools toosolve problems when they occur.</span></span>

<span data-ttu-id="8ab2c-105">Każdej sekcji tego dokumentu przechodzi przez określoną funkcję.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="8ab2c-106">Korzystanie z funkcji hello razem umożliwiają:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-106">Using hello features together let you:</span></span>
- <span data-ttu-id="8ab2c-107">Identyfikowanie problemu w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="8ab2c-108">Określanie, kiedy hello przyczyną problemu jest kod lub hello platformy.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-108">Determining when hello issue is caused by your code or hello platform.</span></span>
- <span data-ttu-id="8ab2c-109">Zawęź hello źródłem problemu hello w kodzie.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-109">Narrow down hello source of hello problem in your code.</span></span>
- <span data-ttu-id="8ab2c-110">Debugowanie i rozwiązywania problemu hello.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-110">Debugging and fixing hello issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8ab2c-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="8ab2c-111">Before you begin</span></span>
- <span data-ttu-id="8ab2c-112">Należy toomonitor aplikacji sieci Web i wykonaj hello opisane kroki.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-112">You need a Web App toomonitor and follow hello outlined steps.</span></span>
    - <span data-ttu-id="8ab2c-113">Można utworzyć aplikacji hello wykonaj czynności opisane w hello [tworzenie aplikacji ASP.NET na platformie Azure z bazy danych SQL](app-service-web-tutorial-dotnet-sqldatabase.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-113">You can create an application following hello steps described in hello [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="8ab2c-114">Jeśli chcesz tootry **zdalnego debugowania** aplikacji, potrzebujesz programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-114">If you want tootry out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="8ab2c-115">Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello wolnego [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8ab2c-115">If you don’t already have Visual Studio 2017 installed, you can download and use hello free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="8ab2c-116">Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-116">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

## <span data-ttu-id="8ab2c-117"><a name="metrics"></a>Krok 1 — widok metryk</span><span class="sxs-lookup"><span data-stu-id="8ab2c-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="8ab2c-118">**Metryki** są przydatne toounderstand:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-118">**Metrics** are useful toounderstand:</span></span>
- <span data-ttu-id="8ab2c-119">Kondycja aplikacji</span><span class="sxs-lookup"><span data-stu-id="8ab2c-119">Application health</span></span>
- <span data-ttu-id="8ab2c-120">Wydajność aplikacji</span><span class="sxs-lookup"><span data-stu-id="8ab2c-120">App performance</span></span>
- <span data-ttu-id="8ab2c-121">Użycie zasobów</span><span class="sxs-lookup"><span data-stu-id="8ab2c-121">Resource consumption</span></span>

<span data-ttu-id="8ab2c-122">Po zbadaniu problemu z aplikacją, przeglądanie metryki jest toostart dobrym miejscem.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-122">When investigating an application issue, reviewing metrics is a good place toostart.</span></span> <span data-ttu-id="8ab2c-123">Azure portal ma toovisually szybko sprawdzić za pomocą aplikacji hello metryki **Azure Monitor**.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-123">Azure portal has a quick way toovisually inspect hello metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="8ab2c-124">Metryki udostępnianie widok historycznych w kilku agregacjach klucza dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="8ab2c-125">Dla dowolnej aplikacji hostowanej w usłudze app service należy monitorować zarówno hello aplikacji sieci Web, jak i hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-125">For any app hosted in app service, you should monitor both hello Web App and hello App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="8ab2c-126">Plan usługi aplikacji reprezentuje kolekcję hello toohost fizyczne zasoby używane aplikacje.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-126">An App Service plan represents hello collection of physical resources used toohost your apps.</span></span> <span data-ttu-id="8ab2c-127">Wszystkie aplikacje przypisane tooan planu usługi aplikacji udziału hello zasobów zdefiniowana przez nią stosowanie koszt toosave odnośnie do hostowania wielu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-127">All applications assigned tooan App Service plan share hello resources defined by it allowing you toosave cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="8ab2c-128">Plany usługi App Service definiują następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-128">App Service plans define:</span></span>
> * <span data-ttu-id="8ab2c-129">Region: Europa Północna, wschodnie stany USA, Azja południowo-wschodnia,... itd.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="8ab2c-130">Rozmiar wystąpienia: Mały, Średni, duża itp.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="8ab2c-131">Liczba skali: jedną, dwie lub trzy wystąpienia, itp.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="8ab2c-132">Jednostka SKU: Wolne Shared Basic, Standard, Premium, itp.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="8ab2c-133">metryki tooreview dla aplikacji sieci Web, przejdź toohello **omówienie** bloku aplikacji hello ma toomonitor.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-133">tooreview metrics for your Web App, go toohello **Overview** blade of hello app you want toomonitor.</span></span> <span data-ttu-id="8ab2c-134">W tym miejscu można wyświetlić wykresu dla metryki aplikacji jako **Kafelek monitorowanie**.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="8ab2c-135">Kliknij przycisk tooedit kafelka hello i skonfiguruj jakie tooview metryki oraz hello toodisplay zakresu czasu.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-135">Click hello tile tooedit and configure what metrics tooview and hello time range toodisplay.</span></span>

<span data-ttu-id="8ab2c-136">W bloku zasobów hello domyślne udostępnia widok hello żądań aplikacji i błędów dotyczących hello ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-136">By default hello resource blade provides a view for hello Application Requests and errors for hello last hour.</span></span>
<span data-ttu-id="8ab2c-137">![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="8ab2c-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="8ab2c-138">Jak widać w przykładzie hello mamy aplikacji, która generuje wiele **błędy serwera HTTP**.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-138">As you can see in hello example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="8ab2c-139">duża liczba błędów Hello jest hello pierwsze wskazanie potrzebne tooinvestigate tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-139">hello high volume of errors is hello first indication we need tooinvestigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="8ab2c-140">Więcej informacji na temat Monitora Azure z hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-140">Learn more about Azure Monitor with hello following links:</span></span>
> - [<span data-ttu-id="8ab2c-141">Rozpoczynanie pracy z monitorem Azure</span><span class="sxs-lookup"><span data-stu-id="8ab2c-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="8ab2c-142">Metryki Azure</span><span class="sxs-lookup"><span data-stu-id="8ab2c-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="8ab2c-143">Obsługiwane metryki z monitorem Azure</span><span class="sxs-lookup"><span data-stu-id="8ab2c-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="8ab2c-144">Azure pulpity nawigacyjne</span><span class="sxs-lookup"><span data-stu-id="8ab2c-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="8ab2c-145"><a name="alerts"></a>Krok 2 — Konfigurowanie alertów</span><span class="sxs-lookup"><span data-stu-id="8ab2c-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="8ab2c-146">**Alerty** może być skonfigurowany tootrigger przy użyciu określonych warunków dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-146">**Alerts** can be configured tootrigger on specific conditions for your app.</span></span>

<span data-ttu-id="8ab2c-147">W [krok 1 — widok metryki](#metrics), widzieliśmy, że aplikacja hello miała dużą liczbę błędów.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-147">In [Step 1 - View metrics](#metrics), we saw that hello application had a high number of errors.</span></span>

<span data-ttu-id="8ab2c-148">Pozwala skonfigurować alert tooautomatically Otrzymuj powiadomienia w przypadku błędów.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-148">Lets configure an alert tooautomatically get notified when errors occur.</span></span> <span data-ttu-id="8ab2c-149">W takim przypadku firma Microsoft ma hello toosend alertów i wiadomości e-mail za każdym razem, gdy hello liczbę błędów HTTP 50 X przechodzi przez określony próg.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-149">In this case, we want hello alert toosend and e-mail every time hello number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="8ab2c-150">toocreate alertu, przejdź zbyt**monitorowanie** > **alerty** i kliknij przycisk **[+] Dodaj Alert**.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-150">toocreate an alert, navigate too**Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Alerty](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="8ab2c-152">Podaj wartości dla konfiguracji alertu hello:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-152">Provide values for hello Alert configuration:</span></span>
- <span data-ttu-id="8ab2c-153">**Zasób:** hello toomonitor lokacji hello alert.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-153">**Resource:** hello site toomonitor with hello alert.</span></span>
- <span data-ttu-id="8ab2c-154">**Nazwa:** nazwę alertu, w tym przypadku: *wysokiej HTTP 50 X*.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="8ab2c-155">**Opis:** wyjaśnienie ten alert spojrzenie na zwykły tekst.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="8ab2c-156">**Alert dotyczący:** alerty można przeglądać metryki lub zdarzeń, w tym przykładzie czekamy na metryki.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="8ab2c-157">**Metryka:** jakie toomonitor metryki, w tym przypadku: *błędy serwera HTTP*.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-157">**Metric:** What metric toomonitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="8ab2c-158">**Warunek:** po tooalert, w tym przypadku wybierz hello *większe* opcji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-158">**Condition:** When tooalert, in this case select hello *greater than* option.</span></span>
- <span data-ttu-id="8ab2c-159">**Próg:** toolook wartości, co jest w tym przypadku: *400*.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-159">**Threshold:** What is value toolook for, in this case: *400*.</span></span>
- <span data-ttu-id="8ab2c-160">**Okres:** alerty działają na powitania średnia wartość metryki.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-160">**Period:** Alerts operate over hello average value of a metric.</span></span> <span data-ttu-id="8ab2c-161">Mniejsze okresów uzyskanie bardziej poufnego alerty.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="8ab2c-162">w takim przypadku czekamy na *5 minut*.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="8ab2c-163">**Wyślij wiadomość e-mail właściciele i Współautorzy:** w takim przypadku: *włączone*.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="8ab2c-164">Teraz, gdy hello alert jest tworzony wiadomości e-mail są wysyłane za każdym razem, gdy hello aplikacja przechodzi powyżej wartości progowej hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-164">Now that hello alert is created an email is sent every time hello app goes over hello configured threshold.</span></span> <span data-ttu-id="8ab2c-165">Aktywne alerty mogą być przeglądane również na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-165">Active alerts can also be reviewed in hello Azure portal.</span></span>

![Wyzwalanie alertów](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="8ab2c-167">Dowiedz się więcej o alertach Azure z hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-167">Learn more about Azure Alerts with hello following links:</span></span>
> - [<span data-ttu-id="8ab2c-168">Co to są alerty na platformie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8ab2c-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="8ab2c-169">Podejmij działanie metryk</span><span class="sxs-lookup"><span data-stu-id="8ab2c-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="8ab2c-170">Tworzenie metryk alertów</span><span class="sxs-lookup"><span data-stu-id="8ab2c-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="8ab2c-171"><a name="companion"></a>Krok 3 — Pomocnik usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="8ab2c-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="8ab2c-172">**Pomocnik usługi aplikacji** oferuje toomonitor wygodny sposób aplikacji z natywnym środowiskiem urządzenia przenośnego (z systemem iOS lub Android).</span><span class="sxs-lookup"><span data-stu-id="8ab2c-172">**App Service companion** offers a convenient way toomonitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="8ab2c-173">Użyj Pomocnik usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="8ab2c-174">Przejrzyj metryki aplikacji</span><span class="sxs-lookup"><span data-stu-id="8ab2c-174">Review application metrics</span></span>
- <span data-ttu-id="8ab2c-175">Przejrzyj i korzystania z aplikacji, alertów i zalecenia</span><span class="sxs-lookup"><span data-stu-id="8ab2c-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="8ab2c-176">Rozwiązywania problemów z podstawowego (przeglądania, uruchom, Zatrzymaj, ponowne uruchomienie aplikacji hello)</span><span class="sxs-lookup"><span data-stu-id="8ab2c-176">Perform basic troubleshooting (browse, start, stop, restart hello app)</span></span>
- <span data-ttu-id="8ab2c-177">Uzyskiwanie powiadomień wypychanych dla zdarzeń krytycznych.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-177">Get push notifications for critical events.</span></span>

![Pomocnik usługi aplikacji](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="8ab2c-179">[![Aplikacja usługi pomocnika sklepu](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Google Play pomocniczy usługi aplikacji](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="8ab2c-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="8ab2c-180">Pomocnik usługi aplikacji można zainstalować z hello [sklepu z aplikacjami](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) lub [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="8ab2c-180">You can install App Service companion from hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="8ab2c-181"><a name="diagnose"></a>Krok 4 — diagnozowanie i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="8ab2c-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="8ab2c-182">**Diagnozowanie i rozwiązywanie problemów** pomaga oddzielić problemy aplikacji tworzą problemy platformy.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="8ab2c-183">On również sugerować możliwe ograniczenie jego skutków tooget toohealthy wstecz Twojej aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-183">It can also suggest possible mitigations tooget your Web App back toohealthy.</span></span>

![Diagnozowanie i rozwiązywanie problemów](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="8ab2c-185">Kontynuowaniem hello przykład formularz poprzednie kroki, zobaczysz, że aplikacja hello ma zostać problemy dostępności.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-185">Continuing with hello example form previous steps, we can see that hello application has been having availably issues.</span></span> <span data-ttu-id="8ab2c-186">Z kolei hello platformy dostępności nie zostały przeniesione od 100%.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-186">In contrast, hello platform availability has not moved from 100%.</span></span>

<span data-ttu-id="8ab2c-187">Gdy aplikacji hello nastąpił problem i hello platformy pozostaje w górę, jest jasne wskazanie, że firma Microsoft ma do czynienia z problemu z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-187">When hello app is having issue and hello platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="8ab2c-188"><a name="logging"></a>Krok 5 — rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="8ab2c-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="8ab2c-189">Teraz, gdy będziemy mieć zawęzić hello problemu z aplikacją tooan błędów, może przyjrzymy się tooget Dzienniki aplikacji i serwerze hello więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-189">Now that we have narrowed down hello failures tooan application issue, we can look at hello application and server logs tooget more information.</span></span>

<span data-ttu-id="8ab2c-190">Rejestrowanie umożliwia toocollect zarówno **programu Application Diagnostics** i **diagnostyki serwera sieci Web** dzienników aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-190">Logging allows you toocollect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="8ab2c-191">Usługa Application Diagnostics</span><span class="sxs-lookup"><span data-stu-id="8ab2c-191">Application Diagnostics</span></span>
<span data-ttu-id="8ab2c-192">Diagnostyki aplikacji umożliwia możesz toocapture śladów utworzonego przez aplikacji hello w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-192">Application diagnostics allows you toocapture traces produced by hello application at runtime.</span></span>

<span data-ttu-id="8ab2c-193">Dodawanie tooyour śledzenie aplikacji znacznie skraca toodebug możliwości, a punkt przypięcia problemy.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-193">Adding tracing tooyour application greatly improves your ability toodebug and pin-point issues.</span></span>

<span data-ttu-id="8ab2c-194">W programie ASP.NET, możesz zalogować się przy użyciu śladów aplikacji [System.Diagnostics.Trace — klasa](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate zdarzenia, które są przechwytywane przez infrastrukturę dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate events that are captured by hello log infrastructure.</span></span> <span data-ttu-id="8ab2c-195">Można również określić ważność hello śledzenia hello łatwiejsze filtrowania.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-195">You can also specify hello severity of hello trace for easier filtering.</span></span>

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
<span data-ttu-id="8ab2c-196">Rejestrowanie aplikacji tooenable Przejdź zbyt**monitorowanie** > **dzienników diagnostycznych** i włączyć rejestrowania aplikacji przy użyciu hello przełączników.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-196">tooenable Application logging Go too**Monitoring** > **Diagnostic Logs** and Enable Application Logging using hello toggles.</span></span>

![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="8ab2c-198">Dzienniki aplikacji może być aplikacja sieci Web tooyour przechowywanych w systemie plików lub wypchnięty tooblob magazynu.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-198">Application logs can be stored tooyour Web App's file system or pushed out tooblob storage.</span></span> <span data-ttu-id="8ab2c-199">Scenariusze produkcji jest zalecana toouse magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-199">For production scenarios, it's recommended toouse blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ab2c-200">Włączanie rejestrowania ma wpływ na wykorzystanie wydajności i zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="8ab2c-201">W scenariuszach produkcji zaleca się w dzienniku błędów.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="8ab2c-202">Pełniejsze rejestrowanie należy włączyć tylko podczas badania problemów.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="8ab2c-203">Diagnostyka serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="8ab2c-203">Web Server Diagnostics</span></span>
<span data-ttu-id="8ab2c-204">Dzienniki serwera sieci Web są generowane, nawet jeśli aplikacja nie została zinstrumentowana.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="8ab2c-205">Usługi aplikacji może zbierać trzy różne typy dzienników serwera:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="8ab2c-206">**Rejestrowanie pracy serwera sieci Web**</span><span class="sxs-lookup"><span data-stu-id="8ab2c-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="8ab2c-207">Informacje o transakcjach HTTP przy użyciu hello [rozszerzonym formacie W3C dziennika pliku](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ab2c-207">Information about HTTP transactions using hello [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="8ab2c-208">Przydatne podczas określania ogólną metryki lokacji, takie jak hello liczba żądań obsłużonych lub liczbę żądań pochodzą z określonego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-208">Useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="8ab2c-209">**Szczegółowe informacje o błędzie logowania**</span><span class="sxs-lookup"><span data-stu-id="8ab2c-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="8ab2c-210">Szczegółowe informacje o błędzie kodów stanu HTTP, które wskazania błędu (kod stanu 400 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="8ab2c-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="8ab2c-211">Dowiedz się więcej na temat rejestrowania szczegółowe informacje o błędzie</span><span class="sxs-lookup"><span data-stu-id="8ab2c-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="8ab2c-212">**Śledzenie niepomyślnych żądań**</span><span class="sxs-lookup"><span data-stu-id="8ab2c-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="8ab2c-213">Szczegółowe informacje dotyczące żądań zakończonych niepowodzeniem, w tym śledzenia hello komponenty używane tooprocess hello żądania i hello czas w poszczególnych składników.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-213">Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span>
    - <span data-ttu-id="8ab2c-214">Żądań zakończonych niepowodzeniem dzienniki są przydatne podczas próby tooisolate, co jest przyczyną błędu HTTP.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-214">Failed request logs are useful when trying tooisolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="8ab2c-215">Dowiedz się więcej na temat śledzenia nieudanych żądań</span><span class="sxs-lookup"><span data-stu-id="8ab2c-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="8ab2c-216">Rejestrowanie serwera tooenable:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-216">tooenable Server logging:</span></span>
- <span data-ttu-id="8ab2c-217">Przejdź za**monitorowanie** > **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-217">go too**Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="8ab2c-218">Włącz hello różne rodzaje diagnostyki serwera sieci Web za pomocą przełączników hello.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-218">Enable hello different types of Web Server Diagnostics using hello toggles.</span></span>

![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="8ab2c-220">Włączanie rejestrowania ma wpływ na wykorzystanie wydajności i zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="8ab2c-221">W przypadku scenariuszy produkcji dzienniki błędów są zalecane, włączyć tylko pełniejsze rejestrowanie podczas badania problemów.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="8ab2c-222">Uzyskiwanie dostępu do dzienników</span><span class="sxs-lookup"><span data-stu-id="8ab2c-222">Accessing Logs</span></span>
<span data-ttu-id="8ab2c-223">Dzienników przechowywanych w magazynie obiektów blob są dostępne za pomocą Eksploratora usługi Storage platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="8ab2c-224">Dzienników przechowywanych w aplikacji sieci Web hello systemu plików są dostępne za pośrednictwem FTP w obszarze hello następującej ścieżki:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-224">Logs stored in hello Web App's filesystem are accessed through FTP under hello following paths:</span></span>

- <span data-ttu-id="8ab2c-225">**Dzienniki aplikacji** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="8ab2c-226">Ten folder zawiera jeden lub więcej plików tekstowych, zawierający informacje o wygenerowane przez rejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="8ab2c-227">**Nie powiodło się żądanie śladów** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="8ab2c-228">Ten folder zawiera plik XSL i co najmniej jeden plik XML.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="8ab2c-229">**Szczegółowe dzienniki błędów** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="8ab2c-230">Ten folder zawiera co najmniej jeden plik .htm o wiele informacji dotyczących błędów HTTP wygenerowany przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="8ab2c-231">**Dzienniki serwera w sieci Web** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="8ab2c-232">Ten folder zawiera jeden lub więcej plików tekst sformatowany przy użyciu hello W3C rozszerzony format pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-232">This folder contains one or more text files formatted using hello W3C extended log file format.</span></span>

## <span data-ttu-id="8ab2c-233"><a name="streaming"></a>Krok 6 - dzienników przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="8ab2c-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="8ab2c-234">Dzienniki przesyłania strumieniowego są wygodne podczas debugowania aplikacji, ponieważ zaoszczędzić czas, w porównaniu zbyt[podczas uzyskiwania dostępu do dzienników hello](#Accessing-Logs) za pośrednictwem FTP.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-234">Streaming logs are convenient when debugging an application since it saves time compared too[accessing hello logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="8ab2c-235">Usługi aplikacji może być przesyłany strumieniowo **Dzienniki aplikacji** i **dzienniki serwera sieci Web** zgodnie z ich wygenerowaniu.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="8ab2c-236">Przed podjęciem próby toostream dzienniki, upewnij się, że włączono zbieranie dzienników zgodnie z opisem w hello [rejestrowanie](#logging) sekcji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-236">Before trying toostream logs, make sure you have enabled collecting logs as described in hello [Logging](#logging) section.</span></span>

<span data-ttu-id="8ab2c-237">Dzienniki toostream Przejdź zbyt**monitorowanie**> **strumienia dziennika**.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-237">toostream logs, go too**Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="8ab2c-238">Wybierz **Dzienniki aplikacji** lub **dzienniki serwera w sieci Web** zależności informacjach szukasz.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="8ab2c-239">W tym miejscu mogą również wstrzymać, uruchom ponownie i hello buforu.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-239">From here, you can also pause, restart, and clear hello buffer.</span></span>

![Dzienniki przesyłania strumieniowego](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="8ab2c-241">Dzienniki są generowane tylko, gdy ruchu w aplikacji hello, a także może zwiększyć poziom szczegółowości hello tooget dzienniki więcej zdarzeń lub informacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-241">Logs are only generated when there is traffic on hello app, you can also increase hello verbosity of logs tooget more events or information.</span></span>

## <span data-ttu-id="8ab2c-242"><a name="remote"></a>Krok 7. debugowanie zdalne</span><span class="sxs-lookup"><span data-stu-id="8ab2c-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="8ab2c-243">Po utworzeniu wskazywanej przez kod pin hello źródło problemów aplikacji hello użyj **zdalnego debugowania** toowalk za pośrednictwem hello kodu.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-243">Once you have pin-pointed hello source of hello applications problems, use **Remote Debugging** toowalk through hello code.</span></span>

<span data-ttu-id="8ab2c-244">Zdalne debugowanie umożliwia, możesz dołączyć debuger tooyour aplikacji sieci Web w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-244">Remote debugging lets you attach a debugger tooyour Web App running in hello cloud.</span></span> <span data-ttu-id="8ab2c-245">Można ustawić punktów przerwania, manipulowanie nimi pamięci bezpośrednio, krokowo kodu oraz nawet zmienić ścieżkę kodu hello, podobnie jak w przypadku aplikacji uruchomionej na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-245">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path just like you do for an app running locally.</span></span>

<span data-ttu-id="8ab2c-246">tooattach hello debugera tooyour aplikacji uruchomionej w chmurze hello:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-246">tooattach hello debugger tooyour app running in hello cloud:</span></span>

- <span data-ttu-id="8ab2c-247">Za pomocą programu Visual Studio 2017 r hello Otwórz rozwiązanie dla aplikacji hello ma toodebug</span><span class="sxs-lookup"><span data-stu-id="8ab2c-247">Using Visual Studio 2017, open hello solution for hello app you want toodebug</span></span>
- <span data-ttu-id="8ab2c-248">Ustaw niektórych punktach hamulca, tak jak dla rozwoju lokalnych.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="8ab2c-249">Otwórz **Eksplorator chmury** (kont. + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="8ab2c-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="8ab2c-250">Zaloguj się przy użyciu poświadczeń platformy azure, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="8ab2c-251">Znajdź aplikacji hello ma toodebug</span><span class="sxs-lookup"><span data-stu-id="8ab2c-251">Find hello app you want toodebug</span></span>
- <span data-ttu-id="8ab2c-252">Wybierz **dołączyć debuger** hello formularza **akcje** okienka.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-252">Select **Attach Debugger** form hello **Actions** pane.</span></span>

![Debugowanie zdalne](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="8ab2c-254">Visual Studio konfiguruje aplikację do zdalnego debugowania i uruchamia okno przeglądarki, który nawiguje tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates tooyour app.</span></span> <span data-ttu-id="8ab2c-255">Przejrzyj punkty przerwania tootrigger aplikacji i wykonywać krokowo kodu hello.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-255">Browse through your app tootrigger break points and step through hello code.</span></span>

> [!WARNING]
> <span data-ttu-id="8ab2c-256">Nie zaleca się uruchamiania w trybie debugowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="8ab2c-257">Jeśli wystąpienia serwera toomultiple nie skalowania aplikacji produkcyjnych, debugowanie zapobiec powitania serwera sieci web z odpowiada tooother żądań.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-257">If your production app is not scaled out toomultiple server instances, debugging prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="8ab2c-258">Podczas rozwiązywania problemów w środowisku produkcyjnym, najlepiej zasobu jest zbyt[skonfigurować rejestrowanie](#logging) i [usługi Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="8ab2c-258">For troubleshooting production problems, your best resource is too[configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="8ab2c-259"><a name="explorer"></a>Krok 8 - Eksploratora procesów</span><span class="sxs-lookup"><span data-stu-id="8ab2c-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="8ab2c-260">Gdy aplikacja jest skalowana w poziomie toomore niż jedno wystąpienie **Eksploratora procesów** mogą ułatwić identyfikację wystąpienia określonych problemów.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-260">When your application is scaled out toomore than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="8ab2c-261">Użyj **przetworzyć Explorer** do:</span><span class="sxs-lookup"><span data-stu-id="8ab2c-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="8ab2c-262">Wylicza wszystkie procesy hello w różnych wystąpieniach planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-262">Enumerate all hello processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="8ab2c-263">Przechodzenie i wyświetlanie uchwytów hello i moduły skojarzone z każdym procesie.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-263">Drill down and view hello handles and modules associated with each process.</span></span>
- <span data-ttu-id="8ab2c-264">Liczba Procesora widoku, zestaw roboczy i wątku na powitania przetworzyć poziomu toohelp zidentyfikować wyczerpania procesów</span><span class="sxs-lookup"><span data-stu-id="8ab2c-264">View CPU, Working Set, and Thread count at hello process level toohelp you identify runaway processes</span></span>
- <span data-ttu-id="8ab2c-265">Znajdź dojść otwartych plików, a nawet kill wystąpienia określonego procesu.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="8ab2c-266">Eksploratora procesów można znaleźć w **monitorowanie** > **Eksploratora procesów**.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Eksplorator procesów](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="8ab2c-268"><a name="insights"></a>Krok 9 - usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="8ab2c-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="8ab2c-269">**Usługa Application Insights** zapewnia profilowania aplikacji i zaawansowanych możliwości monitorowania dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="8ab2c-270">Użyj usługi Application Insights toodetect i diagnozowanie wyjątków i problemy z wydajnością w aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-270">Use Application Insights toodetect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="8ab2c-271">Można włączyć usługi Application Insights dla aplikacji sieci Web, w obszarze **monitorowanie** > **usługi Application Insights**</span><span class="sxs-lookup"><span data-stu-id="8ab2c-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="8ab2c-272">Usługa Application Insights może monitować tooinstall hello usługi Application Insights lokacji rozszerzenia toostart zbierania danych.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-272">Application Insights might prompt you tooinstall hello Application Insights site extension toostart collecting data.</span></span> <span data-ttu-id="8ab2c-273">Instalowanie rozszerzenia lokacji hello powoduje ponowne uruchomienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-273">Installing hello site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="8ab2c-275">Usługa Application Insights ma zaawansowanych funkcji ustawiona, toolearn, wykonaj łącza hello w hello [następne kroki](#next) sekcji.</span><span class="sxs-lookup"><span data-stu-id="8ab2c-275">Application Insights has a rich feature set, toolearn more, follow hello links included in hello [Next Steps](#next) section.</span></span>

## <span data-ttu-id="8ab2c-276"><a name="next"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ab2c-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="8ab2c-277">Co to jest usługa Application Insights</span><span class="sxs-lookup"><span data-stu-id="8ab2c-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="8ab2c-278">Monitorowanie wydajności aplikacji sieci web platformy Azure przy użyciu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="8ab2c-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="8ab2c-279">Monitorowanie dostępności i szybkość reakcji każdej witrynie sieci web z usługą Application Insights</span><span class="sxs-lookup"><span data-stu-id="8ab2c-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
