---
title: "aaaHow tooconfigure dane wyjściowe do zadania usługi analiza strumienia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie danych wyjściowych do zadania usługi analiza strumienia | Learning segmentu ścieżki."
keywords: "dane wyjściowe, przenoszenie danych"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a>Jak tooconfigure dane wyjściowe do zadania usługi analiza strumienia

Zadania usługi analiza strumienia Azure mogą być połączone tooone lub więcej danych dane wyjściowe, które definiują połączenia tooan istniejące dane w zbiorniku. Zadanie Stream Analytics przetwarza i przekształca przychodzących danych, strumień danych zdarzeń dane wyjściowe są zapisywane dane wyjściowe zadania tooyour.

Strumień analizy danych wyjściowych może być toosource używane w czasie rzeczywistym pulpitów nawigacyjnych i alertów, przepływy pracy przepływu danych wyzwalacza ani po prostu archiwum danych podczas przetwarzania wsadowego później. Analiza strumienia ma pierwszej klasie integracji z kilku usług platformy Azure, które opisano szczegółowo w tym miejscu.

Zadanie usługi analiza strumienia wyjściowego tooyour tooadd:

1. W hello [portalu Azure](https://portal.azure.com)Otwórz swoją pracę i kliknij **dane wyjściowe** , a następnie kliknij przycisk **Dodaj** w wyświetlonym bloku danych wyjściowych hello.
   
    ![Dodawanie danych wyjściowych](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. Podaj przyjazną nazwę dla tego raportu w hello **Alias wyjściowy** pole. Ta nazwa może być używany w zapytaniu zadania kopii później na wyjściu toohello toorefer.  
   
    Wypełnij hello reszty hello wymagane połączenia właściwości tooconnect tooyour wyjściowego.  Te pola zależą od typu danych wyjściowych i są zdefiniowane tutaj.  
   
    ![Wybierz typ przepływu danych](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. W zależności od typu danych wyjściowych hello może być konieczne toospecify sposób serializacji lub sformatowany hello danych. w tym miejscu opisano Hello serializacji określonego ustawienia dla każdego typu danych wyjściowych.
   
    Wypełnij hello reszty źródła danych tooyour tooconnect hello połączenia wymagane właściwości. Te pola zależą od typu danych wejściowych i źródła i są zdefiniowane w części hello [artykułu Utwórz zadanie](stream-analytics-create-a-job.md).  

> [!Note]
>
> Wszystkie zadania toohello dodany element danych wyjściowych musi istnieć przed uruchomiono zadanie hello i uruchomić zdarzeń przepływu. Na przykład jeśli używasz magazynu obiektów Blob jako dane wyjściowe zadania hello nie utworzy konta magazynu automatycznie. Musi on toobe utworzone przez użytkownika hello, przed rozpoczęciem powitalne ASA zadania.
> 
 

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

