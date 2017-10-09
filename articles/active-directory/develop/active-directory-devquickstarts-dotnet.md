---
title: .NET aaaAzure AD wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji .NET pulpitu systemu Windows, która integruje się z usługą Azure AD w celu logowania się i wymaga usługi Azure AD chronione w trybie OAuth interfejsów API."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="5553f-103">Integrowanie usługi Azure AD w aplikacji WPF pulpitu systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5553f-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="5553f-104">Jeśli projektujesz klasycznej aplikacji usługi Azure AD umożliwia proste i bezpośrednie dla tooauthenticate można z użytkownikami przy użyciu ich kont usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5553f-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="5553f-105">Umożliwia również toosecurely Twojej aplikacji korzystać z dowolnej sieci web interfejsu API chronione przez usługę Azure AD, takich jak hello interfejsami API usługi Office 365 lub hello interfejsu API Azure.</span><span class="sxs-lookup"><span data-stu-id="5553f-105">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="5553f-106">W przypadku klientów platformy .NET native wymagające tooaccess chronionych zasobów usługi Azure AD zapewnia hello biblioteki uwierzytelniania usługi Active Directory lub biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="5553f-106">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="5553f-107">Jedynym celem ADAL jego życia jest toomake go łatwo tooget tokenów dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5553f-107">ADAL's sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="5553f-108">toodemonstrate Ci, jak łatwo jest, w tym miejscu będzie budujemy aplikacji listy zadań do wykonania WPF .NET który:</span><span class="sxs-lookup"><span data-stu-id="5553f-108">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="5553f-109">Pobiera dostępu tokeny na potrzeby wywoływania hello Azure AD Graph API przy użyciu hello [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="5553f-109">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="5553f-110">Przeszukuje katalog dla użytkowników z podanego aliasu.</span><span class="sxs-lookup"><span data-stu-id="5553f-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="5553f-111">Znaki użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5553f-111">Signs users out.</span></span>

<span data-ttu-id="5553f-112">toobuild hello pełną działającą aplikację, musisz:</span><span class="sxs-lookup"><span data-stu-id="5553f-112">toobuild hello complete working application, you'll need to:</span></span>

1. <span data-ttu-id="5553f-113">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5553f-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="5553f-114">Instalowanie i konfigurowanie biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="5553f-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="5553f-115">Używaj tokenów ADAL tooget z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5553f-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="5553f-116">Rozpoczęto, tooget [pobrać szkielet aplikacji hello](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5553f-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="5553f-117">Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5553f-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="5553f-118">Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="5553f-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directorysearcher-application"></a><span data-ttu-id="5553f-119">1. Zarejestruj hello DirectorySearcher aplikacji</span><span class="sxs-lookup"><span data-stu-id="5553f-119">1. Register hello DirectorySearcher Application</span></span>
<span data-ttu-id="5553f-120">tooenable tokenów tooget aplikacji, musisz najpierw tooregister dzierżawy w usługi Azure AD i udzielić jej uprawnienia tooaccess hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="5553f-120">tooenable your app tooget tokens, you'll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="5553f-121">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5553f-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5553f-122">Na górnym pasku hello, kliknij na Twoim koncie, a w obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, którym chcesz tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5553f-122">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="5553f-123">Polecenie **więcej usług** w hello nawigacji po lewej stronie i wybierz polecenie **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5553f-123">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="5553f-124">Polecenie **rejestracji aplikacji** i wybierz polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5553f-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="5553f-125">Postępuj zgodnie z monitami hello i utworzyć nową **natywną aplikację kliencką**.</span><span class="sxs-lookup"><span data-stu-id="5553f-125">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="5553f-126">Witaj **nazwa** z hello aplikacji opisano użytkownikom tooend aplikacji</span><span class="sxs-lookup"><span data-stu-id="5553f-126">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="5553f-127">Witaj **identyfikator Uri przekierowania** jest kombinacją schemat i ciąg, które będą używane przez usługi Azure AD tooreturn odpowiedzi tokenu.</span><span class="sxs-lookup"><span data-stu-id="5553f-127">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="5553f-128">Wprowadź wartość tooyour określonych aplikacji, np. `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="5553f-128">Enter a value specific tooyour application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="5553f-129">Po zakończeniu rejestracji usługi AAD przypisze aplikacji Unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5553f-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="5553f-130">Ta wartość jest potrzebny w kolejnych sekcjach hello, dlatego skopiuj go ze strony aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5553f-130">You'll need this value in hello next sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="5553f-131">Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia** i wybierz polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5553f-131">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="5553f-132">Wybierz hello **Microsoft Graph** jako hello interfejsu API i Dodaj hello **Czytaj dane katalogu** uprawnienie w obszarze **delegowane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="5553f-132">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="5553f-133">Spowoduje to włączenie użytkownika hello tooquery aplikacji interfejsu API programu Graph dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5553f-133">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="5553f-134">2. Instalowanie i konfigurowanie biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="5553f-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="5553f-135">Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="5553f-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="5553f-136">Aby mogli toocommunicate ADAL toobe z usługą Azure AD, należy tooprovide go niektóre informacje o rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5553f-136">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="5553f-137">Rozpocznij, dodając ADAL toohello DirectorySearcher projektu przy użyciu konsoli Menedżera pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="5553f-137">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="5553f-138">W projekcie DirectorySearcher hello Otwórz `app.config`.</span><span class="sxs-lookup"><span data-stu-id="5553f-138">In hello DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="5553f-139">Zastąp wartości hello elementów hello na powitania `<appSettings>` hello tooreflect sekcji wartości danych wejściowych do hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5553f-139">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="5553f-140">Kod będzie odwoływać tych wartości, przy każdym użyciu biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="5553f-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="5553f-141">Witaj `ida:Tenant` jest hello domeny dzierżawy usługi Azure AD, np. contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="5553f-141">hello `ida:Tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="5553f-142">Witaj `ida:ClientId` jest clientId hello skopiowany z portalu hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5553f-142">hello `ida:ClientId` is hello clientId of your application you copied from hello portal.</span></span>
  * <span data-ttu-id="5553f-143">Witaj `ida:RedirectUri` hello jest zarejestrowany w portalu hello adres url przekierowania.</span><span class="sxs-lookup"><span data-stu-id="5553f-143">hello `ida:RedirectUri` is hello redirect url you registered in hello portal.</span></span>

