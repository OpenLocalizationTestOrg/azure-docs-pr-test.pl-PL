---
title: "Dodaj łącznik usługi Twilio w aplikacje logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Omówienie łącznika usługi Twilio z parametrami interfejsu API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a790ac51b0fea7e3fa379d20e0e094e7ce0d7696
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twilio-connector"></a><span data-ttu-id="64523-103">Rozpoczynanie pracy z łącznikiem usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="64523-103">Get started with the Twilio connector</span></span>
<span data-ttu-id="64523-104">Nawiązać połączenia z usługi Twilio do wysyłania i odbierania globalne wiadomości SMS i MMS, adresu IP.</span><span class="sxs-lookup"><span data-stu-id="64523-104">Connect to Twilio to send and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="64523-105">Za pomocą usługi Twilio można:</span><span class="sxs-lookup"><span data-stu-id="64523-105">With Twilio, you can:</span></span>

* <span data-ttu-id="64523-106">Tworzenie sieci przepływu biznesowe na podstawie danych otrzymywanych z usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="64523-106">Build your business flow based on the data you get from Twilio.</span></span> 
* <span data-ttu-id="64523-107">Użyj akcje, które pobierają wiadomości, lista wiadomości i inne.</span><span class="sxs-lookup"><span data-stu-id="64523-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="64523-108">Te akcje uzyskać odpowiedzi, a następnie udostępnić dane wyjściowe do innych działań.</span><span class="sxs-lookup"><span data-stu-id="64523-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="64523-109">Na przykład gdy pojawi się nowy komunikat usługi Twilio, można ten komunikat i używać go w przepływie pracy usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="64523-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="64523-110">Rozpoczynanie pracy przez tworzenie aplikacji logiki; zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="64523-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-twilio"></a><span data-ttu-id="64523-111">Utwórz połączenie z usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="64523-111">Create a connection to Twilio</span></span>
<span data-ttu-id="64523-112">Po dodaniu tego łącznika do aplikacji logiki, wprowadź następujące wartości usługi Twilio:</span><span class="sxs-lookup"><span data-stu-id="64523-112">When you add this Connector to your logic apps, enter the following Twilio values:</span></span>

| <span data-ttu-id="64523-113">Właściwość</span><span class="sxs-lookup"><span data-stu-id="64523-113">Property</span></span> | <span data-ttu-id="64523-114">Wymagane</span><span class="sxs-lookup"><span data-stu-id="64523-114">Required</span></span> | <span data-ttu-id="64523-115">Opis</span><span class="sxs-lookup"><span data-stu-id="64523-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64523-116">Identyfikator konta</span><span class="sxs-lookup"><span data-stu-id="64523-116">Account ID</span></span> |<span data-ttu-id="64523-117">Tak</span><span class="sxs-lookup"><span data-stu-id="64523-117">Yes</span></span> |<span data-ttu-id="64523-118">Wprowadź identyfikator konta usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="64523-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="64523-119">Token dostępu</span><span class="sxs-lookup"><span data-stu-id="64523-119">Access Token</span></span> |<span data-ttu-id="64523-120">Tak</span><span class="sxs-lookup"><span data-stu-id="64523-120">Yes</span></span> |<span data-ttu-id="64523-121">Wprowadź token dostępu usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="64523-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps to create a connection to Twilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="64523-122">Jeśli nie masz tokenu dostępu usługi Twilio, zobacz [tożsamości użytkowników i tokenów dostępu](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="64523-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="64523-123">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="64523-123">Connector-specific details</span></span>

<span data-ttu-id="64523-124">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="64523-124">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="64523-125">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="64523-125">More connectors</span></span>
<span data-ttu-id="64523-126">Wróć do [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="64523-126">Go back to the [APIs list](apis-list.md).</span></span>