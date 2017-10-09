---
title: "aaaLearn toouse hello łącznika usług Salesforce w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Witaj łącznika usług Salesforce umożliwia toowork interfejsu API z obiektami usługi Salesforce."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b14b41fa8a4648b4f0090472dc0f9575bf13a2ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-salesforce-connector"></a><span data-ttu-id="5b68e-104">Rozpoczynanie pracy z hello łącznika usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="5b68e-104">Get started with hello Salesforce connector</span></span>
<span data-ttu-id="5b68e-105">Witaj łącznika usług Salesforce umożliwia toowork interfejsu API z obiektami usługi Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5b68e-105">hello Salesforce Connector provides an API toowork with Salesforce objects.</span></span>

<span data-ttu-id="5b68e-106">toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="5b68e-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="5b68e-107">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5b68e-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosalesforce-connector"></a><span data-ttu-id="5b68e-108">Połącz tooSalesforce łącznika</span><span class="sxs-lookup"><span data-stu-id="5b68e-108">Connect tooSalesforce connector</span></span>
<span data-ttu-id="5b68e-109">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate *połączenia* toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="5b68e-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="5b68e-110">A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="5b68e-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosalesforce-connector"></a><span data-ttu-id="5b68e-111">Tworzenie łącznika tooSalesforce połączenia</span><span class="sxs-lookup"><span data-stu-id="5b68e-111">Create a connection tooSalesforce connector</span></span>
> [!INCLUDE [Steps toocreate a connection tooSalesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="5b68e-112">Użyj wyzwalacz łącznika usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="5b68e-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="5b68e-113">Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="5b68e-113">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="5b68e-114">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="5b68e-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="5b68e-115">Dodaj warunek</span><span class="sxs-lookup"><span data-stu-id="5b68e-115">Add a condition</span></span>
> [!INCLUDE [Steps toocreate a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="5b68e-116">Za pomocą akcji łącznika usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="5b68e-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="5b68e-117">Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="5b68e-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="5b68e-118">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="5b68e-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="5b68e-119">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="5b68e-119">Connector-specific details</span></span>

<span data-ttu-id="5b68e-120">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="5b68e-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5b68e-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5b68e-121">Next steps</span></span>
[<span data-ttu-id="5b68e-122">Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="5b68e-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

