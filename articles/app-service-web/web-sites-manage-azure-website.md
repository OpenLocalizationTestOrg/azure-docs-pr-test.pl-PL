---
title: "aaaManage aplikacji sieci web w usłudze Azure App Service"
description: "Tooresources łącza do zarządzania aplikacji sieci web w usłudze Azure App Service."
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
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="fb522-103">Zarządzanie aplikacji sieci web w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fb522-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="fb522-104">Ten temat zawiera tooresources łącza do zarządzania aplikacji sieci web w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="fb522-104">This topic contains links tooresources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="fb522-105">Zarządzanie obejmuje wszystkie zadania hello, zachowujących sprawnego działania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="fb522-105">Management includes all of hello tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="fb522-106">Hello okresu istnienia aplikacji sieci web będzie wykonywać różnymi zadaniami zarządzania, jak przenieść z operacji toonormal początkowe wdrożenie, obsługi i aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="fb522-106">Over hello lifetime of a web app, you will perform different management tasks, as you move from initial deployment toonormal operation, maintenance, and updates.</span></span>

<span data-ttu-id="fb522-107">Wiele zadań zarządzania aplikacji sieci web można wykonać w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fb522-107">Many web app management tasks can be performed in hello Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-tooproduction"></a><span data-ttu-id="fb522-108">Przed wdrożeniem tooproduction aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="fb522-108">Before you deploy your web app tooproduction</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="fb522-109">Wybierz warstwę</span><span class="sxs-lookup"><span data-stu-id="fb522-109">Choose a tier</span></span>
<span data-ttu-id="fb522-110">Usługa aplikacji Azure jest oferowany pięciu warstw: Zwolnij udostępnione, podstawowa, standardowa i Premium.</span><span class="sxs-lookup"><span data-stu-id="fb522-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="fb522-111">Aby uzyskać informacje o funkcjach hello i ceny dla każdej warstwy, zobacz [szczegóły cennika](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="fb522-111">For information about hello features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="fb522-112">[Planów usługi App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) pozwalają na grupowanie wielu aplikacji sieci web w obszarze hello tej samej warstwie.</span><span class="sxs-lookup"><span data-stu-id="fb522-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under hello same tier.</span></span>
* <span data-ttu-id="fb522-113">Możesz zawsze [przełącznik warstwy](web-sites-scale.md) po utworzeniu aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="fb522-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="fb522-114">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="fb522-114">Configuration</span></span>
<span data-ttu-id="fb522-115">Użyj hello [Azure Portal](https://portal.azure.com/) tooset różne opcje konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fb522-115">Use hello [Azure Portal](https://portal.azure.com/) tooset various configuration options.</span></span> <span data-ttu-id="fb522-116">Aby uzyskać więcej informacji, zobacz [Konfigurowanie aplikacji sieci web w usłudze Azure App Service](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="fb522-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="fb522-117">Poniżej przedstawiono szybki Lista kontrolna:</span><span class="sxs-lookup"><span data-stu-id="fb522-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="fb522-118">Wybierz **wersji środowiska uruchomieniowego** dla platformy .NET, PHP, Java lub Python, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="fb522-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="fb522-119">Włącz **Websocket** Jeśli protokół WebSocket hello korzysta z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="fb522-119">Enable **WebSockets** if your web app uses hello WebSocket protocol.</span></span> <span data-ttu-id="fb522-120">(Dotyczy to aplikacji, które używają [ASP.NET SignalR](http://www.asp.net/signalr) lub [użyciu biblioteki socket.io](web-sites-nodejs-chat-app-socketio.md).)</span><span class="sxs-lookup"><span data-stu-id="fb522-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="fb522-121">Używasz ciągłego web zadania?</span><span class="sxs-lookup"><span data-stu-id="fb522-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="fb522-122">Jeśli tak, Włącz **zawsze na**.</span><span class="sxs-lookup"><span data-stu-id="fb522-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="fb522-123">Zestaw hello **dokument domyślny**, takich jak index.html.</span><span class="sxs-lookup"><span data-stu-id="fb522-123">Set hello **default document**, such as index.html.</span></span>

<span data-ttu-id="fb522-124">W ustawieniach konfiguracji podstawowej toothese dodanie może być tooconfigure hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="fb522-124">In addition toothese basic configuration settings, you may want tooconfigure hello following:</span></span>

* <span data-ttu-id="fb522-125">**Secure Socket Layer (SSL)** szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="fb522-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="fb522-126">toouse SSL z niestandardowej nazwy domeny, należy uzyskać SSL certyfikatów i skonfigurować toouse aplikacji sieci web go.</span><span class="sxs-lookup"><span data-stu-id="fb522-126">toouse SSL with a custom domain name, you must get an SSL certificate and configure your web app toouse it.</span></span> <span data-ttu-id="fb522-127">Zobacz [Włącz protokół HTTPS dla aplikacji sieci web w usłudze Azure App Service](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="fb522-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="fb522-128">**Nazwa domeny niestandardowej.**</span><span class="sxs-lookup"><span data-stu-id="fb522-128">**Custom domain name.**</span></span> <span data-ttu-id="fb522-129">Aplikacja sieci web ma automatycznie poddomeny w obszarze azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="fb522-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="fb522-130">Możesz skojarzyć niestandardowej nazwy domeny, np. contoso.com. Zobacz [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="fb522-130">You can associate a custom domain name, such as contoso.com. See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="fb522-131">Konfiguracja specyficzny dla języka:</span><span class="sxs-lookup"><span data-stu-id="fb522-131">Language-specific configuration:</span></span>

* <span data-ttu-id="fb522-132">**PHP**: [skonfigurować PHP w aplikacjach sieci Web usługi aplikacji Azure](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="fb522-132">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="fb522-133">**Python**: [Konfigurowanie Python z usługi aplikacji Azure Web Apps](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="fb522-133">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="fb522-134">Aplikacja sieci web jest uruchomiona</span><span class="sxs-lookup"><span data-stu-id="fb522-134">While your web app is running</span></span>
<span data-ttu-id="fb522-135">Po uruchomieniu aplikacji sieci web ma toomake się, że jest dostępny i że skaluje się toomeet ruchu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fb522-135">While your web app is running, you want toomake sure it is available, and that it scales toomeet user traffic.</span></span> <span data-ttu-id="fb522-136">Możesz także tootroubleshoot błędy.</span><span class="sxs-lookup"><span data-stu-id="fb522-136">You may also need tootroubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="fb522-137">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="fb522-137">Monitoring</span></span>
* <span data-ttu-id="fb522-138">Za pomocą hello portalu Azure, możesz [dodać metryki wydajności](web-sites-monitor.md) użycia procesora CPU i liczby żądań klientów.</span><span class="sxs-lookup"><span data-stu-id="fb522-138">Through hello Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="fb522-139">[Skalowanie aplikacji sieci web](web-sites-scale.md) w tootraffic odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fb522-139">[Scale your web app](web-sites-scale.md) in response tootraffic.</span></span> <span data-ttu-id="fb522-140">W zależności od warstwę można skalować hello liczbę maszyn wirtualnych i/lub rozmiaru hello hello wystąpień maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="fb522-140">Depending on your tier, you can scale hello number of VMs and/or hello size of hello VM instances.</span></span> <span data-ttu-id="fb522-141">W hello Standard i Premium warstw można również skonfigurować Skalowanie automatyczne, dzięki aplikacji sieci web skaluje automatycznie, zgodnie z ustalonym harmonogramem lub w tooload odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="fb522-141">In hello Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response tooload.</span></span>  

### <a name="backups"></a><span data-ttu-id="fb522-142">Tworzenie kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="fb522-142">Backups</span></span>
* <span data-ttu-id="fb522-143">Ustaw [automatycznego tworzenia kopii zapasowych](web-sites-backup.md) aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="fb522-143">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="fb522-144">Dowiedz się więcej na temat tworzenia kopii zapasowych w [ten film](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="fb522-144">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="fb522-145">Dowiedz się więcej o opcjach hello [odzyskiwanie bazy danych](../sql-database/sql-database-business-continuity.md) w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fb522-145">Learn about hello options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="fb522-146">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="fb522-146">Troubleshooting</span></span>
* <span data-ttu-id="fb522-147">Jeśli jakaś nieprawidłowość, możesz [Rozwiązywanie problemów w programie Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), przy użyciu dzienników diagnostycznych i debugowania w chmurze hello na żywo.</span><span class="sxs-lookup"><span data-stu-id="fb522-147">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in hello cloud.</span></span> 
* <span data-ttu-id="fb522-148">Poza Visual Studio istnieją różne sposoby toocollect diagnostycznych dzienników.</span><span class="sxs-lookup"><span data-stu-id="fb522-148">Outside of Visual Studio, there are various ways toocollect diagnostic logs.</span></span> <span data-ttu-id="fb522-149">Zobacz [Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="fb522-149">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="fb522-150">Dla aplikacji programu Node.js [jak toodebug Node.js sieci web aplikacji w usłudze Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="fb522-150">For Node.js applications, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="fb522-151">Przywracanie danych</span><span class="sxs-lookup"><span data-stu-id="fb522-151">Restoring Data</span></span>
* <span data-ttu-id="fb522-152">[Przywróć](web-sites-restore.md) aplikacji sieci web, która została wcześniej utworzona kopia zapasowa.</span><span class="sxs-lookup"><span data-stu-id="fb522-152">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="fb522-153">Podczas aktualizacji aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="fb522-153">When you update your web app</span></span>
<span data-ttu-id="fb522-154">Jeśli nie włączono automatycznego tworzenia kopii zapasowych, możesz utworzyć [ręcznego wykonywania kopii zapasowej](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="fb522-154">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="fb522-155">Należy rozważyć użycie [przemieszczane wdrożenia](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="fb522-155">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="fb522-156">Ta opcja umożliwia publikowanie przemieszczania wdrożenia, który uruchamia side-by-side tooa aktualizacje z wdrożeniem w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="fb522-156">This option lets you publish updates tooa staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


