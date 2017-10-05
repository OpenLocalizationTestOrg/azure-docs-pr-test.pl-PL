---
title: "Dodawanie uwierzytelniania na Apache Cordova w usłudze Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak korzystać z aplikacji mobilnych w usłudze Azure App Service uwierzytelniać użytkowników aplikacji oprogramowania Apache Cordova za pomocą różnych dostawców tożsamości, obejmującej Google, Facebook, Twitter i Microsoft."
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
ms.openlocfilehash: b7362b7f26859de541f792e714502851d74c98e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-apache-cordova-app"></a><span data-ttu-id="a3f21-103">Dodawanie uwierzytelniania do aplikacji platformy Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="a3f21-103">Add authentication to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="a3f21-104">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a3f21-104">Summary</span></span>
<span data-ttu-id="a3f21-105">W tym samouczku należy dodać do listy zadań projektu szybkiego startu w programie Apache Cordova przy użyciu dostawcy tożsamości obsługiwanych uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a3f21-105">In this tutorial, you add authentication to the todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="a3f21-106">W tym samouczku jest oparta na [Rozpoczynanie pracy z usługą Mobile Apps] — samouczek, należy najpierw wykonać.</span><span class="sxs-lookup"><span data-stu-id="a3f21-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="a3f21-107"><a name="register"></a>Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="a3f21-107"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="a3f21-108">Obejrzyj wideo przedstawiające podobne kroki</span><span class="sxs-lookup"><span data-stu-id="a3f21-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="a3f21-109"><a name="permissions"></a>Ogranicz uprawnienia dla uwierzytelnionych użytkowników</span><span class="sxs-lookup"><span data-stu-id="a3f21-109"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="a3f21-110">Teraz można sprawdzić dostępu anonimowego z wewnętrzną bazą danych zostało wyłączone.</span><span class="sxs-lookup"><span data-stu-id="a3f21-110">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="a3f21-111">W programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="a3f21-111">In Visual Studio:</span></span>

