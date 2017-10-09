---
title: "Uwierzytelnianie aaaAdd na Apache Cordova w usłudze Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Mobile Apps w usłudze Azure App Service tooauthenticate użytkowników aplikacji oprogramowania Apache Cordova za pomocą różnych dostawców tożsamości, obejmującej Google, Facebook, Twitter i Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a><span data-ttu-id="63dc0-103">Dodawanie aplikacji oprogramowania Apache Cordova tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="63dc0-103">Add authentication tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="63dc0-104">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="63dc0-104">Summary</span></span>
<span data-ttu-id="63dc0-105">W tym samouczku możesz dodać projekt szybkiego startu todolist toohello uwierzytelniania w przypadku oprogramowania Apache Cordova przy użyciu dostawcy tożsamości obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="63dc0-105">In this tutorial, you add authentication toohello todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="63dc0-106">W tym samouczku jest oparta na powitania [Rozpoczynanie pracy z usługą Mobile Apps] — samouczek, należy najpierw wykonać.</span><span class="sxs-lookup"><span data-stu-id="63dc0-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="63dc0-107"><a name="register"></a>Zarejestrować aplikację do uwierzytelniania i skonfigurować hello usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="63dc0-107"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="63dc0-108">Obejrzyj wideo przedstawiające podobne kroki</span><span class="sxs-lookup"><span data-stu-id="63dc0-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="63dc0-109"><a name="permissions"></a>Ogranicz uprawnienia tooauthenticated użytkowników</span><span class="sxs-lookup"><span data-stu-id="63dc0-109"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="63dc0-110">Teraz możesz sprawdzić, czy ten dostęp anonimowy tooyour wewnętrznej bazy danych została wyłączona.</span><span class="sxs-lookup"><span data-stu-id="63dc0-110">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="63dc0-111">W programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="63dc0-111">In Visual Studio:</span></span>

