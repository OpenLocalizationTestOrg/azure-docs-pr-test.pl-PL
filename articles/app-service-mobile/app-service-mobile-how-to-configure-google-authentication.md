---
title: "aaaHow tooconfigure Google uwierzytelniania dla aplikacji usługi aplikacji"
description: "Dowiedz się, jak uwierzytelniania serwisu Google tooconfigure aplikacji usługi aplikacji."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a><span data-ttu-id="46fc9-103">Jak tooconfigure logowanie Google toouse aplikacji usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="46fc9-103">How tooconfigure your App Service application toouse Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="46fc9-104">W tym temacie opisano sposób tooconfigure usłudze Azure App Service toouse Google jako dostawcy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="46fc9-104">This topic shows you how tooconfigure Azure App Service toouse Google as an authentication provider.</span></span>

<span data-ttu-id="46fc9-105">toocomplete hello procedurze w tym temacie, musi mieć konto Google ze zweryfikowanym adresem e-mail.</span><span class="sxs-lookup"><span data-stu-id="46fc9-105">toocomplete hello procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="46fc9-106">toocreate nowe konto Google, przejdź zbyt[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="46fc9-106">toocreate a new Google account, go too[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="46fc9-107"><a name="register"></a>Zarejestrować aplikację w usłudze Google</span><span class="sxs-lookup"><span data-stu-id="46fc9-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="46fc9-108">Zaloguj się na toohello [portalu Azure]i przejdź tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="46fc9-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="46fc9-109">Kopiowanie z **adres URL**, która użyj nowszej tooconfigure aplikacji Google.</span><span class="sxs-lookup"><span data-stu-id="46fc9-109">Copy your **URL**, which you use later tooconfigure your Google app.</span></span>
2. <span data-ttu-id="46fc9-110">Przejdź toohello [interfejsy API Google](http://go.microsoft.com/fwlink/p/?LinkId=268303) kliknij witrynę sieci Web, zaloguj się przy użyciu poświadczeń konta Google **tworzenia projektu**, podaj **Nazwa projektu**, następnie kliknij przycisk  **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-110">Navigate toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="46fc9-111">W obszarze **społecznościowych interfejsów API** kliknij **interfejsu API Google +** , a następnie **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="46fc9-112">W hello lewy pasek nawigacyjny **poświadczenia** > **ekranu zgoda OAuth**, a następnie wybierz pozycję z **adres E-mail**, wprowadź **nazwa produktu**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-112">In hello left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="46fc9-113">W hello **poświadczenia** , kliknij pozycję **Utwórz poświadczenia** > **identyfikator klienta OAuth**, a następnie wybierz pozycję **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-113">In hello **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="46fc9-114">Wklej hello usługi aplikacji **adres URL** zostanie wcześniej skopiowany do **autoryzowany źródeł JavaScript**, Wklej przekierowania z identyfikatora URI do **autoryzowany identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-114">Paste hello App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="46fc9-115">Witaj przekierowania URI jest adresem URL hello aplikacji dołączony ścieżki hello, */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="46fc9-115">hello redirect URI is hello URL of your application appended with hello path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="46fc9-116">Na przykład `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="46fc9-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="46fc9-117">Upewnij się, że używasz hello schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="46fc9-117">Make sure that you are using hello HTTPS scheme.</span></span> <span data-ttu-id="46fc9-118">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-118">Then click **Create**.</span></span>
7. <span data-ttu-id="46fc9-119">Na następnym ekranie powitania zanotuj wartości powitania klienta hello klucz tajny identyfikator i klienta.</span><span class="sxs-lookup"><span data-stu-id="46fc9-119">On hello next screen, make a note of hello values of hello client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="46fc9-120">klucz tajny klienta Hello jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="46fc9-120">hello client secret is an important security credential.</span></span> <span data-ttu-id="46fc9-121">Nie udostępniaj nikomu ten klucz tajny i rozpowszechnienie go w aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="46fc9-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="46fc9-122"><a name="secrets"></a>Google dodać informacje tooyour aplikacji</span><span class="sxs-lookup"><span data-stu-id="46fc9-122"><a name="secrets"> </a>Add Google information tooyour application</span></span>
1. <span data-ttu-id="46fc9-123">Po powrocie do hello [portalu Azure], przejdź tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="46fc9-123">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="46fc9-124">Kliknij przycisk **ustawienia**, a następnie **uwierzytelniania / autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="46fc9-125">Jeśli hello uwierzytelniania / autoryzacji funkcja nie jest włączona, włącz przełącznik hello zbyt**na**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-125">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="46fc9-126">Kliknij przycisk **Google**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-126">Click **Google**.</span></span> <span data-ttu-id="46fc9-127">Wklej w wartości Identyfikatora aplikacji i klucz tajny aplikacji hello, które uzyskany wcześniej i opcjonalnie włączyć wszystkie zakresy wymaganych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="46fc9-127">Paste in hello App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="46fc9-128">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="46fc9-129">Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowany dostęp do zawartości witryny tooyour i interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="46fc9-129">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="46fc9-130">Musisz zezwolić użytkownikom w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="46fc9-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="46fc9-131">(Opcjonalnie) toorestrict dostępu tooyour lokacji tooonly użytkowników uwierzytelnionych przez firmę Google, ustaw **tootake akcji w przypadku nieuwierzytelnionego żądania** za**Google**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-131">(Optional) toorestrict access tooyour site tooonly users authenticated by Google, set **Action tootake when request is not authenticated** too**Google**.</span></span> <span data-ttu-id="46fc9-132">Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są tooGoogle przekierowany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="46fc9-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooGoogle for authentication.</span></span>
5. <span data-ttu-id="46fc9-133">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="46fc9-133">Click **Save**.</span></span>

<span data-ttu-id="46fc9-134">Wszystko jest teraz gotowy toouse Google do uwierzytelniania w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="46fc9-134">You are now ready toouse Google for authentication in your app.</span></span>

## <span data-ttu-id="46fc9-135"><a name="related-content"></a>Związane z zawartością</span><span class="sxs-lookup"><span data-stu-id="46fc9-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portalu Azure]: https://portal.azure.com/