## <a name="3----use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="5553f-144">3.    Używaj tokenów ADAL tooGet z usługi AAD</span><span class="sxs-lookup"><span data-stu-id="5553f-144">3.    Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="5553f-145">Witaj podstawową zasadą za ADAL jest czy zawsze, gdy Twoja aplikacja powinna tokenu dostępu, po prostu wywołuje `authContext.AcquireTokenAsync(...)`, i ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="5553f-145">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="5553f-146">W hello `DirectorySearcher` otwarciu projektu `MainWindow.xaml.cs` i Znajdź hello `MainWindow()` metody.</span><span class="sxs-lookup"><span data-stu-id="5553f-146">In hello `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate hello `MainWindow()` method.</span></span>  <span data-ttu-id="5553f-147">pierwszym krokiem Hello jest tooinitialize aplikacji `AuthenticationContext` -ADAL obiektu klasy podstawowej.</span><span class="sxs-lookup"><span data-stu-id="5553f-147">hello first step is tooinitialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="5553f-148">Jest to, gdy przekazujesz ADAL hello współrzędne musi toocommunicate z usługą Azure AD i poinformuj go jak toocache tokenów.</span><span class="sxs-lookup"><span data-stu-id="5553f-148">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="5553f-149">Znajdź teraz hello `Search(...)` metodę, która będzie wywoływana, gdy przycisk "Wyszukiwanie" w Interfejsie użytkownika aplikacji hello hello hello cliks użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5553f-149">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="5553f-150">Ta metoda ułatwia tworzenie tooquery toohello interfejsu API usługi Azure AD Graph żądania GET do użytkowników, których nazwy UPN zaczyna się hello danego wyszukiwanego terminu.</span><span class="sxs-lookup"><span data-stu-id="5553f-150">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="5553f-151">Jednak w kolejności tooquery hello interfejsu API programu Graph, tooinclude ' access_token ' w hello `Authorization` żądania nagłówek hello — jest to, gdzie ADAL jest dostarczany.</span><span class="sxs-lookup"><span data-stu-id="5553f-151">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="5553f-152">Gdy aplikacja żąda token przez wywołanie metody `AcquireTokenAsync(...)`, ADAL podejmie tooreturn token bez monitowania użytkownika hello o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="5553f-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="5553f-153">Jeśli ADAL ustali, że ten użytkownik hello musi toosign w tooget token, zostanie wyświetlane okno dialogowe logowania, zbieranie poświadczeń użytkownika hello i zwracają token, po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="5553f-153">If ADAL determines that hello user needs toosign in tooget a token, it will display a login dialog, collect hello user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="5553f-154">Jeśli ADAL zostanie tooreturn tokenu z jakiegokolwiek powodu, zgłosi `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="5553f-154">If ADAL is unable tooreturn a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="5553f-155">Zwróć uwagę, że hello `AuthenticationResult` zawiera obiekt `UserInfo` obiektów, które mogą być używane toocollect informacji o aplikacji może być konieczne.</span><span class="sxs-lookup"><span data-stu-id="5553f-155">Notice that hello `AuthenticationResult` object contains a `UserInfo` object that can be used toocollect information your app may need.</span></span>  <span data-ttu-id="5553f-156">W hello DirectorySearcher `UserInfo` interfejsu użytkownika aplikacji hello toocustomize używanych z identyfikatorem użytkownika hello jest.</span><span class="sxs-lookup"><span data-stu-id="5553f-156">In hello DirectorySearcher, `UserInfo` is used toocustomize hello app's UI with hello user's id.</span></span>
* <span data-ttu-id="5553f-157">Gdy hello użytkownik kliknie przycisk "Wyloguj" hello, chcemy tooensure, który hello następne wywołanie za`AcquireTokenAsync(...)` poprosi hello toosign użytkownika w.</span><span class="sxs-lookup"><span data-stu-id="5553f-157">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenAsync(...)` will ask hello user toosign in.</span></span>  <span data-ttu-id="5553f-158">Przy użyciu biblioteki ADAL jest tak proste, jak czyszczenie pamięci podręcznej tokenu hello:</span><span class="sxs-lookup"><span data-stu-id="5553f-158">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="5553f-159">Jednak jeśli użytkownik hello nie klikać przycisku "Wyloguj" hello, można toomaintain hello sesji użytkownika dla hello następnym uruchomieniu hello DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="5553f-159">However, if hello user does not click hello "Sign Out" button, you will want toomaintain hello user's session for hello next time they run hello DirectorySearcher.</span></span>  <span data-ttu-id="5553f-160">Po uruchomieniu aplikacji hello należy sprawdzić ADAL w pamięci podręcznej tokenu dla istniejącego tokenu, a następnie odpowiednio zaktualizować hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5553f-160">When hello app launches, you can check ADAL's token cache for an existing token and update hello UI accordingly.</span></span>  <span data-ttu-id="5553f-161">W hello `CheckForCachedToken()` metody wywoływania innego zbyt`AcquireTokenAsync(...)`, przekazując hello teraz `PromptBehavior.Never` parametru.</span><span class="sxs-lookup"><span data-stu-id="5553f-161">In hello `CheckForCachedToken()` method, make another call too`AcquireTokenAsync(...)`, this time passing in hello `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="5553f-162">`PromptBehavior.Never`powiadomi ADAL, że użytkownik hello nie powinien być monitowany w celu logowania się i ADAL należy zamiast tego zgłoszenia wyjątku, jeśli jest tooreturn tokenu.</span><span class="sxs-lookup"><span data-stu-id="5553f-162">`PromptBehavior.Never` will tell ADAL that hello user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable tooreturn a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="5553f-163">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="5553f-163">Congratulations!</span></span> <span data-ttu-id="5553f-164">Możesz teraz działa aplikacja .NET WPF, która ma hello możliwości tooauthenticate użytkowników, bezpiecznie wywoływania interfejsów API sieci Web przy użyciu protokołu OAuth 2.0 i uzyskać podstawowe informacje o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="5553f-164">You now have a working .NET WPF application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="5553f-165">Jeśli nie jest jeszcze teraz jest hello toopopulate czas dzierżawy z niektórych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5553f-165">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="5553f-166">Uruchom aplikację DirectorySearcher i zaloguj się przy użyciu jednej z tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5553f-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="5553f-167">Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.</span><span class="sxs-lookup"><span data-stu-id="5553f-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="5553f-168">Aplikacja hello Zamknij i uruchom je ponownie.</span><span class="sxs-lookup"><span data-stu-id="5553f-168">Close hello app, and re-run it.</span></span>  <span data-ttu-id="5553f-169">Zwróć uwagę, jak hello sesja pozostanie niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="5553f-169">Notice how hello user's session remains intact.</span></span>  <span data-ttu-id="5553f-170">Wyloguj się i zaloguj się ponownie jako inny użytkownik.</span><span class="sxs-lookup"><span data-stu-id="5553f-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="5553f-171">Biblioteka ADAL umożliwia łatwe tooincorporate wszystkie te typowe funkcje tożsamości w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5553f-171">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="5553f-172">Zapewnia obsługę wszystkich hello dirty pracy dla Ciebie — Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika za pomocą interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="5553f-172">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="5553f-173">Naprawdę tooknow wystarczy jednego wywołania interfejsu API, `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="5553f-173">All you really need tooknow is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="5553f-174">Odwołania, przykładowy ukończyć powitalnych (bez wartości konfiguracji) jest dostarczany [tutaj](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5553f-174">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="5553f-175">Możesz teraz przejść na tooadditional scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="5553f-175">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="5553f-176">Można tootry:</span><span class="sxs-lookup"><span data-stu-id="5553f-176">You may want tootry:</span></span>

[<span data-ttu-id="5553f-177">Zabezpieczanie interfejsu API za pomocą usługi Azure AD sieci Web .NET >></span><span class="sxs-lookup"><span data-stu-id="5553f-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

