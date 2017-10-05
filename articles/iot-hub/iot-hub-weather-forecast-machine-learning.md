---
title: "Pogody prognozy przy użyciu danych z Centrum IoT przy użyciu usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Machine Learning przewidzieć ryzyko ustaniu oparte na danych temperatury i wilgotności, które z czujnika zbiera dane Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: uczenie maszynowe prognozie pogody
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 50ae54b9476c49b80236e295c0bf244df8236cff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="9c2eb-104">Pogody prognozy przy użyciu danych czujnika z Centrum IoT w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9c2eb-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="9c2eb-106">Machine learning to technika analizy danych, która pomaga komputerom z istniejących danych w celu przewidywania przyszłych zachowań, rezultatów i trendów.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="9c2eb-107">Usługa Azure Machine Learning to oparta na chmurze usługa analizy predykcyjnej, która pozwala na szybkie tworzenie i wdrażanie modeli predykcyjnych jako rozwiązań analitycznych.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="9c2eb-108">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="9c2eb-108">What you learn</span></span>

<span data-ttu-id="9c2eb-109">Sposób na potrzeby usługi Azure Machine Learning pogodowe prognozy (szansy ustaniu) przy użyciu danych temperatury i wilgotności z Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="9c2eb-110">Ryzyko ustaniu jest dane wyjściowe przygotowane pogody modelu prognozy.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-110">The chance of rain is the output of a prepared weather prediction model.</span></span> <span data-ttu-id="9c2eb-111">Model jest oparty na danych historycznych Prognozowanie szansy ustaniu na podstawie temperatury i wilgotności.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="9c2eb-112">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="9c2eb-112">What you do</span></span>

- <span data-ttu-id="9c2eb-113">Wdróż model prognozowania pogody jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-113">Deploy the weather prediction model as a web service.</span></span>
- <span data-ttu-id="9c2eb-114">Przygotuj się Centrum IoT na dostęp do danych przez dodanie grupy odbiorców.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="9c2eb-115">Utwórz zadanie usługi analiza strumienia i skonfigurować zadanie, aby:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-115">Create a Stream Analytics job and configure the job to:</span></span>
  - <span data-ttu-id="9c2eb-116">Odczytywanie danych temperatury i wilgotności z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="9c2eb-117">Wywołanie usługi sieci web można pobrać ustaniu szansy.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-117">Call the web service to get the rain chance.</span></span>
  - <span data-ttu-id="9c2eb-118">Zapisz wynik do magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-118">Save the result to an Azure blob storage.</span></span>
- <span data-ttu-id="9c2eb-119">Umożliwia wyświetlanie prognozie pogody Eksploratora magazynu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9c2eb-120">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="9c2eb-120">What you need</span></span>

- <span data-ttu-id="9c2eb-121">Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="9c2eb-122">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="9c2eb-123">Centrum Azure IoT w ramach Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="9c2eb-124">Aplikacja klienta, która wysyła komunikaty do Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-124">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="9c2eb-125">Konto usługi Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="9c2eb-126">([Bezpłatnie spróbuj Machine Learning Studio](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="9c2eb-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="9c2eb-127">Wdróż model prognozowania pogody jako usługę sieci web</span><span class="sxs-lookup"><span data-stu-id="9c2eb-127">Deploy the weather prediction model as a web service</span></span>

