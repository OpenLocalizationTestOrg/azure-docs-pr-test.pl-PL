---
title: Wprowadzenie do uwierzytelniania dla aplikacji mobilnych w dla systemu Xamarin Android
description: "Dowiedz się, jak korzystać z aplikacji mobilnej uwierzytelniać użytkowników aplikacji platformy Xamarin Android za pomocą różnych dostawców tożsamości, obejmującej AAD, Google, Facebook, Twitter i Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 8f9a1109018c708d52cdcb7b8bce43861cecd31c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinandroid-app"></a><span data-ttu-id="5cdd7-103">Dodawanie uwierzytelniania do aplikacji platformy Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="5cdd7-103">Add authentication to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="5cdd7-104">W tym temacie przedstawiono, jak uwierzytelniać użytkowników aplikacji mobilnych z aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-104">This topic shows you how to authenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="5cdd7-105">W tym samouczku należy dodać do projektu szybkiego startu przy użyciu dostawcy tożsamości, który jest obsługiwany przez usługi Azure Mobile Apps uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-105">In this tutorial, you add authentication to the quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="5cdd7-106">Po pomyślnie trwa uwierzytelnieniu i autoryzacji w aplikacji mobilnej, jest wyświetlana wartość Identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-106">After being successfully authenticated and authorized in the Mobile App, the user ID value is displayed.</span></span>

<span data-ttu-id="5cdd7-107">W tym samouczku jest oparta na aplikacja mobilna — Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-107">This tutorial is based on the Mobile App quickstart.</span></span> <span data-ttu-id="5cdd7-108">Należy również najpierw Ukończ samouczek [tworzenie aplikacji platformy Xamarin.Android].</span><span class="sxs-lookup"><span data-stu-id="5cdd7-108">You must also first complete the tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="5cdd7-109">Jeśli nie używasz szybki start pobrany Projekt serwera, należy dodać pakietu rozszerzenia uwierzytelniania do projektu.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-109">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="5cdd7-110">Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5cdd7-110">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="5cdd7-111"><a name="register"></a>Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="5cdd7-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="5cdd7-112"><a name="redirecturl"></a>Dodaj aplikację do dozwolonych przekierowania zewnętrzne adresy URL</span><span class="sxs-lookup"><span data-stu-id="5cdd7-112"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="5cdd7-113">Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="5cdd7-114">Dzięki temu system uwierzytelniania przekierować z powrotem do aplikacji po zakończeniu procesu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-114">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="5cdd7-115">W tym samouczku używamy schemat adresu URL _appname_ w ciągu.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-115">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="5cdd7-116">Można jednak użyć dowolnego wybranego schematu URL.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="5cdd7-117">Powinien być unikatowy w aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-117">It should be unique to your mobile application.</span></span> <span data-ttu-id="5cdd7-118">Aby włączyć przekierowywanie po stronie serwera:</span><span class="sxs-lookup"><span data-stu-id="5cdd7-118">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="5cdd7-119">W [portalu Azure] wybierz usługę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-119">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="5cdd7-120">Kliknij przycisk **uwierzytelniania / autoryzacji** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-120">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="5cdd7-121">W **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-121">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="5cdd7-122">**Url_scheme_of_your_app** w tym ciągu jest schemat adresu URL dla aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-122">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="5cdd7-123">Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).</span><span class="sxs-lookup"><span data-stu-id="5cdd7-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="5cdd7-124">Należy zanotuj ciąg, który wybrany jako trzeba będzie dostosować kodu aplikacji mobilnej przy użyciu schemat adresu URL w kilku miejscach.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-124">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="5cdd7-125">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-125">Click **OK**.</span></span>

5. <span data-ttu-id="5cdd7-126">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-126">Click **Save**.</span></span>

## <span data-ttu-id="5cdd7-127"><a name="permissions"></a>Ogranicz uprawnienia dla uwierzytelnionych użytkowników</span><span class="sxs-lookup"><span data-stu-id="5cdd7-127"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="5cdd7-128">W programie Visual Studio lub Xamarin Studio uruchamianie projektu klienta na urządzenia lub emulatora.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="5cdd7-129">Upewnij się, że wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="5cdd7-130">Dzieje się tak, ponieważ aplikacja próbuje uzyskać dostęp jako użytkownik nieuwierzytelniony zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-130">This happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="5cdd7-131">*TodoItem* tabeli teraz wymaga uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-131">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="5cdd7-132">Następnie możesz zaktualizuje aplikacji klienckiej żądania zasobów z zaplecza aplikacji mobilnej z uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-132">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="5cdd7-133"><a name="add-authentication"></a>Dodawanie uwierzytelniania do aplikacji</span><span class="sxs-lookup"><span data-stu-id="5cdd7-133"><a name="add-authentication"></a>Add authentication to the app</span></span>
<span data-ttu-id="5cdd7-134">Gdy aplikacja jest zaktualizowana, aby wymagać od użytkowników wybierz **Zaloguj** przycisk i uwierzytelniania przed wyświetleniem danych.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-134">The app is updated to require users to tap the **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="5cdd7-135">Dodaj następujący kod do **TodoActivity** klasy:</span><span class="sxs-lookup"><span data-stu-id="5cdd7-135">Add the following code to the **TodoActivity** class:</span></span>
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide the button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load the data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="5cdd7-136">Spowoduje to utworzenie nowej metody do uwierzytelniania użytkownika i metody obsługi nowej **Zaloguj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-136">This creates a new method to authenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="5cdd7-137">W powyższym przykładowym kodzie użytkownika jest uwierzytelniany przy użyciu identyfikatora logowania usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-137">The user in the example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="5cdd7-138">Okno dialogowe służy do wyświetlania raz uwierzytelnić użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-138">A dialog is used to display the user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5cdd7-139">Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, zmień wartość przekazana do **LoginAsync** powyżej do jednej z następujących czynności: *MicrosoftAccount*, *Twitter*, *Google*, lub *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-139">If you are using an identity provider other than Facebook, change the value passed to **LoginAsync** above to one of the following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="5cdd7-140">W **OnCreate** metody, usunąć lub komentarz następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="5cdd7-140">In the **OnCreate** method, delete or comment-out the following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="5cdd7-141">W pliku Activity_To_Do.axml, Dodaj następujący *odwoływały* przycisk definicji przed istniejące *AddItem* przycisk:</span><span class="sxs-lookup"><span data-stu-id="5cdd7-141">In the Activity_To_Do.axml file, add the following *LoginUser* button definition before the existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="5cdd7-142">Dodaj następujący element do pliku zasobów Strings.xml:</span><span class="sxs-lookup"><span data-stu-id="5cdd7-142">Add the following element to the Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="5cdd7-143">Otwórz plik AndroidManifest.xml, Dodaj następujący kod wewnątrz `<application>` — element XML:</span><span class="sxs-lookup"><span data-stu-id="5cdd7-143">Open the AndroidManifest.xml file, add the following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="5cdd7-144">W programie Visual Studio lub Xamarin Studio uruchamianie projektu klienta na urządzeniu lub emulatorze i zaloguj się przy użyciu dostawcy tożsamości wybrany.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-144">In Visual Studio or Xamarin Studio, run the client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="5cdd7-145">Pomyślnie zalogowany, aplikacja wyświetli Identyfikatora logowania i Lista zadań do wykonania, i umożliwia aktualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="5cdd7-145">When you are successfully logged-in, the app will display your login ID and the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
<span data-ttu-id="5cdd7-146">[tworzenie aplikacji platformy Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="5cdd7-146">[Create a Xamarin.Android app]: app-service-mobile-xamarin-android-get-started.md</span></span>