---
title: Wprowadzenie do uwierzytelniania dla aplikacji mobilnej w aplikacji platformy Xamarin Forms | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak korzystać z aplikacji mobilnej uwierzytelniać użytkowników aplikacji platformy Xamarin Forms za pomocą różnych dostawców tożsamości, obejmującej AAD, Google, Facebook, Twitter i Microsoft."
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
ms.openlocfilehash: 9e14e95793bcc81ad46783fd50ba223eec4ea360
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="add-authentication-to-your-xamarin-forms-app"></a><span data-ttu-id="deb1e-103">Dodawanie uwierzytelniania do aplikacji platformy Xamarin Forms</span><span class="sxs-lookup"><span data-stu-id="deb1e-103">Add authentication to your Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="deb1e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="deb1e-104">Overview</span></span>
<span data-ttu-id="deb1e-105">W tym temacie przedstawiono, jak uwierzytelniać użytkowników aplikacji usługi Mobile aplikacji z poziomu aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="deb1e-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="deb1e-106">W tym samouczku Dodawanie uwierzytelniania do projektu szybkiego startu Xamarin Forms przy użyciu dostawcy tożsamości, która jest obsługiwana przez usługę App Service.</span><span class="sxs-lookup"><span data-stu-id="deb1e-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="deb1e-107">Po pomyślnie trwa uwierzytelnieniu i autoryzacji w aplikacji mobilnej, jest wyświetlana wartość Identyfikatora użytkownika i będzie można uzyskać dostęp do danych tabeli ograniczone.</span><span class="sxs-lookup"><span data-stu-id="deb1e-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="deb1e-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="deb1e-108">Prerequisites</span></span>
<span data-ttu-id="deb1e-109">Aby uzyskać najlepsze wyniki z tego samouczka, zaleca się wykonanie [tworzenie aplikacji platformy Xamarin Forms] [ 1] samouczka.</span><span class="sxs-lookup"><span data-stu-id="deb1e-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="deb1e-110">Po ukończeniu tego samouczka, konieczne będzie projektu Xamarin Forms aplikacji TodoList wielu platform.</span><span class="sxs-lookup"><span data-stu-id="deb1e-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="deb1e-111">Jeśli nie używasz szybki start pobrany Projekt serwera, należy dodać pakietu rozszerzenia uwierzytelniania do projektu.</span><span class="sxs-lookup"><span data-stu-id="deb1e-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="deb1e-112">Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="deb1e-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="deb1e-113">Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="deb1e-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="deb1e-114"><a name="redirecturl"></a>Dodaj aplikację do dozwolonych przekierowania zewnętrzne adresy URL</span><span class="sxs-lookup"><span data-stu-id="deb1e-114"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="deb1e-115">Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deb1e-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="deb1e-116">Dzięki temu system uwierzytelniania przekierować z powrotem do aplikacji po zakończeniu procesu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="deb1e-116">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="deb1e-117">W tym samouczku używamy schemat adresu URL _appname_ w ciągu.</span><span class="sxs-lookup"><span data-stu-id="deb1e-117">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="deb1e-118">Można jednak użyć dowolnego wybranego schematu URL.</span><span class="sxs-lookup"><span data-stu-id="deb1e-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="deb1e-119">Powinien być unikatowy w aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="deb1e-119">It should be unique to your mobile application.</span></span> <span data-ttu-id="deb1e-120">Aby włączyć przekierowywanie po stronie serwera:</span><span class="sxs-lookup"><span data-stu-id="deb1e-120">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="deb1e-121">W [portalu Azure] wybierz usługę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deb1e-121">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="deb1e-122">Kliknij przycisk **uwierzytelniania / autoryzacji** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="deb1e-122">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="deb1e-123">W **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="deb1e-123">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="deb1e-124">**Url_scheme_of_your_app** w tym ciągu jest schemat adresu URL dla aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="deb1e-124">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="deb1e-125">Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).</span><span class="sxs-lookup"><span data-stu-id="deb1e-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="deb1e-126">Należy zanotuj ciąg, który wybrany jako trzeba będzie dostosować kodu aplikacji mobilnej przy użyciu schemat adresu URL w kilku miejscach.</span><span class="sxs-lookup"><span data-stu-id="deb1e-126">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="deb1e-127">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="deb1e-127">Click **OK**.</span></span>