* <span data-ttu-id="a3f21-112">Otwórz projekt, który został utworzony po ukończeniu samouczka [Rozpoczynanie pracy z usługą Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="a3f21-112">Open the project that you created when you completed the tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="a3f21-113">Uruchom aplikację w **Emulator systemu Google Android**.</span><span class="sxs-lookup"><span data-stu-id="a3f21-113">Run your application in the **Google Android Emulator**.</span></span>
* <span data-ttu-id="a3f21-114">Sprawdź, czy wystąpił nieoczekiwany błąd połączenia jest wyświetlany po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a3f21-114">Verify that an Unexpected Connection Failure is shown after the app starts.</span></span>

<span data-ttu-id="a3f21-115">Następnie zaktualizuj aplikację do uwierzytelniania użytkowników przed wysłaniem żądania zasobów z zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a3f21-115">Next, update the app to authenticate users before requesting resources from the Mobile App backend.</span></span>

## <span data-ttu-id="a3f21-116"><a name="add-authentication"></a>Dodawanie uwierzytelniania do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a3f21-116"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="a3f21-117">Otwórz projekt w **programu Visual Studio**, następnie otwórz `www/index.html` plik do edycji.</span><span class="sxs-lookup"><span data-stu-id="a3f21-117">Open your project in **Visual Studio**, then open the `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="a3f21-118">Zlokalizuj `Content-Security-Policy` metatag elementu head.</span><span class="sxs-lookup"><span data-stu-id="a3f21-118">Locate the `Content-Security-Policy` meta tag in the head section.</span></span>  <span data-ttu-id="a3f21-119">Dodaj hosta OAuth do listy dozwolonych źródeł.</span><span class="sxs-lookup"><span data-stu-id="a3f21-119">Add the OAuth host to the list of allowed sources.</span></span>

   | <span data-ttu-id="a3f21-120">Dostawca</span><span class="sxs-lookup"><span data-stu-id="a3f21-120">Provider</span></span> | <span data-ttu-id="a3f21-121">Nazwa dostawcy zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="a3f21-121">SDK Provider Name</span></span> | <span data-ttu-id="a3f21-122">OAuth Host</span><span class="sxs-lookup"><span data-stu-id="a3f21-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="a3f21-123">Usługa Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3f21-123">Azure Active Directory</span></span> | <span data-ttu-id="a3f21-124">usługi AAD</span><span class="sxs-lookup"><span data-stu-id="a3f21-124">aad</span></span> | <span data-ttu-id="a3f21-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="a3f21-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="a3f21-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="a3f21-126">Facebook</span></span> | <span data-ttu-id="a3f21-127">Usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="a3f21-127">facebook</span></span> | <span data-ttu-id="a3f21-128">https://www.Facebook.com</span><span class="sxs-lookup"><span data-stu-id="a3f21-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="a3f21-129">Google</span><span class="sxs-lookup"><span data-stu-id="a3f21-129">Google</span></span> | <span data-ttu-id="a3f21-130">Google</span><span class="sxs-lookup"><span data-stu-id="a3f21-130">google</span></span> | <span data-ttu-id="a3f21-131">https://accounts.Google.com</span><span class="sxs-lookup"><span data-stu-id="a3f21-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="a3f21-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="a3f21-132">Microsoft</span></span> | <span data-ttu-id="a3f21-133">MicrosoftAccount</span><span class="sxs-lookup"><span data-stu-id="a3f21-133">microsoftaccount</span></span> | <span data-ttu-id="a3f21-134">https://login.Live.com</span><span class="sxs-lookup"><span data-stu-id="a3f21-134">https://login.live.com</span></span> |
   | <span data-ttu-id="a3f21-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="a3f21-135">Twitter</span></span> | <span data-ttu-id="a3f21-136">W usłudze Twitter</span><span class="sxs-lookup"><span data-stu-id="a3f21-136">twitter</span></span> | <span data-ttu-id="a3f21-137">https://API.twitter.com</span><span class="sxs-lookup"><span data-stu-id="a3f21-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="a3f21-138">Przykład zawartość--zasady zabezpieczeń (zaimplementowany dla usługi Azure Active Directory) jest następujący:</span><span class="sxs-lookup"><span data-stu-id="a3f21-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="a3f21-139">Zastąp `https://login.microsoftonline.com` z hostem OAuth z powyższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="a3f21-139">Replace `https://login.microsoftonline.com` with the OAuth host from the preceding table.</span></span>  <span data-ttu-id="a3f21-140">Aby uzyskać więcej informacji o metatag zawartości zabezpieczeń zasad, zobacz [zasadę zawartość dokumentacji].</span><span class="sxs-lookup"><span data-stu-id="a3f21-140">For more information about the content-security-policy meta tag, see the [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="a3f21-141">Niektórzy dostawcy uwierzytelniania nie wymaga się, że zawartość zabezpieczeń zasady zostanie zmieniona, gdy na urządzeniach przenośnych odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="a3f21-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="a3f21-142">Na przykład żadnych zmian zawartości zabezpieczeń zasady są wymagane w przypadku przy użyciu uwierzytelniania serwisu Google na urządzeniu z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="a3f21-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="a3f21-143">Otwórz `www/js/index.js` pliku do edycji, Znajdź `onDeviceReady()` metody i w obszarze tworzenia klienta kodzie Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="a3f21-143">Open the `www/js/index.js` file for editing, locate the `onDeviceReady()` method, and under the client  creation code add the following code:</span></span>

        // Login to the service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="a3f21-144">Ten kod zastępuje istniejący kod, który tworzy odwołania do tabeli i odświeża interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a3f21-144">This code replaces the existing code that creates the table reference and refreshes the UI.</span></span>

    <span data-ttu-id="a3f21-145">Metoda: login() uruchamia uwierzytelniania z dostawcą.</span><span class="sxs-lookup"><span data-stu-id="a3f21-145">The login() method starts authentication with the provider.</span></span> <span data-ttu-id="a3f21-146">Metoda: login() jest z funkcji asynchronicznych, która zwraca JavaScript Promise.</span><span class="sxs-lookup"><span data-stu-id="a3f21-146">The login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="a3f21-147">Pozostałe inicjowanie jest umieszczony wewnątrz odpowiedzi promise, tak aby nie jest wykonywany przed zakończeniem metody: login().</span><span class="sxs-lookup"><span data-stu-id="a3f21-147">The rest of the initialization is placed inside the promise response so that it is not executed until the login() method completes.</span></span>

4. <span data-ttu-id="a3f21-148">W kodzie, który właśnie został dodany, Zastąp `SDK_Provider_Name` o nazwie dostawcą logowania.</span><span class="sxs-lookup"><span data-stu-id="a3f21-148">In the code that you just added, replace `SDK_Provider_Name` with the name of your login provider.</span></span> <span data-ttu-id="a3f21-149">Na przykład dla usługi Azure Active Directory, należy użyć `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="a3f21-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="a3f21-150">Uruchom projekt.</span><span class="sxs-lookup"><span data-stu-id="a3f21-150">Run your project.</span></span>  <span data-ttu-id="a3f21-151">Po zakończeniu projektu podczas inicjowania aplikacji zawiera strony logowania OAuth dla dostawcy uwierzytelniania wybrany.</span><span class="sxs-lookup"><span data-stu-id="a3f21-151">When the project has finished initializing, your application shows the OAuth login page for the chosen authentication provider.</span></span>

## <span data-ttu-id="a3f21-152"><a name="next-steps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a3f21-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="a3f21-153">Dowiedz się więcej [o uwierzytelniania] z usługi Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a3f21-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="a3f21-154">Kontynuuj samouczek, dodając [powiadomień wypychanych] do swojej aplikacji Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="a3f21-154">Continue the tutorial by adding [Push Notifications] to your Apache Cordova app.</span></span>

<span data-ttu-id="a3f21-155">Dowiedz się, jak korzystać z zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="a3f21-155">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="a3f21-156">[Zestaw Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="a3f21-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="a3f21-157">[Zestaw ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="a3f21-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="a3f21-158">[Zestaw Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="a3f21-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
<span data-ttu-id="a3f21-159">[Rozpoczynanie pracy z usługą Mobile Apps]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="a3f21-159">[Get started with Mobile Apps]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="a3f21-160">[zasadę zawartość dokumentacji]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span><span class="sxs-lookup"><span data-stu-id="a3f21-160">[Content-Security-Policy documentation]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html</span></span>
<span data-ttu-id="a3f21-161">[powiadomień wypychanych]: app-service-mobile-cordova-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="a3f21-161">[Push Notifications]: app-service-mobile-cordova-get-started-push.md</span></span>
<span data-ttu-id="a3f21-162">[o uwierzytelniania]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="a3f21-162">[About Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="a3f21-163">[Zestaw Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="a3f21-163">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="a3f21-164">[Zestaw ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="a3f21-164">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="a3f21-165">[Zestaw Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="a3f21-165">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>
