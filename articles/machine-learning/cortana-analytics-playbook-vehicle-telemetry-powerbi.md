---
title: aaaPower BI pulpit nawigacyjny kondycji vehicle i kierowania zwyczaje - Azure | Dokumentacja firmy Microsoft
description: "Korzystanie z możliwości hello wgląd w czasie rzeczywistym oraz predykcyjnej toogain Cortana Intelligence na kondycji vehicle i wspierającym zwyczaje."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="55779-103">Instrukcje instalacji pulpitu nawigacyjnego programu Power BI szablon rozwiązania vehicle telemetrii analityka</span><span class="sxs-lookup"><span data-stu-id="55779-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="55779-104">To **menu** toohello rozdziałów tego podręcznika dotyczącego łączy.</span><span class="sxs-lookup"><span data-stu-id="55779-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="55779-105">ilustrację Hello rozwiązania analizy Telemetrii Vehicle jak przedstawicielstw samochodu handlowych, producentów samochodów i ubezpieczeń mogą korzystać z możliwości hello Cortana Intelligence toogain w czasie rzeczywistym oraz predykcyjnej rozeznanie vehicle kondycji i wspierającym ulepszenia toodrive zwyczaje w obszarze powitania klienta wystąpić R & D i kampanii marketingowych.</span><span class="sxs-lookup"><span data-stu-id="55779-105">hello Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits toodrive improvements in hello area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="55779-106">Ten dokument zawiera instrukcje krok po kroku dotyczące sposobu konfigurowania raportów usługi Power BI hello i pulpitu nawigacyjnego po wdrożeniu rozwiązania hello w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="55779-106">This document contains step by step instructions on how you can configure hello Power BI reports and dashboard once hello solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="55779-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="55779-107">Prerequisites</span></span>
1. <span data-ttu-id="55779-108">Wdrażanie hello [analizy Telemetrii](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) rozwiązania</span><span class="sxs-lookup"><span data-stu-id="55779-108">Deploy hello [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="55779-109">Zainstaluj program Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="55779-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="55779-110">[Subskrypcji platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55779-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="55779-111">Jeśli nie masz subskrypcji platformy Azure, Rozpoczynanie pracy z bezpłatnej subskrypcji Azure</span><span class="sxs-lookup"><span data-stu-id="55779-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="55779-112">Konto usługi Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="55779-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="55779-113">Składników pakietu Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="55779-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="55779-114">W ramach szablon rozwiązania analizy Telemetrii Vehicle hello hello następujące usługi Cortana Intelligence są wdrażane w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="55779-114">As part of hello Vehicle Telemetry Analytics solution template, hello following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="55779-115">**Centrum zdarzeń** służy do wprowadzania miliony zdarzeń telemetrii vehicle na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="55779-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="55779-116">**Analiza strumienia** do uzyskania wgląd w czasie rzeczywistym w kondycję vehicle i będzie się powtarzał tych danych do długoterminowego przechowywania dla bardziej zaawansowane funkcje analizy partii.</span><span class="sxs-lookup"><span data-stu-id="55779-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="55779-117">**Machine Learning** wykrywania anomalii w czasie rzeczywistym i insights predykcyjnej toogain przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="55779-117">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="55779-118">**HDInsight** jest wykorzystywana tootransform danych na dużą skalę</span><span class="sxs-lookup"><span data-stu-id="55779-118">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="55779-119">**Fabryka danych** obsługuje aranżacji, potoku przetwarzania wsadowego hello monitorowania i planowania zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="55779-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>

<span data-ttu-id="55779-120">**Power BI** daje to rozwiązanie sformatowanego pulpitu nawigacyjnego w czasie rzeczywistym danych i wizualizacji analizy predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="55779-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="55779-121">rozwiązanie Hello używa dwóch różnych źródeł danych: **symulowane sygnały vehicle i danych diagnostycznych** i **katalogu vehicle**.</span><span class="sxs-lookup"><span data-stu-id="55779-121">hello solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="55779-122">Symulator telematyki vehicle wchodzi w skład tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="55779-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="55779-123">Emituje informacje diagnostyczne, a sygnały odpowiadający mu stan toohello hello vehicle i kierowania wzorca w danym punkcie w czasie.</span><span class="sxs-lookup"><span data-stu-id="55779-123">It emits diagnostic information and signals corresponding toohello state of hello vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="55779-124">Witaj Vehicle katalogu jest odwołanie do zestawu danych zawierającego VIN toomodel mapowania</span><span class="sxs-lookup"><span data-stu-id="55779-124">hello Vehicle Catalog is a reference dataset containing VIN toomodel mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="55779-125">Power BI pulpitu nawigacyjnego przygotowania</span><span class="sxs-lookup"><span data-stu-id="55779-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="55779-126">Pulpit nawigacyjny Instalatora Power BI w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="55779-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="55779-127">**Uruchom aplikację w czasie rzeczywistym pulpitu nawigacyjnego hello** po zakończeniu wdrażania hello należy wykonać instrukcje działania ręcznego hello</span><span class="sxs-lookup"><span data-stu-id="55779-127">**Start hello real-time dashboard application** Once hello deployment is completed, you should follow hello Manual Operation Instructions</span></span>

* <span data-ttu-id="55779-128">Pobierz aplikację pulpitu nawigacyjnego w czasie rzeczywistym RealtimeDashboardApp.zip i Rozpakuj go.</span><span class="sxs-lookup"><span data-stu-id="55779-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="55779-129">W folderze rozpakowane hello należy otworzyć pliku konfiguracji aplikacji 'RealtimeDashboardApp.exe.config' appSettings Zamień połączeń usługi Eventhub, magazynu obiektów Blob i ML wartościami hello w hello instrukcje działania ręcznego, a następnie zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="55779-129">In hello unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with hello values in hello Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="55779-130">Uruchom aplikację RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="55779-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="55779-131">Podręczne, podaj prawidłowe poświadczenia usługi Power Bi i kliknij przycisk hello okna logowania **Akceptuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="55779-131">A login window will pop up, provide your valid PowerBI credentials and click hello **Accept** button.</span></span> <span data-ttu-id="55779-132">Następnie aplikacja hello rozpocznie toorun.</span><span class="sxs-lookup"><span data-stu-id="55779-132">Then hello app will start toorun.</span></span>

   ![Logowanie tooPower analizy Biznesowej](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI pulpitu nawigacyjnego uprawnień](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="55779-135">Logowania tooPowerBI witryny sieci Web i utworzyć pulpit nawigacyjny w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="55779-135">Login tooPowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="55779-136">Teraz są tooconfigure gotowy pulpit nawigacyjny usługi Power BI hello z toogain zaawansowane wizualizacje w czasie rzeczywistym i zwyczaje predykcyjnej rozeznanie vehicle kondycji i wspierającym.</span><span class="sxs-lookup"><span data-stu-id="55779-136">Now, you are ready tooconfigure hello Power BI dashboard with rich visualizations toogain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="55779-137">Trwa około 45 minut tooan godzina toocreate hello wszystkich raportów i skonfigurować hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="55779-137">It takes about 45 minutes tooan hour toocreate all hello reports and configure hello dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="55779-138">Konfigurowanie raportów usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="55779-138">Configure Power BI reports</span></span>
<span data-ttu-id="55779-139">Witaj w czasie rzeczywistym raporty i pulpit nawigacyjny hello zająć o toocomplete 30-45 minut.</span><span class="sxs-lookup"><span data-stu-id="55779-139">hello real-time reports and hello dashboard take about 30-45 minutes toocomplete.</span></span> <span data-ttu-id="55779-140">Przeglądaj zbyt[http://powerbi.com](http://powerbi.com) i logowania.</span><span class="sxs-lookup"><span data-stu-id="55779-140">Browse too[http://powerbi.com](http://powerbi.com) and login.</span></span>

![Logowanie tooPower analizy Biznesowej](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="55779-142">Nowy zestaw danych jest generowany w usłudze Power BI.</span><span class="sxs-lookup"><span data-stu-id="55779-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="55779-143">Kliknij przycisk hello **ConnectedCarsRealtime** zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="55779-143">Click hello **ConnectedCarsRealtime** dataset.</span></span>

![Zestaw danych w czasie rzeczywistym samochodów połączone zaznaczeniu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="55779-145">Zapisz przy użyciu pustego raportu hello **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="55779-145">Save hello blank report using **Ctrl + s**.</span></span>

![Zapisz raport puste](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="55779-147">Podaj nazwę raportu *Vehicle Telemetrii Analytics online w czasie rzeczywistym - raporty*.</span><span class="sxs-lookup"><span data-stu-id="55779-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Podaj nazwę raportu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="55779-149">Raporty w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="55779-149">Real-time reports</span></span>
<span data-ttu-id="55779-150">Istnieją trzy raporty w czasie rzeczywistym, w tym rozwiązaniu:</span><span class="sxs-lookup"><span data-stu-id="55779-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="55779-151">Pojazdów w operacji</span><span class="sxs-lookup"><span data-stu-id="55779-151">Vehicles in operation</span></span>
2. <span data-ttu-id="55779-152">Pojazdów wymagających konserwacji</span><span class="sxs-lookup"><span data-stu-id="55779-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="55779-153">Statystyki kondycji pojazdów</span><span class="sxs-lookup"><span data-stu-id="55779-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="55779-154">Wybierz tooconfigure wszystkie hello trzy raporty w czasie rzeczywistym lub po każdym etapie i kontynuować toohello następnej sekcji konfiguracji hello partii raportów.</span><span class="sxs-lookup"><span data-stu-id="55779-154">You can choose tooconfigure all hello three real-time reports or stop after any stage and proceed toohello next section of configuring hello batch reports.</span></span> <span data-ttu-id="55779-155">Zalecamy toocreate wszystkie hello trzy raporty toovisualize hello pełny wgląd hello ścieżki w czasie rzeczywistym hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="55779-155">We recommend you toocreate all hello three reports toovisualize hello full insights of hello real-time path of hello solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="55779-156">1. Pojazdów w operacji</span><span class="sxs-lookup"><span data-stu-id="55779-156">1. Vehicles in operation</span></span>
<span data-ttu-id="55779-157">Kliknij dwukrotnie **strona 1** i zmień jego nazwę za "Pojazdów w operacji"</span><span class="sxs-lookup"><span data-stu-id="55779-157">Double-click **Page 1** and rename it too“Vehicles in operation”</span></span>  
    <span data-ttu-id="55779-158">![Połączone samochodów - pojazdów w operacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="55779-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="55779-159">Wybierz **vin** pola **pola** i wybierz typ wizualizacji jako **"Karta"**.</span><span class="sxs-lookup"><span data-stu-id="55779-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="55779-160">Wizualizacja karty jest tworzony, jak pokazano na rysunku.</span><span class="sxs-lookup"><span data-stu-id="55779-160">Card visualization is created as shown in figure.</span></span>  
    ![Połączone samochodów — wybierz vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="55779-162">Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-162">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="55779-163">Wybierz **miasta** i **vin** z pól.</span><span class="sxs-lookup"><span data-stu-id="55779-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="55779-164">Zmień wizualizacji zbyt**"Map"**.</span><span class="sxs-lookup"><span data-stu-id="55779-164">Change visualization too**“Map”**.</span></span> <span data-ttu-id="55779-165">Przeciągnij **vin** w obszarze wartości.</span><span class="sxs-lookup"><span data-stu-id="55779-165">Drag **vin** in values area.</span></span> <span data-ttu-id="55779-166">Przeciągnij **miasta** z pól zbyt**legendy** obszaru.</span><span class="sxs-lookup"><span data-stu-id="55779-166">Drag **city** from fields too**Legend** area.</span></span>   
    <span data-ttu-id="55779-167">![Połączone samochodów — karta wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="55779-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="55779-168">Wybierz **format** sekcji z **wizualizacje**, kliknij przycisk **tytuł** i zmień hello **tekst** zbyt**"pojazdów Operacja przez Miasto"**.</span><span class="sxs-lookup"><span data-stu-id="55779-168">Select **format** section from **Visualizations**, click **Title** and change hello **Text** too**“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="55779-169">![Połączone samochodów - pojazdów w operacji przez miasta](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="55779-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="55779-170">Wizualizacja końcowego wygląda jak pokazano na rysunku.</span><span class="sxs-lookup"><span data-stu-id="55779-170">Final visualization looks as shown in figure.</span></span>    
    ![Połączone samochodów - końcowego wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="55779-172">Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-172">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="55779-173">Wybierz **miasta** i **vin**, Zmień typ wizualizacji zbyt**wykres kolumnowy grupowany**.</span><span class="sxs-lookup"><span data-stu-id="55779-173">Select **City** and **vin**, change visualization type too**Clustered Column Chart**.</span></span> <span data-ttu-id="55779-174">Upewnij się, **miasta** w **osi obszaru** i **vin** w **wartość obszaru**</span><span class="sxs-lookup"><span data-stu-id="55779-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="55779-175">Wykres sortowania według **"Liczba vin"**</span><span class="sxs-lookup"><span data-stu-id="55779-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="55779-176">![Połączone samochodów — liczba vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="55779-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="55779-177">Zmień wykres **tytuł** zbyt**"Pojazdów w operacji według miast."**</span><span class="sxs-lookup"><span data-stu-id="55779-177">Change chart **Title** too**“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="55779-178">Kliknij hello **Format** sekcji, a następnie wybierz **kolory danych**, kliknij przycisk hello **"Na"** zbyt**Pokaż wszystko**</span><span class="sxs-lookup"><span data-stu-id="55779-178">Click hello **Format** section, then select **Data Colors**,  Click hello **“On”** too**Show All**</span></span>  
    <span data-ttu-id="55779-179">![Połączone samochodów — Pokaż wszystkie kolory danych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="55779-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="55779-180">Zmiana koloru hello poszczególnych Miasto, klikając ikonę kolorów.</span><span class="sxs-lookup"><span data-stu-id="55779-180">Change hello color of individual city by clicking on color icon.</span></span>  
    ![Połączone samochodów - Zmienianie kolorów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="55779-182">Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-182">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="55779-183">Wybierz **wykres kolumnowy grupowany** wizualizacji z wizualizacji, przeciągnij **miasta** w **osi** obszarze **modelu** w **Legendy** obszaru i **vin** w **wartość** obszaru.</span><span class="sxs-lookup"><span data-stu-id="55779-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="55779-184">![Połączone samochodów - kolumnowy grupowany](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="55779-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="55779-185">![Połączone samochodów - renderowania](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="55779-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="55779-186">Rozmieszczanie wszystkich wizualizacji na tej stronie, jak pokazano na rysunku.</span><span class="sxs-lookup"><span data-stu-id="55779-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Połączone samochodów - wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="55779-188">Raport w czasie rzeczywistym "Pojazdów w operacji" hello została pomyślnie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="55779-188">You have successfully configured hello “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="55779-189">Można kontynuować toocreate hello dalej raportu w czasie rzeczywistym lub zatrzymać w tym miejscu i skonfigurować hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="55779-189">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="55779-190">2. Pojazdów wymagających konserwacji</span><span class="sxs-lookup"><span data-stu-id="55779-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="55779-191">Kliknij przycisk ![Dodaj](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nowy raport, zmień jego nazwę zbyt**"Pojazdów wymagających obsługi"**</span><span class="sxs-lookup"><span data-stu-id="55779-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd a new report, rename it too**“Vehicles Requiring Maintenance”**</span></span>

![Połączone samochodów - pojazdów wymagających konserwacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="55779-193">Wybierz **vin** pól i zmień typ wizualizacji zbyt**karty**.</span><span class="sxs-lookup"><span data-stu-id="55779-193">Select **vin** field and change visualization type too**Card**.</span></span>  
    <span data-ttu-id="55779-194">![Połączone samochodów — karta Vin wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="55779-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="55779-195">Mamy pole o nazwie "MaintenanceLabel" w zestawie danych hello.</span><span class="sxs-lookup"><span data-stu-id="55779-195">We have a field named “MaintenanceLabel” In hello dataset.</span></span> <span data-ttu-id="55779-196">To pole może mieć wartość "0" lub "1"."</span><span class="sxs-lookup"><span data-stu-id="55779-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="55779-197">Ta wartość jest ustawiana przez hello Azure Machine Learning model udostępniane w ramach rozwiązania i zintegrowane z hello ścieżki w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="55779-197">It is set by hello Azure Machine Learning model provisioned as part of solution and integrated with hello real-time path.</span></span> <span data-ttu-id="55779-198">Witaj, wartość "1" oznacza, że vehicle wymaga konserwacji.</span><span class="sxs-lookup"><span data-stu-id="55779-198">hello value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="55779-199">tooadd **poziomu strony** filtr przedstawiający pojazdów danych, które wymagają obsługi:</span><span class="sxs-lookup"><span data-stu-id="55779-199">tooadd a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="55779-200">Przeciągnij hello **"MaintenanceLabel"** pole do **filtrów stron poziomu**.</span><span class="sxs-lookup"><span data-stu-id="55779-200">Drag hello **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="55779-201">![Połączone samochodów — filtry poziomu strony](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="55779-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="55779-202">Kliknij przycisk **podstawowe filtrowanie** w dolnej części filtru poziomu strony MaintenanceLabel menu.</span><span class="sxs-lookup"><span data-stu-id="55779-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="55779-203">![Połączone samochodów — podstawowe filtrowanie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="55779-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="55779-204">Ustaw dla niego wartość filtru zbyt**"1"**  </span><span class="sxs-lookup"><span data-stu-id="55779-204">Set its filter value too**“1”**  </span></span>  
   <span data-ttu-id="55779-205">![Połączone samochodów — wartość filtru](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="55779-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="55779-206">Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-206">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="55779-207">Wybierz **wykres kolumnowy grupowany** z wizualizacji</span><span class="sxs-lookup"><span data-stu-id="55779-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="55779-208">![Połączone samochodów — karta Vind wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="55779-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="55779-209">![Połączone samochodów - kolumnowy grupowany](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="55779-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="55779-210">Przeciągnij pole **modelu** do **osi** obszarze **Vin** za**wartość** obszaru.</span><span class="sxs-lookup"><span data-stu-id="55779-210">Drag field **Model** into **Axis** area, **Vin** too**Value** area.</span></span> <span data-ttu-id="55779-211">Następnie Sortuj wizualizacji przez **liczba vin**.</span><span class="sxs-lookup"><span data-stu-id="55779-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="55779-212">Zmień wykres **tytuł** zbyt**"Pojazdów wymagających obsługi przez model"**</span><span class="sxs-lookup"><span data-stu-id="55779-212">Change chart **Title** too**“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="55779-213">Przeciągnij **vin** pól do **nasycenie kolorów** w **pola** ![pola](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) sekcji **wizualizacji**kartę</span><span class="sxs-lookup"><span data-stu-id="55779-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="55779-214">![Połączone samochodów - nasycenie kolorów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="55779-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="55779-215">Zmień **kolory danych** w wizualizacji z **Format** sekcji</span><span class="sxs-lookup"><span data-stu-id="55779-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="55779-216">Zmień kolor Minimum: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="55779-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="55779-217">Zmień kolor wartości maksymalnej do: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="55779-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="55779-218">![Połączone samochodów — zmiany kolorów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="55779-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="55779-219">![Połączone samochodów — nowe kolory wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="55779-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="55779-220">Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-220">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="55779-221">Wybierz **klastrowanych kolumnowy** z wizualizacji, przeciągnij **vin** pole do **wartość** obszaru, przeciągnij **miasta** pole do **Osi** obszaru.</span><span class="sxs-lookup"><span data-stu-id="55779-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="55779-222">Wykres sortowania przez **"Liczba vin"**.</span><span class="sxs-lookup"><span data-stu-id="55779-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="55779-223">Zmień wykres **tytuł** zbyt**"Pojazdów wymagających obsługi przez Miasto"** </span><span class="sxs-lookup"><span data-stu-id="55779-223">Change chart **Title** too**“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="55779-224">![Połączone samochodów - pojazdów wymagających obsługi przez miasta](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="55779-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="55779-225">Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-225">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="55779-226">Wybierz **karty wielowierszowych** wizualizacji z wizualizacji, przeciągnij **modelu** i **vin** do hello **pola** obszaru.</span><span class="sxs-lookup"><span data-stu-id="55779-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into hello **Fields** area.</span></span>  
<span data-ttu-id="55779-227">![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="55779-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="55779-228">Zmienianie rozmieszczenia wszystkie hello wizualizacji, raport końcowy hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="55779-228">Rearranging all of hello visualization, hello final report looks as follows:</span></span>  
![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="55779-230">Raport w czasie rzeczywistym "Pojazdów wymagających obsługi" hello została pomyślnie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="55779-230">You have successfully configured hello “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="55779-231">Można kontynuować toocreate hello dalej raportu w czasie rzeczywistym lub zatrzymać w tym miejscu i skonfigurować hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="55779-231">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="55779-232">3. Statystyki kondycji pojazdów</span><span class="sxs-lookup"><span data-stu-id="55779-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="55779-233">Kliknij przycisk ![Dodaj](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nowy raport, zmień jego nazwę zbyt**"Statystyki kondycji pojazdów"**</span><span class="sxs-lookup"><span data-stu-id="55779-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd new report, rename it too**“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="55779-234">Wybierz **miernika** wizualizacji z wizualizacji, a następnie przeciągnij hello **szybkości** pole do **wartości, wartość minimalna, wartość maksymalna** obszarów.</span><span class="sxs-lookup"><span data-stu-id="55779-234">Select **Gauge** visualization from visualizations, then drag hello **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="55779-235">![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="55779-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="55779-236">Zmienić domyślne hello agregacji **szybkości** w **wartość obszaru** zbyt**średni**</span><span class="sxs-lookup"><span data-stu-id="55779-236">Change hello default aggregation of **speed** in **Value area** too**Average**</span></span> 

<span data-ttu-id="55779-237">Zmienić domyślne hello agregacji **szybkości** w **obszar minimalny** zbyt**minimalna**</span><span class="sxs-lookup"><span data-stu-id="55779-237">Change hello default aggregation of **speed** in **Minimum area** too**Minimum**</span></span>

<span data-ttu-id="55779-238">Zmienić domyślne hello agregacji **szybkości** w **maksymalny obszar** zbyt**maksymalna**</span><span class="sxs-lookup"><span data-stu-id="55779-238">Change hello default aggregation of **speed** in **Maximum area** too**Maximum**</span></span>

![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="55779-240">Zmień nazwę hello **tytuł miernika** zbyt**"Średnia szybkość"**</span><span class="sxs-lookup"><span data-stu-id="55779-240">Rename hello **Gauge Title** too**“Average speed”**</span></span> 

![Połączone samochodów - miernika](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="55779-242">Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-242">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="55779-243">Podobnie dodać **miernika** dla **średni wydobycie ropy naftowej aparat**, **średni paliwa**, i **aparat średnia temperatura**.</span><span class="sxs-lookup"><span data-stu-id="55779-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="55779-244">Zmień hello domyślnej agregacji pól w każdym miernika zgodnie powyżej kroki opisane w **"Średnia szybkość"** miernika.</span><span class="sxs-lookup"><span data-stu-id="55779-244">Change hello default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Połączone samochodów - mierników](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="55779-246">Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-246">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="55779-247">Wybierz **liniowy i kolumnowy grupowany** z wizualizacji, przeciągnij **miasta** pole do **udostępnionych osi**, przeciągnij **szybkości**, **pól tirepressure i engineoil** do **wartości w kolumnie** obszaru, zmień ich typ agregacji zbyt**średni**.</span><span class="sxs-lookup"><span data-stu-id="55779-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type too**Average**.</span></span> 

<span data-ttu-id="55779-248">Przeciągnij hello **engineTemperature** pole do **wartości wiersza** obszaru, Zmień typ agregacji hello zbyt**średni**.</span><span class="sxs-lookup"><span data-stu-id="55779-248">Drag hello **engineTemperature** field into **Line Values** area, change hello  aggregation type too**Average**.</span></span> 

![Połączone samochodów - pola wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="55779-250">Zmień wykres hello **tytuł** za**"Średnia szybkość, opona wykorzystania, aparat wydobycie ropy naftowej i temperatury aparat"**.</span><span class="sxs-lookup"><span data-stu-id="55779-250">Change hello chart **Title** too**“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Połączone samochodów - pola wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="55779-252">Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-252">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="55779-253">Wybierz **właściwości** wizualizacji z wizualizacji, przeciągnij hello **modelu** pole do hello **grupy** obszarów i pól hello przeciągania  **MaintenanceProbability** do hello **wartości** obszaru.</span><span class="sxs-lookup"><span data-stu-id="55779-253">Select **Treemap** visualization from visualizations, drag hello **Model** field into hello **Group** area, and drag hello field **MaintenanceProbability** into hello **Values** area.</span></span>

<span data-ttu-id="55779-254">Zmień wykres hello **tytuł** za**"Modele pojazdów wymagających obsługi"**.</span><span class="sxs-lookup"><span data-stu-id="55779-254">Change hello chart **Title** too**“Vehicle models requiring maintenance”**.</span></span>

![Połączone samochodów — Zmień tytuł wykresu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="55779-256">Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-256">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="55779-257">Wybierz **100% skumulowany wykres słupkowy** z wizualizacji, przeciągnij hello **miasta** pole do hello **osi** obszaru i przeciągnij hello **MaintenanceProbability**, **RecallProbability** pola na powitania **wartość** obszaru.</span><span class="sxs-lookup"><span data-stu-id="55779-257">Select **100% Stacked Bar Chart** from visualization, drag hello **city** field into hello **Axis** area, and drag hello **MaintenanceProbability**, **RecallProbability** fields into hello **Value** area.</span></span>

![Połączone samochodów — Dodawanie nowej wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="55779-259">Kliknij przycisk **Format**, wybierz pozycję **kolory danych**i ustaw hello **MaintenanceProbability** toohello wartości koloru **"F2C80F"**.</span><span class="sxs-lookup"><span data-stu-id="55779-259">Click **Format**, select **Data Colors**, and set hello **MaintenanceProbability** color toohello value **“F2C80F”**.</span></span>

<span data-ttu-id="55779-260">Zmień hello **tytuł** z hello wykresu za**"Prawdopodobieństwo z Vehicle konserwacji & Wycofaj przez Miasto"**.</span><span class="sxs-lookup"><span data-stu-id="55779-260">Change hello **Title** of hello chart too**“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Połączone samochodów — Dodawanie nowej wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="55779-262">Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-262">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="55779-263">Wybierz **wykres warstwowy** z wizualizacji z wizualizacji, przeciągnij hello **modelu** pole do hello **osi** obszaru i przeciągnij hello **engineOil, tirepressure, szybkość i MaintenanceProbability** pola na powitania **wartości** obszaru.</span><span class="sxs-lookup"><span data-stu-id="55779-263">Select **Area Chart** from visualization from visualizations, drag hello **Model** field into hello **Axis** area, and drag hello **engineOil, tirepressure, speed and MaintenanceProbability** fields into hello **Values** area.</span></span> <span data-ttu-id="55779-264">Zmień ich typ agregacji zbyt**"Średni"**.</span><span class="sxs-lookup"><span data-stu-id="55779-264">Change their aggregation type too**“Average”**.</span></span> 

![Połączone samochodów — Zmień typ agregacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="55779-266">Zmień tytuł hello wykresu hello zbyt**"Średni aparat wydobycie ropy naftowej, opona prawdopodobieństwo wykorzystania, szybkość i konserwacja przez model"**.</span><span class="sxs-lookup"><span data-stu-id="55779-266">Change hello title of hello chart too**“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Połączone samochodów — Zmień tytuł wykresu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="55779-268">Kliknij hello pusty obszar tooadd nowej wizualizacji:</span><span class="sxs-lookup"><span data-stu-id="55779-268">Click hello blank area tooadd new visualization:</span></span>

1. <span data-ttu-id="55779-269">Wybierz **wykres punktowy** wizualizacji z wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="55779-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="55779-270">Przeciągnij hello **modelu** pole do hello **szczegóły** i **legendy** obszaru.</span><span class="sxs-lookup"><span data-stu-id="55779-270">Drag hello **Model** field into hello **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="55779-271">Przeciągnij hello **paliwa** pole do hello **osi x** obszaru, zmień agregacji hello zbyt**średni**.</span><span class="sxs-lookup"><span data-stu-id="55779-271">Drag hello **fuel** field into hello **X-Axis** area, change hello aggregation too**Average**.</span></span>
4. <span data-ttu-id="55779-272">Przeciągnij **engineTemparature** do **osi y obszaru**, zmień agregacji hello zbyt**średni**</span><span class="sxs-lookup"><span data-stu-id="55779-272">Drag **engineTemparature** into **Y-Axis area**, change hello aggregation too**Average**</span></span>
5. <span data-ttu-id="55779-273">Przeciągnij hello **vin** pole do hello **rozmiar** obszaru.</span><span class="sxs-lookup"><span data-stu-id="55779-273">Drag hello **vin** field into hello **Size** area.</span></span>

![Połączone samochodów — Dodawanie nowej wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="55779-275">Zmień wykres hello **tytuł** za**"Średnie paliwa, aparat temperatury przez Model"**.</span><span class="sxs-lookup"><span data-stu-id="55779-275">Change hello chart **Title** too**“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Połączone samochodów — Zmień tytuł wykresu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="55779-277">raport końcowy Hello będzie wyglądać jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="55779-277">hello final report will look like as shown below.</span></span>

![Połączony raport końcowy samochodów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a><span data-ttu-id="55779-279">Wizualizacje numeru PIN z pulpitu nawigacyjnego hello raporty toohello w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="55779-279">Pin visualizations from hello reports toohello real-time dashboard</span></span>
<span data-ttu-id="55779-280">Utwórz pusty pulpit nawigacyjny, klikając hello plus ikona tooDashboards dalej.</span><span class="sxs-lookup"><span data-stu-id="55779-280">Create a blank dashboard by clicking on hello plus icon next tooDashboards.</span></span> <span data-ttu-id="55779-281">Można określić nazwę "Pulpitu nawigacyjnego Analytics Vehicle Telemetrii"</span><span class="sxs-lookup"><span data-stu-id="55779-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Połączone samochodów pulpitu nawigacyjnego](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="55779-283">Wizualizacja PIN hello z hello powyżej toohello raporty w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="55779-283">Pin hello visualization from hello above reports toohello dashboard.</span></span> 

![Połączone samochodów pulpitu nawigacyjnego](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="55779-285">pulpit nawigacyjny Hello powinna wyglądać następująco po wszystkich hello, które są tworzone trzy raporty i hello odpowiadającego wizualizacje przypiętych toohello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="55779-285">hello dashboard should look as follows when all hello three reports are created and hello corresponding visualizations are pinned toohello dashboard.</span></span> <span data-ttu-id="55779-286">Jeśli nie utworzono wszystkich raportów hello, pulpit nawigacyjny może wyglądać inaczej.</span><span class="sxs-lookup"><span data-stu-id="55779-286">If you have not created all hello reports, your dashboard could look different.</span></span> 

![Połączone samochodów pulpitu nawigacyjnego](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="55779-288">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="55779-288">Congratulations!</span></span> <span data-ttu-id="55779-289">Pomyślnie utworzono hello w czasie rzeczywistym pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="55779-289">You have successfully created hello real-time dashboard.</span></span> <span data-ttu-id="55779-290">Kontynuując tooexecute CarEventGenerator.exe i RealtimeDashboardApp.exe, powinny pojawić się aktualizacje na żywo na powitania pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="55779-290">As you continue tooexecute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on hello dashboard.</span></span> <span data-ttu-id="55779-291">Powinien upłynąć hello toocomplete too15 około 10 minut z następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="55779-291">It should take about 10 too15 minutes toocomplete hello following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="55779-292">Konfiguracja pulpitu nawigacyjnego przetwarzania wsadowego usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="55779-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="55779-293">Trwa około dwie godziny (od hello pomyślnego wdrożenia hello) dla partii tooend zakończenia hello przetwarzania potoku toofinish wykonywania, a przetworzyć wygenerowanych danych, przez które roku.</span><span class="sxs-lookup"><span data-stu-id="55779-293">It takes about two hours (from hello successful completion of hello deployment) for hello end tooend batch processing pipeline toofinish execution and process a year worth of generated data.</span></span> <span data-ttu-id="55779-294">Dlatego poczekaj hello przetwarzania toofinish przed kontynuowaniem hello następne kroki.</span><span class="sxs-lookup"><span data-stu-id="55779-294">So wait for hello processing toofinish before proceeding with hello next steps.</span></span> 
> 
> 

<span data-ttu-id="55779-295">**Pobierz plik projektanta usługi Power BI hello**</span><span class="sxs-lookup"><span data-stu-id="55779-295">**Download hello Power BI designer file**</span></span>

* <span data-ttu-id="55779-296">Wstępnie skonfigurowane pliku projektanta usługi Power BI wchodzi w skład wdrożenia hello instrukcje działania ręczne</span><span class="sxs-lookup"><span data-stu-id="55779-296">A pre-configured Power BI designer file is included as part of hello deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="55779-297">Poszukaj 2.</span><span class="sxs-lookup"><span data-stu-id="55779-297">Look for 2.</span></span> <span data-ttu-id="55779-298">Instalator usługi Power BI partii przetwarzania w pulpicie nawigacyjnym możesz pobrać hello szablonu usługi Power BI dla pulpitu nawigacyjnego przetwarzania wsadowego nosi nazwę **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="55779-298">Setup PowerBI batch processing dashboard You can download hello PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="55779-299">Zapisz lokalnie</span><span class="sxs-lookup"><span data-stu-id="55779-299">Save locally</span></span>

<span data-ttu-id="55779-300">**Konfigurowanie raportów usługi Power BI**</span><span class="sxs-lookup"><span data-stu-id="55779-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="55779-301">Otwórz hello pliku projektanta "**ConnectedCarsPbiReport.pbix**" przy użyciu Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="55779-301">Open hello designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="55779-302">Jeśli nie już zainstalujesz hello Power BI Desktop z [instalacji Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="55779-302">If you do not already have, install hello Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="55779-303">Kliknij przycisk hello **edytowanie zapytań**.</span><span class="sxs-lookup"><span data-stu-id="55779-303">Click hello **Edit Queries**.</span></span>

![Edytuj zapytanie usługi Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="55779-305">Kliknij dwukrotnie hello **źródła**.</span><span class="sxs-lookup"><span data-stu-id="55779-305">Double-click hello **Source**.</span></span>

![Źródło usługi Power BI zbioru](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="55779-307">Zaktualizuj parametry połączenia serwera z hello Azure SQL server, które uzyskano udostępnione jako część wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="55779-307">Update Server connection string with hello Azure SQL server that got provisioned as part of hello deployment.</span></span>  <span data-ttu-id="55779-308">Szukaj w instrukcjach operacji ręcznego hello w obszarze</span><span class="sxs-lookup"><span data-stu-id="55779-308">Look in hello Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="55779-309">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="55779-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="55779-310">Serwer: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="55779-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="55779-311">Baza danych: connectedcar</span><span class="sxs-lookup"><span data-stu-id="55779-311">Database: connectedcar</span></span>
    * <span data-ttu-id="55779-312">Nazwa użytkownika: nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="55779-312">Username: username</span></span>
    * <span data-ttu-id="55779-313">Hasło: Hasło programu SQL server można zarządzać z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="55779-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="55779-314">Pozostaw **bazy danych** jako *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="55779-314">Leave **Database** as *connectedcar*.</span></span>

![Ustaw bazę danych usługi Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="55779-316">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="55779-316">Click **OK**.</span></span>
* <span data-ttu-id="55779-317">Zobaczysz **poświadczenia systemu Windows** kartę domyślnie zaznaczone, zmień ją za**bazy danych poświadczeń** , klikając **bazy danych** kartę w prawym rogu.</span><span class="sxs-lookup"><span data-stu-id="55779-317">You will see **Windows credential** tab selected by default, change it too**Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="55779-318">Podaj hello **Username** i **hasło** Twojej bazy danych SQL Azure, która została określona podczas jego wdrażania instalacji.</span><span class="sxs-lookup"><span data-stu-id="55779-318">Provide hello **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Podaj poświadczenia bazy danych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="55779-320">Kliknij przycisk **połączenia**</span><span class="sxs-lookup"><span data-stu-id="55779-320">Click **Connect**</span></span>
* <span data-ttu-id="55779-321">Powtórz hello powyżej kroki dla każdego hello trzy pozostałe zapytań w okienku po prawej stronie, a następnie zaktualizuj szczegóły połączenia źródła danych hello.</span><span class="sxs-lookup"><span data-stu-id="55779-321">Repeat hello above steps for each of hello three remaining queries present at right pane, and then update hello data source connection details.</span></span>
* <span data-ttu-id="55779-322">Kliknij przycisk **Zamknij i załadować**.</span><span class="sxs-lookup"><span data-stu-id="55779-322">Click **Close and Load**.</span></span> <span data-ttu-id="55779-323">Power BI Desktop pliku z zestawów danych są tooSQL połączonych tabel bazy danych Azure.</span><span class="sxs-lookup"><span data-stu-id="55779-323">Power BI Desktop file datasets are connected tooSQL Azure Database tables.</span></span>
* <span data-ttu-id="55779-324">**Zamknij** pliku Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="55779-324">**Close** Power BI Desktop file.</span></span>

![Zamknij usługę Power BI desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="55779-326">Kliknij przycisk **zapisać** przycisk toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="55779-326">Click **Save** button toosave hello changes.</span></span> 

<span data-ttu-id="55779-327">Wszystkie raporty hello odpowiadającego ścieżka przetwarzania wsadowego toohello w rozwiązaniu hello został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="55779-327">You have now configured all hello reports corresponding toohello batch processing path in hello solution.</span></span> 

## <a name="upload-toopowerbicom"></a><span data-ttu-id="55779-328">Przekaż zbyt*witrynie powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="55779-328">Upload too*powerbi.com*</span></span>
1. <span data-ttu-id="55779-329">Przejdź portalu sieci web usługi Power BI toohello http://powerbi.com i logowania.</span><span class="sxs-lookup"><span data-stu-id="55779-329">Navigate toohello Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="55779-330">Kliknij przycisk **pobieranie danych**</span><span class="sxs-lookup"><span data-stu-id="55779-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="55779-331">Przekaż hello Power BI Desktop pliku.</span><span class="sxs-lookup"><span data-stu-id="55779-331">Upload hello Power BI Desktop File.</span></span>  
4. <span data-ttu-id="55779-332">tooupload, kliknij przycisk **Pobierz dane -> pliki -> pliku lokalnego**</span><span class="sxs-lookup"><span data-stu-id="55779-332">tooupload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="55779-333">Przejdź toohello **"**ConnectedCarsPbiReport.pbix**"**</span><span class="sxs-lookup"><span data-stu-id="55779-333">Navigate toohello **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="55779-334">Po przekazaniu pliku hello można nawigować tooyour wstecz obszar roboczy usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="55779-334">Once hello file is uploaded, you will be navigated back tooyour Power BI work space.</span></span>  

<span data-ttu-id="55779-335">Zestaw danych, raportów i pustego pulpitu nawigacyjnego zostanie utworzona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="55779-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="55779-336">Numer PIN wykresy nowego pulpitu nawigacyjnego tooa o nazwie **pulpitu nawigacyjnego Analytics Telemetrii Vehicle** w **usługi Power BI**.</span><span class="sxs-lookup"><span data-stu-id="55779-336">Pin charts tooa new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="55779-337">Kliknij pozycję puste pulpit nawigacyjny hello utworzone powyżej, a następnie przejdź toohello **raporty** kliknij sekcję hello nowo przekazać raportu.</span><span class="sxs-lookup"><span data-stu-id="55779-337">Click hello blank dashboard created above and then navigate toohello **Reports** section click hello newly uploaded report.</span></span>  

![Vehicle Telemetrii Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="55779-339">**Uwaga hello raport ma sześć stron:**</span><span class="sxs-lookup"><span data-stu-id="55779-339">**Note hello report has six pages:**</span></span>  
<span data-ttu-id="55779-340">Strona 1: Gęstość Vehicle</span><span class="sxs-lookup"><span data-stu-id="55779-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="55779-341">Strona 2: Kondycja vehicle w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="55779-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="55779-342">Strona 3: Agresywnie zmiennych pojazdów</span><span class="sxs-lookup"><span data-stu-id="55779-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="55779-343">4 strony: Pojazdów odwołane</span><span class="sxs-lookup"><span data-stu-id="55779-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="55779-344">5 strony: Efektywne zmiennych pojazdów paliwa</span><span class="sxs-lookup"><span data-stu-id="55779-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="55779-345">6 strony: Logo firmy Contoso</span><span class="sxs-lookup"><span data-stu-id="55779-345">Page 6: Contoso Logo</span></span>  

![Połączone samochodów Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="55779-347">**Z 3 stron**, przypiąć hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="55779-347">**From Page 3**, pin hello following:</span></span>  

1. <span data-ttu-id="55779-348">Liczba VIN</span><span class="sxs-lookup"><span data-stu-id="55779-348">Count of VIN</span></span>  
   ![Połączone samochodów Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="55779-350">Agresywnie zmiennych pojazdów przez model — wykresu wykresu kaskadowego</span><span class="sxs-lookup"><span data-stu-id="55779-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Vehicle Telemetrii - Pin wykresy 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="55779-352">**Od 5 strony**, przypiąć hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="55779-352">**From Page 5**, pin hello following:</span></span> 

1. <span data-ttu-id="55779-353">Liczba vin</span><span class="sxs-lookup"><span data-stu-id="55779-353">Count of vin</span></span>    
   ![Vehicle Telemetrii - Pin wykresy 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="55779-355">Paliwa pojazdów wydajne przez model: kolumnowy grupowany</span><span class="sxs-lookup"><span data-stu-id="55779-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Vehicle Telemetrii - Pin wykresy 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="55779-357">**Z 4 strony**, przypiąć hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="55779-357">**From Page 4**, pin hello following:</span></span>  

1. <span data-ttu-id="55779-358">Liczba vin</span><span class="sxs-lookup"><span data-stu-id="55779-358">Count of vin</span></span>  
   ![Vehicle Telemetrii - Pin wykresy 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="55779-360">Odwołane pojazdów miejscowość, model: właściwości</span><span class="sxs-lookup"><span data-stu-id="55779-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Vehicle Telemetrii - Pin wykresy 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="55779-362">**Od 6 do strony**, przypiąć hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="55779-362">**From Page 6**, pin hello following:</span></span>  

1. <span data-ttu-id="55779-363">Logo firmy Contoso silniki</span><span class="sxs-lookup"><span data-stu-id="55779-363">Contoso Motors logo</span></span>  
   ![Vehicle Telemetrii - Pin wykresy 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="55779-365">**Organizowanie hello pulpitu nawigacyjnego**</span><span class="sxs-lookup"><span data-stu-id="55779-365">**Organize hello dashboard**</span></span>  

1. <span data-ttu-id="55779-366">Przejdź do pulpitu nawigacyjnego toohello</span><span class="sxs-lookup"><span data-stu-id="55779-366">Navigate toohello dashboard</span></span>
2. <span data-ttu-id="55779-367">Umieść kursor nad każdym wykresu i zmień jego nazwę oparte na powitania nazewnictwa w hello pełny pulpit nawigacyjny obraz poniżej.</span><span class="sxs-lookup"><span data-stu-id="55779-367">Hover over each chart and rename it based on hello naming provided in hello complete dashboard image below.</span></span> <span data-ttu-id="55779-368">Przenieś również wykresy hello wokół toolook, takich jak pulpit nawigacyjny hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="55779-368">Also move hello charts around toolook like hello dashboard below.</span></span>  
   ![Vehicle Telemetrii - organizowanie pulpitu nawigacyjnego 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle Telemetrii Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="55779-371">Jeśli utworzono wszystkich raportów hello, jak wspomniano w tym dokumencie hello końcowego zakończonych pulpitu nawigacyjnego powinien wyglądać powitania po rysunku.</span><span class="sxs-lookup"><span data-stu-id="55779-371">If you have created all hello reports as mentioned in this document, hello final completed dashboard should look like hello following figure.</span></span> 

![Vehicle Telemetrii - organizowanie pulpitu nawigacyjnego 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="55779-373">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="55779-373">Congratulations!</span></span> <span data-ttu-id="55779-374">Pomyślnie utworzono hello raporty i hello toogain pulpitu nawigacyjnego w czasie rzeczywistym, predykcyjnej i zwyczaje rozeznanie partii vehicle kondycji i zwiększa.</span><span class="sxs-lookup"><span data-stu-id="55779-374">You have successfully created hello reports and hello dashboard toogain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
