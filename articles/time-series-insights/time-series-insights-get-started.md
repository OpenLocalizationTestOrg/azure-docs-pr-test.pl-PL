---
title: "aaaCreate środowiska Azure czas serii Insights | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, jak toocreate środowisko serii czasu, podłącz go źródło zdarzenia tooan i gotowe tooanalyze danych zdarzeń w minutach."
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
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a><span data-ttu-id="77e41-103">Tworzenie nowego środowiska czasu serii wgląd w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="77e41-103">Create a new Time Series Insights environment in hello Azure portal</span></span>

<span data-ttu-id="77e41-104">Środowisko usługi Time Series Insights jest zasobem platformy Azure, który umożliwia pozyskiwanie i magazynowanie danych.</span><span class="sxs-lookup"><span data-stu-id="77e41-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="77e41-105">Klienci udostępnić środowiska za pośrednictwem portalu Azure hello hello wymagana pojemność.</span><span class="sxs-lookup"><span data-stu-id="77e41-105">Customers provision environments via hello Azure portal with hello required capacity.</span></span>

## <a name="steps-toocreate-hello-environment"></a><span data-ttu-id="77e41-106">Kroki toocreate hello środowiska</span><span class="sxs-lookup"><span data-stu-id="77e41-106">Steps toocreate hello environment</span></span>

<span data-ttu-id="77e41-107">Wykonaj te kroki toocreate środowiska:</span><span class="sxs-lookup"><span data-stu-id="77e41-107">Follow these steps toocreate your environment:</span></span>

1.  <span data-ttu-id="77e41-108">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="77e41-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="77e41-109">Kliknij znak ("+") plus hello hello górnym lewym rogu.</span><span class="sxs-lookup"><span data-stu-id="77e41-109">Click hello plus sign (“+”) in hello top left corner.</span></span>
3.  <span data-ttu-id="77e41-110">Wyszukiwanie "Czas serii Insights" w polu wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="77e41-110">Search for “Time Series Insights” in hello search box.</span></span>

  ![Utwórz środowisko czasu serii Insights hello](media/get-started/getstarted-create-environment1.png)

4.  <span data-ttu-id="77e41-112">Wybierz pozycję „Time Series Insights” i kliknij przycisk „Utwórz”.</span><span class="sxs-lookup"><span data-stu-id="77e41-112">Select “Time Series Insights”, click “Create”.</span></span>

  ![Utwórz grupę zasobów hello Insights serii czasu](media/get-started/getstarted-create-environment2.png)

5.  <span data-ttu-id="77e41-114">Podaj nazwę środowiska.</span><span class="sxs-lookup"><span data-stu-id="77e41-114">Specify environment name.</span></span> <span data-ttu-id="77e41-115">Ta nazwa będzie reprezentować środowiska hello [Eksploratorze serię czas](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="77e41-115">This name will represent hello environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="77e41-116">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="77e41-116">Select a subscription.</span></span> <span data-ttu-id="77e41-117">Musi ona zawierać źródło zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="77e41-117">Choose one that contains your event source.</span></span> <span data-ttu-id="77e41-118">Czas serii Insights może automatycznie wykrywa Centrum IoT Azure i Centrum zdarzeń zasobów istniejących w hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="77e41-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in hello same subscription.</span></span>
7.  <span data-ttu-id="77e41-119">Wybierz lub utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="77e41-119">Select or create a resource group.</span></span> <span data-ttu-id="77e41-120">Grupa zasobów jest kolekcją używanych razem zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77e41-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="77e41-121">Wybierz lokalizację hostowania.</span><span class="sxs-lookup"><span data-stu-id="77e41-121">Select a hosting location.</span></span> <span data-ttu-id="77e41-122">w centrach tooavoid przenoszenie danych między danych, wybierz lokalizację, która zawiera źródło zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="77e41-122">tooavoid moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="77e41-123">Wybierz warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="77e41-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="77e41-124">Wybierz wydajność.</span><span class="sxs-lookup"><span data-stu-id="77e41-124">Select capacity.</span></span> <span data-ttu-id="77e41-125">Wydajność środowiska można zmienić po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="77e41-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="77e41-126">Utwórz środowisko.</span><span class="sxs-lookup"><span data-stu-id="77e41-126">Create your environment.</span></span> <span data-ttu-id="77e41-127">Możesz również przypiąć pulpitu nawigacyjnego toohello środowisko, by mieć łatwy dostęp przy każdym logowaniu.</span><span class="sxs-lookup"><span data-stu-id="77e41-127">You can also pin your environment toohello dashboard for easy access whenever you sign in.</span></span>

  ![Utwórz hello Insights serii czasu numeru pin toodashboard](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="77e41-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77e41-129">Next steps</span></span>

* <span data-ttu-id="77e41-130">[Definiowanie zasad dostępu danych](time-series-insights-data-access.md) tooaccess środowiska w [portalu Insights serii czasu](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="77e41-130">[Define data access policies](time-series-insights-data-access.md) tooaccess your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
* [<span data-ttu-id="77e41-131">Tworzenie źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="77e41-131">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="77e41-132">[Wysyłanie zdarzeń](time-series-insights-send-events.md) toohello źródło zdarzenia</span><span class="sxs-lookup"><span data-stu-id="77e41-132">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
