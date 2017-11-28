---
title: "aaaSCOM integracji z usługą Application Insights | Dokumentacja firmy Microsoft"
description: "Jeśli jesteś użytkownikiem SCOM monitorowania wydajności i diagnozowanie problemów z usługą Application Insights. Kompleksowe pulpity nawigacyjne, inteligentne alertów, zaawansowanych narzędzi diagnostycznych i zapytań analiz."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="03751-104">Monitorowanie wydajności aplikacji za pomocą usługi Application Insights dla oprogramowania SCOM</span><span class="sxs-lookup"><span data-stu-id="03751-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="03751-105">Jeśli używasz programu System Center Operations Manager (SCOM) toomanage serwerów, można monitorować wydajność i diagnozowanie problemów z wydajnością z pomocy hello [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="03751-105">If you use System Center Operations Manager (SCOM) toomanage your servers, you can monitor performance and diagnose performance issues with hello help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="03751-106">Usługi Application Insights monitoruje aplikację sieci web żądania przychodzące, wychodzące REST i wywołania SQL, wyjątków i ślady dziennika.</span><span class="sxs-lookup"><span data-stu-id="03751-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="03751-107">Zapewnia on pulpity nawigacyjne z wykresami metryki i inteligentne alerty, a także zaawansowane wyszukiwanie diagnostycznych i zapytania analityczne przez ten telemetrii.</span><span class="sxs-lookup"><span data-stu-id="03751-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="03751-108">Można przełączyć na monitorowanie usługi Application Insights przy użyciu pakietu administracyjnego programu SCOM.</span><span class="sxs-lookup"><span data-stu-id="03751-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="03751-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="03751-109">Before you start</span></span>
<span data-ttu-id="03751-110">Przyjęto założenie:</span><span class="sxs-lookup"><span data-stu-id="03751-110">We assume:</span></span>

