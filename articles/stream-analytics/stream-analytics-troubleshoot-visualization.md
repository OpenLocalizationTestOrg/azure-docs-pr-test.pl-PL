---
title: "aaaVisualize i rozwiązywać problemy dotyczące zadania usługi analiza strumienia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toovisualize zadanie usługi Stream Analytics potoku dla Rozwiązywanie problemów przy użyciu funkcji diagram diagnostyki hello samoobsługi."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a>Tworzenie wizualizacji i rozwiązywanie problemów z zadania usługi analiza strumienia
W Stream Analytics tak jak w przypadku innych technologii chmurowych rozwiązywania problemów jest czasami toolook potrzebne do dlaczego zadania nie tworzy hello oczekiwane dane wyjściowe (lub żadnych danych wyjściowych istotnego dla badania). Pamiętając o tym Stream Analytics zapewnia możliwość hello do wizualizacji zadanie przesyłania strumieniowego. To jest również przydatne jako narzędzia do modelowania i ma powitania po stronie korzyści dla ludzi wymagających dokumentacji ich pracy.

W wizualizacji hello są widoczne oraz zapytania hello panelu hello wejść, a następnie wszystkie dane wyjściowe hello konfigurować. Problemy z łącznością lub konfiguracją może okazać się bardziej, a można też przydatne toosee wizualną reprezentację danej konfiguracji.

## <a name="using-hello-diagnosis-diagram-tool"></a>Za pomocą narzędzia diagram diagnostyki hello
tooaccess tego wizualizatora, po prostu kliknij hello przycisk "Diagnostyki diagram" w hello bloku "Ustawienia" hello hello zadanie usługi Stream Analytics.

![Stream-Analytics-Troubleshoot-visualization-Diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

Co wejściowa i wyjściowa jest zaznaczony kolorami tooindicate hello bieżący stan tego składnika, jak pokazano poniżej.

![Stream-Analytics-Troubleshoot-visualization-Input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

Gdy hello użytkownik chce toolook na pośrednie kroki toounderstand hello danych przepływu wzorców zapytań wewnątrz zadania, narzędziem hello zawiera widok podział hello hello zapytania do jej kroki składnika i hello sekwencja przepływu. Kliknięcie na każdym etapie zapytania spowoduje wyświetlenie hello odpowiedniej sekcji w zapytaniu edycji okienku zgodnie z opisami. 

![Stream-Analytics-Troubleshoot-visualization-Intermediate-Steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

