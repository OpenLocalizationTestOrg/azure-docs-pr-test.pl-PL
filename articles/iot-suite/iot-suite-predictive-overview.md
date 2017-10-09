---
title: "Konserwacja aaaPredictive wstępnie skonfigurowane rozwiązanie | Dokumentacja firmy Microsoft"
description: "Opis konserwacji predykcyjnej pakiet IoT Azure hello wstępnie skonfigurowane rozwiązanie."
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
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="e3990-103">Omówienie wstępnie skonfigurowanego rozwiązania konserwacji predykcyjnej</span><span class="sxs-lookup"><span data-stu-id="e3990-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="e3990-104">Witaj *konserwacji predykcyjnej* [wstępnie skonfigurowane rozwiązanie] [ lnk_preconfigured_solutions] jest jednym z hello [pakiet IoT Microsoft Azure] [ lnk_iot_suite] wstępnie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e3990-104">hello *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of hello [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="e3990-105">To rozwiązanie obejmuje zbieranie danych telemetrycznych z urządzeń w czasie rzeczywistym i model predykcyjny utworzony za pomocą usługi [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="e3990-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="e3990-106">Z pakiet IoT Azure można szybko i łatwo połączyć tooand monitor zasobów i analizowania telemetrii w czasie rzeczywistym w pulpitach nawigacyjnych i wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="e3990-106">With Azure IoT Suite, you can quickly and easily connect tooand monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="e3990-107">W rozwiązaniu konserwacji predykcyjnej hello hello pulpitów nawigacyjnych i wizualizacji umożliwiają nowe analizy, które można dysków wydajność i zwiększyć przychody strumieni.</span><span class="sxs-lookup"><span data-stu-id="e3990-107">In hello predictive maintenance solution, hello dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="hello-scenario"></a><span data-ttu-id="e3990-108">Witaj scenariusza</span><span class="sxs-lookup"><span data-stu-id="e3990-108">hello Scenario</span></span>

<span data-ttu-id="e3990-109">Fabrikam to regionalny przewoźnik lotniczy, ukierunkowany na zapewnienie doskonałej obsługi klientów przy zachowaniu konkurencyjnych cen.</span><span class="sxs-lookup"><span data-stu-id="e3990-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="e3990-110">Jedną z przyczyn powodujących opóźnienia lotów są kwestie związane z obsługą techniczną samolotów. Dotyczy to w szczególności konserwacji silników.</span><span class="sxs-lookup"><span data-stu-id="e3990-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="e3990-111">Firma Fabrikam należy unikać błąd aparatu w locie za wszelką cenę regularnie bada jego aparaty i harmonogramy konserwacji zgodnie z planem tooa.</span><span class="sxs-lookup"><span data-stu-id="e3990-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according tooa plan.</span></span> <span data-ttu-id="e3990-112">Jednak powietrznego przez aparaty nie zawsze nosić hello takie same.</span><span class="sxs-lookup"><span data-stu-id="e3990-112">However, aircraft engines don’t always wear hello same.</span></span> <span data-ttu-id="e3990-113">Zdarzają się przypadki wykonania prac konserwacyjnych, które nie były konieczne.</span><span class="sxs-lookup"><span data-stu-id="e3990-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="e3990-114">Co więcej, pojawiają się problemy, które mogą prowadzić do uziemienia danego samolotu, dopóki nie zostanie przeprowadzona konserwacja.</span><span class="sxs-lookup"><span data-stu-id="e3990-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="e3990-115">Jeśli samolotu znajduje się w lokalizacji gdzie hello techników prawo lub zamiennych nie są dostępne, te problemy mogą być szczególnie kosztowne.</span><span class="sxs-lookup"><span data-stu-id="e3990-115">If an aircraft is at a location where hello right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="e3990-116">aparaty Hello samolotów firmy są instrumentowane przy użyciu czujników, które monitorują aparat warunków w locie.</span><span class="sxs-lookup"><span data-stu-id="e3990-116">hello engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="e3990-117">Firma Fabrikam stosuje hello konserwacji predykcyjnej rozwiązania toocollect hello czujnik dane zebrane podczas transmitowane hello.</span><span class="sxs-lookup"><span data-stu-id="e3990-117">Fabrikam uses hello predictive maintenance solution toocollect hello sensor data collected during hello flight.</span></span> <span data-ttu-id="e3990-118">Po kumulowanych lat aparatu operacyjne i dane awarii analityków danych w firmie Fabrikam mają modelowane hello toopredict sposób pozostała użytkowania (RUL) powietrznego aparatu.</span><span class="sxs-lookup"><span data-stu-id="e3990-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="e3990-119">Hello model używa korelacji między danymi z czterech hello aparat czujników i zużycia aparatu, który prowadzi tooeventual awarii.</span><span class="sxs-lookup"><span data-stu-id="e3990-119">hello model uses a correlation between data from four of hello engine sensors and engine wear that leads tooeventual failure.</span></span> <span data-ttu-id="e3990-120">Gdy firma Fabrikam nadal tooperform regularne inspekcje tooensure bezpieczeństwa, go teraz używać hello modele toocompute hello RUL dla każdego aparatu po każdym locie.</span><span class="sxs-lookup"><span data-stu-id="e3990-120">While Fabrikam continues tooperform regular inspections tooensure safety, it can now use hello models toocompute hello RUL for each engine after every flight.</span></span> <span data-ttu-id="e3990-121">Hello model używa hello dane telemetryczne zebrane z aparaty hello w locie hello.</span><span class="sxs-lookup"><span data-stu-id="e3990-121">hello model uses hello telemetry collected from hello engines during hello flight.</span></span> <span data-ttu-id="e3990-122">Pozwala to przewidywać przyszłe awarie i odpowiednio wcześniej zaplanować prace konserwacyjne i naprawcze.</span><span class="sxs-lookup"><span data-stu-id="e3990-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="e3990-123">model rozwiązania Hello używa aparatu rzeczywistego zużycia danych.</span><span class="sxs-lookup"><span data-stu-id="e3990-123">hello solution model uses actual engine wear data.</span></span>

<span data-ttu-id="e3990-124">Przez punkt hello gdy wymagana jest obsługa, Fabrikam można optymalizować koszty tooreduce jego operacji.</span><span class="sxs-lookup"><span data-stu-id="e3990-124">By predicting hello point when maintenance is required, Fabrikam can optimize its operations tooreduce costs.</span></span>

<span data-ttu-id="e3990-125">Współpraca koordynatorów ds. konserwacji z personelem odpowiedzialnym za rozkład lotów ma na celu:</span><span class="sxs-lookup"><span data-stu-id="e3990-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="e3990-126">Planowanie obsługi toocoincide z samolotu zatrzymywanie w określonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e3990-126">Plan maintenance toocoincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="e3990-127">Upewnij się, że czas wystarczający jest dostępna dla hello powietrznego toobe poza eksploatacją bez powodowania przerw w działaniu harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="e3990-127">Ensure sufficient time is available for hello aircraft toobe out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="e3990-128">tooensure techników tooschedule efektywną obsługę powietrznego bez czasu oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="e3990-128">tooschedule technicians tooensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="e3990-129">Menedżerowie odpowiedzialni za magazyny podzespołów mają dostęp do planów konserwacji, dzięki czemu mogą zoptymalizować zapasy części zamiennych i proces ich zamawiania.</span><span class="sxs-lookup"><span data-stu-id="e3990-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="e3990-130">Te działania firmy Fabrikam toominimize powietrznego podstaw czas i zmniejszyć koszty operacyjne, przy równoczesnym zapewnieniu bezpieczeństwa hello osób i zespół ds..</span><span class="sxs-lookup"><span data-stu-id="e3990-130">These activities enable Fabrikam toominimize aircraft ground time and reduce operating costs while ensuring hello safety of passengers and crew.</span></span>

<span data-ttu-id="e3990-131">toounderstand jak [pakiet IoT Azure] [ lnk_iot_suite] zapewnia hello możliwości klienci muszą potencjalne hello toorealize konserwacji predykcyjnej, przejrzyj to [infographic] [lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="e3990-131">toounderstand how [Azure IoT Suite][lnk_iot_suite] provides hello capabilities customers need toorealize hello potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-hello-predictive-maintenance-solution-is-built"></a><span data-ttu-id="e3990-132">Jak jest wbudowane rozwiązanie do konserwacji predykcyjnej hello</span><span class="sxs-lookup"><span data-stu-id="e3990-132">How hello predictive maintenance solution is built</span></span>

<span data-ttu-id="e3990-133">rozwiązanie Hello używa istniejącego modelu uczenia maszynowego Azure dostępna jako tooshow szablonu te możliwości pracy z telemetrii urządzenia zbieranych za pośrednictwem usługi pakiet IoT.</span><span class="sxs-lookup"><span data-stu-id="e3990-133">hello solution uses an existing Azure Machine Learning model available as a template tooshow these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="e3990-134">Microsoft opracowała [modelu regresji] [ lnk_regression_model] aparatu powietrznego na podstawie publicznie dostępnych danych<sup>\[1\]</sup>i krok po kroku wskazówki dotyczące sposobu toouse hello modelu.</span><span class="sxs-lookup"><span data-stu-id="e3990-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how toouse hello model.</span></span>

<span data-ttu-id="e3990-135">Hello Azure IoT rozwiązanie do konserwacji predykcyjnej wykorzystuje model regresji hello utworzone na podstawie tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="e3990-135">hello Azure IoT predictive maintenance solution uses hello regression model created from this template.</span></span> <span data-ttu-id="e3990-136">Hello model jest wdrożonych w ramach subskrypcji platformy Azure i dostępne za pośrednictwem interfejsu API wygenerowanej automatycznie.</span><span class="sxs-lookup"><span data-stu-id="e3990-136">hello model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="e3990-137">rozwiązanie Hello zawiera podzbiór hello testowania dane reprezentujące 4 (całkowita liczba 100) aparaty oraz strumieni danych czujnika hello 4 (of 21 całkowita).</span><span class="sxs-lookup"><span data-stu-id="e3990-137">hello solution includes a subset of hello testing data representing 4 (of 100 total) engines and hello 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="e3990-138">Te dane są wystarczające tooprovide dokładne wyniku hello trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="e3990-138">This data is sufficient tooprovide an accurate result from hello trained model.</span></span>

<span data-ttu-id="e3990-139">*\[1\] A. Saxena and K. Goebel (2008). „Turbofan Engine Degradation Simulation Data Set” (Zestaw danych dotyczących symulacji degradacji silnika turbowentylatorowego), repozytorium danych prognostycznych NASA w Ames (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), ośrodek badawczy NASA w Ames, Moffett Field, Kalifornia*</span><span class="sxs-lookup"><span data-stu-id="e3990-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="e3990-140">Rozpoczynanie pracy z konserwacja predykcyjną</span><span class="sxs-lookup"><span data-stu-id="e3990-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="e3990-141">Ten samouczek pokazuje, jak tooprovision hello rozwiązanie do konserwacji predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="e3990-141">This tutorial shows you how tooprovision hello predictive maintenance solution.</span></span> <span data-ttu-id="e3990-142">On również przeprowadzi Cię przez hello podstawowych funkcji hello rozwiązanie do konserwacji predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="e3990-142">It also walks you through hello basic features of hello predictive maintenance solution.</span></span> <span data-ttu-id="e3990-143">Wiele z tych funkcji dostępne za pośrednictwem pulpitu nawigacyjnego rozwiązania hello, która wdraża wraz z hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="e3990-143">You can access many of these features through hello solution dashboard that deploys along with hello preconfigured solution.</span></span>

<span data-ttu-id="e3990-144">toocomplete tego samouczka należy aktywną subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e3990-144">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e3990-145">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="e3990-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e3990-146">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="e3990-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="e3990-147">Zaloguj się za[azureiotsuite.com] [ lnk-azureiotsuite] poświadczenia konta przy użyciu platformy Azure i kliknij przycisk  **+**  toocreate rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e3990-147">Log on too[azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** toocreate a solution.</span></span>
1. <span data-ttu-id="e3990-148">Kliknij przycisk **wybierz** hello **konserwacji predykcyjnej** kafelka.</span><span class="sxs-lookup"><span data-stu-id="e3990-148">Click **Select** hello **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="e3990-149">W polu **Nazwa rozwiązania** wprowadź nazwę wstępnie skonfigurowanego rozwiązania konserwacji predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="e3990-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="e3990-150">Wybierz hello **Region** i **subskrypcji** toouse tooprovision hello rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="e3990-150">Select hello **Region** and **Subscription** you want toouse tooprovision hello solution.</span></span>
1. <span data-ttu-id="e3990-151">Kliknij przycisk **Utwórz rozwiązanie** hello toobegin w procesie inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="e3990-151">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="e3990-152">Ten proces zwykle trwa kilka minut toorun.</span><span class="sxs-lookup"><span data-stu-id="e3990-152">This process typically takes several minutes toorun.</span></span>

### <a name="wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="e3990-153">Poczekaj, aż hello inicjowania obsługi administracyjnej toocomplete procesu</span><span class="sxs-lookup"><span data-stu-id="e3990-153">Wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="e3990-154">Kliknij Kafelek hello rozwiązania z **inicjowania obsługi administracyjnej** stanu.</span><span class="sxs-lookup"><span data-stu-id="e3990-154">Click hello tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="e3990-155">Powiadomienie hello **inicjowania obsługi administracyjnej stanów** podczas wdrażania usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e3990-155">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="e3990-156">Po ukończeniu inicjowania obsługi administracyjnej hello zmiany stanu zbyt**gotowe**.</span><span class="sxs-lookup"><span data-stu-id="e3990-156">Once provisioning completes, hello status changes too**Ready**.</span></span>
1. <span data-ttu-id="e3990-157">Kliknij przycisk hello kafelka toosee hello szczegóły rozwiązania w okienku po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="e3990-157">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span> <span data-ttu-id="e3990-158">W tym okienku możesz uruchomić hello rozwiązania dostępu i pulpit nawigacyjny hello obszaru roboczego uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="e3990-158">From this pane, you can launch hello solution dashboard and access hello Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="e3990-159">Jeśli wystąpią problemy dotyczące wdrażania rozwiązania hello wstępnie skonfigurowane, przejrzyj [uprawnienia w witrynie azureiotsuite.com hello] [ lnk-permissions] i hello [— często zadawane pytania] [ lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="e3990-159">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [FAQ][lnk-faq].</span></span> <span data-ttu-id="e3990-160">Jeśli hello problemy będą się powtarzać, Utwórz biletu usługi na powitania [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="e3990-160">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="e3990-161">Czy istnieją szczegółowe informacje można oczekiwać toosee, które nie są wyświetlane dla rozwiązania?</span><span class="sxs-lookup"><span data-stu-id="e3990-161">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="e3990-162">Prześlij nam swoje propozycje dotyczące funkcji, korzystając ze strony [User Voice](https://feedback.azure.com/forums/321918-azure-iot) (Opinie użytkowników).</span><span class="sxs-lookup"><span data-stu-id="e3990-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-hello-solution"></a><span data-ttu-id="e3990-163">Wyświetl hello rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="e3990-163">View hello solution</span></span>

<span data-ttu-id="e3990-164">Ta sekcja przeprowadzi Cię przez rozwiązanie hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e3990-164">This section guides you through hello solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="e3990-165">Pulpit nawigacyjny konserwacji predykcyjnej</span><span class="sxs-lookup"><span data-stu-id="e3990-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="e3990-166">Ta strona w aplikacji sieci web hello używa kontrolek JavaScript usługi Power BI (zobacz hello [repozytorium elementów wizualnych usługi Power BI][lnk-powerbi]) toovisualize:</span><span class="sxs-lookup"><span data-stu-id="e3990-166">This page in hello web application uses PowerBI JavaScript controls (see hello [PowerBI-visuals repository][lnk-powerbi]) toovisualize:</span></span>

* <span data-ttu-id="e3990-167">Witaj danych wyjściowych z zadania usługi analiza strumienia hello w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e3990-167">hello output data from hello Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="e3990-168">Witaj RUL i cyklu liczba na powietrznego aparatu.</span><span class="sxs-lookup"><span data-stu-id="e3990-168">hello RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a><span data-ttu-id="e3990-169">Obserwowania zachowanie hello hello rozwiązania chmury</span><span class="sxs-lookup"><span data-stu-id="e3990-169">Observing hello behavior of hello cloud solution</span></span>

<span data-ttu-id="e3990-170">W portalu Azure Witaj, przejdź toohello grupy zasobów o nazwie rozwiązania hello wybrano tooview udostępnione zasoby.</span><span class="sxs-lookup"><span data-stu-id="e3990-170">In hello Azure portal, navigate toohello resource group with hello solution name you chose tooview your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="e3990-171">Podczas obsługi administracyjnej hello wstępnie skonfigurowane rozwiązanie otrzymasz wiadomość e-mail z obszaru roboczego uczenia maszynowego toohello łącza.</span><span class="sxs-lookup"><span data-stu-id="e3990-171">When you provision hello preconfigured solution, you receive an email with a link toohello Machine Learning workspace.</span></span> <span data-ttu-id="e3990-172">Można także przechodzić obszaru roboczego uczenia maszynowego toohello z hello [azureiotsuite.com] [ lnk-azureiotsuite] strony elastycznie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e3990-172">You can also navigate toohello Machine Learning workspace from hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="e3990-173">Kafelek jest dostępne na tej stronie, gdy rozwiązanie hello jest hello **gotowe** stanu.</span><span class="sxs-lookup"><span data-stu-id="e3990-173">A tile is available on this page when hello solution is in hello **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="e3990-174">W portalu rozwiązania hello można zauważyć, że z próbką hello jest udostępniane z dwóch powietrznego toorepresent cztery symulowanego urządzenia dwa aparaty na lotniczych, każdy z czterech czujników.</span><span class="sxs-lookup"><span data-stu-id="e3990-174">In hello solution portal, you can see that hello sample is provisioned with four simulated devices toorepresent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="e3990-175">Podczas pierwszego przechodzenia toohello rozwiązanie portalu, symulacji hello jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="e3990-175">When you first navigate toohello solution portal, hello simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="e3990-176">Kliknij przycisk **Start symulacji** toobegin hello symulacji.</span><span class="sxs-lookup"><span data-stu-id="e3990-176">Click **Start simulation** toobegin hello simulation.</span></span> <span data-ttu-id="e3990-177">Witaj historii czujnika, RUL cykle i RUL historii wypełnić hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e3990-177">hello sensor history, RUL, Cycles, and RUL history populate hello dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="e3990-178">Gdy RUL jest mniejsza niż 160 (dowolnego próg wybrany dla celów demonstracyjnych), portalu rozwiązania hello wyświetla ostrzeżenie symbol toohello dalej, wyświetlić RUL.</span><span class="sxs-lookup"><span data-stu-id="e3990-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), hello solution portal displays a warning symbol next toohello RUL display.</span></span> <span data-ttu-id="e3990-179">portal rozwiązania Hello również wyodrębnić hello powietrznego aparat kolorem żółtym.</span><span class="sxs-lookup"><span data-stu-id="e3990-179">hello solution portal also highlights hello aircraft engine in yellow.</span></span> <span data-ttu-id="e3990-180">Zwróć uwagę, jak hello RUL wartości mają ogólne trend pobieranej ogólnej, ale mają tendencję toobounce w górę i w dół.</span><span class="sxs-lookup"><span data-stu-id="e3990-180">Notice how hello RUL values have a general downward trend overall, but tend toobounce up and down.</span></span> <span data-ttu-id="e3990-181">To zachowanie jest wynikiem hello różne długości cyklu i hello dokładności modelu.</span><span class="sxs-lookup"><span data-stu-id="e3990-181">This behavior results from hello varying cycle lengths and hello model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="e3990-182">Pełna symulacji Hello trwa około 35 toocomplete minut 148 cykle.</span><span class="sxs-lookup"><span data-stu-id="e3990-182">hello full simulation takes around 35 minutes toocomplete 148 cycles.</span></span> <span data-ttu-id="e3990-183">Hello 160 RUL osiągnięty jest próg dla powitania po raz pierwszy po około 5 minut, a oba aparaty trafienie próg hello około 8 minut.</span><span class="sxs-lookup"><span data-stu-id="e3990-183">hello 160 RUL threshold is met for hello first time at around 5 minutes and both engines hit hello threshold at around 8 minutes.</span></span>

<span data-ttu-id="e3990-184">Symulacja Hello jest uruchomiony za pośrednictwem hello pełen zestaw 148 cykle i reguluje na wartości końcowe RUL i cyklu.</span><span class="sxs-lookup"><span data-stu-id="e3990-184">hello simulation runs through hello complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="e3990-185">Można zatrzymać symulacji hello w dowolnym punkt, ale kliknięcie **Start symulacji** odtworzenie hello symulacji od początku hello hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="e3990-185">You can stop hello simulation at any point, but clicking **Start Simulation** replays hello simulation from hello start of hello dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3990-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3990-186">Next steps</span></span>

<span data-ttu-id="e3990-187">więcej informacji na temat sposobu Azure IoT umożliwia scenariuszy konserwacji predykcyjnej, przeczytaj toolearn [przechwytywania wartość z Internetu rzeczy hello][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="e3990-187">toolearn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from hello Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="e3990-188">Podejmij [wskazówki] [ lnk-predictive-walkthrough] hello konserwacji predykcyjnej rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e3990-188">Take a [walkthrough][lnk-predictive-walkthrough] of hello predictive maintenance solution.</span></span>

<span data-ttu-id="e3990-189">Możesz też przeglądać niektóre hello inne funkcje i możliwości rozwiązań pakiet IoT wstępnie hello:</span><span class="sxs-lookup"><span data-stu-id="e3990-189">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="e3990-190">[Często zadawane pytania dotyczące Pakietu IoT][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="e3990-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="e3990-191">[Zabezpieczenia IoT z hello tła w][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="e3990-191">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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