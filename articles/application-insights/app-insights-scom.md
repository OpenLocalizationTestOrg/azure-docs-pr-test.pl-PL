---
title: "Integracja programu SCOM z usługi Application Insights | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 9c205465981fabdbb696cdc44f765532bbb992b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="56591-104">Monitorowanie wydajności aplikacji za pomocą usługi Application Insights dla oprogramowania SCOM</span><span class="sxs-lookup"><span data-stu-id="56591-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="56591-105">Jeśli używasz programu System Center Operations Manager (SCOM) do zarządzania serwerami, można monitorować wydajność i diagnozowanie problemów z wydajnością przy pomocy [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="56591-105">If you use System Center Operations Manager (SCOM) to manage your servers, you can monitor performance and diagnose performance issues with the help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="56591-106">Usługi Application Insights monitoruje aplikację sieci web żądania przychodzące, wychodzące REST i wywołania SQL, wyjątków i ślady dziennika.</span><span class="sxs-lookup"><span data-stu-id="56591-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="56591-107">Zapewnia on pulpity nawigacyjne z wykresami metryki i inteligentne alerty, a także zaawansowane wyszukiwanie diagnostycznych i zapytania analityczne przez ten telemetrii.</span><span class="sxs-lookup"><span data-stu-id="56591-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="56591-108">Można przełączyć na monitorowanie usługi Application Insights przy użyciu pakietu administracyjnego programu SCOM.</span><span class="sxs-lookup"><span data-stu-id="56591-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="56591-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="56591-109">Before you start</span></span>
<span data-ttu-id="56591-110">Przyjęto założenie:</span><span class="sxs-lookup"><span data-stu-id="56591-110">We assume:</span></span>

* <span data-ttu-id="56591-111">Serwery sieci web znasz SCOM i użyj SCOM 2012 R2 lub 2016 do zarządzania programu IIS.</span><span class="sxs-lookup"><span data-stu-id="56591-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 to manage your IIS web servers.</span></span>
* <span data-ttu-id="56591-112">Zostały już zainstalowane na serwerach aplikacji sieci web, który chcesz monitorować za pomocą usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="56591-112">You have already installed on your servers a web application that you want to monitor with Application Insights.</span></span>
* <span data-ttu-id="56591-113">Wersja platformy aplikacji jest .NET 4.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="56591-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="56591-114">Masz dostęp do subskrypcji w [Microsoft Azure](https://azure.com) i zalogować się do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="56591-114">You have access to a subscription in [Microsoft Azure](https://azure.com) and can sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="56591-115">Twoja organizacja może mieć subskrypcję, a do niej dodać konto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="56591-115">Your organization may have a subscription, and can add your Microsoft account to it.</span></span>

<span data-ttu-id="56591-116">(Zespół deweloperów może zbudować [zestaw SDK usługi Application Insights](app-insights-asp-net.md) do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="56591-116">(The development team might build the [Application Insights SDK](app-insights-asp-net.md) into the web app.</span></span> <span data-ttu-id="56591-117">Instrumentacja to czas kompilacji daje im większa elastyczność w pisaniu telemetria niestandardowa.</span><span class="sxs-lookup"><span data-stu-id="56591-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="56591-118">Jednak nie ma znaczenia: możesz wykonać kroki opisane w tym miejscu lub bez wbudowany zestaw SDK.)</span><span class="sxs-lookup"><span data-stu-id="56591-118">However, it doesn't matter: you can follow the steps described here either with or without the SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="56591-119">(Jeden raz) Zainstaluj pakiet administracyjny usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="56591-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="56591-120">Na komputerze, na którym uruchamiasz programu Operations Manager:</span><span class="sxs-lookup"><span data-stu-id="56591-120">On the machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="56591-121">Odinstaluj wszelkie starą wersję pakietu administracyjnego:</span><span class="sxs-lookup"><span data-stu-id="56591-121">Uninstall any old version of the management pack:</span></span>
   1. <span data-ttu-id="56591-122">W programie Operations Manager Otwórz administracji, pakietów administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="56591-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="56591-123">Usuń starą wersję.</span><span class="sxs-lookup"><span data-stu-id="56591-123">Delete the old version.</span></span>
2. <span data-ttu-id="56591-124">Pobierz i zainstaluj pakiet administracyjny z katalogu.</span><span class="sxs-lookup"><span data-stu-id="56591-124">Download and install the management pack from the catalog.</span></span>
3. <span data-ttu-id="56591-125">Ponowne uruchomienie programu Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="56591-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="56591-126">Utwórz pakiet administracyjny</span><span class="sxs-lookup"><span data-stu-id="56591-126">Create a management pack</span></span>
1. <span data-ttu-id="56591-127">W programie Operations Manager, otwórz **tworzenie**, **.NET... with usługi Application Insights**, **Kreator dodawania monitorowania**i ponownie wybierz **.NET... z aplikacją Informacje na temat technologii**.</span><span class="sxs-lookup"><span data-stu-id="56591-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="56591-128">Nazwa konfiguracji po aplikacji.</span><span class="sxs-lookup"><span data-stu-id="56591-128">Name the configuration after your app.</span></span> <span data-ttu-id="56591-129">(Należy Instrumentacja jedną aplikację naraz.)</span><span class="sxs-lookup"><span data-stu-id="56591-129">(You have to instrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="56591-130">Na tej samej stronie kreatora Utwórz nowy pakiet administracyjny albo wybierz pakiet, który wcześniej utworzony dla usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="56591-130">On the same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="56591-131">(W usłudze Application Insights [pakiet administracyjny](https://technet.microsoft.com/library/cc974491.aspx) szablonem, z którego można utworzyć wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="56591-131">(The Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="56591-132">Można ponownie użyć tego samego wystąpienia później.)</span><span class="sxs-lookup"><span data-stu-id="56591-132">You can reuse the same instance later.)</span></span>

    ![Na karcie Ogólne właściwości wpisz nazwę aplikacji.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="56591-136">Wybierz jedną aplikację, która ma być monitorowany.</span><span class="sxs-lookup"><span data-stu-id="56591-136">Choose one app that you want to monitor.</span></span> <span data-ttu-id="56591-137">Funkcja wyszukiwania wyszukuje między aplikacji zainstalowanych na serwerach.</span><span class="sxs-lookup"><span data-stu-id="56591-137">The search feature searches among apps installed on your servers.</span></span>
   
    ![Co na karcie monitorowanie kliknij przycisk Dodaj, wpisz część nazwy aplikacji, kliknij przycisk Wyszukaj, wybierz aplikację, a następnie dodaj OK.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="56591-139">Pole opcjonalne zakresu monitorowania można określić podzestaw serwerów, jeśli nie chcesz monitorować aplikację na wszystkich serwerach.</span><span class="sxs-lookup"><span data-stu-id="56591-139">The optional Monitoring scope field can be used to specify a subset of your servers, if you don't want to monitor the app in all servers.</span></span>
2. <span data-ttu-id="56591-140">Na następnej stronie kreatora musisz podać swoje poświadczenia, aby zalogować się do systemu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="56591-140">On the next wizard page, you must first provide your credentials to sign in to Microsoft Azure.</span></span>
   
    <span data-ttu-id="56591-141">Na tej stronie wybierz polecenie zasobu usługi Application Insights miejscu danych telemetrycznych i przeanalizowane.</span><span class="sxs-lookup"><span data-stu-id="56591-141">On this page, you choose the Application Insights resource where you want the telemetry data to be analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="56591-142">Jeśli aplikacja została skonfigurowana pod kątem usługi Application Insights podczas tworzenia, wybierz jej istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="56591-142">If the application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="56591-143">W przeciwnym razie utwórz nowy zasób o nazwie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="56591-143">Otherwise, create a new resource named for the app.</span></span> <span data-ttu-id="56591-144">Jeśli istnieją inne aplikacje, które są składnikami tego samego systemu, umieść je w tej samej grupie zasobów, aby ułatwić dostęp na podstawie danych telemetrycznych do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="56591-144">If there are other apps that are components of the same system, put them in the same resource group, to make access to the telemetry easier to manage.</span></span>
     
     <span data-ttu-id="56591-145">Te ustawienia można zmienić później.</span><span class="sxs-lookup"><span data-stu-id="56591-145">You can change these settings later.</span></span>
     
     ![Na karcie Ustawienia usługi Application Insights kliknij przycisk "Zarejestruj" i podaj poświadczenia konta Microsoft Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="56591-148">Ukończ pracę kreatora.</span><span class="sxs-lookup"><span data-stu-id="56591-148">Complete the wizard.</span></span>
   
    ![Kliknięcie pozycji Utwórz](./media/app-insights-scom/070.png)

<span data-ttu-id="56591-150">Powtórz tę procedurę dla każdej aplikacji, które chcesz monitorować.</span><span class="sxs-lookup"><span data-stu-id="56591-150">Repeat this procedure for each app that you want to monitor.</span></span>

<span data-ttu-id="56591-151">Jeśli trzeba zmienić ustawienia, ponownie otwórz właściwości monitora z okna Tworzenie.</span><span class="sxs-lookup"><span data-stu-id="56591-151">If you need to change settings later, re-open the properties of the monitor from the Authoring window.</span></span>

![W tworzenie, wybierz opcję monitorowanie wydajności aplikacji .NET z usługi Application Insights, wybierz monitora, a następnie kliknij przycisk Właściwości.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="56591-153">Sprawdź monitorowania</span><span class="sxs-lookup"><span data-stu-id="56591-153">Verify monitoring</span></span>
<span data-ttu-id="56591-154">Monitor, na każdym serwerze zainstalowano wyszukiwania dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="56591-154">The monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="56591-155">Gdy znajdzie aplikacji, ponieważ konfiguruje Monitor stanu usługi Application Insights do monitorowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="56591-155">Where it finds the app, it configures Application Insights Status Monitor to monitor the app.</span></span> <span data-ttu-id="56591-156">W razie potrzeby najpierw instaluje Monitor stanu na serwerze.</span><span class="sxs-lookup"><span data-stu-id="56591-156">If necessary, it first installs Status Monitor on the server.</span></span>

<span data-ttu-id="56591-157">Aby sprawdzić, które wystąpienia aplikacji znalazła:</span><span class="sxs-lookup"><span data-stu-id="56591-157">You can verify which instances of the app it has found:</span></span>

![Monitorowanie, otwórz usługę Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="56591-159">Dane telemetryczne wyświetleń w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="56591-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="56591-160">W [portalu Azure](https://portal.azure.com), przejdź do zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="56591-160">In the [Azure portal](https://portal.azure.com), browse to the resource for your app.</span></span> <span data-ttu-id="56591-161">Możesz [zobaczyć wykresy przedstawiający telemetrii](app-insights-dashboards.md) z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="56591-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="56591-162">(Jeśli go nie nie pojawiają na stronie głównej jeszcze, kliknij strumień na żywo metryk).</span><span class="sxs-lookup"><span data-stu-id="56591-162">(If it hasn't shown up on the main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="56591-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="56591-163">Next steps</span></span>
* <span data-ttu-id="56591-164">[Konfigurowanie pulpitu nawigacyjnego](app-insights-dashboards.md) ze sobą najważniejszych wykresy monitorowania to i inne aplikacje.</span><span class="sxs-lookup"><span data-stu-id="56591-164">[Set up a dashboard](app-insights-dashboards.md) to bring together the most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="56591-165">Dowiedz się więcej o metryk</span><span class="sxs-lookup"><span data-stu-id="56591-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="56591-166">Konfigurowanie alertów</span><span class="sxs-lookup"><span data-stu-id="56591-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="56591-167">Diagnozowanie problemów z wydajnością</span><span class="sxs-lookup"><span data-stu-id="56591-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="56591-168">Zaawansowane zapytania analityczne</span><span class="sxs-lookup"><span data-stu-id="56591-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="56591-169">Dostępność testy sieci web</span><span class="sxs-lookup"><span data-stu-id="56591-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

