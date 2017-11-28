---
title: "Omówienie połączonej fabryki Pakietu Azure IoT | Microsoft Docs"
description: "Opis wstępnie skonfigurowanego rozwiązania połączonej fabryki Pakietu Azure IoT."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: d502c8e2e2715899279f6ebcf7ed89c19a1bb9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-connected-factory-preconfigured-solution"></a><span data-ttu-id="ab27a-103">Wprowadzenie do wstępnie skonfigurowanego rozwiązania połączonej fabryki</span><span class="sxs-lookup"><span data-stu-id="ab27a-103">Get started with the connected factory preconfigured solution</span></span>

<span data-ttu-id="ab27a-104">[Wstępnie skonfigurowane rozwiązania][lnk-preconfigured-solutions] Pakietu IoT Azure obejmują wiele usług Azure IoT, co pozwala dostarczać kompleksowe rozwiązania, które umożliwiają implementowanie typowych scenariuszy biznesowych IoT.</span><span class="sxs-lookup"><span data-stu-id="ab27a-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="ab27a-105">Wstępnie skonfigurowane rozwiązanie *połączonej fabryki* łączy i monitoruje urządzenia przemysłowe.</span><span class="sxs-lookup"><span data-stu-id="ab27a-105">The *connected factory* preconfigured solution connects to and monitors your industrial devices.</span></span> <span data-ttu-id="ab27a-106">To rozwiązanie może służyć do analizowania strumienia danych z urządzeń i zwiększania produktywności operacyjnej oraz rentowności.</span><span class="sxs-lookup"><span data-stu-id="ab27a-106">You can use the solution to analyze the stream of data from your devices and to drive operational productivity and profitability.</span></span>

<span data-ttu-id="ab27a-107">W tym samouczku przedstawiono sposób aprowizowania wstępnie skonfigurowanego rozwiązania połączonej fabryki.</span><span class="sxs-lookup"><span data-stu-id="ab27a-107">This tutorial shows you how to provision the connected factory preconfigured solution.</span></span> <span data-ttu-id="ab27a-108">Dostępny jest również opis podstawowych funkcji wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ab27a-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="ab27a-109">Dostęp do wielu z tych funkcji można uzyskać z *pulpitu nawigacyjnego* rozwiązania, który jest wdrażany jako część wstępnie skonfigurowanego rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="ab27a-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania połączonej fabryki][img-cf-home]

<span data-ttu-id="ab27a-111">Do wykonania kroków tego samouczka jest potrzebna aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab27a-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="ab27a-112">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="ab27a-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ab27a-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="ab27a-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-the-solution"></a><span data-ttu-id="ab27a-114">Aprowizacja rozwiązania</span><span class="sxs-lookup"><span data-stu-id="ab27a-114">Provision the solution</span></span>

1. <span data-ttu-id="ab27a-115">Zaloguj się w witrynie azureiotsuite.com przy użyciu poświadczeń konta platformy Azure i kliknij pozycję „**+**”, aby utworzyć rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="ab27a-115">Log on to azureiotsuite.com using your Azure account credentials, and click "**+**" to create a solution.</span></span>
2. <span data-ttu-id="ab27a-116">Kliknij pozycję **Wybierz** na kafelku **Połączona fabryka**.</span><span class="sxs-lookup"><span data-stu-id="ab27a-116">Click **Select** on the **Connected factory** tile.</span></span>
3. <span data-ttu-id="ab27a-117">W polu **Nazwa rozwiązania** wprowadź nazwę wstępnie skonfigurowanego rozwiązania dla połączonej fabryki.</span><span class="sxs-lookup"><span data-stu-id="ab27a-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="ab27a-118">W polach **Subskrypcja** i **Region** wybierz wartości, których chcesz użyć do aprowizacji rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ab27a-118">Select the **Subscription** and **Region** you want to use to provision the solution.</span></span>
5. <span data-ttu-id="ab27a-119">Kliknij pozycję **Utwórz rozwiązanie**, aby rozpocząć proces aprowizowania.</span><span class="sxs-lookup"><span data-stu-id="ab27a-119">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="ab27a-120">Zwykle trwa on kilka minut.</span><span class="sxs-lookup"><span data-stu-id="ab27a-120">This process typically takes several minutes to run.</span></span>

