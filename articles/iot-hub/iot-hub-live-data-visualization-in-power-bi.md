---
title: "wizualizacji danych czasu aaaReal danych czujnika z Centrum IoT Azure — usługi Power BI | Dokumentacja firmy Microsoft"
description: "Użyj usługi Power BI toovisualize temperatury i wilgotności danych zbieranych z czujnika hello i wysyłane tooyour Centrum Azure IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "wizualizację danych czasu rzeczywistego, wizualizacji danych na żywo czujnik wizualizacji danych"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="8d4bf-104">Wizualizacja danych czujnika w czasie rzeczywistym z Centrum IoT Azure przy użyciu usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="8d4bf-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="8d4bf-106">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="8d4bf-106">What you learn</span></span>

<span data-ttu-id="8d4bf-107">Dowiesz się, jak toovisualize czujnika w czasie rzeczywistym danych Centrum Azure IoT odbieranych przez usługę Power BI.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-107">You learn how toovisualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="8d4bf-108">Jeśli chcesz tootry wizualizacji danych hello w Centrum IoT z aplikacjami sieci Web, zobacz [danych czujnika w czasie rzeczywistym toovisualize Użyj Azure Web Apps z Centrum IoT Azure](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="8d4bf-108">If you want tootry visualize hello data in your IoT hub with Web Apps, please see [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="8d4bf-109">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="8d4bf-109">What you do</span></span>

- <span data-ttu-id="8d4bf-110">Przygotuj się Centrum IoT na dostęp do danych przez dodanie grupy odbiorców.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="8d4bf-111">Tworzenie, konfigurowanie i uruchamianie zadania usługi analiza strumienia do transferu danych z Twojego tooyour Centrum IoT konta usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub tooyour Power BI account.</span></span>
- <span data-ttu-id="8d4bf-112">Tworzenie i publikowanie danych hello toovisualize raportu usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-112">Create and publish a Power BI report toovisualize hello data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8d4bf-113">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="8d4bf-113">What you need</span></span>

- <span data-ttu-id="8d4bf-114">Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje hello następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="8d4bf-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="8d4bf-115">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="8d4bf-116">Centrum Azure IoT w ramach Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="8d4bf-117">Aplikacja klienta, która wysyła komunikaty tooyour Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-117">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="8d4bf-118">Konto usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-118">A Power BI account.</span></span> <span data-ttu-id="8d4bf-119">([Spróbuj bezpłatnie usługę Power BI](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="8d4bf-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="8d4bf-120">Tworzenie, konfigurowanie i uruchamianie zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="8d4bf-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="8d4bf-121">Tworzenie zadania usługi Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8d4bf-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="8d4bf-122">W portalu Azure Witaj, kliknij przycisk Nowy > Internetu rzeczy > Zadanie usługi Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-122">In hello Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="8d4bf-123">Wprowadź następujące informacje dotyczące zadania hello hello.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-123">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="8d4bf-124">**Nazwa zadania**: Nazwa hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-124">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="8d4bf-125">Nazwa Hello musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-125">hello name must be globally unique.</span></span>

   <span data-ttu-id="8d4bf-126">**Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-126">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="8d4bf-127">**Lokalizacja**: Użyj hello sam lokalizacji, w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-127">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="8d4bf-128">**Numer PIN toodashboard**: Zaznacz tę opcję, Centrum IoT tooyour łatwy dostęp z poziomu pulpitu nawigacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-128">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Utwórz zadanie usługi Stream Analytics na platformie Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="8d4bf-130">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-130">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="8d4bf-131">Dodaj zadanie usługi analiza strumienia wejściowego toohello</span><span class="sxs-lookup"><span data-stu-id="8d4bf-131">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="8d4bf-132">Zadanie Stream Analytics hello otwarte.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-132">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="8d4bf-133">W obszarze **topologii zadania**, kliknij przycisk **dane wejściowe**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="8d4bf-134">W hello **dane wejściowe** okienku, kliknij przycisk **Dodaj**, a następnie wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="8d4bf-134">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="8d4bf-135">**Alias wejściowy**: hello unikatowego aliasu dla hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-135">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="8d4bf-136">**Źródło**: Wybierz **Centrum IoT**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="8d4bf-137">**Grupy odbiorców**: grupy odbiorców hello wybierz właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-137">**Consumer group**: Select hello consumer group you just created.</span></span>
