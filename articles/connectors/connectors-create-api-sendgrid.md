---
title: SendGrid | Dokumentacja firmy Microsoft
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Dostawca połączeń SendGrid umożliwia wysyłanie wiadomości e-mail i zarządzanie nimi listy adresatów."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: bc4f1fc2-824c-4ed7-8de8-e82baff3b746
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 9ff0591741899d65b8274fb14ab3f3c8db9abe36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sendgrid-connector"></a><span data-ttu-id="58d94-104">Rozpoczynanie pracy z łącznika SendGrid</span><span class="sxs-lookup"><span data-stu-id="58d94-104">Get started with the SendGrid connector</span></span>
<span data-ttu-id="58d94-105">Dostawca połączeń SendGrid umożliwia wysyłanie wiadomości e-mail i zarządzanie nimi listy adresatów.</span><span class="sxs-lookup"><span data-stu-id="58d94-105">SendGrid Connection Provider lets you send email and manage recipient lists.</span></span>

<span data-ttu-id="58d94-106">Rozpoczynanie pracy przez teraz tworzenie aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="58d94-106">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sendgrid"></a><span data-ttu-id="58d94-107">Utwórz połączenie SendGrid</span><span class="sxs-lookup"><span data-stu-id="58d94-107">Create a connection to SendGrid</span></span>
<span data-ttu-id="58d94-108">Do tworzenia aplikacji logiki sendgrid, należy najpierw utworzyć **połączenia** następnie podaj szczegóły następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="58d94-108">To create Logic apps with SendGrid, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="58d94-109">Właściwość</span><span class="sxs-lookup"><span data-stu-id="58d94-109">Property</span></span> | <span data-ttu-id="58d94-110">Wymagane</span><span class="sxs-lookup"><span data-stu-id="58d94-110">Required</span></span> | <span data-ttu-id="58d94-111">Opis</span><span class="sxs-lookup"><span data-stu-id="58d94-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58d94-112">apiKey</span><span class="sxs-lookup"><span data-stu-id="58d94-112">ApiKey</span></span> |<span data-ttu-id="58d94-113">Tak</span><span class="sxs-lookup"><span data-stu-id="58d94-113">Yes</span></span> |<span data-ttu-id="58d94-114">Podaj klucz interfejsu Api SendGrid</span><span class="sxs-lookup"><span data-stu-id="58d94-114">Provide Your SendGrid Api Key</span></span> |

> [!INCLUDE [Steps to create a connection to SendGrid](../../includes/connectors-create-api-sendgrid.md)]
> 


<span data-ttu-id="58d94-115">Po utworzeniu połączenia, służy ona do wykonywania działań i nasłuchiwania wyzwalacze.</span><span class="sxs-lookup"><span data-stu-id="58d94-115">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="58d94-116">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="58d94-116">Connector-specific details</span></span>

<span data-ttu-id="58d94-117">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/sendgrid/).</span><span class="sxs-lookup"><span data-stu-id="58d94-117">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sendgrid/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="58d94-118">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="58d94-118">More connectors</span></span>
<span data-ttu-id="58d94-119">Wróć do [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="58d94-119">Go back to the [APIs list](apis-list.md).</span></span>