---
title: "aaaAzure pakiet IoT połączone fabryki omówienie | Dokumentacja firmy Microsoft"
description: "Opis hello pakiet IoT Azure połączone fabryki wstępnie skonfigurowane rozwiązanie."
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
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a><span data-ttu-id="59909-103">Rozpoczynanie pracy z hello połączone fabryki wstępnie skonfigurowane rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="59909-103">Get started with hello connected factory preconfigured solution</span></span>

<span data-ttu-id="59909-104">Pakiet Azure IoT [wstępnie rozwiązań] [ lnk-preconfigured-solutions] łączenie wielu Azure IoT usług toodeliver end-to-end rozwiązania, które implementuje typowych scenariuszy biznesowych IoT.</span><span class="sxs-lookup"><span data-stu-id="59909-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="59909-105">Witaj *połączonych fabryki* wstępnie skonfigurowane rozwiązanie łączy monitorów tooand przemysłowych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="59909-105">hello *connected factory* preconfigured solution connects tooand monitors your industrial devices.</span></span> <span data-ttu-id="59909-106">Możesz użyć hello rozwiązania tooanalyze hello strumienia danych z urządzenia i wydajności operacyjnej toodrive i rentowność.</span><span class="sxs-lookup"><span data-stu-id="59909-106">You can use hello solution tooanalyze hello stream of data from your devices and toodrive operational productivity and profitability.</span></span>

<span data-ttu-id="59909-107">W tym samouczku przedstawiono sposób tooprovision hello połączenia fabryki wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="59909-107">This tutorial shows you how tooprovision hello connected factory preconfigured solution.</span></span> <span data-ttu-id="59909-108">On również przeprowadzi Cię przez hello podstawowych funkcji hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="59909-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="59909-109">Dostępne wiele z tych funkcji z rozwiązania hello *pulpitu nawigacyjnego* która wdraża jako część rozwiązania hello wstępnie skonfigurowane:</span><span class="sxs-lookup"><span data-stu-id="59909-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania połączonej fabryki][img-cf-home]

<span data-ttu-id="59909-111">toocomplete tego samouczka należy aktywną subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59909-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="59909-112">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="59909-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="59909-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="59909-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-hello-solution"></a><span data-ttu-id="59909-114">Zainicjuj obsługę hello rozwiązania</span><span class="sxs-lookup"><span data-stu-id="59909-114">Provision hello solution</span></span>

