---
title: "aaaLearn jak toouse hello łącznik Twitter w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Omówienie łącznik Twitter z parametrami interfejsu API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a><span data-ttu-id="b5a14-103">Rozpoczynanie pracy z powitania łącznik Twitter</span><span class="sxs-lookup"><span data-stu-id="b5a14-103">Get started with hello Twitter connector</span></span>
<span data-ttu-id="b5a14-104">Łącznik Twitter hello można:</span><span class="sxs-lookup"><span data-stu-id="b5a14-104">With hello Twitter connector you can:</span></span>

* <span data-ttu-id="b5a14-105">Publikowanie tweetów i tweetów get</span><span class="sxs-lookup"><span data-stu-id="b5a14-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="b5a14-106">Dostęp do osi czasu, znajomych i adherentami</span><span class="sxs-lookup"><span data-stu-id="b5a14-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="b5a14-107">Wykonaj jedną z hello w innych działań i wyzwalaczy opisanych poniżej</span><span class="sxs-lookup"><span data-stu-id="b5a14-107">Perform any of hello other actions and triggers described below</span></span>  

<span data-ttu-id="b5a14-108">toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b5a14-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="b5a14-109">Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b5a14-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-tootwitter"></a><span data-ttu-id="b5a14-110">Połącz tooTwitter</span><span class="sxs-lookup"><span data-stu-id="b5a14-110">Connect tooTwitter</span></span>
<span data-ttu-id="b5a14-111">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate *połączenia* toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="b5a14-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="b5a14-112">A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="b5a14-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tootwitter"></a><span data-ttu-id="b5a14-113">Tworzenie tooTwitter połączenia</span><span class="sxs-lookup"><span data-stu-id="b5a14-113">Create a connection tooTwitter</span></span>
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="b5a14-114">Użyj wyzwalacz Twitter</span><span class="sxs-lookup"><span data-stu-id="b5a14-114">Use a Twitter trigger</span></span>
<span data-ttu-id="b5a14-115">Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="b5a14-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="b5a14-116">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b5a14-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="b5a14-117">W tym przykładzie I przedstawia sposób toouse hello **po jest przesyłana z nowego tweet** wyzwolić toosearch dla #Seattle i, w przypadku znalezienia #Seattle zaktualizowany plik w Dropbox z tekstem hello hello tweet.</span><span class="sxs-lookup"><span data-stu-id="b5a14-117">In this example, I will show you how toouse hello **When a new tweet is posted**  trigger toosearch for #Seattle and, if #Seattle is found, update a file in Dropbox with hello text from hello tweet.</span></span> <span data-ttu-id="b5a14-118">W przykładzie przedsiębiorstwa można wyszukać hello nazwę swojej firmy i zaktualizować bazę danych SQL z tekstem hello hello tweet.</span><span class="sxs-lookup"><span data-stu-id="b5a14-118">In an enterprise example, you could search for hello name of your company and update a SQL database with hello text from hello tweet.</span></span>

