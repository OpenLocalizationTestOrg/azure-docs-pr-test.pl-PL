---
title: "dzienniki diagnostyczne aaaAzure usługi Service Bus | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset zapasowe dzienników diagnostycznych dla usługi Service Bus na platformie Azure."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a>Dzienniki diagnostyczne usługi Service Bus

Dla usługi Azure Service Bus, można wyświetlić dwa typy dzienników:
* **[Dzienniki aktywności](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Dzienniki te zawierają informacje o operacji wykonywanych w zadaniu. Dzienniki Hello są zawsze włączone.
* **[Dzienniki diagnostyczne](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. Można skonfigurować dziennika diagnostycznego bardziej rozbudowane informacje o wszystko, co się stanie w ramach danego zadania. Dzienniki diagnostyczne obejmują działania, od czasu hello, utworzenia zadania hello do momentu usunięcia zadania hello, w tym aktualizacje i działania, które są wykonywane, gdy jest wykonywane zadanie hello.

## <a name="turn-on-diagnostic-logs"></a>Włączanie dzienników diagnostycznych

Dzienniki diagnostyczne są domyślnie wyłączone. tooenable dzienników diagnostycznych, wykonaj następujące kroki hello:

1.  W hello [portalu Azure](https://portal.azure.com)w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **dzienników diagnostycznych**.

    ![Dzienniki toodiagnostic nawigacji bloku](./media/service-bus-diagnostic-logs/image1.png)

2. Kliknij zasób hello ma toomonitor.  

3.  Kliknij przycisk **Włącz diagnostykę**.

    ![Włączanie dzienników diagnostycznych](./media/service-bus-diagnostic-logs/image2.png)

4.  Aby uzyskać **stan**, kliknij przycisk **na**.

    ![Zmień stan dzienników diagnostycznych](./media/service-bus-diagnostic-logs/image3.png)

5.  Zestaw docelowy archiwum hello, który ma; na przykład konto magazynu, Centrum zdarzeń lub Analiza dzienników Azure.

6.  Zapisz hello nowe ustawienia diagnostyki.

Nowe ustawienia zaczęły obowiązywać w ciągu około 10 minut. Po wykonaniu tej dzienników pojawia się w celu archiwizacji hello skonfigurowane, na powitania **dzienników diagnostycznych** bloku.

Aby uzyskać więcej informacji na temat konfigurowania diagnostyki, zobacz hello [omówienie Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-schema"></a>Dzienniki diagnostyczne schematu

Wszystkie dzienniki są przechowywane w formacie JavaScript Object Notation (JSON). Każdy wpis ma pól ciągów, w formacie hello opisane w następujących sekcji hello.

## <a name="operational-logs-schema"></a>Schemat operacyjne dzienniki

Loguje hello **OperationalLogs** kategorii przechwytywania, co się dzieje podczas operacji usługi Service Bus. W szczególności te dzienniki przechwytywania hello operacji typu, w tym tworzenie kolejek, zasoby używane i hello stan hello operacji.

Dziennik operacyjny JSON ciągi zawierać elementy wymienione w poniższej tabeli hello:

Nazwa | Opis
------- | -------
Identyfikator działania | Wewnętrzny identyfikator używany do śledzenia
EventName | Nazwa operacji           
resourceId | Identyfikator zasobu usługi Azure Resource Manager
SubscriptionId | Identyfikator subskrypcji
EventTimeString | Czas operacji
EventProperties | Właściwości operacji
Stan | Stan operacji
Obiekt wywołujący | Obiekt wywołujący operacji (Azure portalu lub zarządzania klienta)
category | OperationalLogs

Poniżej przedstawiono przykładowy dziennik operacyjny ciągu JSON:

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Następne kroki

Odwiedź powitania po toolearn łącza więcej o magistrali usług:

* [Wprowadzenie tooService magistrali](service-bus-messaging-overview.md)
* [Rozpoczynanie pracy z usługą Service Bus](service-bus-dotnet-get-started-with-queues.md)
