---
title: Azure AD platformy .NET wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak utworzyć aplikację .NET pulpitu systemu Windows, która integruje się z usługą Azure AD w celu logowania się i wymaga usługi Azure AD chronione interfejsów API w trybie OAuth."
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
ms.openlocfilehash: 7a252e0e5243c7b7489373845531cb913ca1f6aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="47189-103">Integrowanie usługi Azure AD w aplikacji WPF pulpitu systemu Windows</span><span class="sxs-lookup"><span data-stu-id="47189-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="47189-104">Jeśli projektujesz klasycznej aplikacji usługi Azure AD umożliwia proste i bezpośrednie umożliwia uwierzytelnianie użytkowników przy użyciu ich kont usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="47189-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="47189-105">Umożliwia również aplikacji bezpiecznego używać dowolnego składnika web API chronione przez usługę Azure AD, takie jak interfejsami API usługi Office 365 lub interfejsu API platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47189-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="47189-106">Dla platformy .NET native klientów, którzy potrzebują dostępu do chronionych zasobów Usługa Azure AD zapewnia biblioteki uwierzytelniania usługi Active Directory lub biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="47189-106">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="47189-107">ADAL w wyłącznie życia ma na celu ułatwić aplikację, aby uzyskać dostęp do tokenów.</span><span class="sxs-lookup"><span data-stu-id="47189-107">ADAL's sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="47189-108">Aby zademonstrować, jak łatwo jest, w tym miejscu będzie budujemy aplikacji listy zadań do wykonania WPF .NET który:</span><span class="sxs-lookup"><span data-stu-id="47189-108">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="47189-109">Pobiera dostępu tokenów do wywoływania za pomocą interfejsu API usługi Azure AD Graph [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="47189-109">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="47189-110">Przeszukuje katalog dla użytkowników z podanego aliasu.</span><span class="sxs-lookup"><span data-stu-id="47189-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="47189-111">Znaki użytkowników.</span><span class="sxs-lookup"><span data-stu-id="47189-111">Signs users out.</span></span>

<span data-ttu-id="47189-112">Aby utworzyć pełną działającą aplikację, musisz:</span><span class="sxs-lookup"><span data-stu-id="47189-112">To build the complete working application, you'll need to:</span></span>

