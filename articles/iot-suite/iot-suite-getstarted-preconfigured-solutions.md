---
title: "Wprowadzenie do wstępnie skonfigurowanych rozwiązań | Microsoft Docs"
description: "Wykonaj czynności opisane w tym samouczku, aby dowiedzieć się, jak wdrożyć wstępnie skonfigurowane rozwiązanie Pakiet IoT Azure."
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
ms.openlocfilehash: 466825ab78a5ac9773d8beff69cca90ff9db6c01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-preconfigured-solutions"></a><span data-ttu-id="f7583-103">Wprowadzenie do wstępnie skonfigurowanych rozwiązań</span><span class="sxs-lookup"><span data-stu-id="f7583-103">Get started with the preconfigured solutions</span></span>

<span data-ttu-id="f7583-104">[Wstępnie skonfigurowane rozwiązania][lnk-preconfigured-solutions] Pakietu IoT Azure obejmują wiele usług Azure IoT, co pozwala dostarczać kompleksowe rozwiązania, które umożliwiają implementowanie typowych scenariuszy biznesowych IoT.</span><span class="sxs-lookup"><span data-stu-id="f7583-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="f7583-105">Wstępnie skonfigurowane rozwiązanie do *monitorowania zdalnego* łączy i monitoruje urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7583-105">The *remote monitoring* preconfigured solution connects to and monitors your devices.</span></span> <span data-ttu-id="f7583-106">Rozwiązanie to umożliwia analizowanie strumienia danych z urządzeń oraz poprawianie wyników biznesowych dzięki zautomatyzowaniu odpowiedzi procesów na ten strumień danych.</span><span class="sxs-lookup"><span data-stu-id="f7583-106">You can use the solution to analyze the stream of data from your devices and to improve business outcomes by making processes respond automatically to that stream of data.</span></span>

<span data-ttu-id="f7583-107">W tym samouczku przedstawiono sposób aprowizowania wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="f7583-107">This tutorial shows you how to provision the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="f7583-108">Dostępny jest również opis podstawowych funkcji wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7583-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="f7583-109">Dostęp do wielu z tych funkcji można uzyskać z *pulpitu nawigacyjnego* rozwiązania, który jest wdrażany jako część wstępnie skonfigurowanego rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="f7583-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][img-dashboard]

<span data-ttu-id="f7583-111">Do wykonania kroków tego samouczka jest potrzebna aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f7583-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="f7583-112">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f7583-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f7583-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="f7583-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="f7583-114">Omówienie scenariusza</span><span class="sxs-lookup"><span data-stu-id="f7583-114">Scenario overview</span></span>

<span data-ttu-id="f7583-115">Podczas wdrażania wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego jest ono wstępnie wypełniane zasobami, które umożliwiają wykonanie kroków opisanych w typowym scenariuszu zdalnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="f7583-115">When you deploy the remote monitoring preconfigured solution, it is prepopulated with resources that enable you to step through a common remote monitoring scenario.</span></span> <span data-ttu-id="f7583-116">W tym scenariuszu kilka urządzeń podłączonych do rozwiązania zgłasza nieoczekiwane wartości temperatury.</span><span class="sxs-lookup"><span data-stu-id="f7583-116">In this scenario, several devices connected to the solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="f7583-117">W poniższych sekcjach opisano sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f7583-117">The following sections show you how to:</span></span>

* <span data-ttu-id="f7583-118">Określenie urządzeń wysyłających nieoczekiwane wartości temperatury.</span><span class="sxs-lookup"><span data-stu-id="f7583-118">Identify the devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="f7583-119">Skonfigurowanie tych urządzeń do wysłania bardziej szczegółowych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="f7583-119">Configure these devices to send more detailed telemetry.</span></span>
* <span data-ttu-id="f7583-120">Rozwiązanie problemu przez aktualizację oprogramowania układowego na tych urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="f7583-120">Fix the problem by updating the firmware on these devices.</span></span>
* <span data-ttu-id="f7583-121">Sprawdzenie, czy podjęte akcje spowodowały rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="f7583-121">Verify that your action has resolved the issue.</span></span>

<span data-ttu-id="f7583-122">Kluczową cechą tego scenariusza jest to, że te wszystkie akcje można wykonać zdalnie z poziomu pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7583-122">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="f7583-123">Nie jest konieczny fizyczny dostęp do urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f7583-123">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="f7583-124">Wyświetlanie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="f7583-124">View the solution dashboard</span></span>

<span data-ttu-id="f7583-125">Pulpit nawigacyjny pozwala zarządzać wdrożonym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="f7583-125">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="f7583-126">Można na przykład wyświetlać dane telemetryczne, dodawać urządzenia i konfigurować reguły.</span><span class="sxs-lookup"><span data-stu-id="f7583-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="f7583-127">Jeśli aprowizacja została ukończona, a na kafelku wstępnie skonfigurowanego rozwiązania jest wyświetlany stan **Gotowe**, wybierz pozycję **Uruchom**, aby otworzyć portal rozwiązania do monitorowania zdalnego na nowej karcie.</span><span class="sxs-lookup"><span data-stu-id="f7583-127">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Uruchamianie wstępnie skonfigurowanego rozwiązania][img-launch-solution]

1. <span data-ttu-id="f7583-129">Domyślnie w portalu rozwiązania jest wyświetlany *pulpit nawigacyjny*.</span><span class="sxs-lookup"><span data-stu-id="f7583-129">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="f7583-130">Korzystając z menu po lewej stronie, można przejść do innych obszarów portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7583-130">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Pulpit nawigacyjny wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego][img-menu]

<span data-ttu-id="f7583-132">Pulpit nawigacyjny udostępnia następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="f7583-132">The dashboard displays the following information:</span></span>

