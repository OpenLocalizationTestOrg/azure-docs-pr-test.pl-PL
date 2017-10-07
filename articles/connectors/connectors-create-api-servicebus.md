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
# <a name="get-started-with-hello-azure-service-bus-connector"></a><span data-ttu-id="8b9e8-105">Rozpoczynanie pracy z łącznika usługi Azure Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="8b9e8-105">Get started with hello Azure Service Bus connector</span></span>
<span data-ttu-id="8b9e8-106">Połącz tooAzure toosend usługi Service Bus i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="8b9e8-106">Connect tooAzure Service Bus toosend and receive messages.</span></span> <span data-ttu-id="8b9e8-107">Może wykonywać akcje, takie jak tooqueue wysyłania, wysyłania tootopic, odbierania z kolejki i odbierania z subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8b9e8-107">You can perform actions such as send tooqueue, send tootopic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="8b9e8-108">toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="8b9e8-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="8b9e8-109">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8b9e8-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooservice-bus"></a><span data-ttu-id="8b9e8-110">Połącz tooService magistrali</span><span class="sxs-lookup"><span data-stu-id="8b9e8-110">Connect tooService Bus</span></span>
<span data-ttu-id="8b9e8-111">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate usługi toohello połączenia.</span><span class="sxs-lookup"><span data-stu-id="8b9e8-111">Before your logic app can access any service, you first need toocreate a connection toohello service.</span></span> <span data-ttu-id="8b9e8-112">A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="8b9e8-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="8b9e8-113">Użyj wyzwalacz usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="8b9e8-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="8b9e8-114">Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="8b9e8-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="8b9e8-115">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="8b9e8-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="8b9e8-116">Za pomocą akcji usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="8b9e8-116">Use a Service Bus action</span></span>
<span data-ttu-id="8b9e8-117">Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="8b9e8-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="8b9e8-118">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="8b9e8-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="8b9e8-119">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="8b9e8-119">Connector-specific details</span></span>

<span data-ttu-id="8b9e8-120">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="8b9e8-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8b9e8-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8b9e8-121">Next steps</span></span>
<span data-ttu-id="8b9e8-122">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8b9e8-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

