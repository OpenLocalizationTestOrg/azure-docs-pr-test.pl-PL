---
title: "Wstępnie skonfigurowane rozwiązanie konserwacji predykcyjnej | Microsoft Docs"
description: "Opis wstępnie skonfigurowanego rozwiązania Pakietu Azure IoT do konserwacji predykcyjnej."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 8bad198488c4940a83eb32ec02122a91d47ca86c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="bb67f-103">Omówienie wstępnie skonfigurowanego rozwiązania konserwacji predykcyjnej</span><span class="sxs-lookup"><span data-stu-id="bb67f-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="bb67f-104">[Wstępnie skonfigurowane rozwiązanie][lnk_preconfigured_solutions] *konserwacji predykcyjnej* jest jednym ze wstępnie skonfigurowanych rozwiązań [Pakietu IoT Microsoft Azure][lnk_iot_suite].</span><span class="sxs-lookup"><span data-stu-id="bb67f-104">The *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of the [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="bb67f-105">To rozwiązanie obejmuje zbieranie danych telemetrycznych z urządzeń w czasie rzeczywistym i model predykcyjny utworzony za pomocą usługi [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="bb67f-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="bb67f-106">Pakiet IoT Azure pozwala szybko i łatwo łączyć się z zasobami i monitorować je oraz analizować dane telemetryczne w czasie rzeczywistym w ramach pulpitów nawigacyjnych i wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="bb67f-106">With Azure IoT Suite, you can quickly and easily connect to and monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="bb67f-107">W przypadku rozwiązania konserwacji predykcyjnej pulpity nawigacyjne i wizualizacje dostarczają nowe informacje analityczne, które pozwalają zwiększyć wydajność i wygenerować dodatkowe źródła przychodów.</span><span class="sxs-lookup"><span data-stu-id="bb67f-107">In the predictive maintenance solution, the dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="the-scenario"></a><span data-ttu-id="bb67f-108">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="bb67f-108">The Scenario</span></span>

<span data-ttu-id="bb67f-109">Fabrikam to regionalny przewoźnik lotniczy, ukierunkowany na zapewnienie doskonałej obsługi klientów przy zachowaniu konkurencyjnych cen.</span><span class="sxs-lookup"><span data-stu-id="bb67f-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="bb67f-110">Jedną z przyczyn powodujących opóźnienia lotów są kwestie związane z obsługą techniczną samolotów. Dotyczy to w szczególności konserwacji silników.</span><span class="sxs-lookup"><span data-stu-id="bb67f-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="bb67f-111">Firma Fabrikam musi za wszelką cenę zapobiegać awariom silników podczas lotu, zatem przeprowadza regularne przeglądy sprzętu i tworzy odpowiedni harmonogram konserwacji.</span><span class="sxs-lookup"><span data-stu-id="bb67f-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according to a plan.</span></span> <span data-ttu-id="bb67f-112">Jednak występują różnice dotyczące stopnia zużycia silników samolotów.</span><span class="sxs-lookup"><span data-stu-id="bb67f-112">However, aircraft engines don’t always wear the same.</span></span> <span data-ttu-id="bb67f-113">Zdarzają się przypadki wykonania prac konserwacyjnych, które nie były konieczne.</span><span class="sxs-lookup"><span data-stu-id="bb67f-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="bb67f-114">Co więcej, pojawiają się problemy, które mogą prowadzić do uziemienia danego samolotu, dopóki nie zostanie przeprowadzona konserwacja.</span><span class="sxs-lookup"><span data-stu-id="bb67f-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="bb67f-115">Te problemy powodują kosztowne opóźnienia, zwłaszcza jeśli samolot znajduje się w lokalizacji, w której nie są dostępne części zamienne lub odpowiednio wykwalifikowany personel.</span><span class="sxs-lookup"><span data-stu-id="bb67f-115">If an aircraft is at a location where the right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="bb67f-116">Silniki samolotów linii Fabrikam są wyposażone w czujniki, które monitorują stan silnika podczas lotu.</span><span class="sxs-lookup"><span data-stu-id="bb67f-116">The engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="bb67f-117">Firma Fabrikam korzysta z rozwiązania do konserwacji predykcyjnej w celu gromadzenia danych zebranych z czujników podczas lotu.</span><span class="sxs-lookup"><span data-stu-id="bb67f-117">Fabrikam uses the predictive maintenance solution to collect the sensor data collected during the flight.</span></span> <span data-ttu-id="bb67f-118">Zbierane przez całe lata dane dotyczące pracy i awarii silników umożliwiły inżynierom danych w firmie Fabrikam opracowanie modelu przewidywania pozostałego czasu eksploatacji silnika samolotu.</span><span class="sxs-lookup"><span data-stu-id="bb67f-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="bb67f-119">Model korzysta z zależności między danymi pochodzącymi z czterech czujników w silniku a zużyciem silnika, które może prowadzić do wystąpienia awarii.</span><span class="sxs-lookup"><span data-stu-id="bb67f-119">The model uses a correlation between data from four of the engine sensors and engine wear that leads to eventual failure.</span></span> <span data-ttu-id="bb67f-120">Linie Fabrikam wciąż regularnie przeprowadzają przeglądy w celu zapewnienia bezpieczeństwa, ale dysponują również modelami, które umożliwiają obliczenie pozostałego czasu eksploatacji poszczególnych silników po każdym locie.</span><span class="sxs-lookup"><span data-stu-id="bb67f-120">While Fabrikam continues to perform regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span></span> <span data-ttu-id="bb67f-121">Model wykorzystuje dane telemetryczne zebrane z silników podczas lotu.</span><span class="sxs-lookup"><span data-stu-id="bb67f-121">The model uses the telemetry collected from the engines during the flight.</span></span> <span data-ttu-id="bb67f-122">Pozwala to przewidywać przyszłe awarie i odpowiednio wcześniej zaplanować prace konserwacyjne i naprawcze.</span><span class="sxs-lookup"><span data-stu-id="bb67f-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="bb67f-123">W modelu rozwiązania wykorzystano dane dotyczące rzeczywistego zużycia silników.</span><span class="sxs-lookup"><span data-stu-id="bb67f-123">The solution model uses actual engine wear data.</span></span>