* <span data-ttu-id="f7583-133">Mapę zawierającą lokalizację każdego urządzenia połączonego z rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="f7583-133">A map that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="f7583-134">Przy pierwszym uruchomieniu rozwiązania dostępnych jest 25 symulowanych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f7583-134">When you first run the solution, there are 25 simulated devices.</span></span> <span data-ttu-id="f7583-135">Są one implementowane jako zadania WebJob Azure, a wykreślanie informacji na mapie odbywa się za pomocą interfejsu API Map Bing.</span><span class="sxs-lookup"><span data-stu-id="f7583-135">The simulated devices are implemented as Azure WebJobs, and the solution uses the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="f7583-136">Zobacz [Często zadawane pytania][lnk-faq], aby dowiedzieć się, jak utworzyć dynamiczną mapę.</span><span class="sxs-lookup"><span data-stu-id="f7583-136">See the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="f7583-137">Panel **Historia telemetrii**, na którym są wyświetlane niemal w czasie rzeczywistym dane telemetryczne dotyczące wilgotności i temperatury pochodzące z wybranego urządzenia oraz dane zagregowane, takie jak wilgotność maksymalna, minimalna i średnia.</span><span class="sxs-lookup"><span data-stu-id="f7583-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="f7583-138">Panel **Historia alarmów**, na którym są wyświetlane ostatnie zdarzenia alarmów generowane w przypadku przekroczenia progu przez wartość telemetryczną.</span><span class="sxs-lookup"><span data-stu-id="f7583-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="f7583-139">Wstępnie skonfigurowane rozwiązanie zawiera przykładowe alarmy, ale można też definiować własne.</span><span class="sxs-lookup"><span data-stu-id="f7583-139">You can define your own alarms in addition to the examples created by the preconfigured solution.</span></span>
* <span data-ttu-id="f7583-140">Panel **Zadania**, na którym są wyświetlane informacje o zaplanowanych zadaniach.</span><span class="sxs-lookup"><span data-stu-id="f7583-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="f7583-141">Własne zadania można zaplanować na stronie **Zadania zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="f7583-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="f7583-142">Wyświetlanie alarmów</span><span class="sxs-lookup"><span data-stu-id="f7583-142">View alarms</span></span>

<span data-ttu-id="f7583-143">Na panelu Historia alarmów widać, że pięć urządzeń zgłasza wyższe niż oczekiwano wartości telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="f7583-143">The alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![DO ZROBIENIA Historia alarmów na pulpicie nawigacyjnym rozwiązania][img-alarms]

> [!NOTE]
> <span data-ttu-id="f7583-145">Te alarmy są generowane przez regułę dołączoną do wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7583-145">These alarms are generated by a rule that is included in the preconfigured solution.</span></span> <span data-ttu-id="f7583-146">Ta reguła generuje alert, gdy wartość temperatury wysyłana przez urządzenie przekracza 60.</span><span class="sxs-lookup"><span data-stu-id="f7583-146">This rule generates an alert when the temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="f7583-147">Można zdefiniować własne reguły i akcje, wybierając pozycje [Reguły](#add-a-rule) i [Akcje](#add-an-action) w menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="f7583-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in the left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="f7583-148">Wyświetlanie urządzeń</span><span class="sxs-lookup"><span data-stu-id="f7583-148">View devices</span></span>

<span data-ttu-id="f7583-149">*Lista urządzeń* zawiera wszystkie zarejestrowane urządzenia należące do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7583-149">The *devices* list shows all the registered devices in the solution.</span></span> <span data-ttu-id="f7583-150">Korzystając z listy urządzeń, można wyświetlać i edytować metadane urządzeń, dodawać lub usuwać urządzenia i wywoływać metody na urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="f7583-150">From the device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="f7583-151">Urządzenia znajdujące się na liście można filtrować i sortować.</span><span class="sxs-lookup"><span data-stu-id="f7583-151">You can filter and sort the list of devices in the device list.</span></span> <span data-ttu-id="f7583-152">Na liście urządzeń można również dostosować kolumny.</span><span class="sxs-lookup"><span data-stu-id="f7583-152">You can also customize the columns shown in the device list.</span></span>

1. <span data-ttu-id="f7583-153">Wybierz pozycję **Urządzenia**, aby wyświetlić listę urządzeń dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7583-153">Choose **Devices** to show the device list for this solution.</span></span>

   ![Widok listy urządzeń w portalu rozwiązania][img-devicelist]

1. <span data-ttu-id="f7583-155">Na liście początkowo jest widocznych 25 symulowanych urządzeń utworzonych w procesie aprowizacji.</span><span class="sxs-lookup"><span data-stu-id="f7583-155">The device list initially shows 25 simulated devices created by the provisioning process.</span></span> <span data-ttu-id="f7583-156">Do rozwiązania można dodać dodatkowe symulowane i fizyczne urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7583-156">You can add additional simulated and physical devices to the solution.</span></span>

1. <span data-ttu-id="f7583-157">Aby wyświetlić szczegóły dotyczące urządzenia, wybierz odpowiednią pozycję z listy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f7583-157">To view the details of a device, choose a device in the device list.</span></span>

   ![Widok szczegółów dotyczących urządzenia w portalu rozwiązania][img-devicedetails]

<span data-ttu-id="f7583-159">Panel **Szczegóły urządzenia** zawiera sześć sekcji:</span><span class="sxs-lookup"><span data-stu-id="f7583-159">The **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="f7583-160">Kolekcja linków umożliwiająca dostosowanie ikony urządzenia, wyłączenie urządzenia, dodanie reguły, wywołanie metody lub wysłanie polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7583-160">A collection of links that enable you to customize the device icon, disable the device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="f7583-161">Porównanie poleceń (komunikatów wysyłanych z urządzenia do chmury) i metod (metod bezpośrednich) znajduje się w temacie [Wskazówki dotyczące komunikacji z chmury do urządzenia][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="f7583-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="f7583-162">Sekcja **Bliźniacza reprezentacja urządzenia — Tagi** umożliwia edytowanie wartości tagów dla urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7583-162">The **Device Twin - Tags** section enables you to edit tag values for the device.</span></span> <span data-ttu-id="f7583-163">Wartości tagów można wyświetlać na liście urządzeń i używać ich do filtrowania tej listy.</span><span class="sxs-lookup"><span data-stu-id="f7583-163">You can display tag values in the device list and use tag values to filter the device list.</span></span>
* <span data-ttu-id="f7583-164">Sekcja **Bliźniacza reprezentacja urządzenia —Żądane właściwości** umożliwia ustawianie wartości właściwości wysyłanych do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7583-164">The **Device Twin - Desired Properties** section enables you to set property values to be sent to the device.</span></span>
* <span data-ttu-id="f7583-165">Sekcja **Bliźniacza reprezentacja urządzenia — Zgłaszane właściwości** umożliwia wyświetlanie wartości właściwości wysyłanych z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7583-165">The **Device Twin - Reported Properties** section shows property values sent from the device.</span></span>
* <span data-ttu-id="f7583-166">Sekcja **Właściwości urządzenia** zawiera informacje z rejestru tożsamości, takie jak identyfikator urządzenia i klucze uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="f7583-166">The **Device Properties** section shows information from the identity registry such as the device id and authentication keys.</span></span>
* <span data-ttu-id="f7583-167">Sekcja **Ostatnie zadania** zawiera informacje o wszystkich zadaniach, które były ukierunkowane na to urządzenie.</span><span class="sxs-lookup"><span data-stu-id="f7583-167">The **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-the-device-list"></a><span data-ttu-id="f7583-168">Filtrowanie listy urządzeń</span><span class="sxs-lookup"><span data-stu-id="f7583-168">Filter the device list</span></span>

