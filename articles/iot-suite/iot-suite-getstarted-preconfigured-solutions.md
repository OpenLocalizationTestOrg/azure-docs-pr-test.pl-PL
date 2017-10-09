---
title: "aaaGet pracę z wstępnie rozwiązania | Dokumentacja firmy Microsoft"
description: "Postępuj zgodnie z tego samouczka toolearn jak toodeploy pakiet IoT Azure wstępnie skonfigurowane rozwiązanie."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a><span data-ttu-id="5b766-103">Rozpoczynanie pracy z rozwiązaniami hello wstępnie</span><span class="sxs-lookup"><span data-stu-id="5b766-103">Get started with hello preconfigured solutions</span></span>

<span data-ttu-id="5b766-104">Pakiet Azure IoT [wstępnie rozwiązań] [ lnk-preconfigured-solutions] łączenie wielu Azure IoT usług toodeliver end-to-end rozwiązania, które implementuje typowych scenariuszy biznesowych IoT.</span><span class="sxs-lookup"><span data-stu-id="5b766-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="5b766-105">Witaj *monitorowania zdalnego* wstępnie skonfigurowane rozwiązanie łączy monitorów tooand urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5b766-105">hello *remote monitoring* preconfigured solution connects tooand monitors your devices.</span></span> <span data-ttu-id="5b766-106">Można użyć hello rozwiązania tooanalyze hello strumienia danych z urządzeniami i wyników biznesowych tooimprove poprzez procesy automatycznie odpowiadać toothat strumienia danych.</span><span class="sxs-lookup"><span data-stu-id="5b766-106">You can use hello solution tooanalyze hello stream of data from your devices and tooimprove business outcomes by making processes respond automatically toothat stream of data.</span></span>

<span data-ttu-id="5b766-107">W tym samouczku przedstawiono sposób monitorowania zdalnego hello tooprovision wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="5b766-107">This tutorial shows you how tooprovision hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="5b766-108">On również przeprowadzi Cię przez hello podstawowych funkcji hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="5b766-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="5b766-109">Dostępne wiele z tych funkcji z rozwiązania hello *pulpitu nawigacyjnego* która wdraża jako część rozwiązania hello wstępnie skonfigurowane:</span><span class="sxs-lookup"><span data-stu-id="5b766-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][img-dashboard]

<span data-ttu-id="5b766-111">toocomplete tego samouczka należy aktywną subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5b766-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="5b766-112">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="5b766-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5b766-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="5b766-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="5b766-114">Omówienie scenariusza</span><span class="sxs-lookup"><span data-stu-id="5b766-114">Scenario overview</span></span>

<span data-ttu-id="5b766-115">Podczas wdrażania hello zdalnego wstępnie skonfigurowane rozwiązanie monitorujące, jest wypełniana wstępnie zasobów umożliwiających toostep za pośrednictwem zdalnego typowym scenariuszem monitorowania.</span><span class="sxs-lookup"><span data-stu-id="5b766-115">When you deploy hello remote monitoring preconfigured solution, it is prepopulated with resources that enable you toostep through a common remote monitoring scenario.</span></span> <span data-ttu-id="5b766-116">W tym scenariuszu kilka urządzeń podłączonych toohello rozwiązania są raportowania temperatury nieoczekiwane wartości.</span><span class="sxs-lookup"><span data-stu-id="5b766-116">In this scenario, several devices connected toohello solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="5b766-117">Hello następnych sekcjach opisano sposób do:</span><span class="sxs-lookup"><span data-stu-id="5b766-117">hello following sections show you how to:</span></span>

* <span data-ttu-id="5b766-118">Identyfikowanie urządzeń hello wysyłania temperatury nieoczekiwane wartości.</span><span class="sxs-lookup"><span data-stu-id="5b766-118">Identify hello devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="5b766-119">Skonfiguruj te urządzenia toosend bardziej szczegółowe dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="5b766-119">Configure these devices toosend more detailed telemetry.</span></span>
* <span data-ttu-id="5b766-120">Rozwiąż hello problem przez aktualizację oprogramowania układowego hello na tych urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="5b766-120">Fix hello problem by updating hello firmware on these devices.</span></span>
* <span data-ttu-id="5b766-121">Upewnij się, że Twoje działanie zostało rozwiązane hello problem.</span><span class="sxs-lookup"><span data-stu-id="5b766-121">Verify that your action has resolved hello issue.</span></span>

<span data-ttu-id="5b766-122">Kluczowy element w tym scenariuszu jest, że te akcje można wykonać zdalnie z poziomu pulpitu nawigacyjnego hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5b766-122">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="5b766-123">Nie trzeba urządzeń toohello fizyczny dostęp.</span><span class="sxs-lookup"><span data-stu-id="5b766-123">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="5b766-124">Pulpit nawigacyjny rozwiązania hello widoku</span><span class="sxs-lookup"><span data-stu-id="5b766-124">View hello solution dashboard</span></span>

<span data-ttu-id="5b766-125">pulpit nawigacyjny rozwiązania Hello umożliwia toomanage hello wdrożyć rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="5b766-125">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="5b766-126">Można na przykład wyświetlać dane telemetryczne, dodawać urządzenia i konfigurować reguły.</span><span class="sxs-lookup"><span data-stu-id="5b766-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="5b766-127">Po ukończeniu inicjowania obsługi administracyjnej hello i wskazuje hello Kafelek wstępnie skonfigurowane rozwiązanie **gotowe**, wybierz **uruchamianie** tooopen zdalnego monitorowania rozwiązania portalem na nowej karcie.</span><span class="sxs-lookup"><span data-stu-id="5b766-127">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Uruchamianie hello wstępnie skonfigurowane rozwiązanie][img-launch-solution]

1. <span data-ttu-id="5b766-129">Domyślnie hello rozwiązanie portalu pokazuje hello *pulpitu nawigacyjnego*.</span><span class="sxs-lookup"><span data-stu-id="5b766-129">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="5b766-130">Można przejść obszarów tooother hello rozwiązanie portalu przy użyciu hello menu na powitania po lewej stronie powitania strony.</span><span class="sxs-lookup"><span data-stu-id="5b766-130">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][img-menu]

