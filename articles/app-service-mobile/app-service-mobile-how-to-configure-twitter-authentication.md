---
title: "Jak skonfigurować uwierzytelnianie usługi Twitter dla aplikacji usługi aplikacji"
description: "Dowiedz się, jak skonfigurować uwierzytelnianie usługi Twitter dla aplikacji usługi aplikacji."
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
ms.openlocfilehash: afde020b7817dc58ecea24eb4a09cf93d0986eb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-twitter-login"></a><span data-ttu-id="32511-103">Konfigurowanie aplikacji usługi aplikacji umożliwiająca użycie logowania usługi Twitter</span><span class="sxs-lookup"><span data-stu-id="32511-103">How to configure your App Service application to use Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="32511-104">W tym temacie przedstawiono sposób konfigurowania usługi Azure App Service, aby użyć usługi Twitter jako dostawcy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="32511-104">This topic shows you how to configure Azure App Service to use Twitter as an authentication provider.</span></span>

<span data-ttu-id="32511-105">Aby ukończyć tę procedurę w tym temacie, musi mieć konto usługi Twitter, które ma zweryfikowano e-mail adres i numer telefonu.</span><span class="sxs-lookup"><span data-stu-id="32511-105">To complete the procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="32511-106">Aby utworzyć nowe konto usługi Twitter, przejdź do <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="32511-106">To create a new Twitter account, go to <a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="32511-107"><a name="register"></a>Zarejestrować aplikację w usłudze Twitter</span><span class="sxs-lookup"><span data-stu-id="32511-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="32511-108">Zaloguj się do [portalu Azure], a następnie przejdź do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32511-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="32511-109">Kopiowanie z **adres URL**.</span><span class="sxs-lookup"><span data-stu-id="32511-109">Copy your **URL**.</span></span> <span data-ttu-id="32511-110">Umożliwia to skonfigurować aplikację usługi Twitter.</span><span class="sxs-lookup"><span data-stu-id="32511-110">You will use this to configure your Twitter app.</span></span>
2. <span data-ttu-id="32511-111">Przejdź do [Twitter deweloperzy] witryny sieci Web, zaloguj się przy użyciu poświadczeń konta usługi Twitter, a następnie kliknij przycisk **Utwórz nową aplikację**.</span><span class="sxs-lookup"><span data-stu-id="32511-111">Navigate to the [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="32511-112">Wpisz w **nazwa** i **opis** dla nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32511-112">Type in the **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="32511-113">Wklej do aplikacji **adres URL** dla **witryny sieci Web** wartość.</span><span class="sxs-lookup"><span data-stu-id="32511-113">Paste in your application's **URL** for the **Website** value.</span></span> <span data-ttu-id="32511-114">Następnie dla **wywołania zwrotnego adresu URL**, Wklej **wywołania zwrotnego adresu URL** wcześniej zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="32511-114">Then, for the **Callback URL**, paste the **Callback URL** you copied earlier.</span></span> <span data-ttu-id="32511-115">To jest dołączany wraz ze ścieżką Centrum aplikacji mobilnej */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="32511-115">This is your Mobile App gateway appended with the path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="32511-116">Na przykład `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="32511-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="32511-117">Upewnij się, że używasz schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="32511-117">Make sure that you are using the HTTPS scheme.</span></span>
4. <span data-ttu-id="32511-118">Na dole strony przeczytaj i zaakceptuj postanowienia.</span><span class="sxs-lookup"><span data-stu-id="32511-118">At the bottom the page, read and accept the terms.</span></span> <span data-ttu-id="32511-119">Następnie kliknij przycisk **tworzenie aplikacji Twitter**.</span><span class="sxs-lookup"><span data-stu-id="32511-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="32511-120">Rejestruje to aplikacja jest wyświetlana szczegółów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32511-120">This registers the app displays the application details.</span></span>
5. <span data-ttu-id="32511-121">Kliknij przycisk **ustawienia** karcie wyboru **zezwolić tej aplikacji należy się zalogować za pomocą usługi Twitter**, następnie kliknij przycisk **ustawienia aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="32511-121">Click the **Settings** tab, check **Allow this application to be used to sign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="32511-122">Wybierz **kluczy i tokenów dostępu** kartę.</span><span class="sxs-lookup"><span data-stu-id="32511-122">Select the **Keys and Access Tokens** tab.</span></span> <span data-ttu-id="32511-123">Zanotuj wartości **konsumenta (klucz interfejsu API)** i **klucz tajny klienta (klucz tajny interfejsu API)**.</span><span class="sxs-lookup"><span data-stu-id="32511-123">Make a note of the values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="32511-124">Klucz tajny klienta jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="32511-124">The consumer secret is an important security credential.</span></span> <span data-ttu-id="32511-125">Nie udostępniaj nikomu ten klucz tajny i rozpowszechnienie go z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="32511-125">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="32511-126"><a name="secrets"></a>Dodaj Twitter informacje dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="32511-126"><a name="secrets"> </a>Add Twitter information to your application</span></span>
1. <span data-ttu-id="32511-127">W [portalu Azure], przejdź do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32511-127">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="32511-128">Kliknij przycisk **ustawienia**, a następnie **uwierzytelniania / autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="32511-128">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="32511-129">Jeśli uwierzytelnianie / autoryzacja funkcja nie jest włączona, włącz przełącznik do **na**.</span><span class="sxs-lookup"><span data-stu-id="32511-129">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="32511-130">Kliknij przycisk **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="32511-130">Click **Twitter**.</span></span> <span data-ttu-id="32511-131">Wklej wartości, które uzyskany wcześniej identyfikator aplikacji i klucz tajny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32511-131">Paste in the App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="32511-132">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="32511-132">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="32511-133">Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowanego dostępu do interfejsów API i zawartości witryny.</span><span class="sxs-lookup"><span data-stu-id="32511-133">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="32511-134">Musisz zezwolić użytkownikom w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32511-134">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="32511-135">(Opcjonalnie) Aby ograniczyć dostęp do witryny użytkownikom tylko uwierzytelniony przez usługi Twitter, ustaw **działania należy podjąć w przypadku nieuwierzytelnionego żądania** do **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="32511-135">(Optional) To restrict access to your site to only users authenticated by Twitter, set **Action to take when request is not authenticated** to **Twitter**.</span></span> <span data-ttu-id="32511-136">Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są przekierowywane do usługi Twitter dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="32511-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Twitter for authentication.</span></span>
5. <span data-ttu-id="32511-137">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="32511-137">Click **Save**.</span></span>

<span data-ttu-id="32511-138">Teraz można przystąpić do uwierzytelniania w aplikacji Twitter.</span><span class="sxs-lookup"><span data-stu-id="32511-138">You are now ready to use Twitter for authentication in your app.</span></span>

## <span data-ttu-id="32511-139"><a name="related-content"></a>Związane z zawartością</span><span class="sxs-lookup"><span data-stu-id="32511-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

<span data-ttu-id="32511-140">[Twitter deweloperzy]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span><span class="sxs-lookup"><span data-stu-id="32511-140">[Twitter Developers]: http://go.microsoft.com/fwlink/p/?LinkId=268300</span></span>
<span data-ttu-id="32511-141">[portalu Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="32511-141">[Azure portal]: https://portal.azure.com/</span></span>
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