<span data-ttu-id="f7583-169">Aby wyświetlić tylko te urządzenia, które wysyłają nieoczekiwane wartości temperatury, można użyć filtru.</span><span class="sxs-lookup"><span data-stu-id="f7583-169">You can use a filter to display only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="f7583-170">Wstępnie skonfigurowane rozwiązania do zdalnego monitorowania zawiera filtr **Urządzenia w niedobrej kondycji**, który umożliwia wyświetlenie urządzeń mających wartość średniej temperatury większą niż 60.</span><span class="sxs-lookup"><span data-stu-id="f7583-170">The remote monitoring preconfigured solution includes the **Unhealthy devices** filter to show devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="f7583-171">Możesz również [utworzyć własne filtry](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="f7583-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="f7583-172">Wybierz pozycję **Otwórz zapisany filtr**, aby wyświetlić listę dostępnych filtrów.</span><span class="sxs-lookup"><span data-stu-id="f7583-172">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="f7583-173">Następnie wybierz pozycję **Urządzenia w niedobrej kondycji**, aby zastosować filtr:</span><span class="sxs-lookup"><span data-stu-id="f7583-173">Then choose **Unhealthy devices** to apply the filter:</span></span>

    ![Wyświetlanie listy filtrów][img-unhealthy-filter]

1. <span data-ttu-id="f7583-175">Na liście urządzeń są teraz pokazywane tylko urządzenia z wartością średniej temperatury większą niż 60.</span><span class="sxs-lookup"><span data-stu-id="f7583-175">The device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Widok filtrowanej listy urządzeń przedstawiający urządzenia w niedobrej kondycji][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="f7583-177">Aktualizowanie żądanych właściwości</span><span class="sxs-lookup"><span data-stu-id="f7583-177">Update desired properties</span></span>

<span data-ttu-id="f7583-178">Na tym etapie zidentyfikowano zestaw urządzeń, które mogą wymagać naprawy.</span><span class="sxs-lookup"><span data-stu-id="f7583-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="f7583-179">Wygląda jednak na to, że 15-sekundowa częstotliwość próbkowania danych jest niewystarczająca, aby jednoznacznie określić przyczynę problemu.</span><span class="sxs-lookup"><span data-stu-id="f7583-179">However, you decide that the data frequency of 15 seconds is not sufficient for a clear diagnosis of the issue.</span></span> <span data-ttu-id="f7583-180">Częstotliwość próbkowania danych telemetrycznych zostanie więc zmieniona na pięć sekund, co zapewni więcej punktów danych w celu lepszego zdiagnozowania problemu.</span><span class="sxs-lookup"><span data-stu-id="f7583-180">Changing the telemetry frequency to five seconds to provide you with more data points to better diagnose the issue.</span></span> <span data-ttu-id="f7583-181">Tę zmianę konfiguracji można wypchnąć do urządzeń zdalnych za pośrednictwem portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7583-181">You can push this configuration change to your remote devices from the solution portal.</span></span> <span data-ttu-id="f7583-182">Można wprowadzić jednorazową zmianę, ocenić jej skutki, a następnie podjąć odpowiednie działania zgodnie z otrzymanymi wynikami.</span><span class="sxs-lookup"><span data-stu-id="f7583-182">You can make the change once, evaluate the impact, and then act on the results.</span></span>

<span data-ttu-id="f7583-183">Wykonaj następujące kroki, aby uruchomić zadanie zmieniające żądaną właściwość **TelemetryInterval** dla uwzględnionych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f7583-183">Follow these steps to run a job that changes the **TelemetryInterval** desired property for the affected devices.</span></span> <span data-ttu-id="f7583-184">Po otrzymaniu przez urządzenia nowej wartości właściwości **TelemetryInterval** zmieniają one swoją konfigurację i zaczynają wysyłać dane telemetryczne co pięć sekund zamiast co 15 sekund:</span><span class="sxs-lookup"><span data-stu-id="f7583-184">When the devices receive the new **TelemetryInterval** property value, they change their configuration to send telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="f7583-185">Podczas wyświetlania na liście urządzeń w niedobrej kondycji wybierz pozycję **Harmonogram zadań**, a następnie pozycję **Edytuj bliźniaczą reprezentację urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="f7583-185">While you are showing the list of unhealthy devices in the device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="f7583-186">Wywołaj zadanie **Zmiana interwału telemetrii**.</span><span class="sxs-lookup"><span data-stu-id="f7583-186">Call the job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="f7583-187">Zmień wartość **żądanej właściwości** o nazwie **desired.Config.TelemetryInterval** na pięć sekund.</span><span class="sxs-lookup"><span data-stu-id="f7583-187">Change the value of the **Desired Property** name **desired.Config.TelemetryInterval** to five seconds.</span></span>

1. <span data-ttu-id="f7583-188">Wybierz pozycję **Zaplanuj**.</span><span class="sxs-lookup"><span data-stu-id="f7583-188">Choose **Schedule**.</span></span>

    ![Zmiana wartości właściwości TelemetryInterval na pięć sekund][img-change-interval]

1. <span data-ttu-id="f7583-190">Postęp zadania można monitorować na stronie **Zadania zarządzania** w portalu.</span><span class="sxs-lookup"><span data-stu-id="f7583-190">You can monitor the progress of the job on the **Management Jobs** page in the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="f7583-191">Jeśli chcesz zmienić wartość żądanej właściwości dla konkretnego urządzenia, użyj sekcji **Żądane właściwości** na panelu **Szczegóły urządzenia**, zamiast uruchamiać zadanie.</span><span class="sxs-lookup"><span data-stu-id="f7583-191">If you want to change a desired property value for an individual device, use the **Desired Properties** section in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="f7583-192">To zadanie ustawia wartość żądanej właściwości **TelemetryInterval** w bliźniaczej reprezentacji urządzenia dla wszystkich urządzeń wybranych za pomocą filtru.</span><span class="sxs-lookup"><span data-stu-id="f7583-192">This job sets the value of the **TelemetryInterval** desired property in the device twin for all the devices selected by the filter.</span></span> <span data-ttu-id="f7583-193">Urządzenia pobierają tę wartość z bliźniaczej reprezentacji urządzenia i aktualizują swoje zachowanie.</span><span class="sxs-lookup"><span data-stu-id="f7583-193">The devices retrieve this value from the device twin and update their behavior.</span></span> <span data-ttu-id="f7583-194">Kiedy urządzenie pobiera i przetwarza żądaną właściwość z bliźniaczej reprezentacji urządzenia, ustawia odpowiednią wartość zgłoszonej właściwości.</span><span class="sxs-lookup"><span data-stu-id="f7583-194">When a device retrieves and processes a desired property from a device twin, it sets the corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="f7583-195">Wywoływanie metod</span><span class="sxs-lookup"><span data-stu-id="f7583-195">Invoke methods</span></span>

<span data-ttu-id="f7583-196">Podczas wykonywania zadania na liście urządzeń w niedobrej kondycji można zauważyć, że wszystkie te urządzenia mają starą (wcześniejszą niż 1.6) wersję oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="f7583-196">While the job runs, you notice in the list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Wyświetlanie zgłaszanej wersji oprogramowania układowego urządzeń w niedobrej kondycji][img-old-firmware]

