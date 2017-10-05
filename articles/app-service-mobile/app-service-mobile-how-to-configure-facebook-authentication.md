---
title: "Konfigurowanie uwierzytelniania serwisu Facebook dla aplikacji usługi aplikacji"
description: "Informacje o sposobie konfigurowania uwierzytelniania serwisu Facebook dla aplikacji usługi aplikacji."
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
ms.openlocfilehash: c1b4c91d384c56c4f55bf8d31ced250f51c0d837
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-facebook-login"></a><span data-ttu-id="da44a-103">Jak skonfigurować aplikację App Service, aby używała logowania do usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="da44a-103">How to configure your App Service application to use Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="da44a-104">W tym temacie przedstawiono sposób konfigurowania usługi aplikacji Azure do użycia jako dostawcę uwierzytelniania serwisu Facebook.</span><span class="sxs-lookup"><span data-stu-id="da44a-104">This topic shows you how to configure Azure App Service to use Facebook as an authentication provider.</span></span>

<span data-ttu-id="da44a-105">Aby ukończyć tę procedurę w tym temacie, musi mieć konto usługi Facebook, które ma ze zweryfikowanym adresem e-mail i numer telefonu komórkowego.</span><span class="sxs-lookup"><span data-stu-id="da44a-105">To complete the procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="da44a-106">Aby utworzyć nowe konto usługi Facebook, przejdź do [facebook.com].</span><span class="sxs-lookup"><span data-stu-id="da44a-106">To create a new Facebook account, go to [facebook.com].</span></span>

