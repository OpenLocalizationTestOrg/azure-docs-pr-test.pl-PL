---
title: "aaaMonitor na żywo ASP.NET sieci web aplikacji za pomocą usługi Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Monitorowanie wydajności witryny sieci Web bez jej ponownego wdrażania. Działa z aplikacjami sieci Web platformy ASP.NET hostowanymi lokalnie na maszynach wirtualnych lub platformie Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="c51ee-104">Instrumentowanie aplikacji sieci Web w czasie wykonywania za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="c51ee-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="c51ee-105">Można Instrumentacja aplikacji sieci web na żywo z usługą Azure Application Insights, bez konieczności toomodify lub ponownego wdrażania kodu.</span><span class="sxs-lookup"><span data-stu-id="c51ee-105">You can instrument a live web app with Azure Application Insights, without having toomodify or redeploy your code.</span></span> <span data-ttu-id="c51ee-106">Jeśli Twoje aplikacje są hostowane na lokalnym serwerze IIS, zainstaluj monitor stanu.</span><span class="sxs-lookup"><span data-stu-id="c51ee-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="c51ee-107">Jeśli zostaną aplikacji sieci web platformy Azure lub uruchomić w maszynie Wirtualnej platformy Azure, możesz przełączyć się na monitorowanie usługi Application Insights z poziomu Panelu sterowania Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c51ee-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from hello Azure control panel.</span></span> <span data-ttu-id="c51ee-108">Istnieją także osobne artykuły na temat instrumentacji [działających aplikacji sieci Web w technologii J2EE](app-insights-java-live.md) i [usług Azure Cloud Services](app-insights-cloudservices.md). Potrzebna jest subskrypcja platformy [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="c51ee-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![przykładowe wykresy](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="c51ee-110">Dostępne są opcje trzy aplikacji sieci web, tras tooapply usługi Application Insights tooyour .NET:</span><span class="sxs-lookup"><span data-stu-id="c51ee-110">You have a choice of three routes tooapply Application Insights tooyour .NET web applications:</span></span>

* <span data-ttu-id="c51ee-111">**Czas kompilacji:** [hello Dodaj zestaw SDK usługi Application Insights] [ greenbrown] kodu aplikacji sieci web tooyour.</span><span class="sxs-lookup"><span data-stu-id="c51ee-111">**Build time:** [Add hello Application Insights SDK][greenbrown] tooyour web app code.</span></span>
* <span data-ttu-id="c51ee-112">**Czas wykonywania:** Instrumentacja aplikacji sieci web na serwerze hello zgodnie z opisem poniżej, bez odbudowywania ani ponownego wdrażania hello kodu.</span><span class="sxs-lookup"><span data-stu-id="c51ee-112">**Run time:** Instrument your web app on hello server, as described below, without rebuilding and redeploying hello code.</span></span>
* <span data-ttu-id="c51ee-113">**Zarówno:** kompilacji hello zestawu SDK do kodu aplikacji sieci web, a także zastosować dla niej hello rozszerzenia środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="c51ee-113">**Both:** Build hello SDK into your web app code, and also apply hello run-time extensions.</span></span> <span data-ttu-id="c51ee-114">Pobierz hello najlepszy obie opcje.</span><span class="sxs-lookup"><span data-stu-id="c51ee-114">Get hello best of both options.</span></span>

<span data-ttu-id="c51ee-115">Poniżej przedstawiono podsumowanie tego, co można uzyskać, korzystając z danej trasy:</span><span class="sxs-lookup"><span data-stu-id="c51ee-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="c51ee-116">W czasie kompilacji</span><span class="sxs-lookup"><span data-stu-id="c51ee-116">Build time</span></span> | <span data-ttu-id="c51ee-117">W czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="c51ee-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c51ee-118">Żądania i wyjątki</span><span class="sxs-lookup"><span data-stu-id="c51ee-118">Requests & exceptions</span></span> |<span data-ttu-id="c51ee-119">Tak</span><span class="sxs-lookup"><span data-stu-id="c51ee-119">Yes</span></span> |<span data-ttu-id="c51ee-120">Tak</span><span class="sxs-lookup"><span data-stu-id="c51ee-120">Yes</span></span> |
| [<span data-ttu-id="c51ee-121">Bardziej szczegółowe wyjątki</span><span class="sxs-lookup"><span data-stu-id="c51ee-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="c51ee-122">Tak</span><span class="sxs-lookup"><span data-stu-id="c51ee-122">Yes</span></span> |
| [<span data-ttu-id="c51ee-123">Diagnostyka zależności</span><span class="sxs-lookup"><span data-stu-id="c51ee-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="c51ee-124">Na platformie .NET 4.6 +, ale mniej szczegółów</span><span class="sxs-lookup"><span data-stu-id="c51ee-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="c51ee-125">Tak, kompletne szczegóły: kody wyników, tekst polecenia SQL, czasownik HTTP</span><span class="sxs-lookup"><span data-stu-id="c51ee-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="c51ee-126">Liczniki wydajności sytemu</span><span class="sxs-lookup"><span data-stu-id="c51ee-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="c51ee-127">Tak</span><span class="sxs-lookup"><span data-stu-id="c51ee-127">Yes</span></span> |<span data-ttu-id="c51ee-128">Tak</span><span class="sxs-lookup"><span data-stu-id="c51ee-128">Yes</span></span> |
| <span data-ttu-id="c51ee-129">[Interfejs API dla telemetrii niestandardowej][api]</span><span class="sxs-lookup"><span data-stu-id="c51ee-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="c51ee-130">Tak</span><span class="sxs-lookup"><span data-stu-id="c51ee-130">Yes</span></span> |<span data-ttu-id="c51ee-131">Nie</span><span class="sxs-lookup"><span data-stu-id="c51ee-131">No</span></span> |
| [<span data-ttu-id="c51ee-132">Integracja dziennika śledzenia</span><span class="sxs-lookup"><span data-stu-id="c51ee-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="c51ee-133">Tak</span><span class="sxs-lookup"><span data-stu-id="c51ee-133">Yes</span></span> |<span data-ttu-id="c51ee-134">Nie</span><span class="sxs-lookup"><span data-stu-id="c51ee-134">No</span></span> |
| [<span data-ttu-id="c51ee-135">Widok strony i dane użytkownika</span><span class="sxs-lookup"><span data-stu-id="c51ee-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="c51ee-136">Tak</span><span class="sxs-lookup"><span data-stu-id="c51ee-136">Yes</span></span> |<span data-ttu-id="c51ee-137">Nie</span><span class="sxs-lookup"><span data-stu-id="c51ee-137">No</span></span> |
| <span data-ttu-id="c51ee-138">Kod toorebuild potrzebny</span><span class="sxs-lookup"><span data-stu-id="c51ee-138">Need toorebuild code</span></span> |<span data-ttu-id="c51ee-139">Tak</span><span class="sxs-lookup"><span data-stu-id="c51ee-139">Yes</span></span> | <span data-ttu-id="c51ee-140">Nie</span><span class="sxs-lookup"><span data-stu-id="c51ee-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="c51ee-141">Monitorowanie działającej aplikacji sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c51ee-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="c51ee-142">Jeśli aplikacja jest uruchomiona jako usługa Azure usługi sieci web, tutaj w sposób tooswitch dotyczące monitorowania:</span><span class="sxs-lookup"><span data-stu-id="c51ee-142">If your application is running as an Azure web service, here's how tooswitch on monitoring:</span></span>

* <span data-ttu-id="c51ee-143">Wybierz usługi Application Insights w Panelu sterowania aplikacji hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c51ee-143">Select Application Insights on hello app's control panel in Azure.</span></span>

    ![Konfigurowanie usługi Application Insights dla aplikacji sieci Web platformy Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="c51ee-145">Po otwarciu strony podsumowania hello usługi Application Insights, kliknij łącze hello na powitania dolnej tooopen hello pełne zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c51ee-145">When hello Application Insights summary page opens, click hello link at hello bottom tooopen hello full Application Insights resource.</span></span>

    ![Kliknij go, tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="c51ee-147">[Monitorowanie aplikacji w chmurze i na maszynie wirtualnej](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="c51ee-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="c51ee-148">Włączanie monitorowania po stronie klienta na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="c51ee-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="c51ee-149">Po włączeniu usługi Application Insights na platformie Azure możesz dodać telemetrię widoku strony i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c51ee-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="c51ee-150">Wybierz kolejno pozycje Ustawienia > Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="c51ee-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="c51ee-151">W obszarze Ustawienia aplikacji dodaj nową parę klucz-wartość:</span><span class="sxs-lookup"><span data-stu-id="c51ee-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="c51ee-152">Klucz: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="c51ee-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="c51ee-153">Wartość:`true`</span><span class="sxs-lookup"><span data-stu-id="c51ee-153">Value: `true`</span></span>
3. <span data-ttu-id="c51ee-154">**Zapisz** hello ustawienia i **ponowne uruchomienie** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c51ee-154">**Save** hello settings and **Restart** your app.</span></span>

<span data-ttu-id="c51ee-155">zestaw SDK usługi Application Insights JavaScript Hello jest teraz wprowadzić do każdej strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="c51ee-155">hello Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="c51ee-156">Monitorowanie działającej aplikacji sieci Web usług IIS</span><span class="sxs-lookup"><span data-stu-id="c51ee-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="c51ee-157">Jeśli aplikacja jest hostowana na serwerze usług IIS, włącz usługę Application Insights przy użyciu monitora stanu.</span><span class="sxs-lookup"><span data-stu-id="c51ee-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="c51ee-158">Zaloguj się na serwerze sieci Web usług IIS, używając poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="c51ee-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="c51ee-159">Jeśli Monitor stanu usługi Application Insights nie jest już zainstalowany, Pobierz i uruchom hello [Instalator Monitor stanu](http://go.microsoft.com/fwlink/?LinkId=506648) (lub uruchom [Instalatora platformy sieci Web](https://www.microsoft.com/web/downloads/platform.aspx) i wyszukaj w nim Application Insights stanu Monitor).</span><span class="sxs-lookup"><span data-stu-id="c51ee-159">If Application Insights Status Monitor is not already installed, download and run hello [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="c51ee-160">Monitor stanu, wybierz hello zainstalowanych aplikacji sieci web lub witryny sieci Web, które mają toomonitor.</span><span class="sxs-lookup"><span data-stu-id="c51ee-160">In Status Monitor, select hello installed web application or website that you want toomonitor.</span></span> <span data-ttu-id="c51ee-161">Zaloguj się przy użyciu poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c51ee-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="c51ee-162">Konfigurowanie zasobów hello miejscu powoduje hello toosee hello portalu Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c51ee-162">Configure hello resource where you want toosee hello results in hello Application Insights portal.</span></span> <span data-ttu-id="c51ee-163">(Zazwyczaj jest najlepszym toocreate nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="c51ee-163">(Normally, it's best toocreate a new resource.</span></span> <span data-ttu-id="c51ee-164">Wybierz istniejący zasób, jeśli masz już [testy sieci Web][availability] lub [monitorowanie klienta][client] dla tej aplikacji).</span><span class="sxs-lookup"><span data-stu-id="c51ee-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Wybór aplikacji i zasobu.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="c51ee-166">Uruchom ponownie usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="c51ee-166">Restart IIS.</span></span>

    ![Wybierz ponowne uruchomienie u góry hello hello okna dialogowego.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="c51ee-168">Działanie usługi sieci Web zostanie na krótko przerwane.</span><span class="sxs-lookup"><span data-stu-id="c51ee-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="c51ee-169">Dostosowywanie opcji monitorowania</span><span class="sxs-lookup"><span data-stu-id="c51ee-169">Customize monitoring options</span></span>

<span data-ttu-id="c51ee-170">Włączanie usługi Application Insights dodaje biblioteki dll i ApplicationInsights.config tooyour aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c51ee-170">Enabling Application Insights adds DLLs and ApplicationInsights.config tooyour web app.</span></span> <span data-ttu-id="c51ee-171">Możesz [edycji pliku .config hello](app-insights-configuration-with-applicationinsights-config.md) toochange niektórych opcji hello.</span><span class="sxs-lookup"><span data-stu-id="c51ee-171">You can [edit hello .config file](app-insights-configuration-with-applicationinsights-config.md) toochange some of hello options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="c51ee-172">Po ponownym opublikowaniu aplikacji ponownie włącz usługę Application Insights</span><span class="sxs-lookup"><span data-stu-id="c51ee-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="c51ee-173">Aby ponownie opublikować aplikację, należy wziąć pod uwagę [Dodawanie usługi Application Insights toohello kodu w programie Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="c51ee-173">Before you re-publish your app, consider [adding Application Insights toohello code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="c51ee-174">Można uzyskać bardziej szczegółowe dane telemetryczne i telemetria niestandardowa toowrite hello możliwości.</span><span class="sxs-lookup"><span data-stu-id="c51ee-174">You'll get more detailed telemetry and hello ability toowrite custom telemetry.</span></span>

<span data-ttu-id="c51ee-175">Jeśli chcesz, aby toore-opublikować bez dodawania usługi Application Insights toohello kodu, należy pamiętać, że proces wdrażania hello może usunąć hello bibliotek DLL i ApplicationInsights.config z hello opublikowane witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="c51ee-175">If you want toore-publish without adding Application Insights toohello code, be aware that hello deployment process may delete hello DLLs and ApplicationInsights.config from hello published web site.</span></span> <span data-ttu-id="c51ee-176">Zatem:</span><span class="sxs-lookup"><span data-stu-id="c51ee-176">Therefore:</span></span>

1. <span data-ttu-id="c51ee-177">Jeśli edytowano plik ApplicationInsights.config, utwórz jego kopię przed ponownym opublikowaniem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c51ee-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="c51ee-178">Ponownie opublikuj aplikację.</span><span class="sxs-lookup"><span data-stu-id="c51ee-178">Republish your app.</span></span>
3. <span data-ttu-id="c51ee-179">Ponownie włącz monitorowanie za pomocą usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c51ee-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="c51ee-180">(Użyj odpowiedniej metody hello: panel sterowania aplikacji sieci web platformy Azure hello lub hello Monitor stanu na hoście usług IIS.)</span><span class="sxs-lookup"><span data-stu-id="c51ee-180">(Use hello appropriate method: either hello Azure web app control panel, or hello Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="c51ee-181">Przywraca wszelkich zmian, które należy wykonać w pliku .config hello.</span><span class="sxs-lookup"><span data-stu-id="c51ee-181">Reinstate any edits you performed on hello .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="c51ee-182">Rozwiązywanie problemów z konfiguracją środowiska uruchomieniowego usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="c51ee-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="c51ee-183">Nie można nawiązać połączenia?</span><span class="sxs-lookup"><span data-stu-id="c51ee-183">Can't connect?</span></span> <span data-ttu-id="c51ee-184">Brak telemetrii?</span><span class="sxs-lookup"><span data-stu-id="c51ee-184">No telemetry?</span></span>

* <span data-ttu-id="c51ee-185">Otwórz [hello niezbędne porty wychodzące](app-insights-ip-addresses.md#outgoing-ports) w toowork Monitor stanu tooallow zapory na serwerze.</span><span class="sxs-lookup"><span data-stu-id="c51ee-185">Open [hello necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall tooallow Status Monitor toowork.</span></span>

* <span data-ttu-id="c51ee-186">Otwórz monitor stanu i wybierz swoją aplikację w lewym okienku.</span><span class="sxs-lookup"><span data-stu-id="c51ee-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="c51ee-187">Sprawdź, czy istnieją jakiekolwiek komunikaty diagnostyczne dla tej aplikacji w sekcji "Konfiguracja powiadomienia" hello:</span><span class="sxs-lookup"><span data-stu-id="c51ee-187">Check if there are any diagnostics messages for this application in hello "Configuration notifications" section:</span></span>

  ![Otwórz hello wydajności bloku toosee żądania, czas odpowiedzi, zależności i innych danych](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="c51ee-189">Na serwerze hello Jeśli zostanie wyświetlony komunikat informujący o "niewystarczające uprawnienia", spróbuj następujących hello:</span><span class="sxs-lookup"><span data-stu-id="c51ee-189">On hello server, if you see a message about "insufficient permissions", try hello following:</span></span>
  * <span data-ttu-id="c51ee-190">W Menedżerze usług IIS wybierz pulę aplikacji, otwórz **Zaawansowane ustawienia**i w obszarze **Model procesu** należy zwrócić uwagę hello tożsamości.</span><span class="sxs-lookup"><span data-stu-id="c51ee-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note hello identity.</span></span>
  * <span data-ttu-id="c51ee-191">W Panelu sterowania Zarządzanie komputerem Dodaj tę grupę Użytkownicy monitora wydajności toohello tożsamości.</span><span class="sxs-lookup"><span data-stu-id="c51ee-191">In Computer management control panel, add this identity toohello Performance Monitor Users group.</span></span>
* <span data-ttu-id="c51ee-192">Jeśli na serwerze jest zainstalowany agent MMA/SCOM (Systems Center Operations Manager), niektóre wersje mogą powodować konflikt.</span><span class="sxs-lookup"><span data-stu-id="c51ee-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="c51ee-193">Odinstaluj zarówno SCOM i Monitor stanu i ponownie zainstalować najnowsze wersje hello.</span><span class="sxs-lookup"><span data-stu-id="c51ee-193">Uninstall both SCOM and Status Monitor, and re-install hello latest versions.</span></span>
* <span data-ttu-id="c51ee-194">Zobacz [Rozwiązywanie problemów][qna].</span><span class="sxs-lookup"><span data-stu-id="c51ee-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="c51ee-195">Wymagania systemu</span><span class="sxs-lookup"><span data-stu-id="c51ee-195">System Requirements</span></span>
<span data-ttu-id="c51ee-196">Serwerowe systemy operacyjne obsługiwane przez monitor stanu usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="c51ee-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="c51ee-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="c51ee-197">Windows Server 2008</span></span>
* <span data-ttu-id="c51ee-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c51ee-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="c51ee-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c51ee-199">Windows Server 2012</span></span>
* <span data-ttu-id="c51ee-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c51ee-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="c51ee-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c51ee-201">Windows Server 2016</span></span>

<span data-ttu-id="c51ee-202">z najnowszym dodatkiem SP oraz platformą .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="c51ee-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="c51ee-203">Po stronie klienta hello: Windows 7, 8, 8.1, 10, ponownie z programu .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="c51ee-203">On hello client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="c51ee-204">Obsługiwane wersje usług IIS: 7, 7.5, 8, 8.5 (usługi IIS są wymagane)</span><span class="sxs-lookup"><span data-stu-id="c51ee-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="c51ee-205">Automatyzacja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c51ee-205">Automation with PowerShell</span></span>
<span data-ttu-id="c51ee-206">Monitorowanie można uruchomić i zatrzymać przy użyciu programu PowerShell na serwerze usług IIS.</span><span class="sxs-lookup"><span data-stu-id="c51ee-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="c51ee-207">Najpierw zaimportować moduł usługi Application Insights hello:</span><span class="sxs-lookup"><span data-stu-id="c51ee-207">First import hello Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="c51ee-208">Dowiedz się, które aplikacje są monitorowane:</span><span class="sxs-lookup"><span data-stu-id="c51ee-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="c51ee-209">`-Name`Witaj (opcjonalnie) Nazwa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c51ee-209">`-Name` (Optional) hello name of a web app.</span></span>
* <span data-ttu-id="c51ee-210">Wyświetla hello monitorowania stanu usługi Application Insights dla każdej aplikacji sieci web (lub o nazwie aplikacji hello) na serwerze IIS.</span><span class="sxs-lookup"><span data-stu-id="c51ee-210">Displays hello Application Insights monitoring status for each web app (or hello named app) in this IIS server.</span></span>
* <span data-ttu-id="c51ee-211">Zwraca obiekt `ApplicationInsightsApplication` dla każdej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="c51ee-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="c51ee-212">`SdkState==EnabledAfterDeployment`: Aplikacja jest monitorowana i było instrumentowane w czasie wykonywania przez narzędzie Monitor stanu hello, lub `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="c51ee-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by hello Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="c51ee-213">`SdkState==Disabled`: aplikacja hello nie został zinstrumentowany na potrzeby usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c51ee-213">`SdkState==Disabled`: hello app is not instrumented for Application Insights.</span></span> <span data-ttu-id="c51ee-214">Nigdy nie było instrumentowane albo monitorowanie czasu wykonywania zostało wyłączone za pomocą narzędzia Monitor stanu hello lub z `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="c51ee-214">Either it was never instrumented, or run-time monitoring was disabled with hello Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="c51ee-215">`SdkState==EnabledByCodeInstrumentation`: aplikacja hello było instrumentowane przez dodanie hello SDK toohello źródła kodu.</span><span class="sxs-lookup"><span data-stu-id="c51ee-215">`SdkState==EnabledByCodeInstrumentation`: hello app was instrumented by adding hello SDK toohello source code.</span></span> <span data-ttu-id="c51ee-216">Nie można zaktualizować ani zatrzymać tego zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="c51ee-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="c51ee-217">`SdkVersion`Pokazuje hello wersja używana do monitorowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c51ee-217">`SdkVersion` shows hello version in use for monitoring this app.</span></span>
  * <span data-ttu-id="c51ee-218">`LatestAvailableSdkVersion`zawiera obecnie dostępna jest wersja hello hello galerii NuGet.</span><span class="sxs-lookup"><span data-stu-id="c51ee-218">`LatestAvailableSdkVersion`shows hello version currently available on hello NuGet gallery.</span></span> <span data-ttu-id="c51ee-219">Wersja toothis tooupgrade hello aplikacji, użyj `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="c51ee-219">tooupgrade hello app toothis version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="c51ee-220">`-Name`Nazwa Hello aplikacji hello w usługach IIS</span><span class="sxs-lookup"><span data-stu-id="c51ee-220">`-Name` hello name of hello app in IIS</span></span>
* <span data-ttu-id="c51ee-221">`-InstrumentationKey`Witaj ikey hello miejscu hello toobe wyniki wyświetlane zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c51ee-221">`-InstrumentationKey` hello ikey of hello Application Insights resource where you want hello results toobe displayed.</span></span>
* <span data-ttu-id="c51ee-222">To polecenie cmdlet dotyczy tylko aplikacji, dla których nie przeprowadzono jeszcze instrumentacji (czyli SdkState == NotInstrumented).</span><span class="sxs-lookup"><span data-stu-id="c51ee-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="c51ee-223">polecenia cmdlet Hello nie wpływa na aplikację, która jest już instrumentowany.</span><span class="sxs-lookup"><span data-stu-id="c51ee-223">hello cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="c51ee-224">Nie ma znaczenia, czy aplikacja hello było instrumentowane w czasie kompilacji przez dodanie hello SDK toohello kodu, ani nie na czas wykonywania przez poprzednie użycie tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c51ee-224">It does not matter whether hello app was instrumented at build time by adding hello SDK toohello code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="c51ee-225">Witaj SDK wersja użyta tooinstrument hello aplikacji jest hello wersji, która została ostatnio większości pobrane toothis serwera.</span><span class="sxs-lookup"><span data-stu-id="c51ee-225">hello SDK version used tooinstrument hello app is hello version that was most recently downloaded toothis server.</span></span>

    <span data-ttu-id="c51ee-226">toodownload hello najnowszą wersję, użyj ApplicationInsightsVersion aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="c51ee-226">toodownload hello latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="c51ee-227">Zwraca obiekt `ApplicationInsightsApplication` w przypadku powodzenia.</span><span class="sxs-lookup"><span data-stu-id="c51ee-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="c51ee-228">W przypadku niepowodzenia logowania toostderr śledzenia.</span><span class="sxs-lookup"><span data-stu-id="c51ee-228">If it fails, it logs a trace toostderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="c51ee-229">`-Name`Nazwa Hello aplikacji w usługach IIS</span><span class="sxs-lookup"><span data-stu-id="c51ee-229">`-Name` hello name of an app in IIS</span></span>
* <span data-ttu-id="c51ee-230">`-All` Zatrzymuje monitorowanie wszystkich aplikacji na tym serwerze usług IIS, dla których `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="c51ee-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="c51ee-231">Zatrzymuje monitorowanie hello określonych aplikacji i usuwa instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="c51ee-231">Stops monitoring hello specified apps and removes instrumentation.</span></span> <span data-ttu-id="c51ee-232">Działa tylko dla aplikacji, które zostały zinstrumentowane w czasie wykonywania za pomocą hello narzędzia do monitorowania stanu lub Start ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="c51ee-232">It only works for apps that have been instrumented at run-time using hello Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="c51ee-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="c51ee-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="c51ee-234">Zwraca obiekt ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="c51ee-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="c51ee-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="c51ee-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="c51ee-236">`-Name`: hello nazwę aplikacji sieci web w usługach IIS.</span><span class="sxs-lookup"><span data-stu-id="c51ee-236">`-Name`: hello name of a web app in IIS.</span></span>
* <span data-ttu-id="c51ee-237">`-InstrumentationKey` (opcjonalnie). Użycie wysłania tego toochange hello zasobów toowhich hello danych telemetrycznych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c51ee-237">`-InstrumentationKey` (Optional.) Use this toochange hello resource toowhich hello app's telemetry is sent.</span></span>
* <span data-ttu-id="c51ee-238">To polecenie cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c51ee-238">This cmdlet:</span></span>
  * <span data-ttu-id="c51ee-239">Hello uaktualnienia o nazwie toohello wersji aplikacji hello SDK ostatnio pobrana toothis maszyny.</span><span class="sxs-lookup"><span data-stu-id="c51ee-239">Upgrades hello named app toohello version of hello SDK most recently downloaded toothis machine.</span></span> <span data-ttu-id="c51ee-240">(Działa tylko wtedy, gdy `SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="c51ee-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="c51ee-241">Jeśli podasz klucza Instrumentacji o nazwie aplikacji hello jest ponownie skonfigurowanych toosend telemetrii toohello zasobów z tego klucza.</span><span class="sxs-lookup"><span data-stu-id="c51ee-241">If you provide an instrumentation key, hello named app is reconfigured toosend telemetry toohello resource with that key.</span></span> <span data-ttu-id="c51ee-242">(Działa, jeśli `SdkState != Disabled`)</span><span class="sxs-lookup"><span data-stu-id="c51ee-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="c51ee-243">Pobiera hello najnowszy zestaw SDK usługi Application Insights toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="c51ee-243">Downloads hello latest Application Insights SDK toohello server.</span></span>

## <span data-ttu-id="c51ee-244"><a name="questions"></a>Pytania dotyczące monitora stanu</span><span class="sxs-lookup"><span data-stu-id="c51ee-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="c51ee-245">Co to jest monitor stanu?</span><span class="sxs-lookup"><span data-stu-id="c51ee-245">What is Status Monitor?</span></span>

<span data-ttu-id="c51ee-246">Aplikacja klasyczna, która jest instalowana na serwerze sieci Web usług IIS.</span><span class="sxs-lookup"><span data-stu-id="c51ee-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="c51ee-247">Ułatwia ona instrumentację i konfigurowanie aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c51ee-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="c51ee-248">Kiedy należy używać monitora stanu?</span><span class="sxs-lookup"><span data-stu-id="c51ee-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="c51ee-249">tooinstrument dowolnej sieci web aplikacji, która jest uruchomiona na serwerze IIS — nawet wtedy, gdy jest już uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="c51ee-249">tooinstrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="c51ee-250">dodatkowe dane telemetryczne tooenable dla aplikacji sieci web, które zostały [skompilowanych przy użyciu zestawu SDK usługi Application Insights hello](app-insights-asp-net.md) w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c51ee-250">tooenable additional telemetry for web apps that have been [built with hello Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="c51ee-251">Czy można zamknąć go po uruchomieniu?</span><span class="sxs-lookup"><span data-stu-id="c51ee-251">Can I close it after it runs?</span></span>

<span data-ttu-id="c51ee-252">Tak.</span><span class="sxs-lookup"><span data-stu-id="c51ee-252">Yes.</span></span> <span data-ttu-id="c51ee-253">Po ma instrumentowane hello witryn sieci Web, którą wybierzesz możesz go zamknąć.</span><span class="sxs-lookup"><span data-stu-id="c51ee-253">After it has instrumented hello websites you select, you can close it.</span></span>

<span data-ttu-id="c51ee-254">Nie zbiera on telemetrii samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="c51ee-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="c51ee-255">Po prostu konfiguruje hello aplikacji sieci web i ustawia niektóre uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="c51ee-255">It just configures hello web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="c51ee-256">Co robi monitor stanu?</span><span class="sxs-lookup"><span data-stu-id="c51ee-256">What does Status Monitor do?</span></span>

<span data-ttu-id="c51ee-257">Po wybraniu aplikacji sieci web dla tooinstrument Monitor stanu:</span><span class="sxs-lookup"><span data-stu-id="c51ee-257">When you select a web app for Status Monitor tooinstrument:</span></span>

* <span data-ttu-id="c51ee-258">Pobiera i umieszcza hello zestawy usługi Application Insights i pliku .config w aplikacji sieci web hello folder plików binarnych.</span><span class="sxs-lookup"><span data-stu-id="c51ee-258">Downloads and places hello Application Insights assemblies and .config file in hello web app's binaries folder.</span></span>
* <span data-ttu-id="c51ee-259">Modyfikuje `web.config` tooadd hello Application Insights HTTP śledzenia modułu.</span><span class="sxs-lookup"><span data-stu-id="c51ee-259">Modifies `web.config` tooadd hello Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="c51ee-260">Włącza profilowanie wywołania zależności toocollect CLR.</span><span class="sxs-lookup"><span data-stu-id="c51ee-260">Enables CLR profiling toocollect dependency calls.</span></span>

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a><span data-ttu-id="c51ee-261">Należy toorun Monitor stanu zawsze, gdy zaktualizuję aplikacji hello?</span><span class="sxs-lookup"><span data-stu-id="c51ee-261">Do I need toorun Status Monitor whenever I update hello app?</span></span>

<span data-ttu-id="c51ee-262">Nie, jeśli ponowne wdrażanie odbywa się przyrostowo.</span><span class="sxs-lookup"><span data-stu-id="c51ee-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="c51ee-263">Wybranie opcji "Usuń istniejące pliki" hello w hello proces publikowania, będzie potrzebny toore Uruchom Monitor stanu tooconfigure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c51ee-263">If you select hello 'delete existing files' option in hello publish process, you would need toore-run Status Monitor tooconfigure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="c51ee-264">Jakie dane telemetrii są zbierane?</span><span class="sxs-lookup"><span data-stu-id="c51ee-264">What telemetry is collected?</span></span>

<span data-ttu-id="c51ee-265">W przypadku aplikacji z instrumentacją tylko w czasie wykonywania za pomocą monitora stanu:</span><span class="sxs-lookup"><span data-stu-id="c51ee-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="c51ee-266">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="c51ee-266">HTTP requests</span></span>
* <span data-ttu-id="c51ee-267">Wywołuje toodependencies</span><span class="sxs-lookup"><span data-stu-id="c51ee-267">Calls toodependencies</span></span>
* <span data-ttu-id="c51ee-268">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="c51ee-268">Exceptions</span></span>
* <span data-ttu-id="c51ee-269">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="c51ee-269">Performance counters</span></span>

<span data-ttu-id="c51ee-270">W przypadku aplikacji już instrumentowanych w czasie kompilacji:</span><span class="sxs-lookup"><span data-stu-id="c51ee-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="c51ee-271">Liczniki procesu.</span><span class="sxs-lookup"><span data-stu-id="c51ee-271">Process counters.</span></span>
 * <span data-ttu-id="c51ee-272">Wywołania zależności (.NET 4.5); wartości zwracane w wywołaniach zależności (.NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="c51ee-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="c51ee-273">Wartości śladu stosu wyjątków.</span><span class="sxs-lookup"><span data-stu-id="c51ee-273">Exception stack trace values.</span></span>

[<span data-ttu-id="c51ee-274">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="c51ee-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="c51ee-275">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="c51ee-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="c51ee-276"><a name="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c51ee-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="c51ee-277">Wyświetlanie telemetrii:</span><span class="sxs-lookup"><span data-stu-id="c51ee-277">View your telemetry:</span></span>

* <span data-ttu-id="c51ee-278">[Eksploruj metryki](app-insights-metrics-explorer.md) toomonitor wydajności i użycia</span><span class="sxs-lookup"><span data-stu-id="c51ee-278">[Explore metrics](app-insights-metrics-explorer.md) toomonitor performance and usage</span></span>
* <span data-ttu-id="c51ee-279">[Wyszukiwanie zdarzeń i dzienniki] [ diagnostic] toodiagnose problemów</span><span class="sxs-lookup"><span data-stu-id="c51ee-279">[Search events and logs][diagnostic] toodiagnose problems</span></span>
* <span data-ttu-id="c51ee-280">[Analiza](app-insights-analytics.md) dla bardziej zaawansowanych zapytań</span><span class="sxs-lookup"><span data-stu-id="c51ee-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="c51ee-281">Tworzenie pulpitów nawigacyjnych</span><span class="sxs-lookup"><span data-stu-id="c51ee-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="c51ee-282">Dodawanie kolejnych funkcji telemetrii:</span><span class="sxs-lookup"><span data-stu-id="c51ee-282">Add more telemetry:</span></span>

* <span data-ttu-id="c51ee-283">[Tworzenie testów sieci web] [ availability] toomake się, że witryna pozostaje na żywo.</span><span class="sxs-lookup"><span data-stu-id="c51ee-283">[Create web tests][availability] toomake sure your site stays live.</span></span>
* <span data-ttu-id="c51ee-284">[Dodaj telemetrię usługi sieci web klienta] [ usage] toosee wyjątki od kodu strony sieci web i toolet wstawiania śledzenia wywołań.</span><span class="sxs-lookup"><span data-stu-id="c51ee-284">[Add web client telemetry][usage] toosee exceptions from web page code and toolet you insert trace calls.</span></span>
* <span data-ttu-id="c51ee-285">[Dodaj kod, zestaw SDK usługi Application Insights tooyour] [ greenbrown] tak, aby można wstawiać śledzenia i rejestrowania zgłoszeń</span><span class="sxs-lookup"><span data-stu-id="c51ee-285">[Add Application Insights SDK tooyour code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
