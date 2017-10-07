---
title: "aaaAdd danych wejściowych zadania usługi analiza strumienia tooyour | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toohook się tooyour źródła danych usługi analiza strumienia zadania strumieniowych jako dane wejściowe z usługi Event Hubs lub odwołanie do danych z magazynu blogu."
keywords: "danych wejściowych, przesyłanie strumieniowe danych"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a>Dodaj zadanie przesyłania strumieniowego danych wejściowych lub odwołanie do danych tooa analiza strumienia
Dowiedz się, jak toohook się tooyour źródła danych usługi analiza strumienia zadania strumieniowych jako dane wejściowe z usługi Event Hubs lub odwołanie do danych z magazynu obiektów Blob.

Zadania usługi analiza strumienia Azure może być tooone połączonych danych wejściowych lub większą, z których każdy zdefiniować źródło połączenia tooan istniejących danych. Ponieważ dane są przesyłane toothat źródła danych, jest używane przez zadanie usługi Stream Analytics hello i przetwarzane w czasie rzeczywistym jako strumienia danych. Analiza strumienia ma pierwszej klasie integracji z [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) i [magazynu obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) w obrębie i poza hello zadanie subskrypcji.

W tym artykule jest etapem hello [ścieżka szkoleniowa dotycząca usługi analiza strumienia](/documentation/learning-paths/stream-analytics/).

## <a name="data-input-streaming-data-and-reference-data"></a>Dane wejściowe: przesyłanie strumieniowe danych i danych referencyjnych
Istnieją dwa różne typy dane wejściowe, Stream Analytics: strumienie danych i danych referencyjnych.

* **Strumienie danych**: zadania usługi analiza strumienia musi zawierać co najmniej jeden danych strumienia wejściowego toobe używane i przekształcenia przez zadanie hello. Azure Blob storage i Azure Event Hubs są obsługiwane jako źródeł dla wejścia strumienia danych. Usługa Azure Event Hubs są używane toocollect strumieni zdarzeń z połączonych urządzeń, usług i aplikacji. Magazyn obiektów Blob Azure może służyć jako źródło danych wejściowych do wprowadzania danych zbiorczego jako strumień.  
* **Danych referencyjnych**: analiza strumienia obsługuje drugi typ pomocniczy odwołanie do danych wejściowych o nazwie danych.  Jako min. toodata w ruchu te dane są statyczne lub spowalniając zmiana.  Zazwyczaj jest używany do wykonywania wyszukania i korelacji z toocreate strumieni danych bogatszy zestaw danych.  Magazyn obiektów Blob Azure jest obecnie obsługiwane tylko hello źródło danych wejściowych danych referencyjnych.  

zadania usługi analiza strumienia wejściowego tooyour tooadd:

1. W portalu Azure powitania kliknij **dane wejściowe** , a następnie kliknij przycisk **dodać dane wejściowe** w zadania usługi analiza strumienia.
   
    ![Klasyczny portal Azure — Dodawanie danych wejściowych.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    W hello portalu Azure kliknij hello **dane wejściowe** kafelka w zadania usługi analiza strumienia.  
   
    ![Portal Azure — Dodawanie danych wejściowych.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. Określ typ hello hello danych wejściowych: albo **strumienia danych** lub **danych referencyjnych**.
   
    ![Dodaj hello prawidłowe dane wejściowe, strumieniowo lub odwołania](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Dodaj hello prawidłowe dane wejściowe, strumieniowo lub odwołania](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. W przypadku tworzenia elementu wejściowego strumienia danych, określ typ źródła hello reakcję hello.  Ten krok można pominąć podczas tworzenia danych referencyjnych jako tylko obiektu Blob magazynu jest obsługiwana w tej chwili.
   
    ![Dodawanie danych strumienia danych wejściowych](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Dodawanie danych strumienia danych wejściowych](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. Podaj przyjazną nazwę dla tego hello wejściowych w polu Alias wejściowy.  Ta nazwa będzie używana w zapytaniu programu zadanie później na wejściu toohello toorefer.
   
    Wypełnij hello reszty źródła danych tooyour tooconnect hello połączenia wymagane właściwości. Te pola zależą od typu danych wejściowych i źródła i szczegółowo zdefiniowane [tutaj](stream-analytics-create-a-job.md).  
   
    ![Dodawanie zdarzeń centrum danych wejściowych](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. Określ ustawienia serializacji hello hello danych wejściowych:
   
   * toomake się, że zapytania mogły działać hello zgodnie z oczekiwaniami, określ hello **Format serializacji zdarzeń** przychodzących danych.  Serializacja obsługiwane formaty to JSON, CSV i Avro.
   * Sprawdź hello **kodowanie** hello danych.  Witaj obsługiwany tylko format kodowania w tej chwili jest UTF-8.
     
     ![Ustawienia danych serializacji dla hello danych wejściowych](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Ustawienia danych serializacji dla hello danych wejściowych](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. Po zakończeniu tworzenia wejściowych hello, Stream Analytics sprawdzi, czy można połączyć toohello źródło danych wejściowych.  Można wyświetlić stan hello hello operację połączenia testowego w hello Centrum powiadomień.
   
    ![Testuj połączenie hello strumienia danych wejściowych](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Testuj połączenie hello strumienia danych wejściowych](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a>Uzyskaj pomoc dotyczącą strumienia danych wejściowych danych
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

