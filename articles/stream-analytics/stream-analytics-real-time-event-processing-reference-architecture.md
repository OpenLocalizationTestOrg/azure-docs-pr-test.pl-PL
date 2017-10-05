---
title: "Zdarzenia w czasie rzeczywistym przetwarzania za pomocą usługi Stream Analytics przetwarzania zdarzeń | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak to zestaw usług Azure mogą współdziałać umożliwiających analytics i przetwarzania zdarzeń w czasie rzeczywistym."
keywords: "przetwarzanie w czasie rzeczywistym, przetwarzanie zdarzeń, architektura referencyjna"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: b3057be995e551aac0761c3ce40a8dbf828a5f29
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="ffe02-104">Architektura odwołania: zdarzeń w czasie rzeczywistym przetwarzania za pomocą usługi Microsoft Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ffe02-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="ffe02-105">Architektura referencyjna dla zdarzenia w czasie rzeczywistym przetwarzania za pomocą usługi Azure Stream Analytics mają na celu dostarczenie ogólnego planu wdrażania platformy w czasie rzeczywistym jako rozwiązanie przetwarzania strumienia usługa (PaaS) w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ffe02-105">The reference architecture for real-time event processing with Azure Stream Analytics is intended to provide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="ffe02-106">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="ffe02-106">Summary</span></span>
<span data-ttu-id="ffe02-107">Tradycyjnie rozwiązań analitycznych, została oparta na możliwości, takie jak ETL (extract, transform, load) i magazynowanie danych, których są przechowywane dane przed analizą.</span><span class="sxs-lookup"><span data-stu-id="ffe02-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior to analysis.</span></span> <span data-ttu-id="ffe02-108">Zmieniających się wymagań, w tym więcej danych szybko nadchodzących, push istniejący model i ten limit.</span><span class="sxs-lookup"><span data-stu-id="ffe02-108">Changing requirements, including more rapidly arriving data, are pushing this existing model to the limit.</span></span> <span data-ttu-id="ffe02-109">Zdolność do analizowania danych w ramach przenoszenie strumieni przed magazynu jest jedno rozwiązanie, a mimo że nie jest dostępna nowa funkcja, to rozwiązanie nie powszechnie przyjęto we wszystkich przypadkach branżowych.</span><span class="sxs-lookup"><span data-stu-id="ffe02-109">The ability to analyze data within moving streams prior to storage is one solution, and while it is not a new capability, the approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="ffe02-110">Microsoft Azure udostępnia szeroką gamę katalog analytics technologii, które mogą obsłużyć tablicy scenariuszy różnych rozwiązań i wymagań.</span><span class="sxs-lookup"><span data-stu-id="ffe02-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="ffe02-111">Wybrać usługi systemu Azure, które do wdrożenia rozwiązania na trasie, może być wyzwaniem podana szerokość oferty.</span><span class="sxs-lookup"><span data-stu-id="ffe02-111">Selecting which Azure services to deploy for an end-to-end solution can be a challenge given the breadth of offerings.</span></span> <span data-ttu-id="ffe02-112">Ten dokument jest przeznaczony do opisano współdziałanie różnych usług Azure, które obsługują rozwiązanie strumienia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ffe02-112">This paper is designed to describe the capabilities and interoperation of the various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="ffe02-113">Objaśniono także niektóre scenariusze, w których klienci mogą korzystać z takiego podejścia.</span><span class="sxs-lookup"><span data-stu-id="ffe02-113">It also explains some of the scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="ffe02-114">Zawartość</span><span class="sxs-lookup"><span data-stu-id="ffe02-114">Contents</span></span>
* <span data-ttu-id="ffe02-115">Podsumowanie dla kierownictwa</span><span class="sxs-lookup"><span data-stu-id="ffe02-115">Executive Summary</span></span>
* <span data-ttu-id="ffe02-116">Wprowadzenie do analiz w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="ffe02-116">Introduction to Real-Time Analytics</span></span>
* <span data-ttu-id="ffe02-117">Wartości oferty w czasie rzeczywistym danych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ffe02-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="ffe02-118">Typowe scenariusze dotyczące analiz w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="ffe02-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="ffe02-119">Architektura i składniki</span><span class="sxs-lookup"><span data-stu-id="ffe02-119">Architecture and Components</span></span>
  * <span data-ttu-id="ffe02-120">Źródła danych</span><span class="sxs-lookup"><span data-stu-id="ffe02-120">Data Sources</span></span>
  * <span data-ttu-id="ffe02-121">Integracja danych warstwy</span><span class="sxs-lookup"><span data-stu-id="ffe02-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="ffe02-122">Warstwa analiz w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="ffe02-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="ffe02-123">Warstwa magazynu danych</span><span class="sxs-lookup"><span data-stu-id="ffe02-123">Data Storage Layer</span></span>
  * <span data-ttu-id="ffe02-124">Prezentacja / warstwy zużycie</span><span class="sxs-lookup"><span data-stu-id="ffe02-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="ffe02-125">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="ffe02-125">Conclusion</span></span>

<span data-ttu-id="ffe02-126">**Autor:** Centrum Insights danych Charlesa Feddersen, architektów rozwiązania doskonałości, firmy Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="ffe02-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="ffe02-127">**Opublikowane:** stycznia 2015</span><span class="sxs-lookup"><span data-stu-id="ffe02-127">**Published:** January 2015</span></span>

<span data-ttu-id="ffe02-128">**Poprawka:** 1.0</span><span class="sxs-lookup"><span data-stu-id="ffe02-128">**Revision:** 1.0</span></span>

<span data-ttu-id="ffe02-129">**Pobieranie:** [zdarzeń w czasie rzeczywistym przetwarzania za pomocą usługi Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="ffe02-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="ffe02-130">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="ffe02-130">Get help</span></span>
<span data-ttu-id="ffe02-131">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="ffe02-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffe02-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ffe02-132">Next steps</span></span>
* [<span data-ttu-id="ffe02-133">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ffe02-133">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ffe02-134">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="ffe02-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ffe02-135">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="ffe02-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ffe02-136">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="ffe02-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ffe02-137">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="ffe02-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