<span data-ttu-id="bb67f-124">Dzięki możliwości przewidywania terminu wymaganej obsługi technicznej firma Fabrikam może zoptymalizować swoje operacje, aby obniżyć koszty.</span><span class="sxs-lookup"><span data-stu-id="bb67f-124">By predicting the point when maintenance is required, Fabrikam can optimize its operations to reduce costs.</span></span>

<span data-ttu-id="bb67f-125">Współpraca koordynatorów ds. konserwacji z personelem odpowiedzialnym za rozkład lotów ma na celu:</span><span class="sxs-lookup"><span data-stu-id="bb67f-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="bb67f-126">Opracowanie harmonogramu, który umożliwia przeprowadzanie prac technicznych podczas postoju samolotu w danej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="bb67f-126">Plan maintenance to coincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="bb67f-127">Zapewnienie, że dostępna jest wystarczająca ilość czasu na serwisowanie samolotu, aby nie spowodować występowania zakłóceń w rozkładzie.</span><span class="sxs-lookup"><span data-stu-id="bb67f-127">Ensure sufficient time is available for the aircraft to be out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="bb67f-128">Zaplanowanie pracy personelu technicznego tak, aby serwisowanie samolotów odbywało się bez przestojów.</span><span class="sxs-lookup"><span data-stu-id="bb67f-128">To schedule technicians to ensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="bb67f-129">Menedżerowie odpowiedzialni za magazyny podzespołów mają dostęp do planów konserwacji, dzięki czemu mogą zoptymalizować zapasy części zamiennych i proces ich zamawiania.</span><span class="sxs-lookup"><span data-stu-id="bb67f-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="bb67f-130">Te działania umożliwiają firmie Fabrikam zminimalizowanie czasu obsługi naziemnej samolotów i zmniejszenie kosztów operacyjnych przy jednoczesnym zapewnieniu bezpieczeństwa pasażerów i załóg.</span><span class="sxs-lookup"><span data-stu-id="bb67f-130">These activities enable Fabrikam to minimize aircraft ground time and reduce operating costs while ensuring the safety of passengers and crew.</span></span>

