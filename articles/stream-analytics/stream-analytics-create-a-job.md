---
title: "toocreate aaaHow zadania przetwarzania analizy danych dla usługi Stream Analytics | Dokumentacja firmy Microsoft"
description: "Utwórz zadanie przetwarzania analizy danych dla usługi Stream Analytics | Learning segmentu ścieżki."
keywords: przetwarzanie analizy danych
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a>Jak toocreate przetwarzania analizy danych zadanie usługi analiza strumienia
Witaj zasób najwyższego poziomu w Azure Stream Analytics jest zadania usługi analiza strumienia.  Składa się z jednego lub więcej wejściowych źródeł danych, zapytania, przedstawiając hello transformacji danych i co najmniej jeden wyjściowy obiektów docelowych, które wyniki są zapisywane do. Włącz te razem hello użytkownika tooperform danych analizy w przetwarzania dla dane przesyłane strumieniowo scenariuszy.

toostart za pomocą usługi Stream Analytics, Rozpocznij od utworzenia nowego zadania usługi analiza strumienia.  Należy zauważyć, że ta akcja nie daje żadnych skutków rozliczeń do momentu rozpoczęcia zadania hello.

1. Zaloguj się na hello online [klasycznego portalu Azure](http://manage.windowsazure.com) lub hello [portalu Azure](https://portal.azure.com/).
2. W portalu hello: **kliknij nowy**, następnie kliknij przycisk **usług danych** lub **analizy danych** w zależności od portalu, a następnie kliknij przycisk **Azure Stream Analytics** lub **strumienia Analytics** , a następnie **szybkie tworzenie**.
   
   ![Kreator zadania przetwarzania analizy danych](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Utwórz zadanie przetwarzania analizy danych](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. Określ żądaną konfiguracją hello zadania usługi analiza strumienia hello.
   
   * W hello **Nazwa zadania** wprowadź nazwę zadania usługi analiza strumienia hello tooidentify. Gdy hello **Nazwa zadania** jest weryfikowane, w polu Nazwa zadania hello jest wyświetlany zielony znacznik wyboru. Witaj **Nazwa zadania** może zawierać tylko znaki alfanumeryczne i hello '-' znaków i musi zawierać od 3 do 63 znaków.
   * Użyj **Region** w portalu Azure hello lub **lokalizacji** w hello Azure portalu toospecify hello lokalizacji geograficznej, w którym ma toorun hello zadania.
   * Jeśli przy użyciu hello portalu Azure, wybierz lub Utwórz toouse konta magazynu, jako hello **konto magazynu monitorowania regionalnego**. To konto magazynu jest używana toostore danych monitorowania dla wszystkich zadań usługi Stream Analytics uruchomione w tym regionie.
   * Przy użyciu hello portalu Azure, określić nową lub istniejącą **grupy zasobów** toohold powiązanych zasobów dla aplikacji.
4. Po skonfigurowaniu hello nowe opcje zadania Stream Analytics kliknij **utworzyć zadania usługi analiza strumienia**. Może upłynąć kilka minut, aż toobe zadania usługi analiza strumienia hello utworzony. Stan hello toocheck, możesz monitorować postęp hello hello Centrum powiadomień.
   
   ![Centrum powiadomień zadania przetwarzania analizy danych](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure w portalu analityka danych przetwarzania zadania tworzenia zadania](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. nowe zadanie Hello będzie wyświetlany stan **utworzony**. Zwróć uwagę, że hello **Start** przycisk jest niedostępny. Przed rozpoczęciem powitalne zadania, należy skonfigurować dane wejściowe zadania hello, zapytań i danych wyjściowych.
   
   ![Zadanie przetwarzania analizy danych stanu](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure w portalu analityka danych przetwarzania stanu zadania](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

