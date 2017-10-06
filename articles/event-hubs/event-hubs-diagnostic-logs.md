---
title: "dzienniki diagnostyczne aaaAzure usługi Event Hubs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset zapasowe dzienników diagnostycznych usługi event hubs na platformie Azure."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a>Dzienniki diagnostyczne centra zdarzeń

Dla usługi Azure Event Hubs można wyświetlić dwa typy dzienników:
* **[Dzienniki aktywności](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Te dzienniki ma informacje o operacji wykonywanych w zadaniu. Dzienniki Hello są zawsze włączone.
* **[Dzienniki diagnostyczne](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. Dzienniki diagnostyczne bardziej zaawansowane funkcje dostępne w widoku wszystkich podejmowanych można skonfigurować za pomocą zadania. Dzienniki diagnostyczne obejmują działania, od czasu hello, utworzenia zadania hello do momentu usunięcia zadania hello, w tym aktualizacje i działania, które są wykonywane, gdy jest wykonywane zadanie hello.

## <a name="turn-on-diagnostic-logs"></a>Włączanie dzienników diagnostycznych
Dzienniki diagnostyczne są domyślnie wyłączone. dzienniki diagnostyczne tooenable:

1.  W hello [portalu Azure](https://portal.azure.com)w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **dzienników diagnostycznych**.

    ![Dzienniki toodiagnostic nawigacji bloku](./media/event-hubs-diagnostic-logs/image1.png)

2.  Kliknij zasób hello ma toomonitor.

3.  Kliknij przycisk **Włącz diagnostykę**.

    ![Włączanie dzienników diagnostycznych](./media/event-hubs-diagnostic-logs/image2.png)

4.  Aby uzyskać **stan**, kliknij przycisk **na**.

    ![Zmiana stanu hello dzienników diagnostycznych](./media/event-hubs-diagnostic-logs/image3.png)

5.  Zestaw docelowy archiwum hello, który ma; na przykład konto magazynu, Centrum zdarzeń lub Analiza dzienników Azure.

6.  Zapisz hello nowe ustawienia diagnostyki.

Nowe ustawienia zaczęły obowiązywać w ciągu około 10 minut. Po wykonaniu tej dzienników pojawia się w celu archiwizacji hello skonfigurowane, na powitania **dzienników diagnostycznych** bloku.

Aby uzyskać więcej informacji na temat konfigurowania diagnostyki, zobacz hello [omówienie Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-categories"></a>Dzienniki diagnostyczne kategorii
Centra zdarzeń przechwytuje dzienniki diagnostyczne dla dwóch kategorii:

* **ArchiveLogs**: dzienniki powiązane tooEvent archiwów koncentratory, w szczególności rejestruje błędy tooarchive pokrewne.
* **OperationalLogs**: informacje o tym, co dzieje podczas operacji usługi Event Hubs, w szczególności hello typ operacji, w tym tworzenia Centrum zdarzeń, zasoby używane i hello stan hello operacji.

## <a name="diagnostic-logs-schema"></a>Dzienniki diagnostyczne schematu
Wszystkie dzienniki są przechowywane w formacie JavaScript Object Notation (JSON). Każdy wpis ma pól ciągów, w formacie hello opisanego w hello następujące sekcje.

### <a name="archive-logs-schema"></a>Schemat dzienniki archiwum

Ciągi JSON dziennika archiwum obejmują elementy wymienione w poniższej tabeli hello:

Nazwa | Opis
------- | -------
TaskName | Opis hello zadań, które zakończyły się niepowodzeniem.
Identyfikator działania | Wewnętrzny identyfikator używany do śledzenia.
trackingId | Wewnętrzny identyfikator używany do śledzenia.
resourceId | Identyfikator usługi Azure Resource Manager zasobu.
EventHub | Centrum zdarzeń Pełna nazwa (w tym nazwę przestrzeni nazw).
partitionId | Zapisywana partycji Centrum zdarzeń.
archiveStep | ArchiveFlushWriter
startTime | Godzina rozpoczęcia awarii.
błędy | Liczba wystąpił błąd.
durationInSeconds | Czas trwania awarii.
Komunikat | Komunikat o błędzie.
category | ArchiveLogs

Witaj następujący kod jest przykładem dziennika archiwum ciągu JSON:

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a>Schemat operacyjne dzienniki

Dziennik operacyjny JSON ciągi zawierać elementy wymienione w poniższej tabeli hello:

Nazwa | Opis
------- | -------
Identyfikator działania | Wewnętrzny identyfikator używany tootrack cel.
EventName | Nazwa operacji.  
resourceId | Identyfikator usługi Azure Resource Manager zasobu.
SubscriptionId | Identyfikator subskrypcji.
EventTimeString | Czas operacji.
EventProperties | Właściwości operacji.
Stan | Stan operacji.
Obiekt wywołujący | Obiekt wywołujący operacji (Azure portalu lub zarządzania klienta).
category | OperationalLogs

Witaj następujący kod jest przykładem ciągu JSON dziennik operacji:

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooEvent koncentratory](event-hubs-what-is-event-hubs.md)
* [Omówienie interfejsu API usługi Event Hubs](event-hubs-api-overview.md)
* [Rozpoczynanie pracy z usługą Event Hubs](event-hubs-csharp-ephcs-getstarted.md)
