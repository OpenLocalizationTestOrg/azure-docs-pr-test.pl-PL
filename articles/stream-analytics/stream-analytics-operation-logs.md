---
title: "aaaDebug przy użyciu dzienników operacji i usługi w Stream Analytics | Dokumentacja firmy Microsoft"
description: Jak toouse Stream Analytics dzienniki operacji
keywords: "dzienniki usługi"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a>Debugowanie przy użyciu dzienników usługi i działania zadania usługi analiza strumienia
Wszystkie szczegóły toorecord toousers komunikatów rejestrowania operacyjne dostawy usług Azure powiązanych toomanagement operacji. W systemie Azure Stream Analytics tych informacji może służyć do debugowania, takich jak wyświetlanie stanu zadania, postęp zadania i niepowodzenia wiadomości tootrack hello postępu zadania w czasie, od początku tooprocessing toooutput.

## <a name="find-operation-logs-in-hello-azure-management-portal"></a>Znajdź w portalu zarządzania Azure hello dzienniki operacji
Dzienniki operacji można uzyskiwać na dwa sposoby:  

* Pulpit nawigacyjny hello zadania usługi analiza strumienia  
* Usługi zarządzania w hello klasycznego portalu Azure  

## <a name="dashboard-of-hello-stream-analytics-job"></a>Pulpit nawigacyjny hello zadania usługi analiza strumienia
Toohello łącza, odpowiadającego dzienników zadania Stream Analytics jest wyświetlane na karcie pulpit nawigacyjny hello zadania. Po kliknięciu tego łącza zostanie ustawiony hello filtrów w sposób zawiera najnowsze dzienniki dla określonego zadania.

  ![Wybierz dzienniki usługi zarządzania](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a>Usługi zarządzania
toomanually Przejdź dzienniki operacji toohello Stream Analytics i innych usług w hello klasycznego portalu Azure:

1. Polecenie **usług zarządzania** w hello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Wybierz **Stream Analytics** dla **typu** i nazwę hello zadanie hello **nazwa usługi**.  
   
   ![Wybierz usługi analiza strumienia](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a>Znajdowanie dzienników inspekcji w hello portalu Azure
toofind operacyjne dzienniki dla zadania usługi analiza strumienia w hello portalu Azure, kliknij przycisk **Przeglądaj** , a następnie wybierz **dzienniki inspekcji**.

  ![Wybierz usługę Stream Analytics w portalu Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

Spowoduje to otwarcie bloku, wyświetlanie zdarzeń z hello ostatnich 7 dni dla wszystkich zasobów w ramach subskrypcji.  Można filtrować zdarzenia toosee, określ typ lub przedział czasu, klikając hello **filtru** polecenia.

  ![Wybierz usługę Stream Analytics w portalu Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a>Uzyskiwanie szczegółowych informacji dziennika
Można filtrować według stanu tooview hello dzienniki i zakres czasu dla zadania.

W portalu zarządzania Azure hello, kliknij na powitania **szczegóły** przycisk u dołu hello tooview okna hello więcej szczegółów na temat wybranego zdarzenia. 

  ![Wybierz szczegóły](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

W hello portalu Azure, kliknij polecenie toosee wpisu dziennika hello szczegółowych informacji o zdarzeniach w nim.

  ![Wybierz szczegóły portalu Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

Z tego miejsca, możesz otworzyć hello **szczegółów** bloku, klikając hello zdarzeń.

  ![Wybierz szczegóły portalu Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a>Debugowanie zadanie zakończone niepowodzeniem
W portalu zarządzania Azure hello kliknij ikonę wyszukiwania hello i wpisz "nie powiodło się". Daje w wyniku wszystkie dzienniki z błędami. 

  ![Debugowanie zadanie zakończone niepowodzeniem](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

Hello portalu Azure, można filtrować według poziomu tooview komunikat **krytyczny** zdarzenia.

  ![Debugowania portalu Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

Wybierz jeden z błędami hello i kliknij na powitania **szczegóły** Aby uzyskać więcej informacji na temat błędu hello.  Niektóre komunikaty o błędach zawierają również informacje dotyczące sposobu toomitigate hello problem. 

  ![Szczegóły operacji](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

W razie potrzeby toocontact [Obsługa](https://azure.microsoft.com/support/options/) lub podaj informacje toohello zespołu za pomocą hello [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), należy pamiętać, szczegóły operacji hello, w szczególności hello **identyfikator korelacji**. 

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

