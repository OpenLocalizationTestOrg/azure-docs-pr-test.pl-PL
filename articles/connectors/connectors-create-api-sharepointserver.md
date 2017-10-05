---
title: "Używany jest łącznik serwera programu SharePoint w aplikacji logiki | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy przy użyciu łącznika serwera programu SharePoint w aplikacji logiki"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0f3274816e279a1aa57febaa2f8294914900799a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-connector"></a><span data-ttu-id="70716-103">Rozpoczynanie pracy z łącznikiem programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="70716-103">Get started with the SharePoint connector</span></span>
<span data-ttu-id="70716-104">Łącznik programu SharePoint umożliwia pracę z listy w programie SharePoint.</span><span class="sxs-lookup"><span data-stu-id="70716-104">The SharePoint Connector provides an way to work with Lists on SharePoint.</span></span>

<span data-ttu-id="70716-105">Rozpoczynanie pracy przez tworzenie aplikacji logiki; zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="70716-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sharepoint"></a><span data-ttu-id="70716-106">Utwórz połączenie programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="70716-106">Create a connection to SharePoint</span></span>
<span data-ttu-id="70716-107">Do korzystania z łącznika programu SharePoint, należy najpierw utworzyć **połączenia** następnie podaj szczegóły tych właściwości:</span><span class="sxs-lookup"><span data-stu-id="70716-107">To use the SharePoint Connector , you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="70716-108">Właściwość</span><span class="sxs-lookup"><span data-stu-id="70716-108">Property</span></span> | <span data-ttu-id="70716-109">Wymagane</span><span class="sxs-lookup"><span data-stu-id="70716-109">Required</span></span> | <span data-ttu-id="70716-110">Opis</span><span class="sxs-lookup"><span data-stu-id="70716-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="70716-111">Token</span><span class="sxs-lookup"><span data-stu-id="70716-111">Token</span></span> |<span data-ttu-id="70716-112">Tak</span><span class="sxs-lookup"><span data-stu-id="70716-112">Yes</span></span> |<span data-ttu-id="70716-113">Podaj poświadczenia programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="70716-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="70716-114">Aby nawiązać połączenie **SharePoint**, wprowadź swoją tożsamość, (nazwa użytkownika i hasło, inteligentne poświadczeń karty, itp.) w programie SharePoint.</span><span class="sxs-lookup"><span data-stu-id="70716-114">To connect to **SharePoint**, enter your identity (username and password, smart card credentials, etc.) to SharePoint.</span></span> <span data-ttu-id="70716-115">Po zostały uwierzytelniono, można przystąpić do korzystania z łącznika programu SharePoint w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="70716-115">Once you've been authenticated, you can proceed to use the SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="70716-116">W Projektancie aplikacji logiki, wykonaj następujące kroki, aby zalogować się do programu SharePoint do utworzenia połączenia **połączenia** do użycia w aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="70716-116">While on the designer of your logic app, follow these steps to sign into SharePoint to create the connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="70716-117">Wprowadź w polu wyszukiwania programu SharePoint i poczekaj, aż wyszukiwania zwrócić wszystkie wpisy z programem SharePoint w nazwie:</span><span class="sxs-lookup"><span data-stu-id="70716-117">Enter SharePoint in the search box and wait for the search to return all entries with SharePoint in the name:</span></span>   
   ![Konfigurowanie programu SharePoint][1]  
2. <span data-ttu-id="70716-119">Wybierz **SharePoint — po utworzeniu pliku**</span><span class="sxs-lookup"><span data-stu-id="70716-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="70716-120">Wybierz **Zaloguj się do programu SharePoint**:</span><span class="sxs-lookup"><span data-stu-id="70716-120">Select **Sign in to SharePoint**:</span></span>   
   <span data-ttu-id="70716-121">![Konfigurowanie programu SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="70716-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="70716-122">Podaj poświadczenia programu SharePoint, aby zalogować się do uwierzytelniania za pomocą programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="70716-122">Provide your SharePoint credentials to sign in to authenticate with SharePoint</span></span>   
   ![Konfigurowanie programu SharePoint][3]     
5. <span data-ttu-id="70716-124">Po zakończeniu uwierzytelniania będzie zostanie przekierowany do aplikacji logiki do ukończenia jej przez skonfigurowanie SharePoint **podczas tworzenia pliku** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="70716-124">After the authentication completes you'll be redirected to your logic app to complete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="70716-125">![Konfigurowanie programu SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="70716-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="70716-126">Następnie można dodać inne wyzwalacze i akcje, które należy wykonać aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="70716-126">You can then add other triggers and actions that you need to complete your logic app.</span></span>   
7. <span data-ttu-id="70716-127">Zapisz swoją pracę, wybierając **zapisać** na pasku menu powyżej.</span><span class="sxs-lookup"><span data-stu-id="70716-127">Save your work by selecting **Save** on the menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="70716-128">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="70716-128">Connector-specific details</span></span>

<span data-ttu-id="70716-129">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="70716-129">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="70716-130">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="70716-130">More connectors</span></span>
<span data-ttu-id="70716-131">Wróć do [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="70716-131">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
