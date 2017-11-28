---
title: aaaAzure Windows Phone AD wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji Windows Phone, która integruje się z usługą Azure AD w celu logowania się i wymaga usługi Azure AD chronione w trybie OAuth interfejsów API."
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
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="47887-103">Integrowanie usługi Azure AD w aplikacji Windows Phone</span><span class="sxs-lookup"><span data-stu-id="47887-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="47887-104">Projekty systemu Windows Phone 8.1 i wcześniejszych nie są obsługiwane w programie Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="47887-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="47887-105">Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="47887-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="47887-106">Jeśli projektujesz aplikacji Windows Phone 8.1, usługi Azure AD umożliwia proste i bezpośrednie dla tooauthenticate możesz z użytkownikami przy użyciu ich kont usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="47887-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="47887-107">Umożliwia również toosecurely Twojej aplikacji korzystać z dowolnej sieci web interfejsu API chronione przez usługę Azure AD, takich jak hello interfejsami API usługi Office 365 lub hello interfejsu API Azure.</span><span class="sxs-lookup"><span data-stu-id="47887-107">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="47887-108">Ten przykładowy kod używa biblioteki ADAL w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="47887-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="47887-109">Hello najnowszych technologii, można spróbować tooinstead naszych [samouczek aplikacji uniwersalnych systemu Windows przy użyciu biblioteki ADAL w wersji 3.0](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="47887-109">For hello latest technology, you may want tooinstead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="47887-110">Jeśli tworzysz rzeczywiście aplikacji dla systemu Windows Phone 8.1, to hello w odpowiednim miejscu.</span><span class="sxs-lookup"><span data-stu-id="47887-110">If you are indeed building an app for Windows Phone 8.1, this is hello right place.</span></span>  <span data-ttu-id="47887-111">ADAL w wersji 2.0 jest nadal w pełni obsługiwane, a jest hello zalecany sposób tworzenie agianst aplikacji Windows Phone 8.1 przy użyciu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47887-111">ADAL v2.0 is still fully supported, and is hello recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="47887-112">W przypadku klientów platformy .NET native wymagające tooaccess chronionych zasobów usługi Azure AD zapewnia hello biblioteki uwierzytelniania usługi Active Directory lub biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="47887-112">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="47887-113">Jedynym celem ADAL jego życia jest toomake go łatwo tooget tokenów dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47887-113">ADAL’s sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="47887-114">toodemonstrate Ci, jak łatwo jest, w tym miejscu będzie budujemy "katalog modułu wyszukującego" aplikacji systemu Windows Phone 8.1 który:</span><span class="sxs-lookup"><span data-stu-id="47887-114">toodemonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="47887-115">Pobiera dostępu tokeny na potrzeby wywoływania hello Azure AD Graph API przy użyciu hello [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="47887-115">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="47887-116">Przeszukuje katalog dla użytkowników z danym głównej nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47887-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="47887-117">Znaki użytkowników.</span><span class="sxs-lookup"><span data-stu-id="47887-117">Signs users out.</span></span>

