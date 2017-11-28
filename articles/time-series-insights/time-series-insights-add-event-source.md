---
title: "Dodawanie źródła zdarzeń do środowiska usługi Azure Time Series Insights | Microsoft Docs"
description: "W tym samouczku omówiono łączenie źródła zdarzeń ze środowiskiem usługi Time Series Insights"
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
ms.openlocfilehash: ffa2eaf3680e68ac14aabf49b6308caeb173fd43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-the-ibiza-portal"></a><span data-ttu-id="07b71-103">Tworzenie źródła zdarzeń dla środowiska usługi Time Series Insights przy użyciu portalu Ibiza</span><span class="sxs-lookup"><span data-stu-id="07b71-103">Create an event source for your Time Series Insights environment using the Ibiza portal</span></span>

<span data-ttu-id="07b71-104">Źródło zdarzeń usługi Time Series Insights pochodzi od brokera zdarzeń, takiego jak usługa Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="07b71-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="07b71-105">Usługa Time Series Insights łączy się bezpośrednio ze źródłami zdarzeń, umożliwiając pozyskiwanie strumienia danych bez konieczności pisania kodu przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="07b71-105">Time Series Insights connects directly to Event Sources, ingesting the data stream without requiring users to write a single line of code.</span></span> <span data-ttu-id="07b71-106">Obecnie usługa Time Series Insights obsługuje centra zdarzeń Azure Event Hub i Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="07b71-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs.</span></span> <span data-ttu-id="07b71-107">W przyszłości zostanie dodanych więcej źródeł zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="07b71-107">In the future, more Event Sources will be added.</span></span>

## <a name="steps-to-add-an-event-source-to-your-environment"></a><span data-ttu-id="07b71-108">Procedura dodawania źródła zdarzeń do środowiska</span><span class="sxs-lookup"><span data-stu-id="07b71-108">Steps to add an event source to your environment</span></span>

1.  <span data-ttu-id="07b71-109">Zaloguj się w [portalu Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07b71-109">Sign in to the [Ibiza portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="07b71-110">W menu po lewej stronie w portalu Ibiza kliknij pozycję „Wszystkie zasoby”.</span><span class="sxs-lookup"><span data-stu-id="07b71-110">Click “All resources” in the menu on the left side of the Ibiza portal.</span></span>
3.  <span data-ttu-id="07b71-111">Wybierz środowisko usługi Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="07b71-111">Select your Time Series Insights environment.</span></span>

  ![Tworzenie źródła zdarzeń usługi Time Series Insights](media/add-event-source/getstarted-create-event-source-1.png)

4.  <span data-ttu-id="07b71-113">Wybierz pozycję „Źródła zdarzeń” i kliknij przycisk „+ Dodaj”.</span><span class="sxs-lookup"><span data-stu-id="07b71-113">Select “Event Sources”, click “+ Add.”</span></span>

  ![Tworzenie źródła zdarzeń usługi Time Series Insights — szczegóły](media/add-event-source/getstarted-create-event-source-2.png)

5.  <span data-ttu-id="07b71-115">Podaj nazwę źródła zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="07b71-115">Specify the name of the event source.</span></span> <span data-ttu-id="07b71-116">Nazwa ta zostanie skojarzona ze wszystkimi zdarzeniami pochodzącymi z tego źródła zdarzeń i będzie dostępna w czasie wykonywania zapytań.</span><span class="sxs-lookup"><span data-stu-id="07b71-116">This name is associated with all events coming from this event source and is available at query time.</span></span>
6.  <span data-ttu-id="07b71-117">Wybierz centrum zdarzeń z listy zasobów Centrum zdarzeń w bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="07b71-117">Select an event hub from the list of Event Hub resources in the current subscription.</span></span> <span data-ttu-id="07b71-118">W przeciwnym razie wybierz opcję importowania „Podaj ręcznie ustawienia centrum zdarzeń”, aby określić centrum zdarzeń w innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="07b71-118">Otherwise choose import option "Provide Event Hub settings manually” to specify an event hub in another subscription.</span></span> <span data-ttu-id="07b71-119">Zdarzenia muszą być publikowane w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="07b71-119">Events must be published in JSON format.</span></span>
7.  <span data-ttu-id="07b71-120">Wybierz zasady, które mają uprawnienia do odczytu w centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="07b71-120">Select policy that has read permission in the event hub.</span></span>
8.  <span data-ttu-id="07b71-121">Wskaż grupę odbiorców centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="07b71-121">Specify event hub consumer group.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="07b71-122">Sprawdź, czy ta grupa odbiorców nie jest używana przez żadną inną usługę (np. zadanie usługi Stream Analytics lub drugie środowisko usługi Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="07b71-122">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="07b71-123">Używanie grupy odbiorców przez inne usługi ma negatywny wpływ na operacje odczytu w bieżącym środowisku i tych usługach.</span><span class="sxs-lookup"><span data-stu-id="07b71-123">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="07b71-124">Użycie grupy odbiorców „$Default” może potencjalnie spowodować jej ponowne użycie przez inne czytniki.</span><span class="sxs-lookup"><span data-stu-id="07b71-124">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

9.  <span data-ttu-id="07b71-125">Kliknij przycisk „Utwórz”.</span><span class="sxs-lookup"><span data-stu-id="07b71-125">Click “Create.”</span></span>

<span data-ttu-id="07b71-126">Po utworzeniu źródła zdarzeń usługa Time Series Insights automatycznie rozpocznie przesyłanie strumieni danych do środowiska.</span><span class="sxs-lookup"><span data-stu-id="07b71-126">After creation of the event source, Time Series Insights will automatically start streaming data into your environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07b71-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07b71-127">Next steps</span></span>

* <span data-ttu-id="07b71-128">[Wysyłanie zdarzeń](time-series-insights-send-events.md) do źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="07b71-128">[Send events](time-series-insights-send-events.md) to the event source</span></span>
* <span data-ttu-id="07b71-129">Wyświetlanie środowiska w [Portalu usługi Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="07b71-129">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
