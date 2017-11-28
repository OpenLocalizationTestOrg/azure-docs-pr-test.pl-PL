---
title: "aaaAdd hello łącznika usługi Twilio w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Omówienie hello łącznika usługi Twilio z parametrami interfejsu API REST"
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
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a><span data-ttu-id="3aba1-103">Rozpoczynanie pracy z łącznikiem usługi Twilio hello</span><span class="sxs-lookup"><span data-stu-id="3aba1-103">Get started with hello Twilio connector</span></span>
<span data-ttu-id="3aba1-104">Połącz tooTwilio toosend i odbierać globalne wiadomości SMS i MMS, adresu IP.</span><span class="sxs-lookup"><span data-stu-id="3aba1-104">Connect tooTwilio toosend and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="3aba1-105">Za pomocą usługi Twilio można:</span><span class="sxs-lookup"><span data-stu-id="3aba1-105">With Twilio, you can:</span></span>

* <span data-ttu-id="3aba1-106">Tworzenie sieci przepływu biznesowe na podstawie danych hello, które można uzyskać z usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="3aba1-106">Build your business flow based on hello data you get from Twilio.</span></span> 
* <span data-ttu-id="3aba1-107">Użyj akcje, które pobierają wiadomości, lista wiadomości i inne.</span><span class="sxs-lookup"><span data-stu-id="3aba1-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="3aba1-108">Te akcje odpowiedzi, a następnie wprowadź dane wyjściowe hello dostępne dla innych działań.</span><span class="sxs-lookup"><span data-stu-id="3aba1-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="3aba1-109">Na przykład gdy pojawi się nowy komunikat usługi Twilio, można ten komunikat i używać go w przepływie pracy usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3aba1-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="3aba1-110">Rozpoczynanie pracy przez tworzenie aplikacji logiki; zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3aba1-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tootwilio"></a><span data-ttu-id="3aba1-111">Tworzenie tooTwilio połączenia</span><span class="sxs-lookup"><span data-stu-id="3aba1-111">Create a connection tooTwilio</span></span>
<span data-ttu-id="3aba1-112">Po dodaniu aplikacji logiki tooyour tego łącznika, wprowadź następujące wartości usługi Twilio hello:</span><span class="sxs-lookup"><span data-stu-id="3aba1-112">When you add this Connector tooyour logic apps, enter hello following Twilio values:</span></span>

| <span data-ttu-id="3aba1-113">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3aba1-113">Property</span></span> | <span data-ttu-id="3aba1-114">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3aba1-114">Required</span></span> | <span data-ttu-id="3aba1-115">Opis</span><span class="sxs-lookup"><span data-stu-id="3aba1-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3aba1-116">Identyfikator konta</span><span class="sxs-lookup"><span data-stu-id="3aba1-116">Account ID</span></span> |<span data-ttu-id="3aba1-117">Tak</span><span class="sxs-lookup"><span data-stu-id="3aba1-117">Yes</span></span> |<span data-ttu-id="3aba1-118">Wprowadź identyfikator konta usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="3aba1-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="3aba1-119">Token dostępu</span><span class="sxs-lookup"><span data-stu-id="3aba1-119">Access Token</span></span> |<span data-ttu-id="3aba1-120">Tak</span><span class="sxs-lookup"><span data-stu-id="3aba1-120">Yes</span></span> |<span data-ttu-id="3aba1-121">Wprowadź token dostępu usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="3aba1-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="3aba1-122">Jeśli nie masz tokenu dostępu usługi Twilio, zobacz [tożsamości użytkowników i tokenów dostępu](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="3aba1-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="3aba1-123">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="3aba1-123">Connector-specific details</span></span>

<span data-ttu-id="3aba1-124">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="3aba1-124">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="3aba1-125">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="3aba1-125">More connectors</span></span>
<span data-ttu-id="3aba1-126">Przejdź wstecz toohello [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="3aba1-126">Go back toohello [APIs list](apis-list.md).</span></span>
