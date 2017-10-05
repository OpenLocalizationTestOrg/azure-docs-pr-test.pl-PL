---
title: "Łącznik usługi Outlook.com w programie Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Łącznik usługi Outlook.com umożliwia zarządzanie poczty, kontaktów i kalendarzy. Można wykonywać różne akcje, takie jak wysyłania wiadomości e-mail, planować spotkania, Dodaj kontakty itp."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 87113c85-d158-4dd5-9ed5-5748130003d6
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: bde1629504c97cf6706b42219570ffa6243073dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-outlookcom-connector"></a><span data-ttu-id="8f24f-105">Rozpoczynanie pracy z łącznikiem usługi Outlook.com</span><span class="sxs-lookup"><span data-stu-id="8f24f-105">Get started with the Outlook.com connector</span></span>
<span data-ttu-id="8f24f-106">Łącznik usługi Outlook.com umożliwia zarządzanie poczty, kontaktów i kalendarzy.</span><span class="sxs-lookup"><span data-stu-id="8f24f-106">Outlook.com connector allows you to manage your mail, calendars, and contacts.</span></span> <span data-ttu-id="8f24f-107">Można wykonywać różne akcje, takie jak wysyłania wiadomości e-mail, planować spotkania, Dodaj kontakty itp.</span><span class="sxs-lookup"><span data-stu-id="8f24f-107">You can perform various actions such as send mail, schedule meetings, add contacts, etc.</span></span>

<span data-ttu-id="8f24f-108">Rozpoczynanie pracy przez teraz tworzenie aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8f24f-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-outlookcom"></a><span data-ttu-id="8f24f-109">Utwórz połączenie Outlook.com</span><span class="sxs-lookup"><span data-stu-id="8f24f-109">Create a connection to Outlook.com</span></span>
<span data-ttu-id="8f24f-110">Do tworzenia aplikacji logiki z usługi Outlook.com, należy najpierw utworzyć **połączenia** następnie podaj szczegóły następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="8f24f-110">To create Logic apps with Outlook.com, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="8f24f-111">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8f24f-111">Property</span></span> | <span data-ttu-id="8f24f-112">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8f24f-112">Required</span></span> | <span data-ttu-id="8f24f-113">Opis</span><span class="sxs-lookup"><span data-stu-id="8f24f-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8f24f-114">Token</span><span class="sxs-lookup"><span data-stu-id="8f24f-114">Token</span></span> |<span data-ttu-id="8f24f-115">Tak</span><span class="sxs-lookup"><span data-stu-id="8f24f-115">Yes</span></span> |<span data-ttu-id="8f24f-116">Podaj poświadczenia usługi Outlook.com</span><span class="sxs-lookup"><span data-stu-id="8f24f-116">Provide Outlook.com Credentials</span></span> |

<span data-ttu-id="8f24f-117">Po utworzeniu połączenia, można go wykonać akcje i będzie nasłuchiwać wyzwalaczy opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="8f24f-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to Outlook.com](../../includes/connectors-create-api-outlook.md)]
>

## <a name="connector-specific-details"></a><span data-ttu-id="8f24f-118">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="8f24f-118">Connector-specific details</span></span>

<span data-ttu-id="8f24f-119">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/outlook/).</span><span class="sxs-lookup"><span data-stu-id="8f24f-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/outlook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="8f24f-120">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="8f24f-120">More connectors</span></span>
<span data-ttu-id="8f24f-121">Wróć do [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8f24f-121">Go back to the [APIs list](apis-list.md).</span></span>