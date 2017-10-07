---
title: aaaGet uruchomiono z uwierzytelniania dla aplikacji mobilnej w aplikacji platformy Xamarin Forms | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Mobile Apps tooauthenticate użytkowników aplikacji platformy Xamarin Forms za pomocą różnych dostawców tożsamości, obejmującej AAD, Google, Facebook, Twitter i firmy Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a><span data-ttu-id="ab474-103">Dodaj aplikację platformy Xamarin Forms tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="ab474-103">Add authentication tooyour Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="ab474-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ab474-104">Overview</span></span>
<span data-ttu-id="ab474-105">W tym temacie opisano sposób tooauthenticate użytkowników aplikację usługi Mobile aplikacji z poziomu aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="ab474-105">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="ab474-106">W tym samouczku Dodawanie uwierzytelniania do projektu szybkiego startu Xamarin Forms hello przy użyciu dostawcy tożsamości, która jest obsługiwana przez usługę App Service.</span><span class="sxs-lookup"><span data-stu-id="ab474-106">In this tutorial, you add authentication to hello Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="ab474-107">Po pomyślnie trwa uwierzytelnieniu i autoryzacji w aplikacji mobilnej, jest wyświetlana wartość Identyfikatora użytkownika hello i będą mogli tooaccess ograniczone tabeli danych.</span><span class="sxs-lookup"><span data-stu-id="ab474-107">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed, and you will be able tooaccess restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab474-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ab474-108">Prerequisites</span></span>
<span data-ttu-id="ab474-109">Witaj najlepszych wyników z tego samouczka, zaleca się wykonanie hello [tworzenie aplikacji platformy Xamarin Forms] [ 1] samouczka.</span><span class="sxs-lookup"><span data-stu-id="ab474-109">For hello best result with this tutorial, we recommend that you first complete hello [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="ab474-110">Po ukończeniu tego samouczka, konieczne będzie projektu Xamarin Forms aplikacji TodoList wielu platform.</span><span class="sxs-lookup"><span data-stu-id="ab474-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="ab474-111">Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać projekt tooyour hello uwierzytelniania rozszerzenie pakietu.</span><span class="sxs-lookup"><span data-stu-id="ab474-111">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="ab474-112">Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="ab474-112">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="ab474-113">Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="ab474-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="ab474-114"><a name="redirecturl"></a>Dodaj adresy URL przekierowania zewnętrznych dozwolone Twojej aplikacji toohello</span><span class="sxs-lookup"><span data-stu-id="ab474-114"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="ab474-115">Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ab474-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="ab474-116">Po zakończeniu procesu uwierzytelniania hello dzięki temu hello uwierzytelniania systemu tooredirect wstecz tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ab474-116">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="ab474-117">W tym samouczku używamy schemat adresu URL hello _appname_ w ciągu.</span><span class="sxs-lookup"><span data-stu-id="ab474-117">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="ab474-118">Można jednak użyć dowolnego wybranego schematu URL.</span><span class="sxs-lookup"><span data-stu-id="ab474-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="ab474-119">Powinna być unikatowa tooyour aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="ab474-119">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="ab474-120">Przekierowanie hello tooenable na powitania po stronie serwera:</span><span class="sxs-lookup"><span data-stu-id="ab474-120">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="ab474-121">W hello [portalu Azure] wybierz usługę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ab474-121">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="ab474-122">Kliknij przycisk hello **uwierzytelniania / autoryzacji** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="ab474-122">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="ab474-123">W hello **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="ab474-123">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="ab474-124">Witaj **url_scheme_of_your_app** w tym ciągu jest hello schemat adresu URL aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="ab474-124">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="ab474-125">Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).</span><span class="sxs-lookup"><span data-stu-id="ab474-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="ab474-126">Należy zanotuj ciąg hello, który możesz wybrać, ponieważ będzie potrzebny tooadjust kodu aplikacji mobilnej przy użyciu hello schemat adresu URL w kilku miejscach.</span><span class="sxs-lookup"><span data-stu-id="ab474-126">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="ab474-127">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab474-127">Click **OK**.</span></span>

5. <span data-ttu-id="ab474-128">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ab474-128">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="ab474-129">Ogranicz uprawnienia tooauthenticated użytkowników</span><span class="sxs-lookup"><span data-stu-id="ab474-129">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a><span data-ttu-id="ab474-130">Dodawanie biblioteki klas przenośnych toohello uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="ab474-130">Add authentication toohello portable class library</span></span>
<span data-ttu-id="ab474-131">Aplikacje mobilne używa hello [LoginAsync] [ 3] — metoda rozszerzenia na powitania [MobileServiceClient] [ 4] toosign użytkownika z usługi aplikacji uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="ab474-131">Mobile Apps uses hello [LoginAsync][3] extension method on hello [MobileServiceClient][4] toosign in a user with App Service authentication.</span></span> <span data-ttu-id="ab474-132">W przykładzie użyto przepływ uwierzytelniania serwer zarządzany, który wyświetla dostawcy hello w interfejsie logowania w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ab474-132">This sample uses a server-managed authentication flow that displays hello provider's sign-in interface in hello app.</span></span> <span data-ttu-id="ab474-133">Aby uzyskać więcej informacji, zobacz [serwer zarządzany uwierzytelniania][5].</span><span class="sxs-lookup"><span data-stu-id="ab474-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="ab474-134">Aby zapewnić lepsze środowisko użytkownika w aplikacji produkcyjnej, należy rozważyć zamiast za pomocą [zarządzanych przez klienta uwierzytelniania][6].</span><span class="sxs-lookup"><span data-stu-id="ab474-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="ab474-135">Zdefiniuj tooauthenticate z projektem Xamarin Forms **IAuthenticate** interfejsu w hello przenośnej biblioteki klas dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ab474-135">tooauthenticate with a Xamarin Forms project, define an **IAuthenticate** interface in hello Portable Class Library for hello app.</span></span> <span data-ttu-id="ab474-136">Następnie dodaj **logowania** interfejsu użytkownika toohello przycisk zdefiniowane w hello przenośną bibliotekę klas, którego kliknięcie toostart uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="ab474-136">Then add a **Sign-in** button toohello user interface defined in hello Portable Class Library, which you click toostart authentication.</span></span> <span data-ttu-id="ab474-137">Dane są ładowane z zaplecza aplikacji mobilnej powitania po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="ab474-137">Data is loaded from hello mobile app backend after successful authentication.</span></span>

<span data-ttu-id="ab474-138">Implementowanie hello **IAuthenticate** interfejs dla każdej platformy obsługiwane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="ab474-138">Implement hello **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="ab474-139">W programie Visual Studio lub Xamarin Studio Otwórz App.cs z projektu hello z **przenośne** w polu Nazwa hello jest projektu biblioteki przenośnej klasy, a następnie dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="ab474-139">In Visual Studio or Xamarin Studio, open App.cs from hello project with **Portable** in hello name, which is Portable Class Library project, then  add hello following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="ab474-140">W App.cs, Dodaj następujące hello `IAuthenticate` definicji bezpośrednio przed hello interfejsu `App` definicji klasy.</span><span class="sxs-lookup"><span data-stu-id="ab474-140">In App.cs, add hello following `IAuthenticate` interface definition immediately before hello `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="ab474-141">Interfejs hello tooinitialize z implementacją specyficzne dla platformy, Dodaj powitania po toohello statyczne elementy członkowskie **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="ab474-141">tooinitialize hello interface with a platform-specific implementation, add hello following static members toohello **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="ab474-142">Otwórz TodoList.xaml z projektu biblioteki klas przenośnych hello, Dodaj następujące hello **przycisk** element hello *buttonsPanel* elementu układu po istniejącego przycisku hello:</span><span class="sxs-lookup"><span data-stu-id="ab474-142">Open TodoList.xaml from hello Portable Class Library project, add hello following **Button** element in hello *buttonsPanel* layout element, after hello existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="ab474-143">Ten przycisk wyzwala serwer zarządzany uwierzytelniania za pomocą zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="ab474-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="ab474-144">Otwórz TodoList.xaml.cs z projektu biblioteki klas przenośnych hello, a następnie dodaj następujące pola toohello hello `TodoList` klasy:</span><span class="sxs-lookup"><span data-stu-id="ab474-144">Open TodoList.xaml.cs from hello Portable Class Library project, then add hello following field toohello `TodoList` class:</span></span>

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="ab474-145">Zastąp hello **OnAppearing** metody z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="ab474-145">Replace hello **OnAppearing** method with hello following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="ab474-146">Ten kod upewnia się, że tylko odświeżania danych z usługi powitania po Cię uwierzytelniono.</span><span class="sxs-lookup"><span data-stu-id="ab474-146">This code makes sure that data is only refreshed from hello service after you have been authenticated.</span></span>
7. <span data-ttu-id="ab474-147">Dodaj powitania po obsługę hello **kliknięto element** toohello zdarzeń **TodoList** klasy:</span><span class="sxs-lookup"><span data-stu-id="ab474-147">Add hello following handler for hello **Clicked** event toohello **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="ab474-148">Zapisz zmiany i skompiluj ponownie projektu biblioteki klas przenośnych hello weryfikowanie żadne błędy.</span><span class="sxs-lookup"><span data-stu-id="ab474-148">Save your changes and rebuild hello Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-toohello-android-app"></a><span data-ttu-id="ab474-149">Dodawanie aplikacji dla systemu Android toohello uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="ab474-149">Add authentication toohello Android app</span></span>
<span data-ttu-id="ab474-150">W tej sekcji przedstawiono sposób tooimplement hello **IAuthenticate** interfejs w projekcie aplikacji systemu Android hello.</span><span class="sxs-lookup"><span data-stu-id="ab474-150">This section shows how tooimplement hello **IAuthenticate** interface in hello Android app project.</span></span> <span data-ttu-id="ab474-151">Pomiń tę sekcję, jeśli urządzenia z systemem Android nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ab474-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="ab474-152">W programie Visual Studio lub Xamarin Studio kliknij prawym przyciskiem myszy hello **droid** projektu, następnie **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="ab474-152">In Visual Studio or Xamarin Studio, right-click hello **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="ab474-153">Naciśnij klawisz F5 toostart hello projektu w debugerze hello, a następnie sprawdź, czy wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ab474-153">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="ab474-154">Kod 401 Hello jest generowany, ponieważ dostęp hello wewnętrznej bazy danych jest tylko użytkownicy tooauthorized ograniczone.</span><span class="sxs-lookup"><span data-stu-id="ab474-154">hello 401 code is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="ab474-155">Otwórz MainActivity.cs w hello projekt systemu Android i dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="ab474-155">Open MainActivity.cs in hello Android project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="ab474-156">Aktualizacja hello **MainActivity** hello tooimplement klasy **IAuthenticate** interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab474-156">Update hello **MainActivity** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="ab474-157">Aktualizacja hello **MainActivity** klasy, dodając **MobileServiceUser** pola i **Uwierzytelnij** metodę, która jest wymagana przez hello **IAuthenticate ** interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab474-157">Update hello **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="ab474-158">Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, wybierz inną wartość dla [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="ab474-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="ab474-159">Dodaj następujące kodu wewnątrz hello <application> węzła AndroidManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="ab474-159">Add hello following code inside <application> node of AndroidManifest.xml:</span></span>

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. <span data-ttu-id="ab474-160">Dodaj hello następującego kodu toohello **OnCreate** metody hello **MainActivity** klasy przed wywołaniem hello zbyt`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="ab474-160">Add hello following code toohello **OnCreate** method of hello **MainActivity** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="ab474-161">Ten kod gwarantuje, że wystawca uwierzytelnienia hello jest inicjowana przed obciążeń aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ab474-161">This code ensures hello authenticator is initialized before hello app loads.</span></span>
2. <span data-ttu-id="ab474-162">Odbuduj aplikacji hello, uruchom go, a następnie zaloguj się przy użyciu dostawcy uwierzytelniania hello wybranego i sprawdź, czy są możliwe tooaccess danych jako użytkownik uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="ab474-162">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toohello-ios-app"></a><span data-ttu-id="ab474-163">Dodawanie aplikacji dla systemu iOS toohello uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="ab474-163">Add authentication toohello iOS app</span></span>
<span data-ttu-id="ab474-164">W tej sekcji przedstawiono sposób tooimplement hello **IAuthenticate** interfejs w projekcie aplikacji systemu iOS hello.</span><span class="sxs-lookup"><span data-stu-id="ab474-164">This section shows how tooimplement hello **IAuthenticate** interface in hello iOS app project.</span></span> <span data-ttu-id="ab474-165">Pomiń tę sekcję, jeśli urządzenia z systemem iOS nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ab474-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="ab474-166">W programie Visual Studio lub Xamarin Studio kliknij prawym przyciskiem myszy hello **iOS** projektu, następnie **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="ab474-166">In Visual Studio or Xamarin Studio, right-click hello **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="ab474-167">Naciśnij klawisz F5 toostart hello projektu w debugerze hello, a następnie sprawdź, czy wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ab474-167">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="ab474-168">odpowiedzi 401 Hello jest generowany, ponieważ dostęp hello wewnętrznej bazy danych jest tylko użytkownicy tooauthorized ograniczone.</span><span class="sxs-lookup"><span data-stu-id="ab474-168">hello 401 response is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="ab474-169">Otwórz AppDelegate.cs w projekcie systemu iOS hello i dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="ab474-169">Open AppDelegate.cs in hello iOS project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="ab474-170">Aktualizacja hello **AppDelegate** hello tooimplement klasy **IAuthenticate** interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab474-170">Update hello **AppDelegate** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="ab474-171">Aktualizacja hello **AppDelegate** klasy, dodając **MobileServiceUser** pola i **Uwierzytelnij** metodę, która jest wymagana przez hello **IAuthenticate ** interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab474-171">Update hello **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="ab474-172">Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, wybierz inną wartość dla [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="ab474-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="ab474-173">Aktualizacja klasy AppDelegate hello przez dodanie przeciążenie metody OpenUrl (Opcje NSDictionary aplikacji, nsurl oczekiwanego adresu url, UIApplication)</span><span class="sxs-lookup"><span data-stu-id="ab474-173">Update hello AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="ab474-174">Dodaj powitania po wierszu kodu toohello **FinishedLaunching** za wywołanie metody przed hello`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="ab474-174">Add hello following line of code toohello **FinishedLaunching** method before hello call too`LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="ab474-175">Ten kod gwarantuje, że wystawca uwierzytelnienia hello jest zainicjowany przed załadowaniem aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ab474-175">This code ensures hello authenticator is initialized before hello app is loaded.</span></span>

6. <span data-ttu-id="ab474-176">Dodaj **{url_scheme_of_your_app}** tooURL programów w pliku Info.plist.</span><span class="sxs-lookup"><span data-stu-id="ab474-176">Add **{url_scheme_of_your_app}** tooURL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="ab474-177">Odbuduj aplikacji hello, uruchom go, a następnie zaloguj się przy użyciu dostawcy uwierzytelniania hello wybranego i sprawdź, czy są możliwe tooaccess danych jako użytkownik uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="ab474-177">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a><span data-ttu-id="ab474-178">Dodawanie uwierzytelniania tooWindows 10 (takie jak telefon) projekty aplikacji</span><span class="sxs-lookup"><span data-stu-id="ab474-178">Add authentication tooWindows 10 (including Phone) app projects</span></span>
<span data-ttu-id="ab474-179">W tej sekcji przedstawiono sposób tooimplement hello **IAuthenticate** interfejsu w projektach aplikacji hello systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="ab474-179">This section shows how tooimplement hello **IAuthenticate** interface in hello Windows 10 app projects.</span></span> <span data-ttu-id="ab474-180">Zastosuj te same czynności dla projektów uniwersalnych platformy systemu Windows (UWP), ale przy użyciu hello Hello **platformy uniwersalnej systemu Windows** projektu (ze zmianami dostrzeżone).</span><span class="sxs-lookup"><span data-stu-id="ab474-180">hello same steps apply for Universal Windows Platform (UWP) projects, but using hello **UWP** project (with noted changes).</span></span> <span data-ttu-id="ab474-181">Pomiń tę sekcję, jeśli urządzenia z systemem Windows nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ab474-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="ab474-182">"W programie Visual Studio, kliknij prawym przyciskiem myszy albo hello **UWP** projektu, następnie **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="ab474-182">"In Visual Studio, right-click either hello **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="ab474-183">Naciśnij klawisz F5 toostart hello projektu w debugerze hello, a następnie sprawdź, czy wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ab474-183">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="ab474-184">odpowiedzi 401 Hello odbywa się, ponieważ dostęp hello wewnętrznej bazy danych jest ograniczone tooauthorized tylko użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ab474-184">hello 401 response happens because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="ab474-185">Otwórz MainPage.xaml.cs dla projektu aplikacji Windows hello i dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="ab474-185">Open MainPage.xaml.cs for hello Windows app project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="ab474-186">Zastąp `<your_Portable_Class_Library_namespace>` z przestrzenią nazw hello biblioteki klas przenośnych.</span><span class="sxs-lookup"><span data-stu-id="ab474-186">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>
4. <span data-ttu-id="ab474-187">Aktualizacja hello **MainPage** hello tooimplement klasy **IAuthenticate** interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab474-187">Update hello **MainPage** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="ab474-188">Aktualizacja hello **MainPage** klasy, dodając **MobileServiceUser** pola i **Uwierzytelnij** metodę, która jest wymagana przez hello **IAuthenticate** interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab474-188">Update hello **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="ab474-189">Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, wybierz inną wartość dla [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="ab474-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="ab474-190">Dodaj następującego wiersza kodu w Konstruktorze hello hello hello **MainPage** klasy przed wywołaniem hello zbyt`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="ab474-190">Add hello following line of code in hello constructor for hello **MainPage** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="ab474-191">Zastąp `<your_Portable_Class_Library_namespace>` z przestrzenią nazw hello biblioteki klas przenośnych.</span><span class="sxs-lookup"><span data-stu-id="ab474-191">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>

3. <span data-ttu-id="ab474-192">Jeśli używasz **platformy uniwersalnej systemu Windows**, Dodaj następujące hello **OnActivated** metoda przesłania toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="ab474-192">If you are using **UWP**, add hello following **OnActivated** method override toohello **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="ab474-193">Zastąpienie metody hello już istnieje, należy dodać kodu warunkowego hello z hello poprzedzających fragment.</span><span class="sxs-lookup"><span data-stu-id="ab474-193">When hello method override already exists, add hello conditional code from hello preceding snippet.</span></span>  <span data-ttu-id="ab474-194">Ten kod nie jest wymagane dla projektów uniwersalnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ab474-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="ab474-195">Dodaj **{url_scheme_of_your_app}** w Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="ab474-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="ab474-196">Odbuduj aplikacji hello, uruchom go, a następnie zaloguj się przy użyciu dostawcy uwierzytelniania hello wybranego i sprawdź, czy są możliwe tooaccess danych jako użytkownik uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="ab474-196">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab474-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab474-197">Next steps</span></span>
<span data-ttu-id="ab474-198">Teraz, aby ukończyć w tym samouczku uwierzytelnianie podstawowe, należy wziąć pod uwagę kontynuować tooone hello następujące samouczki:</span><span class="sxs-lookup"><span data-stu-id="ab474-198">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="ab474-199">Dodaj aplikację tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="ab474-199">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="ab474-200">Dowiedz się, jak powiadomień wypychanych tooadd obsługują tooyour aplikacji i Konfigurowanie powiadomień wypychanych toosend usługi Azure Notification Hubs toouse aplikacji mobilnej wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ab474-200">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="ab474-201">Włączanie synchronizacji w trybie offline dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="ab474-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="ab474-202">Dowiedz się, jak w trybie offline tooadd obsługują aplikację przy użyciu zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="ab474-202">Learn how tooadd offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="ab474-203">Synchronizacja w trybie offline umożliwia toointeract użytkowników końcowych z aplikacji mobilnej — przeglądanie, dodawanie lub modyfikowanie danych — nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="ab474-203">Offline sync allows end users toointeract with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
