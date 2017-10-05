---
title: "Przewidywanie vehicle kondycji i wspierającym zwyczaje - Azure | Dokumentacja firmy Microsoft"
description: "Korzystanie z możliwości Cortana Intelligence, aby uzyskać wgląd w czasie rzeczywistym oraz predykcyjnej na vehicle kondycji i wspierającym zwyczaje."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: d202d314c61416cf306f760f93e0a4a88a1ab42b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="acbbb-103">Podręcznik dotyczący rozwiązań analizy telemetrii pojazdów</span><span class="sxs-lookup"><span data-stu-id="acbbb-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="acbbb-104">To **menu** łącza do rozdziały tego podręcznika dotyczącego.</span><span class="sxs-lookup"><span data-stu-id="acbbb-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="acbbb-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="acbbb-105">Overview</span></span>
<span data-ttu-id="acbbb-106">Komputery Super został przeniesiony poza laboratorium i są teraz stoi w naszym garaż!</span><span class="sxs-lookup"><span data-stu-id="acbbb-106">Super computers have moved out of the lab and are now parked in our garage!</span></span> <span data-ttu-id="acbbb-107">Tych samochodów najnowocześniejsze zawierać większą liczbą czujników, zapewniając im możliwość śledzenie i monitorowanie miliony zdarzeń w ciągu sekundy.</span><span class="sxs-lookup"><span data-stu-id="acbbb-107">These cutting-edge automobiles contain a myriad of sensors, giving them the ability to track and monitor millions of events every second.</span></span> <span data-ttu-id="acbbb-108">Oczekuje się, że 2020, większość tych samochodów będzie mieć został połączony z Internetem.</span><span class="sxs-lookup"><span data-stu-id="acbbb-108">We expect that by 2020, most of these cars will have been connected to the Internet.</span></span> <span data-ttu-id="acbbb-109">Wyobraź sobie naciśnięcie przycisku w tym wiele danych, aby zapewnić większe bezpieczeństwo, niezawodność i pobudzenie lepsze środowisko!</span><span class="sxs-lookup"><span data-stu-id="acbbb-109">Imagine tapping into this wealth of data to provide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="acbbb-110">Firma Microsoft wprowadziła to marzy rzeczywistością z Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="acbbb-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="acbbb-111">Firmy Microsoft Cortana Intelligence jest pełni zarządzanych danych big data oraz pakiet zaawansowane metody analizy, który pozwala na przekształcanie danych do inteligentnego akcji.</span><span class="sxs-lookup"><span data-stu-id="acbbb-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you to transform your data into intelligent action.</span></span> <span data-ttu-id="acbbb-112">Chcemy przedstawiono szablon rozwiązania analizy Telemetrii Cortana analizy pojazdów.</span><span class="sxs-lookup"><span data-stu-id="acbbb-112">We want to introduce you to the Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="acbbb-113">To rozwiązanie pokazano, jak przedstawicielstw samochodu handlowych, producentów samochodów i ubezpieczeń można używać funkcji Cortana Intelligence w celu uzyskania w czasie rzeczywistym i zwyczaje predykcyjnej rozeznanie vehicle kondycji i wspierającym.</span><span class="sxs-lookup"><span data-stu-id="acbbb-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="acbbb-114">Rozwiązanie jest zaimplementowany jako [wzorzec architektury lambda](https://en.wikipedia.org/wiki/Lambda_architecture) przedstawiający potencjalnych platformy Cortana Intelligence pełnego w czasie rzeczywistym i przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="acbbb-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing the full potential of the Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="acbbb-115">Rozwiązanie:</span><span class="sxs-lookup"><span data-stu-id="acbbb-115">The solution:</span></span> 