<span data-ttu-id="5b766-132">pulpit nawigacyjny Hello Wyświetla hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="5b766-132">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="5b766-133">Mapy zawiera hello lokalizację każdego urządzenia połączone toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5b766-133">A map that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="5b766-134">Przy pierwszym uruchomieniu rozwiązania hello, istnieją 25 urządzeń symulowane.</span><span class="sxs-lookup"><span data-stu-id="5b766-134">When you first run hello solution, there are 25 simulated devices.</span></span> <span data-ttu-id="5b766-135">Witaj symulowanego urządzenia są zaimplementowane jako zadań Webjob Azure, a rozwiązania hello używa informacji tooplot interfejsu API map Bing hello na mapie hello.</span><span class="sxs-lookup"><span data-stu-id="5b766-135">hello simulated devices are implemented as Azure WebJobs, and hello solution uses hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="5b766-136">Zobacz hello [— często zadawane pytania] [ lnk-faq] toolearn jak toomake hello dynamicznie mapy.</span><span class="sxs-lookup"><span data-stu-id="5b766-136">See hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="5b766-137">Panel **Historia telemetrii**, na którym są wyświetlane niemal w czasie rzeczywistym dane telemetryczne dotyczące wilgotności i temperatury pochodzące z wybranego urządzenia oraz dane zagregowane, takie jak wilgotność maksymalna, minimalna i średnia.</span><span class="sxs-lookup"><span data-stu-id="5b766-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="5b766-138">Panel **Historia alarmów**, na którym są wyświetlane ostatnie zdarzenia alarmów generowane w przypadku przekroczenia progu przez wartość telemetryczną.</span><span class="sxs-lookup"><span data-stu-id="5b766-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="5b766-139">W przykładach toohello dodanie utworzone przez hello wstępnie skonfigurowane rozwiązanie można zdefiniować własne alarmy.</span><span class="sxs-lookup"><span data-stu-id="5b766-139">You can define your own alarms in addition toohello examples created by hello preconfigured solution.</span></span>
* <span data-ttu-id="5b766-140">Panel **Zadania**, na którym są wyświetlane informacje o zaplanowanych zadaniach.</span><span class="sxs-lookup"><span data-stu-id="5b766-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="5b766-141">Własne zadania można zaplanować na stronie **Zadania zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="5b766-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="5b766-142">Wyświetlanie alarmów</span><span class="sxs-lookup"><span data-stu-id="5b766-142">View alarms</span></span>

<span data-ttu-id="5b766-143">panel Historia alarm Hello pokazuje wyższe niż wartości oczekiwanej telemetrii raportowania pięciu urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5b766-143">hello alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Historia TODO Alarm hello pulpit nawigacyjny rozwiązania][img-alarms]