### <a name="while-you-wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="ab27a-121">Podczas oczekiwania na ukończenie procesu aprowizacji</span><span class="sxs-lookup"><span data-stu-id="ab27a-121">While you wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="ab27a-122">Kliknij kafelek swojego rozwiązania zawierający informację o stanie **aprowizacji**.</span><span class="sxs-lookup"><span data-stu-id="ab27a-122">Click the tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="ab27a-123">Zwróć uwagę na informację o **stanach aprowizacji** podczas wdrażania usług Azure w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab27a-123">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="ab27a-124">Po ukończeniu aprowizowania stan zmieni się na wartość **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="ab27a-124">Once provisioning completes, the status changes to **Ready**.</span></span>
4. <span data-ttu-id="ab27a-125">Kliknij kafelek, aby wyświetlić szczegóły rozwiązania w prawym okienku.</span><span class="sxs-lookup"><span data-stu-id="ab27a-125">Click the tile to see the details of your solution in the right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="ab27a-126">Jeśli podczas wdrażania wstępnie skonfigurowanego rozwiązania pojawią się problemy, zapoznaj się z tematami [Uprawnienia w witrynie azureiotsuite.com][lnk-permissions] i [Connected factory FAQ (Połączona fabryka — często zadawane pytania)](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="ab27a-126">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="ab27a-127">Jeśli problemy będą się powtarzać, utwórz żądanie pomocy w [portalu][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="ab27a-127">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="ab27a-128">Czy istnieją jakieś szczegóły dotyczące Twojego rozwiązania, które nie są wyświetlane, a Twoim zdaniem powinny być widoczne?</span><span class="sxs-lookup"><span data-stu-id="ab27a-128">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="ab27a-129">Prześlij nam swoje propozycje dotyczące funkcji, korzystając ze strony [User Voice](https://feedback.azure.com/forums/321918-azure-iot) (Opinie użytkowników).</span><span class="sxs-lookup"><span data-stu-id="ab27a-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="ab27a-130">Omówienie scenariusza</span><span class="sxs-lookup"><span data-stu-id="ab27a-130">Scenario overview</span></span>

<span data-ttu-id="ab27a-131">Podczas wdrażania wstępnie skonfigurowanego rozwiązania połączonej fabryki jest ono wstępnie wypełniane zasobami, które umożliwiają wykonanie kroków opisanych w typowym scenariuszu przemysłowym.</span><span class="sxs-lookup"><span data-stu-id="ab27a-131">When you deploy the connected factory preconfigured solution, it is prepopulated with resources that enable you to step through a common industrial scenario.</span></span> <span data-ttu-id="ab27a-132">W tym scenariuszu kilka fabryk połączonych z rozwiązaniem raportuje wartości danych wymagane do obliczenia ogólnej wydajności sprzętu (OEE) oraz kluczowych wskaźników wydajności (KPI).</span><span class="sxs-lookup"><span data-stu-id="ab27a-132">In this scenario, several factories connected to the solution report the data values required to compute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="ab27a-133">W poniższych sekcjach opisano sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="ab27a-133">The following sections show you how to:</span></span>

* <span data-ttu-id="ab27a-134">Monitorowanie fabryki, linii produkcyjnych, ogólnej wydajności stacji i wartości kluczowych wskaźników wydajności.</span><span class="sxs-lookup"><span data-stu-id="ab27a-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="ab27a-135">Analizowanie danych telemetrycznych generowanych przez te urządzenia za pomocą usługi Azure Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="ab27a-135">Analyze the telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="ab27a-136">Reagowanie na alerty i rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="ab27a-136">Act on alerts to fix issues</span></span>

<span data-ttu-id="ab27a-137">Kluczową cechą tego scenariusza jest to, że te wszystkie akcje można wykonać zdalnie z poziomu pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ab27a-137">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="ab27a-138">Nie jest konieczny fizyczny dostęp do urządzeń.</span><span class="sxs-lookup"><span data-stu-id="ab27a-138">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="ab27a-139">Wyświetlanie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="ab27a-139">View the solution dashboard</span></span>

<span data-ttu-id="ab27a-140">Pulpit nawigacyjny pozwala zarządzać wdrożonym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="ab27a-140">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="ab27a-141">Jest to hierarchiczna reprezentacja globalnej konfiguracji fabryki.</span><span class="sxs-lookup"><span data-stu-id="ab27a-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="ab27a-142">Można na przykład wyświetlić ogólną wydajność sprzętu oraz kluczowe wskaźniki wydajności, opublikować nowe węzły na potrzeby telemetrii i reagować na alerty.</span><span class="sxs-lookup"><span data-stu-id="ab27a-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="ab27a-143">Jeśli aprowizacja została ukończona, a na kafelku wstępnie skonfigurowanego rozwiązania jest wyświetlany stan **Gotowe**, wybierz pozycję **Uruchom**, aby otworzyć portal rozwiązania połączonej fabryki na nowej karcie.</span><span class="sxs-lookup"><span data-stu-id="ab27a-143">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your connected factory solution portal in a new tab.</span></span>

    ![Uruchamianie wstępnie skonfigurowanego rozwiązania][img-launch-solution]

1. <span data-ttu-id="ab27a-145">Domyślnie w portalu rozwiązania jest wyświetlany *pulpit nawigacyjny*.</span><span class="sxs-lookup"><span data-stu-id="ab27a-145">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="ab27a-146">Korzystając z menu znajdującego się w lewej części strony, można przejść do innych obszarów portalu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-146">To navigate to other areas of the portal, use the menu on the left-hand side of the page.</span></span>

    ![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania połączonej fabryki][cf-img-menu]

<span data-ttu-id="ab27a-148">Pulpit nawigacyjny udostępnia następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="ab27a-148">The dashboard displays the following information:</span></span>

* <span data-ttu-id="ab27a-149">Panel **Lista fabryk**, który przedstawia stan, lokalizację i bieżącą konfigurację produkcji w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-149">A **Factory list** panel that shows the status, location, and current production configuration in the solution.</span></span> <span data-ttu-id="ab27a-150">Przy pierwszym uruchomieniu rozwiązania dostępnych jest kilka symulowanych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="ab27a-150">When you first run the solution, there are a number of simulated devices.</span></span> <span data-ttu-id="ab27a-151">Symulacja linii produkcyjnej składa się z trzech prawdziwych serwerów OPC UA na każdą linię produkcyjną, które wykonują symulowane zadania i udostępniają dane.</span><span class="sxs-lookup"><span data-stu-id="ab27a-151">The production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="ab27a-152">Aby uzyskać więcej informacji na temat OPC UA, zobacz [Connected factory FAQ (Połączona fabryka — często zadawane pytania)](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="ab27a-152">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="ab27a-153">**Mapę** zawierającą lokalizację każdego urządzenia połączonego z rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="ab27a-153">A **map** that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="ab27a-154">Rozwiązanie może korzystać z interfejsu API usługi Mapy Bing do wykreślania informacji na mapie.</span><span class="sxs-lookup"><span data-stu-id="ab27a-154">The solution can use the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="ab27a-155">Jeśli subskrypcja obejmuje interfejs API usługi Mapy Bing w wersji Enterprise, ta funkcja jest używana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ab27a-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="ab27a-156">W przeciwnym razie zobacz [Często zadawane pytania][lnk-faq], aby dowiedzieć się, jak utworzyć dynamiczną mapę.</span><span class="sxs-lookup"><span data-stu-id="ab27a-156">If not, see the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="ab27a-157">Panel **Alerty**, na którym są wyświetlane alerty generowane, gdy wartość telemetrii lub ogólnej wydajności sprzętu bądź kluczowego wskaźnika wydajności przekroczy określony próg.</span><span class="sxs-lookup"><span data-stu-id="ab27a-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="ab27a-158">Panel **Ogólna wydajność sprzętu**, na którym są pokazane wartości ogólnej wydajności sprzętu dla całego przedsiębiorstwa lub przeglądanej fabryki/linii produkcyjnej/stacji.</span><span class="sxs-lookup"><span data-stu-id="ab27a-158">An **Overall Equipment Efficiency** panel that shows the OEE values for the whole enterprise, or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="ab27a-159">Ta wartość jest agregowana od widoku stacji do poziomu przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="ab27a-159">This value is aggregated from the station view to the enterprise level.</span></span> <span data-ttu-id="ab27a-160">Dane ogólnej wydajności sprzętu i jej składowe elementy można dokładniej analizować.</span><span class="sxs-lookup"><span data-stu-id="ab27a-160">The OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="ab27a-161">Panel **Kluczowe wskaźniki wydajności**, na którym jest wyświetlana liczba wyprodukowanych jednostek i ilość zużytej energii w całym przedsiębiorstwie lub w przeglądanej fabryce/linii produkcyjnej/stacji.</span><span class="sxs-lookup"><span data-stu-id="ab27a-161">**Key Performance Indicators** panel that displays the number of units produced and energy used by the whole enterprise or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="ab27a-162">Te wartości są agregowane od widoku stacji do poziomu przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="ab27a-162">These values are aggregated from a station view to the enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="ab27a-163">Wyświetlanie fabryk</span><span class="sxs-lookup"><span data-stu-id="ab27a-163">View factories</span></span>

<span data-ttu-id="ab27a-164">Na panelu *Fabryki* jest wyświetlana lokalizacja geograficzna wszystkich fabryk w rozwiązaniu, ich stan i bieżąca konfiguracja produkcji.</span><span class="sxs-lookup"><span data-stu-id="ab27a-164">The *Factories* panel shows you the geographical location of all the factories in the solution, their status, and current production configuration.</span></span> <span data-ttu-id="ab27a-165">Z listy lokalizacji można przejść do innych poziomów w hierarchii rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ab27a-165">From the locations list, you can navigate to the other levels in the solution hierarchy.</span></span> <span data-ttu-id="ab27a-166">Wiersze listy są hiperlinkami umożliwiającymi wyświetlenie szczegółowych informacji dotyczących linii produkcyjnych w lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="ab27a-166">The rows in the list are hyperlinks that link details of the production lines at that location.</span></span> <span data-ttu-id="ab27a-167">Możliwe jest również przejście do szczegółów linii produkcyjnej i w dół do widoku poziomu stacji.</span><span class="sxs-lookup"><span data-stu-id="ab27a-167">It is then possible to drill into the production line details and down to the station level view.</span></span> <span data-ttu-id="ab27a-168">Do listy można także zastosować filtr.</span><span class="sxs-lookup"><span data-stu-id="ab27a-168">You can also apply a filter to the list.</span></span>

![Fabryki we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-factories] 

1. <span data-ttu-id="ab27a-170">Na **panelu Fabryki** jest wyświetlana lista fabryk dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ab27a-170">The **Factory panel** shows the factory list for this solution.</span></span>

2. <span data-ttu-id="ab27a-171">Na liście początkowo jest widocznych 6 fabryk utworzonych w procesie aprowizacji.</span><span class="sxs-lookup"><span data-stu-id="ab27a-171">The factory list initially shows six factories created by the provisioning process.</span></span> <span data-ttu-id="ab27a-172">Do rozwiązania można dodać dodatkowe symulowane i fizyczne urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ab27a-172">You can add additional simulated and physical devices to the solution.</span></span>

3. <span data-ttu-id="ab27a-173">Aby wyświetlić szczegóły fabryki, kliknij wiersz na liście fabryk.</span><span class="sxs-lookup"><span data-stu-id="ab27a-173">To view the details of a factory, click the row in the factory list.</span></span>

4. <span data-ttu-id="ab27a-174">Aby wyświetlić szczegóły linii produkcyjnej, kliknij wiersz na liście.</span><span class="sxs-lookup"><span data-stu-id="ab27a-174">To view the details of a production line, click the row in the list.</span></span>

5. <span data-ttu-id="ab27a-175">Aby wyświetlić opublikowane węzły OPC UA stacji z linii produkcyjnej, kliknij wiersz na liście.</span><span class="sxs-lookup"><span data-stu-id="ab27a-175">To view the published OPC UA nodes of a station on the production line, click the row in the list.</span></span>

6. <span data-ttu-id="ab27a-176">Aby wyświetlić szczegóły dotyczące określonego węzła w stacji, kliknij wiersz na liście.</span><span class="sxs-lookup"><span data-stu-id="ab27a-176">To view details on a specific node in the station, click the row in the list.</span></span> <span data-ttu-id="ab27a-177">Ta akcja uruchamia panel kontekstowy z wizualizacjami usługi Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="ab27a-177">This action launches the context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="ab27a-178">Kliknięcie takiego wykresu umożliwia przeprowadzenie dalszej analizy w środowisku eksploratora usługi Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="ab27a-178">Click these graphs to do further analysis in the Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="ab27a-179">Wyświetlanie mapy</span><span class="sxs-lookup"><span data-stu-id="ab27a-179">View map</span></span>

<span data-ttu-id="ab27a-180">Jeśli Twoja subskrypcja ma dostęp do interfejsu API usługi Mapy Bing, na mapie *Fabryki* są wyświetlane lokalizacje geograficzne i status wszystkich fabryk w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-180">If your subscription has access to the Bing Maps API, the *Factories* map shows you the geographical location and status of all the factories in the solution.</span></span> <span data-ttu-id="ab27a-181">Aby przejść do szczegółów lokalizacji, kliknij lokalizacje wyświetlane na mapie.</span><span class="sxs-lookup"><span data-stu-id="ab27a-181">To drill into the location details, click the locations displayed on the map.</span></span>

![Mapa we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="ab27a-183">Wyświetlanie alertów</span><span class="sxs-lookup"><span data-stu-id="ab27a-183">View alerts</span></span>

<span data-ttu-id="ab27a-184">Na panelu **Alert** są wyświetlane alerty wygenerowane z powodu wystąpienia wartości zgłoszonej lub wartości obliczonej ogólnej wydajności sprzętu bądź kluczowego wskaźnika wydajności, która przekroczyła skonfigurowaną wartość progową.</span><span class="sxs-lookup"><span data-stu-id="ab27a-184">The **Alert** panel shows you alerts generated due to a reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="ab27a-185">Na tym panelu pojawiają się alerty dotyczące każdego poziomu hierarchii: od poziomu stacji do widoku globalnego.</span><span class="sxs-lookup"><span data-stu-id="ab27a-185">This panel displays alerts at each level of the hierarchy, from the station level view to the global view.</span></span> <span data-ttu-id="ab27a-186">Alerty zawierają opis alertu, datę, godzinę, lokalizację i liczbę wystąpień.</span><span class="sxs-lookup"><span data-stu-id="ab27a-186">The alerts contain a description of the alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="ab27a-187">Korzystając z danych usługi Time Series Insights, można uzyskać wgląd w dane, które spowodowały wystąpienie alertu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-187">You can gain insights in to the data that caused the alert using the Time Series Insights data.</span></span> <span data-ttu-id="ab27a-188">Dane usługi Time Series Insights są wizualizowane w alertach, gdy ma to uzasadnienie.</span><span class="sxs-lookup"><span data-stu-id="ab27a-188">The Time Series Insights data is visualized in the alerts where applicable.</span></span> <span data-ttu-id="ab27a-189">Jeśli jesteś administratorem, możesz wykonywać domyślne akcje na alertach, takie jak:</span><span class="sxs-lookup"><span data-stu-id="ab27a-189">If you are an Administrator, you can take default actions on the alerts such as:</span></span>

* <span data-ttu-id="ab27a-190">Zamknięcie alertu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-190">Close the alert.</span></span>
* <span data-ttu-id="ab27a-191">Potwierdzenie alertu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-191">Acknowledge the alert.</span></span>

<span data-ttu-id="ab27a-192">Opcjonalnie możesz wykonać bardziej złożone akcje.</span><span class="sxs-lookup"><span data-stu-id="ab27a-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="ab27a-193">Na przykład dla węzła OPC UA Ciśnienie zestawu można wykonać następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="ab27a-193">For example, for the Pressure OPC UA Node of the Assembly you could:</span></span>

* <span data-ttu-id="ab27a-194">Wyświetlenie dodatkowych informacji na stronie internetowej w nowym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="ab27a-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="ab27a-195">Wyeliminowanie przyczyny alertu za pomocą wywołania metody OPC UA na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-195">Mitigate the cause of the alert by calling an OPC UA method on the device.</span></span>
* <span data-ttu-id="ab27a-196">Pominięcie dostępności domyślnych akcji.</span><span class="sxs-lookup"><span data-stu-id="ab27a-196">Suppress the availability of the default actions.</span></span>

    ![Alerty we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="ab27a-198">Te alerty są generowane na podstawie reguł określonych w pliku konfiguracyjnym we wstępnie skonfigurowanym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-198">These alerts are generated by rules that are specified in a configuration file in the preconfigured solution.</span></span> <span data-ttu-id="ab27a-199">Te reguły mogą generować alerty, gdy wartości ogólnej wydajności sprzętu lub kluczowego wskaźnika wydajności bądź wartości węzła OPC UA przekraczają skonfigurowany dla nich próg.</span><span class="sxs-lookup"><span data-stu-id="ab27a-199">These rules can generate alerts when the OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="ab27a-200">Na **panelu Alerty** są wyświetlane alerty wygenerowane w tym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-200">The **Alerts panel** shows the alerts generated in this solution.</span></span>

2. <span data-ttu-id="ab27a-201">Aby wyświetlić szczegóły alertu, kliknij jego nazwę na panelu alertów.</span><span class="sxs-lookup"><span data-stu-id="ab27a-201">To view the details of an alert, click the alert in the alerts panel.</span></span>

3. <span data-ttu-id="ab27a-202">W celu przeprowadzenia dalszej analizy danych alertu kliknij wykres na panelu alertu, aby otworzyć środowiska eksploratora usługi Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="ab27a-202">To further analyze the alert data, click the graph in the alert panel to open the Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="ab27a-203">Aby rozwiązać alert, na panelu alertów jest dostępnych kilka akcji.</span><span class="sxs-lookup"><span data-stu-id="ab27a-203">To address the alert, several actions are available in the alert panel.</span></span> <span data-ttu-id="ab27a-204">Wybierz odpowiednią opcję i kliknij przycisk polecenia wykonania akcji.</span><span class="sxs-lookup"><span data-stu-id="ab27a-204">Choose the appropriate option for you and click the execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="ab27a-205">Wyświetlanie ogólnej wydajności sprzętu</span><span class="sxs-lookup"><span data-stu-id="ab27a-205">View overall equipment efficiency</span></span>

<span data-ttu-id="ab27a-206">Ogólna wydajność sprzętu (OEE) pozwala ocenić wydajność procesu produkcyjnego przy użyciu kluczowych parametrów operacyjnych powiązanych z produkcją.</span><span class="sxs-lookup"><span data-stu-id="ab27a-206">OEE rates the efficiency of the manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="ab27a-207">Ogólna wydajność sprzętu to standardowy pomiar branżowy obliczany przez pomnożenie współczynników dostępności, wydajności i jakości: OEE = dostępność x wydajność x jakość.</span><span class="sxs-lookup"><span data-stu-id="ab27a-207">OEE is an industry standard measure calculated by multiplying the availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![Ogólna wydajność sprzętu we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-oee]

1. <span data-ttu-id="ab27a-209">Aby wyświetlić ogólną wydajność sprzętu na dowolnym poziomie hierarchii, przejdź do wymaganego widoku.</span><span class="sxs-lookup"><span data-stu-id="ab27a-209">To view OEE for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="ab27a-210">Ogólna wydajność sprzętu dla tego widoku będzie wyświetlana na panelu razem ze wszystkimi elementami składowymi procentowej wartości OEE.</span><span class="sxs-lookup"><span data-stu-id="ab27a-210">The OEE for that view displays in the panel along with each of the elements that make up the OEE percentage.</span></span>

2. <span data-ttu-id="ab27a-211">W celu dalszej analizy ogólnej wydajności sprzętu na dowolnym poziomie w danych hierarchii, kliknij pozycję dotyczącą wartości procentowej dla ogólnej wydajności sprzętu, dostępności, wydajności lub jakości.</span><span class="sxs-lookup"><span data-stu-id="ab27a-211">To further analyze the OEE for any level in the hierarchy data, click either the OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="ab27a-212">Zostanie wyświetlony panel kontekstowy zawierający wizualizacje usługi Time Series Insights z danymi z ostatniej godziny, ostatnich 24 godzin i ostatnich 7 dni.</span><span class="sxs-lookup"><span data-stu-id="ab27a-212">A context panel appears with Time Series Insights powered visualizations that shows data from the last hour, last 24 hours, and last 7 days.</span></span>

    ![Wizualizacje usługi TSI we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-tsi-visualization]

3. <span data-ttu-id="ab27a-214">Aby dalej analizować dane alertów, kliknij wykres na panelu alertu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-214">To further analyze the alert data, click the graph in the alert panel.</span></span> <span data-ttu-id="ab27a-215">Spowoduje to otwarcie środowiska eksploratora usługi Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="ab27a-215">This action opens the Time Series Insights explorer environment.</span></span>

    ![Eksplorator usługi TSI we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="ab27a-217">Wyświetlanie kluczowych wskaźników wydajności</span><span class="sxs-lookup"><span data-stu-id="ab27a-217">View Key Performance Indicators</span></span>

<span data-ttu-id="ab27a-218">Rozwiązanie zapewnia dwa kluczowe wskaźniki wydajności: *liczba jednostek na godzinę* i *zużycie energii w kWh*.</span><span class="sxs-lookup"><span data-stu-id="ab27a-218">The solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![Kluczowy wskaźnik wydajności we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-kpi]

1. <span data-ttu-id="ab27a-220">Aby wyświetlić liczbę jednostek na godzinę lub ilość zużytej energii na dowolnym poziomie hierarchii, przejdź do wymaganego widoku.</span><span class="sxs-lookup"><span data-stu-id="ab27a-220">To view units per hour or energy used for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="ab27a-221">Liczba jednostek na godzinę i ilość zużytej energii zostaną wyświetlone na panelu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-221">The units per hour and energy used display in the panel.</span></span>

2. <span data-ttu-id="ab27a-222">Aby przeprowadzić dalszą analizę liczby jednostek na godzinę lub ilości zużytej energii na dowolnym poziomie w ramach hierarchii, kliknij miernik na panelu **Kluczowe wskaźniki wydajności**.</span><span class="sxs-lookup"><span data-stu-id="ab27a-222">To analyze units per hour or energy used for any level in the hierarchy further, click the gauge in the **Key Performance Indicators** panel.</span></span> <span data-ttu-id="ab27a-223">Zostanie wyświetlony panel kontekstowy zawierający wizualizacje usługi Time Series Insights umożliwiające przeglądanie danych z ostatniej godziny, ostatnich 24 godzin i ostatnich 7 dni.</span><span class="sxs-lookup"><span data-stu-id="ab27a-223">A context panel appears with Time Series Insights powered visualizations enabling you to view data from the last hour, the last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="ab27a-224">Przegląd scenariusza</span><span class="sxs-lookup"><span data-stu-id="ab27a-224">Scenario review</span></span>

<span data-ttu-id="ab27a-225">W tym scenariuszu na pulpicie nawigacyjnym były monitorowane wartości ogólnej wydajności sprzętu i kluczowych wskaźników wydajności fabryk.</span><span class="sxs-lookup"><span data-stu-id="ab27a-225">In this scenario, you monitored your factories OEE and KPIs values, in the dashboard.</span></span> <span data-ttu-id="ab27a-226">Następnie użyto usługi Time Series Insights w celu udostępnienia większej ilości informacji ułatwiających dalsze badanie danych telemetrycznych ogólnej wydajności sprzętu i kluczowych wskaźników wydajności pomagających w wykrywaniu nieprawidłowości.</span><span class="sxs-lookup"><span data-stu-id="ab27a-226">You then used Time Series Insights to provide more information to help drill further into the telemetry data for OEE and KPIs to help with detecting anomalies.</span></span> <span data-ttu-id="ab27a-227">Użyto również panelu alertów do wyświetlenia problemów dotyczących fabryk i skorzystano z dostępnych akcji w celu rozwiązania alertu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-227">You also used the alert panel to view issues with your factories and you used the actions available to you to resolve the alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="ab27a-228">Pozostałe funkcje</span><span class="sxs-lookup"><span data-stu-id="ab27a-228">Other features</span></span>

<span data-ttu-id="ab27a-229">W poniższych sekcjach opisano niektóre dodatkowe funkcje rozwiązania połączonej fabryki, które nie zostały opisane w poprzednim scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-229">The following sections describe some additional features of the connected factory solution that are not described in the previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="ab27a-230">Stosowanie filtrów</span><span class="sxs-lookup"><span data-stu-id="ab27a-230">Apply filters</span></span>

1. <span data-ttu-id="ab27a-231">Kliknij **cudzysłów ostrokątny**, aby wyświetlić listę dostępnych filtrów na panelu lokalizacji fabryk lub panelu alertów.</span><span class="sxs-lookup"><span data-stu-id="ab27a-231">Click the **chevron** to display a list of available filters in either the factory locations panel or the alerts panel.</span></span>

2. <span data-ttu-id="ab27a-232">Poniżej przedstawiono panel filtrów.</span><span class="sxs-lookup"><span data-stu-id="ab27a-232">The filters panel is displayed for you.</span></span> 

    ![Filtry we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-alert-filter]

3. <span data-ttu-id="ab27a-234">Wybierz wymagany filtr.</span><span class="sxs-lookup"><span data-stu-id="ab27a-234">Choose the filter that you require.</span></span> <span data-ttu-id="ab27a-235">Możesz również wpisać dowolny tekst w polach filtrów.</span><span class="sxs-lookup"><span data-stu-id="ab27a-235">It is also possible to type free text into the filter fields.</span></span>

4. <span data-ttu-id="ab27a-236">Wybrany filtr zostanie zastosowany.</span><span class="sxs-lookup"><span data-stu-id="ab27a-236">The filter is then applied for you.</span></span> <span data-ttu-id="ab27a-237">Stan filtru jest również wyświetlany na pulpicie nawigacyjnym za pomocą lejka w tabelach fabryk i alertów.</span><span class="sxs-lookup"><span data-stu-id="ab27a-237">The filter state is also shown in the dashboard via a funnel that displays in the factories and alerts tables.</span></span>

    ![Filtry we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="ab27a-239">Aktywny filtr nie ma wpływu na wyświetlanie wartości ogólnej wydajności sprzętu i kluczowych wskaźników wydajności. Filtrowana jest tylko zawartość listy.</span><span class="sxs-lookup"><span data-stu-id="ab27a-239">An active filter does not affect the displayed OEE and KPI values, it only filters the list contents.</span></span>

5. <span data-ttu-id="ab27a-240">Aby usunąć filtr, kliknij ikonę lejka, a następnie kliknij filtr na panelu kontekstowym filtru.</span><span class="sxs-lookup"><span data-stu-id="ab27a-240">To clear a filter, click the funnel and click filter in the filter context panel.</span></span> <span data-ttu-id="ab27a-241">W tabelach fabryk i alertów zostanie wyświetlony tekst **Wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="ab27a-241">The text **All** is displayed in the factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="ab27a-242">Przeglądanie serwera OPC UA</span><span class="sxs-lookup"><span data-stu-id="ab27a-242">Browse an OPC UA server</span></span>

<span data-ttu-id="ab27a-243">Podczas wdrażania wstępnie skonfigurowanego rozwiązania następuje automatyczna aprowizacja symulowanych serwerów OPC UA, które można przeglądać za pomocą przeglądarki rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ab27a-243">When you deploy the preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via the solution browser.</span></span> <span data-ttu-id="ab27a-244">Są to *symulowane serwery OPC UA*.</span><span class="sxs-lookup"><span data-stu-id="ab27a-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="ab27a-245">Symulowane serwery ułatwiają eksperymentowanie ze wstępnie skonfigurowanym rozwiązaniem bez konieczności wdrażania prawdziwych serwerów fizycznych.</span><span class="sxs-lookup"><span data-stu-id="ab27a-245">Simulated servers make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical servers.</span></span> <span data-ttu-id="ab27a-246">Jeśli chcesz połączyć prawdziwy serwer OPC UA z rozwiązaniem, zobacz samouczek [Connect your OPC UA device to the connected factory preconfigured solution][lnk-connect-cf] (Łączenie urządzenia OPC UA ze wstępnie skonfigurowanym rozwiązaniem połączonej fabryki).</span><span class="sxs-lookup"><span data-stu-id="ab27a-246">If you do want to connect a real OPC UA server to the solution, see the [Connect your OPC UA device to the connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="ab27a-247">Kliknij **ikonę fabryki** na pasku nawigacyjnym pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ab27a-247">Click the **factory icon** in the dashboard navigation bar.</span></span>

    ![Przeglądarka serwerów we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-server-browser]

2. <span data-ttu-id="ab27a-249">Wybierz jeden z serwerów ze wstępnie skonfigurowanej listy.</span><span class="sxs-lookup"><span data-stu-id="ab27a-249">Choose one of the servers from the preconfigured list.</span></span> <span data-ttu-id="ab27a-250">Ta lista zawiera serwery wdrożone we wstępnie skonfigurowanym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-250">This list shows the servers that are deployed for you in the preconfigured solution.</span></span>

    ![Wybieranie serwerów we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-server-choice]

3. <span data-ttu-id="ab27a-252">Kliknij przycisk **Połącz**. Zostanie wyświetlone okno dialogowe zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ab27a-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="ab27a-253">W tej symulacji można bezpiecznie kliknąć pozycję **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="ab27a-253">For the simulation, it is safe to click **Proceed**</span></span>

4. <span data-ttu-id="ab27a-254">Aby rozwinąć dowolny węzeł w drzewie serwerów, kliknij go.</span><span class="sxs-lookup"><span data-stu-id="ab27a-254">To expand any of the nodes in the server tree, click it.</span></span> <span data-ttu-id="ab27a-255">Węzły, które publikują dane telemetryczne, mają obok swoich nazw znaczniki.</span><span class="sxs-lookup"><span data-stu-id="ab27a-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Drzewo serwerów we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-server-tree]

5. <span data-ttu-id="ab27a-257">Kliknij element prawym przyciskiem myszy, aby odczytać, zapisać, opublikować lub wywołać ten węzeł.</span><span class="sxs-lookup"><span data-stu-id="ab27a-257">Right-click an item to read, write, publish, or call that node.</span></span> <span data-ttu-id="ab27a-258">Dostępne akcje zależą od uprawnień posiadanych przez użytkownika i atrybutów węzła.</span><span class="sxs-lookup"><span data-stu-id="ab27a-258">The actions available to you depend on your permissions and the attributes of the node.</span></span> <span data-ttu-id="ab27a-259">Wybranie opcji odczytu powoduje wyświetlenie panelu kontekstowego z wartością konkretnego węzła.</span><span class="sxs-lookup"><span data-stu-id="ab27a-259">The read option to displays a context panel showing the value of the specific node.</span></span> <span data-ttu-id="ab27a-260">Wybranie opcji zapisu powoduje wyświetlenie panelu kontekstowego, w którym można wprowadzić nową wartość.</span><span class="sxs-lookup"><span data-stu-id="ab27a-260">The write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="ab27a-261">Wybranie opcji wywołania powoduje wyświetlenie węzła i umożliwia wprowadzenie parametrów wywołania.</span><span class="sxs-lookup"><span data-stu-id="ab27a-261">The call option displays a node where you can enter the parameters for the call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="ab27a-262">Publikowanie węzła</span><span class="sxs-lookup"><span data-stu-id="ab27a-262">Publish a node</span></span>

<span data-ttu-id="ab27a-263">Podczas przeglądania *symulowanego serwera OPC UA* można również opublikować nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="ab27a-263">When you browse a *simulated OPC UA server*, you can also choose to publish new nodes.</span></span> <span data-ttu-id="ab27a-264">W rozwiązaniu można przeanalizować dane telemetryczne z tych węzłów.</span><span class="sxs-lookup"><span data-stu-id="ab27a-264">You can analyze the telemetry from these nodes in the solution.</span></span> <span data-ttu-id="ab27a-265">Te *symulowane serwery OPC UA* ułatwiają eksperymentowanie ze wstępnie skonfigurowanym rozwiązaniem bez konieczności wdrażania prawdziwych urządzeń fizycznych.</span><span class="sxs-lookup"><span data-stu-id="ab27a-265">These *simulated OPC UA servers* make it easy to experiment with the preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="ab27a-266">W drzewie przeglądarki serwerów OPC UA przejdź do węzła, który chcesz opublikować.</span><span class="sxs-lookup"><span data-stu-id="ab27a-266">Browse to a node in the OPC UA server browser tree that you wish to publish.</span></span>

2. <span data-ttu-id="ab27a-267">Kliknij węzeł prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="ab27a-267">Right-click the node.</span></span>

3. <span data-ttu-id="ab27a-268">Wybierz polecenie **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="ab27a-268">Choose **Publish**.</span></span>

    ![Publikowanie węzła przez połączoną fabrykę][cf-img-publish-node]

4. <span data-ttu-id="ab27a-270">Wyświetlony panel kontekstowy informuje, że publikowanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="ab27a-270">A context panel appears which tells you that the publish has succeeded.</span></span> <span data-ttu-id="ab27a-271">Węzeł pojawi się w widoku poziomu stacji z umieszczonym obok znacznikiem.</span><span class="sxs-lookup"><span data-stu-id="ab27a-271">The node appears in the station level view with a check mark beside it.</span></span>

    ![Pomyślne publikowanie we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="ab27a-273">Sterowanie i kontrola</span><span class="sxs-lookup"><span data-stu-id="ab27a-273">Command and control</span></span>

<span data-ttu-id="ab27a-274">Połączona fabryka umożliwia sterowanie urządzeniami przemysłowymi i kontrolowanie ich bezpośrednio z chmury.</span><span class="sxs-lookup"><span data-stu-id="ab27a-274">The connected factory allows you command and control your industry devices directly from the cloud.</span></span> <span data-ttu-id="ab27a-275">Tej funkcji można używać do odpowiadania na alerty generowane przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="ab27a-275">You can use this feature to respond to alerts generated by the device.</span></span> <span data-ttu-id="ab27a-276">Można na przykład wysłać polecenie do urządzenia z chmury.</span><span class="sxs-lookup"><span data-stu-id="ab27a-276">For example, you could send a command to the device from the cloud.</span></span> <span data-ttu-id="ab27a-277">Dostępne polecenia można znaleźć w węźle **StationCommands** w drzewie przeglądarki serwerów OPC UA.</span><span class="sxs-lookup"><span data-stu-id="ab27a-277">You can find the available commands in the **StationCommands** node in the OPC UA servers browser tree.</span></span> <span data-ttu-id="ab27a-278">W tym scenariuszu otwierasz zawór bezpieczeństwa na stanowisku montażowym linii produkcyjnej w Monachium.</span><span class="sxs-lookup"><span data-stu-id="ab27a-278">In this scenario, you open a pressure release valve on the assembly station of a production line in Munich.</span></span> <span data-ttu-id="ab27a-279">Aby móc skorzystać z funkcji sterowania i kontroli, musisz mieć rolę **administratora** we wdrożeniu wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ab27a-279">To use the command and control functionality, you must be in the **Administrator** role for the preconfigured solution deployment.</span></span>

1. <span data-ttu-id="ab27a-280">W drzewie przeglądarki serwerów OPC UA przejdź do węzła **StationCommands**.</span><span class="sxs-lookup"><span data-stu-id="ab27a-280">Browse to the **StationCommands** node in the OPC UA server browser tree.</span></span>

2. <span data-ttu-id="ab27a-281">Wybierz polecenie, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="ab27a-281">Choose the command that you wish use.</span></span>

3. <span data-ttu-id="ab27a-282">Kliknij węzeł prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="ab27a-282">Right-click the node.</span></span>

4. <span data-ttu-id="ab27a-283">Wybierz polecenie **Wywołaj**.</span><span class="sxs-lookup"><span data-stu-id="ab27a-283">Choose **Call**.</span></span>

    ![Polecenie wywoływania we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-call-command]

5. <span data-ttu-id="ab27a-285">Zostanie wyświetlony panel kontekstowy z informacjami o metodzie, która ma zostać wywołana, i szczegółami parametru, jeśli ma to zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="ab27a-285">A context panel appears informing you which method you are about to call and any parameter details is applicable.</span></span>

6. <span data-ttu-id="ab27a-286">Wybierz polecenie **Wywołaj**.</span><span class="sxs-lookup"><span data-stu-id="ab27a-286">Choose **Call**.</span></span>

    ![Kontekst wywołania we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-call-context]

7. <span data-ttu-id="ab27a-288">Panel kontekstowy zostanie zaktualizowany o informacje o powodzeniu wywołania metody.</span><span class="sxs-lookup"><span data-stu-id="ab27a-288">The context panel is updated to inform you that the method call succeeded.</span></span> <span data-ttu-id="ab27a-289">Powodzenie wywołania metody można sprawdzić, odczytując zaktualizowaną w wyniku wywołania wartość węzła ciśnienia.</span><span class="sxs-lookup"><span data-stu-id="ab27a-289">You can verify the call succeeded by reading the value of the pressure node that updated as a result of the call.</span></span>

    ![Powodzenie wywołania we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-call-success]


## <a name="behind-the-scenes"></a><span data-ttu-id="ab27a-291">Za kulisami</span><span class="sxs-lookup"><span data-stu-id="ab27a-291">Behind the scenes</span></span>

<span data-ttu-id="ab27a-292">Podczas wdrażania wstępnie skonfigurowanego rozwiązania jest tworzonych wiele zasobów w ramach wybranej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab27a-292">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="ab27a-293">Można je wyświetlić w witrynie Azure [Portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="ab27a-293">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="ab27a-294">W procesie wdrażania jest tworzona **grupa zasobów** o nazwie odpowiadającej nazwie wstępnie skonfigurowanego rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="ab27a-294">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Wstępnie skonfigurowane rozwiązanie w portalu Azure][img-cf-portal]

<span data-ttu-id="ab27a-296">Aby wyświetlić ustawienia danego zasobu, wybierz go z listy w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="ab27a-296">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="ab27a-297">Można również wyświetlić kod źródłowy wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ab27a-297">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="ab27a-298">Kod źródłowy wstępnie skonfigurowanego rozwiązania połączonej fabryki znajduje się w repozytorium GitHub [azure-iot-connected-factory][lnk-cfgithub]:</span><span class="sxs-lookup"><span data-stu-id="ab27a-298">The connected factory preconfigured solution source code is in the [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="ab27a-299">Gdy wszystko będzie gotowe, możesz usunąć wstępnie skonfigurowane rozwiązanie z subskrypcji platformy Azure w witrynie [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="ab27a-299">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="ab27a-300">Ta witryna umożliwia łatwe usunięcie wszystkich zasobów, które zostały aprowizowane po utworzeniu wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ab27a-300">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="ab27a-301">Aby mieć pewność, że zostaną usunięte wszystkie elementy powiązane ze wstępnie skonfigurowanym rozwiązaniem, usuń rozwiązanie w witrynie [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="ab27a-301">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="ab27a-302">Nie należy usuwać grupy zasobów w portalu.</span><span class="sxs-lookup"><span data-stu-id="ab27a-302">Do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab27a-303">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab27a-303">Next Steps</span></span>

<span data-ttu-id="ab27a-304">Teraz, kiedy zostało wdrożone wstępnie skonfigurowane rozwiązanie, które działa, możesz kontynuować poznawanie Pakietu IoT, czytając następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="ab27a-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="ab27a-305">[Przewodnik po wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="ab27a-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="ab27a-306">[Łączenie urządzenia ze wstępnie skonfigurowanym rozwiązaniem połączonej fabryki][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="ab27a-306">[Connect your device to the Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="ab27a-307">[Uprawnienia w witrynie azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="ab27a-307">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md