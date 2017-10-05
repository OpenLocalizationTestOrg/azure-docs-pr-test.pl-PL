---
title: "Łącznik usługi GitHub w programie Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. GitHub to repozytorium Git opartych na sieci web usługi hosta. Zapewnia ona wszystkich wersji rozproszonej i kontroli źródła kodu zarządzania (SCM) funkcji Git, a także dodawanie własnych funkcji."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: d4614b0ceff0ec0d36dbb1a136551f985f2fc1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-github-connector"></a><span data-ttu-id="1e2e5-105">Rozpoczynanie pracy z łącznikiem usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="1e2e5-105">Get started with the GitHub connector</span></span>
<span data-ttu-id="1e2e5-106">GitHub to repozytorium Git opartych na sieci web usługi hosta.</span><span class="sxs-lookup"><span data-stu-id="1e2e5-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="1e2e5-107">Zapewnia ona wszystkich wersji rozproszonej i kontroli źródła kodu zarządzania (SCM) funkcji Git, a także dodawanie własnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="1e2e5-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

<span data-ttu-id="1e2e5-108">Rozpoczynanie pracy przez teraz tworzenie aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1e2e5-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-github"></a><span data-ttu-id="1e2e5-109">Utwórz połączenie z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="1e2e5-109">Create a connection to GitHub</span></span>
<span data-ttu-id="1e2e5-110">Do tworzenia aplikacji logiki z usługi GitHub, należy najpierw utworzyć **połączenia** następnie podaj szczegóły następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="1e2e5-110">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="1e2e5-111">Właściwość</span><span class="sxs-lookup"><span data-stu-id="1e2e5-111">Property</span></span> | <span data-ttu-id="1e2e5-112">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1e2e5-112">Required</span></span> | <span data-ttu-id="1e2e5-113">Opis</span><span class="sxs-lookup"><span data-stu-id="1e2e5-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1e2e5-114">Token</span><span class="sxs-lookup"><span data-stu-id="1e2e5-114">Token</span></span> |<span data-ttu-id="1e2e5-115">Tak</span><span class="sxs-lookup"><span data-stu-id="1e2e5-115">Yes</span></span> |<span data-ttu-id="1e2e5-116">Podaj poświadczenia usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="1e2e5-116">Provide GitHub Credentials</span></span> |

<span data-ttu-id="1e2e5-117">Po utworzeniu połączenia, można go wykonać akcje i będzie nasłuchiwać wyzwalaczy opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="1e2e5-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span> 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="1e2e5-118">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="1e2e5-118">Connector-specific details</span></span>

<span data-ttu-id="1e2e5-119">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/github/).</span><span class="sxs-lookup"><span data-stu-id="1e2e5-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/github/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="1e2e5-120">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="1e2e5-120">More connectors</span></span>
<span data-ttu-id="1e2e5-121">Wróć do [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="1e2e5-121">Go back to the [APIs list](apis-list.md).</span></span>