5. <span data-ttu-id="deb1e-128">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="deb1e-128">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="deb1e-129">Ogranicz uprawnienia dla uwierzytelnionych użytkowników</span><span class="sxs-lookup"><span data-stu-id="deb1e-129">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-to-the-portable-class-library"></a><span data-ttu-id="deb1e-130">Dodawanie uwierzytelniania do biblioteki klas przenośnych</span><span class="sxs-lookup"><span data-stu-id="deb1e-130">Add authentication to the portable class library</span></span>
<span data-ttu-id="deb1e-131">Aplikacje mobilne używa [LoginAsync] [ 3] — metoda rozszerzenia na [MobileServiceClient] [ 4] do logowania użytkownika z usługi aplikacji uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="deb1e-131">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span></span> <span data-ttu-id="deb1e-132">W przykładzie użyto przepływ uwierzytelniania serwer zarządzany, który wyświetla dostawcy w interfejsie logowania w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deb1e-132">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span></span> <span data-ttu-id="deb1e-133">Aby uzyskać więcej informacji, zobacz [serwer zarządzany uwierzytelniania][5].</span><span class="sxs-lookup"><span data-stu-id="deb1e-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="deb1e-134">Aby zapewnić lepsze środowisko użytkownika w aplikacji produkcyjnej, należy rozważyć zamiast za pomocą [zarządzanych przez klienta uwierzytelniania][6].</span><span class="sxs-lookup"><span data-stu-id="deb1e-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="deb1e-135">Do uwierzytelniania za pomocą projektu Xamarin Forms, zdefiniuj **IAuthenticate** interfejsu przenośnej biblioteki klas dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deb1e-135">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span></span> <span data-ttu-id="deb1e-136">Następnie dodaj **logowania** przycisk interfejsu użytkownika zdefiniowane w przenośną bibliotekę klas kliknij, aby uruchomić uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="deb1e-136">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span></span> <span data-ttu-id="deb1e-137">Dane są ładowane z zaplecza aplikacji mobilnej po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="deb1e-137">Data is loaded from the mobile app backend after successful authentication.</span></span>

