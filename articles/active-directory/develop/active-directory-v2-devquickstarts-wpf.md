---
title: "Natywnych aplikacji .NET v2.0 usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Sposób tworzenia natywnych aplikacji .NET i logowania użytkowników przy użyciu obu Account Microsoft i konta służbowego."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 7389f55ee6fef9548abb0ca4ac1bbd0399868d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-desktop-app"></a><span data-ttu-id="7cfa8-103">Dodaj logowanie do aplikacji Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="7cfa8-103">Add sign-in to a Windows Desktop app</span></span>
<span data-ttu-id="7cfa8-104">Z punktu końcowego v2.0, można szybko dodać uwierzytelniania aplikacji klasycznych z obsługą oba osobistego konta Microsoft i konta firmowego lub szkolnego.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-104">With the the v2.0 endpoint, you can quickly add authentication to your desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="7cfa8-105">Umożliwia również aplikacji do bezpiecznego komunikowania się z wewnętrznej bazy danych sieci web interfejsu api, a także [Microsoft Graph](https://graph.microsoft.io) i kilka [Office 365 Unified API](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="7cfa8-105">It also enables your app to securely communicate with a backend web api, as well as [the Microsoft Graph](https://graph.microsoft.io) and a few of the [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="7cfa8-106">Nie wszystkie scenariusze Azure Active Directory (AD) i funkcji obsługiwanych przez punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-106">Not all Azure Active Directory (AD) scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="7cfa8-107">Aby ustalić, czy należy używać punktu końcowego v2.0, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="7cfa8-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="7cfa8-108">Aby uzyskać [natywnych aplikacji .NET, na urządzeniu z systemem](active-directory-v2-flows.md#mobile-and-native-apps), usługa Azure AD zapewnia biblioteki uwierzytelniania tożsamości firmy Microsoft lub MSAL.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides the Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="7cfa8-109">Jedynym celem MSAL jego życia jest ułatwiają aplikację, aby uzyskać tokenów dla wywołania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-109">MSAL's sole purpose in life is to make it easy for your app to get tokens for calling web services.</span></span>  <span data-ttu-id="7cfa8-110">Aby zademonstrować, jak łatwo jest, w tym miejscu będzie budujemy aplikację listy zadań do wykonania WPF .NET który:</span><span class="sxs-lookup"><span data-stu-id="7cfa8-110">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="7cfa8-111">Pobiera dostęp do tokenów przy użyciu & loguje się użytkownik [protokół uwierzytelniania OAuth 2.0](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="7cfa8-111">Signs the user in & gets access tokens using the [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="7cfa8-112">Bezpieczne wywołania wewnętrznej bazy danych usługi sieci web listy zadań do wykonania, która jest również chroniony przez OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="7cfa8-113">Wylogowaniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-113">Signs the user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="7cfa8-114">Pobierz przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="7cfa8-114">Download sample code</span></span>
<span data-ttu-id="7cfa8-115">Kod używany w tym samouczku jest przechowywany [ w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="7cfa8-115">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="7cfa8-116">Aby z niego skorzystać, można [pobrać szkielet aplikacji w formie .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) lub sklonować szkielet:</span><span class="sxs-lookup"><span data-stu-id="7cfa8-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="7cfa8-117">Ukończonej aplikacji znajduje się na końcu również w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-117">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="7cfa8-118">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="7cfa8-118">Register an app</span></span>
<span data-ttu-id="7cfa8-119">Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="7cfa8-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="7cfa8-120">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="7cfa8-120">Make sure to:</span></span>

* <span data-ttu-id="7cfa8-121">Skopiuj **identyfikator aplikacji** przypisany do aplikacji, będzie on potrzebny wkrótce.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-121">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="7cfa8-122">Dodaj **Mobile** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-122">Add the **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="7cfa8-123">Instalowanie i konfigurowanie MSAL</span><span class="sxs-lookup"><span data-stu-id="7cfa8-123">Install & Configure MSAL</span></span>
<span data-ttu-id="7cfa8-124">Teraz, gdy masz aplikację w zarejestrowany z firmą Microsoft, można zainstalować MSAL i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="7cfa8-125">MSAL mieć możliwość komunikacji z punktem końcowym v2.0, należy dostarczyć informacji o rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-125">In order for MSAL to be able to communicate the v2.0 endpoint, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="7cfa8-126">Rozpocznij, dodając MSAL do projektu TodoListClient przy użyciu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-126">Begin by adding MSAL to the TodoListClient project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="7cfa8-127">W projekcie TodoListClient Otwórz `app.config`.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-127">In the TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="7cfa8-128">Zastąp wartości elementów w `<appSettings>` sekcji, aby odzwierciedlić wartości wejściowych do portalu rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-128">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the app registration portal.</span></span>  <span data-ttu-id="7cfa8-129">Kod będzie odwoływać tych wartości, przy każdym użyciu MSAL.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="7cfa8-130">`ida:ClientId` Jest **identyfikator aplikacji** aplikacji został skopiowany z portalu.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-130">The `ida:ClientId` is the **Application Id** of your app you copied from the portal.</span></span>
* <span data-ttu-id="7cfa8-131">W projekcie usługi TodoList Otwórz `web.config` w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-131">In the TodoList-Service project, open `web.config` in the root of the project.</span></span>  
  
  * <span data-ttu-id="7cfa8-132">Zastąp `ida:Audience` wartości o takim samym **identyfikator aplikacji** z portalu.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-132">Replace the `ida:Audience` value with the same **Application Id** from the portal.</span></span>

## <a name="use-msal-to-get-tokens"></a><span data-ttu-id="7cfa8-133">Aby uzyskać tokeny, użyj MSAL</span><span class="sxs-lookup"><span data-stu-id="7cfa8-133">Use MSAL to get tokens</span></span>
<span data-ttu-id="7cfa8-134">Podstawową zasadą za MSAL jest, że zawsze, gdy Twoja aplikacja powinna tokenu dostępu, należy po prostu wywołać `app.AcquireToken(...)`, i MSAL zajmie się resztą.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-134">The basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does the rest.</span></span>  

* <span data-ttu-id="7cfa8-135">W `TodoListClient` otwarciu projektu `MainWindow.xaml.cs` i Znajdź `OnInitialized(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-135">In the `TodoListClient` project, open `MainWindow.xaml.cs` and locate the `OnInitialized(...)` method.</span></span>  <span data-ttu-id="7cfa8-136">Pierwszym krokiem jest zainicjowanie aplikacji `PublicClientApplication` -MSAL dla klasy podstawowej reprezentujący natywnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-136">The first step is to initialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="7cfa8-137">Jest to, gdy przekazujesz MSAL współrzędne potrzebne do komunikowania się z usługą Azure AD i poinformuj go, jak pamięci podręcznej tokenów.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-137">This is where you pass MSAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="7cfa8-138">Podczas uruchamiania aplikacji, chcemy do sprawdzenia, czy użytkownik jest już zalogowany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-138">When the app starts up, we want to check and see if the user is already signed into the app.</span></span>  <span data-ttu-id="7cfa8-139">Jednak nie chcemy jeszcze wywołania interfejsu użytkownika logowania — wybierzemy użytkownika, kliknij przycisk "Zarejestruj" Aby to zrobić.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-139">However, we don't want to invoke a sign-in UI just yet - we'll make the user click "Sign In" to do so.</span></span>  <span data-ttu-id="7cfa8-140">Również w `OnInitialized(...)` metody:</span><span class="sxs-lookup"><span data-stu-id="7cfa8-140">Also in the `OnInitialized(...)` method:</span></span>

```C#
// As the app starts, we want to check to see if the user is already signed in.
// You can do so by trying to get a token from MSAL, using the method
// AcquireTokenSilent.  This forces MSAL to throw an exception if it cannot
// get a token for the user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in the cache - or MSAL was able to get a new oen via refresh token.
    // Proceed to fetch the user's tasks from the TodoListService via the GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, the app should take no action,
        // and simply show the user the sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* <span data-ttu-id="7cfa8-141">Jeśli użytkownik nie jest zalogowany i kliknięciu przycisku "Zaloguj", chcemy wywołania interfejsu użytkownika logowania i użytkownika, wprowadź swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-141">If the user is not signed in and they click the "Sign In" button, we want to invoke a login UI and have the user enter their credentials.</span></span>  <span data-ttu-id="7cfa8-142">Implementowanie obsługi przycisk Zaloguj:</span><span class="sxs-lookup"><span data-stu-id="7cfa8-142">Implement the Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign the user out if they clicked the "Clear Cache" button

// If the user clicked the 'Sign-In' button, force
// MSAL to prompt the user for credentials by using
// AcquireTokenAsync, a method that is guaranteed to show a prompt to the user.
// MSAL will get a token for the TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If the user canceled the login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by the user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* <span data-ttu-id="7cfa8-143">Jeśli użytkownik pomyślnie logowania, MSAL będą odbierać i pamięci podręcznej tokenu i można przejść do wywołania `GetTodoList()` metody bez obaw.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-143">If the user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed to call the `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="7cfa8-144">Pozostało można pobrać zadań użytkownika jest zaimplementowanie `GetTodoList()` metody.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-144">All that's left to get a user's tasks is to implement the `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try to get an access token to call the TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL to throw an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show the user a message
    // and let them click the Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once the token has been returned by MSAL,
// add it to the http authorization header,
// before making the call to access the To Do list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When the user is done managing their To-Do List, they may finally sign out of the app by clicking the "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If the user clicked the 'clear cache' button,
        // clear the MSAL token cache and show the user as signed out.
        // It's also necessary to clear the cookies from the browser
        // control so the next user has a chance to sign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a><span data-ttu-id="7cfa8-145">Uruchom polecenie</span><span class="sxs-lookup"><span data-stu-id="7cfa8-145">Run</span></span>
<span data-ttu-id="7cfa8-146">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="7cfa8-146">Congratulations!</span></span> <span data-ttu-id="7cfa8-147">Masz teraz aplikacji .NET WPF pracy, który ma możliwość uwierzytelniania użytkowników i bezpiecznie wywoływać interfejsy API sieci Web przy użyciu protokołu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-147">You now have a working .NET WPF app that has the ability to authenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="7cfa8-148">Uruchom oba projekty i zaloguj się za pomocą osobistego konta Microsoft lub konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="7cfa8-149">Dodawanie zadań do listy zadań do wykonania tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-149">Add tasks to that user's To-Do list.</span></span>  <span data-ttu-id="7cfa8-150">Wyloguj się i zaloguj się ponownie jako inny użytkownik, aby wyświetlić ich listy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-150">Sign out, and sign back in as another user to view their To-Do list.</span></span>  <span data-ttu-id="7cfa8-151">Zamknij aplikację i uruchom je ponownie.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-151">Close the app, and re-run it.</span></span>  <span data-ttu-id="7cfa8-152">Zwróć uwagę, jak sesji użytkownika pozostanie niezmieniona — to aplikacja przechowuje w pamięci podręcznej tokenów w pliku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-152">Notice how the user's session remains intact - that is because the app caches tokens in a local file.</span></span>

<span data-ttu-id="7cfa8-153">MSAL można łatwo zastosować wspólne funkcje tożsamości w aplikacji, za pomocą konta osobiste oraz firmowe.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-153">MSAL makes it easy to incorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="7cfa8-154">Zapewnia obsługę pracy dirty dla Ciebie — Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający użytkownika za pomocą interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-154">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="7cfa8-155">Tak naprawdę trzeba wiedzieć jednego wywołania interfejsu API, jest `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-155">All you really need to know is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="7cfa8-156">Próbka ukończone (bez wartości konfiguracji) [jest dostarczane jako zip w tym miejscu](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), lub można ją sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="7cfa8-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="7cfa8-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7cfa8-157">Next steps</span></span>
<span data-ttu-id="7cfa8-158">Możesz teraz przejść do bardziej zaawansowanych tematów.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="7cfa8-159">Można spróbować:</span><span class="sxs-lookup"><span data-stu-id="7cfa8-159">You may want to try:</span></span>

* [<span data-ttu-id="7cfa8-160">Zabezpieczanie interfejsu API sieci Web TodoListService z punktem końcowym v2.0</span><span class="sxs-lookup"><span data-stu-id="7cfa8-160">Securing the TodoListService Web API with the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="7cfa8-161">Aby uzyskać dodatkowe zasoby Zobacz:</span><span class="sxs-lookup"><span data-stu-id="7cfa8-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="7cfa8-162">Przewodnik dewelopera v2.0 >></span><span class="sxs-lookup"><span data-stu-id="7cfa8-162">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="7cfa8-163">Tag "msal" StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="7cfa8-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="7cfa8-164">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="7cfa8-164">Get security updates for our products</span></span>
<span data-ttu-id="7cfa8-165">Firma Microsoft zachęca do przekazywania powiadomień o występujących incydentach zabezpieczeń poprzez wizytę na [tej stronie](https://technet.microsoft.com/security/dd252948) i subskrybowanie Doradczych alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="7cfa8-165">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

