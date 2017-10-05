---
title: "Uwierzytelniania w usłudze Mobile Engagement REST API - instalacji ręcznej"
description: "Opisuje, jak ręcznie skonfigurować uwierzytelnianie dla interfejsów API REST usługi Engagement Mobile"
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
ms.openlocfilehash: 9d6132e1a01be489b8e8e28a0219cf8a0b50b318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="96d0c-103">Uwierzytelniania w usłudze Mobile Engagement REST API - instalacji ręcznej</span><span class="sxs-lookup"><span data-stu-id="96d0c-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="96d0c-104">To jest dokumentacji dodatku do [Uwierzytelnij z interfejsów API REST usługi Engagement Mobile](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="96d0c-104">This is an appendix documentation to [Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="96d0c-105">Upewnij się, że jej najpierw uzyskać kontekst odczytu.</span><span class="sxs-lookup"><span data-stu-id="96d0c-105">Make sure you read it first to get the context.</span></span> <span data-ttu-id="96d0c-106">Opisuje alternatywny sposób celu jednorazowej konfiguracji dotyczące konfigurowania uwierzytelniania dla mobilnych interfejsów API REST usługi Engagement przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="96d0c-106">This describes an alternate way to do the One-time setup for setting up your authentication for the Mobile Engagement REST APIs using the Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="96d0c-107">Poniższe instrukcje są oparte na tym [przewodnik usługi Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) i dostosowywać do co to jest wymagany do uwierzytelniania dla mobilnych interfejsów API usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="96d0c-107">The instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="96d0c-108">Aby zapoznać się go, jeśli chcesz zrozumieć poniższe kroki szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="96d0c-108">So refer to it if you want to understand the steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="96d0c-109">Zaloguj się do konta platformy Azure za pośrednictwem [klasyczny portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="96d0c-109">Login to your Azure Account through the [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="96d0c-110">Wybierz **usługi Active Directory** w lewym okienku.</span><span class="sxs-lookup"><span data-stu-id="96d0c-110">Select **Active Directory** from the left pane.</span></span>
   
     ![Wybierz usługi Active Directory][1]
