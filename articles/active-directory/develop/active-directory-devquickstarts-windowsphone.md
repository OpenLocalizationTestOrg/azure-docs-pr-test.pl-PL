---
title: "Wprowadzenie do usługi Azure AD Windows Phone | Dokumentacja firmy Microsoft"
description: "Sposób tworzenia aplikacji Windows Phone, która integruje się z usługą Azure AD w celu logowania się i wymaga usługi Azure AD chronione w trybie OAuth interfejsów API."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 03c4b6d225dce99d79ef6c1ba2af43af8dea3eae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="2ea6b-103">Integrowanie usługi Azure AD w aplikacji Windows Phone</span><span class="sxs-lookup"><span data-stu-id="2ea6b-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="2ea6b-104">Projekty systemu Windows Phone 8.1 i wcześniejszych nie są obsługiwane w programie Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="2ea6b-105">Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="2ea6b-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="2ea6b-106">Jeśli projektujesz aplikacji Windows Phone 8.1, usługi Azure AD umożliwia proste i bezpośrednie umożliwia uwierzytelnianie użytkowników przy użyciu ich kont usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="2ea6b-107">Umożliwia również aplikacji bezpiecznego używać dowolnego składnika web API chronione przez usługę Azure AD, takie jak interfejsami API usługi Office 365 lub interfejsu API platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-107">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="2ea6b-108">Ten przykładowy kod używa biblioteki ADAL w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="2ea6b-109">Aby uzyskać najnowsze technologie, warto zamiast tego spróbuj naszych [samouczek aplikacji uniwersalnych systemu Windows przy użyciu biblioteki ADAL w wersji 3.0](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="2ea6b-109">For the latest technology, you may want to instead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="2ea6b-110">Jeśli tworzysz rzeczywiście aplikacji dla systemu Windows Phone 8.1, jest właściwym miejscu.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-110">If you are indeed building an app for Windows Phone 8.1, this is the right place.</span></span>  <span data-ttu-id="2ea6b-111">ADAL w wersji 2.0 jest nadal obsługiwane i jest zalecanym sposobem tworzenia agianst aplikacji Windows Phone 8.1 przy użyciu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-111">ADAL v2.0 is still fully supported, and is the recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="2ea6b-112">Dla platformy .NET native klientów, którzy potrzebują dostępu do chronionych zasobów Usługa Azure AD zapewnia biblioteki uwierzytelniania usługi Active Directory lub biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-112">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="2ea6b-113">ADAL w wyłącznie życia ma na celu ułatwić aplikację, aby uzyskać dostęp do tokenów.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-113">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="2ea6b-114">Aby zademonstrować, jak łatwo jest, w tym miejscu będzie budujemy "katalog modułu wyszukującego" aplikacji systemu Windows Phone 8.1 który:</span><span class="sxs-lookup"><span data-stu-id="2ea6b-114">To demonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="2ea6b-115">Pobiera dostępu tokenów do wywoływania za pomocą interfejsu API usługi Azure AD Graph [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ea6b-115">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="2ea6b-116">Przeszukuje katalog dla użytkowników z danym głównej nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="2ea6b-117">Znaki użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-117">Signs users out.</span></span>

