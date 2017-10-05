---
title: "Dodaj logowanie do aplikacji systemu iOS przy użyciu punktu końcowego v2.0 usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak utworzyć aplikację systemu iOS logujący się użytkownicy z obu osobistego konta Microsoft i kont służbowych przy użyciu bibliotek innych firm."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: cf1455dc3d55ea3581195f7a315556d134c23a26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-ios-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="98610-103">Dodaj logowanie do aplikacji systemu iOS przy użyciu biblioteki innych firm z interfejsu API programu Graph przy użyciu punktu końcowego v2.0</span><span class="sxs-lookup"><span data-stu-id="98610-103">Add sign-in to an iOS app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="98610-104">Platforma Microsoft Identity korzysta z otwartych standardów, takich jak OAuth2 i OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="98610-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="98610-105">Deweloperzy mogą używać dowolnej bibliotece potrzebnymi do integracji z naszych usług.</span><span class="sxs-lookup"><span data-stu-id="98610-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="98610-106">Aby pomóc deweloperom korzystać z innych bibliotek platformy, możemy napisanych kilka wskazówki podobny do pokazują, jak skonfigurować biblioteki innych firm, aby nawiązać połączenia z platformą tożsamości Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98610-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="98610-107">Większość bibliotek, które implementują [specyfikację RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) można nawiązać połączenia z platformą tożsamości Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98610-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="98610-108">Aplikacja, która tworzy tego przewodnika użytkownicy mogą zalogować się do organizacji i wyszukać innych użytkowników w organizacji za pomocą interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="98610-108">With the application that this walkthrough creates, users can sign in to their organization and then search for others in their organization by using the Graph API.</span></span>

