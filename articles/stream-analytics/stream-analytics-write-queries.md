---
title: aaaHow toowrite zapytania w Stream Analytics | Dokumentacja firmy Microsoft
description: "Zapisywanie zapytań w Stream Analytics i dane zapytań | Learning segmentu ścieżki."
keywords: "jak toowrite kwerend danych zapytania, napisz zapytanie, Pisanie zapytań"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a>Jak toowrite zapytania w programie usługi analiza strumienia
Pisanie zapytań dla strumienia przetwarzania logiki w usłudze Azure Stream Analytics jest implementowany jako "zapytania stały", zdefiniowanej przed zadanie uruchamia i wykonać na danych, ponieważ osiągnie hello zadania. przekształcenia danych Hello jest wyrażona w język kwerendy przypominającego SQL, które przede wszystkim podzbiór T-SQL wraz z dodawanej rozszerzeń języka, na przykład [okien](https://msdn.microsoft.com/library/azure/dn835019.aspx) używane tooexpress semantyki danych czasowych.

## <a name="writing-queries"></a>Pisanie zapytań:
1. W Twojej zadania usługi analiza strumienia w portalu zarządzania Azure powitania kliknij **zapytania**.
   
    ![Wybierz zapytanie](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    W portalu Azure hello, kliknij przycisk **zapytania**.
   
    ![Wybierz Podgląd kwerendy](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. Nowe zadania mają toohelp szablonu zapytania, ułatwiające rozpoczęcie pracy. Witaj się, że szablon wykonuje "przekazującego" query tego projektów wszystkie pola w zdarzeniach wejściowych w danych wyjściowych hello.  
   
   * Jeśli zdefiniowano co najmniej jeden dane wejściowe i wyjściowe dla zadania, można zastąpić hello symbolu zastępczego "[YourOutputAlias]" i pola "[YourInputAlias]" hello aliasy hello wejściowa i wyjściowa ma użyj najpierw. Ponadto nadal tworzyć i przetestować zapytanie w hello klasycznego portalu Azure bez zdefiniowania wejściami i wyjściami na powitania zadania.
   * W razie potrzeby tooperform przetwarzanie więcej niż proste przekazującego można edytować hello definicji zapytania. tooget wprowadzenie do tworzenia zapytań, Przyjrzyjmy się niektóre typowe zapytania są przechwytywane wzorce [tutaj](stream-analytics-stream-analytics-query-patterns.md).  
   
   ![Dane zapytania okna](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a>dane zapytania toovalidate działa:
Można sprawdzić, czy zapytanie działa zgodnie z oczekiwaniami przez uruchomienie jej w przeglądarce hello, przez co najmniej jeden lokalnego plik JSON zawierający dane testowe. To nie będzie uruchomić zadanie hello lub mają wpływ na wszystkie rozliczeń.

> [!NOTE]
> Obecnie testowanie zapytań w przeglądarce nie jest obsługiwana w hello portalu Azure.  
> 
> 

1. Upewnij się, że nie ma żadnych błędów w zapytaniu hello (w przeciwnym razie hello przycisk Test zostanie wyłączony) i kliknij przycisk Test hello.  
   
   ![Dane zapytania testowego](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. Zostanie wyświetlony monit o toospecify plików dla każdego hello dane wejściowe, do którego odwołuje się zapytanie hello będzie. W tym przykładzie zapytanie szablonu hello pozostało jako — jest, więc okna dialogowego hello jest monitowanie o danych wejściowych o nazwie "yourinputalias".  
   
   ![Badanie danych zapytania](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. Przeglądaj plik testowy tooa. Kilka przykładowych plików są dostępne na [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) i może również pobierać dane przykładowe z własnych danych wejściowych strumienia danych za pośrednictwem hello funkcja przykładowych danych na karcie dane wejściowe hello.  
   
   ![Zapytanie danych wejściowych](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. Po zamknięciu okna dialogowego hello, zapytanie zostanie uruchomiony za pośrednictwem hello danych testowych i zobaczysz hello wyników u dołu hello hello zapytania strony.  
   
   ![Podsumowanie zapytania](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

