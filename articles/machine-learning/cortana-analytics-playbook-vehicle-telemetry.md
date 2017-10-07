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
# <a name="vehicle-telemetry-analytics-solution-playbook"></a>Podręcznik dotyczący rozwiązań analizy telemetrii pojazdów
To **menu** toohello rozdziałów tego podręcznika dotyczącego łączy. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a>Omówienie
Komputery Super został przeniesiony poza hello laboratorium i są teraz stoi w naszym garaż! Tych samochodów najnowocześniejsze zawierać większą liczbą czujników, zapewniając im hello możliwości tootrack i monitorować miliony zdarzeń w ciągu sekundy. Oczekuje się, że 2020, większość tych samochodów będzie zostały toohello połączenia internetowego. Wyobraź sobie naciśnięcie przycisku do tego wiele danych tooprovide większe bezpieczeństwo, niezawodność i pobudzenie lepsze środowisko! Firma Microsoft wprowadziła to marzy rzeczywistością z Cortana Intelligence.

Firmy Microsoft Cortana Intelligence jest w pełni zarządzana danych big data oraz zaawansowane analytics suite, umożliwiający tootransform danych do inteligentnego akcji. Chcemy toointroduce toohello szablon rozwiązania Analytics Telemetrii Cortana Intelligence pojazdów. To rozwiązanie pokazano, jak przedstawicielstw samochodu handlowych, producentów samochodów i ubezpieczeń można użyć możliwości hello toogain Cortana analizy w czasie rzeczywistym i zwyczaje predykcyjnej rozeznanie vehicle kondycji i wspierającym. 

rozwiązanie Hello jest zaimplementowany jako [wzorzec architektury lambda](https://en.wikipedia.org/wiki/Lambda_architecture) przedstawiający hello potencjał platformy Cortana Intelligence hello w czasie rzeczywistym i przetwarzania wsadowego. rozwiązanie Hello: 

* udostępnia symulatora telematyki Vehicle
* korzysta z usługi Event Hubs służy do wprowadzania miliony zdarzeń telemetrii symulowane vehicle na platformie Azure 
* używa wgląd w czasie rzeczywistym usługi Stream Analytics toogain na vehicle kondycji
* utrzymuje hello danych do długoterminowego przechowywania dla bardziej zaawansowane funkcje analizy partii. 
* korzysta z uczenia maszynowego wykrywania anomalii w czasie rzeczywistym i insights predykcyjnej toogain przetwarzania wsadowego.
* wykorzystanie danych tootransform HDInsight w skali i fabryki danych orchestration toohandle, planowanie, zarządzanie zasobami i monitorowanie potoku przetwarzania wsadowego hello 
* daje to rozwiązanie sformatowanego pulpitu nawigacyjnego w czasie rzeczywistym danych i wizualizacji analizy predykcyjnej przy użyciu usługi Power BI

## <a name="architecture"></a>Architektura
![Diagram architektury rozwiązania](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*rysunek 1 — Architektura rozwiązania analizy Telemetrii Vehicle*

To rozwiązanie obejmuje następujące hello **Cortana Intelligence składniki** i ich integracji tooend zakończenia ilustrację:

* **Centra zdarzeń** służy do wprowadzania miliony zdarzeń telemetrii vehicle na platformie Azure.
* **Analiza strumienia** do uzyskania wgląd w czasie rzeczywistym w kondycję vehicle i będzie się powtarzał tych danych do długoterminowego przechowywania dla bardziej zaawansowane funkcje analizy partii.
* **Machine Learning** wykrywania anomalii w czasie rzeczywistym i insights predykcyjnej toogain przetwarzania wsadowego.
* **HDInsight** jest wykorzystywana tootransform danych na dużą skalę
* **Fabryka danych** obsługuje aranżacji, potoku przetwarzania wsadowego hello monitorowania i planowania zarządzania zasobami.
* **Power BI** daje to rozwiązanie sformatowanego pulpitu nawigacyjnego w czasie rzeczywistym danych i wizualizacji analizy predykcyjnej.

To rozwiązanie uzyskuje dostęp do dwóch różnych **źródeł danych**: 

* **Symulowane sygnały vehicle i informacji diagnostycznych**: symulatora telematyki vehicle emituje sygnałów, które odpowiadają toohello stan hello vehicle i hello zwiększają wzorca w danym punkcie w czasie i informacji diagnostycznych. 
* **Vehicle katalogu**: odwołanie do zestawu danych zawierające mapowanie toomodel VIN.

