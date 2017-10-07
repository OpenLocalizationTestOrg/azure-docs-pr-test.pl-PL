---
title: aaaAzure AD Xamarin wprowadzenie | Dokumentacja firmy Microsoft
description: "Tworzenie aplikacji platformy Xamarin integracji z usługą Azure AD, logowania i wywoływanie Azure API chronione przez usługi AD w trybie OAuth."
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="0dddf-103">Integrowanie usługi Azure AD przy użyciu aplikacji Xamarin</span><span class="sxs-lookup"><span data-stu-id="0dddf-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="0dddf-104">Za pomocą platformy Xamarin można napisać aplikacji mobilnych w języku C#, który można uruchomić w systemach iOS, Android i Windows (urządzeń przenośnych i komputerów).</span><span class="sxs-lookup"><span data-stu-id="0dddf-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="0dddf-105">Jeśli tworzysz aplikację za pomocą platformy Xamarin usługi Azure Active Directory (Azure AD) umożliwia proste tooauthenticate użytkownikom ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dddf-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple tooauthenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="0dddf-106">Aplikacja Hello także bezpiecznie może używać dowolnego interfejsu API sieci web chronionej przez usługę Azure AD, takie jak hello interfejsami API usługi Office 365 lub hello interfejsu API usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="0dddf-106">hello app can also securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="0dddf-107">W przypadku aplikacji platformy Xamarin wymagające tooaccess chronionych zasobów usługi Azure AD zapewnia hello Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="0dddf-107">For Xamarin apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="0dddf-108">jedynym celem ADAL Hello jest toomake go łatwo tokenów dostępu tooget aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0dddf-108">hello sole purpose of ADAL is toomake it easy for apps tooget access tokens.</span></span> <span data-ttu-id="0dddf-109">toodemonstrate, jak łatwo jest, w tym artykule przedstawiono sposób aplikacji DirectorySearcher toobuild który:</span><span class="sxs-lookup"><span data-stu-id="0dddf-109">toodemonstrate how easy it is, this article shows how toobuild DirectorySearcher apps that:</span></span>

