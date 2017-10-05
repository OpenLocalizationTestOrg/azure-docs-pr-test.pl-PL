---
title: "Łącznik usługi Dropbox w programie Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Podłącz do skrzynki do zarządzania plikami. Można wykonywać różne akcje, takie jak przekazywanie, zaktualizować, Pobierz i usuwania plików skrzynki."
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
ms.openlocfilehash: 0d09580c60fd620811b539147439d0922839fe7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-dropbox-connector"></a><span data-ttu-id="79ee5-105">Rozpoczynanie pracy z łącznikiem usługi Dropbox</span><span class="sxs-lookup"><span data-stu-id="79ee5-105">Get started with the Dropbox connector</span></span>
<span data-ttu-id="79ee5-106">Podłącz do skrzynki do zarządzania plikami.</span><span class="sxs-lookup"><span data-stu-id="79ee5-106">Connect to Dropbox to manage your files.</span></span> <span data-ttu-id="79ee5-107">Można wykonywać różne akcje, takie jak przekazywanie, zaktualizować, Pobierz i usuwania plików skrzynki.</span><span class="sxs-lookup"><span data-stu-id="79ee5-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="79ee5-108">Aby użyć [każdy łącznik](apis-list.md), należy najpierw utworzyć aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="79ee5-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="79ee5-109">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="79ee5-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-dropbox"></a><span data-ttu-id="79ee5-110">Nawiązać skrzynki</span><span class="sxs-lookup"><span data-stu-id="79ee5-110">Connect to Dropbox</span></span>
<span data-ttu-id="79ee5-111">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* do usługi.</span><span class="sxs-lookup"><span data-stu-id="79ee5-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="79ee5-112">Połączenie stanowi połączenie między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="79ee5-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="79ee5-113">Na przykład, aby nawiązać połączenie usługi Dropbox, należy najpierw Dropbox *połączenia*.</span><span class="sxs-lookup"><span data-stu-id="79ee5-113">For example, in order to connect to Dropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="79ee5-114">Aby utworzyć połączenie, musisz podać poświadczenia, które zwykle jest używana do uzyskania dostępu do usługi, który chcesz połączyć się z.</span><span class="sxs-lookup"><span data-stu-id="79ee5-114">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="79ee5-115">Tak w tym przykładzie skrzynki konieczne będzie poświadczenia konta Dropbox, aby utworzyć połączenie usługi Dropbox.</span><span class="sxs-lookup"><span data-stu-id="79ee5-115">So, in the Dropbox example, you would need the credentials to your Dropbox account in order to create the connection to Dropbox.</span></span> [<span data-ttu-id="79ee5-116">Dowiedz się więcej na temat połączenia</span><span class="sxs-lookup"><span data-stu-id="79ee5-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-to-dropbox"></a><span data-ttu-id="79ee5-117">Utwórz połączenie usługi Dropbox</span><span class="sxs-lookup"><span data-stu-id="79ee5-117">Create a connection to Dropbox</span></span>
> [!INCLUDE [Steps to create a connection to Dropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="79ee5-118">Użyj wyzwalacz skrzynki</span><span class="sxs-lookup"><span data-stu-id="79ee5-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="79ee5-119">Wyzwalacz to zdarzenie służy do uruchomienia przepływu pracy zdefiniowanych w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="79ee5-119">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="79ee5-120">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="79ee5-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="79ee5-121">W tym przykładzie używamy **podczas tworzenia pliku** wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="79ee5-121">In this example, we will use the **When a file is created** trigger.</span></span> <span data-ttu-id="79ee5-122">W przypadku wystąpienia tego wyzwalacza będzie nazywamy **pobieranie plików zawartości przy użyciu ścieżki** skrzynki akcji.</span><span class="sxs-lookup"><span data-stu-id="79ee5-122">When this trigger occurs, we will call the **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="79ee5-123">Wprowadź *dropbox* w polu wyszukiwania w Projektancie aplikacji logiki, następnie wybierz **Dropbox — po utworzeniu pliku** wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="79ee5-123">Enter *dropbox* in the search box on the Logic Apps designer, then select the **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="79ee5-124">Wybierz folder, w którym mają być śledzone tworzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="79ee5-124">Select the folder in which you want to track file creation.</span></span> <span data-ttu-id="79ee5-125">Wybierz... (określone w czerwonym prostokątem), a następnie przejdź do folderu, który chcesz wybrać w odniesieniu do danych wejściowych wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="79ee5-125">Select ... (identified in the red box) and browse to the folder you wish to select for the trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="79ee5-126">Za pomocą akcji skrzynki</span><span class="sxs-lookup"><span data-stu-id="79ee5-126">Use a Dropbox action</span></span>
<span data-ttu-id="79ee5-127">Akcja jest przeprowadzane przez przepływ pracy zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="79ee5-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="79ee5-128">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="79ee5-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="79ee5-129">Teraz, wyzwalacz został dodany, wykonaj następujące kroki, aby dodać akcję, która zostanie wyświetlony nowy plik zawartości.</span><span class="sxs-lookup"><span data-stu-id="79ee5-129">Now that the trigger has been added, follow these steps to add an action that will get the new file's content.</span></span>

1. <span data-ttu-id="79ee5-130">Wybierz **+ nowy krok** Aby dodać akcję chcesz wykonać, gdy zostanie utworzony nowy plik.</span><span class="sxs-lookup"><span data-stu-id="79ee5-130">Select **+ New Step** to add the action you would like to take when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="79ee5-131">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="79ee5-131">Select **Add an action**.</span></span> <span data-ttu-id="79ee5-132">Służy to pole wyszukiwania, gdzie możesz wyszukać dowolną akcję użytkownik chce przejąć.</span><span class="sxs-lookup"><span data-stu-id="79ee5-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="79ee5-133">Wprowadź *dropbox* do wyszukania akcji związanych z Dropbox.</span><span class="sxs-lookup"><span data-stu-id="79ee5-133">Enter *dropbox* to search for actions related to Dropbox.</span></span>  
4. <span data-ttu-id="79ee5-134">Wybierz **Dropbox - pobrania zawartości pliku przy użyciu ścieżki** jako akcję wykonywaną, gdy nowy plik jest tworzony w wybranym folderze Dropbox.</span><span class="sxs-lookup"><span data-stu-id="79ee5-134">Select **Dropbox - Get file content using path** as the action to take when a new file is created in the selected Dropbox folder.</span></span> <span data-ttu-id="79ee5-135">Zostanie otwarty blok kontroli akcji.</span><span class="sxs-lookup"><span data-stu-id="79ee5-135">The action control block opens.</span></span> <span data-ttu-id="79ee5-136">Pojawi się monit o autoryzowanie aplikację logiki, aby uzyskać dostęp do konta Dropbox, jeśli nie zostało zrobione to wcześniej.</span><span class="sxs-lookup"><span data-stu-id="79ee5-136">You will be prompted to authorize your logic app to access your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="79ee5-137">Wybierz... (znajdujący się w prawej części **ścieżka pliku** sterowania) i przejdź do ścieżki pliku chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="79ee5-137">Select ... (located at the right side of the **File Path** control) and browse to the file path you would like to use.</span></span> <span data-ttu-id="79ee5-138">Lub użyj **ścieżka pliku** tokenu, aby przyspieszyć tworzenie aplikacji sieci logiczne.</span><span class="sxs-lookup"><span data-stu-id="79ee5-138">Or, use the **file path** token to speed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="79ee5-139">Zapisz swoją pracę i Utwórz nowy plik w Dropbox, aby aktywować przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="79ee5-139">Save your work and create a new file in Dropbox to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="79ee5-140">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="79ee5-140">Connector-specific details</span></span>

<span data-ttu-id="79ee5-141">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="79ee5-141">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="79ee5-142">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="79ee5-142">More connectors</span></span>
<span data-ttu-id="79ee5-143">Wróć do [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="79ee5-143">Go back to the [APIs list](apis-list.md).</span></span>