* <span data-ttu-id="03751-111">Serwery sieci web znasz SCOM i korzystanie z programu SCOM 2012 R2 lub 2016 toomanage programu IIS.</span><span class="sxs-lookup"><span data-stu-id="03751-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 toomanage your IIS web servers.</span></span>
* <span data-ttu-id="03751-112">Użytkownik zainstalował już na serwerach aplikacji sieci web, które mają toomonitor z usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="03751-112">You have already installed on your servers a web application that you want toomonitor with Application Insights.</span></span>
* <span data-ttu-id="03751-113">Wersja platformy aplikacji jest .NET 4.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="03751-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="03751-114">Masz subskrypcję tooa dostępu [Microsoft Azure](https://azure.com) i zalogować się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03751-114">You have access tooa subscription in [Microsoft Azure](https://azure.com) and can sign in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="03751-115">Organizacji mogą mieć subskrypcję i dodać Twojego tooit konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="03751-115">Your organization may have a subscription, and can add your Microsoft account tooit.</span></span>

<span data-ttu-id="03751-116">(zespół deweloperów hello może zbudować hello [zestaw SDK usługi Application Insights](app-insights-asp-net.md) do aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="03751-116">(hello development team might build hello [Application Insights SDK](app-insights-asp-net.md) into hello web app.</span></span> <span data-ttu-id="03751-117">Instrumentacja to czas kompilacji daje im większa elastyczność w pisaniu telemetria niestandardowa.</span><span class="sxs-lookup"><span data-stu-id="03751-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="03751-118">Jednak nie ma znaczenia,:, można wykonać hello czynności opisane w tym miejscu lub bez hello wbudowany zestaw SDK.)</span><span class="sxs-lookup"><span data-stu-id="03751-118">However, it doesn't matter: you can follow hello steps described here either with or without hello SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="03751-119">(Jeden raz) Zainstaluj pakiet administracyjny usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="03751-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="03751-120">Na komputerze hello realizującym programu Operations Manager:</span><span class="sxs-lookup"><span data-stu-id="03751-120">On hello machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="03751-121">Odinstaluj wszelkie starą wersję pakietu administracyjnego hello:</span><span class="sxs-lookup"><span data-stu-id="03751-121">Uninstall any old version of hello management pack:</span></span>
   1. <span data-ttu-id="03751-122">W programie Operations Manager Otwórz administracji, pakietów administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="03751-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="03751-123">Usuń starą wersję hello.</span><span class="sxs-lookup"><span data-stu-id="03751-123">Delete hello old version.</span></span>
2. <span data-ttu-id="03751-124">Pobierz i zainstaluj pakiet administracyjny hello z hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="03751-124">Download and install hello management pack from hello catalog.</span></span>
3. <span data-ttu-id="03751-125">Ponowne uruchomienie programu Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="03751-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="03751-126">Utwórz pakiet administracyjny</span><span class="sxs-lookup"><span data-stu-id="03751-126">Create a management pack</span></span>
1. <span data-ttu-id="03751-127">W programie Operations Manager, otwórz **tworzenie**, **.NET... with usługi Application Insights**, **Kreator dodawania monitorowania**i ponownie wybierz **.NET... z aplikacją Informacje na temat technologii**.</span><span class="sxs-lookup"><span data-stu-id="03751-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="03751-128">Nazwa konfiguracji powitania po aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03751-128">Name hello configuration after your app.</span></span> <span data-ttu-id="03751-129">(Masz tooinstrument jedną aplikację naraz.)</span><span class="sxs-lookup"><span data-stu-id="03751-129">(You have tooinstrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="03751-130">Na hello sama strona kreatora tworzenia nowej zarządzania dodatkiem Service pack, lub wybierz pakiet, który wcześniej utworzony dla usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="03751-130">On hello same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="03751-131">(hello usługi Application Insights [pakiet administracyjny](https://technet.microsoft.com/library/cc974491.aspx) szablonem, z którego można utworzyć wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="03751-131">(hello Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="03751-132">Można użyć ponownie hello samo wystąpienie później.)</span><span class="sxs-lookup"><span data-stu-id="03751-132">You can reuse hello same instance later.)</span></span>

    ![W hello karta Ogólne właściwości wpisz nazwę hello aplikacji hello.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="03751-136">Wybierz jedną aplikację, które mają toomonitor.</span><span class="sxs-lookup"><span data-stu-id="03751-136">Choose one app that you want toomonitor.</span></span> <span data-ttu-id="03751-137">Hello funkcja wyszukiwania wyszukuje między aplikacji zainstalowanych na serwerach.</span><span class="sxs-lookup"><span data-stu-id="03751-137">hello search feature searches among apps installed on your servers.</span></span>
   
    ![Na jakie kartę tooMonitor kliknij przycisk Dodaj, wpisz część nazwy aplikacji hello, kliknij przycisk Wyszukaj, wybierz OK aplikacji hello, a następnie Dodaj.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="03751-139">Hello pole opcjonalne zakresu monitorowania może być używane toospecify podzestawu serwerów, jeśli nie chcesz, aby aplikacja hello toomonitor na wszystkich serwerach.</span><span class="sxs-lookup"><span data-stu-id="03751-139">hello optional Monitoring scope field can be used toospecify a subset of your servers, if you don't want toomonitor hello app in all servers.</span></span>
2. <span data-ttu-id="03751-140">Na następnej stronie kreatora hello musisz podać toosign Twoje poświadczenia w tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="03751-140">On hello next wizard page, you must first provide your credentials toosign in tooMicrosoft Azure.</span></span>
   
    <span data-ttu-id="03751-141">Na tej stronie wybierz polecenie zasobu usługi Application Insights hello miejscu hello toobe danych telemetrycznych przeanalizowany i wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="03751-141">On this page, you choose hello Application Insights resource where you want hello telemetry data toobe analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="03751-142">Jeśli aplikacja hello został skonfigurowany dla usługi Application Insights podczas tworzenia, wybierz jej istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="03751-142">If hello application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="03751-143">W przeciwnym razie utwórz nowy zasób o nazwie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="03751-143">Otherwise, create a new resource named for hello app.</span></span> <span data-ttu-id="03751-144">Jeśli istnieją inne aplikacje, które są składnikami programu hello tego samego systemu, umieść je w hello tej samej grupie zasobów, toomanage łatwiejsze toohello telemetrii toomake dostępu.</span><span class="sxs-lookup"><span data-stu-id="03751-144">If there are other apps that are components of hello same system, put them in hello same resource group, toomake access toohello telemetry easier toomanage.</span></span>
     
     <span data-ttu-id="03751-145">Te ustawienia można zmienić później.</span><span class="sxs-lookup"><span data-stu-id="03751-145">You can change these settings later.</span></span>
     
     ![Na karcie Ustawienia usługi Application Insights kliknij przycisk "Zarejestruj" i podaj poświadczenia konta Microsoft Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="03751-148">Kreator hello ukończone.</span><span class="sxs-lookup"><span data-stu-id="03751-148">Complete hello wizard.</span></span>
   
    ![Kliknięcie pozycji Utwórz](./media/app-insights-scom/070.png)

<span data-ttu-id="03751-150">Powtórz tę procedurę dla każdej aplikacji, które mają toomonitor.</span><span class="sxs-lookup"><span data-stu-id="03751-150">Repeat this procedure for each app that you want toomonitor.</span></span>

<span data-ttu-id="03751-151">Ustawienia toochange później, należy ponownie otworzyć właściwości hello hello monitora z okna Tworzenie hello.</span><span class="sxs-lookup"><span data-stu-id="03751-151">If you need toochange settings later, re-open hello properties of hello monitor from hello Authoring window.</span></span>

![W tworzenie, wybierz opcję monitorowanie wydajności aplikacji .NET z usługi Application Insights, wybierz monitora, a następnie kliknij przycisk Właściwości.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="03751-153">Sprawdź monitorowania</span><span class="sxs-lookup"><span data-stu-id="03751-153">Verify monitoring</span></span>
<span data-ttu-id="03751-154">monitor Hello na każdym serwerze zainstalowano wyszukiwania dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03751-154">hello monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="03751-155">Gdy znajdzie aplikacji hello konfiguruje aplikacji hello toomonitor Monitor stanu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="03751-155">Where it finds hello app, it configures Application Insights Status Monitor toomonitor hello app.</span></span> <span data-ttu-id="03751-156">W razie potrzeby najpierw instaluje Monitor stanu na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="03751-156">If necessary, it first installs Status Monitor on hello server.</span></span>

<span data-ttu-id="03751-157">Aby sprawdzić, które wystąpienia aplikacji hello znaleziono:</span><span class="sxs-lookup"><span data-stu-id="03751-157">You can verify which instances of hello app it has found:</span></span>

![Monitorowanie, otwórz usługę Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="03751-159">Dane telemetryczne wyświetleń w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="03751-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="03751-160">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03751-160">In hello [Azure portal](https://portal.azure.com), browse toohello resource for your app.</span></span> <span data-ttu-id="03751-161">Możesz [zobaczyć wykresy przedstawiający telemetrii](app-insights-dashboards.md) z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03751-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="03751-162">(Jeśli go nie pokazano na stronie głównej hello jeszcze, kliknij strumień na żywo metryk).</span><span class="sxs-lookup"><span data-stu-id="03751-162">(If it hasn't shown up on hello main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="03751-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="03751-163">Next steps</span></span>
* <span data-ttu-id="03751-164">[Konfigurowanie pulpitu nawigacyjnego](app-insights-dashboards.md) toobring razem hello najważniejszych wykresy monitorowania to i inne aplikacje.</span><span class="sxs-lookup"><span data-stu-id="03751-164">[Set up a dashboard](app-insights-dashboards.md) toobring together hello most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="03751-165">Dowiedz się więcej o metryk</span><span class="sxs-lookup"><span data-stu-id="03751-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="03751-166">Konfigurowanie alertów</span><span class="sxs-lookup"><span data-stu-id="03751-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="03751-167">Diagnozowanie problemów z wydajnością</span><span class="sxs-lookup"><span data-stu-id="03751-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="03751-168">Zaawansowane zapytania analityczne</span><span class="sxs-lookup"><span data-stu-id="03751-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="03751-169">Dostępność testy sieci web</span><span class="sxs-lookup"><span data-stu-id="03751-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

