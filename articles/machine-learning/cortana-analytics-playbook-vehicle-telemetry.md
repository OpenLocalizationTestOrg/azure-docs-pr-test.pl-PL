---
title: "aaaPredict vehicle kondycji i wspierającym zwyczaje - Azure | Dokumentacja firmy Microsoft"
description: "Korzystanie z możliwości hello wgląd w czasie rzeczywistym oraz predykcyjnej toogain Cortana Intelligence na kondycji vehicle i wspierającym zwyczaje."
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
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="29243-103">Podręcznik dotyczący rozwiązań analizy telemetrii pojazdów</span><span class="sxs-lookup"><span data-stu-id="29243-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="29243-104">To **menu** toohello rozdziałów tego podręcznika dotyczącego łączy.</span><span class="sxs-lookup"><span data-stu-id="29243-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="29243-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="29243-105">Overview</span></span>
<span data-ttu-id="29243-106">Komputery Super został przeniesiony poza hello laboratorium i są teraz stoi w naszym garaż!</span><span class="sxs-lookup"><span data-stu-id="29243-106">Super computers have moved out of hello lab and are now parked in our garage!</span></span> <span data-ttu-id="29243-107">Tych samochodów najnowocześniejsze zawierać większą liczbą czujników, zapewniając im hello możliwości tootrack i monitorować miliony zdarzeń w ciągu sekundy.</span><span class="sxs-lookup"><span data-stu-id="29243-107">These cutting-edge automobiles contain a myriad of sensors, giving them hello ability tootrack and monitor millions of events every second.</span></span> <span data-ttu-id="29243-108">Oczekuje się, że 2020, większość tych samochodów będzie zostały toohello połączenia internetowego.</span><span class="sxs-lookup"><span data-stu-id="29243-108">We expect that by 2020, most of these cars will have been connected toohello Internet.</span></span> <span data-ttu-id="29243-109">Wyobraź sobie naciśnięcie przycisku do tego wiele danych tooprovide większe bezpieczeństwo, niezawodność i pobudzenie lepsze środowisko!</span><span class="sxs-lookup"><span data-stu-id="29243-109">Imagine tapping into this wealth of data tooprovide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="29243-110">Firma Microsoft wprowadziła to marzy rzeczywistością z Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="29243-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="29243-111">Firmy Microsoft Cortana Intelligence jest w pełni zarządzana danych big data oraz zaawansowane analytics suite, umożliwiający tootransform danych do inteligentnego akcji.</span><span class="sxs-lookup"><span data-stu-id="29243-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you tootransform your data into intelligent action.</span></span> <span data-ttu-id="29243-112">Chcemy toointroduce toohello szablon rozwiązania Analytics Telemetrii Cortana Intelligence pojazdów.</span><span class="sxs-lookup"><span data-stu-id="29243-112">We want toointroduce you toohello Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="29243-113">To rozwiązanie pokazano, jak przedstawicielstw samochodu handlowych, producentów samochodów i ubezpieczeń można użyć możliwości hello toogain Cortana analizy w czasie rzeczywistym i zwyczaje predykcyjnej rozeznanie vehicle kondycji i wspierającym.</span><span class="sxs-lookup"><span data-stu-id="29243-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="29243-114">rozwiązanie Hello jest zaimplementowany jako [wzorzec architektury lambda](https://en.wikipedia.org/wiki/Lambda_architecture) przedstawiający hello potencjał platformy Cortana Intelligence hello w czasie rzeczywistym i przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="29243-114">hello solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing hello full potential of hello Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="29243-115">rozwiązanie Hello:</span><span class="sxs-lookup"><span data-stu-id="29243-115">hello solution:</span></span> 

