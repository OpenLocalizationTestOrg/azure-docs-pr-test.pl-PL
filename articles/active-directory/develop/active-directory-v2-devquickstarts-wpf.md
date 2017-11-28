---
title: "v2.0 usługi Active Directory aaaAzure natywnych aplikacji .NET | Dokumentacja firmy Microsoft"
description: "Jak toobuild natywnych aplikacji .NET który loguje się użytkowników z obu Account firmy Microsoft i konta firmowego lub szkolnego."
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
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a><span data-ttu-id="3636a-103">Dodaj tooa logowania w aplikacji Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="3636a-103">Add sign-in tooa Windows Desktop app</span></span>
<span data-ttu-id="3636a-104">Z punktem końcowym v2.0 hello hello można szybko dodać uwierzytelniania aplikacji klasycznych tooyour o obsługę zarówno osobistego konta Microsoft i konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="3636a-104">With hello hello v2.0 endpoint, you can quickly add authentication tooyour desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="3636a-105">On również umożliwia toosecurely Twojej aplikacji komunikować się z wewnętrznej bazy danych w sieci web interfejsu api, a także [hello Microsoft Graph](https://graph.microsoft.io) i kilka hello [Office 365 Unified API](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="3636a-105">It also enables your app toosecurely communicate with a backend web api, as well as [hello Microsoft Graph](https://graph.microsoft.io) and a few of hello [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="3636a-106">Nie wszystkie scenariusze Azure Active Directory (AD) i funkcji obsługiwanych przez hello punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="3636a-106">Not all Azure Active Directory (AD) scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="3636a-107">toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3636a-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="3636a-108">Aby uzyskać [natywnych aplikacji .NET, na urządzeniu z systemem](active-directory-v2-flows.md#mobile-and-native-apps), usługa Azure AD zapewnia hello biblioteki uwierzytelniania tożsamości firmy Microsoft lub MSAL.</span><span class="sxs-lookup"><span data-stu-id="3636a-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides hello Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="3636a-109">Jedynym celem MSAL jego życia jest toomake ułatwiają dla twojej aplikacji tooget tokeny wywoływania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="3636a-109">MSAL's sole purpose in life is toomake it easy for your app tooget tokens for calling web services.</span></span>  <span data-ttu-id="3636a-110">toodemonstrate Ci, jak łatwo jest, w tym miejscu będzie budujemy aplikację listy zadań do wykonania WPF .NET który:</span><span class="sxs-lookup"><span data-stu-id="3636a-110">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="3636a-111">Pobiera dostęp do tokenów przy użyciu hello & znaki hello użytkownika w [protokół uwierzytelniania OAuth 2.0](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="3636a-111">Signs hello user in & gets access tokens using hello [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="3636a-112">Bezpieczne wywołania wewnętrznej bazy danych usługi sieci web listy zadań do wykonania, która jest również chroniony przez OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3636a-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="3636a-113">Znaki hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3636a-113">Signs hello user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="3636a-114">Pobierz przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="3636a-114">Download sample code</span></span>
<span data-ttu-id="3636a-115">Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="3636a-115">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="3636a-116">toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) lub klonowania hello szkielet:</span><span class="sxs-lookup"><span data-stu-id="3636a-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="3636a-117">ukończyć powitalnych aplikacji znajduje się na końcu hello również w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="3636a-117">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="3636a-118">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="3636a-118">Register an app</span></span>
<span data-ttu-id="3636a-119">Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="3636a-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="3636a-120">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="3636a-120">Make sure to:</span></span>