## <span data-ttu-id="da44a-107"><a name="register"></a>Zarejestrować aplikację w usłudze Facebook</span><span class="sxs-lookup"><span data-stu-id="da44a-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="da44a-108">Zaloguj się do [portalu Azure], a następnie przejdź do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da44a-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="da44a-109">Kopiowanie z **adres URL**.</span><span class="sxs-lookup"><span data-stu-id="da44a-109">Copy your **URL**.</span></span> <span data-ttu-id="da44a-110">Umożliwia to konfigurowanie aplikacji usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="da44a-110">You will use this to configure your Facebook app.</span></span>
2. <span data-ttu-id="da44a-111">W innym oknie przeglądarki, przejdź do [deweloperzy Facebook] poświadczenia konta witryny sieci Web i logowania z użytkownika usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="da44a-111">In another browser window, navigate to the [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="da44a-112">(Opcjonalnie) Jeśli nie została jeszcze zarejestrowana, kliknij przycisk **aplikacje** > **Zarejestruj się jako deweloper**, Zaakceptuj zasady i wykonaj kroki rejestracji.</span><span class="sxs-lookup"><span data-stu-id="da44a-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept the policy and follow the registration steps.</span></span>
4. <span data-ttu-id="da44a-113">Kliknij przycisk **Moje aplikacje** > **Dodaj nową aplikację** > **witryny sieci Web** > **pominąć i utworzyć identyfikator aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="da44a-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="da44a-114">W **Nazwa wyświetlana**, wpisz unikatową nazwę dla aplikacji, typ użytkownika **E-mail kontaktu**, wybierz **kategorii** dla aplikacji, następnie kliknij przycisk **utworzyć identyfikator aplikacji** i ukończyć sprawdzanie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="da44a-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete the security check.</span></span> <span data-ttu-id="da44a-115">Powoduje to przejście do projektanta pulpitu nawigacyjnego dla nowej aplikacji usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="da44a-115">This takes you to the developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="da44a-116">W obszarze "Logowanie usługi Facebook", kliknij przycisk **wprowadzenie**.</span><span class="sxs-lookup"><span data-stu-id="da44a-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="da44a-117">Dodawanie aplikacji **identyfikator URI przekierowania** do **prawidłowy OAuth przekierowania URI**, następnie kliknij przycisk **Zapisz zmiany**.</span><span class="sxs-lookup"><span data-stu-id="da44a-117">Add your application's **Redirect URI** to **Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="da44a-118">Twoje przekierowania URI jest adres URL aplikacji dołączany wraz ze ścieżką */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="da44a-118">Your redirect URI is the URL of your application appended with the path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="da44a-119">Na przykład `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="da44a-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="da44a-120">Upewnij się, że używasz schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="da44a-120">Make sure that you are using the HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="da44a-121">W obszarze nawigacji po lewej stronie, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="da44a-121">In the left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="da44a-122">Na **klucz tajny aplikacji** kliknij **Pokaż**, podaj hasło, jeśli żądanie, a następnie zanotuj wartości **identyfikator aplikacji** i **klucz tajny aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="da44a-122">On the **App Secret** field, click **Show**, provide your password if requested, then make a note of the values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="da44a-123">Można użyć tych później do konfigurowania aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="da44a-123">You use these later to configure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="da44a-124">Klucz tajny aplikacji jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="da44a-124">The app secret is an important security credential.</span></span> <span data-ttu-id="da44a-125">Nie udostępniaj nikomu ten klucz tajny i rozpowszechnienie go w aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="da44a-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="da44a-126">Konto usługi Facebook, która była używana do rejestrowania aplikacji jest administrator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da44a-126">The Facebook account which was used to register the application is an administrator of the app.</span></span> <span data-ttu-id="da44a-127">W tym momencie tylko administratorzy mogą Zaloguj się do tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da44a-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="da44a-128">Do uwierzytelniania innych kont usługi Facebook, kliknij przycisk **aplikacji przejrzyj** i Włącz **publicznego upewnij < your-app-name >** umożliwia ogólne dostęp publiczny przy użyciu uwierzytelniania serwisu Facebook.</span><span class="sxs-lookup"><span data-stu-id="da44a-128">To authenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** to enable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="da44a-129"><a name="secrets"></a>Informacje dodać Facebook dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="da44a-129"><a name="secrets"> </a>Add Facebook information to your application</span></span>
1. <span data-ttu-id="da44a-130">W [portalu Azure], przejdź do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da44a-130">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="da44a-131">Kliknij przycisk **ustawienia** > **uwierzytelniania / autoryzacji**i upewnij się, że **aplikacji uwierzytelniania usługi** jest **na**.</span><span class="sxs-lookup"><span data-stu-id="da44a-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="da44a-132">Kliknij przycisk **Facebook**, Wklej wartości Identyfikatora aplikacji i klucz tajny aplikacji, które uzyskany wcześniej, opcjonalnie włączyć wszystkie zakresy wymagane przez aplikację, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="da44a-132">Click **Facebook**, paste in the App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="da44a-133">Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowanego dostępu do interfejsów API i zawartości witryny.</span><span class="sxs-lookup"><span data-stu-id="da44a-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="da44a-134">Musisz zezwolić użytkownikom w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da44a-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="da44a-135">(Opcjonalnie) Aby ograniczyć dostęp do witryny użytkownikom tylko uwierzytelniony przez usługi Facebook, ustaw **działania należy podjąć w przypadku nieuwierzytelnionego żądania** do **Facebook**.</span><span class="sxs-lookup"><span data-stu-id="da44a-135">(Optional) To restrict access to your site to only users authenticated by Facebook, set **Action to take when request is not authenticated** to **Facebook**.</span></span> <span data-ttu-id="da44a-136">Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są przekierowywane do serwisu Facebook dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="da44a-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Facebook for authentication.</span></span>
4. <span data-ttu-id="da44a-137">Po zakończeniu konfigurowania uwierzytelniania, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="da44a-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="da44a-138">Teraz można przystąpić do uwierzytelniania w aplikacji usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="da44a-138">You are now ready to use Facebook for authentication in your app.</span></span>

## <span data-ttu-id="da44a-139"><a name="related-content"></a>Związane z zawartością</span><span class="sxs-lookup"><span data-stu-id="da44a-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
<span data-ttu-id="da44a-140">[deweloperzy Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span><span class="sxs-lookup"><span data-stu-id="da44a-140">[Facebook Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268286</span></span>
<span data-ttu-id="da44a-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span><span class="sxs-lookup"><span data-stu-id="da44a-141">[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285</span></span>
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
<span data-ttu-id="da44a-142">[portalu Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="da44a-142">[Azure portal]: https://portal.azure.com/</span></span>