<span data-ttu-id="bb67f-131">Aby dowiedzieć się, jakie funkcje dostępne w [Pakiecie IoT Azure][lnk_iot_suite] umożliwiają klientom wykorzystanie potencjalnych możliwości konserwacji predykcyjnej, zapoznaj się z tą [grafiką informacyjną][lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="bb67f-131">To understand how [Azure IoT Suite][lnk_iot_suite] provides the capabilities customers need to realize the potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-the-predictive-maintenance-solution-is-built"></a><span data-ttu-id="bb67f-132">Jak zbudowane jest rozwiązanie konserwacji predykcyjnej</span><span class="sxs-lookup"><span data-stu-id="bb67f-132">How the predictive maintenance solution is built</span></span>

<span data-ttu-id="bb67f-133">Rozwiązanie korzysta z istniejącego modelu usługi Azure Machine Learning dostępnego w postaci szablonu, który pozwala na demonstrację działania funkcji przy użyciu danych telemetrycznych pochodzących z urządzeń i zebranych za pomocą usług Pakietu IoT.</span><span class="sxs-lookup"><span data-stu-id="bb67f-133">The solution uses an existing Azure Machine Learning model available as a template to show these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="bb67f-134">Firma Microsoft opracowała [model regresji][lnk_regression_model] silnika samolotu na podstawie publicznie dostępnych danych<sup>\[1\]</sup> oraz szczegółowe wskazówki dotyczące używania tego modelu.</span><span class="sxs-lookup"><span data-stu-id="bb67f-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how to use the model.</span></span>

<span data-ttu-id="bb67f-135">Rozwiązanie Azure IoT do konserwacji predykcyjnej używa modelu regresji utworzonego na podstawie tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="bb67f-135">The Azure IoT predictive maintenance solution uses the regression model created from this template.</span></span> <span data-ttu-id="bb67f-136">Model jest wdrożony w ramach subskrypcji platformy Azure i dostępny za pośrednictwem automatycznie generowanego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bb67f-136">The model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="bb67f-137">Rozwiązanie to zawiera podzbiór danych testowych odpowiadających 4 ze 100 silników oraz strumieniom danych z 4 z 21 czujników.</span><span class="sxs-lookup"><span data-stu-id="bb67f-137">The solution includes a subset of the testing data representing 4 (of 100 total) engines and the 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="bb67f-138">Te dane wystarczają do uzyskania dokładnego wyniku za pomocą nauczonego modelu.</span><span class="sxs-lookup"><span data-stu-id="bb67f-138">This data is sufficient to provide an accurate result from the trained model.</span></span>

<span data-ttu-id="bb67f-139">*\[1\] A. Saxena and K. Goebel (2008). „Turbofan Engine Degradation Simulation Data Set” (Zestaw danych dotyczących symulacji degradacji silnika turbowentylatorowego), repozytorium danych prognostycznych NASA w Ames (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), ośrodek badawczy NASA w Ames, Moffett Field, Kalifornia*</span><span class="sxs-lookup"><span data-stu-id="bb67f-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="bb67f-140">Rozpoczynanie pracy z konserwacja predykcyjną</span><span class="sxs-lookup"><span data-stu-id="bb67f-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="bb67f-141">W tym samouczku przedstawiono, jak wykonać aprowizację rozwiązania konserwacji predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="bb67f-141">This tutorial shows you how to provision the predictive maintenance solution.</span></span> <span data-ttu-id="bb67f-142">Samouczek zawiera również opis podstawowych funkcji rozwiązania konserwacji predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="bb67f-142">It also walks you through the basic features of the predictive maintenance solution.</span></span> <span data-ttu-id="bb67f-143">Dostęp do wielu z tych funkcji można uzyskać za pośrednictwem pulpitu nawigacyjnego rozwiązania, który jest wdrażany razem ze wstępnie skonfigurowanym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="bb67f-143">You can access many of these features through the solution dashboard that deploys along with the preconfigured solution.</span></span>

<span data-ttu-id="bb67f-144">Do wykonania kroków tego samouczka jest potrzebna aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bb67f-144">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="bb67f-145">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="bb67f-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="bb67f-146">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="bb67f-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="bb67f-147">Zaloguj się w witrynie [azureiotsuite.com][lnk-azureiotsuite] przy użyciu poświadczeń konta platformy Azure i kliknij pozycję **+**, aby utworzyć rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="bb67f-147">Log on to [azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** to create a solution.</span></span>
1. <span data-ttu-id="bb67f-148">**Wybierz** kafelek **Konserwacja predykcyjna**.</span><span class="sxs-lookup"><span data-stu-id="bb67f-148">Click **Select** the **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="bb67f-149">W polu **Nazwa rozwiązania** wprowadź nazwę wstępnie skonfigurowanego rozwiązania konserwacji predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="bb67f-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="bb67f-150">W polach **Region** i **Subskrypcja** wybierz wartości, których chcesz użyć do aprowizacji rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="bb67f-150">Select the **Region** and **Subscription** you want to use to provision the solution.</span></span>
1. <span data-ttu-id="bb67f-151">Kliknij pozycję **Utwórz rozwiązanie**, aby rozpocząć proces aprowizowania.</span><span class="sxs-lookup"><span data-stu-id="bb67f-151">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="bb67f-152">Zwykle trwa on kilka minut.</span><span class="sxs-lookup"><span data-stu-id="bb67f-152">This process typically takes several minutes to run.</span></span>

### <a name="wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="bb67f-153">Oczekiwanie na ukończenie procesu aprowizowania</span><span class="sxs-lookup"><span data-stu-id="bb67f-153">Wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="bb67f-154">Kliknij kafelek swojego rozwiązania zawierający informację o stanie **aprowizacji**.</span><span class="sxs-lookup"><span data-stu-id="bb67f-154">Click the tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="bb67f-155">Zwróć uwagę na informację o **stanach aprowizacji** podczas wdrażania usług Azure w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bb67f-155">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="bb67f-156">Po ukończeniu aprowizowania stan zmieni się na wartość **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="bb67f-156">Once provisioning completes, the status changes to **Ready**.</span></span>
1. <span data-ttu-id="bb67f-157">Kliknij kafelek, aby wyświetlić szczegóły rozwiązania w prawym okienku.</span><span class="sxs-lookup"><span data-stu-id="bb67f-157">Click the tile to see the details of your solution in the right-hand pane.</span></span> <span data-ttu-id="bb67f-158">Z poziomu tego okienka możesz uruchomić pulpit nawigacyjny rozwiązania i uzyskać dostęp do obszaru roboczego usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bb67f-158">From this pane, you can launch the solution dashboard and access the Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="bb67f-159">Jeśli podczas wdrażania wstępnie skonfigurowanego rozwiązania pojawią się problemy, zapoznaj się z tematami [Uprawnienia w witrynie azureiotsuite.com][lnk-permissions] i [Często zadawane pytania][lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="bb67f-159">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [FAQ][lnk-faq].</span></span> <span data-ttu-id="bb67f-160">Jeśli problemy będą się powtarzać, utwórz żądanie pomocy w [portalu][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="bb67f-160">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="bb67f-161">Czy istnieją jakieś szczegóły dotyczące Twojego rozwiązania, które nie są wyświetlane, a Twoim zdaniem powinny być widoczne?</span><span class="sxs-lookup"><span data-stu-id="bb67f-161">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="bb67f-162">Prześlij nam swoje propozycje dotyczące funkcji, korzystając ze strony [User Voice](https://feedback.azure.com/forums/321918-azure-iot) (Opinie użytkowników).</span><span class="sxs-lookup"><span data-stu-id="bb67f-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-the-solution"></a><span data-ttu-id="bb67f-163">Wyświetlanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="bb67f-163">View the solution</span></span>

<span data-ttu-id="bb67f-164">W tej sekcji opisano interfejs użytkownika rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="bb67f-164">This section guides you through the solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="bb67f-165">Pulpit nawigacyjny konserwacji predykcyjnej</span><span class="sxs-lookup"><span data-stu-id="bb67f-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="bb67f-166">Na tej stronie aplikacji sieci Web są używane kontrolki JavaScript usługi Power BI (zobacz [repozytorium PowerBI-visuals][lnk-powerbi]), które umożliwiają wizualizację następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="bb67f-166">This page in the web application uses PowerBI JavaScript controls (see the [PowerBI-visuals repository][lnk-powerbi]) to visualize:</span></span>

* <span data-ttu-id="bb67f-167">Dane wyjściowe zadań usługi Stream Analytics przechowywane w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="bb67f-167">The output data from the Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="bb67f-168">Liczba cykli i pozostały czas eksploatacji silnika.</span><span class="sxs-lookup"><span data-stu-id="bb67f-168">The RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-the-behavior-of-the-cloud-solution"></a><span data-ttu-id="bb67f-169">Monitorowanie działania rozwiązania w chmurze</span><span class="sxs-lookup"><span data-stu-id="bb67f-169">Observing the behavior of the cloud solution</span></span>

<span data-ttu-id="bb67f-170">W portalu Azure przejdź do grupy zasobów z nazwą wybranego rozwiązania, aby wyświetlić aprowizowane zasoby.</span><span class="sxs-lookup"><span data-stu-id="bb67f-170">In the Azure portal, navigate to the resource group with the solution name you chose to view your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="bb67f-171">Po przeprowadzeniu aprowizacji wstępnie skonfigurowanego rozwiązania otrzymasz wiadomość e-mail z linkiem do obszaru roboczego usługi Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bb67f-171">When you provision the preconfigured solution, you receive an email with a link to the Machine Learning workspace.</span></span> <span data-ttu-id="bb67f-172">Do obszaru roboczego usługi Machine Learning można także przejść ze strony [azureiotsuite.com][lnk-azureiotsuite] zaprowizowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="bb67f-172">You can also navigate to the Machine Learning workspace from the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="bb67f-173">Kafelek jest dostępny na tej stronie, gdy rozwiązanie jest w stanie **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="bb67f-173">A tile is available on this page when the solution is in the **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="bb67f-174">W portalu rozwiązania możesz zobaczyć, że do aprowizacji przykładu użyto czterech symulowanych urządzeń (dwa samoloty z dwoma silnikami każdy) i czterech czujników na silnik.</span><span class="sxs-lookup"><span data-stu-id="bb67f-174">In the solution portal, you can see that the sample is provisioned with four simulated devices to represent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="bb67f-175">Gdy po raz pierwszy przejdziesz do portalu rozwiązania, zobaczysz, że symulacja jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="bb67f-175">When you first navigate to the solution portal, the simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="bb67f-176">Kliknij pozycję **Rozpocznij symulację**, aby uruchomić symulację.</span><span class="sxs-lookup"><span data-stu-id="bb67f-176">Click **Start simulation** to begin the simulation.</span></span> <span data-ttu-id="bb67f-177">Na pulpicie nawigacyjnym zostanie wyświetlona liczba cykli, historia danych z czujników i pozostały czas eksploatacji wraz z historią.</span><span class="sxs-lookup"><span data-stu-id="bb67f-177">The sensor history, RUL, Cycles, and RUL history populate the dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="bb67f-178">Jeśli wartość pozostałego czasu eksploatacji jest mniejsza niż 160 (arbitralna wartość progowa dla celów demonstracyjnych), w portalu rozwiązania zostanie wyświetlony symbol ostrzeżenia obok pozostałego czasu eksploatacji.</span><span class="sxs-lookup"><span data-stu-id="bb67f-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display.</span></span> <span data-ttu-id="bb67f-179">Dodatkowo w portalu rozwiązania silnik samolotu zostanie wyróżniony kolorem żółtym.</span><span class="sxs-lookup"><span data-stu-id="bb67f-179">The solution portal also highlights the aircraft engine in yellow.</span></span> <span data-ttu-id="bb67f-180">Zwróć uwagę na to, jak pozostały czas eksploatacji ma ogólną tendencję zniżkową ze skokami w górę i w dół.</span><span class="sxs-lookup"><span data-stu-id="bb67f-180">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span></span> <span data-ttu-id="bb67f-181">Takie zachowanie wynika z dokładności modelu i różnych czasów trwania cykli.</span><span class="sxs-lookup"><span data-stu-id="bb67f-181">This behavior results from the varying cycle lengths and the model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="bb67f-182">Pełna symulacja, obejmująca 148 cykli, trwa około 35 minut.</span><span class="sxs-lookup"><span data-stu-id="bb67f-182">The full simulation takes around 35 minutes to complete 148 cycles.</span></span> <span data-ttu-id="bb67f-183">Pozostały czas eksploatacji po raz pierwszy osiąga wartość progową równą 160 po upływie około 5 minut, a oba silniki osiągają wartości progowe po upływie około 8 minut.</span><span class="sxs-lookup"><span data-stu-id="bb67f-183">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span></span>

<span data-ttu-id="bb67f-184">W trakcie symulacji obejmującej 148 cykli jest przetwarzany pełny zestaw danych, co prowadzi do określenia końcowej liczby cykli i wartości pozostałego czasu eksploatacji.</span><span class="sxs-lookup"><span data-stu-id="bb67f-184">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="bb67f-185">Symulację można zatrzymać w dowolnym momencie, ale kliknięcie przycisku **Rozpocznij symulację** powoduje ponowne uruchomienie symulacji od początku zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="bb67f-185">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb67f-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bb67f-186">Next steps</span></span>

<span data-ttu-id="bb67f-187">Aby dowiedzieć się więcej o obsłudze scenariuszy konserwacji predykcyjnej w Pakiecie IoT Azure, zapoznaj się z dokumentem[Capture value from the Internet of Things][lnk_capture_value] (Korzyści z Internetu rzeczy).</span><span class="sxs-lookup"><span data-stu-id="bb67f-187">To learn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from the Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="bb67f-188">Skorzystaj z [przewodnika][lnk-predictive-walkthrough] po rozwiązaniu do konserwacji predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="bb67f-188">Take a [walkthrough][lnk-predictive-walkthrough] of the predictive maintenance solution.</span></span>

<span data-ttu-id="bb67f-189">Możesz także wypróbować niektóre inne funkcje i możliwości wstępnie skonfigurowanych rozwiązań Pakietu IoT:</span><span class="sxs-lookup"><span data-stu-id="bb67f-189">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="bb67f-190">[Często zadawane pytania dotyczące Pakietu IoT][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="bb67f-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="bb67f-191">[Zabezpieczenia IoT od podstaw][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="bb67f-191">[IoT security from the ground up][lnk-security-groundup]</span></span>

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/