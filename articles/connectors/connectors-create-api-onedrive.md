---
title: "Łącznik usługi OneDrive hello aaaAdd w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Omówienie hello łącznika usługi OneDrive z parametrami interfejsu API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a><span data-ttu-id="cdf13-103">Rozpoczynanie pracy z łącznikiem usługi OneDrive hello</span><span class="sxs-lookup"><span data-stu-id="cdf13-103">Get started with hello OneDrive connector</span></span>
<span data-ttu-id="cdf13-104">Łączenie plików, w tym przekazywania, get, Usuń pliki i tooOneDrive toomanage.</span><span class="sxs-lookup"><span data-stu-id="cdf13-104">Connect tooOneDrive toomanage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="cdf13-105">Z usługą OneDrive możesz:</span><span class="sxs-lookup"><span data-stu-id="cdf13-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="cdf13-106">Tworzenie przepływu pracy przez zapisanie plików w usłudze OneDrive lub zaktualizować istniejące pliki w usłudze OneDrive.</span><span class="sxs-lookup"><span data-stu-id="cdf13-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="cdf13-107">Użyj toostart wyzwalaczy przepływu pracy, jeśli plik jest tworzony lub aktualizowany w aplikacji OneDrive.</span><span class="sxs-lookup"><span data-stu-id="cdf13-107">Use triggers toostart your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="cdf13-108">Użyj akcji toocreate pliku, usuń plik i inne.</span><span class="sxs-lookup"><span data-stu-id="cdf13-108">Use actions toocreate a file, delete a file, and more.</span></span> <span data-ttu-id="cdf13-109">Na przykład po odebraniu nowej usługi Office 365 wiadomości e-mail z załącznikiem (wyzwalacz) Utwórz nowy plik w usłudze OneDrive (działanie).</span><span class="sxs-lookup"><span data-stu-id="cdf13-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="cdf13-110">W tym temacie pokazano, jak toouse hello łącznika usługi OneDrive w aplikacji logiki, a także list hello wyzwalacze i akcje.</span><span class="sxs-lookup"><span data-stu-id="cdf13-110">This topic shows you how toouse hello OneDrive connector in a logic app, and also lists hello triggers and actions.</span></span>

<span data-ttu-id="cdf13-111">toolearn więcej informacji na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="cdf13-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooonedrive"></a><span data-ttu-id="cdf13-112">Połącz tooOneDrive</span><span class="sxs-lookup"><span data-stu-id="cdf13-112">Connect tooOneDrive</span></span>
<span data-ttu-id="cdf13-113">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="cdf13-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="cdf13-114">Połączenie stanowi połączenie między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="cdf13-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="cdf13-115">Na przykład tooconnect tooOneDrive, należy najpierw OneDrive *połączenia*.</span><span class="sxs-lookup"><span data-stu-id="cdf13-115">For example, tooconnect tooOneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="cdf13-116">toocreate połączenie, wprowadź poświadczenia hello tooaccess hello usługi, które mają tooconnect do zwykle jest używana.</span><span class="sxs-lookup"><span data-stu-id="cdf13-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="cdf13-117">Tak z usługą OneDrive, wprowadź hello poświadczenia tooyour OneDrive konta toocreate hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="cdf13-117">So, with OneDrive, enter hello credentials tooyour OneDrive account  toocreate hello connection.</span></span>

