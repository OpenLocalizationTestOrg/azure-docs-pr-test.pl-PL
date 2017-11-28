---
title: "Zła brama aaaFix 502, 503 obsługi błędów niedostępności | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z 502 Niewłaściwa brama i 503 błędów niedostępności usługi w aplikacji sieci web hostowanych w usłudze Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "Zła brama 502, 503 usługi niedostępne, błąd 503, błąd 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="ba709-104">Rozwiązywanie błędów HTTP "502 Niewłaściwa brama" i "503 Usługa niedostępna" w aplikacjach sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ba709-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="ba709-105">"brama zły 502" i "503 Usługa niedostępna" są typowe błędy w aplikacji sieci web hostowanych w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ba709-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="ba709-106">Ten artykuł pomoże w rozwiązaniu tych błędów.</span><span class="sxs-lookup"><span data-stu-id="ba709-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="ba709-107">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello MSDN Azure i hello przepełnienie stosu fora](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="ba709-107">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="ba709-108">Alternatywnie można również pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ba709-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="ba709-109">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz polecenie **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="ba709-109">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="ba709-110">Objaw</span><span class="sxs-lookup"><span data-stu-id="ba709-110">Symptom</span></span>
<span data-ttu-id="ba709-111">Podczas przeglądania aplikacji sieci web toohello zwraca HTTP HTTP lub błąd "502 Niewłaściwa brama" błąd "503 Usługa niedostępna".</span><span class="sxs-lookup"><span data-stu-id="ba709-111">When you browse toohello web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="ba709-112">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="ba709-112">Cause</span></span>
<span data-ttu-id="ba709-113">Ten problem jest często spowodowane przez problemy z poziomu aplikacji, takich jak:</span><span class="sxs-lookup"><span data-stu-id="ba709-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="ba709-114">żądania zbyt długo</span><span class="sxs-lookup"><span data-stu-id="ba709-114">requests taking a long time</span></span>
* <span data-ttu-id="ba709-115">aplikacji przy użyciu pamięci wysokiej/procesora CPU</span><span class="sxs-lookup"><span data-stu-id="ba709-115">application using high memory/CPU</span></span>
* <span data-ttu-id="ba709-116">Aplikacja awarii z powodu wyjątku tooan.</span><span class="sxs-lookup"><span data-stu-id="ba709-116">application crashing due tooan exception.</span></span>

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="ba709-117">Rozwiązywanie problemów z kroki toosolve "502 Niewłaściwa brama" i "503 Usługa niedostępna" błędy</span><span class="sxs-lookup"><span data-stu-id="ba709-117">Troubleshooting steps toosolve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="ba709-118">Rozwiązywanie problemów, można podzielić na trzy różne zadania, w kolejności sekwencyjnej:</span><span class="sxs-lookup"><span data-stu-id="ba709-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="ba709-119">Sprawdź i monitorowanie zachowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="ba709-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="ba709-120">Zbieranie danych</span><span class="sxs-lookup"><span data-stu-id="ba709-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="ba709-121">Ograniczenia hello problem</span><span class="sxs-lookup"><span data-stu-id="ba709-121">Mitigate hello issue</span></span>](#mitigate)