1. <span data-ttu-id="47189-113">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47189-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="47189-114">Instalowanie i konfigurowanie biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="47189-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="47189-115">Użyj biblioteki ADAL, aby uzyskać tokenów z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47189-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="47189-116">Aby rozpocząć, [pobrać szkielet aplikacji](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) lub [Pobieranie ukończone próbki](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="47189-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="47189-117">Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47189-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="47189-118">Jeśli nie masz już dzierżawę, [Dowiedz się, jak kupić](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="47189-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directorysearcher-application"></a><span data-ttu-id="47189-119">1. Zarejestrować aplikację DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="47189-119">1. Register the DirectorySearcher Application</span></span>
<span data-ttu-id="47189-120">Aby włączyć swoją aplikację w celu uzyskania tokenów, musisz najpierw zarejestrować ją w dzierżawie usługi Azure AD i udzielić jej uprawnienia dostępu do interfejsu API programu Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="47189-120">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="47189-121">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47189-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="47189-122">Na górnym pasku, kliknij na Twoim koncie i w obszarze **katalogu** wybierz dzierżawy usługi Active Directory, w którym chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="47189-122">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="47189-123">Polecenie **więcej usług** w nawigacji po lewej stronie i wybierz polecenie **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47189-123">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="47189-124">Polecenie **rejestracji aplikacji** i wybierz polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="47189-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="47189-125">Postępuj zgodnie z monitami i utworzyć nową **natywną aplikację kliencką**.</span><span class="sxs-lookup"><span data-stu-id="47189-125">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="47189-126">**Nazwa** aplikacji będzie opisywać aplikację dla użytkowników końcowych</span><span class="sxs-lookup"><span data-stu-id="47189-126">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="47189-127">**Identyfikator Uri przekierowania** jest kombinacją schemat i ciąg, używanego do zwracania odpowiedzi tokenu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47189-127">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="47189-128">Wprowadź wartości określonych aplikacji, np. `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="47189-128">Enter a value specific to your application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="47189-129">Po zakończeniu rejestracji usługi AAD przypisze aplikacji Unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47189-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="47189-130">Ta wartość jest potrzebny w kolejnych sekcjach, dlatego skopiuj go ze strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47189-130">You'll need this value in the next sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="47189-131">Z **ustawienia** wybierz pozycję **wymagane uprawnienia** i wybierz polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="47189-131">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="47189-132">Wybierz **Microsoft Graph** jako interfejsu API i Dodaj **Czytaj dane katalogu** uprawnienie w obszarze **delegowane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="47189-132">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="47189-133">Umożliwi to aplikacja do zapytania interfejsu API programu Graph dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="47189-133">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="47189-134">2. Instalowanie i konfigurowanie biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="47189-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="47189-135">Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="47189-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="47189-136">Biblioteki ADAL można było nawiązać połączenia z usługą Azure AD, należy dostarczyć informacji o rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47189-136">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="47189-137">Rozpocznij, dodając biblioteki ADAL do projektu DirectorySearcher przy użyciu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="47189-137">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="47189-138">W projekcie DirectorySearcher Otwórz `app.config`.</span><span class="sxs-lookup"><span data-stu-id="47189-138">In the DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="47189-139">Zastąp wartości elementów w `<appSettings>` sekcji, aby odzwierciedlić wartości wejściowych do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="47189-139">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="47189-140">Kod będzie odwoływać tych wartości, przy każdym użyciu biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="47189-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="47189-141">`ida:Tenant` Jest domeny dzierżawy usługi Azure AD, np. contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="47189-141">The `ida:Tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="47189-142">`ida:ClientId` Jest clientId aplikacji został skopiowany z portalu.</span><span class="sxs-lookup"><span data-stu-id="47189-142">The `ida:ClientId` is the clientId of your application you copied from the portal.</span></span>
  * <span data-ttu-id="47189-143">`ida:RedirectUri` Przekierowania jest adres url jest zarejestrowany w portalu.</span><span class="sxs-lookup"><span data-stu-id="47189-143">The `ida:RedirectUri` is the redirect url you registered in the portal.</span></span>

## <a name="3----use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="47189-144">3.    Aby uzyskać tokenów z usługi AAD, użyj biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="47189-144">3.    Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="47189-145">Zasada podstawowa za ADAL jest, że zawsze, gdy Twoja aplikacja powinna tokenu dostępu, po prostu wywołuje `authContext.AcquireTokenAsync(...)`, a reszta biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="47189-145">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="47189-146">W `DirectorySearcher` otwarciu projektu `MainWindow.xaml.cs` i Znajdź `MainWindow()` metody.</span><span class="sxs-lookup"><span data-stu-id="47189-146">In the `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate the `MainWindow()` method.</span></span>  <span data-ttu-id="47189-147">Pierwszym krokiem jest zainicjowanie aplikacji `AuthenticationContext` -ADAL obiektu klasy podstawowej.</span><span class="sxs-lookup"><span data-stu-id="47189-147">The first step is to initialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="47189-148">Jest to, gdy przekazujesz ADAL współrzędne wymaga do komunikacji z usługą Azure AD i poinformuj go, jak pamięci podręcznej tokenów.</span><span class="sxs-lookup"><span data-stu-id="47189-148">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="47189-149">Znajdź teraz `Search(...)` metodę, która będzie wywoływana, gdy przycisk cliks użytkownika "Wyszukiwanie" w Interfejsie użytkownika aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47189-149">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="47189-150">Ta metoda zgłasza żądanie GET interfejsu API Azure AD Graph zapytania dla użytkowników, których nazwy UPN rozpoczyna się od danego wyszukiwanego.</span><span class="sxs-lookup"><span data-stu-id="47189-150">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="47189-151">Jednak aby można było wykonać kwerendę interfejsu API programu Graph, należy uwzględnić ' access_token ' w `Authorization` nagłówka żądania — jest to, gdzie ADAL jest dostarczany.</span><span class="sxs-lookup"><span data-stu-id="47189-151">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate the Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for the To Do item name");
        return;
    }

    // Get an Access Token for the Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled the sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="47189-152">Gdy aplikacja żąda token przez wywołanie metody `AcquireTokenAsync(...)`, ADAL podejmie próbę zwracają token bez monitowania użytkownika o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="47189-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="47189-153">Jeśli ADAL Określa, czy użytkownik powinien logować się do pobrania tokenu, zostanie wyświetlane okno dialogowe logowania, zbieranie poświadczeń użytkownika i zwracają token, po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="47189-153">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="47189-154">Jeśli nie można zwrócić token jakiegokolwiek powodu ADAL, zgłosi `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="47189-154">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="47189-155">Zwróć uwagę, że `AuthenticationResult` zawiera obiekt `UserInfo` obiektu, który może służyć do zbierania informacji o aplikacji może być konieczne.</span><span class="sxs-lookup"><span data-stu-id="47189-155">Notice that the `AuthenticationResult` object contains a `UserInfo` object that can be used to collect information your app may need.</span></span>  <span data-ttu-id="47189-156">W DirectorySearcher `UserInfo` jest używany do dostosowania interfejsu użytkownika aplikacji z identyfikatorem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47189-156">In the DirectorySearcher, `UserInfo` is used to customize the app's UI with the user's id.</span></span>
