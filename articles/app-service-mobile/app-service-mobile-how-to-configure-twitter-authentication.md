---
title: "aaaHow tooconfigure Twitter uwierzytelniania dla aplikacji usługi aplikacji"
description: "Dowiedz się, jak tooconfigure Twitter uwierzytelniania dla aplikacji usługi aplikacji."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a><span data-ttu-id="2b22e-103">Jak tooconfigure logowanie Twitter toouse aplikacji usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="2b22e-103">How tooconfigure your App Service application toouse Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="2b22e-104">W tym temacie opisano sposób tooconfigure usłudze Azure App Service toouse Twitter jako dostawcy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2b22e-104">This topic shows you how tooconfigure Azure App Service toouse Twitter as an authentication provider.</span></span>

<span data-ttu-id="2b22e-105">toocomplete hello procedurze w tym temacie, musi mieć konto usługi Twitter, które ma zweryfikowano e-mail adres i numer telefonu.</span><span class="sxs-lookup"><span data-stu-id="2b22e-105">toocomplete hello procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="2b22e-106">toocreate nowe konto usługi Twitter, przejdź zbyt<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="2b22e-106">toocreate a new Twitter account, go too<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="2b22e-107"><a name="register"></a>Zarejestrować aplikację w usłudze Twitter</span><span class="sxs-lookup"><span data-stu-id="2b22e-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="2b22e-108">Zaloguj się na toohello [portalu Azure]i przejdź tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b22e-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="2b22e-109">Kopiowanie z **adres URL**.</span><span class="sxs-lookup"><span data-stu-id="2b22e-109">Copy your **URL**.</span></span> <span data-ttu-id="2b22e-110">Użyjesz tego tooconfigure aplikacji Twitter.</span><span class="sxs-lookup"><span data-stu-id="2b22e-110">You will use this tooconfigure your Twitter app.</span></span>
2. <span data-ttu-id="2b22e-111">Przejdź toohello [Twitter deweloperzy] witryny sieci Web, zaloguj się przy użyciu poświadczeń konta usługi Twitter, a następnie kliknij przycisk **Utwórz nową aplikację**.</span><span class="sxs-lookup"><span data-stu-id="2b22e-111">Navigate toohello [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="2b22e-112">Typ w hello **nazwa** i **opis** dla nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b22e-112">Type in hello **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="2b22e-113">Wklej do aplikacji **adres URL** dla hello **witryny sieci Web** wartość.</span><span class="sxs-lookup"><span data-stu-id="2b22e-113">Paste in your application's **URL** for hello **Website** value.</span></span> <span data-ttu-id="2b22e-114">Następnie dla hello **wywołania zwrotnego adresu URL**, Wklej hello **wywołania zwrotnego adresu URL** wcześniej zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="2b22e-114">Then, for hello **Callback URL**, paste hello **Callback URL** you copied earlier.</span></span> <span data-ttu-id="2b22e-115">To jest Centrum aplikacji mobilnej dołączony ścieżki hello */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="2b22e-115">This is your Mobile App gateway appended with hello path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="2b22e-116">Na przykład `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="2b22e-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="2b22e-117">Upewnij się, że używasz hello schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2b22e-117">Make sure that you are using hello HTTPS scheme.</span></span>
4. <span data-ttu-id="2b22e-118">Na stronie powitania dolnej hello przeczytaj i zaakceptuj postanowienia hello.</span><span class="sxs-lookup"><span data-stu-id="2b22e-118">At hello bottom hello page, read and accept hello terms.</span></span> <span data-ttu-id="2b22e-119">Następnie kliknij przycisk **tworzenie aplikacji Twitter**.</span><span class="sxs-lookup"><span data-stu-id="2b22e-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="2b22e-120">Ta aplikacja hello rejestrów Wyświetla szczegóły aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="2b22e-120">This registers hello app displays hello application details.</span></span>
5. <span data-ttu-id="2b22e-121">Kliknij przycisk hello **ustawienia** karcie wyboru **Zezwalaj toosign toobe używać tej aplikacji za pomocą usługi Twitter**, następnie kliknij przycisk **ustawienia aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="2b22e-121">Click hello **Settings** tab, check **Allow this application toobe used toosign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="2b22e-122">Wybierz hello **kluczy i tokenów dostępu** kartę. Zanotuj wartości hello **konsumenta (klucz interfejsu API)** i **klucz tajny klienta (klucz tajny interfejsu API)**.</span><span class="sxs-lookup"><span data-stu-id="2b22e-122">Select hello **Keys and Access Tokens** tab. Make a note of hello values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2b22e-123">klucz tajny klienta Hello jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2b22e-123">hello consumer secret is an important security credential.</span></span> <span data-ttu-id="2b22e-124">Nie udostępniaj nikomu ten klucz tajny i rozpowszechnienie go z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="2b22e-124">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="2b22e-125"><a name="secrets"></a>Dodaj Twitter informacji tooyour aplikacji</span><span class="sxs-lookup"><span data-stu-id="2b22e-125"><a name="secrets"> </a>Add Twitter information tooyour application</span></span>
1. <span data-ttu-id="2b22e-126">Po powrocie do hello [portalu Azure], przejdź tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b22e-126">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="2b22e-127">Kliknij przycisk **ustawienia**, a następnie **uwierzytelniania / autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="2b22e-127">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="2b22e-128">Jeśli hello uwierzytelniania / autoryzacji funkcja nie jest włączona, włącz przełącznik hello zbyt**na**.</span><span class="sxs-lookup"><span data-stu-id="2b22e-128">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="2b22e-129">Kliknij przycisk **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="2b22e-129">Click **Twitter**.</span></span> <span data-ttu-id="2b22e-130">Wklej wartości, które uzyskany wcześniej hello identyfikator aplikacji i klucz tajny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b22e-130">Paste in hello App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="2b22e-131">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b22e-131">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="2b22e-132">Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowany dostęp do zawartości witryny tooyour i interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="2b22e-132">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="2b22e-133">Musisz zezwolić użytkownikom w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b22e-133">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="2b22e-134">(Opcjonalnie) toorestrict dostępu tooyour lokacji tooonly użytkowników uwierzytelnionych przez Twitter, ustaw **tootake akcji w przypadku nieuwierzytelnionego żądania** za**Twitter**.</span><span class="sxs-lookup"><span data-stu-id="2b22e-134">(Optional) toorestrict access tooyour site tooonly users authenticated by Twitter, set **Action tootake when request is not authenticated** too**Twitter**.</span></span> <span data-ttu-id="2b22e-135">Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są tooTwitter przekierowany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2b22e-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooTwitter for authentication.</span></span>
5. <span data-ttu-id="2b22e-136">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="2b22e-136">Click **Save**.</span></span>

<span data-ttu-id="2b22e-137">Wszystko jest teraz gotowy toouse usługi Twitter dla uwierzytelniania w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b22e-137">You are now ready toouse Twitter for authentication in your app.</span></span>

## <span data-ttu-id="2b22e-138"><a name="related-content"></a>Związane z zawartością</span><span class="sxs-lookup"><span data-stu-id="2b22e-138"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter deweloperzy]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[portalu Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
