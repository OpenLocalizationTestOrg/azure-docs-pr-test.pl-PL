---
title: "aaaLearn toouse hello Azure Service Bus łącznika w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Połącz tooAzure toosend usługi Service Bus i odbierania wiadomości. Może wykonywać akcje, takie jak tooqueue wysyłania, wysyłania tootopic, odbierania z kolejki i odbierania z subskrypcji."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a>Rozpoczynanie pracy z łącznika usługi Azure Service Bus hello
Połącz tooAzure toosend usługi Service Bus i odbierania wiadomości. Może wykonywać akcje, takie jak tooqueue wysyłania, wysyłania tootopic, odbierania z kolejki i odbierania z subskrypcji.

toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki. Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooservice-bus"></a>Połącz tooService magistrali
Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate usługi toohello połączenia. A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a>Użyj wyzwalacz usługi Service Bus
Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy. [Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a>Za pomocą akcji usługi Service Bus
Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji. [Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/servicebus/). 

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