1. <span data-ttu-id="9c2eb-128">Przejdź do [stronę modelu prognozy pogody](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="9c2eb-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="9c2eb-129">Kliknij przycisk **Otwórz w Studio** w usłudze Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="9c2eb-130">![Otwórz stronę modelu prognozy pogody w Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="9c2eb-130">![Open the weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="9c2eb-131">Kliknij przycisk **Uruchom** do sprawdzania poprawności kroki w modelu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-131">Click **Run** to validate the steps in the model.</span></span> <span data-ttu-id="9c2eb-132">Ten krok może potrwać 2 minut.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-132">This step might take 2 minutes to complete.</span></span>
   <span data-ttu-id="9c2eb-133">![Otwórz modelu prognozy pogody w usłudze Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="9c2eb-133">![Open the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="9c2eb-134">Kliknij przycisk **Konfigurowanie usługi sieci WEB** > **usługi sieci Web predykcyjnej**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="9c2eb-135">![Wdróż model prognozowania pogody w usłudze Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="9c2eb-135">![Deploy the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="9c2eb-136">Na diagramie, przeciągnij **sieci Web dane wejściowe usługi** modułu gdzieś w pobliżu **Score Model** modułu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span></span>
1. <span data-ttu-id="9c2eb-137">Połącz **sieci Web dane wejściowe usługi** moduł **Score Model** modułu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-137">Connect the **Web service input** module to the **Score Model** module.</span></span>
   <span data-ttu-id="9c2eb-138">![Połącz dwa moduły w usłudze Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="9c2eb-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="9c2eb-139">Kliknij przycisk **Uruchom** do sprawdzania poprawności kroki w modelu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-139">Click **RUN** to validate the steps in the model.</span></span>
1. <span data-ttu-id="9c2eb-140">Kliknij przycisk **wdrażanie usługi sieci WEB** Aby wdrożyć model jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span></span>
1. <span data-ttu-id="9c2eb-141">Na pulpicie nawigacyjnym modelu pobrać **programu Excel 2010 lub starszych skoroszytu** dla **ŻĄDANIA/odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="9c2eb-142">Upewnij się, że możesz pobrać **programu Excel 2010 lub starszych skoroszytu** nawet wtedy, gdy używasz nowszej wersji programu Excel na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Pobieranie programu Excel dla punktu końcowego odpowiedzi na żądanie](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="9c2eb-144">Otwórz skoroszyt programu Excel, zanotuj **adres URL usługi sieci WEB** i **klucz dostępu**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="9c2eb-145">Tworzenie, konfigurowanie i uruchamianie zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="9c2eb-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="9c2eb-146">Tworzenie zadania usługi Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9c2eb-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="9c2eb-147">W [portalu Azure](https://ms.portal.azure.com/), kliknij przycisk **nowy** > **Internetu rzeczy** > **zadanie usługi Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-147">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="9c2eb-148">Wprowadź następujące informacje dla zadania.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-148">Enter the following information for the job.</span></span>

   <span data-ttu-id="9c2eb-149">**Nazwa zadania**: Nazwa zadania.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-149">**Job name**: The name of the job.</span></span> <span data-ttu-id="9c2eb-150">Nazwa musi być unikatowa w skali globalnej.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-150">The name must be globally unique.</span></span>

   <span data-ttu-id="9c2eb-151">**Grupa zasobów**: Użyj tej samej grupie zasobów, która używa Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-151">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="9c2eb-152">**Lokalizacja**: Użyj tej samej lokalizacji co grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-152">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="9c2eb-153">**Przypnij do pulpitu nawigacyjnego**: Zaznacz tę opcję, by mieć łatwy dostęp do Centrum IoT z poziomu pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-153">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Utwórz zadanie usługi Stream Analytics na platformie Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="9c2eb-155">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-155">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="9c2eb-156">Dodawanie danych wejściowych do zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="9c2eb-156">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="9c2eb-157">Otwórz zadanie usługi Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-157">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="9c2eb-158">W obszarze **topologii zadania**, kliknij przycisk **dane wejściowe**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="9c2eb-159">W **dane wejściowe** okienku, kliknij przycisk **Dodaj**, a następnie wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-159">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="9c2eb-160">**Alias wejściowy**: unikatowego aliasu dla danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-160">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="9c2eb-161">**Źródło**: Wybierz **Centrum IoT**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="9c2eb-162">**Grupy odbiorców**: wybierz utworzoną grupę odbiorców.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-162">**Consumer group**: Select the consumer group you created.</span></span>

   ![Dodawanie danych wejściowych do zadania usługi analiza strumienia na platformie Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="9c2eb-164">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-164">Click **Create**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="9c2eb-165">Dodawanie danych wyjściowych do zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="9c2eb-165">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="9c2eb-166">W obszarze **topologii zadania**, kliknij przycisk **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="9c2eb-167">W **dane wyjściowe** okienku, kliknij przycisk **Dodaj**, a następnie wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-167">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="9c2eb-168">**Alias wyjściowy**: unikatowego aliasu dla danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-168">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="9c2eb-169">**Obiekt sink**: Wybierz **magazynu obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="9c2eb-170">**Konto magazynu**: Konto magazynu dla usługi magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-170">**Storage account**: The storage account for your blob storage.</span></span> <span data-ttu-id="9c2eb-171">Można utworzyć konta magazynu lub użyć istniejącego.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="9c2eb-172">**Kontener**: kontener, w której jest zapisywany obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-172">**Container**: The container where the blob is saved.</span></span> <span data-ttu-id="9c2eb-173">Możesz utworzyć kontener lub użyć istniejącego.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="9c2eb-174">**Format serializacji zdarzeń**: Wybierz **CSV**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Dodawanie danych wyjściowych do zadania usługi analiza strumienia na platformie Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="9c2eb-176">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-176">Click **Create**.</span></span>

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a><span data-ttu-id="9c2eb-177">Dodawanie funkcji do zadania usługi analiza strumienia do wywoływania usługi sieci web, na których wdrożono</span><span class="sxs-lookup"><span data-stu-id="9c2eb-177">Add a function to the Stream Analytics job to call the web service you deployed</span></span>

1. <span data-ttu-id="9c2eb-178">W obszarze **topologii zadania**, kliknij przycisk **funkcje** > **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="9c2eb-179">Wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-179">Enter the following information:</span></span>

   <span data-ttu-id="9c2eb-180">**Funkcja Alias**: wprowadź `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="9c2eb-181">**Typ funkcji**: Wybierz **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="9c2eb-182">**Opcji importowania**: Wybierz **importu z innej subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="9c2eb-183">**Adres URL**: Wprowadź adres URL usługi sieci WEB, zanotowaną w dół w skoroszycie programu Excel.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-183">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span></span>

   <span data-ttu-id="9c2eb-184">**Klucz**: Wprowadź klucz dostępu zanotowaną w dół ze skoroszytu programu Excel.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-184">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span></span>

   ![Dodawanie funkcji do zadania usługi analiza strumienia na platformie Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="9c2eb-186">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-186">Click **Create**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="9c2eb-187">Skonfiguruj zapytanie zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="9c2eb-187">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="9c2eb-188">W obszarze **topologii zadania**, kliknij przycisk **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="9c2eb-189">Zastąp istniejący kod następujący kod:</span><span class="sxs-lookup"><span data-stu-id="9c2eb-189">Replace the existing code with the following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="9c2eb-190">Zastąp `[YourInputAlias]` z alias wejściowy zadania.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-190">Replace `[YourInputAlias]` with the input alias of the job.</span></span>

   <span data-ttu-id="9c2eb-191">Zastąp `[YourOutputAlias]` z aliasem dane wyjściowe zadania.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-191">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>

1. <span data-ttu-id="9c2eb-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-192">Click **Save**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="9c2eb-193">Uruchom zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="9c2eb-193">Run the Stream Analytics job</span></span>

<span data-ttu-id="9c2eb-194">W zadaniu Stream Analytics kliknij **Start** > **teraz** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-194">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="9c2eb-195">Gdy zadanie zostanie uruchomiony pomyślnie, stan zadania zmieni się z **zatrzymane** do **systemem**.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-195">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Uruchom zadanie usługi analiza strumienia](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a><span data-ttu-id="9c2eb-197">Umożliwia wyświetlanie prognozie pogody Eksploratora magazynu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9c2eb-197">Use Microsoft Azure Storage Explorer to view the weather forecast</span></span>

<span data-ttu-id="9c2eb-198">Uruchom aplikację klienta do rozpoczęcia zbierania i wysyłania danych temperatury i wilgotności do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-198">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span></span> <span data-ttu-id="9c2eb-199">Dla każdego komunikatu, który odbiera Centrum IoT zadanie usługi Stream Analytics wywołuje usługę sieci web prognozie pogody wygenerowało ryzyko ustaniu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-199">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span></span> <span data-ttu-id="9c2eb-200">Wynik jest zapisywane do usługi magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-200">The result is then saved to your Azure blob storage.</span></span> <span data-ttu-id="9c2eb-201">Eksplorator usługi Storage platformy Azure to narzędzie, które służy do wyświetlenia wyników.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-201">Azure Storage Explorer is a tool that you can use to view the result.</span></span>

1. <span data-ttu-id="9c2eb-202">[Pobieranie i instalowanie Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9c2eb-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="9c2eb-203">Otwórz Eksploratora usługi Storage platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="9c2eb-204">Zaloguj się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-204">Sign in to your Azure account.</span></span>
1. <span data-ttu-id="9c2eb-205">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-205">Select your subscription.</span></span>
1. <span data-ttu-id="9c2eb-206">Kliknij subskrypcję > **kont magazynu** > Twoje konto magazynu > **kontenerów obiektów Blob** > z kontenera.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="9c2eb-207">Otwórz plik CSV, aby zobaczyć wynik.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-207">Open a .csv file to see the result.</span></span> <span data-ttu-id="9c2eb-208">Ostatnia kolumna rejestruje ryzyko ustaniu.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-208">The last column records the chance of rain.</span></span>

   ![Uzyskanie wyniku prognozie pogody przy użyciu usługi Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="9c2eb-210">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="9c2eb-210">Summary</span></span>

<span data-ttu-id="9c2eb-211">Uczenie maszynowe Azure zostało pomyślnie umożliwia tworzenie ryzyko ustaniu na podstawie danych temperatury i wilgotności, który odbiera Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9c2eb-211">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]