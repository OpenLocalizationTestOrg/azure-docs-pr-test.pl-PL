---
title: "aaaWeather prognozy przy użyciu danych z Centrum IoT przy użyciu usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Machine Learning toopredict hello ryzyko ustaniu oparte na powitania temperatury i wilgotności dane, które z czujnika zbiera dane Centrum IoT."
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
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="98b9b-104">Prognoza pogody przy użyciu danych czujnika hello z Centrum IoT w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="98b9b-104">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="98b9b-106">Machine learning to technika analizy danych, która pomaga komputerom informacje z istniejących danych tooforecast przyszłych zachowań, rezultatów i trendów.</span><span class="sxs-lookup"><span data-stu-id="98b9b-106">Machine learning is a technique of data science that helps computers learn from existing data tooforecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="98b9b-107">Azure Machine Learning to usługa analizy predykcyjnej w chmurze, dzięki którym możliwe tooquickly tworzenie i wdrażanie modeli predykcyjnych jako rozwiązań analitycznych.</span><span class="sxs-lookup"><span data-stu-id="98b9b-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible tooquickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="98b9b-108">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="98b9b-108">What you learn</span></span>

<span data-ttu-id="98b9b-109">Dowiedz się, jak toouse usługi Azure Machine Learning toodo prognozie pogody (szansy ustaniu) przy użyciu hello temperatury i wilgotności danych z Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="98b9b-109">You learn how toouse Azure Machine Learning toodo weather forecast (chance of rain) using hello temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="98b9b-110">ryzyko Hello ustaniu jest wyjściem hello przygotowane pogody modelu prognozy.</span><span class="sxs-lookup"><span data-stu-id="98b9b-110">hello chance of rain is hello output of a prepared weather prediction model.</span></span> <span data-ttu-id="98b9b-111">Hello model oparto na ryzyko tooforecast danych historycznych ustaniu na podstawie temperatury i wilgotności.</span><span class="sxs-lookup"><span data-stu-id="98b9b-111">hello model is built upon historic data tooforecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="98b9b-112">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="98b9b-112">What you do</span></span>

- <span data-ttu-id="98b9b-113">Wdrażanie modelu prognozy pogody hello jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="98b9b-113">Deploy hello weather prediction model as a web service.</span></span>
- <span data-ttu-id="98b9b-114">Przygotuj się Centrum IoT na dostęp do danych przez dodanie grupy odbiorców.</span><span class="sxs-lookup"><span data-stu-id="98b9b-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="98b9b-115">Utwórz zadanie usługi analiza strumienia i skonfiguruj na powitania zadania:</span><span class="sxs-lookup"><span data-stu-id="98b9b-115">Create a Stream Analytics job and configure hello job to:</span></span>
  - <span data-ttu-id="98b9b-116">Odczytywanie danych temperatury i wilgotności z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98b9b-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="98b9b-117">Wywołanie hello sieci web usługi tooget hello ustaniu szansy.</span><span class="sxs-lookup"><span data-stu-id="98b9b-117">Call hello web service tooget hello rain chance.</span></span>
  - <span data-ttu-id="98b9b-118">Zapisz magazynu obiektów blob Azure tooan wynik hello.</span><span class="sxs-lookup"><span data-stu-id="98b9b-118">Save hello result tooan Azure blob storage.</span></span>
- <span data-ttu-id="98b9b-119">Użyj prognozie pogody hello tooview Eksploratora magazynu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="98b9b-119">Use Microsoft Azure Storage Explorer tooview hello weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="98b9b-120">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="98b9b-120">What you need</span></span>

