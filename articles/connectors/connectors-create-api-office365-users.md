---
title: "Dodaj użytkowników usługi Office 365 łącznika w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Omówienie łącznika użytkowników usługi Office 365 z parametrami interfejsu API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 330f733440932a769eb0fe6031cd0d947a820080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-users-connector"></a><span data-ttu-id="ad60a-103">Rozpoczynanie pracy z łącznikiem użytkowników usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="ad60a-103">Get started with the Office 365 Users connector</span></span>
<span data-ttu-id="ad60a-104">Podłącz do użytkowników usługi Office 365 można pobrać profilów, Wyszukaj użytkowników i inne.</span><span class="sxs-lookup"><span data-stu-id="ad60a-104">Connect to Office 365 Users to get profiles, search users, and more.</span></span> <span data-ttu-id="ad60a-105">Użytkowników usługi Office 365 możesz:</span><span class="sxs-lookup"><span data-stu-id="ad60a-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="ad60a-106">Tworzenie sieci przepływu biznesowe na podstawie danych, który można uzyskać od użytkowników usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="ad60a-106">Build your business flow based on the data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="ad60a-107">Użyj akcji, które uzyskać bezpośrednich podwładnych pobrać menedżera profilu użytkownika i inne.</span><span class="sxs-lookup"><span data-stu-id="ad60a-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="ad60a-108">Te akcje uzyskać odpowiedzi, a następnie udostępnić dane wyjściowe do innych działań.</span><span class="sxs-lookup"><span data-stu-id="ad60a-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="ad60a-109">Na przykład uzyskać osoby bezpośrednich podwładnych, a następnie pobierać te informacje i zaktualizować bazę danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ad60a-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="ad60a-110">Rozpoczynanie pracy przez teraz tworzenie aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ad60a-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office-365-users"></a><span data-ttu-id="ad60a-111">Utwórz połączenie użytkowników usługi Office 365</span><span class="sxs-lookup"><span data-stu-id="ad60a-111">Create a connection to Office 365 Users</span></span>
<span data-ttu-id="ad60a-112">Po dodaniu tego łącznika do aplikacji logiki, należy zalogować się do konta użytkowników usługi Office 365 i Zezwalaj aplikacjom logiki do łączenia się z kontem.</span><span class="sxs-lookup"><span data-stu-id="ad60a-112">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="ad60a-113">Po utworzeniu połączenie, wprowadź właściwości użytkowników usługi Office 365, takich jak identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ad60a-113">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span></span> <span data-ttu-id="ad60a-114">**Dokumentacji interfejsu API REST** w tym temacie opisano te właściwości.</span><span class="sxs-lookup"><span data-stu-id="ad60a-114">The **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="ad60a-115">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="ad60a-115">Connector-specific details</span></span>

<span data-ttu-id="ad60a-116">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/officeusers/).</span><span class="sxs-lookup"><span data-stu-id="ad60a-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="ad60a-117">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="ad60a-117">More connectors</span></span>
<span data-ttu-id="ad60a-118">Wróć do [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ad60a-118">Go back to the [APIs list](apis-list.md).</span></span>