---
title: "Rozwiązać Zła brama 502, 503 obsługi błędów niedostępności | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 397a6aaf7dc27adfa0fc0e722b8a2be5cc1d75f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="25a0e-104">Rozwiązywanie błędów HTTP "502 Niewłaściwa brama" i "503 Usługa niedostępna" w aplikacjach sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="25a0e-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="25a0e-105">"brama zły 502" i "503 Usługa niedostępna" są typowe błędy w aplikacji sieci web hostowanych w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="25a0e-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="25a0e-106">Ten artykuł pomoże w rozwiązaniu tych błędów.</span><span class="sxs-lookup"><span data-stu-id="25a0e-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="25a0e-107">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się ekspertów platformy Azure na [MSDN Azure i fora przepełnienie stosu](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="25a0e-107">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="25a0e-108">Alternatywnie można również pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="25a0e-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="25a0e-109">Przejdź do [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz polecenie **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="25a0e-109">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="25a0e-110">Objaw</span><span class="sxs-lookup"><span data-stu-id="25a0e-110">Symptom</span></span>
<span data-ttu-id="25a0e-111">Po przejściu do aplikacji sieci web zwraca HTTP HTTP lub błąd "502 Niewłaściwa brama" błąd "503 Usługa niedostępna".</span><span class="sxs-lookup"><span data-stu-id="25a0e-111">When you browse to the web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="25a0e-112">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="25a0e-112">Cause</span></span>
<span data-ttu-id="25a0e-113">Ten problem jest często spowodowane przez problemy z poziomu aplikacji, takich jak:</span><span class="sxs-lookup"><span data-stu-id="25a0e-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="25a0e-114">żądania zbyt długo</span><span class="sxs-lookup"><span data-stu-id="25a0e-114">requests taking a long time</span></span>
* <span data-ttu-id="25a0e-115">aplikacji przy użyciu pamięci wysokiej/procesora CPU</span><span class="sxs-lookup"><span data-stu-id="25a0e-115">application using high memory/CPU</span></span>
* <span data-ttu-id="25a0e-116">Aplikacja awarii z powodu wyjątku.</span><span class="sxs-lookup"><span data-stu-id="25a0e-116">application crashing due to an exception.</span></span>

## <a name="troubleshooting-steps-to-solve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="25a0e-117">Kroki rozwiązywania problemów do rozwiązania "502 Niewłaściwa brama" i "503 Usługa niedostępna" błędów</span><span class="sxs-lookup"><span data-stu-id="25a0e-117">Troubleshooting steps to solve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="25a0e-118">Rozwiązywanie problemów, można podzielić na trzy różne zadania, w kolejności sekwencyjnej:</span><span class="sxs-lookup"><span data-stu-id="25a0e-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="25a0e-119">Sprawdź i monitorowanie zachowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="25a0e-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="25a0e-120">Zbieranie danych</span><span class="sxs-lookup"><span data-stu-id="25a0e-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="25a0e-121">Ograniczenia problem</span><span class="sxs-lookup"><span data-stu-id="25a0e-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="25a0e-122">[Aplikacje sieci Web usługi aplikacji](/services/app-service/web/) zapewnia różne opcje w każdym kroku.</span><span class="sxs-lookup"><span data-stu-id="25a0e-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="25a0e-123">1. Sprawdź i monitorowanie zachowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="25a0e-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="25a0e-124">Śledź usługę kondycji</span><span class="sxs-lookup"><span data-stu-id="25a0e-124">Track Service health</span></span>
<span data-ttu-id="25a0e-125">Microsoft Azure publicizes każdym razem, gdy istnieje degradacji przerw i wydajności usługi.</span><span class="sxs-lookup"><span data-stu-id="25a0e-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="25a0e-126">Kondycja usługi można śledzić na [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="25a0e-126">You can track the health of the service on the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="25a0e-127">Aby uzyskać więcej informacji, zobacz [śledzić kondycja usługi](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="25a0e-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="25a0e-128">Monitorowanie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="25a0e-128">Monitor your web app</span></span>
<span data-ttu-id="25a0e-129">Ta opcja pozwala dowiedzieć się, jeśli masz problemy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25a0e-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="25a0e-130">W bloku aplikacja sieci web, kliknij przycisk **żądań i błędów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="25a0e-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="25a0e-131">**Metryka** bloku wyświetli wszystkie metryki można dodać.</span><span class="sxs-lookup"><span data-stu-id="25a0e-131">The **Metric** blade will show you all the metrics you can add.</span></span>

<span data-ttu-id="25a0e-132">Niektóre metryki, które mogą zostać do monitorowania aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="25a0e-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="25a0e-133">Pamięć średni zestaw roboczy</span><span class="sxs-lookup"><span data-stu-id="25a0e-133">Average memory working set</span></span>
* <span data-ttu-id="25a0e-134">Średni czas odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="25a0e-134">Average response time</span></span>
* <span data-ttu-id="25a0e-135">Czas procesora CPU</span><span class="sxs-lookup"><span data-stu-id="25a0e-135">CPU time</span></span>
* <span data-ttu-id="25a0e-136">Zestaw roboczy pamięci</span><span class="sxs-lookup"><span data-stu-id="25a0e-136">Memory working set</span></span>
* <span data-ttu-id="25a0e-137">Żądania</span><span class="sxs-lookup"><span data-stu-id="25a0e-137">Requests</span></span>

![monitorowanie aplikacji sieci web do rozwiązania błędów HTTP 502 Niewłaściwa brama i 503 Usługa jest niedostępna](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="25a0e-139">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="25a0e-139">For more information, see:</span></span>

* [<span data-ttu-id="25a0e-140">Monitorowanie aplikacji sieci Web w usłudze aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="25a0e-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="25a0e-141">Otrzymywanie powiadomień o alertach</span><span class="sxs-lookup"><span data-stu-id="25a0e-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="25a0e-142">2. Zbieranie danych</span><span class="sxs-lookup"><span data-stu-id="25a0e-142">2. Collect data</span></span>
#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="25a0e-143">Użyj portalu pomocy technicznej usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="25a0e-143">Use the Azure App Service Support Portal</span></span>
<span data-ttu-id="25a0e-144">Aplikacje sieci Web umożliwia rozwiązanie problemów dotyczących aplikacji sieci web, analizując HTTP dzienniki, dzienniki zdarzeń, zrzuty procesu i inne.</span><span class="sxs-lookup"><span data-stu-id="25a0e-144">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="25a0e-145">Można uzyskać dostępu do tych informacji za pomocą portalu pomocy technicznej w **http://&lt;Twojego Nazwa aplikacji >.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="25a0e-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="25a0e-146">Portal Azure App Service obsługuje zawiera trzy oddzielne karty do obsługi trzy kroki typowego scenariusza rozwiązywania problemów:</span><span class="sxs-lookup"><span data-stu-id="25a0e-146">The Azure App Service Support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="25a0e-147">Sprawdź bieżące zachowanie</span><span class="sxs-lookup"><span data-stu-id="25a0e-147">Observe current behavior</span></span>
2. <span data-ttu-id="25a0e-148">Analizowanie zbierania informacji diagnostycznych i uruchamiając analizatorów wbudowane</span><span class="sxs-lookup"><span data-stu-id="25a0e-148">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="25a0e-149">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="25a0e-149">Mitigate</span></span>

<span data-ttu-id="25a0e-150">Problem jest wykonywane od razu, kliknij przycisk **Analizuj** > **diagnostyki** > **diagnozowanie teraz** utworzenie sesji diagnostycznej, do którego będzie zbierać dzienniki HTTP, dzienniki Podglądu zdarzeń, pamięci zrzuty, dzienniki błędów PHP i PHP przetwarzania raportu.</span><span class="sxs-lookup"><span data-stu-id="25a0e-150">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="25a0e-151">Gdy dane są zbierane, zostanie również przeprowadzanie analizy danych i dostarczyć raport HTML.</span><span class="sxs-lookup"><span data-stu-id="25a0e-151">Once the data is collected, it will also run an analysis on the data and provide you with an HTML report.</span></span>

<span data-ttu-id="25a0e-152">W przypadku, gdy chcesz pobrać dane, domyślnie, powinny być przechowywane w folderze D:\home\data\DaaS.</span><span class="sxs-lookup"><span data-stu-id="25a0e-152">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="25a0e-153">Aby uzyskać więcej informacji w portalu pomocy technicznej usługi aplikacji Azure, zobacz [nowe aktualizacje do rozszerzenia witrynę pomocy technicznej dla witryn sieci Web Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="25a0e-153">For more information on the Azure App Service Support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="25a0e-154">Użyj konsoli debugowania aparatu Kudu</span><span class="sxs-lookup"><span data-stu-id="25a0e-154">Use the Kudu Debug Console</span></span>
<span data-ttu-id="25a0e-155">Aplikacje sieci Web jest dostarczany z konsoli debugowania, która służy do debugowania, eksploracji, przekazywania plików, a także pobieranie informacji na temat środowiska punktów końcowych JSON.</span><span class="sxs-lookup"><span data-stu-id="25a0e-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="25a0e-156">Ta metoda jest wywoływana *konsoli Kudu* lub *pulpitu nawigacyjnego SCM* dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="25a0e-156">This is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="25a0e-157">Dostęp do tego pulpitu nawigacyjnego, przechodząc do łącza **https://&lt;Twojego Nazwa aplikacji >.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="25a0e-157">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="25a0e-158">Niektóre czynności, które program Kudu udostępnia są:</span><span class="sxs-lookup"><span data-stu-id="25a0e-158">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="25a0e-159">ustawienia środowiska aplikacji</span><span class="sxs-lookup"><span data-stu-id="25a0e-159">environment settings for your application</span></span>
* <span data-ttu-id="25a0e-160">strumień dziennika</span><span class="sxs-lookup"><span data-stu-id="25a0e-160">log stream</span></span>
* <span data-ttu-id="25a0e-161">diagnostycznych zrzutu</span><span class="sxs-lookup"><span data-stu-id="25a0e-161">diagnostic dump</span></span>
* <span data-ttu-id="25a0e-162">Konsola, w którym można uruchomić poleceń cmdlet programu Powershell i podstawowe polecenia systemu DOS debugowania.</span><span class="sxs-lookup"><span data-stu-id="25a0e-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="25a0e-163">Inny przydatną cechą Kudu jest, że w przypadku, gdy aplikacja jest zgłaszanie wyjątków pierwszej szansy, można użyć Kudu i zrzuty narzędzie SysInternals Procdump utworzyć pamięci.</span><span class="sxs-lookup"><span data-stu-id="25a0e-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="25a0e-164">Te zrzuty pamięci są migawki procesu i często ułatwiają rozwiązywanie problemów z bardziej skomplikowanych problemów z aplikacją sieci web.</span><span class="sxs-lookup"><span data-stu-id="25a0e-164">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="25a0e-165">Aby uzyskać więcej informacji o funkcjach dostępnych w Kudu, zobacz [narzędzia online witryny sieci Web Azure należy wiedzieć o](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="25a0e-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="25a0e-166">3. Ograniczenia problem</span><span class="sxs-lookup"><span data-stu-id="25a0e-166">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="25a0e-167">Skalowanie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="25a0e-167">Scale the web app</span></span>
<span data-ttu-id="25a0e-168">W usłudze Azure App Service Aby zwiększyć wydajność i przepływność, można dostosować skali, w którym są uruchomione aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25a0e-168">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="25a0e-169">Skalowanie w górę aplikacji sieci web obejmuje dwie akcje powiązane: zmiana planu usługi aplikacji na wyższej warstwy cenowej i konfigurowanie niektórych ustawień po przełączeniu do wyższej warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="25a0e-169">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="25a0e-170">Aby uzyskać więcej informacji na temat skalowania, zobacz [skalowanie aplikacji sieci web w usłudze Azure App Service](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="25a0e-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="25a0e-171">Ponadto można wybrać do uruchamiania aplikacji na więcej niż jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="25a0e-171">Additionally, you can choose to run your application on more than one instance .</span></span> <span data-ttu-id="25a0e-172">To nie tylko zapewnia więcej możliwości przetwarzania, ale umożliwia także niektóre ilość odporność na uszkodzenia.</span><span class="sxs-lookup"><span data-stu-id="25a0e-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="25a0e-173">Jeśli proces przestanie działać w jednym wystąpieniu, jak inne wystąpienie będzie nadal obsługiwać żądania.</span><span class="sxs-lookup"><span data-stu-id="25a0e-173">If the process goes down on one instance, the other instance will still continue serving requests.</span></span>

<span data-ttu-id="25a0e-174">Można skonfigurować jako ręczne lub automatyczne skalowanie.</span><span class="sxs-lookup"><span data-stu-id="25a0e-174">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="25a0e-175">Funkcja AutoHeal użycia</span><span class="sxs-lookup"><span data-stu-id="25a0e-175">Use AutoHeal</span></span>
<span data-ttu-id="25a0e-176">Funkcja AutoHeal odtwarzania procesu roboczego dla aplikacji na podstawie ustawień wybranego (na przykład zmiany konfiguracji żądania, limity pamięci lub czas potrzebny na wykonanie żądania).</span><span class="sxs-lookup"><span data-stu-id="25a0e-176">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="25a0e-177">W większości przypadków, odtworzenia procesu jest najszybszym sposobem odzyskanie problem.</span><span class="sxs-lookup"><span data-stu-id="25a0e-177">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="25a0e-178">Chociaż zawsze można ponownie uruchomić aplikacji sieci web z bezpośrednio z poziomu portalu Azure, funkcja AutoHeal będzie robi to automatycznie.</span><span class="sxs-lookup"><span data-stu-id="25a0e-178">Though you can always restart the web app from directly within the Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="25a0e-179">To wszystko, co należy zrobić, Dodaj niektóre wyzwalacze w głównym pliku web.config dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="25a0e-179">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="25a0e-180">Należy pamiętać, że te ustawienia będzie działać w taki sam sposób, nawet jeśli aplikacja nie jest jedną .net.</span><span class="sxs-lookup"><span data-stu-id="25a0e-180">Note that these settings would work in the same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="25a0e-181">Aby uzyskać więcej informacji, zobacz [automatyczne naprawianie Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="25a0e-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="25a0e-182">Uruchom ponownie aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="25a0e-182">Restart the web app</span></span>
<span data-ttu-id="25a0e-183">Często jest najprostszym sposobem, aby rozwiązać jednorazowo występujące problemy.</span><span class="sxs-lookup"><span data-stu-id="25a0e-183">This is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="25a0e-184">Na [Azure Portal](https://portal.azure.com/), w bloku aplikacja sieci web ma opcji, aby zatrzymać lub uruchomić ponownie aplikację.</span><span class="sxs-lookup"><span data-stu-id="25a0e-184">On the [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![Uruchom ponownie aplikację, aby naprawić błędy HTTP 502 Niewłaściwa brama i 503 Usługa jest niedostępna](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="25a0e-186">Można również zarządzać aplikacji sieci web przy użyciu programu Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="25a0e-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="25a0e-187">Aby uzyskać więcej informacji, zobacz temat [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Azure PowerShell z usługą Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="25a0e-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