> [!NOTE]
> <span data-ttu-id="5b766-145">Alarmy te są generowane przez regułę, która znajduje się w hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="5b766-145">These alarms are generated by a rule that is included in hello preconfigured solution.</span></span> <span data-ttu-id="5b766-146">Ta reguła generuje alert, gdy wartość temperatury hello wysyłanych przez urządzenia przekracza 60.</span><span class="sxs-lookup"><span data-stu-id="5b766-146">This rule generates an alert when hello temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="5b766-147">Można zdefiniować własne reguły oraz akcje, wybierając [reguły](#add-a-rule) i [akcje](#add-an-action) w menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="5b766-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in hello left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="5b766-148">Wyświetlanie urządzeń</span><span class="sxs-lookup"><span data-stu-id="5b766-148">View devices</span></span>

<span data-ttu-id="5b766-149">Witaj *urządzeń* lista zawiera wszystkie urządzenia hello zarejestrowane w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="5b766-149">hello *devices* list shows all hello registered devices in hello solution.</span></span> <span data-ttu-id="5b766-150">Z listy urządzeń hello można wyświetlać i edytować metadane urządzenia Dodaj lub usuń urządzeń i wywołania metod na urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="5b766-150">From hello device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="5b766-151">Można filtrować i sortować listę hello urządzeń na liście urządzeń hello.</span><span class="sxs-lookup"><span data-stu-id="5b766-151">You can filter and sort hello list of devices in hello device list.</span></span> <span data-ttu-id="5b766-152">Można również dostosować kolumn hello hello listę urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5b766-152">You can also customize hello columns shown in hello device list.</span></span>

1. <span data-ttu-id="5b766-153">Wybierz **urządzeń** listę urządzeń hello tooshow dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5b766-153">Choose **Devices** tooshow hello device list for this solution.</span></span>

   ![Widok listy urządzeń hello hello rozwiązanie portalu][img-devicelist]

1. <span data-ttu-id="5b766-155">Lista urządzeń Hello pokazuje początkowo 25 urządzeń symulowane utworzonych przez hello w procesie inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="5b766-155">hello device list initially shows 25 simulated devices created by hello provisioning process.</span></span> <span data-ttu-id="5b766-156">Można dodać dodatkowych urządzeń fizycznych i symulowane toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5b766-156">You can add additional simulated and physical devices toohello solution.</span></span>

1. <span data-ttu-id="5b766-157">Szczegóły hello tooview urządzenia, wybierz urządzenie na liście urządzeń hello.</span><span class="sxs-lookup"><span data-stu-id="5b766-157">tooview hello details of a device, choose a device in hello device list.</span></span>

   ![Wyświetl szczegóły urządzenia hello w portalu rozwiązania hello][img-devicedetails]

<span data-ttu-id="5b766-159">Witaj **szczegóły urządzenia** panelu zawiera sześć sekcje:</span><span class="sxs-lookup"><span data-stu-id="5b766-159">hello **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="5b766-160">Kolekcja łączy włączyć możesz toocustomize hello ikonę urządzenia, wyłączyć urządzenie hello, Dodaj regułę, wywoływanie metody lub wysyłać polecenia.</span><span class="sxs-lookup"><span data-stu-id="5b766-160">A collection of links that enable you toocustomize hello device icon, disable hello device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="5b766-161">Porównanie poleceń (komunikatów wysyłanych z urządzenia do chmury) i metod (metod bezpośrednich) znajduje się w temacie [Wskazówki dotyczące komunikacji z chmury do urządzenia][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="5b766-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="5b766-162">Witaj **dwie urządzenia - tagi** sekcja umożliwia wartości tagów tooedit hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5b766-162">hello **Device Twin - Tags** section enables you tooedit tag values for hello device.</span></span> <span data-ttu-id="5b766-163">Można wyświetlić wartości tagów w hello listę urządzeń i używać listę urządzeń hello toofilter wartości tagu.</span><span class="sxs-lookup"><span data-stu-id="5b766-163">You can display tag values in hello device list and use tag values toofilter hello device list.</span></span>
* <span data-ttu-id="5b766-164">Witaj **dwie urządzenia - żądanego właściwości** sekcja umożliwia tooset właściwości wartości toobe wysyłane toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5b766-164">hello **Device Twin - Desired Properties** section enables you tooset property values toobe sent toohello device.</span></span>
* <span data-ttu-id="5b766-165">Hello **dwie urządzenia - zgłosił właściwości** sekcji przedstawiono wysyłane z urządzenia hello wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="5b766-165">hello **Device Twin - Reported Properties** section shows property values sent from hello device.</span></span>
* <span data-ttu-id="5b766-166">Witaj **właściwości urządzenia** sekcja zawiera informacje z rejestru tożsamości hello, takie jak urządzenie hello klucze identyfikator i uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="5b766-166">hello **Device Properties** section shows information from hello identity registry such as hello device id and authentication keys.</span></span>
* <span data-ttu-id="5b766-167">Witaj **ostatnich zadań** sekcja zawiera informacje dotyczące zadań, które ostatnio ustawione tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5b766-167">hello **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-hello-device-list"></a><span data-ttu-id="5b766-168">Lista urządzeń hello filtru</span><span class="sxs-lookup"><span data-stu-id="5b766-168">Filter hello device list</span></span>

<span data-ttu-id="5b766-169">Można użyć tylko te urządzenia, które wysyłają wartości temperatury nieoczekiwany toodisplay filtru.</span><span class="sxs-lookup"><span data-stu-id="5b766-169">You can use a filter toodisplay only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="5b766-170">Hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie obejmuje hello **złej kondycji urządzeń** urządzenia tooshow o wartości średnia temperatura przekracza 60 filtrować.</span><span class="sxs-lookup"><span data-stu-id="5b766-170">hello remote monitoring preconfigured solution includes hello **Unhealthy devices** filter tooshow devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="5b766-171">Możesz również [utworzyć własne filtry](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="5b766-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="5b766-172">Wybierz **Otwórz zapisany filtr** toodisplay listę dostępnych filtrów.</span><span class="sxs-lookup"><span data-stu-id="5b766-172">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="5b766-173">Następnie wybierz pozycję **złej kondycji urządzeń** tooapply hello filtru:</span><span class="sxs-lookup"><span data-stu-id="5b766-173">Then choose **Unhealthy devices** tooapply hello filter:</span></span>

    ![Wyświetl listę hello filtry][img-unhealthy-filter]

1. <span data-ttu-id="5b766-175">Lista urządzeń Hello zawiera obecnie tylko urządzenia z wartością średnią temperaturę większa niż 60.</span><span class="sxs-lookup"><span data-stu-id="5b766-175">hello device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Lista filtrowane urządzeń hello widok przedstawiający złej kondycji urządzenia][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="5b766-177">Aktualizowanie żądanych właściwości</span><span class="sxs-lookup"><span data-stu-id="5b766-177">Update desired properties</span></span>

<span data-ttu-id="5b766-178">Na tym etapie zidentyfikowano zestaw urządzeń, które mogą wymagać naprawy.</span><span class="sxs-lookup"><span data-stu-id="5b766-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="5b766-179">Jednak zdecydujesz, że częstotliwość danych hello 15 sekund jest niewystarczająca dla wyczyść diagnozy problemu hello.</span><span class="sxs-lookup"><span data-stu-id="5b766-179">However, you decide that hello data frequency of 15 seconds is not sufficient for a clear diagnosis of hello issue.</span></span> <span data-ttu-id="5b766-180">Zmiana hello telemetrii częstotliwość toofive sekund tooprovide z więcej toobetter punktów danych zdiagnozowaniu problemu hello.</span><span class="sxs-lookup"><span data-stu-id="5b766-180">Changing hello telemetry frequency toofive seconds tooprovide you with more data points toobetter diagnose hello issue.</span></span> <span data-ttu-id="5b766-181">Ta konfiguracja zmiany tooyour urządzeń zdalnych można wypchnąć hello rozwiązanie portalu.</span><span class="sxs-lookup"><span data-stu-id="5b766-181">You can push this configuration change tooyour remote devices from hello solution portal.</span></span> <span data-ttu-id="5b766-182">Istnieje możliwość zmiany hello raz, ocenić wpływ hello i działa na powitania wyniki.</span><span class="sxs-lookup"><span data-stu-id="5b766-182">You can make hello change once, evaluate hello impact, and then act on hello results.</span></span>

<span data-ttu-id="5b766-183">Wykonaj te kroki toorun zadanie, które zmienia hello **TelemetryInterval** wymaganą właściwość hello wpływ na urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5b766-183">Follow these steps toorun a job that changes hello **TelemetryInterval** desired property for hello affected devices.</span></span> <span data-ttu-id="5b766-184">Gdy urządzenia hello otrzymują hello nowe **TelemetryInterval** wartość właściwości, zmień ich telemetrii toosend konfiguracji co pięć sekund zamiast co 15 sekund:</span><span class="sxs-lookup"><span data-stu-id="5b766-184">When hello devices receive hello new **TelemetryInterval** property value, they change their configuration toosend telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="5b766-185">Gdy hello listę złej kondycji urządzeń są wyświetlane na liście urządzeń hello, wybierz **harmonogramu zadań**, następnie **Edytuj dwie urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="5b766-185">While you are showing hello list of unhealthy devices in hello device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="5b766-186">Wywołanie zadania hello **interwał telemetrii zmiany**.</span><span class="sxs-lookup"><span data-stu-id="5b766-186">Call hello job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="5b766-187">Zmień wartość hello hello **żądanej właściwości** nazwa **żądany. Config.TelemetryInterval** toofive sekund.</span><span class="sxs-lookup"><span data-stu-id="5b766-187">Change hello value of hello **Desired Property** name **desired.Config.TelemetryInterval** toofive seconds.</span></span>

1. <span data-ttu-id="5b766-188">Wybierz pozycję **Zaplanuj**.</span><span class="sxs-lookup"><span data-stu-id="5b766-188">Choose **Schedule**.</span></span>

    ![Zmień hello TelemetryInterval właściwości toofive sekund][img-change-interval]

1. <span data-ttu-id="5b766-190">Możesz monitorować postęp hello zadania hello na powitania **zadań zarządzania** w portalu hello na stronie.</span><span class="sxs-lookup"><span data-stu-id="5b766-190">You can monitor hello progress of hello job on hello **Management Jobs** page in hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5b766-191">Toochange wartość żądanej właściwości dla poszczególnych urządzeń, należy użyć hello **odpowiednie właściwości** części hello **szczegóły urządzenia** panelu zamiast uruchamiania zadania.</span><span class="sxs-lookup"><span data-stu-id="5b766-191">If you want toochange a desired property value for an individual device, use hello **Desired Properties** section in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="5b766-192">To zadanie ustawia wartość hello hello **TelemetryInterval** wymaganą właściwość w Witaj dwie urządzenia dla wszystkich hello urządzenia wybrane przez filtr hello.</span><span class="sxs-lookup"><span data-stu-id="5b766-192">This job sets hello value of hello **TelemetryInterval** desired property in hello device twin for all hello devices selected by hello filter.</span></span> <span data-ttu-id="5b766-193">urządzenia Hello pobierania tej wartości ze Witaj dwie urządzenia i zaktualizować ich zachowanie.</span><span class="sxs-lookup"><span data-stu-id="5b766-193">hello devices retrieve this value from hello device twin and update their behavior.</span></span> <span data-ttu-id="5b766-194">Gdy urządzenie pobiera i przetwarza żądaną właściwość z dwie urządzenia, ustawia hello odpowiadającej podanej wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="5b766-194">When a device retrieves and processes a desired property from a device twin, it sets hello corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="5b766-195">Wywoływanie metod</span><span class="sxs-lookup"><span data-stu-id="5b766-195">Invoke methods</span></span>

<span data-ttu-id="5b766-196">Podczas wykonywania zadania hello zauważysz hello lista urządzeń zła czy te urządzenia mają stary (mniej niż w wersji 1.6) oprogramowania układowego wersji.</span><span class="sxs-lookup"><span data-stu-id="5b766-196">While hello job runs, you notice in hello list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Wersja oprogramowania układowego hello złej kondycji urządzeń zgłoszonych hello widoku][img-old-firmware]

<span data-ttu-id="5b766-198">Ta wersja oprogramowania układowego może być hello głównej przyczyny nieoczekiwanego hello temperatury wartości, ponieważ wiadomo, że inne dobrej kondycji urządzenia były ostatnio zaktualizowano tooversion 2.0.</span><span class="sxs-lookup"><span data-stu-id="5b766-198">This firmware version may be hello root cause of hello unexpected temperature values because you know that other healthy devices were recently updated tooversion 2.0.</span></span> <span data-ttu-id="5b766-199">Można użyć wbudowanych hello **starego oprogramowanie układowe urządzeń** filtrować tooidentify wszystkie urządzenia z stare wersje oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="5b766-199">You can use hello built-in **Old firmware devices** filter tooidentify any devices with old firmware versions.</span></span> <span data-ttu-id="5b766-200">Z portalu hello można zdalnie zaktualizować wszystkie urządzenia hello nadal działa stare wersje oprogramowania układowego:</span><span class="sxs-lookup"><span data-stu-id="5b766-200">From hello portal, you can then remotely update all hello devices still running old firmware versions:</span></span>

1. <span data-ttu-id="5b766-201">Wybierz **Otwórz zapisany filtr** toodisplay listę dostępnych filtrów.</span><span class="sxs-lookup"><span data-stu-id="5b766-201">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="5b766-202">Następnie wybierz pozycję **starego oprogramowanie układowe urządzeń** tooapply hello filtru:</span><span class="sxs-lookup"><span data-stu-id="5b766-202">Then choose **Old firmware devices** tooapply hello filter:</span></span>

    ![Wyświetl listę hello filtry][img-old-filter]

1. <span data-ttu-id="5b766-204">Lista urządzeń Hello zawiera obecnie tylko urządzenia z stare wersje oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="5b766-204">hello device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="5b766-205">Ta lista zawiera pięć urządzeń hello identyfikowane przez hello **złej kondycji urządzeń** filtru oraz trzy dodatkowe urządzenia:</span><span class="sxs-lookup"><span data-stu-id="5b766-205">This list includes hello five devices identified by hello **Unhealthy devices** filter and three additional devices:</span></span>

    ![Lista filtrowane urządzeń hello widok przedstawiający starego urządzeń][img-filtered-old-list]

1. <span data-ttu-id="5b766-207">Wybierz pozycję **Harmonogram zadań**, a następnie pozycję **Wywołaj metodę**.</span><span class="sxs-lookup"><span data-stu-id="5b766-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="5b766-208">Ustaw **Nazwa zadania** za**tooversion aktualizacji oprogramowania układowego 2.0**.</span><span class="sxs-lookup"><span data-stu-id="5b766-208">Set **Job Name** too**Firmware update tooversion 2.0**.</span></span>

1. <span data-ttu-id="5b766-209">Wybierz **InitiateFirmwareUpdate** jako hello **metody**.</span><span class="sxs-lookup"><span data-stu-id="5b766-209">Choose **InitiateFirmwareUpdate** as hello **Method**.</span></span>

1. <span data-ttu-id="5b766-210">Zestaw hello **FwPackageUri** parametru zbyt**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="5b766-210">Set hello **FwPackageUri** parameter too**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="5b766-211">Wybierz pozycję **Zaplanuj**.</span><span class="sxs-lookup"><span data-stu-id="5b766-211">Choose **Schedule**.</span></span> <span data-ttu-id="5b766-212">domyślne Hello jest teraz dla hello toorun zadania.</span><span class="sxs-lookup"><span data-stu-id="5b766-212">hello default is for hello job toorun now.</span></span>

    ![Utwórz zadanie tooupdate hello oprogramowanie układowe hello wybrane urządzeń][img-method-update]

> [!NOTE]
> <span data-ttu-id="5b766-214">Tooinvoke metody na poszczególne urządzenia, wybierz opcję **metody** w hello **szczegóły urządzenia** panelu zamiast uruchamiania zadania.</span><span class="sxs-lookup"><span data-stu-id="5b766-214">If you want tooinvoke a method on an individual device, choose **Methods** in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="5b766-215">To zadanie wywołuje hello **InitiateFirmwareUpdate** metoda bezpośrednia na wszystkich urządzeniach hello wybrane przez filtr hello.</span><span class="sxs-lookup"><span data-stu-id="5b766-215">This job invokes hello **InitiateFirmwareUpdate** direct method on all hello devices selected by hello filter.</span></span> <span data-ttu-id="5b766-216">Urządzenia reagowanie tooIoT koncentratora i inicjuje proces aktualizacji oprogramowania układowego hello asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="5b766-216">Devices respond immediately tooIoT Hub and then initiate hello firmware update process asynchronously.</span></span> <span data-ttu-id="5b766-217">urządzenia Hello Podaj informacjami o stanie procesu aktualizacji oprogramowania układowego hello za pomocą wartości właściwości zgłoszone, jak pokazano w powitania po zrzuty ekranu.</span><span class="sxs-lookup"><span data-stu-id="5b766-217">hello devices provide status information about hello firmware update process through reported property values, as shown in hello following screenshots.</span></span> <span data-ttu-id="5b766-218">Wybierz hello **Odśwież** ikona tooupdate hello informacji hello list urządzeń i zadania:</span><span class="sxs-lookup"><span data-stu-id="5b766-218">Choose hello **Refresh** icon tooupdate hello information in hello device and job lists:</span></span>

<span data-ttu-id="5b766-219">![Listy zadań przedstawiający uruchamianie listy aktualizacji oprogramowania układowego hello][img-update-1]
![listę urządzeń przedstawiający stan aktualizacji oprogramowania układowego][img-update-2]
![listy przedstawiający hello oprogramowania układowego aktualizacji listy zadań ukończone][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="5b766-219">![Job list showing hello firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing hello firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="5b766-220">W środowisku produkcyjnym można zaplanować zadania toorun w oknie obsługi wyznaczonych.</span><span class="sxs-lookup"><span data-stu-id="5b766-220">In a production environment, you can schedule jobs toorun during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="5b766-221">Przegląd scenariusza</span><span class="sxs-lookup"><span data-stu-id="5b766-221">Scenario review</span></span>

<span data-ttu-id="5b766-222">W tym scenariuszu zidentyfikowanego potencjalny problem z niektórych urządzeń zdalnego przy użyciu historii alarm hello na powitania pulpitu nawigacyjnego i filtru.</span><span class="sxs-lookup"><span data-stu-id="5b766-222">In this scenario, you identified a potential issue with some of your remote devices using hello alarm history on hello dashboard and a filter.</span></span> <span data-ttu-id="5b766-223">Następnie używane hello filtru i tooremotely zadania skonfigurować hello urządzeń tooprovide więcej informacji o toohelp zdiagnozować problem hello.</span><span class="sxs-lookup"><span data-stu-id="5b766-223">You then used hello filter and a job tooremotely configure hello devices tooprovide more information toohelp diagnose hello issue.</span></span> <span data-ttu-id="5b766-224">Na koniec użyto filtr i zadania konserwacji tooschedule na urządzeniach hello, których to dotyczy.</span><span class="sxs-lookup"><span data-stu-id="5b766-224">Finally, you used a filter and a job tooschedule maintenance on hello affected devices.</span></span> <span data-ttu-id="5b766-225">Jeśli zwróci toohello pulpitu nawigacyjnego, można sprawdzić, czy nie ma już wszystkie alarmy przesyłanych z urządzeń w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="5b766-225">If you return toohello dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="5b766-226">Można użyć filtru tooverify, że oprogramowanie układowe hello jest aktualny na wszystkich urządzeniach hello rozwiązania, oraz czy nie ma więcej złej kondycji urządzeń:</span><span class="sxs-lookup"><span data-stu-id="5b766-226">You can use a filter tooverify that hello firmware is up-to-date on all hello devices in your solution and that there are no more unhealthy devices:</span></span>

![Filtr przedstawiający, że wszystkie urządzenia mają aktualne oprogramowanie układowe][img-updated]

![Filtr przedstawiający, że wszystkie urządzenia są w dobrej kondycji][img-healthy]

## <a name="other-features"></a><span data-ttu-id="5b766-229">Pozostałe funkcje</span><span class="sxs-lookup"><span data-stu-id="5b766-229">Other features</span></span>

<span data-ttu-id="5b766-230">Witaj poniższych sekcjach opisano niektóre dodatkowe funkcje hello zdalnego wstępnie skonfigurowane rozwiązanie monitorujące, które nie zostały opisane w ramach hello poprzednim scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="5b766-230">hello following sections describe some additional features of hello remote monitoring preconfigured solution that are not described as part of hello previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="5b766-231">Dostosowywanie kolumn</span><span class="sxs-lookup"><span data-stu-id="5b766-231">Customize columns</span></span>

<span data-ttu-id="5b766-232">Można dostosować hello informacje wyświetlane na liście urządzeń hello, wybierając **Edytor kolumn**.</span><span class="sxs-lookup"><span data-stu-id="5b766-232">You can customize hello information shown in hello device list by choosing **Column editor**.</span></span> <span data-ttu-id="5b766-233">Istnieje możliwość dodawania i usuwania kolumn, w których są wyświetlane zgłaszane wartości właściwości i tagów.</span><span class="sxs-lookup"><span data-stu-id="5b766-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="5b766-234">Można również zmieniać kolejność kolumn i ich nazwy:</span><span class="sxs-lookup"><span data-stu-id="5b766-234">You can also reorder and rename columns:</span></span>

   ![Lista urządzeń hello zakres przechowywania Edytor kolumny][img-columneditor]

### <a name="customize-hello-device-icon"></a><span data-ttu-id="5b766-236">Dostosowywanie hello ikonę urządzenia</span><span class="sxs-lookup"><span data-stu-id="5b766-236">Customize hello device icon</span></span>

<span data-ttu-id="5b766-237">Można dostosować wyświetlane na liście urządzeń hello z hello ikonę urządzenia hello **szczegóły urządzenia** panelu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5b766-237">You can customize hello device icon displayed in hello device list from hello **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="5b766-238">Wybierz hello tooopen ikonę ołówka hello **obraz edycji** panelu dla urządzenia:</span><span class="sxs-lookup"><span data-stu-id="5b766-238">Choose hello pencil icon tooopen hello **Edit image** panel for a device:</span></span>

   ![Otwieranie edytora obrazu dla urządzenia][img-startimageedit]

1. <span data-ttu-id="5b766-240">Przekaż nowy obraz lub użyć jednego z istniejących obrazów hello a następnie wybierz pozycję **zapisać**:</span><span class="sxs-lookup"><span data-stu-id="5b766-240">Either upload a new image or use one of hello existing images and then choose **Save**:</span></span>

   ![Edytowanie edytora obrazu dla urządzenia][img-imageedit]

1. <span data-ttu-id="5b766-242">Witaj obrazu teraz wyświetlany w hello **ikona** kolumny hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5b766-242">hello image you selected now displays in hello **Icon** column for hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="5b766-243">Obraz powitania jest przechowywany w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="5b766-243">hello image is stored in blob storage.</span></span> <span data-ttu-id="5b766-244">Tag w dwie urządzenia hello zawiera obraz toohello łącze w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="5b766-244">A tag in hello device twin contains a link toohello image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="5b766-245">Dodawanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="5b766-245">Add a device</span></span>

<span data-ttu-id="5b766-246">Podczas wdrażania rozwiązania hello wstępnie zainicjować obsługę automatycznie 25 urządzeń próbki widoczne w hello listę urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5b766-246">When you deploy hello preconfigured solution, you automatically provision 25 sample devices that you can see in hello device list.</span></span> <span data-ttu-id="5b766-247">Są to *symulowane urządzenia* uruchamiane w zadaniu WebJob Azure.</span><span class="sxs-lookup"><span data-stu-id="5b766-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="5b766-248">Symulowane urządzeń ułatwiają dla Ciebie tooexperiment z rozwiązaniem hello wstępnie bez hello potrzeby toodeploy prawdziwe, fizycznych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5b766-248">Simulated devices make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical devices.</span></span> <span data-ttu-id="5b766-249">Tooconnect rozwiązania toohello rzeczywistego urządzenia, zobacz hello [połączyć Twoje toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie] [ lnk-connect-rm] samouczka.</span><span class="sxs-lookup"><span data-stu-id="5b766-249">If you do want tooconnect a real device toohello solution, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="5b766-250">Witaj poniższej procedurze pokazano, jak tooadd rozwiązania toohello symulowane urządzenie:</span><span class="sxs-lookup"><span data-stu-id="5b766-250">hello following steps show you how tooadd a simulated device toohello solution:</span></span>

1. <span data-ttu-id="5b766-251">Przejdź wstecz toohello listę urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5b766-251">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="5b766-252">Wybierz urządzenie, tooadd **+ Dodaj urządzenie** hello dole po lewej stronie ekranu.</span><span class="sxs-lookup"><span data-stu-id="5b766-252">tooadd a device, choose **+ Add A Device** in hello bottom left corner.</span></span>

   ![Dodaj urządzenie toohello wstępnie skonfigurowane rozwiązanie][img-adddevice]

1. <span data-ttu-id="5b766-254">Wybierz **Dodaj nowy** na powitania **symulowane urządzenie** kafelka.</span><span class="sxs-lookup"><span data-stu-id="5b766-254">Choose **Add New** on hello **Simulated Device** tile.</span></span>

   ![Określanie szczegółów nowego urządzenia na pulpicie nawigacyjnym][img-addnew]

   <span data-ttu-id="5b766-256">W toocreating dodanie nowych symulowane urządzenie, można także dodać urządzenia fizycznego po wybraniu toocreate **urządzenia niestandardowe**.</span><span class="sxs-lookup"><span data-stu-id="5b766-256">In addition toocreating a new simulated device, you can also add a physical device if you choose toocreate a **Custom Device**.</span></span> <span data-ttu-id="5b766-257">toolearn więcej informacji na temat połączenia urządzeń fizycznych toohello rozwiązania, zobacz [połączyć toohello Twojego urządzenia zdalnego wstępnie skonfigurowane rozwiązanie monitorujące, pakiet IoT][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="5b766-257">toolearn more about connecting physical devices toohello solution, see [Connect your device toohello IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="5b766-258">Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia** i wprowadź unikatowy identyfikator urządzenia, np. **moje_urzadzenie_01**.</span><span class="sxs-lookup"><span data-stu-id="5b766-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="5b766-259">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5b766-259">Choose **Create**.</span></span>

   ![Zapisywanie nowego urządzenia][img-definedevice]

1. <span data-ttu-id="5b766-261">W kroku 3 w artykule **dodać symulowane urządzenie**, wybierz **gotowe** tooreturn toohello urządzenia listy.</span><span class="sxs-lookup"><span data-stu-id="5b766-261">In step 3 of **Add a simulated device**, choose **Done** tooreturn toohello device list.</span></span>

1. <span data-ttu-id="5b766-262">Możesz wyświetlić urządzenia **systemem** hello listy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5b766-262">You can view your device **Running** in hello device list.</span></span>

    ![Wyświetlanie nowego urządzenia na liście urządzeń][img-runningnew]

1. <span data-ttu-id="5b766-264">Można również wyświetlić dane telemetryczne z nowego urządzenia na pulpicie nawigacyjnym hello symulowane hello:</span><span class="sxs-lookup"><span data-stu-id="5b766-264">You can also view hello simulated telemetry from your new device on hello dashboard:</span></span>

    ![Wyświetlanie telemetrii z nowego urządzenia][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="5b766-266">Wyłączanie i usuwanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="5b766-266">Disable and delete a device</span></span>

<span data-ttu-id="5b766-267">Można wyłączyć urządzenie, a następnie je usunąć:</span><span class="sxs-lookup"><span data-stu-id="5b766-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Wyłączanie i usuwanie urządzenia][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="5b766-269">Dodawanie reguły</span><span class="sxs-lookup"><span data-stu-id="5b766-269">Add a rule</span></span>

<span data-ttu-id="5b766-270">Brak reguł dla nowego urządzenia hello zostały dodane.</span><span class="sxs-lookup"><span data-stu-id="5b766-270">There are no rules for hello new device you just added.</span></span> <span data-ttu-id="5b766-271">W tej sekcji możesz dodać regułę, która uruchamia alarm, gdy temperatury hello zgłoszone przez hello nowe, że urządzenia przekracza 47 stopni.</span><span class="sxs-lookup"><span data-stu-id="5b766-271">In this section, you add a rule that triggers an alarm when hello temperature reported by hello new device exceeds 47 degrees.</span></span> <span data-ttu-id="5b766-272">Przed rozpoczęciem należy zauważyć, że Pokazuje historię telemetrii hello hello nowe urządzenie na pulpicie nawigacyjnym hello temperatury urządzenia hello nigdy nie przekracza 45 stopni.</span><span class="sxs-lookup"><span data-stu-id="5b766-272">Before you start, notice that hello telemetry history for hello new device on hello dashboard shows hello device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="5b766-273">Przejdź wstecz toohello listę urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5b766-273">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="5b766-274">tooadd reguły hello urządzenia, wybierz nowe urządzenie hello **listy urządzeń**, a następnie wybierz pozycję **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="5b766-274">tooadd a rule for hello device, select your new device in hello **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="5b766-275">Utworzyć regułę, która używa **temperatury** jako hello pola danych i używa **AlarmTemp** jako hello dane wyjściowe, gdy hello temperatura przekracza 47 stopni:</span><span class="sxs-lookup"><span data-stu-id="5b766-275">Create a rule that uses **Temperature** as hello data field and uses **AlarmTemp** as hello output when hello temperature exceeds 47 degrees:</span></span>

    ![Dodawanie reguły urządzenia][img-adddevicerule]

1. <span data-ttu-id="5b766-277">Wybierz zmiany, toosave **Zapisz i Wyświetl reguły**.</span><span class="sxs-lookup"><span data-stu-id="5b766-277">toosave your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="5b766-278">Wybierz **polecenia** w okienku szczegółów urządzenia hello na powitania nowe urządzenie.</span><span class="sxs-lookup"><span data-stu-id="5b766-278">Choose **Commands** in hello device details pane for hello new device.</span></span>

    ![Dodawanie reguły urządzenia][img-adddevicerule2]

1. <span data-ttu-id="5b766-280">Wybierz **ChangeSetPointTemp** z listy poleceń hello i zestaw **SetPointTemp** too45.</span><span class="sxs-lookup"><span data-stu-id="5b766-280">Select **ChangeSetPointTemp** from hello command list and set **SetPointTemp** too45.</span></span> <span data-ttu-id="5b766-281">Następnie wybierz pozycję **Wyślij polecenie**:</span><span class="sxs-lookup"><span data-stu-id="5b766-281">Then choose **Send Command**:</span></span>

    ![Dodawanie reguły urządzenia][img-adddevicerule3]

1. <span data-ttu-id="5b766-283">Przejdź wstecz toohello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="5b766-283">Navigate back toohello dashboard.</span></span> <span data-ttu-id="5b766-284">Po pewnym czasie, pojawi się nowy wpis w hello **historii Alarm** okienku, gdy temperatury hello zgłoszone przez nowe urządzenie przekracza próg stopnia 47 hello:</span><span class="sxs-lookup"><span data-stu-id="5b766-284">After a short time, you will see a new entry in hello **Alarm History** pane when hello temperature reported by your new device exceeds hello 47-degree threshold:</span></span>

    ![Dodawanie reguły urządzenia][img-adddevicerule4]

1. <span data-ttu-id="5b766-286">Możesz sprawdzić i edytować wszystkie reguły na powitania **reguły** strony pulpitu nawigacyjnego hello:</span><span class="sxs-lookup"><span data-stu-id="5b766-286">You can review and edit all your rules on hello **Rules** page of hello dashboard:</span></span>

    ![Wyświetlanie listy reguł urządzenia][img-rules]

1. <span data-ttu-id="5b766-288">Możesz sprawdzić i edytować wszystkie akcje hello, które można podjąć w regule tooa odpowiedzi na powitania **akcje** strony pulpitu nawigacyjnego hello:</span><span class="sxs-lookup"><span data-stu-id="5b766-288">You can review and edit all hello actions that can be taken in response tooa rule on hello **Actions** page of hello dashboard:</span></span>

    ![Wyświetlanie listy akcji urządzenia][img-actions]

> [!NOTE]
> <span data-ttu-id="5b766-290">Jest możliwe toodefine akcje, które można wysyłać wiadomości e-mail lub SMS w odpowiedzi tooa reguły lub zintegrować z systemu z biznesowych, za pośrednictwem [aplikacji logiki][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="5b766-290">It is possible toodefine actions that can send an email message or SMS in response tooa rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="5b766-291">Aby uzyskać więcej informacji, zobacz hello [tooyour połączyć aplikację logiki Azure IoT pakiet monitorowania zdalnego wstępnie skonfigurowane rozwiązanie][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="5b766-291">For more information, see hello [Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="5b766-292">Zarządzanie filtrami</span><span class="sxs-lookup"><span data-stu-id="5b766-292">Manage filters</span></span>

<span data-ttu-id="5b766-293">Na liście urządzeń hello można utworzyć, Zapisz i ponownie załaduj filtry toodisplay niestandardową listą Centrum tooyour podłączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5b766-293">In hello device list, you can create, save, and reload filters toodisplay a customized list of devices connected tooyour hub.</span></span> <span data-ttu-id="5b766-294">toocreate filtru:</span><span class="sxs-lookup"><span data-stu-id="5b766-294">toocreate a filter:</span></span>

1. <span data-ttu-id="5b766-295">Wybierz ikonę filtra edycji hello powyżej hello listę urządzeń:</span><span class="sxs-lookup"><span data-stu-id="5b766-295">Choose hello edit filter icon above hello list of devices:</span></span>

    ![Otwórz hello edytora filtru][img-editfiltericon]

1. <span data-ttu-id="5b766-297">W hello **edytora filtru**, Dodaj hello pola, operatory i listę urządzeń hello toofilter wartości.</span><span class="sxs-lookup"><span data-stu-id="5b766-297">In hello **Filter editor**, add hello fields, operators, and values toofilter hello device list.</span></span> <span data-ttu-id="5b766-298">Wiele toorefine klauzule można dodać filtru.</span><span class="sxs-lookup"><span data-stu-id="5b766-298">You can add multiple clauses toorefine your filter.</span></span> <span data-ttu-id="5b766-299">Wybierz **filtru** tooapply hello filtru:</span><span class="sxs-lookup"><span data-stu-id="5b766-299">Choose **Filter** tooapply hello filter:</span></span>

    ![Tworzenie filtru][img-filtereditor]

1. <span data-ttu-id="5b766-301">W tym przykładzie listy hello są filtrowane według producenta i numer modelu:</span><span class="sxs-lookup"><span data-stu-id="5b766-301">In this example, hello list is filtered by manufacturer and model number:</span></span>

    ![Filtrowana lista][img-filterelist]

1. <span data-ttu-id="5b766-303">toosave filtru o nazwie niestandardowe, wybierz hello **Zapisz jako** ikona:</span><span class="sxs-lookup"><span data-stu-id="5b766-303">toosave your filter with a custom name, choose hello **Save as** icon:</span></span>

    ![Zapisywanie filtru][img-savefilter]

1. <span data-ttu-id="5b766-305">tooreapply filtr zostały zapisane wcześniej, wybierz hello **Otwórz zapisany filtr** ikona:</span><span class="sxs-lookup"><span data-stu-id="5b766-305">tooreapply a filter you saved previously, choose hello **Open saved filter** icon:</span></span>

    ![Otwieranie filtru][img-openfilter]

<span data-ttu-id="5b766-307">Filtry można tworzyć na postawie identyfikatora urządzenia, stanu urządzenia, żądanych właściwości, zgłaszanych właściwości i tagów.</span><span class="sxs-lookup"><span data-stu-id="5b766-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="5b766-308">Dodać własne urządzenie tooa znaczniki niestandardowe w hello **tagi** sekcji hello **szczegóły urządzenia** panelu lub uruchomić tagi tooupdate zadania na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="5b766-308">You add your own custom tags tooa device in hello **Tags** section of hello **Device Details** panel, or run a job tooupdate tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="5b766-309">W hello **edytora filtru**, można użyć hello **Widok zaawansowanego** tekst zapytania hello tooedit bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="5b766-309">In hello **Filter editor**, you can use hello **Advanced view** tooedit hello query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="5b766-310">Polecenia</span><span class="sxs-lookup"><span data-stu-id="5b766-310">Commands</span></span>

<span data-ttu-id="5b766-311">Z hello **szczegóły urządzenia** panelu, możesz wysłać polecenia toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5b766-311">From hello **Device Details** panel, you can send commands toohello device.</span></span> <span data-ttu-id="5b766-312">Po pierwszym uruchomieniu urządzenia, wysyła się, że informacje o hello polecenia obsługuje toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5b766-312">When a device first starts, it sends information about hello commands it supports toohello solution.</span></span> <span data-ttu-id="5b766-313">Omówienie hello różnice między poleceń i metody, zobacz [opcje chmury do urządzenia Azure IoT Hub][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="5b766-313">For a discussion of hello differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="5b766-314">Wybierz **polecenia** w hello **szczegóły urządzenia** panelu dla wybranego urządzenia hello:</span><span class="sxs-lookup"><span data-stu-id="5b766-314">Choose **Commands** in hello **Device Details** panel for hello selected device:</span></span>

   ![Polecenia urządzenia na pulpicie nawigacyjnym][img-devicecommands]

1. <span data-ttu-id="5b766-316">Wybierz **PingDevice** z hello listę poleceń.</span><span class="sxs-lookup"><span data-stu-id="5b766-316">Select **PingDevice** from hello command list.</span></span>

1. <span data-ttu-id="5b766-317">Wybierz pozycję **Wyślij polecenie**.</span><span class="sxs-lookup"><span data-stu-id="5b766-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="5b766-318">Stan hello hello polecenia w historii poleceń hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="5b766-318">You can see hello status of hello command in hello command history.</span></span>

   ![Stan polecenia na pulpicie nawigacyjnym][img-pingcommand]

<span data-ttu-id="5b766-320">rozwiązanie Hello śledzi stan hello każdego polecenia wysyłane.</span><span class="sxs-lookup"><span data-stu-id="5b766-320">hello solution tracks hello status of each command it sends.</span></span> <span data-ttu-id="5b766-321">Początkowo wynik hello jest **oczekujące**.</span><span class="sxs-lookup"><span data-stu-id="5b766-321">Initially hello result is **Pending**.</span></span> <span data-ttu-id="5b766-322">Gdy urządzenie hello zgłasza, że uruchomione polecenie hello, zbyt zestaw wyników hello**Powodzenie**.</span><span class="sxs-lookup"><span data-stu-id="5b766-322">When hello device reports that it has executed hello command, hello result is set too**Success**.</span></span>

## <a name="behind-hello-scenes"></a><span data-ttu-id="5b766-323">Tle hello</span><span class="sxs-lookup"><span data-stu-id="5b766-323">Behind hello scenes</span></span>

<span data-ttu-id="5b766-324">Podczas wdrażania wstępnie skonfigurowanych rozwiązań procesu wdrażania hello tworzy wiele zasobów w hello subskrypcji platformy Azure, które wybrano.</span><span class="sxs-lookup"><span data-stu-id="5b766-324">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="5b766-325">Te zasoby można wyświetlić w hello Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="5b766-325">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="5b766-326">Utworzenie procesu wdrażania Hello **grupy zasobów** o nazwie na podstawie nazwy hello wybierz wstępnie skonfigurowanego rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="5b766-326">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Wstępnie skonfigurowane rozwiązanie w hello portalu Azure][img-portal]

<span data-ttu-id="5b766-328">Można wyświetlać ustawienia hello każdego zasobu, wybierając ją z listy hello zasobów w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="5b766-328">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="5b766-329">Można również wyświetlić kod źródłowy hello hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="5b766-329">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="5b766-330">Hello zdalnej kontroli kodu źródłowego wstępnie skonfigurowane rozwiązanie jest w hello [azure iot — zdalnego monitorowania] [ lnk-rmgithub] repozytorium GitHub:</span><span class="sxs-lookup"><span data-stu-id="5b766-330">hello remote monitoring preconfigured solution source code is in hello [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="5b766-331">Witaj **DeviceAdministration** folder zawiera kod źródłowy hello hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="5b766-331">hello **DeviceAdministration** folder contains hello source code for hello dashboard.</span></span>
* <span data-ttu-id="5b766-332">Witaj **symulatora** folder zawiera kod źródłowy hello hello symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="5b766-332">hello **Simulator** folder contains hello source code for hello simulated device.</span></span>
* <span data-ttu-id="5b766-333">Witaj **EventProcessor** folder zawiera kod źródłowy hello hello zaplecza procesu, który obsługuje hello przychodzących danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="5b766-333">hello **EventProcessor** folder contains hello source code for hello back-end process that handles hello incoming telemetry.</span></span>

<span data-ttu-id="5b766-334">Gdy wszystko będzie gotowe, możesz usunąć hello wstępnie skonfigurowane rozwiązanie z subskrypcją platformy Azure na powitania [azureiotsuite.com] [ lnk-azureiotsuite] lokacji.</span><span class="sxs-lookup"><span data-stu-id="5b766-334">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="5b766-335">Ta witryna umożliwia delete tooeasily hello wszystkie zasoby, które zostały udostępnione po utworzeniu hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="5b766-335">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="5b766-336">tooensure Usuń wszystkie powiązane toohello wstępnie skonfigurowane rozwiązanie, usuń go na powitania [azureiotsuite.com] [ lnk-azureiotsuite] lokacji i nie usuwaj hello grupy zasobów w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="5b766-336">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site and do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b766-337">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5b766-337">Next Steps</span></span>

<span data-ttu-id="5b766-338">Teraz, po wdrożeniu rozwiązania pracy wstępnie skonfigurowane, można nadal wprowadzenie pakiet IoT odczytując hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="5b766-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="5b766-339">[Przewodnik po wstępnie skonfigurowanym rozwiązaniu monitorowania zdalnego][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="5b766-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="5b766-340">[Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="5b766-340">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="5b766-341">[Uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="5b766-341">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md