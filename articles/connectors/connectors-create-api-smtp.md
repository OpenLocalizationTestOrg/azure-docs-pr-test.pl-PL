---
title: "Łącznik aaaSMTP w programie Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Połącz tooSMTP toosend w wiadomości e-mail."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a><span data-ttu-id="9aeae-104">Rozpoczynanie pracy z hello SMTP łącznika</span><span class="sxs-lookup"><span data-stu-id="9aeae-104">Get started with hello SMTP connector</span></span>
<span data-ttu-id="9aeae-105">Połącz tooSMTP toosend w wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="9aeae-105">Connect tooSMTP toosend email.</span></span>

<span data-ttu-id="9aeae-106">toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="9aeae-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="9aeae-107">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9aeae-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosmtp"></a><span data-ttu-id="9aeae-108">Połącz tooSMTP</span><span class="sxs-lookup"><span data-stu-id="9aeae-108">Connect tooSMTP</span></span>
<span data-ttu-id="9aeae-109">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate *połączenia* toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="9aeae-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="9aeae-110">A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="9aeae-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="9aeae-111">Na przykład tooconnect tooSMTP, należy najpierw SMTP *połączenia*.</span><span class="sxs-lookup"><span data-stu-id="9aeae-111">For example, tooconnect tooSMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="9aeae-112">toocreate połączenie, wprowadź poświadczenia hello tooaccess hello usługi, gdy połączysz się zwykle jest używana.</span><span class="sxs-lookup"><span data-stu-id="9aeae-112">toocreate a connection, enter hello credentials you normally use tooaccess hello service you connect to.</span></span> <span data-ttu-id="9aeae-113">Tak w przykładzie hello SMTP, wprowadź nazwę połączenia tooyour poświadczenia hello, adresu serwera SMTP i użytkownika logowania informacji toocreate hello połączenia tooSMTP.</span><span class="sxs-lookup"><span data-stu-id="9aeae-113">So, in hello SMTP example, enter hello credentials tooyour connection name, SMTP server address, and user login information toocreate hello connection tooSMTP.</span></span>  

### <a name="create-a-connection-toosmtp"></a><span data-ttu-id="9aeae-114">Tworzenie tooSMTP połączenia</span><span class="sxs-lookup"><span data-stu-id="9aeae-114">Create a connection tooSMTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="9aeae-115">Użyj wyzwalacz SMTP</span><span class="sxs-lookup"><span data-stu-id="9aeae-115">Use an SMTP trigger</span></span>
<span data-ttu-id="9aeae-116">Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="9aeae-116">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="9aeae-117">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9aeae-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="9aeae-118">W tym przykładzie, ponieważ SMTP nie ma wyzwalacz własnych, użyjemy hello **Salesforce — po utworzeniu obiektu** wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="9aeae-118">In this example, because SMTP does not have a trigger of its own, we'll use hello **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="9aeae-119">Wyzwalacz aktywuje po utworzeniu nowego obiektu w usłudze Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9aeae-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="9aeae-120">W naszym przykładzie skonfigurujemy Twoje go tak, aby zawsze nowego potencjalnego klienta jest tworzony w Salesforce, *wysyłania wiadomości e-mail* akcja jest wykonywana za pośrednictwem łącznika hello SMTP z powiadomienie z informacją o hello realizacji nowego tworzona.</span><span class="sxs-lookup"><span data-stu-id="9aeae-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via hello SMTP connector with a notification of hello new lead being created.</span></span>

1. <span data-ttu-id="9aeae-121">Wprowadź *salesforce* w polu wyszukiwania hello hello logiki aplikacji designer wybierz hello **Salesforce — po utworzeniu obiektu** wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="9aeae-121">Enter *salesforce* in hello search box on hello logic apps designer then select hello **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="9aeae-122">Witaj **podczas tworzenia obiektu** formant jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="9aeae-122">hello **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="9aeae-123">Wybierz hello **typ obiektu** następnie wybierz *prowadzić* z listy hello obiektów.</span><span class="sxs-lookup"><span data-stu-id="9aeae-123">Select hello **Object Type** then select *Lead* from hello list of objects.</span></span> <span data-ttu-id="9aeae-124">W tym kroku wskazujesz, tworzysz wyzwalacz, który powiadomi aplikację logiki, zawsze, gdy nowy realizacji jest tworzony w usłudze Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9aeae-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="9aeae-125">Witaj wyzwalacz został utworzony.</span><span class="sxs-lookup"><span data-stu-id="9aeae-125">hello trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="9aeae-126">Za pomocą akcji SMTP</span><span class="sxs-lookup"><span data-stu-id="9aeae-126">Use an SMTP action</span></span>
<span data-ttu-id="9aeae-127">Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="9aeae-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="9aeae-128">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9aeae-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="9aeae-129">Teraz, gdy hello wyzwalacz został dodany, wykonaj te kroki akcję tooadd serwera SMTP, która zostanie przeprowadzona po utworzeniu nowego potencjalnego klienta w usłudze Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9aeae-129">Now that hello trigger has been added, follow these steps tooadd an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="9aeae-130">Wybierz **+ nowy krok** akcji hello tooadd chcesz tootake po utworzeniu nowego potencjalnego klienta.</span><span class="sxs-lookup"><span data-stu-id="9aeae-130">Select **+ New Step** tooadd hello action you would like tootake when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="9aeae-131">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="9aeae-131">Select **Add an action**.</span></span> <span data-ttu-id="9aeae-132">To pole wyszukiwania hello otwiera gdzie możesz wyszukać dowolną akcję należy chcieliby tootake.</span><span class="sxs-lookup"><span data-stu-id="9aeae-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="9aeae-133">Wprowadź *smtp* toosearch dla tooSMTP powiązanych działań.</span><span class="sxs-lookup"><span data-stu-id="9aeae-133">Enter *smtp* toosearch for actions related tooSMTP.</span></span>  
4. <span data-ttu-id="9aeae-134">Wybierz **SMTP — Wyślij wiadomość E-mail** jako hello tootake akcji po utworzeniu nowego potencjalnego klienta hello.</span><span class="sxs-lookup"><span data-stu-id="9aeae-134">Select **SMTP - Send Email** as hello action tootake when hello new lead is created.</span></span> <span data-ttu-id="9aeae-135">zostanie otwarty blok kontroli Hello akcji.</span><span class="sxs-lookup"><span data-stu-id="9aeae-135">hello action control block opens.</span></span> <span data-ttu-id="9aeae-136">Konieczne będzie tooestablish połączenia smtp w bloku projektanta hello Jeśli nie zostało zrobione to wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9aeae-136">You will have tooestablish your smtp connection in hello designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="9aeae-137">Wprowadzania informacji żądaną poczty e-mail w programie hello **SMTP — Wyślij wiadomość E-mail** bloku.</span><span class="sxs-lookup"><span data-stu-id="9aeae-137">Input your desired email information in hello **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="9aeae-138">Zapisz swoją pracę w kolejności tooactivate przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="9aeae-138">Save your work in order tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="9aeae-139">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="9aeae-139">Connector-specific details</span></span>

<span data-ttu-id="9aeae-140">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="9aeae-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="9aeae-141">Więcej łączników</span><span class="sxs-lookup"><span data-stu-id="9aeae-141">More connectors</span></span>
<span data-ttu-id="9aeae-142">Przejdź wstecz toohello [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="9aeae-142">Go back toohello [APIs list](apis-list.md).</span></span>