<span data-ttu-id="f7583-198">Ta wersja oprogramowania układowego może być podstawową przyczyną występowania nieoczekiwanych wartości temperatury, ponieważ wiadomo, że inne urządzenia w dobrej kondycji zostały ostatnio zaktualizowane do wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="f7583-198">This firmware version may be the root cause of the unexpected temperature values because you know that other healthy devices were recently updated to version 2.0.</span></span> <span data-ttu-id="f7583-199">W celu zidentyfikowania wszystkich urządzeń ze starymi wersjami oprogramowania układowego można użyć wbudowanego filtru **Urządzenia ze starym oprogramowaniem układowym**.</span><span class="sxs-lookup"><span data-stu-id="f7583-199">You can use the built-in **Old firmware devices** filter to identify any devices with old firmware versions.</span></span> <span data-ttu-id="f7583-200">Z poziomu portalu można następnie zdalnie zaktualizować wszystkie urządzenia działające nadal pod kontrolą starych wersji oprogramowania układowego:</span><span class="sxs-lookup"><span data-stu-id="f7583-200">From the portal, you can then remotely update all the devices still running old firmware versions:</span></span>

1. <span data-ttu-id="f7583-201">Wybierz pozycję **Otwórz zapisany filtr**, aby wyświetlić listę dostępnych filtrów.</span><span class="sxs-lookup"><span data-stu-id="f7583-201">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="f7583-202">Następnie wybierz pozycję **Urządzenia ze starym oprogramowaniem układowym**, aby zastosować filtr:</span><span class="sxs-lookup"><span data-stu-id="f7583-202">Then choose **Old firmware devices** to apply the filter:</span></span>

    ![Wyświetlanie listy filtrów][img-old-filter]

1. <span data-ttu-id="f7583-204">Na liście urządzeń są teraz wyświetlane tylko urządzenia ze starymi wersjami oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="f7583-204">The device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="f7583-205">Na liście znajduje się pięć urządzeń zidentyfikowanych przez filtr **Urządzenia w niedobrej kondycji** i trzy dodatkowe urządzenia:</span><span class="sxs-lookup"><span data-stu-id="f7583-205">This list includes the five devices identified by the **Unhealthy devices** filter and three additional devices:</span></span>

    ![Widok filtrowanej listy urządzeń przedstawiający stare urządzenia][img-filtered-old-list]

1. <span data-ttu-id="f7583-207">Wybierz pozycję **Harmonogram zadań**, a następnie pozycję **Wywołaj metodę**.</span><span class="sxs-lookup"><span data-stu-id="f7583-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="f7583-208">W polu **Nazwa zadania** wpisz **Aktualizacja oprogramowania układowego do wersji 2.0**.</span><span class="sxs-lookup"><span data-stu-id="f7583-208">Set **Job Name** to **Firmware update to version 2.0**.</span></span>

1. <span data-ttu-id="f7583-209">W polu **Metoda** wybierz pozycję **InitiateFirmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="f7583-209">Choose **InitiateFirmwareUpdate** as the **Method**.</span></span>

1. <span data-ttu-id="f7583-210">Ustaw parametr **FwPackageUri** na wartość **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="f7583-210">Set the **FwPackageUri** parameter to **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="f7583-211">Wybierz pozycję **Zaplanuj**.</span><span class="sxs-lookup"><span data-stu-id="f7583-211">Choose **Schedule**.</span></span> <span data-ttu-id="f7583-212">Domyślnie zadanie zostanie uruchomione natychmiast.</span><span class="sxs-lookup"><span data-stu-id="f7583-212">The default is for the job to run now.</span></span>

    ![Tworzenie zadania aktualizacji oprogramowania układowego wybranych urządzeń][img-method-update]

> [!NOTE]
> <span data-ttu-id="f7583-214">Aby wywołać metodę dla konkretnego urządzenia, należy wybrać pozycję **Metody** na panelu **Szczegóły urządzenia**, zamiast uruchamiać zadanie.</span><span class="sxs-lookup"><span data-stu-id="f7583-214">If you want to invoke a method on an individual device, choose **Methods** in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="f7583-215">To zadanie wywołuje metodę bezpośrednią **InitiateFirmwareUpdate** na wszystkich urządzeniach wybranych za pomocą filtru.</span><span class="sxs-lookup"><span data-stu-id="f7583-215">This job invokes the **InitiateFirmwareUpdate** direct method on all the devices selected by the filter.</span></span> <span data-ttu-id="f7583-216">Urządzenia odpowiadają natychmiast do usługi IoT Hub, a następnie asynchronicznie inicjują proces aktualizacji oprogramowania układowego.</span><span class="sxs-lookup"><span data-stu-id="f7583-216">Devices respond immediately to IoT Hub and then initiate the firmware update process asynchronously.</span></span> <span data-ttu-id="f7583-217">Urządzenia dostarczają informacje o stanie procesu aktualizacji oprogramowania układowego za pomocą wartości zgłaszanych właściwości, jak pokazano w poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="f7583-217">The devices provide status information about the firmware update process through reported property values, as shown in the following screenshots.</span></span> <span data-ttu-id="f7583-218">Wybierz ikonę **Odśwież**, aby zaktualizować informacje na liście urządzeń i zadań:</span><span class="sxs-lookup"><span data-stu-id="f7583-218">Choose the **Refresh** icon to update the information in the device and job lists:</span></span>

