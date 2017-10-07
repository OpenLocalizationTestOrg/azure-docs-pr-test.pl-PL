---
title: "toostart aaaHow przesyłania strumieniowego zadania Stream Analytics | Dokumentacja firmy Microsoft"
description: "Jak uruchomić zadanie przesyłania strumieniowego w Azure Stream Analytics | Learning segmentu ścieżki."
keywords: "zadania przesyłania strumieniowego"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a>Jak zadanie usługi analiza strumienia Azure toorun przesyłania strumieniowego
Podczas wprowadzania zadania, zapytań i danych wyjściowych wszystkie określono, że można uruchomić zadania Stream Analytics hello.

toostart zadania:

1. W hello klasycznego portalu Azure, z poziomu pulpitu nawigacyjnego hello zadania kliknij **Start** u dołu hello hello strony.
   
   ![Uruchom zadanie przycisku](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   W portalu Azure hello, kliknij przycisk **Start** u góry hello strony zadania.
   
   ![Azure portalu rozpoczęcia zadania przycisku](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. Określ **Start wyjściowy** toodetermine wartość, gdy to zadanie zostanie uruchomione, generuje danych wyjściowych. Witaj domyślne ustawienie dla zadania, które wcześniej nie została uruchomiona jest **czas rozpoczęcia zadania**, co oznacza, że to zadanie hello natychmiast rozpocząć przetwarzania danych. Można również określić **niestandardowy** czasu w hello przeszłości (służący do konsumowania danych historycznych) lub hello przyszłych (toodelay przetwarzania do przyszłych czasu). Dla opcji hello przypadków, gdy zadanie została wcześniej uruchomiona i zatrzymana, **czas ostatniego zatrzymania** jest dostępny w kolejności tooresume hello zadania z hello ostatniego danych wyjściowych i uniknąć utraty danych.  
   
   ![Przesyłanie strumieniowe zadania czas rozpoczęcia](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure portalu Start zadanie przesyłania strumieniowego czasu](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. Potwierdź wybór. zbyt zmieni stan zadania Hello*uruchamianie* i wkrótce zostanie przeniesiona za*systemem* po rozpoczęciu zadania hello. Możesz monitorować postęp hello hello **Start** operacji w hello **Centrum powiadomień**:
   
   ![postęp zadania przesyłania strumieniowego](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Portal Azure przesyłania strumieniowego postęp zadania](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