1. <span data-ttu-id="59909-115">Zaloguj się przy użyciu poświadczeń konta Azure tooazureiotsuite.com, a następnie kliknij przycisk "**+**" toocreate rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="59909-115">Log on tooazureiotsuite.com using your Azure account credentials, and click "**+**" toocreate a solution.</span></span>
2. <span data-ttu-id="59909-116">Kliknij przycisk **wybierz** na powitania **połączonych fabryki** kafelka.</span><span class="sxs-lookup"><span data-stu-id="59909-116">Click **Select** on hello **Connected factory** tile.</span></span>
3. <span data-ttu-id="59909-117">W polu **Nazwa rozwiązania** wprowadź nazwę wstępnie skonfigurowanego rozwiązania dla połączonej fabryki.</span><span class="sxs-lookup"><span data-stu-id="59909-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="59909-118">Wybierz hello **subskrypcji** i **Region** toouse tooprovision hello rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="59909-118">Select hello **Subscription** and **Region** you want toouse tooprovision hello solution.</span></span>
5. <span data-ttu-id="59909-119">Kliknij przycisk **Utwórz rozwiązanie** hello toobegin w procesie inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="59909-119">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="59909-120">Ten proces zwykle trwa kilka minut toorun.</span><span class="sxs-lookup"><span data-stu-id="59909-120">This process typically takes several minutes toorun.</span></span>

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="59909-121">Podczas oczekiwania na powitania inicjowania obsługi administracyjnej toocomplete procesu</span><span class="sxs-lookup"><span data-stu-id="59909-121">While you wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="59909-122">Kliknij Kafelek hello rozwiązania z **inicjowania obsługi administracyjnej** stanu.</span><span class="sxs-lookup"><span data-stu-id="59909-122">Click hello tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="59909-123">Powiadomienie hello **inicjowania obsługi administracyjnej stanów** podczas wdrażania usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59909-123">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="59909-124">Po ukończeniu inicjowania obsługi administracyjnej hello zmiany stanu zbyt**gotowe**.</span><span class="sxs-lookup"><span data-stu-id="59909-124">Once provisioning completes, hello status changes too**Ready**.</span></span>
4. <span data-ttu-id="59909-125">Kliknij przycisk hello kafelka toosee hello szczegóły rozwiązania w okienku po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="59909-125">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="59909-126">Jeśli wystąpią problemy dotyczące wdrażania rozwiązania hello wstępnie skonfigurowane, przejrzyj [uprawnienia w witrynie azureiotsuite.com hello] [ lnk-permissions] i hello [połączone fabryki — często zadawane pytania](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="59909-126">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="59909-127">Jeśli hello problemy będą się powtarzać, Utwórz biletu usługi na powitania [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="59909-127">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="59909-128">Czy istnieją szczegółowe informacje można oczekiwać toosee, które nie są wyświetlane dla rozwiązania?</span><span class="sxs-lookup"><span data-stu-id="59909-128">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="59909-129">Prześlij nam swoje propozycje dotyczące funkcji, korzystając ze strony [User Voice](https://feedback.azure.com/forums/321918-azure-iot) (Opinie użytkowników).</span><span class="sxs-lookup"><span data-stu-id="59909-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="59909-130">Omówienie scenariusza</span><span class="sxs-lookup"><span data-stu-id="59909-130">Scenario overview</span></span>

<span data-ttu-id="59909-131">Podczas wdrażania hello połączone fabryki wstępnie skonfigurowane rozwiązanie, jest on wstępnie wypełnione zasobów umożliwiających toostep za pośrednictwem typowy scenariusz przemysłowych.</span><span class="sxs-lookup"><span data-stu-id="59909-131">When you deploy hello connected factory preconfigured solution, it is prepopulated with resources that enable you toostep through a common industrial scenario.</span></span> <span data-ttu-id="59909-132">W tym scenariuszu kilka fabryki połączony raport rozwiązania toohello hello danych wartości wymagane toocompute ogólnej wydajności sprzętu (OEE) oraz kluczowych wskaźników wydajności (KPI).</span><span class="sxs-lookup"><span data-stu-id="59909-132">In this scenario, several factories connected toohello solution report hello data values required toocompute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="59909-133">Hello następnych sekcjach opisano sposób do:</span><span class="sxs-lookup"><span data-stu-id="59909-133">hello following sections show you how to:</span></span>

* <span data-ttu-id="59909-134">Monitorowanie fabryki, linii produkcyjnych, ogólnej wydajności stacji i wartości kluczowych wskaźników wydajności.</span><span class="sxs-lookup"><span data-stu-id="59909-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="59909-135">Analizowanie danych telemetrycznych hello wygenerowane z tych urządzeń przy użyciu usługi Azure czas serii Insights</span><span class="sxs-lookup"><span data-stu-id="59909-135">Analyze hello telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="59909-136">Działania dotyczące problemów toofix alertów</span><span class="sxs-lookup"><span data-stu-id="59909-136">Act on alerts toofix issues</span></span>

<span data-ttu-id="59909-137">Kluczowy element w tym scenariuszu jest, że te akcje można wykonać zdalnie z poziomu pulpitu nawigacyjnego hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="59909-137">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="59909-138">Nie trzeba urządzeń toohello fizyczny dostęp.</span><span class="sxs-lookup"><span data-stu-id="59909-138">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="59909-139">Pulpit nawigacyjny rozwiązania hello widoku</span><span class="sxs-lookup"><span data-stu-id="59909-139">View hello solution dashboard</span></span>

<span data-ttu-id="59909-140">pulpit nawigacyjny rozwiązania Hello umożliwia toomanage hello wdrożyć rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="59909-140">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="59909-141">Jest to hierarchiczna reprezentacja globalnej konfiguracji fabryki.</span><span class="sxs-lookup"><span data-stu-id="59909-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="59909-142">Można na przykład wyświetlić ogólną wydajność sprzętu oraz kluczowe wskaźniki wydajności, opublikować nowe węzły na potrzeby telemetrii i reagować na alerty.</span><span class="sxs-lookup"><span data-stu-id="59909-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="59909-143">Po ukończeniu inicjowania obsługi administracyjnej hello i wskazuje hello Kafelek wstępnie skonfigurowane rozwiązanie **gotowe**, wybierz **uruchamianie** tooopen portalem rozwiązania połączonych fabryki na nowej karcie.</span><span class="sxs-lookup"><span data-stu-id="59909-143">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your connected factory solution portal in a new tab.</span></span>

    ![Uruchamianie hello wstępnie skonfigurowane rozwiązanie][img-launch-solution]

1. <span data-ttu-id="59909-145">Domyślnie hello rozwiązanie portalu pokazuje hello *pulpitu nawigacyjnego*.</span><span class="sxs-lookup"><span data-stu-id="59909-145">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="59909-146">obszary tooother toonavigate hello portalu, użyj hello menu na powitania po lewej stronie powitania strony.</span><span class="sxs-lookup"><span data-stu-id="59909-146">toonavigate tooother areas of hello portal, use hello menu on hello left-hand side of hello page.</span></span>

    ![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania połączonej fabryki][cf-img-menu]

<span data-ttu-id="59909-148">pulpit nawigacyjny Hello Wyświetla hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="59909-148">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="59909-149">A **listy fabryki** panelu, pokazujący stan hello, lokalizacji i bieżącej konfiguracji produkcji hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="59909-149">A **Factory list** panel that shows hello status, location, and current production configuration in hello solution.</span></span> <span data-ttu-id="59909-150">Przy pierwszym uruchomieniu rozwiązania hello, istnieje wiele urządzeń symulowane.</span><span class="sxs-lookup"><span data-stu-id="59909-150">When you first run hello solution, there are a number of simulated devices.</span></span> <span data-ttu-id="59909-151">Symulacja wiersza produkcyjnym Hello składa się z trzech rzeczywistych OPC UA serwerom na linii produkcyjnej symulowane zadań i udostępnianie danych.</span><span class="sxs-lookup"><span data-stu-id="59909-151">hello production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="59909-152">Aby uzyskać więcej informacji na temat OPC UA Zobacz hello [połączone fabryki — często zadawane pytania](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="59909-152">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="59909-153">A **mapy** czy lokalizacji hello Wyświetla wszystkie urządzenia podłączone toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="59909-153">A **map** that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="59909-154">rozwiązanie Hello można użyć informacji tooplot interfejsu API map Bing hello na mapie hello.</span><span class="sxs-lookup"><span data-stu-id="59909-154">hello solution can use hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="59909-155">Jeśli subskrypcja obejmuje interfejs API usługi Mapy Bing w wersji Enterprise, ta funkcja jest używana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="59909-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="59909-156">Jeśli nie, zobacz hello [— często zadawane pytania] [ lnk-faq] toolearn jak toomake hello dynamicznie mapy.</span><span class="sxs-lookup"><span data-stu-id="59909-156">If not, see hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="59909-157">Panel **Alerty**, na którym są wyświetlane alerty generowane, gdy wartość telemetrii lub ogólnej wydajności sprzętu bądź kluczowego wskaźnika wydajności przekroczy określony próg.</span><span class="sxs-lookup"><span data-stu-id="59909-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="59909-158">**Ogólnej wydajności sprzętu** panelu, które pokazuje hello OEE wartości dla całego przedsiębiorstwa hello lub hello fabryki/produkcji wiersza/stacji można jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="59909-158">An **Overall Equipment Efficiency** panel that shows hello OEE values for hello whole enterprise, or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="59909-159">Ta wartość jest agregowana poziomu hello stacji widoku toohello przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="59909-159">This value is aggregated from hello station view toohello enterprise level.</span></span> <span data-ttu-id="59909-160">Rysunek OEE Hello i jej elementów składowych można analizować dalej.</span><span class="sxs-lookup"><span data-stu-id="59909-160">hello OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="59909-161">**Kluczowe wskaźniki wydajności** panelu, który wyświetla hello liczbę jednostek wyprodukowanych i energii używane przez hello całego przedsiębiorstwa lub wiersza fabryki/produkcyjnego hello stacji można jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="59909-161">**Key Performance Indicators** panel that displays hello number of units produced and energy used by hello whole enterprise or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="59909-162">Wartości te są agregowane z poziomu stacji widoku toohello przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="59909-162">These values are aggregated from a station view toohello enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="59909-163">Wyświetlanie fabryk</span><span class="sxs-lookup"><span data-stu-id="59909-163">View factories</span></span>

<span data-ttu-id="59909-164">Witaj *fabryki* panelu pokazuje hello lokalizację geograficzną wszystkich fabryki hello w hello rozwiązania, stanu i bieżącej konfiguracji produkcji.</span><span class="sxs-lookup"><span data-stu-id="59909-164">hello *Factories* panel shows you hello geographical location of all hello factories in hello solution, their status, and current production configuration.</span></span> <span data-ttu-id="59909-165">Z listy lokalizacje hello można przejść toohello innych poziomów w hierarchii rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="59909-165">From hello locations list, you can navigate toohello other levels in hello solution hierarchy.</span></span> <span data-ttu-id="59909-166">Wiersze Hello liście hello są hiperłącza, które łącze Szczegóły hello produkcji wiersze w tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="59909-166">hello rows in hello list are hyperlinks that link details of hello production lines at that location.</span></span> <span data-ttu-id="59909-167">Następnie jest możliwe toodrill do hello szczegóły wiersza produkcyjnym i w dół widok poziomu toohello stacji.</span><span class="sxs-lookup"><span data-stu-id="59909-167">It is then possible toodrill into hello production line details and down toohello station level view.</span></span> <span data-ttu-id="59909-168">Można także zastosować dla listy toohello filtrów.</span><span class="sxs-lookup"><span data-stu-id="59909-168">You can also apply a filter toohello list.</span></span>

![Fabryki we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-factories] 

1. <span data-ttu-id="59909-170">Witaj **panelu fabryki** pokazuje hello listy fabryki dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="59909-170">hello **Factory panel** shows hello factory list for this solution.</span></span>

2. <span data-ttu-id="59909-171">Lista fabryki Hello początkowo zawiera sześć fabryki utworzone przez hello w procesie inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="59909-171">hello factory list initially shows six factories created by hello provisioning process.</span></span> <span data-ttu-id="59909-172">Można dodać dodatkowych urządzeń fizycznych i symulowane toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="59909-172">You can add additional simulated and physical devices toohello solution.</span></span>

3. <span data-ttu-id="59909-173">Szczegóły hello tooview fabryki, kliknij wiersz hello hello fabryki liście.</span><span class="sxs-lookup"><span data-stu-id="59909-173">tooview hello details of a factory, click hello row in hello factory list.</span></span>

4. <span data-ttu-id="59909-174">tooview hello szczegóły wiersza produkcyjnym, kliknij wiersz hello hello na liście.</span><span class="sxs-lookup"><span data-stu-id="59909-174">tooview hello details of a production line, click hello row in hello list.</span></span>

5. <span data-ttu-id="59909-175">tooview hello opublikowane węzłów OPC UA stacji na linii produkcyjnej hello, kliknij wiersz hello liście hello.</span><span class="sxs-lookup"><span data-stu-id="59909-175">tooview hello published OPC UA nodes of a station on hello production line, click hello row in hello list.</span></span>

6. <span data-ttu-id="59909-176">Szczegóły tooview w określonym węźle w stacji hello, kliknij wiersz hello hello na liście.</span><span class="sxs-lookup"><span data-stu-id="59909-176">tooview details on a specific node in hello station, click hello row in hello list.</span></span> <span data-ttu-id="59909-177">Ta akcja spowoduje uruchomienie hello kontekstu panel z wizualizacji Insights serii czasu.</span><span class="sxs-lookup"><span data-stu-id="59909-177">This action launches hello context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="59909-178">Kliknij te wykresy toodo dalszej analizy w środowisku explorer Insights serii czasu hello.</span><span class="sxs-lookup"><span data-stu-id="59909-178">Click these graphs toodo further analysis in hello Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="59909-179">Wyświetlanie mapy</span><span class="sxs-lookup"><span data-stu-id="59909-179">View map</span></span>

<span data-ttu-id="59909-180">Jeśli subskrypcja obejmuje toohello dostępu do interfejsu API map Bing, hello *fabryki* Mapa pokazuje hello lokalizacji geograficznej i stan fabryk hello w hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="59909-180">If your subscription has access toohello Bing Maps API, hello *Factories* map shows you hello geographical location and status of all hello factories in hello solution.</span></span> <span data-ttu-id="59909-181">toodrill hello lokalizacji uzyskać szczegółowe informacje, kliknij przycisk Lokalizacje hello wyświetlone na mapie hello.</span><span class="sxs-lookup"><span data-stu-id="59909-181">toodrill into hello location details, click hello locations displayed on hello map.</span></span>

![Mapa we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="59909-183">Wyświetlanie alertów</span><span class="sxs-lookup"><span data-stu-id="59909-183">View alerts</span></span>

<span data-ttu-id="59909-184">Witaj **alertu** panelu przedstawia alerty generowane ze względu tooa podać wartość lub obliczoną wartość OEE/KPI przekroczeniu skonfigurowanego progu.</span><span class="sxs-lookup"><span data-stu-id="59909-184">hello **Alert** panel shows you alerts generated due tooa reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="59909-185">Panel ten przedstawia alerty na każdym poziomie hierarchii hello, w widoku globalnego toohello hello stacji widoku poziomu.</span><span class="sxs-lookup"><span data-stu-id="59909-185">This panel displays alerts at each level of hello hierarchy, from hello station level view toohello global view.</span></span> <span data-ttu-id="59909-186">alerty Hello zawierają opis alertu hello, datę, czas, lokalizacji i liczby wystąpień.</span><span class="sxs-lookup"><span data-stu-id="59909-186">hello alerts contain a description of hello alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="59909-187">Aby uzyskać wgląd w dane toohello, który spowodował alert hello przy użyciu hello czasu Insights serii danych.</span><span class="sxs-lookup"><span data-stu-id="59909-187">You can gain insights in toohello data that caused hello alert using hello Time Series Insights data.</span></span> <span data-ttu-id="59909-188">Hello Insights serii czas, który wizualizacji danych w hello alerty, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="59909-188">hello Time Series Insights data is visualized in hello alerts where applicable.</span></span> <span data-ttu-id="59909-189">Jeśli jesteś administratorem, można wykonać akcje domyślne hello alertów, takie jak:</span><span class="sxs-lookup"><span data-stu-id="59909-189">If you are an Administrator, you can take default actions on hello alerts such as:</span></span>

* <span data-ttu-id="59909-190">Witaj Zamknij alert.</span><span class="sxs-lookup"><span data-stu-id="59909-190">Close hello alert.</span></span>
* <span data-ttu-id="59909-191">Wiadomości powitania alertu.</span><span class="sxs-lookup"><span data-stu-id="59909-191">Acknowledge hello alert.</span></span>

<span data-ttu-id="59909-192">Opcjonalnie możesz wykonać bardziej złożone akcje.</span><span class="sxs-lookup"><span data-stu-id="59909-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="59909-193">Na przykład dla hello wykorzystania OPC UA węzła hello zestawu możesz:</span><span class="sxs-lookup"><span data-stu-id="59909-193">For example, for hello Pressure OPC UA Node of hello Assembly you could:</span></span>

* <span data-ttu-id="59909-194">Wyświetlenie dodatkowych informacji na stronie internetowej w nowym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="59909-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="59909-195">Ograniczenia hello Przyczyna alertu hello przez wywołanie metody OPC UA hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="59909-195">Mitigate hello cause of hello alert by calling an OPC UA method on hello device.</span></span>
* <span data-ttu-id="59909-196">Pomiń hello dostępność hello domyślne akcje.</span><span class="sxs-lookup"><span data-stu-id="59909-196">Suppress hello availability of hello default actions.</span></span>

    ![Alerty we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="59909-198">Te alerty są generowane przez zasady, które są określone w pliku konfiguracji w hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="59909-198">These alerts are generated by rules that are specified in a configuration file in hello preconfigured solution.</span></span> <span data-ttu-id="59909-199">Te reguły mogą generować alerty, gdy hello OEE lub wartości wskaźnika KPI lub wartości węzła UA OPC są powyżej ich skonfigurowany próg.</span><span class="sxs-lookup"><span data-stu-id="59909-199">These rules can generate alerts when hello OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="59909-200">Witaj **panelu alerty** pokazuje hello alertów wygenerowanych w tym rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="59909-200">hello **Alerts panel** shows hello alerts generated in this solution.</span></span>

2. <span data-ttu-id="59909-201">tooview hello szczegóły alertu, kliknij alert hello hello alerty panelu.</span><span class="sxs-lookup"><span data-stu-id="59909-201">tooview hello details of an alert, click hello alert in hello alerts panel.</span></span>

3. <span data-ttu-id="59909-202">toofurther analizować dane alertów hello, kliknij wykres hello hello alertu panelu tooopen hello czasu serii Insights explorer środowiska.</span><span class="sxs-lookup"><span data-stu-id="59909-202">toofurther analyze hello alert data, click hello graph in hello alert panel tooopen hello Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="59909-203">tooaddress hello alertu, kilka akcje są dostępne w panelu alertu hello.</span><span class="sxs-lookup"><span data-stu-id="59909-203">tooaddress hello alert, several actions are available in hello alert panel.</span></span> <span data-ttu-id="59909-204">Wybierz odpowiednią opcję powitania dla Ciebie, a następnie kliknij przycisk hello wykonania akcji przycisku polecenia.</span><span class="sxs-lookup"><span data-stu-id="59909-204">Choose hello appropriate option for you and click hello execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="59909-205">Wyświetlanie ogólnej wydajności sprzętu</span><span class="sxs-lookup"><span data-stu-id="59909-205">View overall equipment efficiency</span></span>

<span data-ttu-id="59909-206">Stawki OEE hello wydajności proces produkcji hello przy użyciu klucza parametry operacyjne dotyczące produkcji.</span><span class="sxs-lookup"><span data-stu-id="59909-206">OEE rates hello efficiency of hello manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="59909-207">OEE jest branżowy standard miary obliczane przez pomnożenie hello dostępności szybkości, współczynnik wydajności i jakości szybkość: OEE = dostępności x jakości wydajności x.</span><span class="sxs-lookup"><span data-stu-id="59909-207">OEE is an industry standard measure calculated by multiplying hello availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![Ogólna wydajność sprzętu we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-oee]

1. <span data-ttu-id="59909-209">tooview OEE dla dowolnego poziomu w hierarchii hello Przejdź toohello określony widok, które są wymagane.</span><span class="sxs-lookup"><span data-stu-id="59909-209">tooview OEE for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="59909-210">Witaj OEE w tym widoku są wyświetlane w panelu hello wraz z każdego z elementów hello, wchodzące w skład hello OEE procent.</span><span class="sxs-lookup"><span data-stu-id="59909-210">hello OEE for that view displays in hello panel along with each of hello elements that make up hello OEE percentage.</span></span>

2. <span data-ttu-id="59909-211">toofurther analizowanie hello OEE na dowolnym poziomie hello hierarchii danych, kliknij przycisk hello OEE, dostępności, wydajności i jakości procent.</span><span class="sxs-lookup"><span data-stu-id="59909-211">toofurther analyze hello OEE for any level in hello hierarchy data, click either hello OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="59909-212">Kontekst pojawia się okno z informacjami dotyczącymi serii czasu zasilanego wizualizacje, które zawiera dane ze hello w ciągu ostatniej godziny, ostatnich 24 godzinach i ostatnich 7 dni.</span><span class="sxs-lookup"><span data-stu-id="59909-212">A context panel appears with Time Series Insights powered visualizations that shows data from hello last hour, last 24 hours, and last 7 days.</span></span>

    ![Wizualizacje usługi TSI we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-tsi-visualization]

3. <span data-ttu-id="59909-214">toofurther analizować dane alertów hello, kliknij wykres hello w panelu alertu hello.</span><span class="sxs-lookup"><span data-stu-id="59909-214">toofurther analyze hello alert data, click hello graph in hello alert panel.</span></span> <span data-ttu-id="59909-215">Ta akcja powoduje otwarcie hello czasu serii Insights explorer środowiska.</span><span class="sxs-lookup"><span data-stu-id="59909-215">This action opens hello Time Series Insights explorer environment.</span></span>

    ![Eksplorator usługi TSI we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="59909-217">Wyświetlanie kluczowych wskaźników wydajności</span><span class="sxs-lookup"><span data-stu-id="59909-217">View Key Performance Indicators</span></span>

<span data-ttu-id="59909-218">Witaj rozwiązanie zapewnia dwie kluczowe wskaźniki wydajności, *jednostek na godzinę* i *zużycia energii w kWh*.</span><span class="sxs-lookup"><span data-stu-id="59909-218">hello solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![Kluczowy wskaźnik wydajności we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-kpi]

1. <span data-ttu-id="59909-220">jednostki tooview na godzinę lub energii użytej do dowolnego poziomu hierarchii hello Przejdź toohello określony widok, które są wymagane.</span><span class="sxs-lookup"><span data-stu-id="59909-220">tooview units per hour or energy used for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="59909-221">jednostki Hello na godzinę i energii używane wyświetlania hello panelu.</span><span class="sxs-lookup"><span data-stu-id="59909-221">hello units per hour and energy used display in hello panel.</span></span>

2. <span data-ttu-id="59909-222">jednostki tooanalyze na godzinę lub energii użytej do dowolnego poziomu hierarchii hello co więcej, kliknij przycisk miernika hello w hello **kluczowych wskaźników wydajności** panelu.</span><span class="sxs-lookup"><span data-stu-id="59909-222">tooanalyze units per hour or energy used for any level in hello hierarchy further, click hello gauge in hello **Key Performance Indicators** panel.</span></span> <span data-ttu-id="59909-223">Pojawia się, że okno kontekstu z wizualizacjami Insights serii czasu zasilane umożliwiając tooview danych z hello ostatniej godziny hello w ostatnich 24 godzinach i w ciągu ostatnich 7 dni.</span><span class="sxs-lookup"><span data-stu-id="59909-223">A context panel appears with Time Series Insights powered visualizations enabling you tooview data from hello last hour, hello last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="59909-224">Przegląd scenariusza</span><span class="sxs-lookup"><span data-stu-id="59909-224">Scenario review</span></span>

<span data-ttu-id="59909-225">W tym scenariuszu można monitorować fabryki OEE i wskaźników KPI wartości, na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="59909-225">In this scenario, you monitored your factories OEE and KPIs values, in hello dashboard.</span></span> <span data-ttu-id="59909-226">Następnie użyto tooprovide Insights serii czasu więcej informacji toohelp Przejdź dalej do hello dane telemetryczne dla toohelp OEE i wskaźników KPI z wykrywania anomalii.</span><span class="sxs-lookup"><span data-stu-id="59909-226">You then used Time Series Insights tooprovide more information toohelp drill further into hello telemetry data for OEE and KPIs toohelp with detecting anomalies.</span></span> <span data-ttu-id="59909-227">Problemy tooview alertu panelu hello również używać razem z fabryki i użyto hello Akcje dostępne tooyou tooresolve hello alertu.</span><span class="sxs-lookup"><span data-stu-id="59909-227">You also used hello alert panel tooview issues with your factories and you used hello actions available tooyou tooresolve hello alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="59909-228">Pozostałe funkcje</span><span class="sxs-lookup"><span data-stu-id="59909-228">Other features</span></span>

<span data-ttu-id="59909-229">Hello w następujących sekcjach opisano niektóre dodatkowe funkcje, które nie zostały opisane w poprzednim scenariuszu hello hello połączone fabryki rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="59909-229">hello following sections describe some additional features of hello connected factory solution that are not described in hello previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="59909-230">Stosowanie filtrów</span><span class="sxs-lookup"><span data-stu-id="59909-230">Apply filters</span></span>

1. <span data-ttu-id="59909-231">Kliknij przycisk hello **cudzysłów ostrokątny** toodisplay listę dostępnych filtrów w panelu lokalizacje fabryki hello lub hello alerty panelu.</span><span class="sxs-lookup"><span data-stu-id="59909-231">Click hello **chevron** toodisplay a list of available filters in either hello factory locations panel or hello alerts panel.</span></span>

2. <span data-ttu-id="59909-232">panel Filtry Hello jest wyświetlany dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="59909-232">hello filters panel is displayed for you.</span></span> 

    ![Filtry we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-alert-filter]

3. <span data-ttu-id="59909-234">Wybierz filtr hello, która jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="59909-234">Choose hello filter that you require.</span></span> <span data-ttu-id="59909-235">Możliwe jest również możliwe tootype niezależnych do pól filtr hello.</span><span class="sxs-lookup"><span data-stu-id="59909-235">It is also possible tootype free text into hello filter fields.</span></span>

4. <span data-ttu-id="59909-236">Filtr Hello jest następnie stosowany dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="59909-236">hello filter is then applied for you.</span></span> <span data-ttu-id="59909-237">Stan filtru Hello jest także pokazany na pulpicie nawigacyjnym hello za pośrednictwem lejka, która wyświetla w hello fabryk i alerty tabel.</span><span class="sxs-lookup"><span data-stu-id="59909-237">hello filter state is also shown in hello dashboard via a funnel that displays in hello factories and alerts tables.</span></span>

    ![Filtry we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="59909-239">Filtra aktywnego nie ma wpływu na powitania wyświetlane wartości OEE i kluczowego wskaźnika wydajności, tylko filtry hello wyświetlanie zawartości.</span><span class="sxs-lookup"><span data-stu-id="59909-239">An active filter does not affect hello displayed OEE and KPI values, it only filters hello list contents.</span></span>

5. <span data-ttu-id="59909-240">tooclear filtra, kliknij lejka hello i kliknij filtr w panelu kontekstu filtr hello.</span><span class="sxs-lookup"><span data-stu-id="59909-240">tooclear a filter, click hello funnel and click filter in hello filter context panel.</span></span> <span data-ttu-id="59909-241">Witaj tekst **wszystkie** jest wyświetlana w hello fabryk i alerty tabel.</span><span class="sxs-lookup"><span data-stu-id="59909-241">hello text **All** is displayed in hello factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="59909-242">Przeglądanie serwera OPC UA</span><span class="sxs-lookup"><span data-stu-id="59909-242">Browse an OPC UA server</span></span>

<span data-ttu-id="59909-243">Podczas wdrażania hello wstępnie skonfigurowane rozwiązanie automatycznie udostępnić symulowane serwerów OPC UA, które można przeglądać za pomocą przeglądarki rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="59909-243">When you deploy hello preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via hello solution browser.</span></span> <span data-ttu-id="59909-244">Są to *symulowane serwery OPC UA*.</span><span class="sxs-lookup"><span data-stu-id="59909-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="59909-245">Serwery symulowane ułatwiają dla Ciebie tooexperiment z rozwiązaniem hello wstępnie bez hello potrzeby toodeploy prawdziwe, fizycznych serwerów.</span><span class="sxs-lookup"><span data-stu-id="59909-245">Simulated servers make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical servers.</span></span> <span data-ttu-id="59909-246">Tooconnect rzeczywiste rozwiązania toohello OPC UA serwera, zobacz hello [łączenie rozwiązania fabryki wstępnie toohello podłączone urządzenie OPC UA] [ lnk-connect-cf] samouczka.</span><span class="sxs-lookup"><span data-stu-id="59909-246">If you do want tooconnect a real OPC UA server toohello solution, see hello [Connect your OPC UA device toohello connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="59909-247">Kliknij hello **ikona fabryki** na pasku nawigacyjnym hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="59909-247">Click hello **factory icon** in hello dashboard navigation bar.</span></span>

    ![Przeglądarka serwerów we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-server-browser]

2. <span data-ttu-id="59909-249">Wybierz jeden z serwerów hello hello wstępnie skonfigurowanej listy.</span><span class="sxs-lookup"><span data-stu-id="59909-249">Choose one of hello servers from hello preconfigured list.</span></span> <span data-ttu-id="59909-250">Ta lista zawiera serwery hello, które są wdrażane dla Ciebie w hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="59909-250">This list shows hello servers that are deployed for you in hello preconfigured solution.</span></span>

    ![Wybieranie serwerów we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-server-choice]

3. <span data-ttu-id="59909-252">Kliknij przycisk **Połącz**. Zostanie wyświetlone okno dialogowe zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="59909-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="59909-253">Na symulacyjnych hello jest bezpieczne tooclick **Kontynuuj**</span><span class="sxs-lookup"><span data-stu-id="59909-253">For hello simulation, it is safe tooclick **Proceed**</span></span>

4. <span data-ttu-id="59909-254">tooexpand dowolny z węzłów hello powitania serwera drzewa, kliknij go.</span><span class="sxs-lookup"><span data-stu-id="59909-254">tooexpand any of hello nodes in hello server tree, click it.</span></span> <span data-ttu-id="59909-255">Węzły, które publikują dane telemetryczne, mają obok swoich nazw znaczniki.</span><span class="sxs-lookup"><span data-stu-id="59909-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Drzewo serwerów we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-server-tree]

5. <span data-ttu-id="59909-257">Kliknij prawym przyciskiem myszy element tooread, zapisu, publikować lub wywołać tego węzła.</span><span class="sxs-lookup"><span data-stu-id="59909-257">Right-click an item tooread, write, publish, or call that node.</span></span> <span data-ttu-id="59909-258">tooyou dostępne akcje Hello są zależne od swoje uprawnienia i atrybuty hello hello węzła.</span><span class="sxs-lookup"><span data-stu-id="59909-258">hello actions available tooyou depend on your permissions and hello attributes of hello node.</span></span> <span data-ttu-id="59909-259">Hello odczytać toodisplays opcji panelu kontekstu pokazujący wartość hello hello określonego węzła.</span><span class="sxs-lookup"><span data-stu-id="59909-259">hello read option toodisplays a context panel showing hello value of hello specific node.</span></span> <span data-ttu-id="59909-260">Witaj zapisu opcja wyświetla panel kontekstu, gdzie można wprowadzić nową wartość.</span><span class="sxs-lookup"><span data-stu-id="59909-260">hello write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="59909-261">Opcja wywołania Hello wyświetlany jest węzeł wprowadzane parametry hello hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="59909-261">hello call option displays a node where you can enter hello parameters for hello call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="59909-262">Publikowanie węzła</span><span class="sxs-lookup"><span data-stu-id="59909-262">Publish a node</span></span>

<span data-ttu-id="59909-263">Po przejściu *symulowane serwera OPC UA*, można także toopublish nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="59909-263">When you browse a *simulated OPC UA server*, you can also choose toopublish new nodes.</span></span> <span data-ttu-id="59909-264">Można analizować dane telemetryczne hello z tych węzłów w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="59909-264">You can analyze hello telemetry from these nodes in hello solution.</span></span> <span data-ttu-id="59909-265">Te *symulowane serwerów OPC UA* był łatwo tooexperiment z rozwiązaniem hello wstępnie bez wdrażania rzeczywistego urządzenia fizycznego.</span><span class="sxs-lookup"><span data-stu-id="59909-265">These *simulated OPC UA servers* make it easy tooexperiment with hello preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="59909-266">Przeglądaj tooa węzła w hello OPC UA serwera przeglądarki drzewa, że chcesz toopublish.</span><span class="sxs-lookup"><span data-stu-id="59909-266">Browse tooa node in hello OPC UA server browser tree that you wish toopublish.</span></span>

2. <span data-ttu-id="59909-267">Kliknij prawym przyciskiem myszy węzeł hello.</span><span class="sxs-lookup"><span data-stu-id="59909-267">Right-click hello node.</span></span>

3. <span data-ttu-id="59909-268">Wybierz polecenie **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="59909-268">Choose **Publish**.</span></span>

    ![Publikowanie węzła przez połączoną fabrykę][cf-img-publish-node]

4. <span data-ttu-id="59909-270">Pojawia się okno kontekstu informuje, że hello publikowania zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="59909-270">A context panel appears which tells you that hello publish has succeeded.</span></span> <span data-ttu-id="59909-271">węzeł Hello jest wyświetlany w widoku poziomu stacji hello znacznik wyboru obok siebie.</span><span class="sxs-lookup"><span data-stu-id="59909-271">hello node appears in hello station level view with a check mark beside it.</span></span>

    ![Pomyślne publikowanie we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="59909-273">Sterowanie i kontrola</span><span class="sxs-lookup"><span data-stu-id="59909-273">Command and control</span></span>

<span data-ttu-id="59909-274">Fabryka połączonych Hello umożliwia poleceń i kontroli urządzeń branży bezpośrednio z chmury hello.</span><span class="sxs-lookup"><span data-stu-id="59909-274">hello connected factory allows you command and control your industry devices directly from hello cloud.</span></span> <span data-ttu-id="59909-275">Możesz użyć tej funkcji tooalerts toorespond, który jest generowany przez urządzenie hello.</span><span class="sxs-lookup"><span data-stu-id="59909-275">You can use this feature toorespond tooalerts generated by hello device.</span></span> <span data-ttu-id="59909-276">Na przykład może wysyłać polecenia toohello urządzenia ze hello chmury.</span><span class="sxs-lookup"><span data-stu-id="59909-276">For example, you could send a command toohello device from hello cloud.</span></span> <span data-ttu-id="59909-277">Można znaleźć hello dostępnych poleceń w hello **StationCommands** węzła w hello OPC UA serwerów przeglądarki drzewa.</span><span class="sxs-lookup"><span data-stu-id="59909-277">You can find hello available commands in hello **StationCommands** node in hello OPC UA servers browser tree.</span></span> <span data-ttu-id="59909-278">W tym scenariuszu możesz otworzyć zawór wersji wykorzystania na stacji zestawu hello wiersza produkcyjnym we Wrocławiu.</span><span class="sxs-lookup"><span data-stu-id="59909-278">In this scenario, you open a pressure release valve on hello assembly station of a production line in Munich.</span></span> <span data-ttu-id="59909-279">Funkcje polecenia i kontroli toouse hello, musisz być w hello **administratora** rolę hello wstępnie wdrażania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="59909-279">toouse hello command and control functionality, you must be in hello **Administrator** role for hello preconfigured solution deployment.</span></span>

1. <span data-ttu-id="59909-280">Przeglądaj toohello **StationCommands** węzła w hello OPC UA serwera przeglądarki drzewa.</span><span class="sxs-lookup"><span data-stu-id="59909-280">Browse toohello **StationCommands** node in hello OPC UA server browser tree.</span></span>

2. <span data-ttu-id="59909-281">Wybierz polecenie hello, że chcesz użycia.</span><span class="sxs-lookup"><span data-stu-id="59909-281">Choose hello command that you wish use.</span></span>

3. <span data-ttu-id="59909-282">Kliknij prawym przyciskiem myszy węzeł hello.</span><span class="sxs-lookup"><span data-stu-id="59909-282">Right-click hello node.</span></span>

4. <span data-ttu-id="59909-283">Wybierz polecenie **Wywołaj**.</span><span class="sxs-lookup"><span data-stu-id="59909-283">Choose **Call**.</span></span>

    ![Polecenie wywoływania we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-call-command]

5. <span data-ttu-id="59909-285">Panel kontekstu pojawia się informacją, którego metoda zamierzasz toocall i dotyczy żadnych szczegółów parametru.</span><span class="sxs-lookup"><span data-stu-id="59909-285">A context panel appears informing you which method you are about toocall and any parameter details is applicable.</span></span>

6. <span data-ttu-id="59909-286">Wybierz polecenie **Wywołaj**.</span><span class="sxs-lookup"><span data-stu-id="59909-286">Choose **Call**.</span></span>

    ![Kontekst wywołania we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-call-context]

7. <span data-ttu-id="59909-288">panel kontekstu Hello jest zaktualizowane tooinform że hello wywołania metody, które zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="59909-288">hello context panel is updated tooinform you that hello method call succeeded.</span></span> <span data-ttu-id="59909-289">Możesz sprawdzić hello wywołanie zakończyło się pomyślnie, odczytując wartości hello hello wykorzystania węzła, który zaktualizowany w wyniku wywołania hello.</span><span class="sxs-lookup"><span data-stu-id="59909-289">You can verify hello call succeeded by reading hello value of hello pressure node that updated as a result of hello call.</span></span>

    ![Powodzenie wywołania we wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][cf-img-call-success]


## <a name="behind-hello-scenes"></a><span data-ttu-id="59909-291">Tle hello</span><span class="sxs-lookup"><span data-stu-id="59909-291">Behind hello scenes</span></span>

<span data-ttu-id="59909-292">Podczas wdrażania wstępnie skonfigurowanych rozwiązań procesu wdrażania hello tworzy wiele zasobów w hello subskrypcji platformy Azure, które wybrano.</span><span class="sxs-lookup"><span data-stu-id="59909-292">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="59909-293">Te zasoby można wyświetlić w hello Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="59909-293">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="59909-294">Utworzenie procesu wdrażania Hello **grupy zasobów** o nazwie na podstawie nazwy hello wybierz wstępnie skonfigurowanego rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="59909-294">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Wstępnie skonfigurowane rozwiązanie w hello portalu Azure][img-cf-portal]

<span data-ttu-id="59909-296">Można wyświetlać ustawienia hello każdego zasobu, wybierając ją z listy hello zasobów w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="59909-296">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="59909-297">Można również wyświetlić kod źródłowy hello hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="59909-297">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="59909-298">Hello połączonych fabryki wstępnie skonfigurowane rozwiązanie kod źródłowy jest w hello [azure iot — połączony fabryka] [ lnk-cfgithub] repozytorium GitHub:</span><span class="sxs-lookup"><span data-stu-id="59909-298">hello connected factory preconfigured solution source code is in hello [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="59909-299">Gdy wszystko będzie gotowe, możesz usunąć hello wstępnie skonfigurowane rozwiązanie z subskrypcją platformy Azure na powitania [azureiotsuite.com] [ lnk-azureiotsuite] lokacji.</span><span class="sxs-lookup"><span data-stu-id="59909-299">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="59909-300">Ta witryna umożliwia delete tooeasily hello wszystkie zasoby, które zostały udostępnione po utworzeniu hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="59909-300">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="59909-301">tooensure Usuń wszystkie powiązane toohello wstępnie skonfigurowane rozwiązanie, usuń go na powitania [azureiotsuite.com] [ lnk-azureiotsuite] lokacji.</span><span class="sxs-lookup"><span data-stu-id="59909-301">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="59909-302">Nie należy usuwać hello grupy zasobów w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="59909-302">Do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59909-303">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="59909-303">Next Steps</span></span>

<span data-ttu-id="59909-304">Teraz, po wdrożeniu rozwiązania pracy wstępnie skonfigurowane, można nadal wprowadzenie pakiet IoT odczytując hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="59909-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="59909-305">[Przewodnik po wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="59909-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="59909-306">[Łączenie rozwiązania połączonych fabryki wstępnie toohello urządzenia][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="59909-306">[Connect your device toohello Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="59909-307">[Uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="59909-307">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

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