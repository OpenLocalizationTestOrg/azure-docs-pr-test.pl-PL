---
title: "środowisko Azure czas serii Insights tooyour źródła zdarzeń aaaAdd | Dokumentacja firmy Microsoft"
description: "W tym samouczku połączyć środowisku czasu serii Insights tooyour źródła zdarzeń"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Tworzenie źródła zdarzeń dla danego środowiska Insights serii czasu za pomocą portalu Ibiza hello

Źródło zdarzeń usługi Time Series Insights pochodzi od brokera zdarzeń, takiego jak usługa Azure Event Hubs. Czas serii Insights łączy bezpośrednio tooEvent źródeł, wprowadzania hello strumienia danych bez konieczności toowrite użytkowników pojedynczy wiersz kodu. Obecnie usługa Time Series Insights obsługuje centra zdarzeń Azure Event Hub i Azure IoT Hub. W przyszłości hello zostanie dodany więcej źródła zdarzeń.

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a>Kroki tooadd środowisku tooyour źródła zdarzeń

1.  Zaloguj się toohello [portalu Ibiza](https://portal.azure.com).
2.  Kliknij przycisk "Wszystkie zasoby" hello menu po lewej stronie portalu Ibiza hello hello.
3.  Wybierz środowisko usługi Time Series Insights.

  ![Tworzenie źródła zdarzeń Insights serii czasu hello](media/add-event-source/getstarted-create-event-source-1.png)

4.  Wybierz pozycję „Źródła zdarzeń” i kliknij przycisk „+ Dodaj”.

  ![Tworzenie źródła zdarzeń Insights serii czasu hello — szczegóły](media/add-event-source/getstarted-create-event-source-2.png)

5.  Określ nazwę hello hello źródła zdarzenia. Nazwa ta zostanie skojarzona ze wszystkimi zdarzeniami pochodzącymi z tego źródła zdarzeń i będzie dostępna w czasie wykonywania zapytań.
6.  Wybierz Centrum zdarzeń z listy hello zasobów Centrum zdarzeń w hello bieżącej subskrypcji. W przeciwnym razie wybierz opcję Importuj "ustawień Centrum zdarzeń Podaj ręcznie" toospecify Centrum zdarzeń w innej subskrypcji. Zdarzenia muszą być publikowane w formacie JSON.
7.  Wybierz zasady, które ma uprawnienie w Centrum zdarzeń hello do odczytu.
8.  Wskaż grupę odbiorców centrum zdarzeń.

  > [!IMPORTANT]
  > Sprawdź, czy ta grupa odbiorców nie jest używana przez żadną inną usługę (np. zadanie usługi Stream Analytics lub drugie środowisko usługi Time Series Insights). Jeśli grupy odbiorców jest używany przez inne usługi, odczytać negatywny wpływ na operację dla tego środowiska i hello innych usług. Jeśli używasz "$Default" jako grupy odbiorców hello, połączenie może prowadzić ponownemu toopotential przez inne czytników.

9.  Kliknij przycisk „Utwórz”.

Po utworzeniu hello źródło zdarzenia czas serii wgląd uruchomi strumieniowego przesyłania danych do środowiska.

## <a name="next-steps"></a>Następne kroki

* [Wysyłanie zdarzeń](time-series-insights-send-events.md) toohello źródło zdarzenia
* Wyświetlanie środowiska w [Portalu usługi Time Series Insights](https://insights.timeseries.azure.com)
