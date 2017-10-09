---
title: "Zdarzenie aaaReal czasu przetwarzania za pomocą usługi Stream Analytics przetwarzania zdarzeń | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>Architektura odwołania: zdarzeń w czasie rzeczywistym przetwarzania za pomocą usługi Microsoft Azure Stream Analytics
Architektura referencyjna Hello zdarzenia w czasie rzeczywistym przetwarzania za pomocą usługi Azure Stream Analytics jest zamierzone tooprovide ogólnego planu wdrażania platformy w czasie rzeczywistym jako rozwiązanie przetwarzania strumienia usługa (PaaS) w systemie Microsoft Azure.

## <a name="summary"></a>Podsumowanie
Tradycyjnie rozwiązań analitycznych, została oparta na możliwości, takie jak ETL (extract, transform, load) i magazynowanie danych, których dane są przechowywane tooanalysis wcześniejszych. Zmieniających się wymagań, w tym danych szybko nadchodzących push limit toohello istniejącego modelu. Hello możliwości tooanalyze danych w ramach przenoszenie toostorage wcześniejsze strumieni jest jedno rozwiązanie, a mimo że nie jest dostępna nowa funkcja, podejście hello nie powszechnie przyjęto we wszystkich przypadkach branżowych. 

Microsoft Azure udostępnia szeroką gamę katalog analytics technologii, które mogą obsłużyć tablicy scenariuszy różnych rozwiązań i wymagań. Wybieranie, które toodeploy usług platformy Azure dla rozwiązania na trasie, może być wyzwaniem podana szerokość hello ofert. Ten dokument jest zaprojektowana toodescribe hello możliwości i współdziałanie z hello różnych usług Azure, które obsługują rozwiązania strumienia zdarzeń. Objaśniono także niektóre scenariusze hello, w których klienci mogą korzystać z takiego podejścia.

## <a name="contents"></a>Zawartość
* Podsumowanie dla kierownictwa
* Wprowadzenie czasu tooReal analityka
* Wartości oferty w czasie rzeczywistym danych na platformie Azure
* Typowe scenariusze dotyczące analiz w czasie rzeczywistym
* Architektura i składniki
  * Źródła danych
  * Integracja danych warstwy
  * Warstwa analiz w czasie rzeczywistym
  * Warstwa magazynu danych
  * Prezentacja / warstwy zużycie
* Podsumowanie

**Autor:** Centrum Insights danych Charlesa Feddersen, architektów rozwiązania doskonałości, firmy Microsoft Corporation

**Opublikowane:** stycznia 2015

**Poprawka:** 1.0

**Pobieranie:** [zdarzeń w czasie rzeczywistym przetwarzania za pomocą usługi Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

