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
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="555e4-103">Tworzenie źródła zdarzeń dla danego środowiska Insights serii czasu za pomocą portalu Ibiza hello</span><span class="sxs-lookup"><span data-stu-id="555e4-103">Create an event source for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="555e4-104">Źródło zdarzeń usługi Time Series Insights pochodzi od brokera zdarzeń, takiego jak usługa Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="555e4-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="555e4-105">Czas serii Insights łączy bezpośrednio tooEvent źródeł, wprowadzania hello strumienia danych bez konieczności toowrite użytkowników pojedynczy wiersz kodu.</span><span class="sxs-lookup"><span data-stu-id="555e4-105">Time Series Insights connects directly tooEvent Sources, ingesting hello data stream without requiring users toowrite a single line of code.</span></span> <span data-ttu-id="555e4-106">Obecnie usługa Time Series Insights obsługuje centra zdarzeń Azure Event Hub i Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="555e4-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="555e4-107">W przyszłości hello zostanie dodany więcej źródła zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="555e4-107">In hello future, more Event Sources will be added.</span></span>

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a><span data-ttu-id="555e4-108">Kroki tooadd środowisku tooyour źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="555e4-108">Steps tooadd an event source tooyour environment</span></span>

1.  <span data-ttu-id="555e4-109">Zaloguj się toohello [portalu Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="555e4-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="555e4-110">Kliknij przycisk "Wszystkie zasoby" hello menu po lewej stronie portalu Ibiza hello hello.</span><span class="sxs-lookup"><span data-stu-id="555e4-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3.  <span data-ttu-id="555e4-111">Wybierz środowisko usługi Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="555e4-111">Select your Time Series Insights environment.</span></span>

  ![Tworzenie źródła zdarzeń Insights serii czasu hello](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="555e4-113">Wybierz pozycję „Źródła zdarzeń” i kliknij przycisk „+ Dodaj”.</span><span class="sxs-lookup"><span data-stu-id="555e4-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Tworzenie źródła zdarzeń Insights serii czasu hello — szczegóły](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="555e4-115">Określ nazwę hello hello źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="555e4-115">Specify hello name of hello event source.</span></span> <span data-ttu-id="555e4-116">Nazwa ta zostanie skojarzona ze wszystkimi zdarzeniami pochodzącymi z tego źródła zdarzeń i będzie dostępna w czasie wykonywania zapytań.</span><span class="sxs-lookup"><span data-stu-id="555e4-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="555e4-117">Wybierz Centrum zdarzeń z listy hello zasobów Centrum zdarzeń w hello bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="555e4-117">Select an event hub from hello list of Event Hub resources in hello current subscription.</span></span> <span data-ttu-id="555e4-118">W przeciwnym razie wybierz opcję Importuj "ustawień Centrum zdarzeń Podaj ręcznie" toospecify Centrum zdarzeń w innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="555e4-118">Otherwise choose import option "Provide Event Hub settings manually” toospecify an event hub in another subscription.</span></span> <span data-ttu-id="555e4-119">Zdarzenia muszą być publikowane w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="555e4-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="555e4-120">Wybierz zasady, które ma uprawnienie w Centrum zdarzeń hello do odczytu.</span><span class="sxs-lookup"><span data-stu-id="555e4-120">Select policy that has read permission in hello event hub.</span></span>
8.  <span data-ttu-id="555e4-121">Wskaż grupę odbiorców centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="555e4-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="555e4-122">Sprawdź, czy ta grupa odbiorców nie jest używana przez żadną inną usługę (np. zadanie usługi Stream Analytics lub drugie środowisko usługi Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="555e4-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="555e4-123">Jeśli grupy odbiorców jest używany przez inne usługi, odczytać negatywny wpływ na operację dla tego środowiska i hello innych usług.</span><span class="sxs-lookup"><span data-stu-id="555e4-123">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="555e4-124">Jeśli używasz "$Default" jako grupy odbiorców hello, połączenie może prowadzić ponownemu toopotential przez inne czytników.</span><span class="sxs-lookup"><span data-stu-id="555e4-124">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

9.  <span data-ttu-id="555e4-125">Kliknij przycisk „Utwórz”.</span><span class="sxs-lookup"><span data-stu-id="555e4-125">Click “Create.”</span></span>

<span data-ttu-id="555e4-126">Po utworzeniu hello źródło zdarzenia czas serii wgląd uruchomi strumieniowego przesyłania danych do środowiska.</span><span class="sxs-lookup"><span data-stu-id="555e4-126">After creation of hello event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="555e4-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="555e4-127">Next steps</span></span>

* <span data-ttu-id="555e4-128">[Wysyłanie zdarzeń](time-series-insights-send-events.md) toohello źródło zdarzenia</span><span class="sxs-lookup"><span data-stu-id="555e4-128">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="555e4-129">Wyświetlanie środowiska w [Portalu usługi Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="555e4-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