1. <span data-ttu-id="b5a14-119">Wprowadź *twitter* w polu wyszukiwania hello hello logiki aplikacji designer wybierz hello **Twitter — gdy nowy tweet jest przesyłana** wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="b5a14-119">Enter *twitter* in hello search box on hello logic apps designer then select hello **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="b5a14-120">![Obraz wyzwalacza Twitter 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="b5a14-121">Wprowadź *#Seattle* w hello **tekst do wyszukania** formantu</span><span class="sxs-lookup"><span data-stu-id="b5a14-121">Enter *#Seattle* in hello **Search Text** control</span></span>  
   <span data-ttu-id="b5a14-122">![Wyzwalacz Twitter — obraz 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="b5a14-123">W tym momencie aplikację logiki została skonfigurowana z wyzwalaczy, które rozpocznie Uruchom hello innych wyzwalacze i akcje w przepływie pracy hello.</span><span class="sxs-lookup"><span data-stu-id="b5a14-123">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="b5a14-124">Dla logiki aplikacji toobe funkcjonalności musi ona zawierać przynajmniej jeden wyzwalacz i jedną akcję.</span><span class="sxs-lookup"><span data-stu-id="b5a14-124">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="b5a14-125">Wykonaj kroki hello hello następnej sekcji tooadd akcji.</span><span class="sxs-lookup"><span data-stu-id="b5a14-125">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="b5a14-126">Dodaj warunek</span><span class="sxs-lookup"><span data-stu-id="b5a14-126">Add a condition</span></span>
<span data-ttu-id="b5a14-127">Ponieważ tylko Dbamy o tweetów od użytkowników więcej niż 50 użytkowników, warunek, który potwierdza hello liczba adherentami najpierw należy dodać toohello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b5a14-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms hello number of followers must first be added toohello logic app.</span></span>  

1. <span data-ttu-id="b5a14-128">Wybierz **+ nowy krok** akcji hello tooadd chcesz tootake po znalezieniu #Seattle w nowej tweet</span><span class="sxs-lookup"><span data-stu-id="b5a14-128">Select **+ New step** tooadd hello action you would like tootake when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="b5a14-129">![Obraz akcji Twitter 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="b5a14-130">Wybierz hello **Dodaj warunek** łącza.</span><span class="sxs-lookup"><span data-stu-id="b5a14-130">Select hello **Add a condition** link.</span></span>  
   <span data-ttu-id="b5a14-131">![Obraz warunku Twitter 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="b5a14-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="b5a14-132">Spowoduje to otwarcie hello **warunku** kontrolki, w którym można sprawdzić warunków takich jak *jest równa*, *jest mniejsza niż*, *jest większa niż*, *zawiera*itp.</span><span class="sxs-lookup"><span data-stu-id="b5a14-132">This opens hello **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="b5a14-133">![Warunek Twitter — obraz 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="b5a14-134">Wybierz hello **wybierz wartość** formantu.</span><span class="sxs-lookup"><span data-stu-id="b5a14-134">Select hello **Choose a value** control.</span></span>  
   <span data-ttu-id="b5a14-135">W tym formancie można wybrać jedną lub więcej właściwości hello z poprzedniej akcji lub wyzwalaczy jako wartość hello którego warunku będzie oceniana tootrue lub false.</span><span class="sxs-lookup"><span data-stu-id="b5a14-135">In this control, you can select one or more of hello properties from any previous actions or triggers as hello value whose condition will be evaluated tootrue or false.</span></span>
   <span data-ttu-id="b5a14-136">![Obraz warunku Twitter 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="b5a14-137">Wybierz hello **...**  tooexpand hello listę właściwości, dzięki czemu wszystkie właściwości hello, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b5a14-137">Select hello **...** tooexpand hello list of properties so you can see all hello properties that are available.</span></span>        
   <span data-ttu-id="b5a14-138">![Stan obrazu 4 w usłudze Twitter](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="b5a14-139">Wybierz hello **liczba adherentami** właściwości.</span><span class="sxs-lookup"><span data-stu-id="b5a14-139">Select hello **Followers count** property.</span></span>    
   <span data-ttu-id="b5a14-140">![Obraz warunku Twitter 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="b5a14-141">Zwróć uwagę, adherentami hello właściwość count jest teraz hello wartość formantu.</span><span class="sxs-lookup"><span data-stu-id="b5a14-141">Notice hello Followers count property is now in hello value control.</span></span>    
   ![Stan obrazu 6 w usłudze Twitter](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="b5a14-143">Wybierz **jest większa niż** z listy operatory hello.</span><span class="sxs-lookup"><span data-stu-id="b5a14-143">Select **is greater than** from hello operators list.</span></span>    
   <span data-ttu-id="b5a14-144">![Stan obrazu 7 w usłudze Twitter](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="b5a14-145">Wprowadź 50 jako argument hello hello *jest większa niż* operatora.</span><span class="sxs-lookup"><span data-stu-id="b5a14-145">Enter 50 as hello operand for hello *is greater than* operator.</span></span>  
   <span data-ttu-id="b5a14-146">dodawany jest Hello warunku.</span><span class="sxs-lookup"><span data-stu-id="b5a14-146">hello condition is now added.</span></span> <span data-ttu-id="b5a14-147">Zapisz swoją pracę przy użyciu hello **zapisać** łącze menu hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="b5a14-147">Save your work using hello **Save** link on hello menu above.</span></span>    
   <span data-ttu-id="b5a14-148">![Stan obrazu 8 w usłudze Twitter](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="b5a14-149">Za pomocą akcji usługi Twitter</span><span class="sxs-lookup"><span data-stu-id="b5a14-149">Use a Twitter action</span></span>
<span data-ttu-id="b5a14-150">Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="b5a14-150">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="b5a14-151">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b5a14-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="b5a14-152">Teraz, wyzwalacz został dodany, wykonaj te kroki tooadd akcję, która zostanie wysłany nowy tweet zawartością hello tweetów hello znalezione przez wyzwalacz hello.</span><span class="sxs-lookup"><span data-stu-id="b5a14-152">Now that you have added a trigger, follow these steps tooadd an action that will post a new tweet with hello contents of hello tweets found by hello trigger.</span></span> <span data-ttu-id="b5a14-153">Na potrzeby tego przewodnika hello tylko tweetów od użytkowników więcej niż 50 adherentami zostaną opublikowane.</span><span class="sxs-lookup"><span data-stu-id="b5a14-153">For hello purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="b5a14-154">W następnym kroku hello doda akcji Twitter, który zostanie wysłany tweet niektórych właściwości hello każdego tweet, która została opublikowana przez użytkownika, który ma więcej niż 50 adherentami.</span><span class="sxs-lookup"><span data-stu-id="b5a14-154">In hello next step, you will add a Twitter action that will post a tweet using some of hello properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="b5a14-155">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="b5a14-155">Select **Add an action**.</span></span> <span data-ttu-id="b5a14-156">Spowoduje to otwarcie hello formantu wyszukiwania, których można wyszukiwać innych działań i wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="b5a14-156">This opens hello search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="b5a14-157">![Obraz warunku Twitter 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="b5a14-158">Wprowadź *twitter* do pola wyszukiwania hello wybiorą hello **Twitter — Opublikuj tweet** akcji.</span><span class="sxs-lookup"><span data-stu-id="b5a14-158">Enter *twitter* into hello search box then select hello **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="b5a14-159">Spowoduje to otwarcie hello **Opublikuj tweet** kontroli, gdy zostanie wprowadź wszystkie szczegóły tweet hello ogłaszany.</span><span class="sxs-lookup"><span data-stu-id="b5a14-159">This opens hello **Post a tweet** control where you will enter all details for hello tweet being posted.</span></span>      
   <span data-ttu-id="b5a14-160">![Obraz akcji 1 do 5 w usłudze Twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="b5a14-161">Wybierz hello **Tweetować tekst** formantu.</span><span class="sxs-lookup"><span data-stu-id="b5a14-161">Select hello **Tweet text** control.</span></span> <span data-ttu-id="b5a14-162">Wszystkie dane wyjściowe z poprzedniego działania i jest wyzwalane w aplikacji logiki hello są teraz widoczne.</span><span class="sxs-lookup"><span data-stu-id="b5a14-162">All outputs from previous actions and triggers in hello logic app are now visible.</span></span> <span data-ttu-id="b5a14-163">Można wybrać dowolny z tych i używać ich jako część hello tweet tekst hello tweet nowe.</span><span class="sxs-lookup"><span data-stu-id="b5a14-163">You can select any of these and use them as part of hello tweet text of hello new tweet.</span></span>     
   <span data-ttu-id="b5a14-164">![Obraz akcji Twitter 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="b5a14-165">Wybierz **nazwy użytkownika**</span><span class="sxs-lookup"><span data-stu-id="b5a14-165">Select **User name**</span></span>   
5. <span data-ttu-id="b5a14-166">Wprowadź *mówi:* hello tweet tekst formantu.</span><span class="sxs-lookup"><span data-stu-id="b5a14-166">Enter *says:* in hello tweet text control.</span></span> <span data-ttu-id="b5a14-167">W tym zaraz po nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b5a14-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="b5a14-168">Wybierz *Tweetować tekstu*.</span><span class="sxs-lookup"><span data-stu-id="b5a14-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="b5a14-169">![Obraz akcji Twitter 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="b5a14-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="b5a14-170">Zapisz swoją pracę i publikowała tweet przy tooactivate hasztagiem hello #Seattle przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="b5a14-170">Save your work and send a tweet with hello #Seattle hashtag tooactivate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="b5a14-171">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="b5a14-171">Connector-specific details</span></span>

<span data-ttu-id="b5a14-172">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="b5a14-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b5a14-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b5a14-173">Next steps</span></span>
[<span data-ttu-id="b5a14-174">Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="b5a14-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