- <span data-ttu-id="98b9b-121">Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje hello następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="98b9b-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="98b9b-122">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="98b9b-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="98b9b-123">Centrum Azure IoT w ramach Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="98b9b-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="98b9b-124">Aplikacja klienta, która wysyła komunikaty tooyour Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="98b9b-124">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="98b9b-125">Konto usługi Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="98b9b-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="98b9b-126">([Bezpłatnie spróbuj Machine Learning Studio](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="98b9b-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="98b9b-127">Wdróż hello pogody prognozowania model jako usługę sieci web</span><span class="sxs-lookup"><span data-stu-id="98b9b-127">Deploy hello weather prediction model as a web service</span></span>

1. <span data-ttu-id="98b9b-128">Przejdź toohello [stronę modelu prognozy pogody](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="98b9b-128">Go toohello [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="98b9b-129">Kliknij przycisk **Otwórz w Studio** w usłudze Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="98b9b-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="98b9b-130">![Otwórz hello pogody prognozowania modelu strony w Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="98b9b-130">![Open hello weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="98b9b-131">Kliknij przycisk **Uruchom** toovalidate hello etapami hello modelu.</span><span class="sxs-lookup"><span data-stu-id="98b9b-131">Click **Run** toovalidate hello steps in hello model.</span></span> <span data-ttu-id="98b9b-132">Ten krok może potrwać toocomplete 2 minuty.</span><span class="sxs-lookup"><span data-stu-id="98b9b-132">This step might take 2 minutes toocomplete.</span></span>
   <span data-ttu-id="98b9b-133">![Otwórz hello pogody prognozowania modelu w usłudze Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="98b9b-133">![Open hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="98b9b-134">Kliknij przycisk **Konfigurowanie usługi sieci WEB** > **usługi sieci Web predykcyjnej**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="98b9b-135">![Wdróż model prognozowania pogody hello w usłudze Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="98b9b-135">![Deploy hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="98b9b-136">Na diagramie hello przeciągnij hello **sieci Web dane wejściowe usługi** modułu gdzieś w pobliżu hello **Score Model** modułu.</span><span class="sxs-lookup"><span data-stu-id="98b9b-136">In hello diagram, drag hello **Web service input** module somewhere near hello **Score Model** module.</span></span>
1. <span data-ttu-id="98b9b-137">Połącz hello **sieci Web dane wejściowe usługi** toohello modułu **Score Model** modułu.</span><span class="sxs-lookup"><span data-stu-id="98b9b-137">Connect hello **Web service input** module toohello **Score Model** module.</span></span>
   <span data-ttu-id="98b9b-138">![Połącz dwa moduły w usłudze Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="98b9b-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="98b9b-139">Kliknij przycisk **Uruchom** toovalidate hello etapami hello modelu.</span><span class="sxs-lookup"><span data-stu-id="98b9b-139">Click **RUN** toovalidate hello steps in hello model.</span></span>
1. <span data-ttu-id="98b9b-140">Kliknij przycisk **wdrażanie usługi sieci WEB** toodeploy hello model jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="98b9b-140">Click **DEPLOY WEB SERVICE** toodeploy hello model as a web service.</span></span>
1. <span data-ttu-id="98b9b-141">Na pulpicie nawigacyjnym hello hello modelu, Pobierz hello **programu Excel 2010 lub starszych skoroszytu** dla **ŻĄDANIA/odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-141">On hello dashboard of hello model, download hello **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="98b9b-142">Upewnij się, że pobierać hello **programu Excel 2010 lub starszych skoroszytu** nawet wtedy, gdy używasz nowszej wersji programu Excel na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="98b9b-142">Ensure that you download hello **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Pobierz hello programu Excel dla punktu końcowego odpowiedzi na żądanie hello](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="98b9b-144">Otwórz skoroszyt programu Excel hello, zanotuj hello **adres URL usługi sieci WEB** i **klucz dostępu**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-144">Open hello Excel workbook, make a note of hello **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="98b9b-145">Tworzenie, konfigurowanie i uruchamianie zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="98b9b-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="98b9b-146">Tworzenie zadania usługi Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="98b9b-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="98b9b-147">W hello [portalu Azure](https://ms.portal.azure.com/), kliknij przycisk **nowy** > **Internetu rzeczy** > **zadanie usługi Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-147">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="98b9b-148">Wprowadź następujące informacje dotyczące zadania hello hello.</span><span class="sxs-lookup"><span data-stu-id="98b9b-148">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="98b9b-149">**Nazwa zadania**: Nazwa hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="98b9b-149">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="98b9b-150">Nazwa Hello musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="98b9b-150">hello name must be globally unique.</span></span>

   <span data-ttu-id="98b9b-151">**Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98b9b-151">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="98b9b-152">**Lokalizacja**: Użyj hello sam lokalizacji, w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="98b9b-152">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="98b9b-153">**Numer PIN toodashboard**: Zaznacz tę opcję, Centrum IoT tooyour łatwy dostęp z poziomu pulpitu nawigacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="98b9b-153">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Utwórz zadanie usługi Stream Analytics na platformie Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="98b9b-155">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-155">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="98b9b-156">Dodaj zadanie usługi analiza strumienia wejściowego toohello</span><span class="sxs-lookup"><span data-stu-id="98b9b-156">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="98b9b-157">Zadanie Stream Analytics hello otwarte.</span><span class="sxs-lookup"><span data-stu-id="98b9b-157">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="98b9b-158">W obszarze **topologii zadania**, kliknij przycisk **dane wejściowe**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="98b9b-159">W hello **dane wejściowe** okienku, kliknij przycisk **Dodaj**, a następnie wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="98b9b-159">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="98b9b-160">**Alias wejściowy**: hello unikatowego aliasu dla hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="98b9b-160">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="98b9b-161">**Źródło**: Wybierz **Centrum IoT**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="98b9b-162">**Grupy odbiorców**: grupy odbiorców hello wybierz utworzony.</span><span class="sxs-lookup"><span data-stu-id="98b9b-162">**Consumer group**: Select hello consumer group you created.</span></span>

   ![Dodaj zadanie usługi analiza strumienia wejściowego toohello na platformie Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="98b9b-164">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-164">Click **Create**.</span></span>

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="98b9b-165">Dodaj zadanie usługi analiza strumienia wyjściowego toohello</span><span class="sxs-lookup"><span data-stu-id="98b9b-165">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="98b9b-166">W obszarze **topologii zadania**, kliknij przycisk **dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="98b9b-167">W hello **dane wyjściowe** okienku, kliknij przycisk **Dodaj**, a następnie wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="98b9b-167">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="98b9b-168">**Alias wyjściowy**: hello unikatowego aliasu dla hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="98b9b-168">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="98b9b-169">**Obiekt sink**: Wybierz **magazynu obiektów Blob**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="98b9b-170">**Konto magazynu**: hello konta magazynu dla usługi magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="98b9b-170">**Storage account**: hello storage account for your blob storage.</span></span> <span data-ttu-id="98b9b-171">Można utworzyć konta magazynu lub użyć istniejącego.</span><span class="sxs-lookup"><span data-stu-id="98b9b-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="98b9b-172">**Kontener**: hello kontenera, której jest zapisywany hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="98b9b-172">**Container**: hello container where hello blob is saved.</span></span> <span data-ttu-id="98b9b-173">Możesz utworzyć kontener lub użyć istniejącego.</span><span class="sxs-lookup"><span data-stu-id="98b9b-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="98b9b-174">**Format serializacji zdarzeń**: Wybierz **CSV**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Dodaj zadanie usługi analiza strumienia wyjściowego toohello na platformie Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="98b9b-176">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-176">Click **Create**.</span></span>

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a><span data-ttu-id="98b9b-177">Dodawanie funkcji toohello analiza strumienia zadania toocall hello usługi sieci web wdrożone</span><span class="sxs-lookup"><span data-stu-id="98b9b-177">Add a function toohello Stream Analytics job toocall hello web service you deployed</span></span>

1. <span data-ttu-id="98b9b-178">W obszarze **topologii zadania**, kliknij przycisk **funkcje** > **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="98b9b-179">Wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="98b9b-179">Enter hello following information:</span></span>

   <span data-ttu-id="98b9b-180">**Funkcja Alias**: wprowadź `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="98b9b-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="98b9b-181">**Typ funkcji**: Wybierz **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="98b9b-182">**Opcji importowania**: Wybierz **importu z innej subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="98b9b-183">**Adres URL**: Wprowadź adres URL usługi sieci WEB zanotowaną w dół hello hello skoroszycie programu Excel.</span><span class="sxs-lookup"><span data-stu-id="98b9b-183">**URL**: Enter hello WEB SERVICE URL that you noted down from hello Excel workbook.</span></span>

   <span data-ttu-id="98b9b-184">**Klucz**: Wprowadź hello klucz dostępu, zanotowaną w dół hello skoroszycie programu Excel.</span><span class="sxs-lookup"><span data-stu-id="98b9b-184">**Key**: Enter hello ACCESS KEY that you noted down from hello Excel workbook.</span></span>

   ![Dodaj zadanie usługi Stream Analytics toohello funkcji na platformie Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="98b9b-186">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-186">Click **Create**.</span></span>

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="98b9b-187">Skonfiguruj zapytania hello hello zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="98b9b-187">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="98b9b-188">W obszarze **topologii zadania**, kliknij przycisk **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="98b9b-189">Zastąp istniejący kod hello hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="98b9b-189">Replace hello existing code with hello following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="98b9b-190">Zastąp `[YourInputAlias]` z aliasem hello wejściowych hello zadania.</span><span class="sxs-lookup"><span data-stu-id="98b9b-190">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>

   <span data-ttu-id="98b9b-191">Zastąp `[YourOutputAlias]` z alias wyjściowy hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="98b9b-191">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>

1. <span data-ttu-id="98b9b-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-192">Click **Save**.</span></span>

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="98b9b-193">Uruchom zadanie usługi Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="98b9b-193">Run hello Stream Analytics job</span></span>

<span data-ttu-id="98b9b-194">W zadaniu Stream Analytics hello, kliknij przycisk **Start** > **teraz** > **Start**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-194">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="98b9b-195">Po pomyślnym uruchomieniu zadania hello hello stan zadania zmieni się z **zatrzymane** za**systemem**.</span><span class="sxs-lookup"><span data-stu-id="98b9b-195">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Uruchom zadanie usługi Stream Analytics hello](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a><span data-ttu-id="98b9b-197">Użyj prognozie pogody hello tooview Eksploratora magazynu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="98b9b-197">Use Microsoft Azure Storage Explorer tooview hello weather forecast</span></span>

<span data-ttu-id="98b9b-198">Uruchom powitania klienta aplikacji toostart zbieranie i wysyłanie temperatury i wilgotności Centrum IoT tooyour danych.</span><span class="sxs-lookup"><span data-stu-id="98b9b-198">Run hello client application toostart collecting and sending temperature and humidity data tooyour IoT hub.</span></span> <span data-ttu-id="98b9b-199">Dla każdego komunikatu, który odbiera Centrum IoT zadanie usługi Stream Analytics hello wywołuje hello prognozie pogody sieci web usługi tooproduce hello ryzyko ustaniu.</span><span class="sxs-lookup"><span data-stu-id="98b9b-199">For each message that your IoT hub receives, hello Stream Analytics job calls hello weather forecast web service tooproduce hello chance of rain.</span></span> <span data-ttu-id="98b9b-200">wynik Hello jest zapisywane tooyour magazynu obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="98b9b-200">hello result is then saved tooyour Azure blob storage.</span></span> <span data-ttu-id="98b9b-201">Eksplorator usługi Storage platformy Azure to narzędzie służy tooview hello wynik.</span><span class="sxs-lookup"><span data-stu-id="98b9b-201">Azure Storage Explorer is a tool that you can use tooview hello result.</span></span>

1. <span data-ttu-id="98b9b-202">[Pobieranie i instalowanie Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="98b9b-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="98b9b-203">Otwórz Eksploratora usługi Storage platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="98b9b-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="98b9b-204">Zaloguj się tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="98b9b-204">Sign in tooyour Azure account.</span></span>
1. <span data-ttu-id="98b9b-205">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="98b9b-205">Select your subscription.</span></span>
1. <span data-ttu-id="98b9b-206">Kliknij subskrypcję > **kont magazynu** > Twoje konto magazynu > **kontenerów obiektów Blob** > z kontenera.</span><span class="sxs-lookup"><span data-stu-id="98b9b-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="98b9b-207">Otwórz wynik hello toosee pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="98b9b-207">Open a .csv file toosee hello result.</span></span> <span data-ttu-id="98b9b-208">ostatnie rekordy kolumny Hello hello szansy ustaniu.</span><span class="sxs-lookup"><span data-stu-id="98b9b-208">hello last column records hello chance of rain.</span></span>

   ![Uzyskanie wyniku prognozie pogody przy użyciu usługi Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="98b9b-210">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="98b9b-210">Summary</span></span>

<span data-ttu-id="98b9b-211">Pomyślnie użyto usługi Azure Machine Learning tooproduce hello ryzyko ustaniu na podstawie danych temperatury i wilgotności hello, który odbiera Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98b9b-211">You’ve successfully used Azure Machine Learning tooproduce hello chance of rain based on hello temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]