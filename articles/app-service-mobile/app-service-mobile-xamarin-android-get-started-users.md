---
title: "aaaGet uruchomiony przy użyciu uwierzytelniania dla aplikacji mobilnych w dla systemu Xamarin Android"
description: "Dowiedz się, jak toouse Mobile Apps tooauthenticate użytkowników aplikacji platformy Xamarin Android za pomocą różnych dostawców tożsamości, obejmującej AAD, Google, Facebook, Twitter i firmy Microsoft."
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
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a><span data-ttu-id="9d7ff-103">Dodawanie aplikacji platformy Xamarin.Android tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="9d7ff-103">Add authentication tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="9d7ff-104">W tym temacie opisano sposób tooauthenticate użytkowników aplikacji mobilnych z aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-104">This topic shows you how tooauthenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="9d7ff-105">W tym samouczku należy dodać projekt szybkiego startu toohello uwierzytelniania przy użyciu dostawcy tożsamości, który jest obsługiwany przez usługi Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-105">In this tutorial, you add authentication toohello quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="9d7ff-106">Po trwa pomyślnym uwierzytelnieniu i autoryzacji w aplikacji mobilnej hello wartość Identyfikatora użytkownika hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-106">After being successfully authenticated and authorized in hello Mobile App, hello user ID value is displayed.</span></span>

<span data-ttu-id="9d7ff-107">W tym samouczku jest oparta na powitania aplikacja mobilna — Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-107">This tutorial is based on hello Mobile App quickstart.</span></span> <span data-ttu-id="9d7ff-108">Samouczek hello również najpierw musisz zakończyć [tworzenie aplikacji platformy Xamarin.Android].</span><span class="sxs-lookup"><span data-stu-id="9d7ff-108">You must also first complete hello tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="9d7ff-109">Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać projekt tooyour hello uwierzytelniania rozszerzenie pakietu.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-109">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="9d7ff-110">Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="9d7ff-110">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="9d7ff-111"><a name="register"></a>Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="9d7ff-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="9d7ff-112"><a name="redirecturl"></a>Dodaj adresy URL przekierowania zewnętrznych dozwolone Twojej aplikacji toohello</span><span class="sxs-lookup"><span data-stu-id="9d7ff-112"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="9d7ff-113">Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="9d7ff-114">Po zakończeniu procesu uwierzytelniania hello dzięki temu hello uwierzytelniania systemu tooredirect wstecz tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-114">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="9d7ff-115">W tym samouczku używamy schemat adresu URL hello _appname_ w ciągu.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-115">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="9d7ff-116">Można jednak użyć dowolnego wybranego schematu URL.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="9d7ff-117">Powinna być unikatowa tooyour aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-117">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="9d7ff-118">Przekierowanie hello tooenable na powitania po stronie serwera:</span><span class="sxs-lookup"><span data-stu-id="9d7ff-118">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="9d7ff-119">W hello [portalu Azure] wybierz usługę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-119">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="9d7ff-120">Kliknij przycisk hello **uwierzytelniania / autoryzacji** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-120">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="9d7ff-121">W hello **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-121">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="9d7ff-122">Witaj **url_scheme_of_your_app** w tym ciągu jest hello schemat adresu URL aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-122">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="9d7ff-123">Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).</span><span class="sxs-lookup"><span data-stu-id="9d7ff-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="9d7ff-124">Należy zanotuj ciąg hello, który możesz wybrać, ponieważ będzie potrzebny tooadjust kodu aplikacji mobilnej przy użyciu hello schemat adresu URL w kilku miejscach.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-124">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="9d7ff-125">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-125">Click **OK**.</span></span>

5. <span data-ttu-id="9d7ff-126">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-126">Click **Save**.</span></span>

## <span data-ttu-id="9d7ff-127"><a name="permissions"></a>Ogranicz uprawnienia tooauthenticated użytkowników</span><span class="sxs-lookup"><span data-stu-id="9d7ff-127"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="9d7ff-128">W programie Visual Studio lub Xamarin Studio Uruchom projekt klienta hello na urządzenia lub emulatora.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="9d7ff-129">Upewnij się, że wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="9d7ff-130">Dzieje się tak, ponieważ aplikacja hello prób tooaccess zaplecza aplikacji mobilnej jako nieuwierzytelniony użytkownik.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-130">This happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="9d7ff-131">Witaj *TodoItem* tabeli teraz wymaga uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-131">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="9d7ff-132">Następnie zaktualizuje powitania klienta aplikacji toorequest zasobów z zaplecza aplikacji mobilnej hello z uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-132">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="9d7ff-133"><a name="add-authentication"></a>Dodaj aplikację toohello uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="9d7ff-133"><a name="add-authentication"></a>Add authentication toohello app</span></span>
<span data-ttu-id="9d7ff-134">Aplikacja Hello jest toorequire zaktualizowanych użytkowników tootap hello **Zaloguj** przycisk i uwierzytelniania przed wyświetleniem danych.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-134">hello app is updated toorequire users tootap hello **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="9d7ff-135">Dodaj hello następującego kodu toohello **TodoActivity** klasy:</span><span class="sxs-lookup"><span data-stu-id="9d7ff-135">Add hello following code toohello **TodoActivity** class:</span></span>
   
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
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="9d7ff-136">Spowoduje to utworzenie nowego tooauthenticate — metoda użytkownika i metody obsługi nowej **Zaloguj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-136">This creates a new method tooauthenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="9d7ff-137">Użytkownik Hello w powyższym hello przykładowy kod jest uwierzytelniany przy użyciu identyfikatora logowania usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-137">hello user in hello example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="9d7ff-138">Okno dialogowe jest identyfikator użytkownika hello używane toodisplay raz uwierzytelnić.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-138">A dialog is used toodisplay hello user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9d7ff-139">Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, zmień wartość hello przekazano zbyt**LoginAsync** powyżej tooone następującego hello: *MicrosoftAccount*, *Twitter*, *Google*, lub *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-139">If you are using an identity provider other than Facebook, change hello value passed too**LoginAsync** above tooone of hello following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="9d7ff-140">W hello **OnCreate** metody, usuń lub hello komentarz po wierszu kodu:</span><span class="sxs-lookup"><span data-stu-id="9d7ff-140">In hello **OnCreate** method, delete or comment-out hello following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="9d7ff-141">W pliku Activity_To_Do.axml hello Dodaj następujące hello *odwoływały* przycisk definicji przed istniejących hello *AddItem* przycisk:</span><span class="sxs-lookup"><span data-stu-id="9d7ff-141">In hello Activity_To_Do.axml file, add hello following *LoginUser* button definition before hello existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="9d7ff-142">Dodaj hello następującego pliku zasobów Strings.xml toohello elementu:</span><span class="sxs-lookup"><span data-stu-id="9d7ff-142">Add hello following element toohello Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="9d7ff-143">Otwórz pliku AndroidManifest.xml hello, Dodaj hello następującego kodu wewnątrz `<application>` — element XML:</span><span class="sxs-lookup"><span data-stu-id="9d7ff-143">Open hello AndroidManifest.xml file, add hello following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="9d7ff-144">W programie Visual Studio lub Xamarin Studio Uruchom projekt klienta hello na urządzeniu lub emulatorze i zaloguj się przy użyciu dostawcy tożsamości wybrany.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-144">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="9d7ff-145">Pomyślnie zalogowany, aplikacji hello zostaną wyświetlone Identyfikatora logowania i hello Lista zadań do wykonania, a można udostępnić dane toohello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="9d7ff-145">When you are successfully logged-in, hello app will display your login ID and hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[tworzenie aplikacji platformy Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md