<span data-ttu-id="2ea6b-118">Aby utworzyć pełną działającą aplikację, musisz:</span><span class="sxs-lookup"><span data-stu-id="2ea6b-118">To build the complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="2ea6b-119">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="2ea6b-120">Instalowanie i konfigurowanie biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="2ea6b-121">Użyj biblioteki ADAL, aby uzyskać tokenów z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-121">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="2ea6b-122">Aby rozpocząć, [pobrać szkielet projektu](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) lub [Pobieranie ukończone próbki](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="2ea6b-122">To get started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="2ea6b-123">Każdy jest rozwiązanie Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="2ea6b-124">Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="2ea6b-125">Jeśli nie masz już dzierżawę, [Dowiedz się, jak kupić](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="2ea6b-125">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directory-searcher-application"></a><span data-ttu-id="2ea6b-126">1. Zarejestrować aplikację poszukującego katalogu</span><span class="sxs-lookup"><span data-stu-id="2ea6b-126">1. Register the Directory Searcher Application</span></span>
<span data-ttu-id="2ea6b-127">Aby włączyć swoją aplikację w celu uzyskania tokenów, musisz najpierw zarejestrować ją w dzierżawie usługi Azure AD i udzielić jej uprawnienia dostępu do interfejsu API programu Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="2ea6b-127">To enable your app to get tokens, you’ll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="2ea6b-128">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2ea6b-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2ea6b-129">Na górnym pasku, kliknij na Twoim koncie i w obszarze **katalogu** wybierz dzierżawy usługi Active Directory, w którym chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-129">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="2ea6b-130">Polecenie **więcej usług** w nawigacji po lewej stronie i wybierz polecenie **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-130">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="2ea6b-131">Polecenie **rejestracji aplikacji** i wybierz polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="2ea6b-132">Postępuj zgodnie z monitami i utworzyć nową **natywną aplikację kliencką**.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-132">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="2ea6b-133">**Nazwa** aplikacji będzie opisywać aplikację dla użytkowników końcowych</span><span class="sxs-lookup"><span data-stu-id="2ea6b-133">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="2ea6b-134">**Identyfikator Uri przekierowania** jest kombinacją schemat i ciąg, używanego do zwracania odpowiedzi tokenu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-134">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="2ea6b-135">Wprowadź wartość symbolu zastępczego teraz, np. `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="2ea6b-136">Firma Microsoft będzie później Zastąp tę wartość.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="2ea6b-137">Po zakończeniu rejestracji usługi AAD przypisze aplikacji Unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="2ea6b-138">Ta wartość jest potrzebny w kolejnych sekcjach, dlatego skopiuj go na karcie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-138">You’ll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="2ea6b-139">Z **ustawienia** wybierz pozycję **wymagane uprawnienia** i wybierz polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-139">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="2ea6b-140">Wybierz **Microsoft Graph** jako interfejsu API i Dodaj **Czytaj dane katalogu** uprawnienie w obszarze **delegowane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-140">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="2ea6b-141">Umożliwi to aplikacja do zapytania interfejsu API programu Graph dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-141">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="2ea6b-142">2. Instalowanie i konfigurowanie biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="2ea6b-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="2ea6b-143">Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="2ea6b-144">Biblioteki ADAL można było nawiązać połączenia z usługą Azure AD, należy dostarczyć informacji o rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-144">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="2ea6b-145">Rozpocznij, dodając biblioteki ADAL do projektu DirectorySearcher przy użyciu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-145">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="2ea6b-146">W projekcie DirectorySearcher Otwórz `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-146">In the DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="2ea6b-147">Zastąp wartości w `Config Values` region do wartości wejściowych do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-147">Replace the values in the `Config Values` region to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="2ea6b-148">Kod będzie odwoływać tych wartości, przy każdym użyciu biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="2ea6b-149">`tenant` Jest domeny dzierżawy usługi Azure AD, np. contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="2ea6b-149">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="2ea6b-150">`clientId` Jest clientId aplikacji został skopiowany z portalu.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-150">The `clientId` is the clientId of your application you copied from the portal.</span></span>
* <span data-ttu-id="2ea6b-151">Teraz musisz odnaleźć identyfikator uri wywołania zwrotnego dla aplikacji Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-151">You now need to discover the callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="2ea6b-152">Ustaw punkt przerwania w tym wierszu w `MainPage` metody:</span><span class="sxs-lookup"><span data-stu-id="2ea6b-152">Set a breakpoint on this line in the `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="2ea6b-153">Uruchom aplikację i skopiuj Odłóż wartość `redirectUri` gdy zostaje trafiony punkt przerwania.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-153">Run the app, and copy aside the value of `redirectUri` when the breakpoint is hit.</span></span>  <span data-ttu-id="2ea6b-154">Powinien on wyglądać podobnie jak</span><span class="sxs-lookup"><span data-stu-id="2ea6b-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="2ea6b-155">Ponownie **Konfiguruj** kartę aplikacji w portalu zarządzania Azure, zastąp wartość **RedirectUri** o tej wartości.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-155">Back on the **Configure** tab of your application in the Azure Management Portal, replace the value of the **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="2ea6b-156">3. Aby uzyskać tokenów z usługi AAD, użyj biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="2ea6b-156">3. Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="2ea6b-157">Zasada podstawowa za ADAL jest, że zawsze, gdy Twoja aplikacja powinna tokenu dostępu, po prostu wywołuje `authContext.AcquireToken(…)`, a reszta biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-157">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="2ea6b-158">Pierwszym krokiem jest zainicjowanie aplikacji `AuthenticationContext` -ADAL obiektu klasy podstawowej.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-158">The first step is to initialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="2ea6b-159">Jest to, gdy przekazujesz ADAL współrzędne wymaga do komunikacji z usługą Azure AD i poinformuj go, jak pamięci podręcznej tokenów.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-159">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="2ea6b-160">Znajdź teraz `Search(...)` metodę, która będzie wywoływana, gdy przycisk cliks użytkownika "Wyszukiwanie" w Interfejsie użytkownika aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-160">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="2ea6b-161">Ta metoda zgłasza żądanie GET interfejsu API Azure AD Graph zapytania dla użytkowników, których nazwy UPN rozpoczyna się od danego wyszukiwanego.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-161">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="2ea6b-162">Jednak aby można było wykonać kwerendę interfejsu API programu Graph, należy uwzględnić ' access_token ' w `Authorization` nagłówka żądania — jest to, gdzie ADAL jest dostarczany.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-162">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try to get a token without triggering any user prompt.
    // ADAL will check whether the requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained the QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="2ea6b-163">Jeśli konieczne jest uwierzytelnianie interakcyjne, ADAL użyje Książka adresowa systemu (Windows, Windows Phone w sieci Web uwierzytelniania Broker) i [modelu kontynuacji](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) do wyświetlania na stronie tworzenia konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) to display the Azure AD sign in page.</span></span>  <span data-ttu-id="2ea6b-164">Gdy użytkownik się zaloguje, Twoja aplikacja powinna przekazać ADAL wyniki interakcji Książka adresowa systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-164">When the user signs in, your app needs to pass ADAL the results of the WAB interaction.</span></span>  <span data-ttu-id="2ea6b-165">Jest tak proste, jak implementacja `ContinueWebAuthentication` interfejsu:</span><span class="sxs-lookup"><span data-stu-id="2ea6b-165">This is as simple as implementing the `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when the application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass the authentication interaction results to ADAL, which will
    // conclude the token acquisition operation and invoke the callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="2ea6b-166">Teraz nadszedł czas na użycie `AuthenticationResult` ADAL zwrócona do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-166">Now it's time to use the `AuthenticationResult` that ADAL returned to your app.</span></span>  <span data-ttu-id="2ea6b-167">W `QueryGraph(...)` wywołania zwrotnego, Dołącz ' access_token ' nabył na żądanie GET w nagłówku autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="2ea6b-167">In the `QueryGraph(...)` callback, attach the access_token you acquired to the GET request in the Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add the access token to the Authorization Header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="2ea6b-168">Można również użyć `AuthenticationResult` obiektu, aby wyświetlić informacje o użytkowniku w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-168">You can also use the `AuthenticationResult` object to display information about the user in your app.</span></span> <span data-ttu-id="2ea6b-169">W `QueryGraph(...)` — metoda, za pomocą wynik można wyświetlić identyfikator użytkownika na stronie:</span><span class="sxs-lookup"><span data-stu-id="2ea6b-169">In the `QueryGraph(...)` method, use the result to show the user's id on the page:</span></span>