* <span data-ttu-id="acbbb-116">udostępnia symulatora telematyki Vehicle</span><span class="sxs-lookup"><span data-stu-id="acbbb-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="acbbb-117">korzysta z usługi Event Hubs służy do wprowadzania miliony zdarzeń telemetrii symulowane vehicle na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="acbbb-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="acbbb-118">używa Stream Analytics, aby uzyskać wgląd w czasie rzeczywistym w kondycję vehicle</span><span class="sxs-lookup"><span data-stu-id="acbbb-118">uses Stream Analytics to gain real-time insights on vehicle health</span></span>
* <span data-ttu-id="acbbb-119">utrzymuje dane do długoterminowego przechowywania dla bardziej zaawansowane funkcje analizy partii.</span><span class="sxs-lookup"><span data-stu-id="acbbb-119">persists the data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="acbbb-120">korzysta z uczenia maszynowego wykrywania anomalii w czasie rzeczywistym i partii przetwarzania, aby uzyskać wgląd predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="acbbb-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="acbbb-121">wykorzystuje HDInsight do transformacji danych na dużą skalę i fabryki danych do obsługi aranżacji, planowania, zarządzanie zasobami i monitorowania w potoku przetwarzania wsadowego</span><span class="sxs-lookup"><span data-stu-id="acbbb-121">leverages HDInsight to transform data at scale and Data Factory to handle orchestration, scheduling, resource management, and monitoring of the batch processing pipeline</span></span> 
* <span data-ttu-id="acbbb-122">daje to rozwiązanie sformatowanego pulpitu nawigacyjnego w czasie rzeczywistym danych i wizualizacji analizy predykcyjnej przy użyciu usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="acbbb-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="acbbb-123">Architektura</span><span class="sxs-lookup"><span data-stu-id="acbbb-123">Architecture</span></span>
<span data-ttu-id="acbbb-124">![Diagram architektury rozwiązania](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*rysunek 1 — Architektura rozwiązania analizy Telemetrii Vehicle*</span><span class="sxs-lookup"><span data-stu-id="acbbb-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="acbbb-125">To rozwiązanie obejmuje następujące elementy **Cortana Intelligence składniki** i ich integracji kompleksowe ilustrację:</span><span class="sxs-lookup"><span data-stu-id="acbbb-125">This solution includes the following **Cortana Intelligence components** and showcases their end to end integration:</span></span>

* <span data-ttu-id="acbbb-126">**Centra zdarzeń** służy do wprowadzania miliony zdarzeń telemetrii vehicle na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="acbbb-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="acbbb-127">**Analiza strumienia** do uzyskania wgląd w czasie rzeczywistym w kondycję vehicle i będzie się powtarzał tych danych do długoterminowego przechowywania dla bardziej zaawansowane funkcje analizy partii.</span><span class="sxs-lookup"><span data-stu-id="acbbb-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="acbbb-128">**Machine Learning** wykrywania anomalii w czasie rzeczywistym i przetwarzanie wsadowe, aby uzyskać wgląd predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="acbbb-128">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="acbbb-129">**HDInsight** jest wykorzystywana do przekształcania danych na dużą skalę</span><span class="sxs-lookup"><span data-stu-id="acbbb-129">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="acbbb-130">**Fabryka danych** obsługuje aranżacji, Planowanie zarządzania zasobami i monitorowania w potoku przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="acbbb-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>
* <span data-ttu-id="acbbb-131">**Power BI** daje to rozwiązanie sformatowanego pulpitu nawigacyjnego w czasie rzeczywistym danych i wizualizacji analizy predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="acbbb-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="acbbb-132">To rozwiązanie uzyskuje dostęp do dwóch różnych **źródeł danych**:</span><span class="sxs-lookup"><span data-stu-id="acbbb-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="acbbb-133">**Symulowane sygnały vehicle i informacji diagnostycznych**: symulatora telematyki vehicle emituje informacje diagnostyczne i sygnalizuje, że odpowiada do stanu mechanizm i kierowania wzorca w danym punkcie w czasie.</span><span class="sxs-lookup"><span data-stu-id="acbbb-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="acbbb-134">**Vehicle katalogu**: odwołanie do zestawu danych zawierającego VIN do mapowania modelu.</span><span class="sxs-lookup"><span data-stu-id="acbbb-134">**Vehicle catalog**: A reference dataset containing a VIN to model mapping.</span></span>

