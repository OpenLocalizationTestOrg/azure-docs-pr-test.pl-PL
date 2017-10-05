---
title: "Zarządzanie aplikacji sieci web w usłudze Azure App Service"
description: "Linki do zasobów związanych z zarządzaniem aplikacji sieci web w usłudze Azure App Service."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: 9e19618a1b24bbdf3163ddfc3423c5c932dcd7af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="9f495-103">Zarządzanie aplikacji sieci web w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9f495-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="9f495-104">Ten temat zawiera linki do zasobów związanych z zarządzaniem aplikacji sieci web w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="9f495-104">This topic contains links to resources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="9f495-105">Zarządzanie obejmuje wszystkie zadania zachowujących sprawnego działania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9f495-105">Management includes all of the tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="9f495-106">W okresie istnienia aplikacji sieci web będzie wykonywać różnymi zadaniami zarządzania, w przypadku przejścia od pierwszego wdrożenia do normalnego działania, konserwacji i aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="9f495-106">Over the lifetime of a web app, you will perform different management tasks, as you move from initial deployment to normal operation, maintenance, and updates.</span></span>

<span data-ttu-id="9f495-107">Wiele zadań zarządzania aplikacji sieci web można wykonać w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9f495-107">Many web app management tasks can be performed in the Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-to-production"></a><span data-ttu-id="9f495-108">Przed wdrożeniem aplikacji sieci web w środowisku produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="9f495-108">Before you deploy your web app to production</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="9f495-109">Wybierz warstwę</span><span class="sxs-lookup"><span data-stu-id="9f495-109">Choose a tier</span></span>
<span data-ttu-id="9f495-110">Usługa aplikacji Azure jest oferowany pięciu warstw: Zwolnij udostępnione, podstawowa, standardowa i Premium.</span><span class="sxs-lookup"><span data-stu-id="9f495-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="9f495-111">Informacje o funkcjach i ceny dla każdej warstwy, zobacz [szczegóły cennika](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="9f495-111">For information about the features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="9f495-112">[Planów usługi App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) pozwalają na grupowanie wielu aplikacji sieci web w tej samej warstwie.</span><span class="sxs-lookup"><span data-stu-id="9f495-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under the same tier.</span></span>
* <span data-ttu-id="9f495-113">Możesz zawsze [przełącznik warstwy](web-sites-scale.md) po utworzeniu aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9f495-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="9f495-114">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="9f495-114">Configuration</span></span>
<span data-ttu-id="9f495-115">Użyj [Azure Portal](https://portal.azure.com/) można ustawić różne opcje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9f495-115">Use the [Azure Portal](https://portal.azure.com/) to set various configuration options.</span></span> <span data-ttu-id="9f495-116">Aby uzyskać więcej informacji, zobacz [Konfigurowanie aplikacji sieci web w usłudze Azure App Service](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9f495-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="9f495-117">Poniżej przedstawiono szybki Lista kontrolna:</span><span class="sxs-lookup"><span data-stu-id="9f495-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="9f495-118">Wybierz **wersji środowiska uruchomieniowego** dla platformy .NET, PHP, Java lub Python, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9f495-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="9f495-119">Włącz **Websocket** Jeśli aplikacja sieci web używa protokołu WebSocket.</span><span class="sxs-lookup"><span data-stu-id="9f495-119">Enable **WebSockets** if your web app uses the WebSocket protocol.</span></span> <span data-ttu-id="9f495-120">(Dotyczy to aplikacji, które używają [ASP.NET SignalR](http://www.asp.net/signalr) lub [użyciu biblioteki socket.io](web-sites-nodejs-chat-app-socketio.md).)</span><span class="sxs-lookup"><span data-stu-id="9f495-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="9f495-121">Używasz ciągłego web zadania?</span><span class="sxs-lookup"><span data-stu-id="9f495-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="9f495-122">Jeśli tak, Włącz **zawsze na**.</span><span class="sxs-lookup"><span data-stu-id="9f495-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="9f495-123">Ustaw **dokument domyślny**, takich jak index.html.</span><span class="sxs-lookup"><span data-stu-id="9f495-123">Set the **default document**, such as index.html.</span></span>

<span data-ttu-id="9f495-124">Oprócz tych ustawień konfiguracji podstawowej można skonfigurować następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="9f495-124">In addition to these basic configuration settings, you may want to configure the following:</span></span>

* <span data-ttu-id="9f495-125">**Secure Socket Layer (SSL)** szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="9f495-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="9f495-126">Używanie protokołu SSL z niestandardowej nazwy domeny, należy uzyskać certyfikat SSL i skonfigurować aplikację sieci web w celu używania go.</span><span class="sxs-lookup"><span data-stu-id="9f495-126">To use SSL with a custom domain name, you must get an SSL certificate and configure your web app to use it.</span></span> <span data-ttu-id="9f495-127">Zobacz [Włącz protokół HTTPS dla aplikacji sieci web w usłudze Azure App Service](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="9f495-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="9f495-128">**Nazwa domeny niestandardowej.**</span><span class="sxs-lookup"><span data-stu-id="9f495-128">**Custom domain name.**</span></span> <span data-ttu-id="9f495-129">Aplikacja sieci web ma automatycznie poddomeny w obszarze azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="9f495-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="9f495-130">Możesz skojarzyć niestandardowej nazwy domeny, np. contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9f495-130">You can associate a custom domain name, such as contoso.com.</span></span> <span data-ttu-id="9f495-131">Zobacz [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="9f495-131">See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="9f495-132">Konfiguracja specyficzny dla języka:</span><span class="sxs-lookup"><span data-stu-id="9f495-132">Language-specific configuration:</span></span>

* <span data-ttu-id="9f495-133">**PHP**: [skonfigurować PHP w aplikacjach sieci Web usługi aplikacji Azure](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9f495-133">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="9f495-134">**Python**: [Konfigurowanie Python z usługi aplikacji Azure Web Apps](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="9f495-134">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="9f495-135">Aplikacja sieci web jest uruchomiona</span><span class="sxs-lookup"><span data-stu-id="9f495-135">While your web app is running</span></span>
<span data-ttu-id="9f495-136">Po uruchomieniu aplikacji sieci web ma upewnij się, że jest dostępny i że może spełniać ruchu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9f495-136">While your web app is running, you want to make sure it is available, and that it scales to meet user traffic.</span></span> <span data-ttu-id="9f495-137">Może być również konieczne rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="9f495-137">You may also need to troubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="9f495-138">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="9f495-138">Monitoring</span></span>
* <span data-ttu-id="9f495-139">Za pośrednictwem portalu Azure, możesz [dodać metryki wydajności](web-sites-monitor.md) użycia procesora CPU i liczby żądań klientów.</span><span class="sxs-lookup"><span data-stu-id="9f495-139">Through the Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="9f495-140">[Skalowanie aplikacji sieci web](web-sites-scale.md) w odpowiedzi na ruch.</span><span class="sxs-lookup"><span data-stu-id="9f495-140">[Scale your web app](web-sites-scale.md) in response to traffic.</span></span> <span data-ttu-id="9f495-141">W zależności od warstwę można skalować liczbę maszyn wirtualnych i/lub rozmiaru wystąpień maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9f495-141">Depending on your tier, you can scale the number of VMs and/or the size of the VM instances.</span></span> <span data-ttu-id="9f495-142">W warstwy standardowa i Premium można również skonfigurować Skalowanie automatyczne, więc aplikacji sieci web skaluje automatycznie, zgodnie z ustalonym harmonogramem lub w odpowiedzi na obciążenia.</span><span class="sxs-lookup"><span data-stu-id="9f495-142">In the Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response to load.</span></span>  

### <a name="backups"></a><span data-ttu-id="9f495-143">Tworzenie kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="9f495-143">Backups</span></span>
* <span data-ttu-id="9f495-144">Ustaw [automatycznego tworzenia kopii zapasowych](web-sites-backup.md) aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9f495-144">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="9f495-145">Dowiedz się więcej na temat tworzenia kopii zapasowych w [ten film](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="9f495-145">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="9f495-146">Więcej informacji na temat opcji [odzyskiwanie bazy danych](../sql-database/sql-database-business-continuity.md) w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9f495-146">Learn about the options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="9f495-147">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="9f495-147">Troubleshooting</span></span>
* <span data-ttu-id="9f495-148">Jeśli jakaś nieprawidłowość, możesz [Rozwiązywanie problemów w programie Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), przy użyciu dzienników diagnostycznych i na żywo debugowania w chmurze.</span><span class="sxs-lookup"><span data-stu-id="9f495-148">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in the cloud.</span></span> 
* <span data-ttu-id="9f495-149">Poza Visual Studio istnieją różne sposoby zbierania dzienników diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="9f495-149">Outside of Visual Studio, there are various ways to collect diagnostic logs.</span></span> <span data-ttu-id="9f495-150">Zobacz [Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="9f495-150">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="9f495-151">Dla aplikacji programu Node.js [debugowanie aplikacji sieci web Node.js w usłudze Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="9f495-151">For Node.js applications, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="9f495-152">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="9f495-152">Restoring Data</span></span>
* <span data-ttu-id="9f495-153">[Przywróć](web-sites-restore.md) aplikacji sieci web, która została wcześniej utworzona kopia zapasowa.</span><span class="sxs-lookup"><span data-stu-id="9f495-153">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="9f495-154">Podczas aktualizacji aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="9f495-154">When you update your web app</span></span>
<span data-ttu-id="9f495-155">Jeśli nie włączono automatycznego tworzenia kopii zapasowych, możesz utworzyć [ręcznego wykonywania kopii zapasowej](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="9f495-155">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="9f495-156">Należy rozważyć użycie [przemieszczane wdrożenia](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="9f495-156">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="9f495-157">Ta opcja umożliwia publikowanie aktualizacji do tymczasowej wdrożenia, które uruchamia side-by-side z wdrożeniem w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="9f495-157">This option lets you publish updates to a staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


