---
title: "Łącznik aaaDropbox w programie Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Połącz tooDropbox toomanage plików. Można wykonywać różne akcje, takie jak przekazywanie, zaktualizować, Pobierz i usuwania plików skrzynki."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a><span data-ttu-id="7b5bd-105">Rozpoczynanie pracy z łącznikiem usługi Dropbox hello</span><span class="sxs-lookup"><span data-stu-id="7b5bd-105">Get started with hello Dropbox connector</span></span>
<span data-ttu-id="7b5bd-106">Połącz tooDropbox toomanage plików.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-106">Connect tooDropbox toomanage your files.</span></span> <span data-ttu-id="7b5bd-107">Można wykonywać różne akcje, takie jak przekazywanie, zaktualizować, Pobierz i usuwania plików skrzynki.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="7b5bd-108">toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="7b5bd-109">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7b5bd-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toodropbox"></a><span data-ttu-id="7b5bd-110">Połącz tooDropbox</span><span class="sxs-lookup"><span data-stu-id="7b5bd-110">Connect tooDropbox</span></span>
<span data-ttu-id="7b5bd-111">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate *połączenia* toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="7b5bd-112">Połączenie stanowi połączenie między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="7b5bd-113">Na przykład w kolejności tooconnect tooDropbox, należy najpierw Dropbox *połączenia*.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-113">For example, in order tooconnect tooDropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="7b5bd-114">toocreate połączenie, będzie potrzebny poświadczenia hello tooprovide tooaccess hello usługi, które mają tooconnect do zwykle jest używana.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-114">toocreate a connection, you would need tooprovide hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="7b5bd-115">Tak w przykładzie skrzynki hello będzie potrzebny hello tooyour poświadczenia konta Dropbox w kolejności toocreate hello połączenia tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-115">So, in hello Dropbox example, you would need hello credentials tooyour Dropbox account in order toocreate hello connection tooDropbox.</span></span> [<span data-ttu-id="7b5bd-116">Dowiedz się więcej na temat połączenia</span><span class="sxs-lookup"><span data-stu-id="7b5bd-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-toodropbox"></a><span data-ttu-id="7b5bd-117">Tworzenie tooDropbox połączenia</span><span class="sxs-lookup"><span data-stu-id="7b5bd-117">Create a connection tooDropbox</span></span>
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="7b5bd-118">Użyj wyzwalacz skrzynki</span><span class="sxs-lookup"><span data-stu-id="7b5bd-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="7b5bd-119">Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-119">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="7b5bd-120">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="7b5bd-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="7b5bd-121">W tym przykładzie używamy hello **podczas tworzenia pliku** wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-121">In this example, we will use hello **When a file is created** trigger.</span></span> <span data-ttu-id="7b5bd-122">W przypadku wystąpienia tego wyzwalacza będzie nazywamy hello **pobieranie plików zawartości przy użyciu ścieżki** skrzynki akcji.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-122">When this trigger occurs, we will call hello **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="7b5bd-123">Wprowadź *dropbox* w polu wyszukiwania hello hello Logic Apps designer, a następnie wybierz hello **Dropbox — po utworzeniu pliku** wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-123">Enter *dropbox* in hello search box on hello Logic Apps designer, then select hello **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="7b5bd-124">Wybierz folder hello, w której ma zostać tootrack tworzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-124">Select hello folder in which you want tootrack file creation.</span></span> <span data-ttu-id="7b5bd-125">Wybierz... (określone w polu hello czerwony) i przeglądania folderów toohello ma wejściowych tooselect hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-125">Select ... (identified in hello red box) and browse toohello folder you wish tooselect for hello trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="7b5bd-126">Za pomocą akcji skrzynki</span><span class="sxs-lookup"><span data-stu-id="7b5bd-126">Use a Dropbox action</span></span>
<span data-ttu-id="7b5bd-127">Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="7b5bd-128">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="7b5bd-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="7b5bd-129">Teraz, gdy hello wyzwalacz został dodany, wykonaj te kroki tooadd akcję, która pobierze zawartość hello nowy plik.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-129">Now that hello trigger has been added, follow these steps tooadd an action that will get hello new file's content.</span></span>

1. <span data-ttu-id="7b5bd-130">Wybierz **+ nowy krok** akcji hello tooadd chcesz tootake podczas tworzenia nowego pliku.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-130">Select **+ New Step** tooadd hello action you would like tootake when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="7b5bd-131">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-131">Select **Add an action**.</span></span> <span data-ttu-id="7b5bd-132">To pole wyszukiwania hello otwiera gdzie możesz wyszukać dowolną akcję należy chcieliby tootake.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="7b5bd-133">Wprowadź *dropbox* toosearch dla tooDropbox powiązanych działań.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-133">Enter *dropbox* toosearch for actions related tooDropbox.</span></span>  
4. <span data-ttu-id="7b5bd-134">Wybierz **Dropbox - pobrania zawartości pliku przy użyciu ścieżki** jako hello tootake akcji podczas tworzenia nowego pliku w hello wybrany Dropbox folder.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-134">Select **Dropbox - Get file content using path** as hello action tootake when a new file is created in hello selected Dropbox folder.</span></span> <span data-ttu-id="7b5bd-135">zostanie otwarty blok kontroli Hello akcji.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-135">hello action control block opens.</span></span> <span data-ttu-id="7b5bd-136">Użytkownik będzie zostanie wyświetlony monit o tooauthorize Twojego tooaccess aplikacji logiki usłudze Dropbox konta, jeśli nie zostało zrobione to wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-136">You will be prompted tooauthorize your logic app tooaccess your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="7b5bd-137">Wybierz... (znajdujący się na powitania po prawej stronie powitania **ścieżka pliku** sterowania) i przejdź do ścieżki pliku toohello chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-137">Select ... (located at hello right side of hello **File Path** control) and browse toohello file path you would like toouse.</span></span> <span data-ttu-id="7b5bd-138">Lub użyj hello **ścieżka pliku** tokenu toospeed się z tworzenia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-138">Or, use hello **file path** token toospeed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="7b5bd-139">Zapisz swoją pracę i Utwórz nowy plik w Dropbox tooactivate przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="7b5bd-139">Save your work and create a new file in Dropbox tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="7b5bd-140">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="7b5bd-140">Connector-specific details</span></span>

<span data-ttu-id="7b5bd-141">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="7b5bd-141">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="7b5bd-142">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="7b5bd-142">More connectors</span></span>
<span data-ttu-id="7b5bd-143">Przejdź wstecz toohello [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="7b5bd-143">Go back toohello [APIs list](apis-list.md).</span></span>
