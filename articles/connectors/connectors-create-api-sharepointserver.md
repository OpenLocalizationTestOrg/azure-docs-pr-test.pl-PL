---
title: "Witaj aaaUse łącznika serwera programu SharePoint w aplikacji logiki | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy przy użyciu hello hello łącznika serwera programu SharePoint w aplikacji logiki"
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
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a><span data-ttu-id="eeae9-103">Rozpoczynanie pracy z hello łącznika programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="eeae9-103">Get started with hello SharePoint connector</span></span>
<span data-ttu-id="eeae9-104">Witaj łącznika programu SharePoint zawiera toowork sposób przy użyciu list w programie SharePoint.</span><span class="sxs-lookup"><span data-stu-id="eeae9-104">hello SharePoint Connector provides an way toowork with Lists on SharePoint.</span></span>

<span data-ttu-id="eeae9-105">Rozpoczynanie pracy przez tworzenie aplikacji logiki; zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="eeae9-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toosharepoint"></a><span data-ttu-id="eeae9-106">Tworzenie tooSharePoint połączenia</span><span class="sxs-lookup"><span data-stu-id="eeae9-106">Create a connection tooSharePoint</span></span>
<span data-ttu-id="eeae9-107">toouse hello łącznika programu SharePoint, należy najpierw utworzyć **połączenia** następnie podaj szczegóły hello tych właściwości:</span><span class="sxs-lookup"><span data-stu-id="eeae9-107">toouse hello SharePoint Connector , you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="eeae9-108">Właściwość</span><span class="sxs-lookup"><span data-stu-id="eeae9-108">Property</span></span> | <span data-ttu-id="eeae9-109">Wymagane</span><span class="sxs-lookup"><span data-stu-id="eeae9-109">Required</span></span> | <span data-ttu-id="eeae9-110">Opis</span><span class="sxs-lookup"><span data-stu-id="eeae9-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eeae9-111">Token</span><span class="sxs-lookup"><span data-stu-id="eeae9-111">Token</span></span> |<span data-ttu-id="eeae9-112">Tak</span><span class="sxs-lookup"><span data-stu-id="eeae9-112">Yes</span></span> |<span data-ttu-id="eeae9-113">Podaj poświadczenia programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="eeae9-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="eeae9-114">tooconnect za**SharePoint**, wprowadź tooSharePoint Twojej tożsamości (nazwy użytkownika i hasła, poświadczeń karty inteligentnej, itp.).</span><span class="sxs-lookup"><span data-stu-id="eeae9-114">tooconnect too**SharePoint**, enter your identity (username and password, smart card credentials, etc.) tooSharePoint.</span></span> <span data-ttu-id="eeae9-115">Po zostały uwierzytelniono, można przystąpić toouse hello SharePoint łącznika w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="eeae9-115">Once you've been authenticated, you can proceed toouse hello SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="eeae9-116">Znajduje się na powitania projektanta aplikacji logiki, wykonaj te kroki toosign w SharePoint toocreate hello połączenie **połączenia** do użycia w aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="eeae9-116">While on hello designer of your logic app, follow these steps toosign into SharePoint toocreate hello connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="eeae9-117">Wprowadź w polu wyszukiwania hello programu SharePoint i poczekaj, aż tooreturn wyszukiwania hello, wszystkie wpisy z programem SharePoint w nazwie hello:</span><span class="sxs-lookup"><span data-stu-id="eeae9-117">Enter SharePoint in hello search box and wait for hello search tooreturn all entries with SharePoint in hello name:</span></span>   
   ![Konfigurowanie programu SharePoint][1]  
2. <span data-ttu-id="eeae9-119">Wybierz **SharePoint — po utworzeniu pliku**</span><span class="sxs-lookup"><span data-stu-id="eeae9-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="eeae9-120">Wybierz **Zaloguj tooSharePoint**:</span><span class="sxs-lookup"><span data-stu-id="eeae9-120">Select **Sign in tooSharePoint**:</span></span>   
   <span data-ttu-id="eeae9-121">![Konfigurowanie programu SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="eeae9-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="eeae9-122">Podaj toosign poświadczeń programu SharePoint, korzystając z tooauthenticate z programem SharePoint</span><span class="sxs-lookup"><span data-stu-id="eeae9-122">Provide your SharePoint credentials toosign in tooauthenticate with SharePoint</span></span>   
   ![Konfigurowanie programu SharePoint][3]     
5. <span data-ttu-id="eeae9-124">Po zakończeniu uwierzytelniania hello będzie toocomplete aplikacji logiki przekierowanego tooyour go przez skonfigurowanie SharePoint **podczas tworzenia pliku** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eeae9-124">After hello authentication completes you'll be redirected tooyour logic app toocomplete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="eeae9-125">![Konfigurowanie programu SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="eeae9-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="eeae9-126">Następnie można dodać inne wyzwalacze i akcje muszą toocomplete aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="eeae9-126">You can then add other triggers and actions that you need toocomplete your logic app.</span></span>   
7. <span data-ttu-id="eeae9-127">Zapisz swoją pracę, wybierając **zapisać** na pasku menu hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="eeae9-127">Save your work by selecting **Save** on hello menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="eeae9-128">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="eeae9-128">Connector-specific details</span></span>

<span data-ttu-id="eeae9-129">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="eeae9-129">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="eeae9-130">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="eeae9-130">More connectors</span></span>
<span data-ttu-id="eeae9-131">Przejdź wstecz toohello [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="eeae9-131">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