* <span data-ttu-id="0dddf-110">Uruchom na systemu iOS, Android, Windows Desktop, Windows Phone i Sklep Windows.</span><span class="sxs-lookup"><span data-stu-id="0dddf-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="0dddf-111">Użyj jednej klasy przenośnej biblioteki (PCL) tooauthenticate użytkowników i uzyskać tokenów dla hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="0dddf-111">Use a single portable class library (PCL) tooauthenticate users and get tokens for hello Azure AD Graph API.</span></span>
* <span data-ttu-id="0dddf-112">Wyszukaj katalog dla użytkowników z danym głównej nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0dddf-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="0dddf-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="0dddf-113">Before you get started</span></span>
* <span data-ttu-id="0dddf-114">Pobierz hello [szkielet projektu](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), lub pobrać hello [ukończone próbki](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="0dddf-114">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="0dddf-115">Każdego pobrania to rozwiązanie Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="0dddf-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="0dddf-116">Należy również dzierżawa usługi Azure AD, w których użytkownicy toocreate i aplikacji hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="0dddf-116">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="0dddf-117">Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="0dddf-117">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="0dddf-118">Gdy wszystko będzie gotowe, wykonaj procedury hello hello obok cztery sekcje.</span><span class="sxs-lookup"><span data-stu-id="0dddf-118">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="0dddf-119">Krok 1: Konfigurowanie środowiska deweloperskiego Xamarin</span><span class="sxs-lookup"><span data-stu-id="0dddf-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="0dddf-120">Ten samouczek zawiera projektów dla systemu iOS, Android i Windows, należy Xamarin i Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0dddf-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="0dddf-121">toocreate hello wymagane środowisko, hello ukończenia procesu w [ustawić Konfigurowanie i instalowanie programu Visual Studio i Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="0dddf-121">toocreate hello necessary environment, complete hello process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="0dddf-122">instrukcje Hello obejmować materiału, który można przejrzeć toolearn więcej informacji na temat platformy Xamarin w trakcie oczekiwania dla toobe instalacje hello ukończone.</span><span class="sxs-lookup"><span data-stu-id="0dddf-122">hello instructions include material that you can review toolearn more about Xamarin while you're waiting for hello installations toobe completed.</span></span>

<span data-ttu-id="0dddf-123">Po zakończeniu instalacji hello Otwórz rozwiązanie hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0dddf-123">After you've completed hello setup, open hello solution in Visual Studio.</span></span> <span data-ttu-id="0dddf-124">Istnieje, można znaleźć projektów sześciu: pięć projektów specyficzne dla platformy i jeden PCL, DirectorySearcher.cs, które będą udostępniane na wszystkich platformach.</span><span class="sxs-lookup"><span data-stu-id="0dddf-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-hello-directorysearcher-app"></a><span data-ttu-id="0dddf-125">Krok 2: Rejestrowanie aplikacji DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="0dddf-125">Step 2: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="0dddf-126">tooenable tokenów tooget aplikacji hello, musisz najpierw tooregister w usługi Azure AD dzierżawy i udzielić jej uprawnienia tooaccess hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="0dddf-126">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="0dddf-127">Oto kroki tej procedury:</span><span class="sxs-lookup"><span data-stu-id="0dddf-127">Here's how:</span></span>

1. <span data-ttu-id="0dddf-128">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0dddf-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0dddf-129">Na górnym pasku powitania kliknij swoje konto.</span><span class="sxs-lookup"><span data-stu-id="0dddf-129">On hello top bar, click your account.</span></span> <span data-ttu-id="0dddf-130">Następnie w obszarze hello **katalogu** listy, wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0dddf-130">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="0dddf-131">Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0dddf-131">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="0dddf-132">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0dddf-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="0dddf-133">toocreate nowy **natywną aplikację kliencką**, postępuj zgodnie z monitami hello.</span><span class="sxs-lookup"><span data-stu-id="0dddf-133">toocreate a new **Native Client Application**, follow hello prompts.</span></span>
  * <span data-ttu-id="0dddf-134">**Nazwa** opisuje toousers aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0dddf-134">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="0dddf-135">**Identyfikator URI przekierowania** to kombinacja schemat i ciąg używany tooreturn odpowiedzi tokenu w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dddf-135">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="0dddf-136">Wprowadź wartość (na przykład http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="0dddf-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="0dddf-137">Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji hello identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="0dddf-137">After you’ve completed registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="0dddf-138">Skopiuj wartość hello z hello **aplikacji** karcie, ponieważ będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="0dddf-138">Copy hello value from hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="0dddf-139">Na powitania **ustawienia** wybierz pozycję **wymagane uprawnienia**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0dddf-139">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="0dddf-140">Wybierz **Microsoft Graph** jako hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="0dddf-140">Select **Microsoft Graph** as hello API.</span></span> <span data-ttu-id="0dddf-141">W obszarze **delegowane uprawnienia**, Dodaj hello **Czytaj dane katalogu** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="0dddf-141">Under **Delegated Permissions**, add hello **Read Directory Data** permission.</span></span>  
<span data-ttu-id="0dddf-142">Ta akcja umożliwia aplikacji hello tooquery hello interfejsu API programu Graph dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0dddf-142">This action enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="0dddf-143">Krok 3: Instalowanie i konfigurowanie biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="0dddf-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="0dddf-144">Teraz, gdy masz aplikację w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="0dddf-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="0dddf-145">tooenable toocommunicate ADAL w usłudze Azure AD, nadaj pewne informacje o rejestracji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0dddf-145">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="0dddf-146">Dodaj projekt DirectorySearcher ADAL toohello przy użyciu konsoli Menedżera pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="0dddf-146">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    <span data-ttu-id="0dddf-147">Należy pamiętać, że dwa odwołania biblioteki są dodawane tooeach projektu: hello PCL część ADAL i części specyficzne dla platformy.</span><span class="sxs-lookup"><span data-stu-id="0dddf-147">Note that two library references are added tooeach project: hello PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="0dddf-148">W projekcie DirectorySearcherLib hello Otwórz DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="0dddf-148">In hello DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="0dddf-149">Zastąp wartości elementu członkowskiego klasy hello hello wartości, które wprowadzono w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0dddf-149">Replace hello class member values with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="0dddf-150">Kod odnosi się wartości toothese zawsze, gdy używa biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="0dddf-150">Your code refers toothese values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="0dddf-151">Witaj *dzierżawy* jest hello domeny dzierżawy usługi Azure AD (np. contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="0dddf-151">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="0dddf-152">Witaj *clientId* jest hello identyfikator klienta aplikacji hello, który został skopiowany z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="0dddf-152">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
  * <span data-ttu-id="0dddf-153">Witaj *returnUri* jest hello przekierowania URI, który został wprowadzony w portalu hello (na przykład http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="0dddf-153">hello *returnUri* is hello redirect URI that you entered in hello portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="0dddf-154">Krok 4: Użyj ADAL tooget tokenów z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dddf-154">Step 4: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="0dddf-155">Prawie wszystkie logika uwierzytelniania aplikacji hello znajduje się `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="0dddf-155">Almost all of hello app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="0dddf-156">Wszystko, co jest niezbędne w projektach specyficzne dla platformy hello jest toopass toohello parametru kontekstowego `DirectorySearcher` PCL.</span><span class="sxs-lookup"><span data-stu-id="0dddf-156">All that's necessary in hello platform-specific projects is toopass a contextual parameter toohello `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="0dddf-157">Otwórz DirectorySearcher.cs, a następnie dodaj nowe toohello parametr `SearchByAlias(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="0dddf-157">Open DirectorySearcher.cs, and then add a new parameter toohello `SearchByAlias(...)` method.</span></span> <span data-ttu-id="0dddf-158">`IPlatformParameters`jest uwierzytelniania ADAL potrzeb tooperform hello obiekty hello kontekstowe parametr, który hermetyzuje hello specyficzne dla platformy.</span><span class="sxs-lookup"><span data-stu-id="0dddf-158">`IPlatformParameters` is hello contextual parameter that encapsulates hello platform-specific objects that ADAL needs tooperform hello authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="0dddf-159">Inicjowanie `AuthenticationContext`, która jest hello klasy podstawowej biblioteki adal.</span><span class="sxs-lookup"><span data-stu-id="0dddf-159">Initialize `AuthenticationContext`, which is hello primary class of ADAL.</span></span>  
<span data-ttu-id="0dddf-160">Witaj ADAL przekazuje akcji koordynuje toocommunicate potrzeb z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dddf-160">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD.</span></span>
3. <span data-ttu-id="0dddf-161">Wywołanie `AcquireTokenAsync(...)`, który akceptuje hello `IPlatformParameters` obiektu i wywołuje hello przepływ uwierzytelniania, który jest konieczne tooreturn aplikacji toohello tokenu.</span><span class="sxs-lookup"><span data-stu-id="0dddf-161">Call `AcquireTokenAsync(...)`, which accepts hello `IPlatformParameters` object and invokes hello authentication flow that's necessary tooreturn a token toohello app.</span></span>

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    <span data-ttu-id="0dddf-162">`AcquireTokenAsync(...)`pierwszy tooreturn prób token dla hello żądanego zasobu (hello interfejsu API programu Graph w tym przypadku) bez monitowania użytkowników tooenter poświadczeń (za pośrednictwem buforowanie lub odświeżanie starego tokeny).</span><span class="sxs-lookup"><span data-stu-id="0dddf-162">`AcquireTokenAsync(...)` first attempts tooreturn a token for hello requested resource (hello Graph API in this case) without prompting users tooenter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="0dddf-163">W razie potrzeby przedstawia on użytkowników strony logowania dla usługi Azure AD hello przed uzyskiwanie hello żądanego tokenu.</span><span class="sxs-lookup"><span data-stu-id="0dddf-163">As necessary, it shows users hello Azure AD sign-in page before acquiring hello requested token.</span></span>
4. <span data-ttu-id="0dddf-164">Dołącz hello żądanie interfejsu API programu Graph token toohello dostępu w hello **autoryzacji** nagłówka:</span><span class="sxs-lookup"><span data-stu-id="0dddf-164">Attach hello access token toohello Graph API request in hello **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="0dddf-165">To wszystko dla hello `DirectorySearcher` kodu dotyczące tożsamości PCL i hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0dddf-165">That's all for hello `DirectorySearcher` PCL and hello app's identity-related code.</span></span> <span data-ttu-id="0dddf-166">Liście nie zostanie toocall hello `SearchByAlias(...)` metody w widokach każdej platformy i, w miarę potrzeby kodu tooadd poprawnie obsługi hello cykl życia interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0dddf-166">All that remains is toocall hello `SearchByAlias(...)` method in each platform's views and, where necessary, tooadd code for correctly handling hello UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="0dddf-167">Android</span><span class="sxs-lookup"><span data-stu-id="0dddf-167">Android</span></span>
1. <span data-ttu-id="0dddf-168">W MainActivity.cs, dodaj wywołanie za`SearchByAlias(...)` przycisku powitania kliknij program obsługi:</span><span class="sxs-lookup"><span data-stu-id="0dddf-168">In MainActivity.cs, add a call too`SearchByAlias(...)` in hello button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="0dddf-169">Zastąpienie hello `OnActivityResult` tooforward metody cykl życia uwierzytelniania przekierowuje wstecz toohello odpowiedniej metody.</span><span class="sxs-lookup"><span data-stu-id="0dddf-169">Override hello `OnActivityResult` lifecycle method tooforward any authentication redirects back toohello appropriate method.</span></span> <span data-ttu-id="0dddf-170">Biblioteka ADAL udostępnia metodę pomocnika dla tego w systemie Android:</span><span class="sxs-lookup"><span data-stu-id="0dddf-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="0dddf-171">System Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="0dddf-171">Windows Desktop</span></span>
<span data-ttu-id="0dddf-172">W MainWindow.xaml.cs, nawiązywanie połączeń za`SearchByAlias(...)` przez przekazanie `WindowInteropHelper` na pulpicie hello `PlatformParameters` obiektu:</span><span class="sxs-lookup"><span data-stu-id="0dddf-172">In MainWindow.xaml.cs, make a call too`SearchByAlias(...)` by passing a `WindowInteropHelper` in hello desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="0dddf-173">iOS</span><span class="sxs-lookup"><span data-stu-id="0dddf-173">iOS</span></span>
<span data-ttu-id="0dddf-174">W DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` obiektu przyjmuje odwołanie toohello kontrolera widoku:</span><span class="sxs-lookup"><span data-stu-id="0dddf-174">In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` object takes a reference toohello View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="0dddf-175">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="0dddf-175">Windows Universal</span></span>
<span data-ttu-id="0dddf-176">W uniwersalnych systemu Windows otwórz MainPage.xaml.cs, a następnie wdrożyć hello `Search` metody.</span><span class="sxs-lookup"><span data-stu-id="0dddf-176">In Windows Universal, open MainPage.xaml.cs, and then implement hello `Search` method.</span></span> <span data-ttu-id="0dddf-177">Ta metoda używa metody pomocnika w projekcie udostępnionym tooupdate interfejsu użytkownika w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="0dddf-177">This method uses a helper method in a shared project tooupdate UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="0dddf-178">Co dalej</span><span class="sxs-lookup"><span data-stu-id="0dddf-178">What's next</span></span>
<span data-ttu-id="0dddf-179">Masz teraz pracy aplikacji platformy Xamarin, który może uwierzytelniać użytkowników i bezpiecznie wywoływać interfejsy API sieci web przy użyciu protokołu OAuth 2.0 na pięciu różnych platformach.</span><span class="sxs-lookup"><span data-stu-id="0dddf-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="0dddf-180">Jeśli nie zostało już wypełnione dzierżawy z użytkownikami, teraz jest toodo czas hello tak.</span><span class="sxs-lookup"><span data-stu-id="0dddf-180">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>

1. <span data-ttu-id="0dddf-181">Uruchom aplikację DirectorySearcher, a następnie zaloguj się przy użyciu jednego z hello użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0dddf-181">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="0dddf-182">Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.</span><span class="sxs-lookup"><span data-stu-id="0dddf-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="0dddf-183">ADAL umożliwia łatwe tooincorporate wspólne funkcje tożsamości w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0dddf-183">ADAL makes it easy tooincorporate common identity features into hello app.</span></span> <span data-ttu-id="0dddf-184">Go zajmuje się wszystkie hello dirty pracy, takich jak zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika za pomocą interfejsu użytkownika, nazwy logowania i odświeżanie wygasła tokenów.</span><span class="sxs-lookup"><span data-stu-id="0dddf-184">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="0dddf-185">Należy wywołania tooknow tylko jednego interfejsu API `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="0dddf-185">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="0dddf-186">Odwołania, Pobierz hello [ukończone próbki](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (bez wartości konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="0dddf-186">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="0dddf-187">Możesz teraz przejść na tooadditional tożsamości scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="0dddf-187">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="0dddf-188">Na przykład, spróbuj [zabezpieczyć interfejs API sieci Web .NET z usługą Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0dddf-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
