---
title: "aaaUse hello łącznika zapas czasu w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Połącz tooSlack w aplikacjach logiki"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a><span data-ttu-id="531e7-103">Rozpoczynanie pracy z hello Slack łącznika</span><span class="sxs-lookup"><span data-stu-id="531e7-103">Get started with hello Slack connector</span></span>
<span data-ttu-id="531e7-104">Slack jest narzędziem do komunikacji zespołowej, które łączy całą komunikację zespołową w jednym miejscu. Umożliwia natychmiastowe wyszukiwanie i dostęp do komunikacji z dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="531e7-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="531e7-105">Rozpoczynanie pracy przez tworzenie aplikacji logiki teraz; zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="531e7-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooslack"></a><span data-ttu-id="531e7-106">Tworzenie tooSlack połączenia</span><span class="sxs-lookup"><span data-stu-id="531e7-106">Create a connection tooSlack</span></span>
<span data-ttu-id="531e7-107">Łącznik Slack hello toouse, należy najpierw utworzyć **połączenia** następnie podaj szczegóły hello tych właściwości:</span><span class="sxs-lookup"><span data-stu-id="531e7-107">toouse hello Slack connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="531e7-108">Właściwość</span><span class="sxs-lookup"><span data-stu-id="531e7-108">Property</span></span> | <span data-ttu-id="531e7-109">Wymagane</span><span class="sxs-lookup"><span data-stu-id="531e7-109">Required</span></span> | <span data-ttu-id="531e7-110">Opis</span><span class="sxs-lookup"><span data-stu-id="531e7-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="531e7-111">Token</span><span class="sxs-lookup"><span data-stu-id="531e7-111">Token</span></span> |<span data-ttu-id="531e7-112">Tak</span><span class="sxs-lookup"><span data-stu-id="531e7-112">Yes</span></span> |<span data-ttu-id="531e7-113">Podanie Slack poświadczeń</span><span class="sxs-lookup"><span data-stu-id="531e7-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="531e7-114">Wykonaj te kroki toosign do zapas czasu i hello ukończenia konfiguracji hello zapas czasu **połączenia** w aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="531e7-114">Follow these steps toosign into Slack, and complete hello configuration of hello Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="531e7-115">Wybierz **cyklu**</span><span class="sxs-lookup"><span data-stu-id="531e7-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="531e7-116">Wybierz **częstotliwość** , a następnie wprowadź **interwał**</span><span class="sxs-lookup"><span data-stu-id="531e7-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="531e7-117">Wybierz **Dodaj akcję**</span><span class="sxs-lookup"><span data-stu-id="531e7-117">Select **Add an action**</span></span>  
   <span data-ttu-id="531e7-118">![Skonfiguruj zapas czasu][1]</span><span class="sxs-lookup"><span data-stu-id="531e7-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="531e7-119">Wprowadź w polu wyszukiwania hello zapas czasu i poczekaj, aż tooreturn wyszukiwania hello, wszystkie wpisy z zapas czasu w nazwie hello</span><span class="sxs-lookup"><span data-stu-id="531e7-119">Enter Slack in hello search box and wait for hello search tooreturn all entries with Slack in hello name</span></span>
5. <span data-ttu-id="531e7-120">Wybierz **Slack - Post wiadomości**</span><span class="sxs-lookup"><span data-stu-id="531e7-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="531e7-121">Wybierz **Zaloguj tooSlack**:</span><span class="sxs-lookup"><span data-stu-id="531e7-121">Select **Sign in tooSlack**:</span></span>  
   <span data-ttu-id="531e7-122">![Skonfiguruj zapas czasu][2]</span><span class="sxs-lookup"><span data-stu-id="531e7-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="531e7-123">Podaj toosign Twojego Slack poświadczeń w aplikacji hello tooauthorize</span><span class="sxs-lookup"><span data-stu-id="531e7-123">Provide your Slack credentials toosign in tooauthorize hello  application</span></span>    
   ![Skonfiguruj zapas czasu][3]  
8. <span data-ttu-id="531e7-125">Będziesz dziennika organizacji tooyour przekierowane na stronie.</span><span class="sxs-lookup"><span data-stu-id="531e7-125">You'll be redirected tooyour organization's Log in page.</span></span> <span data-ttu-id="531e7-126">**Autoryzowanie** Slack toointeract z aplikacji logiki:</span><span class="sxs-lookup"><span data-stu-id="531e7-126">**Authorize** Slack toointeract with your logic app:</span></span>      
   <span data-ttu-id="531e7-127">![Skonfiguruj zapas czasu][5]</span><span class="sxs-lookup"><span data-stu-id="531e7-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="531e7-128">Po zakończeniu autoryzacji hello będzie toocomplete aplikacji logiki przekierowanego tooyour go przez skonfigurowanie hello **Slack — pobranie wszystkich wiadomości** sekcji.</span><span class="sxs-lookup"><span data-stu-id="531e7-128">After hello authorization completes you'll be redirected tooyour logic app toocomplete it by configuring hello **Slack - Get all messages** section.</span></span> <span data-ttu-id="531e7-129">Dodawanie innych wyzwalacze i akcje, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="531e7-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="531e7-130">![Skonfiguruj zapas czasu][6]</span><span class="sxs-lookup"><span data-stu-id="531e7-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="531e7-131">Zapisz swoją pracę, wybierając **zapisać** na pasku menu hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="531e7-131">Save your work by selecting **Save** on hello menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="531e7-132">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="531e7-132">Connector-specific details</span></span>

<span data-ttu-id="531e7-133">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="531e7-133">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="531e7-134">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="531e7-134">More connectors</span></span>
<span data-ttu-id="531e7-135">Przejdź wstecz toohello [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="531e7-135">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
