---
title: "uwierzytelniania serwisu Facebook tooconfigure aaaHow aplikacji usługi aplikacji"
description: "Dowiedz się, jak tooconfigure uwierzytelniania serwisu Facebook dla aplikacji usługi aplikacji."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a><span data-ttu-id="b7d24-103">Jak tooconfigure logowanie Facebook toouse aplikacji usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b7d24-103">How tooconfigure your App Service application toouse Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="b7d24-104">W tym temacie opisano sposób tooconfigure usłudze Azure App Service toouse usługi Facebook jako dostawcy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b7d24-104">This topic shows you how tooconfigure Azure App Service toouse Facebook as an authentication provider.</span></span>

<span data-ttu-id="b7d24-105">toocomplete hello procedurze w tym temacie, musisz mieć konto usługi Facebook, ze zweryfikowanym adresem e-mail i numer telefonu komórkowego.</span><span class="sxs-lookup"><span data-stu-id="b7d24-105">toocomplete hello procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="b7d24-106">toocreate nowe konto usługi Facebook, przejdź zbyt[facebook.com].</span><span class="sxs-lookup"><span data-stu-id="b7d24-106">toocreate a new Facebook account, go too[facebook.com].</span></span>

## <span data-ttu-id="b7d24-107"><a name="register"></a>Zarejestrować aplikację w usłudze Facebook</span><span class="sxs-lookup"><span data-stu-id="b7d24-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="b7d24-108">Zaloguj się na toohello [portalu Azure]i przejdź tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7d24-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="b7d24-109">Kopiowanie z **adres URL**.</span><span class="sxs-lookup"><span data-stu-id="b7d24-109">Copy your **URL**.</span></span> <span data-ttu-id="b7d24-110">Użyjesz tego tooconfigure aplikacji Facebook.</span><span class="sxs-lookup"><span data-stu-id="b7d24-110">You will use this tooconfigure your Facebook app.</span></span>
2. <span data-ttu-id="b7d24-111">W innym oknie przeglądarki Przejdź toohello [deweloperzy Facebook] poświadczenia konta witryny sieci Web i logowania z użytkownika usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b7d24-111">In another browser window, navigate toohello [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="b7d24-112">(Opcjonalnie) Jeśli nie została jeszcze zarejestrowana, kliknij przycisk **aplikacje** > **Zarejestruj się jako deweloper**, Zaakceptuj zasady hello i wykonaj kroki rejestracji hello.</span><span class="sxs-lookup"><span data-stu-id="b7d24-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept hello policy and follow hello registration steps.</span></span>
4. <span data-ttu-id="b7d24-113">Kliknij przycisk **Moje aplikacje** > **Dodaj nową aplikację** > **witryny sieci Web** > **pominąć i utworzyć identyfikator aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b7d24-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="b7d24-114">W **Nazwa wyświetlana**, wpisz unikatową nazwę dla aplikacji, typ użytkownika **E-mail kontaktu**, wybierz **kategorii** dla aplikacji, następnie kliknij przycisk **utworzyć identyfikator aplikacji**i ukończyć powitalnych sprawdzania zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b7d24-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete hello security check.</span></span> <span data-ttu-id="b7d24-115">Trwa pulpitu nawigacyjnego developer toohello dla nowej aplikacji usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="b7d24-115">This takes you toohello developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="b7d24-116">W obszarze "Logowanie usługi Facebook", kliknij przycisk **wprowadzenie**.</span><span class="sxs-lookup"><span data-stu-id="b7d24-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="b7d24-117">Dodawanie aplikacji **identyfikator URI przekierowania** za**prawidłowy OAuth przekierowania URI**, następnie kliknij przycisk **Zapisz zmiany**.</span><span class="sxs-lookup"><span data-stu-id="b7d24-117">Add your application's **Redirect URI** too**Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b7d24-118">Twoje przekierowania URI jest adresem URL hello aplikacji dołączony ścieżki hello, */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="b7d24-118">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="b7d24-119">Na przykład `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="b7d24-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="b7d24-120">Upewnij się, że używasz hello schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b7d24-120">Make sure that you are using hello HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="b7d24-121">W nawigacji po lewej stronie powitania, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="b7d24-121">In hello left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="b7d24-122">Na powitania **klucz tajny aplikacji** kliknij **Pokaż**, podaj hasło, jeśli żądanie, a następnie zanotuj wartości hello **identyfikator aplikacji** i **klucz tajny aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b7d24-122">On hello **App Secret** field, click **Show**, provide your password if requested, then make a note of hello values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="b7d24-123">Te nowsze tooconfigure za pomocą aplikacji w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="b7d24-123">You use these later tooconfigure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b7d24-124">klucz tajny aplikacji Hello jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b7d24-124">hello app secret is an important security credential.</span></span> <span data-ttu-id="b7d24-125">Nie udostępniaj nikomu ten klucz tajny i rozpowszechnienie go w aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="b7d24-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="b7d24-126">Witaj konta usługi Facebook, która była używana tooregister aplikacji hello jest administrator aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b7d24-126">hello Facebook account which was used tooregister hello application is an administrator of hello app.</span></span> <span data-ttu-id="b7d24-127">W tym momencie tylko administratorzy mogą Zaloguj się do tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7d24-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="b7d24-128">tooauthenticate inne konta usługi Facebook, kliknij przycisk **aplikacji przejrzyj** i Włącz **publicznego upewnij < your-app-name >** tooenable ogólne publicznego dostępu przy użyciu uwierzytelniania serwisu Facebook.</span><span class="sxs-lookup"><span data-stu-id="b7d24-128">tooauthenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** tooenable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="b7d24-129"><a name="secrets"></a>Facebook dodać informacje tooyour aplikacji</span><span class="sxs-lookup"><span data-stu-id="b7d24-129"><a name="secrets"> </a>Add Facebook information tooyour application</span></span>
1. <span data-ttu-id="b7d24-130">Po powrocie do hello [portalu Azure], przejdź tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7d24-130">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="b7d24-131">Kliknij przycisk **ustawienia** > **uwierzytelniania / autoryzacji**i upewnij się, że **aplikacji uwierzytelniania usługi** jest **na**.</span><span class="sxs-lookup"><span data-stu-id="b7d24-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="b7d24-132">Kliknij przycisk **Facebook**, Wklej wartości Identyfikatora aplikacji i klucz tajny aplikacji hello, które uzyskany wcześniej, opcjonalnie włączyć wszystkie zakresy wymagane przez aplikację, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7d24-132">Click **Facebook**, paste in hello App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="b7d24-133">Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowany dostęp do zawartości witryny tooyour i interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="b7d24-133">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="b7d24-134">Musisz zezwolić użytkownikom w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7d24-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="b7d24-135">(Opcjonalnie) toorestrict dostępu tooyour lokacji tooonly użytkowników uwierzytelnionych przez Facebook, ustawić **tootake akcji w przypadku nieuwierzytelnionego żądania** za**Facebook**.</span><span class="sxs-lookup"><span data-stu-id="b7d24-135">(Optional) toorestrict access tooyour site tooonly users authenticated by Facebook, set **Action tootake when request is not authenticated** too**Facebook**.</span></span> <span data-ttu-id="b7d24-136">Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są tooFacebook przekierowany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b7d24-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooFacebook for authentication.</span></span>
4. <span data-ttu-id="b7d24-137">Po zakończeniu konfigurowania uwierzytelniania, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="b7d24-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="b7d24-138">Wszystko jest teraz gotowy toouse Facebook dla uwierzytelniania w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7d24-138">You are now ready toouse Facebook for authentication in your app.</span></span>

## <span data-ttu-id="b7d24-139"><a name="related-content"></a>Związane z zawartością</span><span class="sxs-lookup"><span data-stu-id="b7d24-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[Deweloperzy usługi Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[Facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[Witryna Azure Portal]: https://portal.azure.com/
