---
title: "Monitorowanie działającej aplikacji sieci Web platformy ASP.NET za pomocą usługi Application Insights | Microsoft Docs"
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
ms.openlocfilehash: d07a0c81f89100c378456bbea8dca1c009cc8d77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="16aff-104">Instrumentowanie aplikacji sieci Web w czasie wykonywania za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="16aff-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="16aff-105">Możliwe jest instrumentowanie działającej aplikacji sieci Web za pomocą usługi Azure Application Insights bez konieczności modyfikowania kodu ani jego ponownego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="16aff-105">You can instrument a live web app with Azure Application Insights, without having to modify or redeploy your code.</span></span> <span data-ttu-id="16aff-106">Jeśli Twoje aplikacje są hostowane na lokalnym serwerze IIS, zainstaluj monitor stanu.</span><span class="sxs-lookup"><span data-stu-id="16aff-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="16aff-107">Jeśli są to aplikacje sieci Web platformy Azure lub jeśli działają one na maszynie wirtualnej platformy Azure, możesz włączyć monitorowanie usługi Application Insights z poziomu panelu sterowania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16aff-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from the Azure control panel.</span></span> <span data-ttu-id="16aff-108">Istnieją także osobne artykuły na temat instrumentacji [działających aplikacji sieci Web w technologii J2EE](app-insights-java-live.md) i [usług Azure Cloud Services](app-insights-cloudservices.md). Potrzebna jest subskrypcja platformy [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="16aff-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![przykładowe wykresy](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="16aff-110">Dostępne są trzy trasy zastosowania usługi Application Insights do aplikacji sieci Web platformy .NET:</span><span class="sxs-lookup"><span data-stu-id="16aff-110">You have a choice of three routes to apply Application Insights to your .NET web applications:</span></span>

* <span data-ttu-id="16aff-111">**W czasie kompilacji:** [dodaj zestaw Application Insights SDK][greenbrown] do kodu aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="16aff-111">**Build time:** [Add the Application Insights SDK][greenbrown] to your web app code.</span></span>
* <span data-ttu-id="16aff-112">**W czasie wykonywania:** przeprowadź instrumentację aplikacji sieci Web na serwerze, jak opisano poniżej, bez konieczności ponownego kompilowania lub wdrażania kodu.</span><span class="sxs-lookup"><span data-stu-id="16aff-112">**Run time:** Instrument your web app on the server, as described below, without rebuilding and redeploying the code.</span></span>
* <span data-ttu-id="16aff-113">**W czasie kompilacji i w czasie wykonywania:** skompiluj zestaw SDK w kodzie aplikacji sieci Web, a także zastosuj rozszerzenia czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="16aff-113">**Both:** Build the SDK into your web app code, and also apply the run-time extensions.</span></span> <span data-ttu-id="16aff-114">Połącz korzyści z obu opcji.</span><span class="sxs-lookup"><span data-stu-id="16aff-114">Get the best of both options.</span></span>

<span data-ttu-id="16aff-115">Poniżej przedstawiono podsumowanie tego, co można uzyskać, korzystając z danej trasy:</span><span class="sxs-lookup"><span data-stu-id="16aff-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="16aff-116">W czasie kompilacji</span><span class="sxs-lookup"><span data-stu-id="16aff-116">Build time</span></span> | <span data-ttu-id="16aff-117">W czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="16aff-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16aff-118">Żądania i wyjątki</span><span class="sxs-lookup"><span data-stu-id="16aff-118">Requests & exceptions</span></span> |<span data-ttu-id="16aff-119">Tak</span><span class="sxs-lookup"><span data-stu-id="16aff-119">Yes</span></span> |<span data-ttu-id="16aff-120">Tak</span><span class="sxs-lookup"><span data-stu-id="16aff-120">Yes</span></span> |
| [<span data-ttu-id="16aff-121">Bardziej szczegółowe wyjątki</span><span class="sxs-lookup"><span data-stu-id="16aff-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="16aff-122">Tak</span><span class="sxs-lookup"><span data-stu-id="16aff-122">Yes</span></span> |
| [<span data-ttu-id="16aff-123">Diagnostyka zależności</span><span class="sxs-lookup"><span data-stu-id="16aff-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="16aff-124">Na platformie .NET 4.6 +, ale mniej szczegółów</span><span class="sxs-lookup"><span data-stu-id="16aff-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="16aff-125">Tak, kompletne szczegóły: kody wyników, tekst polecenia SQL, czasownik HTTP</span><span class="sxs-lookup"><span data-stu-id="16aff-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="16aff-126">Liczniki wydajności sytemu</span><span class="sxs-lookup"><span data-stu-id="16aff-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="16aff-127">Tak</span><span class="sxs-lookup"><span data-stu-id="16aff-127">Yes</span></span> |<span data-ttu-id="16aff-128">Tak</span><span class="sxs-lookup"><span data-stu-id="16aff-128">Yes</span></span> |
| <span data-ttu-id="16aff-129">[Interfejs API dla telemetrii niestandardowej][api]</span><span class="sxs-lookup"><span data-stu-id="16aff-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="16aff-130">Tak</span><span class="sxs-lookup"><span data-stu-id="16aff-130">Yes</span></span> |<span data-ttu-id="16aff-131">Nie</span><span class="sxs-lookup"><span data-stu-id="16aff-131">No</span></span> |
| [<span data-ttu-id="16aff-132">Integracja dziennika śledzenia</span><span class="sxs-lookup"><span data-stu-id="16aff-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="16aff-133">Tak</span><span class="sxs-lookup"><span data-stu-id="16aff-133">Yes</span></span> |<span data-ttu-id="16aff-134">Nie</span><span class="sxs-lookup"><span data-stu-id="16aff-134">No</span></span> |
| [<span data-ttu-id="16aff-135">Widok strony i dane użytkownika</span><span class="sxs-lookup"><span data-stu-id="16aff-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="16aff-136">Tak</span><span class="sxs-lookup"><span data-stu-id="16aff-136">Yes</span></span> |<span data-ttu-id="16aff-137">Nie</span><span class="sxs-lookup"><span data-stu-id="16aff-137">No</span></span> |
| <span data-ttu-id="16aff-138">Konieczność ponownej kompilacji kodu</span><span class="sxs-lookup"><span data-stu-id="16aff-138">Need to rebuild code</span></span> |<span data-ttu-id="16aff-139">Tak</span><span class="sxs-lookup"><span data-stu-id="16aff-139">Yes</span></span> | <span data-ttu-id="16aff-140">Nie</span><span class="sxs-lookup"><span data-stu-id="16aff-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="16aff-141">Monitorowanie działającej aplikacji sieci Web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="16aff-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="16aff-142">Jeśli aplikacja działa jako usługa sieci Web platformy Azure, monitorowanie należy włączyć w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="16aff-142">If your application is running as an Azure web service, here's how to switch on monitoring:</span></span>

* <span data-ttu-id="16aff-143">Wybierz usługę Application Insights w panelu sterowania aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="16aff-143">Select Application Insights on the app's control panel in Azure.</span></span>

    ![Konfigurowanie usługi Application Insights dla aplikacji sieci Web platformy Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="16aff-145">Gdy zostanie otwarta strona podsumowania usługi Application Insights, kliknij link w dolnej części, aby otworzyć pełny zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="16aff-145">When the Application Insights summary page opens, click the link at the bottom to open the full Application Insights resource.</span></span>

    ![Klikaj elementy, aż przejdziesz do usługi Application Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="16aff-147">[Monitorowanie aplikacji w chmurze i na maszynie wirtualnej](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="16aff-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="16aff-148">Włączanie monitorowania po stronie klienta na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="16aff-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="16aff-149">Po włączeniu usługi Application Insights na platformie Azure możesz dodać telemetrię widoku strony i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="16aff-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="16aff-150">Wybierz kolejno pozycje Ustawienia > Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="16aff-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="16aff-151">W obszarze Ustawienia aplikacji dodaj nową parę klucz-wartość:</span><span class="sxs-lookup"><span data-stu-id="16aff-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="16aff-152">Klucz: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="16aff-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="16aff-153">Wartość:`true`</span><span class="sxs-lookup"><span data-stu-id="16aff-153">Value: `true`</span></span>
3. <span data-ttu-id="16aff-154">**Zapisz** ustawienia i **ponownie uruchom** aplikację.</span><span class="sxs-lookup"><span data-stu-id="16aff-154">**Save** the settings and **Restart** your app.</span></span>

<span data-ttu-id="16aff-155">Zestaw SDK języka JavaScript usługi Application Insights został teraz wprowadzony do każdej strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="16aff-155">The Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="16aff-156">Monitorowanie działającej aplikacji sieci Web usług IIS</span><span class="sxs-lookup"><span data-stu-id="16aff-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="16aff-157">Jeśli aplikacja jest hostowana na serwerze usług IIS, włącz usługę Application Insights przy użyciu monitora stanu.</span><span class="sxs-lookup"><span data-stu-id="16aff-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="16aff-158">Zaloguj się na serwerze sieci Web usług IIS, używając poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="16aff-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="16aff-159">Jeśli monitor stanu usługi Application Insights nie został jeszcze zainstalowany, pobierz i uruchom [Instalator monitora stanu](http://go.microsoft.com/fwlink/?LinkId=506648) (lub uruchom [Instalator platformy sieci Web](https://www.microsoft.com/web/downloads/platform.aspx) i wyszukaj w nim monitor stanu usługi Application Insights).</span><span class="sxs-lookup"><span data-stu-id="16aff-159">If Application Insights Status Monitor is not already installed, download and run the [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="16aff-160">W monitorze stanu wybierz zainstalowaną aplikację sieci Web lub witrynę sieci Web, którą chcesz monitorować.</span><span class="sxs-lookup"><span data-stu-id="16aff-160">In Status Monitor, select the installed web application or website that you want to monitor.</span></span> <span data-ttu-id="16aff-161">Zaloguj się przy użyciu poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16aff-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="16aff-162">Skonfiguruj zasób, w którym mają być wyświetlane wyniki w portalu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="16aff-162">Configure the resource where you want to see the results in the Application Insights portal.</span></span> <span data-ttu-id="16aff-163">(Zazwyczaj najlepiej jest utworzyć nowy zasób.</span><span class="sxs-lookup"><span data-stu-id="16aff-163">(Normally, it's best to create a new resource.</span></span> <span data-ttu-id="16aff-164">Wybierz istniejący zasób, jeśli masz już [testy sieci Web][availability] lub [monitorowanie klienta][client] dla tej aplikacji).</span><span class="sxs-lookup"><span data-stu-id="16aff-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Wybór aplikacji i zasobu.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="16aff-166">Uruchom ponownie usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="16aff-166">Restart IIS.</span></span>

    ![Wybór opcji Uruchom ponownie w górnej części okna dialogowego.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="16aff-168">Działanie usługi sieci Web zostanie na krótko przerwane.</span><span class="sxs-lookup"><span data-stu-id="16aff-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="16aff-169">Dostosowywanie opcji monitorowania</span><span class="sxs-lookup"><span data-stu-id="16aff-169">Customize monitoring options</span></span>

<span data-ttu-id="16aff-170">Włączenie usługi Application Insights powoduje dodanie plików DLL i pliku ApplicationInsights.config do aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="16aff-170">Enabling Application Insights adds DLLs and ApplicationInsights.config to your web app.</span></span> <span data-ttu-id="16aff-171">Możesz [edytować plik config](app-insights-configuration-with-applicationinsights-config.md), aby zmienić niektóre opcje.</span><span class="sxs-lookup"><span data-stu-id="16aff-171">You can [edit the .config file](app-insights-configuration-with-applicationinsights-config.md) to change some of the options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="16aff-172">Po ponownym opublikowaniu aplikacji ponownie włącz usługę Application Insights</span><span class="sxs-lookup"><span data-stu-id="16aff-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="16aff-173">Przed ponownym opublikowaniem aplikacji rozważ [dodanie usługi Application Insights do kodu w programie Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="16aff-173">Before you re-publish your app, consider [adding Application Insights to the code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="16aff-174">Uzyskasz bardziej szczegółowe dane telemetryczne oraz możliwość zapisywania niestandardowych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="16aff-174">You'll get more detailed telemetry and the ability to write custom telemetry.</span></span>

<span data-ttu-id="16aff-175">Jeśli chcesz ponownie przeprowadzić publikację bez dodawania usługi Application Insights do kodu, pamiętaj, że proces wdrażania może spowodować usunięcie plików DLL i pliku Application Insights z opublikowanej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="16aff-175">If you want to re-publish without adding Application Insights to the code, be aware that the deployment process may delete the DLLs and ApplicationInsights.config from the published web site.</span></span> <span data-ttu-id="16aff-176">Zatem:</span><span class="sxs-lookup"><span data-stu-id="16aff-176">Therefore:</span></span>

1. <span data-ttu-id="16aff-177">Jeśli edytowano plik ApplicationInsights.config, utwórz jego kopię przed ponownym opublikowaniem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16aff-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="16aff-178">Ponownie opublikuj aplikację.</span><span class="sxs-lookup"><span data-stu-id="16aff-178">Republish your app.</span></span>
3. <span data-ttu-id="16aff-179">Ponownie włącz monitorowanie za pomocą usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="16aff-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="16aff-180">(Użyj odpowiedniej metody: panelu sterowania aplikacji sieci Web platformy Azure lub monitora stanu na hoście usług IIS).</span><span class="sxs-lookup"><span data-stu-id="16aff-180">(Use the appropriate method: either the Azure web app control panel, or the Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="16aff-181">Przywróć wszystkie zmiany wprowadzone w pliku config.</span><span class="sxs-lookup"><span data-stu-id="16aff-181">Reinstate any edits you performed on the .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="16aff-182">Rozwiązywanie problemów z konfiguracją środowiska uruchomieniowego usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="16aff-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="16aff-183">Nie można nawiązać połączenia?</span><span class="sxs-lookup"><span data-stu-id="16aff-183">Can't connect?</span></span> <span data-ttu-id="16aff-184">Brak telemetrii?</span><span class="sxs-lookup"><span data-stu-id="16aff-184">No telemetry?</span></span>

* <span data-ttu-id="16aff-185">Aby umożliwić działanie monitora stanu, na zaporze serwera otwórz [wymagane porty wychodzące](app-insights-ip-addresses.md#outgoing-ports).</span><span class="sxs-lookup"><span data-stu-id="16aff-185">Open [the necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall to allow Status Monitor to work.</span></span>

* <span data-ttu-id="16aff-186">Otwórz monitor stanu i wybierz swoją aplikację w lewym okienku.</span><span class="sxs-lookup"><span data-stu-id="16aff-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="16aff-187">Sprawdź, czy w sekcji „Powiadomienia konfiguracyjne” występują komunikaty diagnostyczne dotyczące tej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="16aff-187">Check if there are any diagnostics messages for this application in the "Configuration notifications" section:</span></span>

  ![Otwórz blok Wydajność, aby zobaczyć żądanie, czas odpowiedzi, zależności i inne dane](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="16aff-189">Jeśli na serwerze zostanie wyświetlony komunikat o „niewystarczających uprawnieniach”, spróbuj wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="16aff-189">On the server, if you see a message about "insufficient permissions", try the following:</span></span>
  * <span data-ttu-id="16aff-190">W Menedżerze usług IIS wybierz pulę aplikacji, otwórz **Ustawienia zaawansowane** i zapamiętaj tożsamość w obszarze **Model procesu**.</span><span class="sxs-lookup"><span data-stu-id="16aff-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note the identity.</span></span>
  * <span data-ttu-id="16aff-191">W panelu sterowania Zarządzanie komputerem dodaj tę tożsamość do grupy Użytkownicy monitora wydajności.</span><span class="sxs-lookup"><span data-stu-id="16aff-191">In Computer management control panel, add this identity to the Performance Monitor Users group.</span></span>
* <span data-ttu-id="16aff-192">Jeśli na serwerze jest zainstalowany agent MMA/SCOM (Systems Center Operations Manager), niektóre wersje mogą powodować konflikt.</span><span class="sxs-lookup"><span data-stu-id="16aff-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="16aff-193">Odinstaluj oprogramowanie SCOM i monitor stanu, a następnie ponownie zainstaluj najnowsze wersje.</span><span class="sxs-lookup"><span data-stu-id="16aff-193">Uninstall both SCOM and Status Monitor, and re-install the latest versions.</span></span>
* <span data-ttu-id="16aff-194">Zobacz [Rozwiązywanie problemów][qna].</span><span class="sxs-lookup"><span data-stu-id="16aff-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="16aff-195">Wymagania systemu</span><span class="sxs-lookup"><span data-stu-id="16aff-195">System Requirements</span></span>
<span data-ttu-id="16aff-196">Serwerowe systemy operacyjne obsługiwane przez monitor stanu usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="16aff-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="16aff-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="16aff-197">Windows Server 2008</span></span>
* <span data-ttu-id="16aff-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="16aff-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="16aff-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="16aff-199">Windows Server 2012</span></span>
* <span data-ttu-id="16aff-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="16aff-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="16aff-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="16aff-201">Windows Server 2016</span></span>

<span data-ttu-id="16aff-202">z najnowszym dodatkiem SP oraz platformą .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="16aff-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="16aff-203">Po stronie klienta: systemy Windows 7, 8, 8.1 i 10, również z programem .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="16aff-203">On the client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="16aff-204">Obsługiwane wersje usług IIS: 7, 7.5, 8, 8.5 (usługi IIS są wymagane)</span><span class="sxs-lookup"><span data-stu-id="16aff-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="16aff-205">Automatyzacja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="16aff-205">Automation with PowerShell</span></span>
<span data-ttu-id="16aff-206">Monitorowanie można uruchomić i zatrzymać przy użyciu programu PowerShell na serwerze usług IIS.</span><span class="sxs-lookup"><span data-stu-id="16aff-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="16aff-207">Najpierw zaimportuj moduł Application Insights:</span><span class="sxs-lookup"><span data-stu-id="16aff-207">First import the Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="16aff-208">Dowiedz się, które aplikacje są monitorowane:</span><span class="sxs-lookup"><span data-stu-id="16aff-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="16aff-209">`-Name` Nazwa aplikacji sieci Web (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="16aff-209">`-Name` (Optional) The name of a web app.</span></span>
* <span data-ttu-id="16aff-210">Wyświetla stan monitorowania usługi Application Insights dla każdej (lub wskazanej z nazwy) aplikacji sieci Web na tym serwerze usług IIS.</span><span class="sxs-lookup"><span data-stu-id="16aff-210">Displays the Application Insights monitoring status for each web app (or the named app) in this IIS server.</span></span>
* <span data-ttu-id="16aff-211">Zwraca obiekt `ApplicationInsightsApplication` dla każdej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="16aff-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="16aff-212">`SdkState==EnabledAfterDeployment`: aplikacja jest monitorowana, a instrumentacja została przeprowadzona w czasie wykonywania za pomocą narzędzia Monitor stanu lub polecenia `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="16aff-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by the Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="16aff-213">`SdkState==Disabled`: nie ma instrumentacji aplikacji dla usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="16aff-213">`SdkState==Disabled`: The app is not instrumented for Application Insights.</span></span> <span data-ttu-id="16aff-214">Instrumentacja nie została nigdy przeprowadzona albo monitorowanie czasu wykonywania zostało wyłączone za pomocą monitora stanu lub polecenia `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="16aff-214">Either it was never instrumented, or run-time monitoring was disabled with the Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="16aff-215">`SdkState==EnabledByCodeInstrumentation`: wykonano instrumentację aplikacji przez dodanie zestawu SDK do kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="16aff-215">`SdkState==EnabledByCodeInstrumentation`: The app was instrumented by adding the SDK to the source code.</span></span> <span data-ttu-id="16aff-216">Nie można zaktualizować ani zatrzymać tego zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="16aff-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="16aff-217">Zestaw `SdkVersion` wyświetla wersję używaną do monitorowania tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16aff-217">`SdkVersion` shows the version in use for monitoring this app.</span></span>
  * <span data-ttu-id="16aff-218">Zestaw `LatestAvailableSdkVersion` wyświetla wersję aktualnie dostępną w galerii NuGet.</span><span class="sxs-lookup"><span data-stu-id="16aff-218">`LatestAvailableSdkVersion`shows the version currently available on the NuGet gallery.</span></span> <span data-ttu-id="16aff-219">Aby uaktualnić aplikację do tej wersji, użyj polecenia `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="16aff-219">To upgrade the app to this version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="16aff-220">`-Name` Nazwa aplikacji w usługach IIS</span><span class="sxs-lookup"><span data-stu-id="16aff-220">`-Name` The name of the app in IIS</span></span>
* <span data-ttu-id="16aff-221">`-InstrumentationKey` Klucz instrumentacji zasobu usługi Application Insights, w którym mają być wyświetlane wyniki.</span><span class="sxs-lookup"><span data-stu-id="16aff-221">`-InstrumentationKey` The ikey of the Application Insights resource where you want the results to be displayed.</span></span>
* <span data-ttu-id="16aff-222">To polecenie cmdlet dotyczy tylko aplikacji, dla których nie przeprowadzono jeszcze instrumentacji (czyli SdkState == NotInstrumented).</span><span class="sxs-lookup"><span data-stu-id="16aff-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="16aff-223">To polecenie cmdlet nie ma wpływu na aplikację, dla której przeprowadzono już instrumentację.</span><span class="sxs-lookup"><span data-stu-id="16aff-223">The cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="16aff-224">Nie ma znaczenia, czy instrumentacji aplikacji dokonano w czasie kompilacji przez dodanie zestawu SDK do kodu, czy w czasie wykonywania przez wcześniejsze użycie tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="16aff-224">It does not matter whether the app was instrumented at build time by adding the SDK to the code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="16aff-225">Wersja zestawu SDK użyta do instrumentacji aplikacji to wersja, która została ostatnio pobrana na ten serwer.</span><span class="sxs-lookup"><span data-stu-id="16aff-225">The SDK version used to instrument the app is the version that was most recently downloaded to this server.</span></span>

    <span data-ttu-id="16aff-226">Aby pobrać najnowszą wersję, użyj polecenia cmdlet Update-ApplicationInsightsVersion.</span><span class="sxs-lookup"><span data-stu-id="16aff-226">To download the latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="16aff-227">Zwraca obiekt `ApplicationInsightsApplication` w przypadku powodzenia.</span><span class="sxs-lookup"><span data-stu-id="16aff-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="16aff-228">W razie niepowodzenia rejestruje ślad do stderr.</span><span class="sxs-lookup"><span data-stu-id="16aff-228">If it fails, it logs a trace to stderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="16aff-229">`-Name` Nazwa aplikacji w usługach IIS</span><span class="sxs-lookup"><span data-stu-id="16aff-229">`-Name` The name of an app in IIS</span></span>
* <span data-ttu-id="16aff-230">`-All` Zatrzymuje monitorowanie wszystkich aplikacji na tym serwerze usług IIS, dla których `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="16aff-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="16aff-231">Zatrzymuje monitorowanie określonych aplikacji i usuwa instrumentację.</span><span class="sxs-lookup"><span data-stu-id="16aff-231">Stops monitoring the specified apps and removes instrumentation.</span></span> <span data-ttu-id="16aff-232">Działa to tylko w przypadku aplikacji, które zostały zinstrumentowane w czasie wykonywania za pomocą monitora stanu lub polecenia cmdlet Start-ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="16aff-232">It only works for apps that have been instrumented at run-time using the Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="16aff-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="16aff-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="16aff-234">Zwraca obiekt ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="16aff-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="16aff-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="16aff-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="16aff-236">`-Name`: nazwa aplikacji sieci Web w usługach IIS.</span><span class="sxs-lookup"><span data-stu-id="16aff-236">`-Name`: The name of a web app in IIS.</span></span>
* <span data-ttu-id="16aff-237">`-InstrumentationKey` (opcjonalnie). umożliwia zmianę zasobu, do którego wysyłana jest telemetria aplikacji.</span><span class="sxs-lookup"><span data-stu-id="16aff-237">`-InstrumentationKey` (Optional.) Use this to change the resource to which the app's telemetry is sent.</span></span>
* <span data-ttu-id="16aff-238">To polecenie cmdlet:</span><span class="sxs-lookup"><span data-stu-id="16aff-238">This cmdlet:</span></span>
  * <span data-ttu-id="16aff-239">Uaktualnia wskazaną aplikację do ostatniej wersji zestawu SDK pobranej na ten komputer.</span><span class="sxs-lookup"><span data-stu-id="16aff-239">Upgrades the named app to the version of the SDK most recently downloaded to this machine.</span></span> <span data-ttu-id="16aff-240">(Działa tylko wtedy, gdy `SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="16aff-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="16aff-241">Jeśli zostanie wprowadzony klucz instrumentacji, wskazana aplikacja jest konfigurowana ponownie do wysłania telemetrii do zasobu dotyczącego tego klucza.</span><span class="sxs-lookup"><span data-stu-id="16aff-241">If you provide an instrumentation key, the named app is reconfigured to send telemetry to the resource with that key.</span></span> <span data-ttu-id="16aff-242">(Działa, jeśli `SdkState != Disabled`)</span><span class="sxs-lookup"><span data-stu-id="16aff-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="16aff-243">Pobiera na serwer najnowszy zestaw SDK usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="16aff-243">Downloads the latest Application Insights SDK to the server.</span></span>

## <span data-ttu-id="16aff-244"><a name="questions"></a>Pytania dotyczące monitora stanu</span><span class="sxs-lookup"><span data-stu-id="16aff-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="16aff-245">Co to jest monitor stanu?</span><span class="sxs-lookup"><span data-stu-id="16aff-245">What is Status Monitor?</span></span>

<span data-ttu-id="16aff-246">Aplikacja klasyczna, która jest instalowana na serwerze sieci Web usług IIS.</span><span class="sxs-lookup"><span data-stu-id="16aff-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="16aff-247">Ułatwia ona instrumentację i konfigurowanie aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="16aff-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="16aff-248">Kiedy należy używać monitora stanu?</span><span class="sxs-lookup"><span data-stu-id="16aff-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="16aff-249">Do instrumentacji dowolnej aplikacji sieci Web uruchamianej na serwerze usług IIS — nawet jeśli już działa.</span><span class="sxs-lookup"><span data-stu-id="16aff-249">To instrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="16aff-250">Aby włączyć dodatkową telemetrię dla aplikacji sieci Web, które zostały [skompilowane przy użyciu zestawu SDK usługi Application Insights](app-insights-asp-net.md) w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="16aff-250">To enable additional telemetry for web apps that have been [built with the Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="16aff-251">Czy można zamknąć go po uruchomieniu?</span><span class="sxs-lookup"><span data-stu-id="16aff-251">Can I close it after it runs?</span></span>

<span data-ttu-id="16aff-252">Tak.</span><span class="sxs-lookup"><span data-stu-id="16aff-252">Yes.</span></span> <span data-ttu-id="16aff-253">Możesz zamknąć go po zakończeniu instrumentacji wybranych witryn sieci Web.</span><span class="sxs-lookup"><span data-stu-id="16aff-253">After it has instrumented the websites you select, you can close it.</span></span>

<span data-ttu-id="16aff-254">Nie zbiera on telemetrii samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="16aff-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="16aff-255">Po prostu konfiguruje aplikacje sieci Web i ustawia niektóre uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="16aff-255">It just configures the web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="16aff-256">Co robi monitor stanu?</span><span class="sxs-lookup"><span data-stu-id="16aff-256">What does Status Monitor do?</span></span>

<span data-ttu-id="16aff-257">Po wybraniu aplikacji sieci Web do instrumentacji za pomocą monitora stanu:</span><span class="sxs-lookup"><span data-stu-id="16aff-257">When you select a web app for Status Monitor to instrument:</span></span>

* <span data-ttu-id="16aff-258">Pobiera i umieszcza zestawy usługi Application Insights i pliku config w folderze plików binarnych aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="16aff-258">Downloads and places the Application Insights assemblies and .config file in the web app's binaries folder.</span></span>
* <span data-ttu-id="16aff-259">Modyfikuje plik `web.config` w celu dodania modułu śledzenia protokołu HTTP usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="16aff-259">Modifies `web.config` to add the Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="16aff-260">Umożliwia profilowanie aparatu CLR w celu gromadzenia wywołań zależności.</span><span class="sxs-lookup"><span data-stu-id="16aff-260">Enables CLR profiling to collect dependency calls.</span></span>

### <a name="do-i-need-to-run-status-monitor-whenever-i-update-the-app"></a><span data-ttu-id="16aff-261">Czy monitor stanu należy uruchamiać podczas każdej aktualizacji aplikacji?</span><span class="sxs-lookup"><span data-stu-id="16aff-261">Do I need to run Status Monitor whenever I update the app?</span></span>

<span data-ttu-id="16aff-262">Nie, jeśli ponowne wdrażanie odbywa się przyrostowo.</span><span class="sxs-lookup"><span data-stu-id="16aff-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="16aff-263">Jeśli w procesie publikowania wybierzesz opcję usuwania istniejących plików, trzeba będzie ponownie uruchomić monitor stanu w celu skonfigurowania usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="16aff-263">If you select the 'delete existing files' option in the publish process, you would need to re-run Status Monitor to configure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="16aff-264">Jakie dane telemetrii są zbierane?</span><span class="sxs-lookup"><span data-stu-id="16aff-264">What telemetry is collected?</span></span>

<span data-ttu-id="16aff-265">W przypadku aplikacji z instrumentacją tylko w czasie wykonywania za pomocą monitora stanu:</span><span class="sxs-lookup"><span data-stu-id="16aff-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="16aff-266">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="16aff-266">HTTP requests</span></span>
* <span data-ttu-id="16aff-267">Wywołania do zależności</span><span class="sxs-lookup"><span data-stu-id="16aff-267">Calls to dependencies</span></span>
* <span data-ttu-id="16aff-268">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="16aff-268">Exceptions</span></span>
* <span data-ttu-id="16aff-269">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="16aff-269">Performance counters</span></span>

<span data-ttu-id="16aff-270">W przypadku aplikacji już instrumentowanych w czasie kompilacji:</span><span class="sxs-lookup"><span data-stu-id="16aff-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="16aff-271">Liczniki procesu.</span><span class="sxs-lookup"><span data-stu-id="16aff-271">Process counters.</span></span>
 * <span data-ttu-id="16aff-272">Wywołania zależności (.NET 4.5); wartości zwracane w wywołaniach zależności (.NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="16aff-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="16aff-273">Wartości śladu stosu wyjątków.</span><span class="sxs-lookup"><span data-stu-id="16aff-273">Exception stack trace values.</span></span>

[<span data-ttu-id="16aff-274">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="16aff-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="16aff-275">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="16aff-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="16aff-276"><a name="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16aff-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="16aff-277">Wyświetlanie telemetrii:</span><span class="sxs-lookup"><span data-stu-id="16aff-277">View your telemetry:</span></span>

* <span data-ttu-id="16aff-278">[Eksplorowanie metryk](app-insights-metrics-explorer.md) w celu monitorowania wydajności i użycia</span><span class="sxs-lookup"><span data-stu-id="16aff-278">[Explore metrics](app-insights-metrics-explorer.md) to monitor performance and usage</span></span>
* <span data-ttu-id="16aff-279">[Wyszukiwanie zdarzeń i dzienników][diagnostic] w celu diagnozowania problemów</span><span class="sxs-lookup"><span data-stu-id="16aff-279">[Search events and logs][diagnostic] to diagnose problems</span></span>
* <span data-ttu-id="16aff-280">[Analiza](app-insights-analytics.md) dla bardziej zaawansowanych zapytań</span><span class="sxs-lookup"><span data-stu-id="16aff-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="16aff-281">Tworzenie pulpitów nawigacyjnych</span><span class="sxs-lookup"><span data-stu-id="16aff-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="16aff-282">Dodawanie kolejnych funkcji telemetrii:</span><span class="sxs-lookup"><span data-stu-id="16aff-282">Add more telemetry:</span></span>

* <span data-ttu-id="16aff-283">[Tworzenie testów sieci Web][availability], aby upewnić się, że witryna pozostaje aktywna.</span><span class="sxs-lookup"><span data-stu-id="16aff-283">[Create web tests][availability] to make sure your site stays live.</span></span>
* <span data-ttu-id="16aff-284">[Dodawanie telemetrii klienta sieci Web][usage], aby zobaczyć wyjątki pochodzące z kodu strony sieci Web i umożliwić wstawianie wywołań śladu.</span><span class="sxs-lookup"><span data-stu-id="16aff-284">[Add web client telemetry][usage] to see exceptions from web page code and to let you insert trace calls.</span></span>
* <span data-ttu-id="16aff-285">[Dodawanie zestawu SDK usługi Application Insights do kodu][greenbrown], aby móc wstawić ślad i rejestrować wywołania.</span><span class="sxs-lookup"><span data-stu-id="16aff-285">[Add Application Insights SDK to your code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