<span data-ttu-id="deb1e-138">Implementowanie **IAuthenticate** interfejs dla każdej platformy obsługiwane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="deb1e-138">Implement the **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="deb1e-139">W programie Visual Studio lub Xamarin Studio Otwórz App.cs z projektu o **przenośne** w nazwie, czyli projektu biblioteki przenośnej klasy, a następnie dodaj następujące `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="deb1e-139">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="deb1e-140">W App.cs, Dodaj następujący `IAuthenticate` definicji interfejsu bezpośrednio przed `App` definicji klasy.</span><span class="sxs-lookup"><span data-stu-id="deb1e-140">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="deb1e-141">Można zainicjować interfejsu z implementacją specyficzne dla platformy, należy dodać następujące statyczne elementy członkowskie do **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="deb1e-141">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="deb1e-142">Otwórz TodoList.xaml z projektu biblioteki klas przenośnych, należy dodać następujące **przycisk** element *buttonsPanel* elementu układu po istniejącego przycisku:</span><span class="sxs-lookup"><span data-stu-id="deb1e-142">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="deb1e-143">Ten przycisk wyzwala serwer zarządzany uwierzytelniania za pomocą zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="deb1e-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="deb1e-144">Otwórz TodoList.xaml.cs z projektu biblioteki klas przenośnych, a następnie dodaj poniższe pole, aby `TodoList` klasy:</span><span class="sxs-lookup"><span data-stu-id="deb1e-144">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span></span>

        // Track whether the user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="deb1e-145">Zastąp **OnAppearing** metodę z następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="deb1e-145">Replace the **OnAppearing** method with the following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems to true in order to synchronize the data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide the Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="deb1e-146">Ten kod upewnia się, że tylko odświeżania danych z usługi po Cię uwierzytelniono.</span><span class="sxs-lookup"><span data-stu-id="deb1e-146">This code makes sure that data is only refreshed from the service after you have been authenticated.</span></span>
7. <span data-ttu-id="deb1e-147">Dodaj następujące obsługę **kliknięto element** zdarzenia **TodoList** klasy:</span><span class="sxs-lookup"><span data-stu-id="deb1e-147">Add the following handler for the **Clicked** event to the **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems to true to synchronize the data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="deb1e-148">Zapisz zmiany i ponownie skompilować projekt przenośnej biblioteki klas weryfikowanie żadne błędy.</span><span class="sxs-lookup"><span data-stu-id="deb1e-148">Save your changes and rebuild the Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-to-the-android-app"></a><span data-ttu-id="deb1e-149">Dodawanie uwierzytelniania do aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="deb1e-149">Add authentication to the Android app</span></span>
<span data-ttu-id="deb1e-150">W tej sekcji przedstawiono sposób wykonania **IAuthenticate** interfejs w projekcie aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="deb1e-150">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span></span> <span data-ttu-id="deb1e-151">Pomiń tę sekcję, jeśli urządzenia z systemem Android nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="deb1e-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="deb1e-152">W programie Visual Studio lub Xamarin Studio kliknij prawym przyciskiem myszy **droid** projektu, następnie **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="deb1e-152">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="deb1e-153">Naciśnij klawisz F5, aby uruchomić projekt w debugerze, a następnie sprawdź, czy wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deb1e-153">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="deb1e-154">401 kod jest generowany, ponieważ dostęp do wewnętrznej bazy danych jest ograniczony tylko autoryzowanym użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="deb1e-154">The 401 code is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="deb1e-155">Otwórz MainActivity.cs w projekcie systemu Android i dodaj następujące `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="deb1e-155">Open MainActivity.cs in the Android project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="deb1e-156">Aktualizacja **MainActivity** klasy do zaimplementowania **IAuthenticate** interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="deb1e-156">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="deb1e-157">Aktualizacja **MainActivity** klasy, dodając **MobileServiceUser** pola i **Uwierzytelnij** metodę, która jest wymagana przez **IAuthenticate** interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="deb1e-157">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="deb1e-158">Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, wybierz inną wartość dla [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="deb1e-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="deb1e-159">Dodaj następujący kod wewnątrz <application> węzła AndroidManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="deb1e-159">Add the following code inside <application> node of AndroidManifest.xml:</span></span>

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

1. <span data-ttu-id="deb1e-160">Dodaj następujący kod do **OnCreate** metody **MainActivity** klasy przed wywołaniem do `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="deb1e-160">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="deb1e-161">Ten kod gwarantuje, że wystawca uwierzytelnienia jest inicjowana przed obciążeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deb1e-161">This code ensures the authenticator is initialized before the app loads.</span></span>
2. <span data-ttu-id="deb1e-162">Skompiluj ponownie aplikację, uruchom go, a następnie zaloguj się przy użyciu dostawcy uwierzytelniania wybraną i sprawdź, czy można uzyskać dostępu do danych jako użytkownik uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="deb1e-162">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-the-ios-app"></a><span data-ttu-id="deb1e-163">Dodawanie uwierzytelniania do aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="deb1e-163">Add authentication to the iOS app</span></span>
<span data-ttu-id="deb1e-164">W tej sekcji przedstawiono sposób wykonania **IAuthenticate** interfejs w projekcie aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="deb1e-164">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span></span> <span data-ttu-id="deb1e-165">Pomiń tę sekcję, jeśli urządzenia z systemem iOS nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="deb1e-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="deb1e-166">W programie Visual Studio lub Xamarin Studio kliknij prawym przyciskiem myszy **iOS** projektu, następnie **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="deb1e-166">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="deb1e-167">Naciśnij klawisz F5, aby uruchomić projekt w debugerze, a następnie sprawdź, czy wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deb1e-167">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="deb1e-168">Odpowiedzi 401 jest generowany, ponieważ dostęp do wewnętrznej bazy danych jest ograniczony tylko autoryzowanym użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="deb1e-168">The 401 response is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="deb1e-169">Otwórz AppDelegate.cs w projekcie systemu iOS i dodaj następujące `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="deb1e-169">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="deb1e-170">Aktualizacja **AppDelegate** klasy do zaimplementowania **IAuthenticate** interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="deb1e-170">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="deb1e-171">Aktualizacja **AppDelegate** klasy, dodając **MobileServiceUser** pola i **Uwierzytelnij** metodę, która jest wymagana przez **IAuthenticate** interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="deb1e-171">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="deb1e-172">Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, wybierz inną wartość dla [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="deb1e-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="deb1e-173">Aktualizacja klasy AppDelegate przez dodanie przeciążenie metody OpenUrl (Opcje NSDictionary aplikacji, nsurl oczekiwanego adresu url, UIApplication)</span><span class="sxs-lookup"><span data-stu-id="deb1e-173">Update the AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="deb1e-174">Dodaj następujący wiersz kodu w celu **FinishedLaunching** metody przed wywołanie `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="deb1e-174">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="deb1e-175">Ten kod gwarantuje, że wystawca uwierzytelnienia jest zainicjowany przed załadowaniem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deb1e-175">This code ensures the authenticator is initialized before the app is loaded.</span></span>

6. <span data-ttu-id="deb1e-176">Dodaj **{url_scheme_of_your_app}** do Schematy adresów URL w pliku Info.plist.</span><span class="sxs-lookup"><span data-stu-id="deb1e-176">Add **{url_scheme_of_your_app}** to URL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="deb1e-177">Skompiluj ponownie aplikację, uruchom go, a następnie zaloguj się przy użyciu dostawcy uwierzytelniania wybraną i sprawdź, czy można uzyskać dostępu do danych jako użytkownik uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="deb1e-177">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-windows-10-including-phone-app-projects"></a><span data-ttu-id="deb1e-178">Dodawanie uwierzytelniania do projektów aplikacji systemu Windows 10 (w tym telefon)</span><span class="sxs-lookup"><span data-stu-id="deb1e-178">Add authentication to Windows 10 (including Phone) app projects</span></span>
<span data-ttu-id="deb1e-179">W tej sekcji przedstawiono sposób wykonania **IAuthenticate** interfejsu w projektach aplikacji systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="deb1e-179">This section shows how to implement the **IAuthenticate** interface in the Windows 10 app projects.</span></span> <span data-ttu-id="deb1e-180">Zastosuj te same kroki dla projektów uniwersalnych platformy systemu Windows (UWP), ale przy użyciu **UWP** projektu (ze zmianami dostrzeżone).</span><span class="sxs-lookup"><span data-stu-id="deb1e-180">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span></span> <span data-ttu-id="deb1e-181">Pomiń tę sekcję, jeśli urządzenia z systemem Windows nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="deb1e-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="deb1e-182">"W programie Visual Studio, kliknij prawym przyciskiem myszy albo **UWP** projektu, następnie **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="deb1e-182">"In Visual Studio, right-click either the **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="deb1e-183">Naciśnij klawisz F5, aby uruchomić projekt w debugerze, a następnie sprawdź, czy wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deb1e-183">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="deb1e-184">Odpowiedzi 401 odbywa się, ponieważ dostęp do wewnętrznej bazy danych jest ograniczony tylko autoryzowanym użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="deb1e-184">The 401 response happens because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="deb1e-185">Otwórz MainPage.xaml.cs dla projektu aplikacji systemu Windows i dodaj następujące `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="deb1e-185">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="deb1e-186">Zastąp `<your_Portable_Class_Library_namespace>` z przestrzenią nazw biblioteki klas przenośnych.</span><span class="sxs-lookup"><span data-stu-id="deb1e-186">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
4. <span data-ttu-id="deb1e-187">Aktualizacja **MainPage** klasy do zaimplementowania **IAuthenticate** interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="deb1e-187">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="deb1e-188">Aktualizacja **MainPage** klasy, dodając **MobileServiceUser** pola i **Uwierzytelnij** metodę, która jest wymagana przez **IAuthenticate**interfejsu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="deb1e-188">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="deb1e-189">Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, wybierz inną wartość dla [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="deb1e-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="deb1e-190">Dodaj następujący wiersz kodu w Konstruktorze **MainPage** klasy przed wywołaniem do `LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="deb1e-190">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="deb1e-191">Zastąp `<your_Portable_Class_Library_namespace>` z przestrzenią nazw biblioteki klas przenośnych.</span><span class="sxs-lookup"><span data-stu-id="deb1e-191">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>

3. <span data-ttu-id="deb1e-192">Jeśli używasz **platformy uniwersalnej systemu Windows**, Dodaj następujący **OnActivated** zastąpienie metody **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="deb1e-192">If you are using **UWP**, add the following **OnActivated** method override to the **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="deb1e-193">Jeśli zastąpienie metody już istnieje, Dodaj warunkowego kod z poprzedniego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="deb1e-193">When the method override already exists, add the conditional code from the preceding snippet.</span></span>  <span data-ttu-id="deb1e-194">Ten kod nie jest wymagane dla projektów uniwersalnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="deb1e-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="deb1e-195">Dodaj **{url_scheme_of_your_app}** w Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="deb1e-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="deb1e-196">Skompiluj ponownie aplikację, uruchom go, a następnie zaloguj się przy użyciu dostawcy uwierzytelniania wybraną i sprawdź, czy można uzyskać dostępu do danych jako użytkownik uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="deb1e-196">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="deb1e-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="deb1e-197">Next steps</span></span>
<span data-ttu-id="deb1e-198">Teraz, aby ukończyć w tym samouczku uwierzytelnianie podstawowe, należy wziąć pod uwagę kontynuowanie na jedno z następujących samouczków:</span><span class="sxs-lookup"><span data-stu-id="deb1e-198">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="deb1e-199">Dodawanie powiadomień wypychanych do aplikacji</span><span class="sxs-lookup"><span data-stu-id="deb1e-199">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="deb1e-200">Dowiedz się, jak dodać obsługę powiadomień wypychanych do aplikacji i skonfigurować zaplecze Aplikacji mobilnej na potrzeby wysyłania powiadomień wypychanych przy użyciu usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="deb1e-200">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="deb1e-201">Włączanie synchronizacji w trybie offline dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="deb1e-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="deb1e-202">Dowiedz się, jak dodać aplikację przy użyciu zaplecza aplikacji mobilnej obsługi w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="deb1e-202">Learn how to add offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="deb1e-203">Synchronizacja w trybie offline umożliwia użytkownikom końcowym interakcję z aplikacji mobilnej — przeglądanie, dodawanie lub modyfikowanie danych — nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="deb1e-203">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
