---
title: "Uwierzytelnianie Microsoft Account tooconfigure aaaHow aplikacji usługi aplikacji"
description: "Dowiedz się, jak uwierzytelnianie Microsoft Account tooconfigure aplikacji usługi aplikacji."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a><span data-ttu-id="a4490-103">Jak tooconfigure logowanie Account Microsoft toouse aplikacji usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="a4490-103">How tooconfigure your App Service application toouse Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="a4490-104">W tym temacie opisano sposób tooconfigure usłudze Azure App Service toouse Account Microsoft jako dostawcy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a4490-104">This topic shows you how tooconfigure Azure App Service toouse Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="a4490-105"><a name="register-microsoft-account"></a>Zarejestrować aplikację z kontem Microsoft</span><span class="sxs-lookup"><span data-stu-id="a4490-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="a4490-106">Zaloguj się na toohello [portalu Azure]i przejdź tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4490-106">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="a4490-107">Kopiowania z **adres URL**, który później możesz użyć tooconfigure aplikacji z Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a4490-107">Copy your **URL**, which later you use tooconfigure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="a4490-108">Przejdź toohello [Moje aplikacje] strony hello Microsoft Account Developer Center i zaloguj się przy użyciu konta Microsoft, jeśli jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="a4490-108">Navigate toohello [My Applications] page in hello Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="a4490-109">Kliknij przycisk **Dodaj aplikację**, następnie wpisz nazwę aplikacji i kliknij przycisk **tworzenie aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="a4490-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="a4490-110">Zanotuj hello **identyfikator aplikacji**, ponieważ będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="a4490-110">Make a note of hello **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="a4490-111">W obszarze "Platform," kliknij **dodać platformy** i wybierz pozycję "Web".</span><span class="sxs-lookup"><span data-stu-id="a4490-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="a4490-112">W obszarze "Identyfikator URI przekierowania" Podaj punkt końcowy hello aplikacji, następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="a4490-112">Under "Redirect URIs" supply hello endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="a4490-113">Twoje przekierowania URI jest adresem URL hello aplikacji dołączony ścieżki hello, */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="a4490-113">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="a4490-114">Na przykład `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="a4490-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="a4490-115">Upewnij się, że używasz hello schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a4490-115">Make sure that you are using hello HTTPS scheme.</span></span>
   
7. <span data-ttu-id="a4490-116">W obszarze "Klucze tajne aplikacji," kliknij **wygenerować nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="a4490-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="a4490-117">Zanotuj wartość hello wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="a4490-117">Make note of hello value that appears.</span></span> <span data-ttu-id="a4490-118">Po wyjściu strony hello go nie pojawi się ponownie.</span><span class="sxs-lookup"><span data-stu-id="a4490-118">Once you leave hello page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a4490-119">hasło Hello jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a4490-119">hello password is an important security credential.</span></span> <span data-ttu-id="a4490-120">Nie udostępniaj nikomu hasła hello lub opublikować go w aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="a4490-120">Do not share hello password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="a4490-121"><a name="secrets"></a>Dodawanie konta Microsoft informacji tooyour aplikacji usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="a4490-121"><a name="secrets"> </a>Add Microsoft Account information tooyour App Service application</span></span>
1. <span data-ttu-id="a4490-122">Po powrocie do hello [portalu Azure]Przejdź tooyour aplikacji, kliknij przycisk **ustawienia** > **uwierzytelniania / autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="a4490-122">Back in hello [Azure portal], navigate tooyour application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="a4490-123">Jeśli hello uwierzytelniania / autoryzacji funkcja nie jest włączona, przełącz go **na**.</span><span class="sxs-lookup"><span data-stu-id="a4490-123">If hello Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="a4490-124">Kliknij przycisk **konta Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="a4490-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="a4490-125">Wklej w wartości Identyfikatora aplikacji i hasło hello, które uzyskany wcześniej i opcjonalnie włączyć wszystkie zakresy wymaganych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="a4490-125">Paste in hello Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="a4490-126">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a4490-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="a4490-127">Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowany dostęp do zawartości witryny tooyour i interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a4490-127">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="a4490-128">Musisz zezwolić użytkownikom w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4490-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="a4490-129">(Opcjonalnie) toorestrict dostępu tooyour lokacji tooonly użytkowników uwierzytelnionych przez konta Microsoft, ustaw **tootake akcji w przypadku nieuwierzytelnionego żądania** za**Account Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="a4490-129">(Optional) toorestrict access tooyour site tooonly users authenticated by Microsoft account, set **Action tootake when request is not authenticated** too**Microsoft Account**.</span></span> <span data-ttu-id="a4490-130">Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są przekierowywane tooMicrosoft konto do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a4490-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooMicrosoft account for authentication.</span></span>
5. <span data-ttu-id="a4490-131">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a4490-131">Click **Save**.</span></span>

<span data-ttu-id="a4490-132">Wszystko jest teraz gotowy toouse Account Microsoft do uwierzytelniania w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4490-132">You are now ready toouse Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="a4490-133"><a name="related-content"></a>Związane z zawartością</span><span class="sxs-lookup"><span data-stu-id="a4490-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[Moje aplikacje]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Witryna Azure Portal]: https://portal.azure.com/
