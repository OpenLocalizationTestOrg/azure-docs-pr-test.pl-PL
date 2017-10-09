---
title: "aaaAdd hello łącznika usługi Yammer w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Omówienie hello łącznika usługi Yammer z parametrami interfejsu API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5ae0827-fbb3-45ec-8f45-ad1cc2e7eccc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: be75df770a8062d839926dff8c0195d2647f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-yammer-connector"></a><span data-ttu-id="f7f17-103">Rozpoczynanie pracy z łącznikiem usługi Yammer hello</span><span class="sxs-lookup"><span data-stu-id="f7f17-103">Get started with hello Yammer connector</span></span>
<span data-ttu-id="f7f17-104">Połącz tooYammer tooaccess konwersacje w sieci przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="f7f17-104">Connect tooYammer tooaccess conversations in your enterprise network.</span></span> <span data-ttu-id="f7f17-105">Za pomocą usługi Yammer można:</span><span class="sxs-lookup"><span data-stu-id="f7f17-105">With Yammer, you can:</span></span>

* <span data-ttu-id="f7f17-106">Tworzenie sieci przepływu biznesowe na podstawie danych hello, który można pobrać z usługi Yammer.</span><span class="sxs-lookup"><span data-stu-id="f7f17-106">Build your business flow based on hello data you get from Yammer.</span></span> 
* <span data-ttu-id="f7f17-107">Użyj uaktywnia dla istnieje nowy komunikat z grupy lub źródło danych z następujących czynności.</span><span class="sxs-lookup"><span data-stu-id="f7f17-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="f7f17-108">Użyj akcji toopost wiadomości, Pobierz wszystkie komunikaty i inne.</span><span class="sxs-lookup"><span data-stu-id="f7f17-108">Use actions toopost a message, get all messages, and more.</span></span> <span data-ttu-id="f7f17-109">Te akcje odpowiedzi, a następnie wprowadź dane wyjściowe hello dostępne dla innych działań.</span><span class="sxs-lookup"><span data-stu-id="f7f17-109">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="f7f17-110">Na przykład gdy pojawi się nowy komunikat, możesz wysłać wiadomość e-mail przy użyciu usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="f7f17-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="f7f17-111">Rozpoczynanie pracy przez tworzenie aplikacji logiki teraz; zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f7f17-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooyammer"></a><span data-ttu-id="f7f17-112">Tworzenie tooYammer połączenia</span><span class="sxs-lookup"><span data-stu-id="f7f17-112">Create a connection tooYammer</span></span>
<span data-ttu-id="f7f17-113">Łącznik usługi Yammer hello toouse, należy najpierw utworzyć **połączenia** następnie podaj szczegóły hello tych właściwości:</span><span class="sxs-lookup"><span data-stu-id="f7f17-113">toouse hello Yammer connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="f7f17-114">Właściwość</span><span class="sxs-lookup"><span data-stu-id="f7f17-114">Property</span></span> | <span data-ttu-id="f7f17-115">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f7f17-115">Required</span></span> | <span data-ttu-id="f7f17-116">Opis</span><span class="sxs-lookup"><span data-stu-id="f7f17-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f7f17-117">Token</span><span class="sxs-lookup"><span data-stu-id="f7f17-117">Token</span></span> |<span data-ttu-id="f7f17-118">Tak</span><span class="sxs-lookup"><span data-stu-id="f7f17-118">Yes</span></span> |<span data-ttu-id="f7f17-119">Podaj poświadczenia usługi Yammer</span><span class="sxs-lookup"><span data-stu-id="f7f17-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps toocreate a connection tooYammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="f7f17-120">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="f7f17-120">Connector-specific details</span></span>

<span data-ttu-id="f7f17-121">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/yammer/).</span><span class="sxs-lookup"><span data-stu-id="f7f17-121">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="f7f17-122">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="f7f17-122">More connectors</span></span>
<span data-ttu-id="f7f17-123">Przejdź wstecz toohello [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f7f17-123">Go back toohello [APIs list](apis-list.md).</span></span>