* <span data-ttu-id="29243-116">udostępnia symulatora telematyki Vehicle</span><span class="sxs-lookup"><span data-stu-id="29243-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="29243-117">korzysta z usługi Event Hubs służy do wprowadzania miliony zdarzeń telemetrii symulowane vehicle na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="29243-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="29243-118">używa wgląd w czasie rzeczywistym usługi Stream Analytics toogain na vehicle kondycji</span><span class="sxs-lookup"><span data-stu-id="29243-118">uses Stream Analytics toogain real-time insights on vehicle health</span></span>
* <span data-ttu-id="29243-119">utrzymuje hello danych do długoterminowego przechowywania dla bardziej zaawansowane funkcje analizy partii.</span><span class="sxs-lookup"><span data-stu-id="29243-119">persists hello data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="29243-120">korzysta z uczenia maszynowego wykrywania anomalii w czasie rzeczywistym i insights predykcyjnej toogain przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="29243-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="29243-121">wykorzystanie danych tootransform HDInsight w skali i fabryki danych orchestration toohandle, planowanie, zarządzanie zasobami i monitorowanie potoku przetwarzania wsadowego hello</span><span class="sxs-lookup"><span data-stu-id="29243-121">leverages HDInsight tootransform data at scale and Data Factory toohandle orchestration, scheduling, resource management, and monitoring of hello batch processing pipeline</span></span> 
* <span data-ttu-id="29243-122">daje to rozwiązanie sformatowanego pulpitu nawigacyjnego w czasie rzeczywistym danych i wizualizacji analizy predykcyjnej przy użyciu usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="29243-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="29243-123">Architektura</span><span class="sxs-lookup"><span data-stu-id="29243-123">Architecture</span></span>
<span data-ttu-id="29243-124">![Diagram architektury rozwiązania](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*rysunek 1 — Architektura rozwiązania analizy Telemetrii Vehicle*</span><span class="sxs-lookup"><span data-stu-id="29243-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="29243-125">To rozwiązanie obejmuje następujące hello **Cortana Intelligence składniki** i ich integracji tooend zakończenia ilustrację:</span><span class="sxs-lookup"><span data-stu-id="29243-125">This solution includes hello following **Cortana Intelligence components** and showcases their end tooend integration:</span></span>

* <span data-ttu-id="29243-126">**Centra zdarzeń** służy do wprowadzania miliony zdarzeń telemetrii vehicle na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="29243-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="29243-127">**Analiza strumienia** do uzyskania wgląd w czasie rzeczywistym w kondycję vehicle i będzie się powtarzał tych danych do długoterminowego przechowywania dla bardziej zaawansowane funkcje analizy partii.</span><span class="sxs-lookup"><span data-stu-id="29243-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="29243-128">**Machine Learning** wykrywania anomalii w czasie rzeczywistym i insights predykcyjnej toogain przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="29243-128">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="29243-129">**HDInsight** jest wykorzystywana tootransform danych na dużą skalę</span><span class="sxs-lookup"><span data-stu-id="29243-129">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="29243-130">**Fabryka danych** obsługuje aranżacji, potoku przetwarzania wsadowego hello monitorowania i planowania zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="29243-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>
* <span data-ttu-id="29243-131">**Power BI** daje to rozwiązanie sformatowanego pulpitu nawigacyjnego w czasie rzeczywistym danych i wizualizacji analizy predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="29243-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="29243-132">To rozwiązanie uzyskuje dostęp do dwóch różnych **źródeł danych**:</span><span class="sxs-lookup"><span data-stu-id="29243-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="29243-133">**Symulowane sygnały vehicle i informacji diagnostycznych**: symulatora telematyki vehicle emituje sygnałów, które odpowiadają toohello stan hello vehicle i hello zwiększają wzorca w danym punkcie w czasie i informacji diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="29243-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond toohello state of hello vehicle and hello driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="29243-134">**Vehicle katalogu**: odwołanie do zestawu danych zawierające mapowanie toomodel VIN.</span><span class="sxs-lookup"><span data-stu-id="29243-134">**Vehicle catalog**: A reference dataset containing a VIN toomodel mapping.</span></span>