### <a name="create-hello-connection"></a><span data-ttu-id="cdf13-118">Utwórz połączenie hello</span><span class="sxs-lookup"><span data-stu-id="cdf13-118">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="cdf13-119">Użyć wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="cdf13-119">Use a trigger</span></span>
<span data-ttu-id="cdf13-120">Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="cdf13-120">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="cdf13-121">Wyzwalacze "sondować" hello usługi interwału i częstotliwość.</span><span class="sxs-lookup"><span data-stu-id="cdf13-121">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="cdf13-122">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="cdf13-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="cdf13-123">W aplikacji logiki hello wpisz "onedrive" tooget listę hello wyzwalaczy:</span><span class="sxs-lookup"><span data-stu-id="cdf13-123">In hello logic app, type "onedrive" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="cdf13-124">Wybierz **modyfikacji pliku**.</span><span class="sxs-lookup"><span data-stu-id="cdf13-124">Select **When a file is modified**.</span></span> <span data-ttu-id="cdf13-125">Jeśli połączenie już istnieje, wybierz opcję tooselect przycisk Pokaż selektora hello folderu.</span><span class="sxs-lookup"><span data-stu-id="cdf13-125">If a connection already exists, then select hello Show Picker button tooselect a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="cdf13-126">Jeśli zostanie wyświetlony monit o toosign w, wprowadź znak hello szczegóły toocreate hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="cdf13-126">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="cdf13-127">[Utwórz połączenie hello](connectors-create-api-onedrive.md#create-the-connection) w tym temacie przedstawiono kroki hello.</span><span class="sxs-lookup"><span data-stu-id="cdf13-127">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="cdf13-128">W tym przykładzie aplikacja logiki hello uruchamiane po pliku w folderze hello, wybranych aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="cdf13-128">In this example, hello logic app runs when a file in hello folder you choose is updated.</span></span> <span data-ttu-id="cdf13-129">wyniki hello toosee tego wyzwalacza, Dodaj inną akcję wysyłanej wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="cdf13-129">toosee hello results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="cdf13-130">Na przykład dodać hello Office 365 Outlook *wysłać wiadomość e-mail* akcję, która wysyła pocztą e-mail, należy po zaktualizowaniu pliku.</span><span class="sxs-lookup"><span data-stu-id="cdf13-130">For example, add hello Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="cdf13-131">Wybierz hello **Edytuj** przycisk i ustaw hello **częstotliwość** i **interwał** wartości.</span><span class="sxs-lookup"><span data-stu-id="cdf13-131">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="cdf13-132">Na przykład, jeśli chcesz toopoll wyzwalacza hello co 15 minut, następnie ustawić hello **częstotliwość** za**minutę**i ustaw hello **interwał** zbyt**15**.</span><span class="sxs-lookup"><span data-stu-id="cdf13-132">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="cdf13-133">**Zapisz** zmiany (lewym górnym rogu paska narzędzi hello).</span><span class="sxs-lookup"><span data-stu-id="cdf13-133">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="cdf13-134">Aplikację logiki jest zapisywana i automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="cdf13-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="cdf13-135">Za pomocą akcji</span><span class="sxs-lookup"><span data-stu-id="cdf13-135">Use an action</span></span>
<span data-ttu-id="cdf13-136">Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="cdf13-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="cdf13-137">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="cdf13-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="cdf13-138">Wybierz znak plus hello.</span><span class="sxs-lookup"><span data-stu-id="cdf13-138">Select hello plus sign.</span></span> <span data-ttu-id="cdf13-139">Zobacz kilka opcji: **Dodaj akcję**, **Dodaj warunek**, lub jeden z hello **więcej** opcje.</span><span class="sxs-lookup"><span data-stu-id="cdf13-139">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="cdf13-140">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="cdf13-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="cdf13-141">W polu tekstowym hello wpisz "onedrive" tooget listę wszystkich hello dostępne akcje.</span><span class="sxs-lookup"><span data-stu-id="cdf13-141">In hello text box, type “onedrive” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="cdf13-142">W tym przykładzie wybierz **OneDrive — Utwórz plik**.</span><span class="sxs-lookup"><span data-stu-id="cdf13-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="cdf13-143">Jeśli połączenie już istnieje, a następnie wybierz hello **ścieżka folderu** tooput hello pliku, wprowadź hello **nazwę pliku**i wybierz polecenie hello **zawartość pliku** chcesz:</span><span class="sxs-lookup"><span data-stu-id="cdf13-143">If a connection already exists, then select hello **Folder Path** tooput hello file, enter hello **File Name**, and choose hello **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="cdf13-144">Jeśli zostanie wyświetlony monit o informacje o połączeniu hello, wprowadź hello szczegóły toocreate hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="cdf13-144">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="cdf13-145">[Utwórz połączenie hello](connectors-create-api-onedrive.md#create-the-connection) w tym temacie opisano te właściwości.</span><span class="sxs-lookup"><span data-stu-id="cdf13-145">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="cdf13-146">W tym przykładzie utworzymy nowy plik w folderze OneDrive.</span><span class="sxs-lookup"><span data-stu-id="cdf13-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="cdf13-147">Mogą wykorzystywać dane z innego pliku OneDrive hello toocreate wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="cdf13-147">You can use output from another trigger toocreate hello OneDrive file.</span></span> <span data-ttu-id="cdf13-148">Na przykład dodać hello Office 365 Outlook *po odebraniu nowej wiadomości e-mail* wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="cdf13-148">For example, add hello Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="cdf13-149">Następnie dodaj hello OneDrive *Utwórz plik* akcję, która używa hello załączników i pola typu zawartości w ramach ForEach toocreate hello nowy plik w usłudze OneDrive.</span><span class="sxs-lookup"><span data-stu-id="cdf13-149">Then add hello OneDrive *Create file* action that uses hello Attachments and Content-Type fields within a ForEach toocreate hello new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="cdf13-150">**Zapisz** zmiany (lewym górnym rogu paska narzędzi hello).</span><span class="sxs-lookup"><span data-stu-id="cdf13-150">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="cdf13-151">Aplikację logiki jest zapisywana i automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="cdf13-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="cdf13-152">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="cdf13-152">Connector-specific details</span></span>

<span data-ttu-id="cdf13-153">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="cdf13-153">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="cdf13-154">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="cdf13-154">More connectors</span></span>
<span data-ttu-id="cdf13-155">Przejdź wstecz toohello [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="cdf13-155">Go back toohello [APIs list](apis-list.md).</span></span>