```C#
// Update the Page UI to represent the signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="2ea6b-170">Na koniec służy ADAL logowania użytkownika z aplikacji, a także.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-170">Finally, you can use ADAL to sign the user out of hte application as well.</span></span>  <span data-ttu-id="2ea6b-171">Gdy użytkownik kliknie przycisk "Wyloguj", chcemy się upewnić się, że następne wywołanie `AcquireTokenSilentAsync(...)` zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-171">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="2ea6b-172">Przy użyciu biblioteki ADAL jest tak proste, jak czyszczenie pamięci podręcznej tokenu:</span><span class="sxs-lookup"><span data-stu-id="2ea6b-172">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from the token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="2ea6b-173">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="2ea6b-173">Congratulations!</span></span> <span data-ttu-id="2ea6b-174">Możesz teraz działa aplikacji Windows Phone, który ma możliwość uwierzytelniania użytkowników, bezpiecznie wywoływać interfejsy API sieci Web przy użyciu protokołu OAuth 2.0 i uzyskać podstawowe informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-174">You now have a working Windows Phone app that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="2ea6b-175">Jeśli nie jest jeszcze nadszedł czas do wypełnienia dzierżawy z niektórych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-175">If you haven’t already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="2ea6b-176">Uruchom aplikację DirectorySearcher i zaloguj się przy użyciu jednej z tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="2ea6b-177">Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="2ea6b-178">Zamknij aplikację i uruchom je ponownie.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-178">Close the app, and re-run it.</span></span>  <span data-ttu-id="2ea6b-179">Zwróć uwagę, jak sesji użytkownika pozostanie niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-179">Notice how the user’s session remains intact.</span></span>  <span data-ttu-id="2ea6b-180">Wyloguj się i zaloguj się ponownie jako inny użytkownik.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="2ea6b-181">Biblioteka ADAL można łatwo zastosować wszystkie te typowe funkcje tożsamości w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-181">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="2ea6b-182">Zapewnia obsługę pracy dirty dla Ciebie — Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający użytkownika za pomocą interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-182">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="2ea6b-183">Tak naprawdę trzeba wiedzieć jednego wywołania interfejsu API, jest `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-183">All you really need to know is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="2ea6b-184">Odwołania, jest dostępne ukończone próbka (bez wartości konfiguracji) [tutaj](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="2ea6b-184">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="2ea6b-185">Możesz teraz przejść do tożsamości dodatkowe scenariusze.</span><span class="sxs-lookup"><span data-stu-id="2ea6b-185">You can now move on to additional identity scenarios.</span></span>  <span data-ttu-id="2ea6b-186">Można spróbować:</span><span class="sxs-lookup"><span data-stu-id="2ea6b-186">You may want to try:</span></span>

[<span data-ttu-id="2ea6b-187">Zabezpieczanie interfejsu API za pomocą usługi Azure AD sieci Web .NET >></span><span class="sxs-lookup"><span data-stu-id="2ea6b-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

