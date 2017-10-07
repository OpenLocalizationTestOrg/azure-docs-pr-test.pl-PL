---
title: "aaaEnable diagnostyczne dla partii zdarzeń - Azure | Dokumentacja firmy Microsoft"
description: "Rejestruj i analizowanie dzienników diagnostycznych zdarzeń dla zasobów konta partii zadań Azure, takich jak pule i zadania."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a>Rejestrowanie zdarzeń diagnostycznych oceny i monitorowania rozwiązań partii

Podobnie jak w przypadku wielu usług Azure, hello usługa partia zadań emituje dla niektórych zasobów podczas hello okres istnienia zasobu hello zdarzenia dziennika. Można Włącz partii zadań Azure dzienników diagnostycznych toorecord zdarzenia dla zasobów, takich jak pule i zadań, a następnie użyj hello dzienników diagnostycznych oceny i monitorowania. Tworzenie zdarzeń, takich jak puli, Usuń puli, uruchamiania zadań zadanie ukończone i inne są wyświetlane w partii dzienników diagnostycznych.

> [!NOTE]
> W tym artykule omówiono rejestrowania zdarzeń dla samych zasobach konta usługi partia zadań, nie zadania i dane wyjściowe zadań. Aby uzyskać więcej informacji na temat przechowywania danych wyjściowych hello zadań i zadań, zobacz [danych wyjściowych i zadań utrwalić partii zadań Azure](batch-task-output.md).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
* [Konto usługi partia zadań Azure](batch-account-create-portal.md)
* [konto usługi Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  dzienniki diagnostyczne partii toopersist, należy utworzyć konta usługi Azure Storage, w którym Azure będą przechowywane dzienniki hello. To konto magazynu można określić podczas możesz [włączyć rejestrowanie diagnostyczne](#enable-diagnostic-logging) dla Twojego konta usługi partia zadań. Witaj konta magazynu, możesz określić, że po włączeniu zbierania dzienników jest hello sam nie jako hello tooin określonego konta magazynu połączone [pakietów aplikacji](batch-application-packages.md) i [trwałości danych wyjściowych zadania](batch-task-output.md) artykułów.
  
  > [!WARNING]
  > Jesteś **obciążona** hello dane przechowywane na koncie magazynu Azure. W tym hello dzienników diagnostycznych omówione w tym artykule. Należy o tym pamiętać podczas projektowania sieci [logowania zasady przechowywania](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).
  > 
  > 

## <a name="enable-diagnostic-logging"></a>Włączanie rejestrowania diagnostycznego
Rejestrowanie diagnostyczne nie jest włączone domyślnie dla Twojego konta usługi partia zadań. Musisz jawnie włączyć rejestrowanie diagnostyczne dla każdego konta usługi partia zadań, które chcesz toomonitor:

[Jak tooenable zbierania dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

Zalecamy przeczytanie hello pełne [Omówienie programu Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain artykułu zrozumienia nie tylko sposób rejestrowania tooenable, ale hello dziennika kategorii obsługiwane przez hello różne usługi platformy Azure. Na przykład w partii zadań Azure obsługuje obecnie jedną kategorię dziennika: **dzienniki usługi**.

## <a name="service-logs"></a>Dzienniki usługi
Dzienniki usługi usługi partia zadań Azure zawiera zdarzenia emitowane przez usługi partia zadań Azure hello okres istnienia hello zasobu partii puli lub zadania. Każde zdarzenie emitowane przez partię są przechowywane w hello określone konto magazynu w formacie JSON. Na przykład to jest treść hello próbki **puli utworzyć zdarzenia**:

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

Każda jednostka zdarzenia znajduje się w JSON pliku w hello określono konto magazynu Azure. Jeśli chcesz tooaccess hello dzienniki bezpośrednio, warto zapoznać się z tooreview hello [schematu dzienników diagnostycznych na koncie magazynu hello](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).

## <a name="service-log-events"></a>Usługa dziennika zdarzeń
Witaj usługa partia zadań emituje obecnie hello następujące zdarzenia logowania do usługi. Ta lista nie może być pełne, ponieważ dodatkowe zdarzenia mogły zostać dodane od momentu ostatniej aktualizacji w tym artykule.

| **Usługa dziennika zdarzeń** |
| --- |
| [Tworzenie puli][pool_create] |
| [Start usuwania puli][pool_delete_start] |
| [Usuwanie puli ukończone][pool_delete_complete] |
| [Początkowy rozmiar puli][pool_resize_start] |
| [Zmiana rozmiaru puli ukończone][pool_resize_complete] |
| [Rozpoczęcia zadania][task_start] |
| [Zadania ukończone][task_complete] |
| [Niepowodzenie zadania][task_fail] |

## <a name="next-steps"></a>Następne kroki
Dodanie toostoring zdarzeń dziennik diagnostyczny na koncie magazynu Azure, możesz również strumienia partii usługi dziennika zdarzeń tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md)i wysyła je za[Azure Log Analytics](../log-analytics/log-analytics-overview.md).

* [Strumień dzienników diagnostycznych platformy Azure tooEvent koncentratory](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  Strumienia partii zdarzeń diagnostycznych toohello wysoce skalowalna Usługa transferu danych, usługa Event Hubs. Centra zdarzeń może obsługiwać miliony zdarzeń na sekundę, który można przekształcić i magazynu przy użyciu dowolnego dostawcy analiz w czasie rzeczywistym.
* [Analizowanie Azure dzienników diagnostycznych przy użyciu analizy dzienników](../log-analytics/log-analytics-azure-storage.md)
  
  Wyślij tooLog Twojego dzienniki diagnostyczne analizy, w którym można analizować je w portalu Operations Management Suite (OMS) hello, lub wyeksportować je do analizy w programie Excel lub usługi Power BI.

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