<span data-ttu-id="f7583-219">![Lista zadań z widoczną listą aktualizacji oprogramowania układowego w stanie uruchomionym][img-update-1]
![Lista urządzeń przedstawiająca stan aktualizacji oprogramowania układowego][img-update-2]
![Lista zadań z widoczną listą aktualizacji oprogramowania układowego w stanie ukończonym][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="f7583-219">![Job list showing the firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing the firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="f7583-220">W środowisku produkcyjnym można zaplanować, aby zadania były uruchamiane w wyznaczonym oknie obsługi.</span><span class="sxs-lookup"><span data-stu-id="f7583-220">In a production environment, you can schedule jobs to run during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="f7583-221">Przegląd scenariusza</span><span class="sxs-lookup"><span data-stu-id="f7583-221">Scenario review</span></span>

<span data-ttu-id="f7583-222">W tym scenariuszu za pomocą historii alarmów na pulpicie nawigacyjnym oraz filtru zidentyfikowano potencjalny problem występujący na niektórych urządzeniach zdalnych.</span><span class="sxs-lookup"><span data-stu-id="f7583-222">In this scenario, you identified a potential issue with some of your remote devices using the alarm history on the dashboard and a filter.</span></span> <span data-ttu-id="f7583-223">Następnie za pomocą filtru oraz zadania skonfigurowano zdalnie urządzenia, aby uzyskać większą ilość informacji ułatwiających zdiagnozowanie problemu.</span><span class="sxs-lookup"><span data-stu-id="f7583-223">You then used the filter and a job to remotely configure the devices to provide more information to help diagnose the issue.</span></span> <span data-ttu-id="f7583-224">Na koniec użyto filtru i zadania w celu zaplanowania obsługi kwalifikujących się urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f7583-224">Finally, you used a filter and a job to schedule maintenance on the affected devices.</span></span> <span data-ttu-id="f7583-225">Po powrocie do pulpitu nawigacyjnego można sprawdzić, czy nie nadchodzą już żadne alarmy z urządzeń w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="f7583-225">If you return to the dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="f7583-226">Korzystając z filtru, można się upewnić, czy oprogramowanie układowe jest aktualne na wszystkich urządzeniach w rozwiązaniu oraz czy nie ma żadnych urządzeń w niedobrej kondycji:</span><span class="sxs-lookup"><span data-stu-id="f7583-226">You can use a filter to verify that the firmware is up-to-date on all the devices in your solution and that there are no more unhealthy devices:</span></span>

![Filtr przedstawiający, że wszystkie urządzenia mają aktualne oprogramowanie układowe][img-updated]

![Filtr przedstawiający, że wszystkie urządzenia są w dobrej kondycji][img-healthy]

## <a name="other-features"></a><span data-ttu-id="f7583-229">Pozostałe funkcje</span><span class="sxs-lookup"><span data-stu-id="f7583-229">Other features</span></span>

<span data-ttu-id="f7583-230">W poniższych sekcjach opisano niektóre dodatkowe funkcje wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego, które nie zostały opisane w poprzednim scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="f7583-230">The following sections describe some additional features of the remote monitoring preconfigured solution that are not described as part of the previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="f7583-231">Dostosowywanie kolumn</span><span class="sxs-lookup"><span data-stu-id="f7583-231">Customize columns</span></span>

<span data-ttu-id="f7583-232">Informacje wyświetlane na liście urządzeń można dostosowywać. W tym celu należy wybrać pozycję **Edytor kolumn**.</span><span class="sxs-lookup"><span data-stu-id="f7583-232">You can customize the information shown in the device list by choosing **Column editor**.</span></span> <span data-ttu-id="f7583-233">Istnieje możliwość dodawania i usuwania kolumn, w których są wyświetlane zgłaszane wartości właściwości i tagów.</span><span class="sxs-lookup"><span data-stu-id="f7583-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="f7583-234">Można również zmieniać kolejność kolumn i ich nazwy:</span><span class="sxs-lookup"><span data-stu-id="f7583-234">You can also reorder and rename columns:</span></span>

   ![Przycisk Edytor kolumn na liście urządzeń][img-columneditor]

### <a name="customize-the-device-icon"></a><span data-ttu-id="f7583-236">Dostosowywanie ikony urządzenia</span><span class="sxs-lookup"><span data-stu-id="f7583-236">Customize the device icon</span></span>

<span data-ttu-id="f7583-237">Ikonę urządzenia wyświetlaną na liście urządzeń można dostosować na panelu **Szczegóły urządzenia** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f7583-237">You can customize the device icon displayed in the device list from the **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="f7583-238">Wybierz ikonę ołówka, aby otworzyć panel **Edytowanie obrazu** dla urządzenia:</span><span class="sxs-lookup"><span data-stu-id="f7583-238">Choose the pencil icon to open the **Edit image** panel for a device:</span></span>

   ![Otwieranie edytora obrazu dla urządzenia][img-startimageedit]

1. <span data-ttu-id="f7583-240">Przekaż nowy obraz lub użyj jednego z istniejących obrazów, a następnie wybierz przycisk **Zapisz**:</span><span class="sxs-lookup"><span data-stu-id="f7583-240">Either upload a new image or use one of the existing images and then choose **Save**:</span></span>

   ![Edytowanie edytora obrazu dla urządzenia][img-imageedit]

1. <span data-ttu-id="f7583-242">Wybrany obraz jest teraz wyświetlany w kolumnie **Ikona** dla urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7583-242">The image you selected now displays in the **Icon** column for the device.</span></span>

> [!NOTE]
> <span data-ttu-id="f7583-243">Obraz jest przechowywany w usłudze Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f7583-243">The image is stored in blob storage.</span></span> <span data-ttu-id="f7583-244">Tag w bliźniaczej reprezentacji urządzenia zawiera link do obrazu w usłudze Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f7583-244">A tag in the device twin contains a link to the image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="f7583-245">Dodawanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="f7583-245">Add a device</span></span>

<span data-ttu-id="f7583-246">Podczas wdrażania wstępnie skonfigurowanego rozwiązania automatycznie aprowizujesz 25 przykładowych urządzeń widocznych na liście urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f7583-246">When you deploy the preconfigured solution, you automatically provision 25 sample devices that you can see in the device list.</span></span> <span data-ttu-id="f7583-247">Są to *symulowane urządzenia* uruchamiane w zadaniu WebJob Azure.</span><span class="sxs-lookup"><span data-stu-id="f7583-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="f7583-248">Symulowane urządzenia ułatwiają eksperymentowanie ze wstępnie skonfigurowanym rozwiązaniem bez konieczności wdrażania prawdziwych urządzeń fizycznych.</span><span class="sxs-lookup"><span data-stu-id="f7583-248">Simulated devices make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical devices.</span></span> <span data-ttu-id="f7583-249">Jeśli chcesz połączyć prawdziwe urządzenie z rozwiązaniem, zobacz samouczek [Łączenie urządzenia ze wstępnie skonfigurowanym rozwiązaniem do monitorowania zdalnego][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="f7583-249">If you do want to connect a real device to the solution, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="f7583-250">Poniższe kroki pokazują, jak dodać symulowane urządzenie do rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="f7583-250">The following steps show you how to add a simulated device to the solution:</span></span>

1. <span data-ttu-id="f7583-251">Wróć do listy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f7583-251">Navigate back to the device list.</span></span>

1. <span data-ttu-id="f7583-252">Aby dodać urządzenie, wybierz pozycję **+ Dodaj urządzenie** w lewym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="f7583-252">To add a device, choose **+ Add A Device** in the bottom left corner.</span></span>

   ![Dodawanie urządzenia do wstępnie skonfigurowanego rozwiązania][img-adddevice]

1. <span data-ttu-id="f7583-254">Wybierz pozycję **Dodaj nowe** na kafelku **Symulowane urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="f7583-254">Choose **Add New** on the **Simulated Device** tile.</span></span>

   ![Określanie szczegółów nowego urządzenia na pulpicie nawigacyjnym][img-addnew]

   <span data-ttu-id="f7583-256">Oprócz tworzenia nowych symulowanych urządzeń można również dodawać urządzenia fizyczne — wystarczy wybrać opcję utworzenia **niestandardowego urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="f7583-256">In addition to creating a new simulated device, you can also add a physical device if you choose to create a **Custom Device**.</span></span> <span data-ttu-id="f7583-257">Aby dowiedzieć się więcej na temat łączenia fizycznych urządzeń z rozwiązaniem, zobacz artykuł [Łączenie urządzenia ze wstępnie skonfigurowanym rozwiązaniem Pakietu IoT służącym do monitorowania zdalnego][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="f7583-257">To learn more about connecting physical devices to the solution, see [Connect your device to the IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="f7583-258">Wybierz pozycję **Pozwól mi zdefiniować własny identyfikator urządzenia** i wprowadź unikatowy identyfikator urządzenia, np. **moje_urzadzenie_01**.</span><span class="sxs-lookup"><span data-stu-id="f7583-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="f7583-259">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f7583-259">Choose **Create**.</span></span>

   ![Zapisywanie nowego urządzenia][img-definedevice]

1. <span data-ttu-id="f7583-261">W kroku 3 procedury **Dodawanie symulowanego urządzenia** wybierz pozycję **Gotowe**, aby powrócić do listy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f7583-261">In step 3 of **Add a simulated device**, choose **Done** to return to the device list.</span></span>

1. <span data-ttu-id="f7583-262">Na liście urządzeń widać, że stan urządzenia ma wartość **Uruchomione**.</span><span class="sxs-lookup"><span data-stu-id="f7583-262">You can view your device **Running** in the device list.</span></span>

    ![Wyświetlanie nowego urządzenia na liście urządzeń][img-runningnew]

1. <span data-ttu-id="f7583-264">Na pulpicie nawigacyjnym można również wyświetlić symulowane dane telemetryczne pochodzące z nowego urządzenia:</span><span class="sxs-lookup"><span data-stu-id="f7583-264">You can also view the simulated telemetry from your new device on the dashboard:</span></span>

    ![Wyświetlanie telemetrii z nowego urządzenia][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="f7583-266">Wyłączanie i usuwanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="f7583-266">Disable and delete a device</span></span>

<span data-ttu-id="f7583-267">Można wyłączyć urządzenie, a następnie je usunąć:</span><span class="sxs-lookup"><span data-stu-id="f7583-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Wyłączanie i usuwanie urządzenia][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="f7583-269">Dodawanie reguły</span><span class="sxs-lookup"><span data-stu-id="f7583-269">Add a rule</span></span>

<span data-ttu-id="f7583-270">Dla nowo dodanego urządzenia nie zostały określone żadne reguły.</span><span class="sxs-lookup"><span data-stu-id="f7583-270">There are no rules for the new device you just added.</span></span> <span data-ttu-id="f7583-271">W tej sekcji dodasz regułę, która powoduje uruchomienie alarmu, gdy temperatura zgłoszona przez nowe urządzenie przekroczy 47 stopni.</span><span class="sxs-lookup"><span data-stu-id="f7583-271">In this section, you add a rule that triggers an alarm when the temperature reported by the new device exceeds 47 degrees.</span></span> <span data-ttu-id="f7583-272">Przed wykonaniem poniższych instrukcji zwróć uwagę na to, że zgodnie z historią telemetrii dla nowego urządzenia dostępną na pulpicie nawigacyjnym temperatura urządzenie nigdy nie przekracza 45 stopni.</span><span class="sxs-lookup"><span data-stu-id="f7583-272">Before you start, notice that the telemetry history for the new device on the dashboard shows the device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="f7583-273">Wróć do listy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f7583-273">Navigate back to the device list.</span></span>

1. <span data-ttu-id="f7583-274">Aby dodać regułę dla urządzenia, wybierz nowe urządzenie na **liście urządzeń**, a następnie wybierz pozycję **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="f7583-274">To add a rule for the device, select your new device in the **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="f7583-275">Utwórz regułę, w której jest używane pole danych **Temperatura** i która generuje dane wyjściowe **AlarmTemp**, gdy temperatura przekroczy 47 stopni:</span><span class="sxs-lookup"><span data-stu-id="f7583-275">Create a rule that uses **Temperature** as the data field and uses **AlarmTemp** as the output when the temperature exceeds 47 degrees:</span></span>

    ![Dodawanie reguły urządzenia][img-adddevicerule]

1. <span data-ttu-id="f7583-277">Aby zapisać zmiany, wybierz pozycję **Zapisz i wyświetl reguły**.</span><span class="sxs-lookup"><span data-stu-id="f7583-277">To save your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="f7583-278">Wybierz pozycję **Polecenia** w okienku szczegółów nowego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7583-278">Choose **Commands** in the device details pane for the new device.</span></span>

    ![Dodawanie reguły urządzenia][img-adddevicerule2]

1. <span data-ttu-id="f7583-280">Wybierz pozycję **ChangeSetPointTemp** z listy poleceń i ustaw parametr **SetPointTemp** na wartość 45.</span><span class="sxs-lookup"><span data-stu-id="f7583-280">Select **ChangeSetPointTemp** from the command list and set **SetPointTemp** to 45.</span></span> <span data-ttu-id="f7583-281">Następnie wybierz pozycję **Wyślij polecenie**:</span><span class="sxs-lookup"><span data-stu-id="f7583-281">Then choose **Send Command**:</span></span>

    ![Dodawanie reguły urządzenia][img-adddevicerule3]

1. <span data-ttu-id="f7583-283">Wróć do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f7583-283">Navigate back to the dashboard.</span></span> <span data-ttu-id="f7583-284">Po pewnym czasie w okienku **Historia alarmów** pojawi się nowy wpis, gdy temperatura urządzenia przekroczy wartość progową równą 47 stopni:</span><span class="sxs-lookup"><span data-stu-id="f7583-284">After a short time, you will see a new entry in the **Alarm History** pane when the temperature reported by your new device exceeds the 47-degree threshold:</span></span>

    ![Dodawanie reguły urządzenia][img-adddevicerule4]

1. <span data-ttu-id="f7583-286">Na stronie **Reguły** pulpitu nawigacyjnego można przeglądać i edytować wszystkie reguły.</span><span class="sxs-lookup"><span data-stu-id="f7583-286">You can review and edit all your rules on the **Rules** page of the dashboard:</span></span>

    ![Wyświetlanie listy reguł urządzenia][img-rules]

1. <span data-ttu-id="f7583-288">Na stronie **Akcje** pulpitu nawigacyjnego można przeglądać i edytować wszystkie akcje, które mogą być wykonywane w odpowiedzi na działanie reguły:</span><span class="sxs-lookup"><span data-stu-id="f7583-288">You can review and edit all the actions that can be taken in response to a rule on the **Actions** page of the dashboard:</span></span>

    ![Wyświetlanie listy akcji urządzenia][img-actions]

> [!NOTE]
> <span data-ttu-id="f7583-290">Istnieje możliwość zdefiniowania akcji, które umożliwiają wysyłanie wiadomości e-mail lub SMS w odpowiedzi na działanie reguły albo pozwalają na integrację z systemem biznesowym za pośrednictwem [aplikacji logiki][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="f7583-290">It is possible to define actions that can send an email message or SMS in response to a rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="f7583-291">Aby uzyskać więcej informacji, zobacz [Łączenie aplikacji logiki ze wstępnie skonfigurowanym rozwiązaniem do zarządzania zdalnego Pakietu IoT Azure][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="f7583-291">For more information, see the [Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="f7583-292">Zarządzanie filtrami</span><span class="sxs-lookup"><span data-stu-id="f7583-292">Manage filters</span></span>

<span data-ttu-id="f7583-293">Na liście urządzeń można tworzyć, zapisywać i ponownie ładować filtry, co umożliwia wyświetlenie niestandardowej listy urządzeń podłączonych do centrum.</span><span class="sxs-lookup"><span data-stu-id="f7583-293">In the device list, you can create, save, and reload filters to display a customized list of devices connected to your hub.</span></span> <span data-ttu-id="f7583-294">Aby utworzyć filtr:</span><span class="sxs-lookup"><span data-stu-id="f7583-294">To create a filter:</span></span>

1. <span data-ttu-id="f7583-295">Wybierz ikonę edycji filtru nad listą urządzeń:</span><span class="sxs-lookup"><span data-stu-id="f7583-295">Choose the edit filter icon above the list of devices:</span></span>

    ![Otwieranie edytora filtru][img-editfiltericon]

1. <span data-ttu-id="f7583-297">W **Edytorze filtrów** można dodawać pola, operatory i wartości, aby filtrować listę urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f7583-297">In the **Filter editor**, add the fields, operators, and values to filter the device list.</span></span> <span data-ttu-id="f7583-298">W celu doprecyzowania filtru można dodać wiele klauzul.</span><span class="sxs-lookup"><span data-stu-id="f7583-298">You can add multiple clauses to refine your filter.</span></span> <span data-ttu-id="f7583-299">Wybierz pozycję **Filtruj**, aby zastosować filtr:</span><span class="sxs-lookup"><span data-stu-id="f7583-299">Choose **Filter** to apply the filter:</span></span>

    ![Tworzenie filtru][img-filtereditor]

1. <span data-ttu-id="f7583-301">W tym przykładzie lista jest filtrowana według producenta i numeru modelu:</span><span class="sxs-lookup"><span data-stu-id="f7583-301">In this example, the list is filtered by manufacturer and model number:</span></span>

    ![Filtrowana lista][img-filterelist]

1. <span data-ttu-id="f7583-303">Aby zapisać filtr pod niestandardową nazwą, wybierz ikonę **Zapisz jako**:</span><span class="sxs-lookup"><span data-stu-id="f7583-303">To save your filter with a custom name, choose the **Save as** icon:</span></span>

    ![Zapisywanie filtru][img-savefilter]

1. <span data-ttu-id="f7583-305">Aby ponownie zastosować uprzednio zapisany filtr, wybierz ikonę **Otwórz zapisany filtr**:</span><span class="sxs-lookup"><span data-stu-id="f7583-305">To reapply a filter you saved previously, choose the **Open saved filter** icon:</span></span>

    ![Otwieranie filtru][img-openfilter]

<span data-ttu-id="f7583-307">Filtry można tworzyć na postawie identyfikatora urządzenia, stanu urządzenia, żądanych właściwości, zgłaszanych właściwości i tagów.</span><span class="sxs-lookup"><span data-stu-id="f7583-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="f7583-308">Własne niestandardowe tagi można dodać do urządzenia w sekcji **Tagi** na panelu **Szczegóły urządzenia**. Można też uruchomić zadanie aktualizacji tagów na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="f7583-308">You add your own custom tags to a device in the **Tags** section of the **Device Details** panel, or run a job to update tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="f7583-309">W **Edytorze filtrów** można użyć **Widoku zaawansowanego**, aby móc bezpośrednio edytować tekst zapytania.</span><span class="sxs-lookup"><span data-stu-id="f7583-309">In the **Filter editor**, you can use the **Advanced view** to edit the query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="f7583-310">Polecenia</span><span class="sxs-lookup"><span data-stu-id="f7583-310">Commands</span></span>

<span data-ttu-id="f7583-311">Korzystając z panelu **Szczegóły urządzenia**, można wysłać polecenia do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7583-311">From the **Device Details** panel, you can send commands to the device.</span></span> <span data-ttu-id="f7583-312">Gdy urządzenie jest uruchamiane po raz pierwszy, wysyła do rozwiązania informacje o obsługiwanych poleceniach.</span><span class="sxs-lookup"><span data-stu-id="f7583-312">When a device first starts, it sends information about the commands it supports to the solution.</span></span> <span data-ttu-id="f7583-313">Aby poznać różnice między poleceniami i metodami, zobacz [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance] (Opcje wysyłania z chmury do urządzenia w usłudze Azure IoT Hub).</span><span class="sxs-lookup"><span data-stu-id="f7583-313">For a discussion of the differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="f7583-314">Wybierz pozycję **Polecenia** na panelu **Szczegóły urządzenia** dla wybranego urządzenia:</span><span class="sxs-lookup"><span data-stu-id="f7583-314">Choose **Commands** in the **Device Details** panel for the selected device:</span></span>

   ![Polecenia urządzenia na pulpicie nawigacyjnym][img-devicecommands]

1. <span data-ttu-id="f7583-316">Wybierz pozycję **PingDevice** na liście poleceń.</span><span class="sxs-lookup"><span data-stu-id="f7583-316">Select **PingDevice** from the command list.</span></span>

1. <span data-ttu-id="f7583-317">Wybierz pozycję **Wyślij polecenie**.</span><span class="sxs-lookup"><span data-stu-id="f7583-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="f7583-318">Stan polecenia można zobaczyć w historii poleceń.</span><span class="sxs-lookup"><span data-stu-id="f7583-318">You can see the status of the command in the command history.</span></span>

   ![Stan polecenia na pulpicie nawigacyjnym][img-pingcommand]

<span data-ttu-id="f7583-320">Rozwiązanie umożliwia śledzenie stanu wszystkich wysyłanych poleceń.</span><span class="sxs-lookup"><span data-stu-id="f7583-320">The solution tracks the status of each command it sends.</span></span> <span data-ttu-id="f7583-321">Na początku wynik ma wartość **Oczekiwanie**.</span><span class="sxs-lookup"><span data-stu-id="f7583-321">Initially the result is **Pending**.</span></span> <span data-ttu-id="f7583-322">Gdy urządzenie zgłosi wykonanie polecenia, wynik jest ustawiany na **Powodzenie**.</span><span class="sxs-lookup"><span data-stu-id="f7583-322">When the device reports that it has executed the command, the result is set to **Success**.</span></span>

## <a name="behind-the-scenes"></a><span data-ttu-id="f7583-323">Za kulisami</span><span class="sxs-lookup"><span data-stu-id="f7583-323">Behind the scenes</span></span>

<span data-ttu-id="f7583-324">Podczas wdrażania wstępnie skonfigurowanego rozwiązania jest tworzonych wiele zasobów w ramach wybranej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f7583-324">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="f7583-325">Można je wyświetlić w witrynie Azure [Portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="f7583-325">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="f7583-326">W procesie wdrażania jest tworzona **grupa zasobów** o nazwie odpowiadającej nazwie wstępnie skonfigurowanego rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="f7583-326">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Wstępnie skonfigurowane rozwiązanie w portalu Azure][img-portal]

<span data-ttu-id="f7583-328">Aby wyświetlić ustawienia danego zasobu, wybierz go z listy w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="f7583-328">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="f7583-329">Można również wyświetlić kod źródłowy wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7583-329">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="f7583-330">Kod źródłowy wstępnie skonfigurowanego rozwiązania do monitorowania zdalnego znajduje się w repozytorium GitHub [azure-iot-remote-monitoring][lnk-rmgithub]:</span><span class="sxs-lookup"><span data-stu-id="f7583-330">The remote monitoring preconfigured solution source code is in the [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="f7583-331">Folder **DeviceAdministration** zawiera kod źródłowy pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f7583-331">The **DeviceAdministration** folder contains the source code for the dashboard.</span></span>
* <span data-ttu-id="f7583-332">Folder **Simulator** zawiera kod źródłowy symulowanego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f7583-332">The **Simulator** folder contains the source code for the simulated device.</span></span>
* <span data-ttu-id="f7583-333">Folder **EventProcessor** zawiera kod źródłowy procesu zaplecza, który obsługuje przychodzące dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="f7583-333">The **EventProcessor** folder contains the source code for the back-end process that handles the incoming telemetry.</span></span>

<span data-ttu-id="f7583-334">Gdy wszystko będzie gotowe, możesz usunąć wstępnie skonfigurowane rozwiązanie z subskrypcji platformy Azure w witrynie [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="f7583-334">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="f7583-335">Ta witryna umożliwia łatwe usunięcie wszystkich zasobów, które zostały aprowizowane po utworzeniu wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f7583-335">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="f7583-336">Aby mieć pewność, że zostaną usunięte wszystkie elementy powiązane ze wstępnie skonfigurowanym rozwiązaniem, nie usuwaj grupy zasobów w portalu, ale usuń rozwiązanie w witrynie [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="f7583-336">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site and do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7583-337">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7583-337">Next Steps</span></span>

<span data-ttu-id="f7583-338">Teraz, kiedy zostało wdrożone wstępnie skonfigurowane rozwiązanie, które działa, możesz kontynuować poznawanie Pakietu IoT, czytając następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="f7583-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="f7583-339">[Przewodnik po wstępnie skonfigurowanym rozwiązaniu monitorowania zdalnego][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="f7583-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="f7583-340">[Łączenie urządzenia ze wstępnie skonfigurowanym rozwiązaniem do monitorowania zdalnego][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="f7583-340">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="f7583-341">[Uprawnienia w witrynie azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="f7583-341">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

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