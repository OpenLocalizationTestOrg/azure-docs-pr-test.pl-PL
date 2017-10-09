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
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a>Prognoza pogody przy użyciu danych czujnika hello z Centrum IoT w usłudze Azure Machine Learning

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

Machine learning to technika analizy danych, która pomaga komputerom informacje z istniejących danych tooforecast przyszłych zachowań, rezultatów i trendów. Azure Machine Learning to usługa analizy predykcyjnej w chmurze, dzięki którym możliwe tooquickly tworzenie i wdrażanie modeli predykcyjnych jako rozwiązań analitycznych.

## <a name="what-you-learn"></a>Omawiane zagadnienia

Dowiedz się, jak toouse usługi Azure Machine Learning toodo prognozie pogody (szansy ustaniu) przy użyciu hello temperatury i wilgotności danych z Centrum Azure IoT. ryzyko Hello ustaniu jest wyjściem hello przygotowane pogody modelu prognozy. Hello model oparto na ryzyko tooforecast danych historycznych ustaniu na podstawie temperatury i wilgotności.

## <a name="what-you-do"></a>Co zrobić

- Wdrażanie modelu prognozy pogody hello jako usługę sieci web.
- Przygotuj się Centrum IoT na dostęp do danych przez dodanie grupy odbiorców.
- Utwórz zadanie usługi analiza strumienia i skonfiguruj na powitania zadania:
  - Odczytywanie danych temperatury i wilgotności z Centrum IoT.
  - Wywołanie hello sieci web usługi tooget hello ustaniu szansy.
  - Zapisz magazynu obiektów blob Azure tooan wynik hello.
- Użyj prognozie pogody hello tooview Eksploratora magazynu Microsoft Azure.

## <a name="what-you-need"></a>Co jest potrzebne

- Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje hello następujące wymagania:
  - Aktywna subskrypcja platformy Azure.
  - Centrum Azure IoT w ramach Twojej subskrypcji.
  - Aplikacja klienta, która wysyła komunikaty tooyour Azure IoT hub.
