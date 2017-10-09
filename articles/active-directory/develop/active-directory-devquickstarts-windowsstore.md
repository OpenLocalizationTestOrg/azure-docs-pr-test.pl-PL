---
title: aaaAzure sklepu AD Windows wprowadzenie | Dokumentacja firmy Microsoft
description: "Aplikacje ze Sklepu Windows kompilacji integracji z usługą Azure AD, logowania, które wywołanie usługi Azure AD chronione interfejsów API w trybie OAuth."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="3eac4-103">Integrowanie usługi Azure AD z aplikacji ze Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="3eac4-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="3eac4-104">Wcześniejsze niż wersja projektów i Sklepu Windows 8.1 nie są obsługiwane w programie Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3eac4-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="3eac4-105">Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="3eac4-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="3eac4-106">Jeśli projektujesz aplikacji dla Sklepu Windows hello Azure Active Directory (Azure AD) umożliwia proste i bezpośrednie tooauthenticate z użytkownikami przy użyciu ich kont usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3eac4-106">If you're developing apps for hello Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward tooauthenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="3eac4-107">Dzięki integracji z usługą Azure AD, aplikacji można bezpiecznie korzystać z dowolnej sieci web interfejsu API, która jest chroniona przez usługę Azure AD, takie jak hello interfejsami API usługi Office 365 lub hello interfejsu API usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="3eac4-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="3eac4-108">Dla Sklepu Windows aplikacji klasycznych wymagające tooaccess chronionych zasobów Usługa Azure AD zapewnia hello Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="3eac4-108">For Windows Store desktop apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="3eac4-109">jedynym celem ADAL Hello jest toomake go łatwo tokenów dostępu tooget aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3eac4-109">hello sole purpose of ADAL is toomake it easy for hello app tooget access tokens.</span></span> <span data-ttu-id="3eac4-110">toodemonstrate, jak łatwo jest, w tym artykule opisano, jak toobuild DirectorySearcher ze Sklepu Windows aplikacji który:</span><span class="sxs-lookup"><span data-stu-id="3eac4-110">toodemonstrate how easy it is, this article shows how toobuild a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="3eac4-111">Pobiera dostępu tokenów do wywoływania interfejsu API Azure AD Graph hello przy użyciu hello [protokół uwierzytelniania OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="3eac4-111">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="3eac4-112">Przeszukuje katalog dla użytkowników z główną nazwę użytkownika (UPN).</span><span class="sxs-lookup"><span data-stu-id="3eac4-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="3eac4-113">Znaki użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3eac4-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="3eac4-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="3eac4-114">Before you get started</span></span>
* <span data-ttu-id="3eac4-115">Pobierz hello [szkielet projektu](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), lub pobrać hello [ukończone próbki](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="3eac4-115">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="3eac4-116">Każdego pobrania to rozwiązanie Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="3eac4-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="3eac4-117">Należy również dzierżawa usługi Azure AD, w których użytkownicy toocreate i aplikacji hello rejestru.</span><span class="sxs-lookup"><span data-stu-id="3eac4-117">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="3eac4-118">Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="3eac4-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="3eac4-119">Gdy wszystko będzie gotowe, wykonaj procedury hello hello trzech kolejnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="3eac4-119">When you are ready, follow hello procedures in hello next three sections.</span></span>

## <a name="step-1-register-hello-directorysearcher-app"></a><span data-ttu-id="3eac4-120">Krok 1: Rejestrowanie aplikacji DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="3eac4-120">Step 1: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="3eac4-121">tooenable tokenów tooget aplikacji hello, musisz najpierw tooregister w usługi Azure AD dzierżawy i udzielić jej uprawnienia tooaccess hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="3eac4-121">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="3eac4-122">Oto kroki tej procedury:</span><span class="sxs-lookup"><span data-stu-id="3eac4-122">Here's how:</span></span>

1. <span data-ttu-id="3eac4-123">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3eac4-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3eac4-124">Na górnym pasku powitania kliknij swoje konto.</span><span class="sxs-lookup"><span data-stu-id="3eac4-124">On hello top bar, click your account.</span></span> <span data-ttu-id="3eac4-125">Następnie w obszarze hello **katalogu** listy, wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3eac4-125">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="3eac4-126">Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3eac4-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="3eac4-127">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="3eac4-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="3eac4-128">Wykonaj hello monity toocreate **natywną aplikację kliencką**.</span><span class="sxs-lookup"><span data-stu-id="3eac4-128">Follow hello prompts toocreate a **Native Client Application**.</span></span>
  * <span data-ttu-id="3eac4-129">**Nazwa** opisuje toousers aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3eac4-129">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="3eac4-130">**Identyfikator URI przekierowania** to kombinacja schemat i ciąg używany tooreturn odpowiedzi tokenu w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3eac4-130">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="3eac4-131">Wprowadź wartość symbolu zastępczego teraz (na przykład **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="3eac4-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="3eac4-132">Będzie Zamień wartość hello później.</span><span class="sxs-lookup"><span data-stu-id="3eac4-132">You'll replace hello value later.</span></span>
6. <span data-ttu-id="3eac4-133">Po zakończeniu rejestracji hello Azure AD przypisuje aplikacji hello identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="3eac4-133">After you’ve completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="3eac4-134">Kopiuj wartość hello na powitania **aplikacji** karcie, ponieważ będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="3eac4-134">Copy hello value on hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="3eac4-135">Na powitania **ustawienia** wybierz pozycję **wymagane uprawnienia**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="3eac4-135">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="3eac4-136">Dla hello **usługi Azure Active Directory** aplikacji, wybierz opcję **Microsoft Graph** jako hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3eac4-136">For hello **Azure Active Directory** app, select **Microsoft Graph** as hello API.</span></span>
9. <span data-ttu-id="3eac4-137">W obszarze **delegowane uprawnienia**, Dodaj hello **dostępu do katalogu hello jako hello zalogowanego użytkownika** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="3eac4-137">Under **Delegated Permissions**, add hello **Access hello directory as hello signed-in user** permission.</span></span> <span data-ttu-id="3eac4-138">Umożliwi to aplikacja hello tooquery hello interfejsu API programu Graph dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3eac4-138">Doing so enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="3eac4-139">Krok 2: Instalowanie i konfigurowanie biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="3eac4-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="3eac4-140">Teraz, gdy masz aplikację w usłudze Azure AD, można zainstalować biblioteki ADAL i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3eac4-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="3eac4-141">tooenable toocommunicate ADAL w usłudze Azure AD, nadaj pewne informacje o rejestracji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3eac4-141">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="3eac4-142">Dodaj projekt DirectorySearcher ADAL toohello przy użyciu konsoli Menedżera pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="3eac4-142">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="3eac4-143">W projekcie DirectorySearcher hello Otwórz MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="3eac4-143">In hello DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="3eac4-144">Zastąp wartości hello hello **wartości konfiguracji** region hello wartości, które wprowadzono w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3eac4-144">Replace hello values in hello **Config Values** region with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="3eac4-145">Kod odnosi się wartości toothese zawsze, gdy używa biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="3eac4-145">Your code refers toothese values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="3eac4-146">Witaj *dzierżawy* jest hello domeny dzierżawy usługi Azure AD (np. contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="3eac4-146">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="3eac4-147">Witaj *clientId* jest hello identyfikator klienta aplikacji hello, który został skopiowany z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="3eac4-147">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
4. <span data-ttu-id="3eac4-148">Teraz należy toodiscover identyfikator URI wywołania zwrotnego powitania dla aplikacji ze Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="3eac4-148">You now need toodiscover hello callback URI for your Windows Store app.</span></span> <span data-ttu-id="3eac4-149">Ustaw punkt przerwania w tym wierszu hello `MainPage` metody:</span><span class="sxs-lookup"><span data-stu-id="3eac4-149">Set a breakpoint on this line in hello `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="3eac4-150">Utworzenie rozwiązania hello, upewniając się, że wszystkie odwołania do pakietu zostaną przywrócone.</span><span class="sxs-lookup"><span data-stu-id="3eac4-150">Build hello solution, making sure that all package references are restored.</span></span> <span data-ttu-id="3eac4-151">Jeśli brakuje żadnych pakietów, otwórz hello Menedżera pakietów NuGet, a następnie przywrócić je.</span><span class="sxs-lookup"><span data-stu-id="3eac4-151">If any packages are missing, open hello NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="3eac4-152">Uruchamianie aplikacji hello i skopiuj wartość hello `redirectUri` po hello przerwania zostaje trafiony.</span><span class="sxs-lookup"><span data-stu-id="3eac4-152">Run hello app, and copy hello value of `redirectUri` when hello breakpoint is hit.</span></span> <span data-ttu-id="3eac4-153">wartość Hello powinien wyglądać jak poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="3eac4-153">hello value should look something like hello following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="3eac4-154">Wróć na powitania **ustawienia** kartę aplikacji hello w hello portalu Azure, Dodaj **RedirectUri** z hello poprzedzających wartość.</span><span class="sxs-lookup"><span data-stu-id="3eac4-154">Back on hello **Settings** tab of hello app in hello Azure portal, add a **RedirectUri** with hello preceding value.</span></span>  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="3eac4-155">Krok 3: Użyj ADAL tooget tokenów z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eac4-155">Step 3: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="3eac4-156">Witaj podstawową zasadą za ADAL jest czy zawsze, gdy aplikacja hello potrzebuje tokenu dostępu, po prostu wywołuje `authContext.AcquireToken(…)`, i ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="3eac4-156">hello basic principle behind ADAL is that whenever hello app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="3eac4-157">Inicjowanie aplikacji hello `AuthenticationContext`, która jest hello klasy podstawowej biblioteki adal.</span><span class="sxs-lookup"><span data-stu-id="3eac4-157">Initialize hello app’s `AuthenticationContext`, which is hello primary class of ADAL.</span></span> <span data-ttu-id="3eac4-158">Ta akcja przekazuje współrzędne ADAL hello wymaga toocommunicate z usługą Azure AD i poinformuj go jak toocache tokenów.</span><span class="sxs-lookup"><span data-stu-id="3eac4-158">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="3eac4-159">Zlokalizuj hello `Search(...)` metodę, która jest wywoływana, gdy użytkownik kliknie hello **wyszukiwania** przycisk w Interfejsie użytkownika aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3eac4-159">Locate hello `Search(...)` method, which is invoked when users click hello **Search** button on hello app's UI.</span></span> <span data-ttu-id="3eac4-160">Ta metoda ułatwia tworzenie tooquery toohello interfejsu API usługi Azure AD Graph żądania get do użytkowników, których nazwy UPN zaczyna się hello danego wyszukiwanego terminu.</span><span class="sxs-lookup"><span data-stu-id="3eac4-160">This method makes a get request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span> <span data-ttu-id="3eac4-161">Witaj tooquery interfejsu API programu Graph, obejmują token dostępu w żądaniu hello **autoryzacji** nagłówka.</span><span class="sxs-lookup"><span data-stu-id="3eac4-161">tooquery hello Graph API, include an access token in hello request's **Authorization** header.</span></span> <span data-ttu-id="3eac4-162">Jest to, gdzie ADAL jest dostarczany.</span><span class="sxs-lookup"><span data-stu-id="3eac4-162">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="3eac4-163">Gdy aplikacja hello żąda token przez wywołanie metody `AcquireTokenAsync(...)`, ADAL prób tooreturn token bez monitowania użytkownika hello o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="3eac4-163">When hello app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span> <span data-ttu-id="3eac4-164">Jeśli ADAL ustali, że ten użytkownik hello musi toosign w tooget token, wyświetla okno dialogowe logowania, służy do zbierania poświadczeń użytkownika hello i zwraca token po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="3eac4-164">If ADAL determines that hello user needs toosign in tooget a token, it displays a sign-in dialog box, collects hello user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="3eac4-165">Jeśli ADAL zostanie tooreturn tokenu z jakiegokolwiek powodu, hello *AuthenticationResult* stanu błędu.</span><span class="sxs-lookup"><span data-stu-id="3eac4-165">If ADAL is unable tooreturn a token for any reason, hello *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="3eac4-166">Teraz jest token dostępu hello toouse czasu, uzyskanych.</span><span class="sxs-lookup"><span data-stu-id="3eac4-166">Now it's time toouse hello access token you just acquired.</span></span> <span data-ttu-id="3eac4-167">Również w hello `Search(...)` metody, Dołącz hello toohello token interfejsu API programu Graph pobrać żądania w hello **autoryzacji** nagłówka:</span><span class="sxs-lookup"><span data-stu-id="3eac4-167">Also in hello `Search(...)` method, attach hello token toohello Graph API get request in hello **Authorization** header:</span></span>

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="3eac4-168">Można użyć hello `AuthenticationResult` obiekt toodisplay informacji na temat hello użytkownika w aplikacji hello, takie jak nazwa użytkownika hello:</span><span class="sxs-lookup"><span data-stu-id="3eac4-168">You can use hello `AuthenticationResult` object toodisplay information about hello user in hello app, such as hello user's ID:</span></span>

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="3eac4-169">Umożliwia także użytkowników ADAL toosign z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3eac4-169">You can also use ADAL toosign users out of hello app.</span></span> <span data-ttu-id="3eac4-170">Po kliknięciu przez użytkownika hello hello **Wyloguj** przycisku, upewnij się, hello kolejnego połączenia z tym zbyt`AcquireTokenAsync(...)` przedstawia widok logowania.</span><span class="sxs-lookup"><span data-stu-id="3eac4-170">When hello user clicks hello **Sign Out** button, ensure that hello next call too`AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="3eac4-171">Przy użyciu biblioteki ADAL ta akcja jest tak proste, jak czyszczenie pamięci podręcznej tokenu hello:</span><span class="sxs-lookup"><span data-stu-id="3eac4-171">With ADAL, this action is as easy as clearing hello token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="3eac4-172">Co dalej</span><span class="sxs-lookup"><span data-stu-id="3eac4-172">What's next</span></span>
<span data-ttu-id="3eac4-173">Masz teraz pracy aplikacji do Sklepu Windows, który może uwierzytelniać użytkowników, bezpiecznie wywołać przy użyciu protokołu OAuth 2.0 interfejsów API sieci web i uzyskać podstawowe informacje o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="3eac4-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about hello user.</span></span>

<span data-ttu-id="3eac4-174">Jeśli nie zostało już wypełnione dzierżawy z użytkownikami, teraz jest toodo czas hello tak.</span><span class="sxs-lookup"><span data-stu-id="3eac4-174">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>
1. <span data-ttu-id="3eac4-175">Uruchom aplikację DirectorySearcher, a następnie zaloguj się przy użyciu jednego z hello użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3eac4-175">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="3eac4-176">Wyszukiwać innych użytkowników, w oparciu o ich nazwy UPN.</span><span class="sxs-lookup"><span data-stu-id="3eac4-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="3eac4-177">Aplikacja hello Zamknij i ponownie ją uruchomić.</span><span class="sxs-lookup"><span data-stu-id="3eac4-177">Close hello app, and rerun it.</span></span> <span data-ttu-id="3eac4-178">Zwróć uwagę, jak hello sesja pozostanie niezmieniona.</span><span class="sxs-lookup"><span data-stu-id="3eac4-178">Notice how hello user’s session remains intact.</span></span>
4. <span data-ttu-id="3eac4-179">Wyloguj się, klikając prawym przyciskiem myszy toodisplay hello dolnym pasku, a następnie zalogować się jako inny użytkownik.</span><span class="sxs-lookup"><span data-stu-id="3eac4-179">Sign out by right-clicking toodisplay hello bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="3eac4-180">Biblioteka ADAL umożliwia łatwe tooincorporate wszystkie te wspólne tożsamości funkcje do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3eac4-180">ADAL makes it easy tooincorporate all these common identity features into hello app.</span></span> <span data-ttu-id="3eac4-181">Go zajmuje się wszystkie hello dirty pracy, takich jak zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika za pomocą interfejsu użytkownika, nazwy logowania i odświeżanie wygasła tokenów.</span><span class="sxs-lookup"><span data-stu-id="3eac4-181">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="3eac4-182">Należy wywołania tooknow tylko jednego interfejsu API `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="3eac4-182">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="3eac4-183">Odwołania, Pobierz hello [ukończone próbki](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (bez wartości konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="3eac4-183">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="3eac4-184">Możesz teraz przejść na tooadditional tożsamości scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="3eac4-184">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="3eac4-185">Na przykład, spróbuj [zabezpieczyć interfejs API sieci Web .NET z usługą Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3eac4-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