1. <span data-ttu-id="8d4bf-138">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-138">Click **Create**.</span></span>

   ![Dodaj zadanie usługi analiza strumienia wejściowego tooa na platformie Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="8d4bf-140">Dodaj zadanie usługi analiza strumienia wyjściowego toohello</span><span class="sxs-lookup"><span data-stu-id="8d4bf-140">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="8d4bf-141">W obszarze **topologii zadania**, kliknij przycisk **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="8d4bf-142">W hello **dane wyjściowe** okienku, kliknij przycisk **Dodaj**, a następnie wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="8d4bf-142">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="8d4bf-143">**Alias wyjściowy**: hello unikatowego aliasu dla hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-143">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="8d4bf-144">**Obiekt sink**: Wybierz **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="8d4bf-145">Kliknij przycisk **autoryzacji**, a następnie zaloguj się na koncie usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="8d4bf-146">Autoryzowany, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="8d4bf-146">Once authorized, enter hello following information:</span></span>

   <span data-ttu-id="8d4bf-147">**Obszar roboczy grupy**: Wybierz docelowy obszar roboczy grupy.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="8d4bf-148">**Nazwa zestawu danych**: Wprowadź nazwę zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="8d4bf-149">**Nazwa tabeli**: Wprowadź nazwę tabeli.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="8d4bf-150">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-150">Click **Create**.</span></span>

   ![Dodaj zadanie usługi analiza strumienia wyjściowego tooa na platformie Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="8d4bf-152">Skonfiguruj zapytania hello hello zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="8d4bf-152">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="8d4bf-153">W obszarze **topologii zadania**, kliknij przycisk **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="8d4bf-154">Zastąp `[YourInputAlias]` z aliasem hello wejściowych hello zadania.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-154">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>
1. <span data-ttu-id="8d4bf-155">Zastąp `[YourOutputAlias]` z alias wyjściowy hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-155">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>
1. <span data-ttu-id="8d4bf-156">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-156">Click **Save**.</span></span>

   ![Dodaj zadanie usługi Stream Analytics tooa zapytania na platformie Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="8d4bf-158">Uruchom zadanie usługi Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="8d4bf-158">Run hello Stream Analytics job</span></span>

<span data-ttu-id="8d4bf-159">W zadaniu Stream Analytics hello, kliknij przycisk **Start** > **teraz** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-159">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="8d4bf-160">Po pomyślnym uruchomieniu zadania hello hello stan zadania zmieni się z **zatrzymane** za**systemem**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-160">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Uruchom zadanie usługi Stream Analytics na platformie Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a><span data-ttu-id="8d4bf-162">Tworzenie i publikowanie danych hello toovisualize raportu usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="8d4bf-162">Create and publish a Power BI report toovisualize hello data</span></span>

1. <span data-ttu-id="8d4bf-163">Upewnij się, że hello Przykładowa aplikacja jest uruchomiona na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-163">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="8d4bf-164">Jeśli nie mogą odwoływać się samouczki toohello w obszarze [skonfigurować na twoim urządzeniu](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="8d4bf-164">If not, you can refer toohello tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="8d4bf-165">Zaloguj się tooyour [usługi Power BI](https://powerbi.microsoft.com/en-us/) konta.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-165">Sign in tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="8d4bf-166">Przejdź toohello obszaru roboczego grupy ustawione podczas tworzenia hello wyjściowego zadania usługi analiza strumienia hello.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-166">Go toohello group workspace that you set when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="8d4bf-167">Kliknij przycisk **przesyłania strumieniowego zestawów danych**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="8d4bf-168">Zestaw danych hello wymienione określony podczas tworzenia hello dane wyjściowe zadania usługi analiza strumienia hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-168">You should see hello listed dataset that you specified when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="8d4bf-169">W obszarze **akcje**, kliknij pierwszy hello toocreate ikonę raportu.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-169">Under **ACTIONS**, click hello first icon toocreate a report.</span></span>

   ![Tworzenie raportu usługi Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="8d4bf-171">Tworzenie linii temperatury w czasie rzeczywistym tooshow wykresu wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-171">Create a line chart tooshow real-time temperature over time.</span></span>
   1. <span data-ttu-id="8d4bf-172">Na stronie tworzenia raportu hello Dodaj wykres liniowy.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-172">On hello report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="8d4bf-173">Na powitania **pola** okienku rozwiń tabeli hello określone podczas tworzenia hello wyjściowego zadania usługi analiza strumienia hello.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-173">On hello **Fields** pane, expand hello table that you specified when you created hello output for hello Stream Analytics job.</span></span>
   1. <span data-ttu-id="8d4bf-174">Przeciągnij **EventEnqueuedUtcTime** za**osi** na powitania **wizualizacje** okienka.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-174">Drag **EventEnqueuedUtcTime** too**Axis** on hello **Visualizations** pane.</span></span>
   1. <span data-ttu-id="8d4bf-175">Przeciągnij **temperatury** za**wartości**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-175">Drag **temperature** too**Values**.</span></span>

      <span data-ttu-id="8d4bf-176">Teraz jest tworzony wykres liniowy.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-176">Now a line chart is created.</span></span> <span data-ttu-id="8d4bf-177">oś x Hello Wyświetla datę i godzinę w strefie czasowej UTC hello.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-177">hello x-axis displays date and time in hello UTC time zone.</span></span> <span data-ttu-id="8d4bf-178">oś y Hello Wyświetla temperatury z czujnika hello.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-178">hello y-axis displays temperature from hello sensor.</span></span>

      ![Dodaj wykres liniowy dla tooa temperatury raportu usługi Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="8d4bf-180">Utwórz innego wiersza wykresu tooshow w czasie rzeczywistym wilgotności wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-180">Create another line chart tooshow real-time humidity over time.</span></span> <span data-ttu-id="8d4bf-181">toodo, wykonaj hello same kroki opisane powyżej i umieścić **EventEnqueuedUtcTime** na osi x hello i **wilgotności** na powitania osi y.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-181">toodo this, follow hello same steps above and place **EventEnqueuedUtcTime** on hello x-axis and **humidity** on hello y-axis.</span></span>

   ![Dodaj wykres wiersza wilgotność tooa raportu usługi Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="8d4bf-183">Kliknij przycisk **zapisać** toosave hello raportu.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-183">Click **Save** toosave hello report.</span></span>
1. <span data-ttu-id="8d4bf-184">Kliknij przycisk **pliku** > **publikowania tooweb**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-184">Click **File** > **Publish tooweb**.</span></span>
1. <span data-ttu-id="8d4bf-185">Kliknij przycisk **kod osadzania, Utwórz**, a następnie kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="8d4bf-186">W przypadku podane łącze do raportu hello, które można udostępniać każda osoba, aby uzyskać dostęp do raportów i raportu hello toointegrate fragment kodu w blogu lub witrynie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-186">You're provided hello report link that you can share with anyone for report access and a code snippet toointegrate hello report into your blog or website.</span></span>

![Publikowanie raportu Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="8d4bf-188">Firma Microsoft oferuje również hello [aplikacji mobilnych usługi Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) do przeglądania i interakcji z raportów i pulpitów nawigacyjnych usługi Power BI na swoim urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-188">Microsoft also offers hello [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d4bf-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8d4bf-189">Next steps</span></span>

<span data-ttu-id="8d4bf-190">Pomyślnie zastosowano danych czujnika w czasie rzeczywistym toovisualize usługi Power BI z Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-190">You’ve successfully used Power BI toovisualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="8d4bf-191">Brak danych toovisualize alternatywny sposób z Centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4bf-191">There is an alternate way toovisualize data from Azure IoT Hub.</span></span> <span data-ttu-id="8d4bf-192">Zobacz [danych czujnika w czasie rzeczywistym toovisualize Użyj Azure Web Apps z Centrum IoT Azure](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="8d4bf-192">See [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