<span data-ttu-id="98610-109">Jeśli jesteś nowym użytkownikiem OAuth2 lub OpenID Connect, znacznie to przykładowa konfiguracja może nie mieć sensu do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="98610-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="98610-110">Zalecamy przeczytanie [protokołów v2.0 - przepływu kodu autoryzacji OAuth 2.0](active-directory-v2-protocols-oauth-code.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="98610-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="98610-111">Niektóre funkcje platformy, które mają wyrażenia OAuth2 lub OpenID Connect standardy, takie jak dostęp warunkowy i zarządzanie zasadami usługi Intune, trzeba użyć naszych Otwórz źródło bibliotek tożsamości usługi Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="98610-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="98610-112">Punktu końcowego v2.0 nie obsługuje wszystkich scenariuszy Azure Active Directory i funkcji.</span><span class="sxs-lookup"><span data-stu-id="98610-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="98610-113">Aby ustalić, czy należy używać punktu końcowego v2.0, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="98610-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="98610-114">Pobierz kod z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="98610-114">Download code from GitHub</span></span>
<span data-ttu-id="98610-115">Kod używany w tym samouczku jest przechowywany [ w serwisie GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="98610-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="98610-116">Aby z niego skorzystać, można [pobrać szkielet aplikacji w formie .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) lub sklonować szkielet:</span><span class="sxs-lookup"><span data-stu-id="98610-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="98610-117">Można także po prostu pobrać przykład i od razu rozpocząć:</span><span class="sxs-lookup"><span data-stu-id="98610-117">You can also just download the sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="98610-118">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="98610-118">Register an app</span></span>
<span data-ttu-id="98610-119">Utwórz nową aplikację na [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj szczegółowy opis kroków w [jak zarejestrować aplikację z punktem końcowym v2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="98610-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at  [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="98610-120">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="98610-120">Make sure to:</span></span>

* <span data-ttu-id="98610-121">Kopiuj **identyfikator aplikacji** przypisany do aplikacji, ponieważ będzie on potrzebny wkrótce.</span><span class="sxs-lookup"><span data-stu-id="98610-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="98610-122">Dodaj **Mobile** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98610-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="98610-123">Kopiuj **identyfikator URI przekierowania** z portalu.</span><span class="sxs-lookup"><span data-stu-id="98610-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="98610-124">Należy użyć wartości domyślnej `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="98610-124">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-the-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="98610-125">Pobierz biblioteki NXOAuth2 innych firm i tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="98610-125">Download the third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="98610-126">W ramach tego przewodnika skorzystasz OAuth2Client z serwisu GitHub, czyli OAuth2 biblioteki dla systemu Mac OS X i iOS (Cocoa i Cocoa touch).</span><span class="sxs-lookup"><span data-stu-id="98610-126">For this walkthrough, you will use the OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="98610-127">Ta biblioteka jest oparta na wersji 10 specyfikacji OAuth2.</span><span class="sxs-lookup"><span data-stu-id="98610-127">This library is based on draft 10 of the OAuth2 spec.</span></span> <span data-ttu-id="98610-128">Ona profil aplikacji natywnej implementuje i obsługuje punktu końcowego autoryzacji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="98610-128">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="98610-129">Są to wszystkie zadania, które należy zintegrować z platformą tożsamości Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98610-129">These are all the things you'll need to integrate with the Microsoft identity platform.</span></span>

### <a name="add-the-library-to-your-project-by-using-cocoapods"></a><span data-ttu-id="98610-130">Dodaj bibliotekę do projektu przy użyciu programu CocoaPods</span><span class="sxs-lookup"><span data-stu-id="98610-130">Add the library to your project by using CocoaPods</span></span>
<span data-ttu-id="98610-131">CocoaPods to menedżer zależności dla projektów Xcode.</span><span class="sxs-lookup"><span data-stu-id="98610-131">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="98610-132">Poprzednie kroki instalacji zarządza automatycznie.</span><span class="sxs-lookup"><span data-stu-id="98610-132">It manages the previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="98610-133">Dodaj następujący kod do tego pliku podfile:</span><span class="sxs-lookup"><span data-stu-id="98610-133">Add the following to this podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="98610-134">Załaduj podfile przy użyciu programu CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="98610-134">Load the podfile by using CocoaPods.</span></span> <span data-ttu-id="98610-135">Spowoduje to utworzenie nowego obszaru roboczego Xcode, który zostanie załadowany.</span><span class="sxs-lookup"><span data-stu-id="98610-135">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-the-structure-of-the-project"></a><span data-ttu-id="98610-136">Eksploruj struktury projektu</span><span class="sxs-lookup"><span data-stu-id="98610-136">Explore the structure of the project</span></span>
<span data-ttu-id="98610-137">Skonfigurowano następującą strukturę dla naszych projektu w szkielecie:</span><span class="sxs-lookup"><span data-stu-id="98610-137">The following structure is set up for our project in the skeleton:</span></span>

* <span data-ttu-id="98610-138">Widok wzorca wyszukiwania nazwy UPN</span><span class="sxs-lookup"><span data-stu-id="98610-138">A Master View with a UPN Search</span></span>
* <span data-ttu-id="98610-139">Widok szczegółów dla danych dotyczących wybranego użytkownika</span><span class="sxs-lookup"><span data-stu-id="98610-139">A Detail View for the data about the selected user</span></span>
* <span data-ttu-id="98610-140">Widok logowania, gdzie użytkownik może zalogować się do aplikacji do badania wykresu</span><span class="sxs-lookup"><span data-stu-id="98610-140">A Login View where a user can sign in to the app to query the graph</span></span>

<span data-ttu-id="98610-141">Firma Microsoft zostanie przeniesione do różnych plików w szkielecie dodać uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="98610-141">We will move to various files in the skeleton to add authentication.</span></span> <span data-ttu-id="98610-142">Inne części kodu, na przykład kod visual nie odnoszą się do tożsamości, ale są udostępniane dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="98610-142">Other parts of the code, such as the visual code, do not pertain to identity but are provided for you.</span></span>

## <a name="set-up-the-settingsplst-file-in-the-library"></a><span data-ttu-id="98610-143">Konfigurowanie pliku settings.plst w bibliotece</span><span class="sxs-lookup"><span data-stu-id="98610-143">Set up the settings.plst file in the library</span></span>
* <span data-ttu-id="98610-144">Otwórz projekt szybkiego startu `settings.plist` pliku.</span><span class="sxs-lookup"><span data-stu-id="98610-144">In the QuickStart project, open the `settings.plist` file.</span></span> <span data-ttu-id="98610-145">Zastąp wartości elementów w sekcji do wartości, które były używane w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="98610-145">Replace the values of the elements in the section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="98610-146">Kod będzie odwoływać tych wartości, przy każdym użyciu biblioteki uwierzytelniania usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="98610-146">Your code will reference these values whenever it uses the Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="98610-147">`clientId` Jest identyfikator klienta aplikacji, który został skopiowany z portalu.</span><span class="sxs-lookup"><span data-stu-id="98610-147">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="98610-148">`redirectUri` Jest adres URL przekierowania, czy dostarczono portalu.</span><span class="sxs-lookup"><span data-stu-id="98610-148">The `redirectUri` is the redirect URL that the portal provided.</span></span>

## <a name="set-up-the-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="98610-149">Konfigurowanie biblioteki NXOAuth2Client w Twojej LoginViewController</span><span class="sxs-lookup"><span data-stu-id="98610-149">Set up the NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="98610-150">Biblioteka NXOAuth2Client wymaga niektórych wartości do.</span><span class="sxs-lookup"><span data-stu-id="98610-150">The NXOAuth2Client library requires some values to get set up.</span></span> <span data-ttu-id="98610-151">Po ukończeniu zadania służy nabytych przez niego token do wywołania interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="98610-151">After you complete that task, you can use the acquired token to call the Graph API.</span></span> <span data-ttu-id="98610-152">Ponieważ `LoginView` zostanie wywołana dowolnej chwili, musimy uwierzytelniania, warto umieścić wartości konfiguracji do tego pliku.</span><span class="sxs-lookup"><span data-stu-id="98610-152">Because `LoginView` will be called any time we need to authenticate, it makes sense to put configuration values in to that file.</span></span>

* <span data-ttu-id="98610-153">Dodajmy niektórych wartości na `LoginViewController.m` plik, aby ustawić kontekst uwierzytelniania i autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="98610-153">Let's add some values to the  `LoginViewController.m` file to set the context for authentication and authorization.</span></span> <span data-ttu-id="98610-154">Szczegółowe informacje o wartości należy wykonać kod.</span><span class="sxs-lookup"><span data-stu-id="98610-154">Details about the values follow the code.</span></span>
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

<span data-ttu-id="98610-155">Oto szczegółowe informacje o kodzie.</span><span class="sxs-lookup"><span data-stu-id="98610-155">Let's look at details about the code.</span></span>

<span data-ttu-id="98610-156">Pierwszy ciąg jest przeznaczony dla `scopes`.</span><span class="sxs-lookup"><span data-stu-id="98610-156">The first string is for `scopes`.</span></span>  <span data-ttu-id="98610-157">`User.Read` Wartość umożliwia odczytanie profilu podstawowego zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="98610-157">The `User.Read` value allows you to read the basic profile of the signed in user.</span></span>

<span data-ttu-id="98610-158">Dowiedz się więcej o wszystkie dostępne zakresy na [zakresy uprawnień Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="98610-158">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="98610-159">Aby uzyskać `authURL`, `loginURL`, `bhh`, i `tokenURL`, należy użyć wartości podane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="98610-159">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use the values provided previously.</span></span> <span data-ttu-id="98610-160">Użycie typu open source bibliotek tożsamości usługi Microsoft Azure, możemy rozwiń tych danych można za pomocą naszych punktu końcowego metadanych.</span><span class="sxs-lookup"><span data-stu-id="98610-160">If you use the open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="98610-161">Włożyliśmy dużo wysiłku w wyodrębnianie tych wartości.</span><span class="sxs-lookup"><span data-stu-id="98610-161">We've done the hard work of extracting these values for you.</span></span>

<span data-ttu-id="98610-162">Wartość `keychain` to kontener, którego biblioteka NXOAuth2Client używa do tworzenia łańcucha kluczy do przechowywania tokenów.</span><span class="sxs-lookup"><span data-stu-id="98610-162">The `keychain` value is the container that the NXOAuth2Client library will use to create a keychain to store your tokens.</span></span> <span data-ttu-id="98610-163">Jeśli chcesz pobrać rejestracji jednokrotnej (SSO) w wielu aplikacjach, można określić tego samego łańcucha kluczy w każdej aplikacji i żądanie stosowania tego łańcucha kluczy w Twoje uprawnienia Xcode.</span><span class="sxs-lookup"><span data-stu-id="98610-163">If you'd like to get single sign-on (SSO) across numerous apps, you can specify the same keychain in each of your applications and request the use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="98610-164">Wyjaśnienie jest zawarte w dokumentacji firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="98610-164">This is explained in the Apple documentation.</span></span>

<span data-ttu-id="98610-165">Pozostała część te wartości są wymagane do korzystania z biblioteki oraz tworzenie miejsc do przenoszenia wartości w kontekście.</span><span class="sxs-lookup"><span data-stu-id="98610-165">The rest of these values are required to use the library and create places for you to carry values to the context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="98610-166">Tworzenie pamięci podręcznej adres URL</span><span class="sxs-lookup"><span data-stu-id="98610-166">Create a URL cache</span></span>
<span data-ttu-id="98610-167">Wewnątrz `(void)viewDidLoad()`, który zawsze jest wywoływana po załadowaniu widoku, pamięć podręczną do użytku w naszym primes następujący kod.</span><span class="sxs-lookup"><span data-stu-id="98610-167">Inside `(void)viewDidLoad()`, which is always called after the view is loaded, the following code primes a cache for our use.</span></span>

<span data-ttu-id="98610-168">Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="98610-168">Add the following code:</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="98610-169">Tworzenie widoku sieci Web dla logowania</span><span class="sxs-lookup"><span data-stu-id="98610-169">Create a WebView for sign-in</span></span>
<span data-ttu-id="98610-170">Widok sieci Web można monit o podanie dodatkowych czynników, takich jak wiadomość SMS (jeśli jest skonfigurowane) lub zwrócić komunikaty o błędach do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="98610-170">A WebView can prompt the user for additional factors like SMS text message (if configured) or return error messages to the user.</span></span> <span data-ttu-id="98610-171">W tym miejscu zostanie ustawiona konfigurowanie widoku sieci Web, a następnie napisać kod, aby obsłużyć wywołania zwrotne, które nastąpi w widoku sieci Web z usług tożsamości.</span><span class="sxs-lookup"><span data-stu-id="98610-171">Here you'll set up the WebView and then later write the code to handle the callbacks that will happen in the WebView from the identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //to sign in to Microsoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate to the URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-the-webview-methods-to-handle-authentication"></a><span data-ttu-id="98610-172">Przesłoń metody WebView na potrzeby obsługi uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="98610-172">Override the WebView methods to handle authentication</span></span>
<span data-ttu-id="98610-173">Aby przekazać widoku sieci Web, co się dzieje, gdy użytkownik musi zalogować się, jak wspomniano wcześniej, można Wklej następujący kod.</span><span class="sxs-lookup"><span data-stu-id="98610-173">To tell the WebView what happens when a user needs to sign in as discussed previously, you can paste the following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get the auth token from a redirect so we need to handle that in the webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // The webview is where all the communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if the UIWebView is showing our authorization URL or consent URL, show the UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read the Location from the UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by the redirect URL we chose to use from Microsoft APIs
        //continue the OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-to-handle-the-result-of-the-oauth2-request"></a><span data-ttu-id="98610-174">Napisz kod obsługujący wynik żądania OAuth2</span><span class="sxs-lookup"><span data-stu-id="98610-174">Write code to handle the result of the OAuth2 request</span></span>
<span data-ttu-id="98610-175">Następujący kod będzie obsługiwać redirectURL, która zwraca widok sieci Web.</span><span class="sxs-lookup"><span data-stu-id="98610-175">The following code will handle the redirectURL that returns from the WebView.</span></span> <span data-ttu-id="98610-176">Jeśli uwierzytelnianie nie powiodło się, kod ponowi próbę.</span><span class="sxs-lookup"><span data-stu-id="98610-176">If authentication wasn't successful, the code will try again.</span></span> <span data-ttu-id="98610-177">W tym samym czasie biblioteki zapewni błędu, który można wyświetlać w konsoli lub obsługi asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="98610-177">Meanwhile, the library will provide the error that you can see in the console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse the response for success or failure
     if (accessResult)
    //if success, complete the OAuth2 flow by handling the redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-the-oauth-context-called-account-store"></a><span data-ttu-id="98610-178">Skonfiguruj kontekst OAuth (nazywane konta magazynu)</span><span class="sxs-lookup"><span data-stu-id="98610-178">Set up the OAuth Context (called account store)</span></span>
<span data-ttu-id="98610-179">W tym miejscu możesz wywołać `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` magazynu udostępnionego konta dla każdej usługi, który ma dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98610-179">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on the shared account store for each service that you want the application to be able to access.</span></span> <span data-ttu-id="98610-180">Typ konta jest ciąg, który jest używany jako identyfikator dla niektórych usługi.</span><span class="sxs-lookup"><span data-stu-id="98610-180">The account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="98610-181">Ponieważ uzyskujesz dostęp do interfejsu API programu Graph, kod odwołuje się do niego jako `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="98610-181">Because you are accessing the Graph API, the code refers to it as `"myGraphService"`.</span></span> <span data-ttu-id="98610-182">Możesz skonfigurować obserwatora, który informuje użytkownika, gdy dowolne zmiany z tokenem.</span><span class="sxs-lookup"><span data-stu-id="98610-182">You then set up an observer that will tell you when anything changes with the token.</span></span> <span data-ttu-id="98610-183">Po uzyskaniu tokenu powrocie użytkownika z powrotem do `masterView`.</span><span class="sxs-lookup"><span data-stu-id="98610-183">After you get the token, you return the user back to the `masterView`.</span></span>

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-the-master-view-to-search-and-display-the-users-from-the-graph-api"></a><span data-ttu-id="98610-184">Ustawianie widoku głównego można wyszukiwać i wyświetlać użytkowników z interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="98610-184">Set up the Master View to search and display the users from the Graph API</span></span>
<span data-ttu-id="98610-185">Aplikacji Master-widok-kontroler (MVC), który wyświetla zwrócone dane w siatce wykracza poza zakres tego przewodnika, a wiele online samouczki wyjaśniają, jak utworzyć.</span><span class="sxs-lookup"><span data-stu-id="98610-185">A Master-View-Controller (MVC) app that displays the returned data in the grid is beyond the scope of this walkthrough, and many online tutorials explain how to build one.</span></span> <span data-ttu-id="98610-186">Ten kod znajduje się w pliku szkielet.</span><span class="sxs-lookup"><span data-stu-id="98610-186">All this code is in the skeleton file.</span></span> <span data-ttu-id="98610-187">Jednak należy uwzględniać kilka czynności w aplikacji MVC:</span><span class="sxs-lookup"><span data-stu-id="98610-187">However, you do need to deal with a few things in this MVC application:</span></span>

* <span data-ttu-id="98610-188">ODCIĘTA, gdy użytkownik wpisze coś w polu wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="98610-188">Intercept when a user types something in the search field</span></span>
* <span data-ttu-id="98610-189">Udostępniają obiektu danych do MasterView, więc można go wyświetlić wyniki w siatce</span><span class="sxs-lookup"><span data-stu-id="98610-189">Provide an object of data back to the MasterView so it can display the results in the grid</span></span>

<span data-ttu-id="98610-190">Robimy tych poniżej.</span><span class="sxs-lookup"><span data-stu-id="98610-190">We'll do those below.</span></span>

### <a name="add-a-check-to-see-if-youre-logged-in"></a><span data-ttu-id="98610-191">Dodaj znacznik wyboru, aby zobaczyć, czy użytkownik jest zalogowany</span><span class="sxs-lookup"><span data-stu-id="98610-191">Add a check to see if you're logged in</span></span>
<span data-ttu-id="98610-192">Aplikacja pojawia się tylko użytkownik nie jest zalogowany, więc sprawne działanie sprawdzić, czy istnieje już token w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="98610-192">The application does little if the user is not signed in, so it's smart to check if there is already a token in the cache.</span></span> <span data-ttu-id="98610-193">Jeśli nie, zostanie przekierowany do LoginView dla użytkownika do logowania.</span><span class="sxs-lookup"><span data-stu-id="98610-193">If not, you redirect to the LoginView for the user to sign in.</span></span> <span data-ttu-id="98610-194">Jeśli odwołanie, jest użycie najlepszym sposobem na wykonywanie czynności po załadowaniu widoku `viewDidLoad()` metoda zapewniająca firmy Apple, NAS.</span><span class="sxs-lookup"><span data-stu-id="98610-194">If you recall, the best way to do actions when a view loads is to use the `viewDidLoad()` method that Apple provides us.</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-the-table-view-when-data-is-received"></a><span data-ttu-id="98610-195">Aktualizowanie widoku tabeli po odebraniu danych</span><span class="sxs-lookup"><span data-stu-id="98610-195">Update the Table View when data is received</span></span>
<span data-ttu-id="98610-196">Po powrocie z interfejsu API programu Graph danych należy do wyświetlania danych.</span><span class="sxs-lookup"><span data-stu-id="98610-196">When the Graph API returns data, you need to display the data.</span></span> <span data-ttu-id="98610-197">Dla uproszczenia w tym miejscu jest cały kod, aby zaktualizować tabeli.</span><span class="sxs-lookup"><span data-stu-id="98610-197">For simplicity, here is all the code to update the table.</span></span> <span data-ttu-id="98610-198">Prawo wartości można wkleić tylko w kodzie umożliwiającego MVC.</span><span class="sxs-lookup"><span data-stu-id="98610-198">You can just paste the right values in your MVC boilerplate code.</span></span>

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure the cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-to-call-the-graph-api-when-someone-types-in-the-search-field"></a><span data-ttu-id="98610-199">Umożliwiają wywołania interfejsu API programu Graph, gdy użytkownik wpisze w polu wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="98610-199">Provide a way to call the Graph API when someone types in the search field</span></span>
<span data-ttu-id="98610-200">Jeśli użytkownik wpisze wyszukiwania w polu, musisz shove który za pośrednictwem do interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="98610-200">When a user types a search in the box, you need to shove that over to the Graph API.</span></span> <span data-ttu-id="98610-201">`GraphAPICaller` Klasy, która będzie kompilowana w poniższym kodzie, oddziela funkcji wyszukiwania z prezentacji.</span><span class="sxs-lookup"><span data-stu-id="98610-201">The `GraphAPICaller` class, which you will build in the following code, separates the lookup functionality from the presentation.</span></span> <span data-ttu-id="98610-202">Na razie Napiszmy kod, który źródła znaków wyszukiwania do interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="98610-202">For now, let's write the code that feeds any search characters to the Graph API.</span></span> <span data-ttu-id="98610-203">Firma Microsoft w tym celu udostępnia metodę o nazwie `lookupInGraph`, który przyjmuje ciąg, który chcesz wyszukać.</span><span class="sxs-lookup"><span data-stu-id="98610-203">We do this by providing a method called `lookupInGraph`, which takes the string that we want to search for.</span></span>

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-to-access-the-graph-api"></a><span data-ttu-id="98610-204">Zapis klasę pomocy umożliwiającą dostęp do interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="98610-204">Write a Helper class to access the Graph API</span></span>
<span data-ttu-id="98610-205">Jest to podstawowy naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98610-205">This is the core of our application.</span></span> <span data-ttu-id="98610-206">Podczas gdy pozostałe został Wstawianie kodu we wzorcu MVC domyślnej od firmy Apple, w tym miejscu pisania kodu zapytania wykresu jako typy użytkowników, a następnie wróć tych danych.</span><span class="sxs-lookup"><span data-stu-id="98610-206">Whereas the rest was inserting code in the default MVC pattern from Apple, here you write code to query the graph as the user types and then return that data.</span></span> <span data-ttu-id="98610-207">Oto kod i następuje szczegółowy opis.</span><span class="sxs-lookup"><span data-stu-id="98610-207">Here's the code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="98610-208">Utwórz nowy plik nagłówka Objective C</span><span class="sxs-lookup"><span data-stu-id="98610-208">Create a new Objective C header file</span></span>
<span data-ttu-id="98610-209">Nadaj nazwę plikowi `GraphAPICaller.h`i Dodaj następujący kod.</span><span class="sxs-lookup"><span data-stu-id="98610-209">Name the file `GraphAPICaller.h`, and add the following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="98610-210">Miejscu zobaczysz, że określona metoda przyjmuje ciągiem i zwraca completionBlock.</span><span class="sxs-lookup"><span data-stu-id="98610-210">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="98610-211">Ta completionBlock jako użytkownik może mieć odgadnąć, spowoduje zaktualizowanie tabeli podając obiektu wypełnione danych w czasie rzeczywistym jako wyszukiwanie użytkowników.</span><span class="sxs-lookup"><span data-stu-id="98610-211">This completionBlock, as you may have guessed, will update the table by providing an object with populated data in real time as the user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="98610-212">Utwórz nowy plik języka Objective C</span><span class="sxs-lookup"><span data-stu-id="98610-212">Create a new Objective C file</span></span>
<span data-ttu-id="98610-213">Nadaj nazwę plikowi `GraphAPICaller.m`i dodaj następującą metodę.</span><span class="sxs-lookup"><span data-stu-id="98610-213">Name the file `GraphAPICaller.m`, and add the following method.</span></span>

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

<span data-ttu-id="98610-214">Przejdźmy za pomocą tej metody szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="98610-214">Let's go through this method in detail.</span></span>

<span data-ttu-id="98610-215">Podstawowe ten kod jest w `NXOAuth2Request`, metodę, która przyjmuje parametry, które zdefiniowano w pliku settings.plist.</span><span class="sxs-lookup"><span data-stu-id="98610-215">The core of this code is in the `NXOAuth2Request`, method which takes the parameters that you've already defined in the settings.plist file.</span></span>

<span data-ttu-id="98610-216">Pierwszym krokiem jest skonstruowanie prawo wywołania interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="98610-216">The first step is to construct the right Graph API call.</span></span> <span data-ttu-id="98610-217">Ponieważ wywoływania `/users`, możesz określić, że przez dołączenie go do zasobu interfejsu API programu Graph wraz z wersją.</span><span class="sxs-lookup"><span data-stu-id="98610-217">Because you are calling `/users`, you specify that by appending it to the Graph API resource along with the version.</span></span> <span data-ttu-id="98610-218">Warto umieścić je w pliku ustawień zewnętrznych, ponieważ te można zmienić w miarę rozwoju środowisko interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="98610-218">It makes sense to put these in an external settings file because these can change as the API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="98610-219">Następnie należy określić parametry, które należy również udostępnić wywołania interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="98610-219">Next, you need to specify parameters that you will also provide to the Graph API call.</span></span> <span data-ttu-id="98610-220">Jest *bardzo ważne* czy należy umieszczać parametrów w punkcie końcowym zasobu, ponieważ która zostaje wyczyszczona dla wszystkich znaków zgodnych-URI w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="98610-220">It is *very important* that you do not put the parameters in the resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="98610-221">Cały kod zapytania należy określić w parametrach.</span><span class="sxs-lookup"><span data-stu-id="98610-221">All query code must be provided in the parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="98610-222">Można zauważyć wymaga `convertParamsToDictionary` metodę, która jeszcze nie zostać jeszcze zapisane.</span><span class="sxs-lookup"><span data-stu-id="98610-222">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="98610-223">Umożliwia to teraz zrobić na końcu pliku:</span><span class="sxs-lookup"><span data-stu-id="98610-223">Let's do so now at the end of the file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="98610-224">Następnie można użyć `NXOAuth2Request` metodę, aby odzyskać dane z interfejsu API w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="98610-224">Next, let's use the `NXOAuth2Request` method to get data back from the API in JSON format.</span></span>

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="98610-225">Na koniec Przyjrzyjmy się jak zwrócić dane do MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="98610-225">Finally, let's look at how you return the data to the MasterViewController.</span></span> <span data-ttu-id="98610-226">Dane zwraca serializowane i musi zostać deserializacji i załadowany w obiekcie, który MainViewController, jaką może wykorzystać.</span><span class="sxs-lookup"><span data-stu-id="98610-226">The data returns as serialized and needs to be deserialized and loaded in an object that the MainViewController can consume.</span></span> <span data-ttu-id="98610-227">W tym celu ma szkielet `User.m/h` pliku, który tworzy obiekt użytkownika.</span><span class="sxs-lookup"><span data-stu-id="98610-227">For this purpose, the skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="98610-228">Należy wypełnić tego obiektu użytkownika o informacje z wykresu.</span><span class="sxs-lookup"><span data-stu-id="98610-228">You populate that User object with information from the graph.</span></span>

```objc
                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-the-sample"></a><span data-ttu-id="98610-229">Uruchom próbki</span><span class="sxs-lookup"><span data-stu-id="98610-229">Run the sample</span></span>
<span data-ttu-id="98610-230">Jeśli został użyty szkielet i stosować wraz z tym przewodnikiem teraz należy uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="98610-230">If you've used the skeleton or followed along with the walkthrough your application should now run.</span></span> <span data-ttu-id="98610-231">Uruchomić symulatora, a następnie kliknij przycisk **Zaloguj** korzystanie z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98610-231">Start the simulator and click **Sign in** to use the application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="98610-232">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="98610-232">Get security updates for our product</span></span>
<span data-ttu-id="98610-233">Firma Microsoft zachęca do przekazywania powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [Witryna TechCenter poświęcona zabezpieczeniom](https://technet.microsoft.com/security/dd252948) i subskrybowanie doradczych alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="98610-233">We encourage you to get notifications of when security incidents occur by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