* <span data-ttu-id="47189-157">Gdy użytkownik kliknie przycisk "Wyloguj", chcemy się upewnić się, że następne wywołanie `AcquireTokenAsync(...)` będzie monitować użytkownika do logowania.</span><span class="sxs-lookup"><span data-stu-id="47189-157">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenAsync(...)` will ask the user to sign in.</span></span>  <span data-ttu-id="47189-158">Przy użyciu biblioteki ADAL jest tak proste, jak czyszczenie pamięci podręcznej tokenu:</span><span class="sxs-lookup"><span data-stu-id="47189-158">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear the token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="47189-159">Jednak jeśli użytkownik nie klikniesz przycisku "Wyloguj", można zachować sesję użytkownika dla przy następnym uruchomieniu DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="47189-159">However, if the user does not click the "Sign Out" button, you will want to maintain the user's session for the next time they run the DirectorySearcher.</span></span>  <span data-ttu-id="47189-160">Po uruchomieniu aplikacji, należy sprawdzić ADAL w pamięci podręcznej tokenu dla istniejącego tokenu, a następnie odpowiednio zaktualizować interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47189-160">When the app launches, you can check ADAL's token cache for an existing token and update the UI accordingly.</span></span>  <span data-ttu-id="47189-161">W `CheckForCachedToken()` metody innego wywoływania `AcquireTokenAsync(...)`, przekazując teraz `PromptBehavior.Never` parametru.</span><span class="sxs-lookup"><span data-stu-id="47189-161">In the `CheckForCachedToken()` method, make another call to `AcquireTokenAsync(...)`, this time passing in the `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="47189-162">`PromptBehavior.Never`informuje ADAL, że użytkownik nie powinien być monitowany w celu logowania się i ADAL zamiast tego powinien zgłosić wyjątek, jeśli nie można zwrócić token.</span><span class="sxs-lookup"><span data-stu-id="47189-162">`PromptBehavior.Never` will tell ADAL that the user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable to return a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As the application starts, try to get an access token without prompting the user.  If one exists, show the user as signed in.
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

        // If user interaction is required, proceed to main page without singing the user in.
        return;
    }

    // A valid token is in the cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="47189-163">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="47189-163">Congratulations!</span></span> <span data-ttu-id="47189-164">Możesz teraz działa aplikacja .NET WPF, która ma możliwość uwierzytelniania użytkowników, bezpiecznie wywoływać interfejsy API sieci Web przy użyciu protokołu OAuth 2.0 i uzyskać podstawowe informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="47189-164">You now have a working .NET WPF application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="47189-165">Jeśli nie jest jeszcze nadszedł czas do wypełnienia dzierżawy z niektórych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="47189-165">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="47189-166">Uruchom aplikację DirectorySearcher i zaloguj się przy użyciu jednej z tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="47189-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="47189-167">Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.</span><span class="sxs-lookup"><span data-stu-id="47189-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="47189-168">Zamknij aplikację i uruchom je ponownie.</span><span class="sxs-lookup"><span data-stu-id="47189-168">Close the app, and re-run it.</span></span>  <span data-ttu-id="47189-169">Zwróć uwagę, jak sesji użytkownika pozostanie niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="47189-169">Notice how the user's session remains intact.</span></span>  <span data-ttu-id="47189-170">Wyloguj się i zaloguj się ponownie jako inny użytkownik.</span><span class="sxs-lookup"><span data-stu-id="47189-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="47189-171">Biblioteka ADAL można łatwo zastosować wszystkie te typowe funkcje tożsamości w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47189-171">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="47189-172">Zapewnia obsługę pracy dirty dla Ciebie — Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający użytkownika za pomocą interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="47189-172">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="47189-173">Tak naprawdę trzeba wiedzieć jednego wywołania interfejsu API, jest `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="47189-173">All you really need to know is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="47189-174">Odwołania, jest dostępne ukończone próbka (bez wartości konfiguracji) [tutaj](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="47189-174">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="47189-175">Możesz teraz przejść do dodatkowe scenariusze.</span><span class="sxs-lookup"><span data-stu-id="47189-175">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="47189-176">Można spróbować:</span><span class="sxs-lookup"><span data-stu-id="47189-176">You may want to try:</span></span>

[<span data-ttu-id="47189-177">Zabezpieczanie interfejsu API za pomocą usługi Azure AD sieci Web .NET >></span><span class="sxs-lookup"><span data-stu-id="47189-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

