---
title: "Dowiedz się, jak używać łącznika usługi Azure Service Bus w aplikacji logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Podłącz do usługi Azure Service Bus do wysyłania i odbierania wiadomości. Można wykonać akcje, takie jak wysyłanie do kolejki, Wyślij do tematu odbierania z kolejki i otrzymywać subskrypcji."
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
ms.openlocfilehash: 1e2ce06f5993280dbdb67121849591e67f7979e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-service-bus-connector"></a><span data-ttu-id="11487-105">Rozpoczynanie pracy z łącznika usługi Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="11487-105">Get started with the Azure Service Bus connector</span></span>
<span data-ttu-id="11487-106">Podłącz do usługi Azure Service Bus do wysyłania i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="11487-106">Connect to Azure Service Bus to send and receive messages.</span></span> <span data-ttu-id="11487-107">Można wykonać akcje, takie jak wysyłanie do kolejki, Wyślij do tematu odbierania z kolejki i otrzymywać subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="11487-107">You can perform actions such as send to queue, send to topic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="11487-108">Aby użyć [każdy łącznik](apis-list.md), należy najpierw utworzyć aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="11487-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="11487-109">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="11487-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-service-bus"></a><span data-ttu-id="11487-110">Połączenia magistrali usług</span><span class="sxs-lookup"><span data-stu-id="11487-110">Connect to Service Bus</span></span>
<span data-ttu-id="11487-111">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć połączenie z usługą.</span><span class="sxs-lookup"><span data-stu-id="11487-111">Before your logic app can access any service, you first need to create a connection to the service.</span></span> <span data-ttu-id="11487-112">A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="11487-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps to create a connection to Azure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="11487-113">Użyj wyzwalacz usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="11487-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="11487-114">Wyzwalacz to zdarzenie służy do uruchomienia przepływu pracy zdefiniowanych w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="11487-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="11487-115">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="11487-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="11487-116">Za pomocą akcji usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="11487-116">Use a Service Bus action</span></span>
<span data-ttu-id="11487-117">Akcja jest przeprowadzane przez przepływ pracy zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="11487-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="11487-118">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="11487-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps to create a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="11487-119">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="11487-119">Connector-specific details</span></span>

<span data-ttu-id="11487-120">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="11487-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="11487-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="11487-121">Next steps</span></span>
<span data-ttu-id="11487-122">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="11487-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