<span data-ttu-id="47887-118">toobuild hello pełną działającą aplikację, musisz:</span><span class="sxs-lookup"><span data-stu-id="47887-118">toobuild hello complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="47887-119">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47887-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="47887-120">Instalowanie i konfigurowanie biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="47887-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="47887-121">Używaj tokenów ADAL tooget z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47887-121">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="47887-122">Rozpoczęto, tooget [pobrać szkielet projektu](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="47887-122">tooget started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="47887-123">Każdy jest rozwiązanie Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="47887-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="47887-124">Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47887-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="47887-125">Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="47887-125">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directory-searcher-application"></a><span data-ttu-id="47887-126">1. Zarejestruj hello aplikacji poszukującego katalogu</span><span class="sxs-lookup"><span data-stu-id="47887-126">1. Register hello Directory Searcher Application</span></span>
<span data-ttu-id="47887-127">tooenable tokenów tooget aplikacji, musisz najpierw tooregister dzierżawy w usługi Azure AD i udzielić jej uprawnienia tooaccess hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="47887-127">tooenable your app tooget tokens, you’ll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="47887-128">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47887-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="47887-129">Na górnym pasku hello, kliknij na Twoim koncie, a w obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, którym chcesz tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47887-129">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="47887-130">Polecenie **więcej usług** w hello nawigacji po lewej stronie i wybierz polecenie **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47887-130">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="47887-131">Polecenie **rejestracji aplikacji** i wybierz polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="47887-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="47887-132">Postępuj zgodnie z monitami hello i utworzyć nową **natywną aplikację kliencką**.</span><span class="sxs-lookup"><span data-stu-id="47887-132">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="47887-133">Witaj **nazwa** z hello aplikacji opisano użytkownikom tooend aplikacji</span><span class="sxs-lookup"><span data-stu-id="47887-133">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="47887-134">Witaj **identyfikator Uri przekierowania** jest kombinacją schemat i ciąg, które będą używane przez usługi Azure AD tooreturn odpowiedzi tokenu.</span><span class="sxs-lookup"><span data-stu-id="47887-134">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="47887-135">Wprowadź wartość symbolu zastępczego teraz, np. `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="47887-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="47887-136">Firma Microsoft będzie później Zastąp tę wartość.</span><span class="sxs-lookup"><span data-stu-id="47887-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="47887-137">Po zakończeniu rejestracji usługi AAD przypisze aplikacji Unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47887-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="47887-138">Ta wartość jest potrzebny w kolejnych sekcjach hello, dlatego skopiuj go na karcie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="47887-138">You’ll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="47887-139">Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia** i wybierz polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="47887-139">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="47887-140">Wybierz hello **Microsoft Graph** jako hello interfejsu API i Dodaj hello **Czytaj dane katalogu** uprawnienie w obszarze **delegowane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="47887-140">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="47887-141">Spowoduje to włączenie użytkownika hello tooquery aplikacji interfejsu API programu Graph dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="47887-141">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="47887-142">2. Instalowanie i konfigurowanie biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="47887-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="47887-143">Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="47887-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="47887-144">Aby mogli toocommunicate ADAL toobe z usługą Azure AD, należy tooprovide go niektóre informacje o rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47887-144">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="47887-145">Rozpocznij, dodając ADAL toohello DirectorySearcher projektu przy użyciu konsoli Menedżera pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="47887-145">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="47887-146">W projekcie DirectorySearcher hello Otwórz `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="47887-146">In hello DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="47887-147">Zastąp wartości hello hello `Config Values` region tooreflect hello wartości danych wejściowych do hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="47887-147">Replace hello values in hello `Config Values` region tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="47887-148">Kod będzie odwoływać tych wartości, przy każdym użyciu biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="47887-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="47887-149">Witaj `tenant` jest hello domeny dzierżawy usługi Azure AD, np. contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="47887-149">hello `tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="47887-150">Witaj `clientId` jest clientId hello skopiowany z portalu hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47887-150">hello `clientId` is hello clientId of your application you copied from hello portal.</span></span>
* <span data-ttu-id="47887-151">Teraz należy toodiscover hello wywołania zwrotnego uri dla aplikacji Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="47887-151">You now need toodiscover hello callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="47887-152">Ustaw punkt przerwania w tym wierszu hello `MainPage` metody:</span><span class="sxs-lookup"><span data-stu-id="47887-152">Set a breakpoint on this line in hello `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="47887-153">Uruchamianie aplikacji hello i skopiuj Odłóż wartość hello `redirectUri` po hello przerwania zostaje trafiony.</span><span class="sxs-lookup"><span data-stu-id="47887-153">Run hello app, and copy aside hello value of `redirectUri` when hello breakpoint is hit.</span></span>  <span data-ttu-id="47887-154">Powinien on wyglądać podobnie jak</span><span class="sxs-lookup"><span data-stu-id="47887-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="47887-155">Wróć na powitania **Konfiguruj** kartę aplikacji hello portalu zarządzania Azure, zastąp wartość hello hello **RedirectUri** o tej wartości.</span><span class="sxs-lookup"><span data-stu-id="47887-155">Back on hello **Configure** tab of your application in hello Azure Management Portal, replace hello value of hello **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="47887-156">3. Używaj tokenów ADAL tooGet z usługi AAD</span><span class="sxs-lookup"><span data-stu-id="47887-156">3. Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="47887-157">Witaj podstawową zasadą za ADAL jest czy zawsze, gdy Twoja aplikacja powinna tokenu dostępu, po prostu wywołuje `authContext.AcquireToken(…)`, i ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="47887-157">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="47887-158">pierwszym krokiem Hello jest tooinitialize aplikacji `AuthenticationContext` -ADAL obiektu klasy podstawowej.</span><span class="sxs-lookup"><span data-stu-id="47887-158">hello first step is tooinitialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="47887-159">Jest to, gdy przekazujesz ADAL hello współrzędne musi toocommunicate z usługą Azure AD i poinformuj go jak toocache tokenów.</span><span class="sxs-lookup"><span data-stu-id="47887-159">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="47887-160">Znajdź teraz hello `Search(...)` metodę, która będzie wywoływana, gdy przycisk "Wyszukiwanie" w Interfejsie użytkownika aplikacji hello hello hello cliks użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47887-160">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="47887-161">Ta metoda ułatwia tworzenie tooquery toohello interfejsu API usługi Azure AD Graph żądania GET do użytkowników, których nazwy UPN zaczyna się hello danego wyszukiwanego terminu.</span><span class="sxs-lookup"><span data-stu-id="47887-161">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="47887-162">Jednak w kolejności tooquery hello interfejsu API programu Graph, tooinclude ' access_token ' w hello `Authorization` żądania nagłówek hello — jest to, gdzie ADAL jest dostarczany.</span><span class="sxs-lookup"><span data-stu-id="47887-162">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="47887-163">Jeśli konieczne jest uwierzytelnianie interakcyjne, ADAL użyje Książka adresowa systemu (Windows, Windows Phone w sieci Web uwierzytelniania Broker) i [modelu kontynuacji](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD, zaloguj się na stronie.</span><span class="sxs-lookup"><span data-stu-id="47887-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sign in page.</span></span>  <span data-ttu-id="47887-164">Po zalogowaniu użytkownika hello Twoja aplikacja powinna toopass ADAL hello wyniki interakcji Książka adresowa systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="47887-164">When hello user signs in, your app needs toopass ADAL hello results of hello WAB interaction.</span></span>  <span data-ttu-id="47887-165">Jest tak proste, jak implementacja hello `ContinueWebAuthentication` interfejsu:</span><span class="sxs-lookup"><span data-stu-id="47887-165">This is as simple as implementing hello `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="47887-166">Teraz nadszedł czas toouse hello `AuthenticationResult` tego ADAL zwrócił tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47887-166">Now it's time toouse hello `AuthenticationResult` that ADAL returned tooyour app.</span></span>  <span data-ttu-id="47887-167">W hello `QueryGraph(...)` wywołania zwrotnego, Dołącz ' access_token ' hello nabył toohello żądanie GET w nagłówku autoryzacji hello:</span><span class="sxs-lookup"><span data-stu-id="47887-167">In hello `QueryGraph(...)` callback, attach hello access_token you acquired toohello GET request in hello Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="47887-168">Można również użyć hello `AuthenticationResult` obiekt toodisplay informacji na temat hello użytkownika w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47887-168">You can also use hello `AuthenticationResult` object toodisplay information about hello user in your app.</span></span> <span data-ttu-id="47887-169">W hello `QueryGraph(...)` metoda, użyj hello wynik tooshow hello identyfikatora użytkownika na stronie powitania:</span><span class="sxs-lookup"><span data-stu-id="47887-169">In hello `QueryGraph(...)` method, use hello result tooshow hello user's id on hello page:</span></span>

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="47887-170">Ponadto można użyć użytkownika hello ADAL toosign z aplikacji, a także.</span><span class="sxs-lookup"><span data-stu-id="47887-170">Finally, you can use ADAL toosign hello user out of hte application as well.</span></span>  <span data-ttu-id="47887-171">Gdy hello użytkownik kliknie przycisk "Wyloguj" hello, chcemy tooensure, który hello następne wywołanie za`AcquireTokenSilentAsync(...)` zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="47887-171">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="47887-172">Przy użyciu biblioteki ADAL jest tak proste, jak czyszczenie pamięci podręcznej tokenu hello:</span><span class="sxs-lookup"><span data-stu-id="47887-172">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="47887-173">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="47887-173">Congratulations!</span></span> <span data-ttu-id="47887-174">Teraz masz pracy aplikacji Windows Phone, który ma hello możliwości tooauthenticate użytkowników, bezpiecznie wywoływać interfejsy API sieci Web przy użyciu protokołu OAuth 2.0, a uzyskać podstawowe informacje o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="47887-174">You now have a working Windows Phone app that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="47887-175">Jeśli nie jest jeszcze teraz jest hello toopopulate czas dzierżawy z niektórych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="47887-175">If you haven’t already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="47887-176">Uruchom aplikację DirectorySearcher i zaloguj się przy użyciu jednej z tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="47887-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="47887-177">Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.</span><span class="sxs-lookup"><span data-stu-id="47887-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="47887-178">Aplikacja hello Zamknij i uruchom je ponownie.</span><span class="sxs-lookup"><span data-stu-id="47887-178">Close hello app, and re-run it.</span></span>  <span data-ttu-id="47887-179">Zwróć uwagę, jak hello sesja pozostanie niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="47887-179">Notice how hello user’s session remains intact.</span></span>  <span data-ttu-id="47887-180">Wyloguj się i zaloguj się ponownie jako inny użytkownik.</span><span class="sxs-lookup"><span data-stu-id="47887-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="47887-181">Biblioteka ADAL umożliwia łatwe tooincorporate wszystkie te typowe funkcje tożsamości w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47887-181">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="47887-182">Zapewnia obsługę wszystkich hello dirty pracy dla Ciebie — Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika za pomocą interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="47887-182">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="47887-183">Naprawdę tooknow wystarczy jednego wywołania interfejsu API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="47887-183">All you really need tooknow is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="47887-184">Odwołania, przykładowy ukończyć powitalnych (bez wartości konfiguracji) jest dostarczany [tutaj](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="47887-184">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="47887-185">Możesz teraz przejść na tooadditional tożsamości scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="47887-185">You can now move on tooadditional identity scenarios.</span></span>  <span data-ttu-id="47887-186">Można tootry:</span><span class="sxs-lookup"><span data-stu-id="47887-186">You may want tootry:</span></span>

[<span data-ttu-id="47887-187">Zabezpieczanie interfejsu API za pomocą usługi Azure AD sieci Web .NET >></span><span class="sxs-lookup"><span data-stu-id="47887-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