* <span data-ttu-id="63dc0-112">Hello Otwórz projekt, który został utworzony po ukończeniu samouczka hello [Rozpoczynanie pracy z usługą Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="63dc0-112">Open hello project that you created when you completed hello tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="63dc0-113">Uruchom aplikację w hello **Emulator systemu Google Android**.</span><span class="sxs-lookup"><span data-stu-id="63dc0-113">Run your application in hello **Google Android Emulator**.</span></span>
* <span data-ttu-id="63dc0-114">Sprawdź, czy wystąpił nieoczekiwany błąd połączenia jest wyświetlany po uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="63dc0-114">Verify that an Unexpected Connection Failure is shown after hello app starts.</span></span>

<span data-ttu-id="63dc0-115">Następnie zaktualizuj użytkownicy tooauthenticate aplikacji hello przed wysłaniem żądania zasobów z hello zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="63dc0-115">Next, update hello app tooauthenticate users before requesting resources from hello Mobile App backend.</span></span>

## <span data-ttu-id="63dc0-116"><a name="add-authentication"></a>Dodaj aplikację toohello uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="63dc0-116"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="63dc0-117">Otwórz projekt w **programu Visual Studio**, następnie otwórz hello `www/index.html` plik do edycji.</span><span class="sxs-lookup"><span data-stu-id="63dc0-117">Open your project in **Visual Studio**, then open hello `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="63dc0-118">Zlokalizuj hello `Content-Security-Policy` metatag w sekcji head hello.</span><span class="sxs-lookup"><span data-stu-id="63dc0-118">Locate hello `Content-Security-Policy` meta tag in hello head section.</span></span>  <span data-ttu-id="63dc0-119">Dodaj hello OAuth hosta toohello listę dozwolonych źródeł.</span><span class="sxs-lookup"><span data-stu-id="63dc0-119">Add hello OAuth host toohello list of allowed sources.</span></span>

   | <span data-ttu-id="63dc0-120">Dostawca</span><span class="sxs-lookup"><span data-stu-id="63dc0-120">Provider</span></span> | <span data-ttu-id="63dc0-121">Nazwa dostawcy zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="63dc0-121">SDK Provider Name</span></span> | <span data-ttu-id="63dc0-122">OAuth Host</span><span class="sxs-lookup"><span data-stu-id="63dc0-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="63dc0-123">Usługa Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63dc0-123">Azure Active Directory</span></span> | <span data-ttu-id="63dc0-124">usługi AAD</span><span class="sxs-lookup"><span data-stu-id="63dc0-124">aad</span></span> | <span data-ttu-id="63dc0-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="63dc0-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="63dc0-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="63dc0-126">Facebook</span></span> | <span data-ttu-id="63dc0-127">Usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="63dc0-127">facebook</span></span> | <span data-ttu-id="63dc0-128">https://www.Facebook.com</span><span class="sxs-lookup"><span data-stu-id="63dc0-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="63dc0-129">Google</span><span class="sxs-lookup"><span data-stu-id="63dc0-129">Google</span></span> | <span data-ttu-id="63dc0-130">Google</span><span class="sxs-lookup"><span data-stu-id="63dc0-130">google</span></span> | <span data-ttu-id="63dc0-131">https://accounts.Google.com</span><span class="sxs-lookup"><span data-stu-id="63dc0-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="63dc0-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="63dc0-132">Microsoft</span></span> | <span data-ttu-id="63dc0-133">MicrosoftAccount</span><span class="sxs-lookup"><span data-stu-id="63dc0-133">microsoftaccount</span></span> | <span data-ttu-id="63dc0-134">https://login.Live.com</span><span class="sxs-lookup"><span data-stu-id="63dc0-134">https://login.live.com</span></span> |
   | <span data-ttu-id="63dc0-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="63dc0-135">Twitter</span></span> | <span data-ttu-id="63dc0-136">W usłudze Twitter</span><span class="sxs-lookup"><span data-stu-id="63dc0-136">twitter</span></span> | <span data-ttu-id="63dc0-137">https://API.twitter.com</span><span class="sxs-lookup"><span data-stu-id="63dc0-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="63dc0-138">Przykład zawartość--zasady zabezpieczeń (zaimplementowany dla usługi Azure Active Directory) jest następujący:</span><span class="sxs-lookup"><span data-stu-id="63dc0-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="63dc0-139">Zastąp `https://login.microsoftonline.com` z hostem OAuth hello hello powyższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="63dc0-139">Replace `https://login.microsoftonline.com` with hello OAuth host from hello preceding table.</span></span>  <span data-ttu-id="63dc0-140">Aby uzyskać więcej informacji na temat hello zawartości zabezpieczeń zasady metatag Zobacz hello [zasadę zawartość dokumentacji].</span><span class="sxs-lookup"><span data-stu-id="63dc0-140">For more information about hello content-security-policy meta tag, see hello [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="63dc0-141">Niektórzy dostawcy uwierzytelniania nie wymaga się, że zawartość zabezpieczeń zasady zostanie zmieniona, gdy na urządzeniach przenośnych odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="63dc0-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="63dc0-142">Na przykład żadnych zmian zawartości zabezpieczeń zasady są wymagane w przypadku przy użyciu uwierzytelniania serwisu Google na urządzeniu z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="63dc0-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="63dc0-143">Otwórz hello `www/js/index.js` pliku do edycji, Znajdź hello `onDeviceReady()` metody i w obszarze powitania klienta tworzenia kodu Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="63dc0-143">Open hello `www/js/index.js` file for editing, locate hello `onDeviceReady()` method, and under hello client  creation code add hello following code:</span></span>

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="63dc0-144">Ten kod zastępuje hello istniejący kod, który tworzy odwołanie do tabeli hello i odświeża hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63dc0-144">This code replaces hello existing code that creates hello table reference and refreshes hello UI.</span></span>

    <span data-ttu-id="63dc0-145">Metoda: login() Hello uruchamia uwierzytelniania z dostawcą hello.</span><span class="sxs-lookup"><span data-stu-id="63dc0-145">hello login() method starts authentication with hello provider.</span></span> <span data-ttu-id="63dc0-146">Metoda: login() Hello jest z funkcji asynchronicznych, która zwraca JavaScript Promise.</span><span class="sxs-lookup"><span data-stu-id="63dc0-146">hello login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="63dc0-147">rest Hello inicjowania hello jest umieszczony wewnątrz hello promise odpowiedź tak, aby nie jest wykonywany przed zakończeniem hello: login() metody.</span><span class="sxs-lookup"><span data-stu-id="63dc0-147">hello rest of hello initialization is placed inside hello promise response so that it is not executed until hello login() method completes.</span></span>

4. <span data-ttu-id="63dc0-148">W kodzie hello, który właśnie został dodany, Zastąp `SDK_Provider_Name` o nazwie hello dostawcy logowania.</span><span class="sxs-lookup"><span data-stu-id="63dc0-148">In hello code that you just added, replace `SDK_Provider_Name` with hello name of your login provider.</span></span> <span data-ttu-id="63dc0-149">Na przykład dla usługi Azure Active Directory, należy użyć `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="63dc0-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="63dc0-150">Uruchom projekt.</span><span class="sxs-lookup"><span data-stu-id="63dc0-150">Run your project.</span></span>  <span data-ttu-id="63dc0-151">Po zakończeniu projektu hello inicjowania aplikacji zawiera stronę logowania OAuth hello hello wybranego dostawcy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="63dc0-151">When hello project has finished initializing, your application shows hello OAuth login page for hello chosen authentication provider.</span></span>

## <span data-ttu-id="63dc0-152"><a name="next-steps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="63dc0-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="63dc0-153">Dowiedz się więcej [o uwierzytelniania] z usługi Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="63dc0-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="63dc0-154">Kontynuuj hello samouczek, dodając [powiadomień wypychanych] tooyour aplikacji oprogramowania Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="63dc0-154">Continue hello tutorial by adding [Push Notifications] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="63dc0-155">Dowiedz się, jak toouse hello zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="63dc0-155">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="63dc0-156">[Zestaw Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="63dc0-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="63dc0-157">[Zestaw ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="63dc0-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="63dc0-158">[Zestaw Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="63dc0-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
[Rozpoczynanie pracy z usługą Mobile Apps]: app-service-mobile-cordova-get-started.md
[zasadę zawartość dokumentacji]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[powiadomień wypychanych]: app-service-mobile-cordova-get-started-push.md
[o uwierzytelniania]: app-service-mobile-auth.md
[Zestaw Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[Zestaw ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Zestaw Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
