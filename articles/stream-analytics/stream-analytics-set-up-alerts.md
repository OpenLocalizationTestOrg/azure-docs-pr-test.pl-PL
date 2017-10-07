---
title: "aaaSet alerty dla zapytań w Stream Analytics | Dokumentacja firmy Microsoft"
description: "Opis usługi Stream Analytics alertów"
keywords: "Konfigurowanie alertów"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a>Ustawianie alertów dla zadania usługi analiza strumienia Azure
## <a name="introduction-monitor-page"></a>Wprowadzenie: Strona Monitor
Można skonfigurować alerty tootrigger alert po metrykę warunek, który określisz. Na przykład skonfigurować alert dla warunku, takie jak następujące hello:

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

Reguły można skonfigurować na metryki za pośrednictwem portalu hello, lub można skonfigurować [programowo](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) na dane dzienników operacji.

## <a name="set-up-alerts-in-hello-azure-portal"></a>Konfigurowanie alertów w hello portalu Azure
1. Otwórz zadanie usługi Stream Analytics hello, który ma toocreate alert dla hello portalu Azure. 

2. W hello **zadania** bloku, kliknij przycisk hello **monitorowanie** sekcji.  

3. W hello **Metryka** bloku, kliknij przycisk hello **Dodaj alert** polecenia.

      ![Instalacja portalu usługi Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. Wprowadź nazwę i opis.

5. Użyj hello selektorów toodefine hello warunku w obszarze hello, które będą wysyłane alerty.

6. Podaj informacje o gdzie hello alertu.

      ![Konfigurowanie alertu dla zadania usługi analiza strumienia Azure](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

Aby uzyskać więcej szczegółów na temat konfigurowania alertów w hello portalu Azure, zobacz [otrzymywać powiadomienia o alertach](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).  


## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-get-started.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

