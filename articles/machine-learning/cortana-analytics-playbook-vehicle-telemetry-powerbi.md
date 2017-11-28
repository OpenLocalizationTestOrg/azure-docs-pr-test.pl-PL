---
title: "Power BI pulpit nawigacyjny kondycji vehicle i wspierającym zwyczaje - Azure | Dokumentacja firmy Microsoft"
description: "Korzystanie z możliwości Cortana Intelligence, aby uzyskać wgląd w czasie rzeczywistym oraz predykcyjnej na vehicle kondycji i wspierającym zwyczaje."
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
ms.openlocfilehash: f880aceb1657ffdfe909b73f175b9673d9ab02cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="c7836-103">Instrukcje instalacji pulpitu nawigacyjnego programu Power BI szablon rozwiązania vehicle telemetrii analityka</span><span class="sxs-lookup"><span data-stu-id="c7836-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="c7836-104">To **menu** łącza do rozdziały tego podręcznika dotyczącego.</span><span class="sxs-lookup"><span data-stu-id="c7836-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="c7836-105">Rozwiązania analizy Telemetrii Vehicle ilustrację jak przedstawicielstw samochodu handlowych, producentów samochodów i ubezpieczeń mogą korzystać z funkcji Cortana Intelligence w celu uzyskania w czasie rzeczywistym i zwyczaje predykcyjnej rozeznanie vehicle kondycji i kierowania do ulepszenia dysku w obszarze klienta wystąpić R & D i kampanii marketingowych.</span><span class="sxs-lookup"><span data-stu-id="c7836-105">The Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits to drive improvements in the area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="c7836-106">Ten dokument zawiera instrukcje krok po kroku dotyczące sposobu konfigurowania raportów usługi Power BI i pulpitu nawigacyjnego po wdrożeniu rozwiązania w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c7836-106">This document contains step by step instructions on how you can configure the Power BI reports and dashboard once the solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c7836-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c7836-107">Prerequisites</span></span>
1. <span data-ttu-id="c7836-108">Wdrażanie [analizy Telemetrii](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) rozwiązania</span><span class="sxs-lookup"><span data-stu-id="c7836-108">Deploy the [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="c7836-109">Zainstaluj program Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c7836-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="c7836-110">[Subskrypcji platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7836-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="c7836-111">Jeśli nie masz subskrypcji platformy Azure, Rozpoczynanie pracy z bezpłatnej subskrypcji Azure</span><span class="sxs-lookup"><span data-stu-id="c7836-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="c7836-112">Konto usługi Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="c7836-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="c7836-113">Składników pakietu Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="c7836-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="c7836-114">W ramach szablon rozwiązania analizy Telemetrii Vehicle następujące usługi Cortana Intelligence są wdrażane w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c7836-114">As part of the Vehicle Telemetry Analytics solution template, the following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="c7836-115">**Centrum zdarzeń** służy do wprowadzania miliony zdarzeń telemetrii vehicle na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c7836-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="c7836-116">**Analiza strumienia** do uzyskania wgląd w czasie rzeczywistym w kondycję vehicle i będzie się powtarzał tych danych do długoterminowego przechowywania dla bardziej zaawansowane funkcje analizy partii.</span><span class="sxs-lookup"><span data-stu-id="c7836-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="c7836-117">**Machine Learning** wykrywania anomalii w czasie rzeczywistym i przetwarzanie wsadowe, aby uzyskać wgląd predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="c7836-117">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="c7836-118">**HDInsight** jest wykorzystywana do przekształcania danych na dużą skalę</span><span class="sxs-lookup"><span data-stu-id="c7836-118">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="c7836-119">**Fabryka danych** obsługuje aranżacji, Planowanie zarządzania zasobami i monitorowania w potoku przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="c7836-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>

<span data-ttu-id="c7836-120">**Power BI** daje to rozwiązanie sformatowanego pulpitu nawigacyjnego w czasie rzeczywistym danych i wizualizacji analizy predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="c7836-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="c7836-121">Rozwiązanie używa dwóch różnych źródeł danych: **symulowane sygnały vehicle i danych diagnostycznych** i **katalogu vehicle**.</span><span class="sxs-lookup"><span data-stu-id="c7836-121">The solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="c7836-122">Symulator telematyki vehicle wchodzi w skład tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c7836-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="c7836-123">Emituje informacje diagnostyczne, a sygnały odpowiadającej stan mechanizm i zwiększają wzorca w danym punkcie w czasie.</span><span class="sxs-lookup"><span data-stu-id="c7836-123">It emits diagnostic information and signals corresponding to the state of the vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="c7836-124">Katalog Vehicle to odwołanie do zestawu danych zawierającego VIN do mapowania modelu</span><span class="sxs-lookup"><span data-stu-id="c7836-124">The Vehicle Catalog is a reference dataset containing VIN to model mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="c7836-125">Power BI pulpitu nawigacyjnego przygotowania</span><span class="sxs-lookup"><span data-stu-id="c7836-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="c7836-126">Pulpit nawigacyjny Instalatora Power BI w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="c7836-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="c7836-127">**Uruchom aplikację w czasie rzeczywistym pulpitu nawigacyjnego** po zakończeniu wdrożenia należy postępuj zgodnie z instrukcjami działania ręczne</span><span class="sxs-lookup"><span data-stu-id="c7836-127">**Start the real-time dashboard application** Once the deployment is completed, you should follow the Manual Operation Instructions</span></span>

* <span data-ttu-id="c7836-128">Pobierz aplikację pulpitu nawigacyjnego w czasie rzeczywistym RealtimeDashboardApp.zip i Rozpakuj go.</span><span class="sxs-lookup"><span data-stu-id="c7836-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="c7836-129">W folderze rozpakowane Otwórz plik konfiguracji aplikacji 'RealtimeDashboardApp.exe.config' appSettings Zamień Eventhub, magazynu obiektów Blob i ML połączeń usługi z wartości w instrukcji działania ręczne i Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="c7836-129">In the unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with the values in the Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="c7836-130">Uruchom aplikację RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="c7836-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="c7836-131">Podręczne, podaj prawidłowe poświadczenia usługi Power Bi i kliknij przycisk okna logowania **Akceptuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c7836-131">A login window will pop up, provide your valid PowerBI credentials and click the **Accept** button.</span></span> <span data-ttu-id="c7836-132">Następnie uruchomi aplikację do uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="c7836-132">Then the app will start to run.</span></span>

   ![Zaloguj się do usługi Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI pulpitu nawigacyjnego uprawnień](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="c7836-135">Zaloguj się do witryny sieci Web usługi Power Bi i utworzyć pulpit nawigacyjny w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="c7836-135">Login to PowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="c7836-136">Teraz można przystąpić do konfigurowania pulpit nawigacyjny usługi Power BI z wizualizacjami sformatowanego uzyskanie w czasie rzeczywistym i zwyczaje predykcyjnej rozeznanie vehicle kondycji i wspierającym.</span><span class="sxs-lookup"><span data-stu-id="c7836-136">Now, you are ready to configure the Power BI dashboard with rich visualizations to gain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="c7836-137">Trwa około 45 minut na godziny, aby utworzyć wszystkich raportów i skonfigurować pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7836-137">It takes about 45 minutes to an hour to create all the reports and configure the dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="c7836-138">Konfigurowanie raportów usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="c7836-138">Configure Power BI reports</span></span>
<span data-ttu-id="c7836-139">W czasie rzeczywistym raporty i pulpit nawigacyjny zająć około 30 do 45 minut, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="c7836-139">The real-time reports and the dashboard take about 30-45 minutes to complete.</span></span> <span data-ttu-id="c7836-140">Przejdź do [http://powerbi.com](http://powerbi.com) i logowania.</span><span class="sxs-lookup"><span data-stu-id="c7836-140">Browse to [http://powerbi.com](http://powerbi.com) and login.</span></span>

![Zaloguj się do usługi Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="c7836-142">Nowy zestaw danych jest generowany w usłudze Power BI.</span><span class="sxs-lookup"><span data-stu-id="c7836-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="c7836-143">Kliknij przycisk **ConnectedCarsRealtime** zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="c7836-143">Click the **ConnectedCarsRealtime** dataset.</span></span>

![Zestaw danych w czasie rzeczywistym samochodów połączone zaznaczeniu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="c7836-145">Zapisz przy użyciu pustego raportu **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="c7836-145">Save the blank report using **Ctrl + s**.</span></span>

![Zapisz raport puste](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="c7836-147">Podaj nazwę raportu *Vehicle Telemetrii Analytics online w czasie rzeczywistym - raporty*.</span><span class="sxs-lookup"><span data-stu-id="c7836-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Podaj nazwę raportu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="c7836-149">Raporty w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="c7836-149">Real-time reports</span></span>
<span data-ttu-id="c7836-150">Istnieją trzy raporty w czasie rzeczywistym, w tym rozwiązaniu:</span><span class="sxs-lookup"><span data-stu-id="c7836-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="c7836-151">Pojazdów w operacji</span><span class="sxs-lookup"><span data-stu-id="c7836-151">Vehicles in operation</span></span>
2. <span data-ttu-id="c7836-152">Pojazdów wymagających konserwacji</span><span class="sxs-lookup"><span data-stu-id="c7836-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="c7836-153">Statystyki kondycji pojazdów</span><span class="sxs-lookup"><span data-stu-id="c7836-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="c7836-154">Można skonfigurować wszystkie trzy raporty w czasie rzeczywistym lub po każdym etapie i przejdź do następnej sekcji konfigurowania raportów partii.</span><span class="sxs-lookup"><span data-stu-id="c7836-154">You can choose to configure all the three real-time reports or stop after any stage and proceed to the next section of configuring the batch reports.</span></span> <span data-ttu-id="c7836-155">Firma Microsoft zaleca Utwórz trzy raporty w celu wizualizacji pełny wgląd w czasie rzeczywistym ścieżki rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c7836-155">We recommend you to create all the three reports to visualize the full insights of the real-time path of the solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="c7836-156">1. Pojazdów w operacji</span><span class="sxs-lookup"><span data-stu-id="c7836-156">1. Vehicles in operation</span></span>
<span data-ttu-id="c7836-157">Kliknij dwukrotnie **strona 1** i zmień jego nazwę na "Pojazdów w operacji"</span><span class="sxs-lookup"><span data-stu-id="c7836-157">Double-click **Page 1** and rename it to “Vehicles in operation”</span></span>  
    <span data-ttu-id="c7836-158">![Połączone samochodów - pojazdów w operacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="c7836-159">Wybierz **vin** pola **pola** i wybierz typ wizualizacji jako **"Karta"**.</span><span class="sxs-lookup"><span data-stu-id="c7836-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="c7836-160">Wizualizacja karty jest tworzony, jak pokazano na rysunku.</span><span class="sxs-lookup"><span data-stu-id="c7836-160">Card visualization is created as shown in figure.</span></span>  
    ![Połączone samochodów — wybierz vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="c7836-162">Kliknij obszar puste, aby dodać nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-162">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c7836-163">Wybierz **miasta** i **vin** z pól.</span><span class="sxs-lookup"><span data-stu-id="c7836-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="c7836-164">Zmień wizualizacji do **"Map"**.</span><span class="sxs-lookup"><span data-stu-id="c7836-164">Change visualization to **“Map”**.</span></span> <span data-ttu-id="c7836-165">Przeciągnij **vin** w obszarze wartości.</span><span class="sxs-lookup"><span data-stu-id="c7836-165">Drag **vin** in values area.</span></span> <span data-ttu-id="c7836-166">Przeciągnij **miasta** z pola do **legendy** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c7836-166">Drag **city** from fields to **Legend** area.</span></span>   
    <span data-ttu-id="c7836-167">![Połączone samochodów — karta wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="c7836-168">Wybierz **format** sekcji z **wizualizacje**, kliknij przycisk **tytuł** i zmienić **tekst** do **"pojazdów w operacji według miast"**.</span><span class="sxs-lookup"><span data-stu-id="c7836-168">Select **format** section from **Visualizations**, click **Title** and change the **Text** to **“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="c7836-169">![Połączone samochodów - pojazdów w operacji przez miasta](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="c7836-170">Wizualizacja końcowego wygląda jak pokazano na rysunku.</span><span class="sxs-lookup"><span data-stu-id="c7836-170">Final visualization looks as shown in figure.</span></span>    
    ![Połączone samochodów - końcowego wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="c7836-172">Kliknij obszar puste, aby dodać nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-172">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c7836-173">Wybierz **miasta** i **vin**, Zmień typ wizualizacji do **wykres kolumnowy grupowany**.</span><span class="sxs-lookup"><span data-stu-id="c7836-173">Select **City** and **vin**, change visualization type to **Clustered Column Chart**.</span></span> <span data-ttu-id="c7836-174">Upewnij się, **miasta** w **osi obszaru** i **vin** w **wartość obszaru**</span><span class="sxs-lookup"><span data-stu-id="c7836-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="c7836-175">Wykres sortowania według **"Liczba vin"**</span><span class="sxs-lookup"><span data-stu-id="c7836-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="c7836-176">![Połączone samochodów — liczba vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="c7836-177">Zmień wykres **tytuł** do **"Pojazdów w operacji według miast."**</span><span class="sxs-lookup"><span data-stu-id="c7836-177">Change chart **Title** to **“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="c7836-178">Kliknij przycisk **Format** sekcji, a następnie wybierz **kolory danych**, kliknij przycisk **"Na"** do **Pokaż wszystko**</span><span class="sxs-lookup"><span data-stu-id="c7836-178">Click the **Format** section, then select **Data Colors**,  Click the **“On”** to **Show All**</span></span>  
    <span data-ttu-id="c7836-179">![Połączone samochodów — Pokaż wszystkie kolory danych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="c7836-180">Zmiana koloru poszczególnych Miasto, klikając ikonę kolorów.</span><span class="sxs-lookup"><span data-stu-id="c7836-180">Change the color of individual city by clicking on color icon.</span></span>  
    ![Połączone samochodów - Zmienianie kolorów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="c7836-182">Kliknij obszar puste, aby dodać nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-182">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c7836-183">Wybierz **wykres kolumnowy grupowany** wizualizacji z wizualizacji, przeciągnij **miasta** w **osi** obszarze **modelu** w **Legendy** obszaru i **vin** w **wartość** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c7836-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="c7836-184">![Połączone samochodów - kolumnowy grupowany](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="c7836-185">![Połączone samochodów - renderowania](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="c7836-186">Rozmieszczanie wszystkich wizualizacji na tej stronie, jak pokazano na rysunku.</span><span class="sxs-lookup"><span data-stu-id="c7836-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Połączone samochodów - wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="c7836-188">Raport w czasie rzeczywistym "Pojazdów w operacji" została pomyślnie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="c7836-188">You have successfully configured the “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="c7836-189">Możesz przejść do tworzenia następnej raportu w czasie rzeczywistym lub zatrzymać w tym miejscu i skonfigurować pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7836-189">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="c7836-190">2. Pojazdów wymagających konserwacji</span><span class="sxs-lookup"><span data-stu-id="c7836-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="c7836-191">Kliknij przycisk ![Dodaj](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) Aby dodać nowy raport, zmienić jego nazwę na **"Pojazdów wymagających obsługi"**</span><span class="sxs-lookup"><span data-stu-id="c7836-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report, rename it to **“Vehicles Requiring Maintenance”**</span></span>

![Połączone samochodów - pojazdów wymagających konserwacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="c7836-193">Wybierz **vin** pól i zmień typ wizualizacji do **karty**.</span><span class="sxs-lookup"><span data-stu-id="c7836-193">Select **vin** field and change visualization type to **Card**.</span></span>  
    <span data-ttu-id="c7836-194">![Połączone samochodów — karta Vin wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="c7836-195">Mamy pole o nazwie "MaintenanceLabel" w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="c7836-195">We have a field named “MaintenanceLabel” In the dataset.</span></span> <span data-ttu-id="c7836-196">To pole może mieć wartość "0" lub "1"."</span><span class="sxs-lookup"><span data-stu-id="c7836-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="c7836-197">Ta wartość jest ustawiana przez model uczenia maszynowego Azure udostępniane w ramach rozwiązania i zintegrowane ze ścieżką w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="c7836-197">It is set by the Azure Machine Learning model provisioned as part of solution and integrated with the real-time path.</span></span> <span data-ttu-id="c7836-198">Wartość "1" oznacza, że vehicle wymaga konserwacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-198">The value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="c7836-199">Aby dodać **poziomu strony** filtr przedstawiający pojazdów danych, które wymagają obsługi:</span><span class="sxs-lookup"><span data-stu-id="c7836-199">To add a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="c7836-200">Przeciągnij **"MaintenanceLabel"** pole do **filtrów stron poziomu**.</span><span class="sxs-lookup"><span data-stu-id="c7836-200">Drag the **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="c7836-201">![Połączone samochodów — filtry poziomu strony](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="c7836-202">Kliknij przycisk **podstawowe filtrowanie** w dolnej części filtru poziomu strony MaintenanceLabel menu.</span><span class="sxs-lookup"><span data-stu-id="c7836-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="c7836-203">![Połączone samochodów — podstawowe filtrowanie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="c7836-204">Ustaw dla niego wartość filtru **"1"**  </span><span class="sxs-lookup"><span data-stu-id="c7836-204">Set its filter value to **“1”**  </span></span>  
   <span data-ttu-id="c7836-205">![Połączone samochodów — wartość filtru](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="c7836-206">Kliknij obszar puste, aby dodać nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-206">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c7836-207">Wybierz **wykres kolumnowy grupowany** z wizualizacji</span><span class="sxs-lookup"><span data-stu-id="c7836-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="c7836-208">![Połączone samochodów — karta Vind wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="c7836-209">![Połączone samochodów - kolumnowy grupowany](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="c7836-210">Przeciągnij pole **modelu** do **osi** obszarze **Vin** do **wartość** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c7836-210">Drag field **Model** into **Axis** area, **Vin** to **Value** area.</span></span> <span data-ttu-id="c7836-211">Następnie Sortuj wizualizacji przez **liczba vin**.</span><span class="sxs-lookup"><span data-stu-id="c7836-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="c7836-212">Zmień wykres **tytuł** do **"Pojazdów wymagających obsługi przez model"**</span><span class="sxs-lookup"><span data-stu-id="c7836-212">Change chart **Title** to **“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="c7836-213">Przeciągnij **vin** pól do **nasycenie kolorów** w **pola** ![pola](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) sekcji **wizualizacji**kartę</span><span class="sxs-lookup"><span data-stu-id="c7836-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="c7836-214">![Połączone samochodów - nasycenie kolorów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="c7836-215">Zmień **kolory danych** w wizualizacji z **Format** sekcji</span><span class="sxs-lookup"><span data-stu-id="c7836-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="c7836-216">Zmień kolor Minimum: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="c7836-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="c7836-217">Zmień kolor wartości maksymalnej do: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="c7836-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="c7836-218">![Połączone samochodów — zmiany kolorów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="c7836-219">![Połączone samochodów — nowe kolory wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="c7836-220">Kliknij obszar puste, aby dodać nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-220">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c7836-221">Wybierz **klastrowanych kolumnowy** z wizualizacji, przeciągnij **vin** pole do **wartość** obszaru, przeciągnij **miasta** pole do **Osi** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c7836-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="c7836-222">Wykres sortowania przez **"Liczba vin"**.</span><span class="sxs-lookup"><span data-stu-id="c7836-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="c7836-223">Zmień wykres **tytuł** do **"Pojazdów wymagających obsługi przez Miasto"** </span><span class="sxs-lookup"><span data-stu-id="c7836-223">Change chart **Title** to **“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="c7836-224">![Połączone samochodów - pojazdów wymagających obsługi przez miasta](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="c7836-225">Kliknij obszar puste, aby dodać nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-225">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c7836-226">Wybierz **karty wielowierszowych** wizualizacji z wizualizacji, przeciągnij **modelu** i **vin** do **pola** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c7836-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into the **Fields** area.</span></span>  
<span data-ttu-id="c7836-227">![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="c7836-228">Zmienianie rozmieszczenia wszystkie wizualizacji, raportu końcowego wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="c7836-228">Rearranging all of the visualization, the final report looks as follows:</span></span>  
![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="c7836-230">Raport w czasie rzeczywistym "Pojazdów wymagających obsługi" została pomyślnie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="c7836-230">You have successfully configured the “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="c7836-231">Możesz przejść do tworzenia następnej raportu w czasie rzeczywistym lub zatrzymać w tym miejscu i skonfigurować pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7836-231">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="c7836-232">3. Statystyki kondycji pojazdów</span><span class="sxs-lookup"><span data-stu-id="c7836-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="c7836-233">Kliknij przycisk ![Dodaj](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) Aby dodać nowy raport, zmienić jego nazwę na **"Statystyki kondycji pojazdów"**</span><span class="sxs-lookup"><span data-stu-id="c7836-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add new report, rename it to **“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="c7836-234">Wybierz **miernika** wizualizacji z wizualizacji, przeciągnij **szybkości** pole do **wartości, wartość minimalna, wartość maksymalna** obszarów.</span><span class="sxs-lookup"><span data-stu-id="c7836-234">Select **Gauge** visualization from visualizations, then drag the **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="c7836-235">![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="c7836-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="c7836-236">Zmień domyślny agregacji **szybkości** w **wartość obszaru** do **średni**</span><span class="sxs-lookup"><span data-stu-id="c7836-236">Change the default aggregation of **speed** in **Value area** to **Average**</span></span> 

<span data-ttu-id="c7836-237">Zmień domyślny agregacji **szybkości** w **obszar minimalny** do **minimalna**</span><span class="sxs-lookup"><span data-stu-id="c7836-237">Change the default aggregation of **speed** in **Minimum area** to **Minimum**</span></span>

<span data-ttu-id="c7836-238">Zmień domyślny agregacji **szybkości** w **maksymalny obszar** do **maksymalna**</span><span class="sxs-lookup"><span data-stu-id="c7836-238">Change the default aggregation of **speed** in **Maximum area** to **Maximum**</span></span>

![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="c7836-240">Zmień nazwę **tytuł miernika** do **"Średnia szybkość"**</span><span class="sxs-lookup"><span data-stu-id="c7836-240">Rename the **Gauge Title** to **“Average speed”**</span></span> 

![Połączone samochodów - miernika](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="c7836-242">Kliknij obszar puste, aby dodać nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-242">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="c7836-243">Podobnie dodać **miernika** dla **średni wydobycie ropy naftowej aparat**, **średni paliwa**, i **aparat średnia temperatura**.</span><span class="sxs-lookup"><span data-stu-id="c7836-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="c7836-244">Zmień agregacji domyślne pól w każdym miernika zgodnie powyżej kroki opisane w **"Średnia szybkość"** miernika.</span><span class="sxs-lookup"><span data-stu-id="c7836-244">Change the default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Połączone samochodów - mierników](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="c7836-246">Kliknij obszar puste, aby dodać nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-246">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="c7836-247">Wybierz **liniowy i kolumnowy grupowany** z wizualizacji, przeciągnij **miasta** pole do **udostępnionych osi**, przeciągnij **szybkości**, **pól tirepressure i engineoil** do **wartości w kolumnie** obszaru, zmień ich typ agregacji do **średni**.</span><span class="sxs-lookup"><span data-stu-id="c7836-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type to **Average**.</span></span> 

<span data-ttu-id="c7836-248">Przeciągnij **engineTemperature** pole do **wartości linii** obszaru, Zmień typ agregacji do **średni**.</span><span class="sxs-lookup"><span data-stu-id="c7836-248">Drag the **engineTemperature** field into **Line Values** area, change the  aggregation type to **Average**.</span></span> 

![Połączone samochodów - pola wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="c7836-250">Zmień wykres **tytuł** do **"Średnia szybkość, opona wykorzystania, aparat wydobycie ropy naftowej i temperatury aparat"**.</span><span class="sxs-lookup"><span data-stu-id="c7836-250">Change the chart **Title** to **“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Połączone samochodów - pola wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="c7836-252">Kliknij obszar puste, aby dodać nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-252">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="c7836-253">Wybierz **właściwości** wizualizacji z wizualizacji, przeciągnij **modelu** pole do **grupy** obszaru, a następnie przeciągnij pole **MaintenanceProbability** do **wartości** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c7836-253">Select **Treemap** visualization from visualizations, drag the **Model** field into the **Group** area, and drag the field **MaintenanceProbability** into the **Values** area.</span></span>

<span data-ttu-id="c7836-254">Zmień wykres **tytuł** do **"Modele pojazdów wymagających obsługi"**.</span><span class="sxs-lookup"><span data-stu-id="c7836-254">Change the chart **Title** to **“Vehicle models requiring maintenance”**.</span></span>

![Połączone samochodów — Zmień tytuł wykresu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="c7836-256">Kliknij obszar puste, aby dodać nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-256">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="c7836-257">Wybierz **100% skumulowany wykres słupkowy** z wizualizacji, przeciągnij **miasta** pole do **osi** obszaru, a następnie przeciągnij **MaintenanceProbability**, **RecallProbability** pól do **wartość** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c7836-257">Select **100% Stacked Bar Chart** from visualization, drag the **city** field into the **Axis** area, and drag the **MaintenanceProbability**, **RecallProbability** fields into the **Value** area.</span></span>

![Połączone samochodów — Dodawanie nowej wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="c7836-259">Kliknij przycisk **Format**, wybierz pozycję **kolory danych**i ustaw **MaintenanceProbability** kolor wartości **"F2C80F"**.</span><span class="sxs-lookup"><span data-stu-id="c7836-259">Click **Format**, select **Data Colors**, and set the **MaintenanceProbability** color to the value **“F2C80F”**.</span></span>

<span data-ttu-id="c7836-260">Zmień **tytuł** wykresu, aby **"Prawdopodobieństwo z Vehicle konserwacji & Wycofaj przez Miasto"**.</span><span class="sxs-lookup"><span data-stu-id="c7836-260">Change the **Title** of the chart to **“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Połączone samochodów — Dodawanie nowej wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="c7836-262">Kliknij obszar puste, aby dodać nowej wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-262">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="c7836-263">Wybierz **wykres warstwowy** z wizualizacji z wizualizacji, przeciągnij **modelu** pole do **osi** obszaru, a następnie przeciągnij **engineOil, tirepressure, szybkość i MaintenanceProbability** pól do **wartości** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c7836-263">Select **Area Chart** from visualization from visualizations, drag the **Model** field into the **Axis** area, and drag the **engineOil, tirepressure, speed and MaintenanceProbability** fields into the **Values** area.</span></span> <span data-ttu-id="c7836-264">Zmień ich typ agregacji do **"Średni"**.</span><span class="sxs-lookup"><span data-stu-id="c7836-264">Change their aggregation type to **“Average”**.</span></span> 

![Połączone samochodów — Zmień typ agregacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="c7836-266">Tytuł wykresu, aby zmienić **"Średni aparat wydobycie ropy naftowej, opona prawdopodobieństwo wykorzystania, szybkość i konserwacja przez model"**.</span><span class="sxs-lookup"><span data-stu-id="c7836-266">Change the title of the chart to **“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Połączone samochodów — Zmień tytuł wykresu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="c7836-268">Kliknij obszar puste, aby dodać nowej wizualizacji:</span><span class="sxs-lookup"><span data-stu-id="c7836-268">Click the blank area to add new visualization:</span></span>

1. <span data-ttu-id="c7836-269">Wybierz **wykres punktowy** wizualizacji z wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="c7836-270">Przeciągnij **modelu** pole do **szczegóły** i **legendy** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c7836-270">Drag the **Model** field into the **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="c7836-271">Przeciągnij **paliwa** pole do **osi x** obszaru, zmień agregacji do **średni**.</span><span class="sxs-lookup"><span data-stu-id="c7836-271">Drag the **fuel** field into the **X-Axis** area, change the aggregation to **Average**.</span></span>
4. <span data-ttu-id="c7836-272">Przeciągnij **engineTemparature** do **osi y obszaru**, zmień agregacji do **średni**</span><span class="sxs-lookup"><span data-stu-id="c7836-272">Drag **engineTemparature** into **Y-Axis area**, change the aggregation to **Average**</span></span>
5. <span data-ttu-id="c7836-273">Przeciągnij **vin** pole do **rozmiar** obszaru.</span><span class="sxs-lookup"><span data-stu-id="c7836-273">Drag the **vin** field into the **Size** area.</span></span>

![Połączone samochodów — Dodawanie nowej wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="c7836-275">Zmień wykres **tytuł** do **"Średnie paliwa, aparat temperatury przez Model"**.</span><span class="sxs-lookup"><span data-stu-id="c7836-275">Change the chart **Title** to **“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Połączone samochodów — Zmień tytuł wykresu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="c7836-277">Raport końcowy będzie wyglądać jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c7836-277">The final report will look like as shown below.</span></span>

![Połączony raport końcowy samochodów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-the-reports-to-the-real-time-dashboard"></a><span data-ttu-id="c7836-279">Wizualizacje numeru PIN z raportów do pulpitu nawigacyjnego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="c7836-279">Pin visualizations from the reports to the real-time dashboard</span></span>
<span data-ttu-id="c7836-280">Utwórz pusty pulpit nawigacyjny, klikając ikonę znaku plus obok pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c7836-280">Create a blank dashboard by clicking on the plus icon next to Dashboards.</span></span> <span data-ttu-id="c7836-281">Można określić nazwę "Pulpitu nawigacyjnego Analytics Vehicle Telemetrii"</span><span class="sxs-lookup"><span data-stu-id="c7836-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Połączone samochodów pulpitu nawigacyjnego](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="c7836-283">Kod PIN wizualizacji z powyższych raportów do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7836-283">Pin the visualization from the above reports to the dashboard.</span></span> 

![Połączone samochodów pulpitu nawigacyjnego](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="c7836-285">Pulpit nawigacyjny powinien wyglądać w następujący sposób od tego, są tworzone trzy raporty i odpowiednie wizualizacje są przypięty do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7836-285">The dashboard should look as follows when all the three reports are created and the corresponding visualizations are pinned to the dashboard.</span></span> <span data-ttu-id="c7836-286">Jeśli nie utworzono wszystkie raporty, pulpit nawigacyjny może wyglądać inaczej.</span><span class="sxs-lookup"><span data-stu-id="c7836-286">If you have not created all the reports, your dashboard could look different.</span></span> 

![Połączone samochodów pulpitu nawigacyjnego](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="c7836-288">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="c7836-288">Congratulations!</span></span> <span data-ttu-id="c7836-289">Pomyślnie utworzono w czasie rzeczywistym pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7836-289">You have successfully created the real-time dashboard.</span></span> <span data-ttu-id="c7836-290">Jak wykonać CarEventGenerator.exe i RealtimeDashboardApp.exe, powinny pojawić się aktualizacje na żywo na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="c7836-290">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on the dashboard.</span></span> <span data-ttu-id="c7836-291">Wykonaj poniższe kroki powinno zająć około 10 – 15 minut.</span><span class="sxs-lookup"><span data-stu-id="c7836-291">It should take about 10 to 15 minutes to complete the following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="c7836-292">Konfiguracja pulpitu nawigacyjnego przetwarzania wsadowego usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="c7836-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="c7836-293">Trwa około dwie godziny (od pomyślnego ukończenia wdrożenia) dla potoku przetwarzania wsadowego kompleksowe na zakończenie wykonywania i przetworzyć roku warto wygenerowanych danych.</span><span class="sxs-lookup"><span data-stu-id="c7836-293">It takes about two hours (from the successful completion of the deployment) for the end to end batch processing pipeline to finish execution and process a year worth of generated data.</span></span> <span data-ttu-id="c7836-294">Dlatego poczekaj na zakończenie przetwarzania przed wykonaniem dalszych kroków.</span><span class="sxs-lookup"><span data-stu-id="c7836-294">So wait for the processing to finish before proceeding with the next steps.</span></span> 
> 
> 

<span data-ttu-id="c7836-295">**Pobierz plik projektanta usługi Power BI**</span><span class="sxs-lookup"><span data-stu-id="c7836-295">**Download the Power BI designer file**</span></span>

* <span data-ttu-id="c7836-296">Wstępnie skonfigurowane pliku projektanta usługi Power BI wchodzi w skład wdrożenia instrukcje działania ręczne</span><span class="sxs-lookup"><span data-stu-id="c7836-296">A pre-configured Power BI designer file is included as part of the deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="c7836-297">Poszukaj 2.</span><span class="sxs-lookup"><span data-stu-id="c7836-297">Look for 2.</span></span> <span data-ttu-id="c7836-298">Instalator usługi Power BI partii przetwarzania w pulpicie nawigacyjnym można pobrać szablonu usługi Power BI dla pulpitu nawigacyjnego przetwarzania wsadowego nosi nazwę **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="c7836-298">Setup PowerBI batch processing dashboard You can download the PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="c7836-299">Zapisz lokalnie</span><span class="sxs-lookup"><span data-stu-id="c7836-299">Save locally</span></span>

<span data-ttu-id="c7836-300">**Konfigurowanie raportów usługi Power BI**</span><span class="sxs-lookup"><span data-stu-id="c7836-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="c7836-301">Otwórz plik projektanta '**ConnectedCarsPbiReport.pbix**"przy użyciu Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c7836-301">Open the designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="c7836-302">Jeśli nie masz już, zainstaluj Power BI Desktop z [instalacji Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="c7836-302">If you do not already have, install the Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="c7836-303">Kliknij przycisk **Edytuj zapytania**.</span><span class="sxs-lookup"><span data-stu-id="c7836-303">Click the **Edit Queries**.</span></span>

![Edytuj zapytanie usługi Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="c7836-305">Kliknij dwukrotnie **źródła**.</span><span class="sxs-lookup"><span data-stu-id="c7836-305">Double-click the **Source**.</span></span>

![Źródło usługi Power BI zbioru](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="c7836-307">Zaktualizuj parametry połączenia serwera z serwerem Azure SQL, które uzyskano udostępnione jako część wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c7836-307">Update Server connection string with the Azure SQL server that got provisioned as part of the deployment.</span></span>  <span data-ttu-id="c7836-308">Szukaj w zgodnie z instrukcjami dotyczącymi działania ręczne</span><span class="sxs-lookup"><span data-stu-id="c7836-308">Look in the Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="c7836-309">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c7836-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="c7836-310">Serwer: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="c7836-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="c7836-311">Baza danych: connectedcar</span><span class="sxs-lookup"><span data-stu-id="c7836-311">Database: connectedcar</span></span>
    * <span data-ttu-id="c7836-312">Nazwa użytkownika: nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="c7836-312">Username: username</span></span>
    * <span data-ttu-id="c7836-313">Hasło: Hasło programu SQL server można zarządzać z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c7836-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="c7836-314">Pozostaw **bazy danych** jako *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="c7836-314">Leave **Database** as *connectedcar*.</span></span>

![Ustaw bazę danych usługi Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="c7836-316">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c7836-316">Click **OK**.</span></span>
* <span data-ttu-id="c7836-317">Zobaczysz **poświadczenia systemu Windows** kartę domyślnie zaznaczone, Zmień, aby **bazy danych poświadczeń** , klikając **bazy danych** kartę w prawym rogu.</span><span class="sxs-lookup"><span data-stu-id="c7836-317">You will see **Windows credential** tab selected by default, change it to **Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="c7836-318">Podaj **Username** i **hasło** Twojej bazy danych SQL Azure, która została określona podczas jego wdrażania instalacji.</span><span class="sxs-lookup"><span data-stu-id="c7836-318">Provide the **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Podaj poświadczenia bazy danych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="c7836-320">Kliknij przycisk **połączenia**</span><span class="sxs-lookup"><span data-stu-id="c7836-320">Click **Connect**</span></span>
* <span data-ttu-id="c7836-321">Powtórz powyższe kroki dla każdego z trzech pozostałych kwerend w okienku po prawej stronie, a następnie zaktualizuj informacje dotyczące połączenia dla źródła danych.</span><span class="sxs-lookup"><span data-stu-id="c7836-321">Repeat the above steps for each of the three remaining queries present at right pane, and then update the data source connection details.</span></span>
* <span data-ttu-id="c7836-322">Kliknij przycisk **Zamknij i załadować**.</span><span class="sxs-lookup"><span data-stu-id="c7836-322">Click **Close and Load**.</span></span> <span data-ttu-id="c7836-323">Power BI Desktop pliku w zestawach danych są połączone z tabelami bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c7836-323">Power BI Desktop file datasets are connected to SQL Azure Database tables.</span></span>
* <span data-ttu-id="c7836-324">**Zamknij** pliku Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c7836-324">**Close** Power BI Desktop file.</span></span>

![Zamknij usługę Power BI desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="c7836-326">Kliknij przycisk **zapisać** przycisk, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="c7836-326">Click **Save** button to save the changes.</span></span> 

<span data-ttu-id="c7836-327">Wszystkie raporty odpowiadający ścieżka przetwarzania wsadowego w rozwiązaniu został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="c7836-327">You have now configured all the reports corresponding to the batch processing path in the solution.</span></span> 

## <a name="upload-to-powerbicom"></a><span data-ttu-id="c7836-328">Przekaż do *witrynie powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="c7836-328">Upload to *powerbi.com*</span></span>
1. <span data-ttu-id="c7836-329">Przejdź do portalu sieci web usługi Power BI na http://powerbi.com i logowania.</span><span class="sxs-lookup"><span data-stu-id="c7836-329">Navigate to the Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="c7836-330">Kliknij przycisk **pobieranie danych**</span><span class="sxs-lookup"><span data-stu-id="c7836-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="c7836-331">Przekaż plik Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c7836-331">Upload the Power BI Desktop File.</span></span>  
4. <span data-ttu-id="c7836-332">Aby przekazać, kliknij przycisk **Pobierz dane -> pliki -> pliku lokalnego**</span><span class="sxs-lookup"><span data-stu-id="c7836-332">To upload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="c7836-333">Przejdź do **"**ConnectedCarsPbiReport.pbix**"**</span><span class="sxs-lookup"><span data-stu-id="c7836-333">Navigate to the **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="c7836-334">Gdy plik jest przekazywany, nastąpi przejście wstecz do obszaru roboczego usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="c7836-334">Once the file is uploaded, you will be navigated back to your Power BI work space.</span></span>  

<span data-ttu-id="c7836-335">Zestaw danych, raportów i pustego pulpitu nawigacyjnego zostanie utworzona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="c7836-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="c7836-336">Wykresy numeru PIN, aby nowy pulpit nawigacyjny o nazwie **pulpitu nawigacyjnego Analytics Telemetrii Vehicle** w **usługi Power BI**.</span><span class="sxs-lookup"><span data-stu-id="c7836-336">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="c7836-337">Kliknij pozycję puste pulpit nawigacyjny utworzone powyżej, a następnie przejdź do **raporty** sekcji kliknij nowo przesłanym raport.</span><span class="sxs-lookup"><span data-stu-id="c7836-337">Click the blank dashboard created above and then navigate to the **Reports** section click the newly uploaded report.</span></span>  

![Vehicle Telemetrii Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="c7836-339">**Należy pamiętać, że raport ma sześć stron:**</span><span class="sxs-lookup"><span data-stu-id="c7836-339">**Note the report has six pages:**</span></span>  
<span data-ttu-id="c7836-340">Strona 1: Gęstość Vehicle</span><span class="sxs-lookup"><span data-stu-id="c7836-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="c7836-341">Strona 2: Kondycja vehicle w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="c7836-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="c7836-342">Strona 3: Agresywnie zmiennych pojazdów</span><span class="sxs-lookup"><span data-stu-id="c7836-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="c7836-343">4 strony: Pojazdów odwołane</span><span class="sxs-lookup"><span data-stu-id="c7836-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="c7836-344">5 strony: Efektywne zmiennych pojazdów paliwa</span><span class="sxs-lookup"><span data-stu-id="c7836-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="c7836-345">6 strony: Logo firmy Contoso</span><span class="sxs-lookup"><span data-stu-id="c7836-345">Page 6: Contoso Logo</span></span>  

![Połączone samochodów Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="c7836-347">**Z 3 stron**, przypiąć następujące:</span><span class="sxs-lookup"><span data-stu-id="c7836-347">**From Page 3**, pin the following:</span></span>  

1. <span data-ttu-id="c7836-348">Liczba VIN</span><span class="sxs-lookup"><span data-stu-id="c7836-348">Count of VIN</span></span>  
   ![Połączone samochodów Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="c7836-350">Agresywnie zmiennych pojazdów przez model — wykresu wykresu kaskadowego</span><span class="sxs-lookup"><span data-stu-id="c7836-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Vehicle Telemetrii - Pin wykresy 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="c7836-352">**Od 5 strony**, przypiąć następujące:</span><span class="sxs-lookup"><span data-stu-id="c7836-352">**From Page 5**, pin the following:</span></span> 

1. <span data-ttu-id="c7836-353">Liczba vin</span><span class="sxs-lookup"><span data-stu-id="c7836-353">Count of vin</span></span>    
   ![Vehicle Telemetrii - Pin wykresy 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="c7836-355">Paliwa pojazdów wydajne przez model: kolumnowy grupowany</span><span class="sxs-lookup"><span data-stu-id="c7836-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Vehicle Telemetrii - Pin wykresy 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="c7836-357">**Z 4 strony**, przypiąć następujące:</span><span class="sxs-lookup"><span data-stu-id="c7836-357">**From Page 4**, pin the following:</span></span>  

1. <span data-ttu-id="c7836-358">Liczba vin</span><span class="sxs-lookup"><span data-stu-id="c7836-358">Count of vin</span></span>  
   ![Vehicle Telemetrii - Pin wykresy 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="c7836-360">Odwołane pojazdów miejscowość, model: właściwości</span><span class="sxs-lookup"><span data-stu-id="c7836-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Vehicle Telemetrii - Pin wykresy 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="c7836-362">**Strona 6**, przypiąć następujące:</span><span class="sxs-lookup"><span data-stu-id="c7836-362">**From Page 6**, pin the following:</span></span>  

1. <span data-ttu-id="c7836-363">Logo firmy Contoso silniki</span><span class="sxs-lookup"><span data-stu-id="c7836-363">Contoso Motors logo</span></span>  
   ![Vehicle Telemetrii - Pin wykresy 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="c7836-365">**Organizowanie pulpitu nawigacyjnego**</span><span class="sxs-lookup"><span data-stu-id="c7836-365">**Organize the dashboard**</span></span>  

1. <span data-ttu-id="c7836-366">Przejdź do pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="c7836-366">Navigate to the dashboard</span></span>
2. <span data-ttu-id="c7836-367">Umieść kursor nad każdy wykres i Zmień nazwę ją zależnie od nazw podane w poniższym obrazie Tworzenie pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c7836-367">Hover over each chart and rename it based on the naming provided in the complete dashboard image below.</span></span> <span data-ttu-id="c7836-368">Również poruszanie wykresy, aby wyglądały jak pulpit nawigacyjny poniżej.</span><span class="sxs-lookup"><span data-stu-id="c7836-368">Also move the charts around to look like the dashboard below.</span></span>  
   ![Vehicle Telemetrii - organizowanie pulpitu nawigacyjnego 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle Telemetrii Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="c7836-371">Jeśli utworzono wszystkie raporty, jak wspomniano w tym dokumencie, końcowego zakończonych pulpitu nawigacyjnego powinien wyglądać poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="c7836-371">If you have created all the reports as mentioned in this document, the final completed dashboard should look like the following figure.</span></span> 

![Vehicle Telemetrii - organizowanie pulpitu nawigacyjnego 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="c7836-373">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="c7836-373">Congratulations!</span></span> <span data-ttu-id="c7836-374">Pomyślnie utworzono raporty i pulpit nawigacyjny, aby uzyskać w czasie rzeczywistym, predykcyjnych i partii rozeznanie vehicle kondycji i wspierającym zwyczaje.</span><span class="sxs-lookup"><span data-stu-id="c7836-374">You have successfully created the reports and the dashboard to gain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
