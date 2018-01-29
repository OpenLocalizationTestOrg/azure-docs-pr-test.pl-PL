---
title: "Ustawianie alertów dla zapytania w Stream Analytics | Dokumentacja firmy Microsoft"
description: "Opis usługi Stream Analytics alertów"
keywords: "Konfigurowanie alertów"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: samacha
ms.openlocfilehash: cdbd7da36f3eb2795fc4548915ebbf18200ca44d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a>Ustawianie alertów dla zadania usługi analiza strumienia Azure
## <a name="introduction-monitor-page"></a>Wprowadzenie: Strona Monitor
Alerty można skonfigurować do wyzwolenia alertu, gdy metryki osiągnie warunek, który określisz. Na przykład skonfigurować alert dla warunku podobne do poniższych:

`If there are zero input events in the last 5 minutes, send email notification to sa-admin@example.com`

Reguły można skonfigurować na metryki za pośrednictwem portalu lub można skonfigurować [programowo](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) na dane dzienników operacji.

## <a name="set-up-alerts-in-the-azure-portal"></a>Konfigurowanie alertów w portalu Azure
1. W portalu Azure Otwórz zadanie usługi Stream Analytics, aby utworzyć alertu dotyczącego. 

2. W **zadania** bloku, kliknij przycisk **monitorowanie** sekcji.  

3. W **Metryka** bloku, kliknij przycisk **Dodaj alert** polecenia.

      ![Instalacja portalu usługi Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. Wprowadź nazwę i opis.

5. Selektory umożliwia definiowanie warunku, pod którą zostanie wysłany alert.

6. Podaj informacje o gdzie alertu.

      ![Konfigurowanie alertu dla zadania usługi analiza strumienia Azure](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

Aby uzyskać więcej szczegółów na temat konfigurowania alertów w portalu Azure, zobacz [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).  


## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie do usługi Azure Stream Analytics](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-get-started.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