* <span data-ttu-id="3636a-121">Skopiuj hello **identyfikator aplikacji** przypisany tooyour aplikacji, będzie on potrzebny wkrótce.</span><span class="sxs-lookup"><span data-stu-id="3636a-121">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="3636a-122">Dodaj hello **Mobile** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3636a-122">Add hello **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="3636a-123">Instalowanie i konfigurowanie MSAL</span><span class="sxs-lookup"><span data-stu-id="3636a-123">Install & Configure MSAL</span></span>
<span data-ttu-id="3636a-124">Teraz, gdy masz aplikację w zarejestrowany z firmą Microsoft, można zainstalować MSAL i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3636a-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="3636a-125">Aby dla punktu końcowego v2.0 hello MSAL toobe toocommunicate stanie, należy tooprovide go niektóre informacje o rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3636a-125">In order for MSAL toobe able toocommunicate hello v2.0 endpoint, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="3636a-126">Rozpocznij, dodając projektu TodoListClient toohello MSAL przy użyciu konsoli Menedżera pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="3636a-126">Begin by adding MSAL toohello TodoListClient project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="3636a-127">W projekcie TodoListClient hello Otwórz `app.config`.</span><span class="sxs-lookup"><span data-stu-id="3636a-127">In hello TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="3636a-128">Zastąp wartości hello elementów hello na powitania `<appSettings>` hello tooreflect sekcji wartości danych wejściowych do portalu rejestracji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3636a-128">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello app registration portal.</span></span>  <span data-ttu-id="3636a-129">Kod będzie odwoływać tych wartości, przy każdym użyciu MSAL.</span><span class="sxs-lookup"><span data-stu-id="3636a-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="3636a-130">Witaj `ida:ClientId` jest hello **identyfikator aplikacji** skopiowany z portalu hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3636a-130">hello `ida:ClientId` is hello **Application Id** of your app you copied from hello portal.</span></span>
* <span data-ttu-id="3636a-131">W projekcie hello listy zadań usługi, otwórz `web.config` w katalogu głównym hello hello projektu.</span><span class="sxs-lookup"><span data-stu-id="3636a-131">In hello TodoList-Service project, open `web.config` in hello root of hello project.</span></span>  
  
  * <span data-ttu-id="3636a-132">Zastąp hello `ida:Audience` wartości z hello sam **identyfikator aplikacji** hello portalu.</span><span class="sxs-lookup"><span data-stu-id="3636a-132">Replace hello `ida:Audience` value with hello same **Application Id** from hello portal.</span></span>

## <a name="use-msal-tooget-tokens"></a><span data-ttu-id="3636a-133">Używaj tokenów tooget MSAL</span><span class="sxs-lookup"><span data-stu-id="3636a-133">Use MSAL tooget tokens</span></span>
<span data-ttu-id="3636a-134">Witaj podstawową zasadą za MSAL jest zawsze, gdy Twoja aplikacja powinna tokenu dostępu, po prostu telefoniczne skontaktowanie się z `app.AcquireToken(...)`, i MSAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="3636a-134">hello basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does hello rest.</span></span>  

