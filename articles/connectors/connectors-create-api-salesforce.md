---
title: "Dowiedz się, jak używać łącznika usług Salesforce w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Łącznik usług Salesforce zapewnia interfejs API do pracy z obiektami Salesforce."
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
ms.openlocfilehash: c2e2efd356382df9404f5c4ed54f24758b2cd22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-salesforce-connector"></a><span data-ttu-id="87ba4-104">Rozpoczynanie pracy z łącznika usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="87ba4-104">Get started with the Salesforce connector</span></span>
<span data-ttu-id="87ba4-105">Łącznik usług Salesforce zapewnia interfejs API do pracy z obiektami Salesforce.</span><span class="sxs-lookup"><span data-stu-id="87ba4-105">The Salesforce Connector provides an API to work with Salesforce objects.</span></span>

<span data-ttu-id="87ba4-106">Aby użyć [każdy łącznik](apis-list.md), należy najpierw utworzyć aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="87ba4-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="87ba4-107">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="87ba4-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-salesforce-connector"></a><span data-ttu-id="87ba4-108">Nawiązać łącznika usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="87ba4-108">Connect to Salesforce connector</span></span>
<span data-ttu-id="87ba4-109">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* do usługi.</span><span class="sxs-lookup"><span data-stu-id="87ba4-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="87ba4-110">A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="87ba4-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-salesforce-connector"></a><span data-ttu-id="87ba4-111">Utwórz połączenie łącznika usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="87ba4-111">Create a connection to Salesforce connector</span></span>
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="87ba4-112">Użyj wyzwalacz łącznika usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="87ba4-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="87ba4-113">Wyzwalacz to zdarzenie służy do uruchomienia przepływu pracy zdefiniowanych w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="87ba4-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="87ba4-114">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="87ba4-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="87ba4-115">Dodaj warunek</span><span class="sxs-lookup"><span data-stu-id="87ba4-115">Add a condition</span></span>
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="87ba4-116">Za pomocą akcji łącznika usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="87ba4-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="87ba4-117">Akcja jest przeprowadzane przez przepływ pracy zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="87ba4-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="87ba4-118">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="87ba4-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="87ba4-119">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="87ba4-119">Connector-specific details</span></span>

<span data-ttu-id="87ba4-120">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="87ba4-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="87ba4-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="87ba4-121">Next steps</span></span>
[<span data-ttu-id="87ba4-122">Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="87ba4-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