<span data-ttu-id="ba709-122">[Aplikacje sieci Web usługi aplikacji](/services/app-service/web/) zapewnia różne opcje w każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="ba709-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="ba709-123">1. Sprawdź i monitorowanie zachowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="ba709-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="ba709-124">Śledź usługę kondycji</span><span class="sxs-lookup"><span data-stu-id="ba709-124">Track Service health</span></span>
<span data-ttu-id="ba709-125">Microsoft Azure publicizes każdym razem, gdy istnieje degradacji przerw i wydajności usługi.</span><span class="sxs-lookup"><span data-stu-id="ba709-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="ba709-126">Kondycja hello hello usługi można śledzić na powitania [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ba709-126">You can track hello health of hello service on hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="ba709-127">Aby uzyskać więcej informacji, zobacz [śledzić kondycja usługi](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="ba709-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="ba709-128">Monitorowanie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="ba709-128">Monitor your web app</span></span>
<span data-ttu-id="ba709-129">Ta opcja umożliwia toofind wychodzących, jeśli masz problemy w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ba709-129">This option enables you toofind out if your application is having any issues.</span></span> <span data-ttu-id="ba709-130">W bloku aplikacja sieci web, kliknij hello **żądań i błędów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="ba709-130">In your web app’s blade, click hello **Requests and errors** tile.</span></span> <span data-ttu-id="ba709-131">Witaj **Metryka** bloku wyświetli wszystkie metryki hello można dodać.</span><span class="sxs-lookup"><span data-stu-id="ba709-131">hello **Metric** blade will show you all hello metrics you can add.</span></span>

<span data-ttu-id="ba709-132">Niektóre hello metryki dla aplikacji sieci web można toomonitor</span><span class="sxs-lookup"><span data-stu-id="ba709-132">Some of hello metrics that you might want toomonitor for your web app are</span></span>

* <span data-ttu-id="ba709-133">Pamięć średni zestaw roboczy</span><span class="sxs-lookup"><span data-stu-id="ba709-133">Average memory working set</span></span>
* <span data-ttu-id="ba709-134">Średni czas odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ba709-134">Average response time</span></span>
* <span data-ttu-id="ba709-135">Czas procesora CPU</span><span class="sxs-lookup"><span data-stu-id="ba709-135">CPU time</span></span>
* <span data-ttu-id="ba709-136">Zestaw roboczy pamięci</span><span class="sxs-lookup"><span data-stu-id="ba709-136">Memory working set</span></span>
* <span data-ttu-id="ba709-137">Żądania</span><span class="sxs-lookup"><span data-stu-id="ba709-137">Requests</span></span>

![monitorowanie aplikacji sieci web do rozwiązania błędów HTTP 502 Niewłaściwa brama i 503 Usługa jest niedostępna](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="ba709-139">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="ba709-139">For more information, see:</span></span>

* [<span data-ttu-id="ba709-140">Monitorowanie aplikacji sieci Web w usłudze aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="ba709-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="ba709-141">Otrzymywanie powiadomień o alertach</span><span class="sxs-lookup"><span data-stu-id="ba709-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="ba709-142">2. Zbieranie danych</span><span class="sxs-lookup"><span data-stu-id="ba709-142">2. Collect data</span></span>
#### <a name="use-hello-azure-app-service-support-portal"></a><span data-ttu-id="ba709-143">Użyj hello portalu pomocy technicznej usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="ba709-143">Use hello Azure App Service Support Portal</span></span>
<span data-ttu-id="ba709-144">Aplikacje sieci Web udostępnia aplikacji sieci web hello możliwości tootroubleshoot problemów powiązanych tooyour analizując HTTP dzienniki, dzienniki zdarzeń, zrzuty procesu i inne.</span><span class="sxs-lookup"><span data-stu-id="ba709-144">Web Apps provides you with hello ability tootroubleshoot issues related tooyour web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="ba709-145">Można uzyskać dostępu do tych informacji za pomocą portalu pomocy technicznej w **http://&lt;Twojego Nazwa aplikacji >.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="ba709-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="ba709-146">Hello portalu pomocy technicznej usługi aplikacji Azure udostępnia trzy oddzielne karty toosupport hello trzy kroki typowego scenariusza rozwiązywania problemów:</span><span class="sxs-lookup"><span data-stu-id="ba709-146">hello Azure App Service Support portal provides you with three separate tabs toosupport hello three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="ba709-147">Sprawdź bieżące zachowanie</span><span class="sxs-lookup"><span data-stu-id="ba709-147">Observe current behavior</span></span>
2. <span data-ttu-id="ba709-148">Analizowanie zbierania informacji diagnostycznych i uruchamiając hello analizatorów wbudowane</span><span class="sxs-lookup"><span data-stu-id="ba709-148">Analyze by collecting diagnostics information and running hello built-in analyzers</span></span>
3. <span data-ttu-id="ba709-149">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="ba709-149">Mitigate</span></span>

<span data-ttu-id="ba709-150">Problem hello jest przeprowadzana od razu, kliknij przycisk **Analizuj** > **diagnostyki** > **diagnozowanie teraz** toocreate sesję diagnostyki, który będzie zbierać HTTP dzienniki, dzienniki Podglądu zdarzeń, pamięci zrzuty, dzienniki błędów PHP i PHP przetwarzania raportu.</span><span class="sxs-lookup"><span data-stu-id="ba709-150">If hello issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** toocreate a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="ba709-151">Po pobraniu danych hello, zostanie również przeprowadzanie analizy na powitania danych oraz zapewnić mu raport HTML.</span><span class="sxs-lookup"><span data-stu-id="ba709-151">Once hello data is collected, it will also run an analysis on hello data and provide you with an HTML report.</span></span>

<span data-ttu-id="ba709-152">W przypadku, gdy chcesz toodownload hello dane, domyślnie, powinny być przechowywane w folderze D:\home\data\DaaS hello.</span><span class="sxs-lookup"><span data-stu-id="ba709-152">In case you want toodownload hello data, by default, it would be stored in hello D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="ba709-153">Aby uzyskać więcej informacji na powitania portalu pomocy technicznej usługi aplikacji Azure, zobacz [tooSupport nowe aktualizacje lokacji rozszerzenie dla witryny sieci Web Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="ba709-153">For more information on hello Azure App Service Support portal, see [New Updates tooSupport Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-hello-kudu-debug-console"></a><span data-ttu-id="ba709-154">Użyj hello Kudu Debug Console</span><span class="sxs-lookup"><span data-stu-id="ba709-154">Use hello Kudu Debug Console</span></span>
<span data-ttu-id="ba709-155">Aplikacje sieci Web jest dostarczany z konsoli debugowania, która służy do debugowania, eksploracji, przekazywania plików, a także pobieranie informacji na temat środowiska punktów końcowych JSON.</span><span class="sxs-lookup"><span data-stu-id="ba709-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="ba709-156">Ta metoda jest wywoływana hello *konsoli Kudu* lub hello *pulpitu nawigacyjnego SCM* dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ba709-156">This is called hello *Kudu Console* or hello *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="ba709-157">Uzyskać dostęp do tego pulpitu nawigacyjnego, przechodząc łącze toohello **https://&lt;Twojego Nazwa aplikacji >.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="ba709-157">You can access this dashboard by going toohello link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="ba709-158">Program Kudu udostępnia zagadnienia hello należą:</span><span class="sxs-lookup"><span data-stu-id="ba709-158">Some of hello things that Kudu provides are:</span></span>

* <span data-ttu-id="ba709-159">ustawienia środowiska aplikacji</span><span class="sxs-lookup"><span data-stu-id="ba709-159">environment settings for your application</span></span>
* <span data-ttu-id="ba709-160">strumień dziennika</span><span class="sxs-lookup"><span data-stu-id="ba709-160">log stream</span></span>
* <span data-ttu-id="ba709-161">diagnostycznych zrzutu</span><span class="sxs-lookup"><span data-stu-id="ba709-161">diagnostic dump</span></span>
* <span data-ttu-id="ba709-162">Konsola, w którym można uruchomić poleceń cmdlet programu Powershell i podstawowe polecenia systemu DOS debugowania.</span><span class="sxs-lookup"><span data-stu-id="ba709-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="ba709-163">Inny przydatną cechą Kudu jest, że w przypadku, gdy aplikacja jest zgłaszanie wyjątków pierwszej szansy, można użyć Kudu i zrzuty hello SysInternals narzędzie Procdump toocreate pamięci.</span><span class="sxs-lookup"><span data-stu-id="ba709-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and hello SysInternals tool Procdump toocreate memory dumps.</span></span> <span data-ttu-id="ba709-164">Te zrzuty pamięci są migawki procesu hello i często ułatwiają rozwiązywanie problemów z bardziej skomplikowanych problemów z aplikacją sieci web.</span><span class="sxs-lookup"><span data-stu-id="ba709-164">These memory dumps are snapshots of hello process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="ba709-165">Aby uzyskać więcej informacji o funkcjach dostępnych w Kudu, zobacz [narzędzia online witryny sieci Web Azure należy wiedzieć o](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="ba709-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a><span data-ttu-id="ba709-166">3. Ograniczenia hello problem</span><span class="sxs-lookup"><span data-stu-id="ba709-166">3. Mitigate hello issue</span></span>
#### <a name="scale-hello-web-app"></a><span data-ttu-id="ba709-167">Aplikacja sieci web hello skali</span><span class="sxs-lookup"><span data-stu-id="ba709-167">Scale hello web app</span></span>
<span data-ttu-id="ba709-168">W usłudze Azure App Service Aby zwiększyć wydajność i przepływność, można dostosować hello skali, w którym są uruchomione aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ba709-168">In Azure App Service, for increased performance and throughput,  you can adjust hello scale at which you are running your application.</span></span> <span data-ttu-id="ba709-169">Skalowanie w górę aplikacji sieci web obejmuje dwie akcje powiązane: zmiana z wyższej warstwy cenowej i konfigurowanie niektórych ustawień po przełączeniu toohello wyższej warstwy cenowej tooa planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ba709-169">Scaling up a web app involves two related actions: changing your App Service plan tooa higher pricing tier, and configuring certain settings after you have switched toohello higher pricing tier.</span></span>

<span data-ttu-id="ba709-170">Aby uzyskać więcej informacji na temat skalowania, zobacz [skalowanie aplikacji sieci web w usłudze Azure App Service](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ba709-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="ba709-171">Ponadto można wybrać toorun aplikacji na więcej niż jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="ba709-171">Additionally, you can choose toorun your application on more than one instance .</span></span> <span data-ttu-id="ba709-172">To nie tylko zapewnia więcej możliwości przetwarzania, ale umożliwia także niektóre ilość odporność na uszkodzenia.</span><span class="sxs-lookup"><span data-stu-id="ba709-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="ba709-173">Jeśli hello procesu przestanie działać w jednym wystąpieniu, hello inne wystąpienie będzie nadal obsługiwać żądania dostępu.</span><span class="sxs-lookup"><span data-stu-id="ba709-173">If hello process goes down on one instance, hello other instance will still continue serving requests.</span></span>

<span data-ttu-id="ba709-174">Można ustawić hello skalowanie toobe ręczne lub automatyczne.</span><span class="sxs-lookup"><span data-stu-id="ba709-174">You can set hello scaling toobe Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="ba709-175">Funkcja AutoHeal użycia</span><span class="sxs-lookup"><span data-stu-id="ba709-175">Use AutoHeal</span></span>
<span data-ttu-id="ba709-176">Funkcja AutoHeal odtwarzania procesu roboczego hello aplikacji na podstawie ustawień wybranego (np. zmiany konfiguracji, żądania, limity pamięci lub czasu hello wymagane tooexecute żądania).</span><span class="sxs-lookup"><span data-stu-id="ba709-176">AutoHeal recycles hello worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or hello time needed tooexecute a request).</span></span> <span data-ttu-id="ba709-177">W większości przypadków hello odtworzenia procesu hello jest hello najszybszy sposób toorecover z problem.</span><span class="sxs-lookup"><span data-stu-id="ba709-177">Most of hello time, recycle hello process is hello fastest way toorecover from a problem.</span></span> <span data-ttu-id="ba709-178">Chociaż można zawsze uruchomić ponownie hello aplikacji sieci web z bezpośrednio z poziomu portalu Azure hello, funkcja AutoHeal będzie robi to automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ba709-178">Though you can always restart hello web app from directly within hello Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="ba709-179">Toodo wystarczy dodać niektóre wyzwalacze w hello głównym pliku web.config dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ba709-179">All you need toodo is add some triggers in hello root web.config for your web app.</span></span> <span data-ttu-id="ba709-180">Należy pamiętać, że te ustawienia będą działać w hello sam sposób, nawet jeśli w aplikacji nie jest jedną .net.</span><span class="sxs-lookup"><span data-stu-id="ba709-180">Note that these settings would work in hello same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="ba709-181">Aby uzyskać więcej informacji, zobacz [automatyczne naprawianie Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="ba709-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-hello-web-app"></a><span data-ttu-id="ba709-182">Ponowne uruchomienie aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="ba709-182">Restart hello web app</span></span>
<span data-ttu-id="ba709-183">Jest to często hello najprostszy sposób toorecover jednorazowo występujące problemy.</span><span class="sxs-lookup"><span data-stu-id="ba709-183">This is often hello simplest way toorecover from one-time issues.</span></span> <span data-ttu-id="ba709-184">Na powitania [Azure Portal](https://portal.azure.com/), w bloku aplikacja sieci web, masz toostop opcje hello lub uruchom ponownie aplikację.</span><span class="sxs-lookup"><span data-stu-id="ba709-184">On hello [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have hello options toostop or restart your app.</span></span>

 ![ponowne uruchomienie aplikacji toosolve HTTP błędy 502 Niewłaściwa brama i 503 Usługa jest niedostępna](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="ba709-186">Można również zarządzać aplikacji sieci web przy użyciu programu Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="ba709-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="ba709-187">Aby uzyskać więcej informacji, zobacz temat [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Azure PowerShell z usługą Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="ba709-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