3. <span data-ttu-id="96d0c-112">Wybierz **domyślne usługi Active Directory** w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="96d0c-112">Choose the **Default Active Directory** in your Azure portal.</span></span> 
   
     ![Wybierz katalog][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="96d0c-114">Ta metoda działa tylko wtedy, gdy pracujesz w domyślnej usługi Active Directory dla konta i nie będzie działać, jeśli robią to w usłudze Active Directory utworzonego w ramach Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="96d0c-114">This approach works only when you are working in the default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="96d0c-115">Aby wyświetlić aplikacje w katalogu, kliknij **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="96d0c-115">To view the applications in your directory, click on **Applications**.</span></span>
   
     ![Wyświetl aplikacje][3]
5. <span data-ttu-id="96d0c-117">Polecenie **dodać**.</span><span class="sxs-lookup"><span data-stu-id="96d0c-117">Click on **ADD**.</span></span> 
   
     ![Dodawanie aplikacji][4]
6. <span data-ttu-id="96d0c-119">Polecenie **Dodaj aplikację moją organizację**</span><span class="sxs-lookup"><span data-stu-id="96d0c-119">Click on **Add an application my organization is developing**</span></span>
   
     ![Nowa aplikacja][5]
7. <span data-ttu-id="96d0c-121">Wprowadź nazwę aplikacji i wybierz typ aplikacji jako **interfejsu API sieci WEB i/lub aplikacji sieci WEB** i kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="96d0c-121">Fill in name of the application and select the type of application as **WEB APPLICATION AND/OR WEB API** and click the next button.</span></span>
   
     ![Nazwa aplikacji][6]
8. <span data-ttu-id="96d0c-123">Możesz podać wszelkie fikcyjny adresy URL dla **adres URL logowania** i **identyfikator URI aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="96d0c-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="96d0c-124">Nie są one używane do naszego scenariusza i same adresy URL nie są weryfikowane.</span><span class="sxs-lookup"><span data-stu-id="96d0c-124">They are not used for our scenario and the URLs themselves are not validated.</span></span>  
   
     ![Właściwości aplikacji][7]
9. <span data-ttu-id="96d0c-126">Na końcu tego będziesz mieć aplikację AAD o nazwie podane wcześniej podobnie do poniższego.</span><span class="sxs-lookup"><span data-stu-id="96d0c-126">At the end of this, you will have an AAD app with the name you provided previously like the following.</span></span> <span data-ttu-id="96d0c-127">Jest to Twoje **AD\_aplikacji\_nazwa** i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="96d0c-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![Nazwa aplikacji][8]
10. <span data-ttu-id="96d0c-129">Kliknij nazwę aplikacji i wybierz polecenie **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="96d0c-129">Click on the app name and click on **Configure**.</span></span>
    
      ![Konfigurowanie aplikacji][9]
11. <span data-ttu-id="96d0c-131">Zanotuj identyfikator klienta, która będzie służyć jako **klienta\_identyfikator** do interfejsu API wywołania.</span><span class="sxs-lookup"><span data-stu-id="96d0c-131">Make a note of the CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![Konfigurowanie aplikacji][10]
12. <span data-ttu-id="96d0c-133">Przewiń w dół do **klucze** i Dodaj klucz o najlepiej czas trwania 2 lata (wygaśnięcia) i kliknij pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="96d0c-133">Scroll down to the **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![Konfigurowanie aplikacji][11]
13. <span data-ttu-id="96d0c-135">Natychmiast skopiować wartość, która jest wyświetlana dla klucza jest wyświetlana tylko teraz, a nie są przechowywane, więc nie zostanie nigdy ponownie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="96d0c-135">Immediately copy the value which is shown for the key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="96d0c-136">W przypadku utraty następnie konieczne będzie wygenerowanie nowego klucza.</span><span class="sxs-lookup"><span data-stu-id="96d0c-136">If you lose it then you will have to generate a new key.</span></span> <span data-ttu-id="96d0c-137">Są to **CLIENT_SECRET** do interfejsu API wywołania.</span><span class="sxs-lookup"><span data-stu-id="96d0c-137">This will be the **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![Konfigurowanie aplikacji][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="96d0c-139">Ten klucz wygaśnie z końcem okresu czasu trwania, które określone, upewnij się, że Odnów go w czasie w przeciwnym razie uwierzytelnianie interfejsu API nie będzie już działać.</span><span class="sxs-lookup"><span data-stu-id="96d0c-139">This key will expire at the end of the duration that you specified so make sure to renew it when the time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="96d0c-140">Można również usunąć i ponownie utwórz ten klucz, jeśli uważasz, że został złamany.</span><span class="sxs-lookup"><span data-stu-id="96d0c-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="96d0c-141">Polecenie **WYŚWIETL punkty końcowe** przycisk teraz który spowoduje to otwarcie **punkty końcowe aplikacji** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="96d0c-141">Click on **VIEW ENDPOINTS** button now which will open up the **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="96d0c-142">W oknie dialogowym punkty końcowe aplikacji skopiuj **KOŃCOWYM TOKENÓW OAUTH 2.0**.</span><span class="sxs-lookup"><span data-stu-id="96d0c-142">From the App Endpoints dialog box, copy the **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="96d0c-143">Ten punkt końcowy będzie w następującym formacie, gdzie jest identyfikator GUID w adresie URL Twojego **TENANT_ID** tak zanotuj go:</span><span class="sxs-lookup"><span data-stu-id="96d0c-143">This endpoint will be in the following form where the GUID in the URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="96d0c-144">Teraz możemy będzie kontynuowana, aby skonfigurować uprawnienia w tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96d0c-144">Now we will proceed to configure the permissions on this app.</span></span> <span data-ttu-id="96d0c-145">W tym konieczne będzie otwarcie [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="96d0c-145">For this you will have to open up the [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="96d0c-146">Polecenie **grup zasobów** i Znajdź **Mobile Engagement** grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="96d0c-146">Click on **Resource Groups** and find the **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="96d0c-147">Kliknij przycisk **Mobile Engagement** zasobów grupy i przejdź do **ustawienia** bloku, w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="96d0c-147">Click the **Mobile Engagement** resource group and navigate to the **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="96d0c-148">Polecenie **użytkowników** w bloku ustawienia i kliknij **Dodaj** Aby dodać użytkownika.</span><span class="sxs-lookup"><span data-stu-id="96d0c-148">Click on **Users** in the Settings blade and then click on **Add** to add a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="96d0c-149">Polecenie **wybierz rolę**</span><span class="sxs-lookup"><span data-stu-id="96d0c-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="96d0c-150">Polecenie **właściciela**</span><span class="sxs-lookup"><span data-stu-id="96d0c-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="96d0c-151">Wyszukaj nazwę aplikacji **AD\_aplikacji\_nazwa** w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="96d0c-151">Search for the name of your application **AD\_APP\_NAME** in the Search box.</span></span> <span data-ttu-id="96d0c-152">Domyślnie w tym miejscu nie będą widzieć to.</span><span class="sxs-lookup"><span data-stu-id="96d0c-152">You will not see this by default here.</span></span> <span data-ttu-id="96d0c-153">Po znalezieniu go, zaznacz go i kliknij na **wybierz** w dolnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="96d0c-153">Once you find it, select it and click on **Select** at the bottom of the blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="96d0c-154">Na **dostępu Dodaj** bloku, zostanie wyświetlona jako **użytkownika 1, 0 grupy**.</span><span class="sxs-lookup"><span data-stu-id="96d0c-154">On the **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="96d0c-155">Kliknij przycisk **OK** w tym bloku, aby potwierdzić zmianę.</span><span class="sxs-lookup"><span data-stu-id="96d0c-155">Click **OK** on this blade to confirm the change.</span></span> 
    
    ![][21]

<span data-ttu-id="96d0c-156">Ukończono wymaganej konfiguracji usługi AAD i możesz są gotowe do wywoływania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="96d0c-156">You have now completed the required AAD configuration and you are all set to call the APIs.</span></span> 

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