- Konto usługi Azure Machine Learning Studio. ([Bezpłatnie spróbuj Machine Learning Studio](https://studio.azureml.net/)).

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a>Wdróż hello pogody prognozowania model jako usługę sieci web

1. Przejdź toohello [stronę modelu prognozy pogody](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).
1. Kliknij przycisk **Otwórz w Studio** w usłudze Microsoft Azure Machine Learning Studio.
   ![Otwórz hello pogody prognozowania modelu strony w Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)
1. Kliknij przycisk **Uruchom** toovalidate hello etapami hello modelu. Ten krok może potrwać toocomplete 2 minuty.
   ![Otwórz hello pogody prognozowania modelu w usłudze Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Kliknij przycisk **Konfigurowanie usługi sieci WEB** > **usługi sieci Web predykcyjnej**.
   ![Wdróż model prognozowania pogody hello w usłudze Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)
1. Na diagramie hello przeciągnij hello **sieci Web dane wejściowe usługi** modułu gdzieś w pobliżu hello **Score Model** modułu.
1. Połącz hello **sieci Web dane wejściowe usługi** toohello modułu **Score Model** modułu.
   ![Połącz dwa moduły w usłudze Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)
1. Kliknij przycisk **Uruchom** toovalidate hello etapami hello modelu.
1. Kliknij przycisk **wdrażanie usługi sieci WEB** toodeploy hello model jako usługę sieci web.
1. Na pulpicie nawigacyjnym hello hello modelu, Pobierz hello **programu Excel 2010 lub starszych skoroszytu** dla **ŻĄDANIA/odpowiedzi**.

   > [!Note]
   > Upewnij się, że pobierać hello **programu Excel 2010 lub starszych skoroszytu** nawet wtedy, gdy używasz nowszej wersji programu Excel na tym komputerze.

   ![Pobierz hello programu Excel dla punktu końcowego odpowiedzi na żądanie hello](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. Otwórz skoroszyt programu Excel hello, zanotuj hello **adres URL usługi sieci WEB** i **klucz dostępu**.

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a>Tworzenie, konfigurowanie i uruchamianie zadania usługi analiza strumienia

### <a name="create-a-stream-analytics-job"></a>Tworzenie zadania usługi Stream Analytics

1. W hello [portalu Azure](https://ms.portal.azure.com/), kliknij przycisk **nowy** > **Internetu rzeczy** > **zadanie usługi Stream Analytics**.
1. Wprowadź następujące informacje dotyczące zadania hello hello.

   **Nazwa zadania**: Nazwa hello hello zadania. Nazwa Hello musi być globalnie unikatowa.

   **Grupa zasobów**: Użyj hello sam grupę zasobów, która korzysta z Centrum IoT.

   **Lokalizacja**: Użyj hello sam lokalizacji, w grupie zasobów.

   **Numer PIN toodashboard**: Zaznacz tę opcję, Centrum IoT tooyour łatwy dostęp z poziomu pulpitu nawigacyjnego hello.

   ![Utwórz zadanie usługi Stream Analytics na platformie Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. Kliknij przycisk **Utwórz**.

### <a name="add-an-input-toohello-stream-analytics-job"></a>Dodaj zadanie usługi analiza strumienia wejściowego toohello

1. Zadanie Stream Analytics hello otwarte.
1. W obszarze **topologii zadania**, kliknij przycisk **dane wejściowe**.
1. W hello **dane wejściowe** okienku, kliknij przycisk **Dodaj**, a następnie wprowadź hello następujących informacji:

   **Alias wejściowy**: hello unikatowego aliasu dla hello danych wejściowych.

   **Źródło**: Wybierz **Centrum IoT**.

   **Grupy odbiorców**: grupy odbiorców hello wybierz utworzony.

   ![Dodaj zadanie usługi analiza strumienia wejściowego toohello na platformie Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. Kliknij przycisk **Utwórz**.

### <a name="add-an-output-toohello-stream-analytics-job"></a>Dodaj zadanie usługi analiza strumienia wyjściowego toohello

1. W obszarze **topologii zadania**, kliknij przycisk **dane wyjściowe**.
1. W hello **dane wyjściowe** okienku, kliknij przycisk **Dodaj**, a następnie wprowadź hello następujących informacji:

   **Alias wyjściowy**: hello unikatowego aliasu dla hello danych wyjściowych.

   **Obiekt sink**: Wybierz **magazynu obiektów Blob**.

   **Konto magazynu**: hello konta magazynu dla usługi magazynu obiektów blob. Można utworzyć konta magazynu lub użyć istniejącego.

   **Kontener**: hello kontenera, której jest zapisywany hello obiektu blob. Możesz utworzyć kontener lub użyć istniejącego.

   **Format serializacji zdarzeń**: Wybierz **CSV**.

   ![Dodaj zadanie usługi analiza strumienia wyjściowego toohello na platformie Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. Kliknij przycisk **Utwórz**.

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a>Dodawanie funkcji toohello analiza strumienia zadania toocall hello usługi sieci web wdrożone

1. W obszarze **topologii zadania**, kliknij przycisk **funkcje** > **Dodaj**.
1. Wprowadź hello następujących informacji:

   **Funkcja Alias**: wprowadź `machinelearning`.

   **Typ funkcji**: Wybierz **Azure ML**.

   **Opcji importowania**: Wybierz **importu z innej subskrypcji**.

   **Adres URL**: Wprowadź adres URL usługi sieci WEB zanotowaną w dół hello hello skoroszycie programu Excel.

   **Klucz**: Wprowadź hello klucz dostępu, zanotowaną w dół hello skoroszycie programu Excel.

   ![Dodaj zadanie usługi Stream Analytics toohello funkcji na platformie Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. Kliknij przycisk **Utwórz**.

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a>Skonfiguruj zapytania hello hello zadania usługi analiza strumienia

1. W obszarze **topologii zadania**, kliknij przycisk **zapytania**.
1. Zastąp istniejący kod hello hello następującego kodu:

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   Zastąp `[YourInputAlias]` z aliasem hello wejściowych hello zadania.

   Zastąp `[YourOutputAlias]` z alias wyjściowy hello hello zadania.

1. Kliknij pozycję **Zapisz**.

### <a name="run-hello-stream-analytics-job"></a>Uruchom zadanie usługi Stream Analytics hello

W zadaniu Stream Analytics hello, kliknij przycisk **Start** > **teraz** > **Start**. Po pomyślnym uruchomieniu zadania hello hello stan zadania zmieni się z **zatrzymane** za**systemem**.

![Uruchom zadanie usługi Stream Analytics hello](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a>Użyj prognozie pogody hello tooview Eksploratora magazynu Microsoft Azure

Uruchom powitania klienta aplikacji toostart zbieranie i wysyłanie temperatury i wilgotności Centrum IoT tooyour danych. Dla każdego komunikatu, który odbiera Centrum IoT zadanie usługi Stream Analytics hello wywołuje hello prognozie pogody sieci web usługi tooproduce hello ryzyko ustaniu. wynik Hello jest zapisywane tooyour magazynu obiektów blob Azure. Eksplorator usługi Storage platformy Azure to narzędzie służy tooview hello wynik.

1. [Pobieranie i instalowanie Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).
1. Otwórz Eksploratora usługi Storage platformy Azure.
1. Zaloguj się tooyour konto platformy Azure.
1. Wybierz subskrypcję.
1. Kliknij subskrypcję > **kont magazynu** > Twoje konto magazynu > **kontenerów obiektów Blob** > z kontenera.
1. Otwórz wynik hello toosee pliku CSV. ostatnie rekordy kolumny Hello hello szansy ustaniu.

   ![Uzyskanie wyniku prognozie pogody przy użyciu usługi Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a>Podsumowanie

Pomyślnie użyto usługi Azure Machine Learning tooproduce hello ryzyko ustaniu na podstawie danych temperatury i wilgotności hello, który odbiera Centrum IoT.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]