* <span data-ttu-id="3636a-135">W hello `TodoListClient` otwarciu projektu `MainWindow.xaml.cs` i Znajdź hello `OnInitialized(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="3636a-135">In hello `TodoListClient` project, open `MainWindow.xaml.cs` and locate hello `OnInitialized(...)` method.</span></span>  <span data-ttu-id="3636a-136">pierwszym krokiem Hello jest tooinitialize aplikacji `PublicClientApplication` -MSAL dla klasy podstawowej reprezentujący natywnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3636a-136">hello first step is tooinitialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="3636a-137">Jest to, gdy przekazujesz MSAL hello współrzędne musi toocommunicate z usługą Azure AD i poinformuj go jak toocache tokenów.</span><span class="sxs-lookup"><span data-stu-id="3636a-137">This is where you pass MSAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="3636a-138">Po uruchomieniu aplikacji hello, firma Microsoft ma toocheck i zobacz, jeśli użytkownik hello jest już zalogowany do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3636a-138">When hello app starts up, we want toocheck and see if hello user is already signed into hello app.</span></span>  <span data-ttu-id="3636a-139">Jednak nie chcemy jeszcze tooinvoke interfejsu użytkownika logowania — wybierzemy hello użytkownika, kliknij przycisk "Zaloguj" toodo tak.</span><span class="sxs-lookup"><span data-stu-id="3636a-139">However, we don't want tooinvoke a sign-in UI just yet - we'll make hello user click "Sign In" toodo so.</span></span>  <span data-ttu-id="3636a-140">Również w hello `OnInitialized(...)` metody:</span><span class="sxs-lookup"><span data-stu-id="3636a-140">Also in hello `OnInitialized(...)` method:</span></span>

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
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

* <span data-ttu-id="3636a-141">Jeśli hello użytkownik nie jest zalogowany i kliknięciu przycisku "Zaloguj" hello, firma Microsoft ma tooinvoke logowania interfejsu użytkownika i użytkownik hello wprowadzić swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="3636a-141">If hello user is not signed in and they click hello "Sign In" button, we want tooinvoke a login UI and have hello user enter their credentials.</span></span>  <span data-ttu-id="3636a-142">Implementowanie obsługi przycisk hello logowania:</span><span class="sxs-lookup"><span data-stu-id="3636a-142">Implement hello Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

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
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
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

* <span data-ttu-id="3636a-143">Jeśli hello pomyślnym zalogowaniu się użytkownika, MSAL będą odbierać i pamięci podręcznej tokenu i można kontynuować toocall hello `GetTodoList()` metody bez obaw.</span><span class="sxs-lookup"><span data-stu-id="3636a-143">If hello user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed toocall hello `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="3636a-144">Opuścił tooget zadań użytkownika jest tooimplement hello `GetTodoList()` metody.</span><span class="sxs-lookup"><span data-stu-id="3636a-144">All that's left tooget a user's tasks is tooimplement hello `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

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

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

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

## <a name="run"></a><span data-ttu-id="3636a-145">Uruchom polecenie</span><span class="sxs-lookup"><span data-stu-id="3636a-145">Run</span></span>
<span data-ttu-id="3636a-146">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="3636a-146">Congratulations!</span></span> <span data-ttu-id="3636a-147">Teraz mieć również działający w aplikacji .NET WPF, który ma hello możliwości tooauthenticate użytkowników i bezpiecznie wywoływać interfejsy API sieci Web przy użyciu protokołu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3636a-147">You now have a working .NET WPF app that has hello ability tooauthenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="3636a-148">Uruchom oba projekty i zaloguj się za pomocą osobistego konta Microsoft lub konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="3636a-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="3636a-149">Dodawanie listy zadań do wykonania zadania toothat użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3636a-149">Add tasks toothat user's To-Do list.</span></span>  <span data-ttu-id="3636a-150">Wyloguj się i zaloguj się ponownie jako inny użytkownik tooview ich listy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="3636a-150">Sign out, and sign back in as another user tooview their To-Do list.</span></span>  <span data-ttu-id="3636a-151">Aplikacja hello Zamknij i uruchom je ponownie.</span><span class="sxs-lookup"><span data-stu-id="3636a-151">Close hello app, and re-run it.</span></span>  <span data-ttu-id="3636a-152">Zwróć uwagę, jak hello sesja pozostanie niezmieniona — to aplikacja hello buforuje tokenów w pliku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="3636a-152">Notice how hello user's session remains intact - that is because hello app caches tokens in a local file.</span></span>

<span data-ttu-id="3636a-153">MSAL umożliwia łatwe tooincorporate wspólne funkcje tożsamości w aplikacji, za pomocą konta osobiste oraz firmowe.</span><span class="sxs-lookup"><span data-stu-id="3636a-153">MSAL makes it easy tooincorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="3636a-154">Zapewnia obsługę wszystkich hello dirty pracy dla Ciebie — Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika za pomocą interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="3636a-154">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="3636a-155">Naprawdę tooknow wystarczy jednego wywołania interfejsu API, `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="3636a-155">All you really need tooknow is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="3636a-156">Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostarczane jako zip w tym miejscu](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), lub można ją sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="3636a-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="3636a-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3636a-157">Next steps</span></span>
<span data-ttu-id="3636a-158">Możesz teraz przejść do bardziej zaawansowanych tematów.</span><span class="sxs-lookup"><span data-stu-id="3636a-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="3636a-159">Można tootry:</span><span class="sxs-lookup"><span data-stu-id="3636a-159">You may want tootry:</span></span>

* [<span data-ttu-id="3636a-160">Zabezpieczanie hello TodoListService interfejsu API sieci Web z punktem końcowym v2.0 hello</span><span class="sxs-lookup"><span data-stu-id="3636a-160">Securing hello TodoListService Web API with hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="3636a-161">Aby uzyskać dodatkowe zasoby Zobacz:</span><span class="sxs-lookup"><span data-stu-id="3636a-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="3636a-162">Przewodnik dewelopera v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="3636a-162">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="3636a-163">Tag "msal" StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="3636a-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="3636a-164">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="3636a-164">Get security updates for our products</span></span>
<span data-ttu-id="3636a-165">Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [tę stronę](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.</span><span class="sxs-lookup"><span data-stu-id="3636a-165">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

