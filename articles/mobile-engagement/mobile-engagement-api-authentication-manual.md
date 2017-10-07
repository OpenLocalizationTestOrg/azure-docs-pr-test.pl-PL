---
title: "aaaAuthenticate z Mobile Engagement REST API - instalacji ręcznej"
description: "W tym artykule opisano, jak toomanually Instalator uwierzytelniania dla interfejsów API REST, Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="de818-103">Uwierzytelniania w usłudze Mobile Engagement REST API - instalacji ręcznej</span><span class="sxs-lookup"><span data-stu-id="de818-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="de818-104">To jest zbyt dokumentacji dodatku[Uwierzytelnij z interfejsów API REST usługi Engagement Mobile](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="de818-104">This is an appendix documentation too[Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="de818-105">Upewnij się, że odczytu pierwszego tooget hello kontekstu.</span><span class="sxs-lookup"><span data-stu-id="de818-105">Make sure you read it first tooget hello context.</span></span> <span data-ttu-id="de818-106">Opisuje to alternatywny sposób toodo hello jednorazowej konfiguracji konfigurowania uwierzytelniania przy użyciu interfejsów API REST usługi Engagement Mobile hello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="de818-106">This describes an alternate way toodo hello One-time setup for setting up your authentication for hello Mobile Engagement REST APIs using hello Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="de818-107">Poniższe instrukcje Hello są oparte na tym [przewodnik usługi Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) i dostosowywać do co to jest wymagany do uwierzytelniania dla mobilnych interfejsów API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="de818-107">hello instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="de818-108">Aby zapoznać tooit, jeśli chcesz, aby toounderstand hello poniższe kroki szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="de818-108">So refer tooit if you want toounderstand hello steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="de818-109">Tooyour logowania konta Azure za pośrednictwem hello [klasyczny portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="de818-109">Login tooyour Azure Account through hello [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="de818-110">Wybierz **usługi Active Directory** w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="de818-110">Select **Active Directory** from hello left pane.</span></span>
   
     ![Wybierz usługi Active Directory][1]
3. <span data-ttu-id="de818-112">Wybierz hello **domyślne usługi Active Directory** w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="de818-112">Choose hello **Default Active Directory** in your Azure portal.</span></span> 
   
     ![Wybierz katalog][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="de818-114">Ta metoda działa tylko wtedy, gdy pracujesz w domyślnej hello usługi Active Directory dla konta i nie będzie działać, jeśli robią to w usłudze Active Directory utworzonego w ramach Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="de818-114">This approach works only when you are working in hello default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="de818-115">tooview aplikacji hello w katalogu, kliknij na **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="de818-115">tooview hello applications in your directory, click on **Applications**.</span></span>
   
     ![Wyświetl aplikacje][3]
5. <span data-ttu-id="de818-117">Polecenie **dodać**.</span><span class="sxs-lookup"><span data-stu-id="de818-117">Click on **ADD**.</span></span> 
   
     ![Dodawanie aplikacji][4]
6. <span data-ttu-id="de818-119">Polecenie **Dodaj aplikację moją organizację**</span><span class="sxs-lookup"><span data-stu-id="de818-119">Click on **Add an application my organization is developing**</span></span>
   
     ![Nowa aplikacja][5]
7. <span data-ttu-id="de818-121">Wprowadź nazwę aplikacji hello i hello wybierz typ aplikacji jako **interfejsu API sieci WEB i/lub aplikacji sieci WEB** i kliknij przycisk Dalej hello.</span><span class="sxs-lookup"><span data-stu-id="de818-121">Fill in name of hello application and select hello type of application as **WEB APPLICATION AND/OR WEB API** and click hello next button.</span></span>
   
     ![Nazwa aplikacji][6]
8. <span data-ttu-id="de818-123">Możesz podać wszelkie fikcyjny adresy URL dla **adres URL logowania** i **identyfikator URI aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="de818-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="de818-124">Nie są one używane do naszego scenariusza i adresy URL hello, same nie są weryfikowane.</span><span class="sxs-lookup"><span data-stu-id="de818-124">They are not used for our scenario and hello URLs themselves are not validated.</span></span>  
   
     ![Właściwości aplikacji][7]
9. <span data-ttu-id="de818-126">Na końcu hello tego będziesz mieć aplikację AAD o nazwie hello, podane wcześniej podobnie następującej hello.</span><span class="sxs-lookup"><span data-stu-id="de818-126">At hello end of this, you will have an AAD app with hello name you provided previously like hello following.</span></span> <span data-ttu-id="de818-127">Jest to Twoje **AD\_aplikacji\_nazwa** i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="de818-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![Nazwa aplikacji][8]
10. <span data-ttu-id="de818-129">Kliknij nazwę aplikacji hello i wybierz polecenie **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="de818-129">Click on hello app name and click on **Configure**.</span></span>
    
      ![Konfigurowanie aplikacji][9]
11. <span data-ttu-id="de818-131">Zanotuj hello Identyfikatora klienta, która będzie służyć jako **klienta\_identyfikator** do interfejsu API wywołania.</span><span class="sxs-lookup"><span data-stu-id="de818-131">Make a note of hello CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![Konfigurowanie aplikacji][10]
12. <span data-ttu-id="de818-133">Przewiń w dół toohello **klucze** i Dodaj klucz o najlepiej czas trwania 2 lata (wygaśnięcia) i kliknij pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="de818-133">Scroll down toohello **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![Konfigurowanie aplikacji][11]
13. <span data-ttu-id="de818-135">Skopiuj natychmiast hello wartość, która jest wyświetlana dla klucza hello jest wyświetlana tylko teraz, a nie są przechowywane, więc nie zostanie nigdy ponownie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="de818-135">Immediately copy hello value which is shown for hello key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="de818-136">W przypadku utraty następnie konieczne będzie toogenerate nowy klucz.</span><span class="sxs-lookup"><span data-stu-id="de818-136">If you lose it then you will have toogenerate a new key.</span></span> <span data-ttu-id="de818-137">Są to hello **CLIENT_SECRET** do interfejsu API wywołania.</span><span class="sxs-lookup"><span data-stu-id="de818-137">This will be hello **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![Konfigurowanie aplikacji][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="de818-139">Ten klucz wygaśnie o hello końca czasu trwania hello określenia tak toorenew się upewnij, który go, gdy czas hello w przeciwnym razie uwierzytelnianie interfejsu API nie będzie już działać.</span><span class="sxs-lookup"><span data-stu-id="de818-139">This key will expire at hello end of hello duration that you specified so make sure toorenew it when hello time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="de818-140">Można również usunąć i ponownie utwórz ten klucz, jeśli uważasz, że został złamany.</span><span class="sxs-lookup"><span data-stu-id="de818-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="de818-141">Polecenie **WYŚWIETL punkty końcowe** przycisk teraz który spowoduje to otwarcie hello **punkty końcowe aplikacji** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="de818-141">Click on **VIEW ENDPOINTS** button now which will open up hello **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="de818-142">Okno dialogowe punkty końcowe aplikacji hello, skopiuj hello **KOŃCOWYM TOKENÓW OAUTH 2.0**.</span><span class="sxs-lookup"><span data-stu-id="de818-142">From hello App Endpoints dialog box, copy hello **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="de818-143">Ten punkt końcowy będzie powitania po formularza, gdzie jest hello identyfikatora GUID w adresie URL hello Twojej **TENANT_ID** tak zanotuj go:</span><span class="sxs-lookup"><span data-stu-id="de818-143">This endpoint will be in hello following form where hello GUID in hello URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="de818-144">Obecnie firma Microsoft będzie kontynuowana tooconfigure hello uprawnienia do tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de818-144">Now we will proceed tooconfigure hello permissions on this app.</span></span> <span data-ttu-id="de818-145">Dla tego trzeba będzie tooopen się hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de818-145">For this you will have tooopen up hello [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="de818-146">Polecenie **grup zasobów** i Znajdź hello **Mobile Engagement** grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="de818-146">Click on **Resource Groups** and find hello **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="de818-147">Kliknij przycisk hello **Mobile Engagement** zasobów grupy i przejdź toohello **ustawienia** bloku, w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="de818-147">Click hello **Mobile Engagement** resource group and navigate toohello **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="de818-148">Polecenie **użytkowników** w hello bloku ustawienia, a następnie kliknij polecenie **Dodaj** tooadd użytkownika.</span><span class="sxs-lookup"><span data-stu-id="de818-148">Click on **Users** in hello Settings blade and then click on **Add** tooadd a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="de818-149">Polecenie **wybierz rolę**</span><span class="sxs-lookup"><span data-stu-id="de818-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="de818-150">Polecenie **właściciela**</span><span class="sxs-lookup"><span data-stu-id="de818-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="de818-151">Wyszukaj nazwę aplikacji hello **AD\_aplikacji\_nazwa** hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="de818-151">Search for hello name of your application **AD\_APP\_NAME** in hello Search box.</span></span> <span data-ttu-id="de818-152">Domyślnie w tym miejscu nie będą widzieć to.</span><span class="sxs-lookup"><span data-stu-id="de818-152">You will not see this by default here.</span></span> <span data-ttu-id="de818-153">Po znalezieniu go, zaznacz go i kliknij na **wybierz** u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="de818-153">Once you find it, select it and click on **Select** at hello bottom of hello blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="de818-154">Na powitania **dostępu Dodaj** bloku, zostanie wyświetlona jako **użytkownika 1, 0 grupy**.</span><span class="sxs-lookup"><span data-stu-id="de818-154">On hello **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="de818-155">Kliknij przycisk **OK** na temat tej zmiany hello tooconfirm bloku.</span><span class="sxs-lookup"><span data-stu-id="de818-155">Click **OK** on this blade tooconfirm hello change.</span></span> 
    
    ![][21]

<span data-ttu-id="de818-156">Ukończono hello wymaganych konfiguracji usługi AAD i są wszystkie hello toocall zestaw interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="de818-156">You have now completed hello required AAD configuration and you are all set toocall hello APIs.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



