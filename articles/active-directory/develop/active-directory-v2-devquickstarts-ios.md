---
title: "aaaAdd tooan logowania dla systemu iOS aplikacji przy użyciu hello punktu końcowego v2.0 usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak toobuild aplikację systemu iOS który loguje się użytkowników z obu osobistego konta Microsoft i kont służbowych przy użyciu bibliotek innych firm."
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
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="58882-103">Dodawanie aplikacji dla systemu iOS tooan logowania przy użyciu biblioteki innych firm z interfejsu API programu Graph przy użyciu punktu końcowego v2.0 hello</span><span class="sxs-lookup"><span data-stu-id="58882-103">Add sign-in tooan iOS app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="58882-104">korzysta z platformą tożsamości Microsoft Hello Otwórz standardy, takie jak OAuth2 i OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="58882-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="58882-105">Deweloperzy mogą używać dowolnej bibliotece mają toointegrate z naszych usług.</span><span class="sxs-lookup"><span data-stu-id="58882-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="58882-106">Deweloperzy toohelp używać platformy z innych bibliotek, możemy napisanych kilka wskazówki, takich jak ta toodemonstrate jeden sposób platformą tożsamości Microsoft tooconnect toohello tooconfigure bibliotek innych firm.</span><span class="sxs-lookup"><span data-stu-id="58882-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="58882-107">Większość bibliotek, które implementują [specyfikację RFC6749 OAuth2 hello](https://tools.ietf.org/html/rfc6749) mogą łączyć się z platformą tożsamości Microsoft toohello.</span><span class="sxs-lookup"><span data-stu-id="58882-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="58882-108">Aplikacja hello, która tworzy tego przewodnika użytkownicy mogą zarejestrować się w organizacji tootheir i następnie wyszukiwania dla innych użytkowników w organizacji przy użyciu hello interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="58882-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for others in their organization by using hello Graph API.</span></span>

<span data-ttu-id="58882-109">Jeśli nowy tooOAuth2 lub OpenID Connect znacznie to przykładowa konfiguracja może nie mieć tooyou znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="58882-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="58882-110">Zalecamy przeczytanie [protokołów v2.0 - przepływu kodu autoryzacji OAuth 2.0](active-directory-v2-protocols-oauth-code.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="58882-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="58882-111">Funkcje platformy, które mają wyrażenia w hello OAuth2 lub standardy OpenID Connect, takie jak dostęp warunkowy i zarządzanie zasadami usługi Intune, wymagają możesz toouse naszych Otwórz źródło bibliotek tożsamości usługi Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="58882-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="58882-112">punktu końcowego v2.0 Hello nie obsługuje wszystkich scenariuszy Azure Active Directory i funkcji.</span><span class="sxs-lookup"><span data-stu-id="58882-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="58882-113">toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="58882-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="58882-114">Pobierz kod z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="58882-114">Download code from GitHub</span></span>
<span data-ttu-id="58882-115">Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="58882-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="58882-116">toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) lub klonowania hello szkielet:</span><span class="sxs-lookup"><span data-stu-id="58882-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="58882-117">Możesz także po prostu pobrać przykładowy hello i od razu rozpocząć:</span><span class="sxs-lookup"><span data-stu-id="58882-117">You can also just download hello sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="58882-118">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="58882-118">Register an app</span></span>
<span data-ttu-id="58882-119">Utwórz nową aplikację na powitania [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj hello szczegółowe kroki opisane w temacie [jak tooregister aplikacji z punktem końcowym v2.0 hello](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="58882-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at  [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="58882-120">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="58882-120">Make sure to:</span></span>

* <span data-ttu-id="58882-121">Kopiuj hello **identyfikator aplikacji** wynika to z przypisaną tooyour aplikacji należy ją szybko.</span><span class="sxs-lookup"><span data-stu-id="58882-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="58882-122">Dodaj hello **Mobile** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="58882-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="58882-123">Kopiuj hello **identyfikator URI przekierowania** hello portalu.</span><span class="sxs-lookup"><span data-stu-id="58882-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="58882-124">Należy użyć wartości domyślnej hello `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="58882-124">You must use hello default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="58882-125">Pobierz hello innych firm NXOAuth2 biblioteki i tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="58882-125">Download hello third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="58882-126">W ramach tego przewodnika skorzystasz hello OAuth2Client z serwisu GitHub, czyli OAuth2 biblioteki dla systemu Mac OS X i iOS (Cocoa i Cocoa touch).</span><span class="sxs-lookup"><span data-stu-id="58882-126">For this walkthrough, you will use hello OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="58882-127">Ta biblioteka jest oparta na projekt 10 hello specyfikację OAuth2. Ona profilu natywnych aplikacji hello implementuje i obsługuje hello punktu końcowego autoryzacji użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="58882-127">This library is based on draft 10 of hello OAuth2 spec. It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="58882-128">Są to wszystko, co hello należy toointegrate z platformą tożsamości Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="58882-128">These are all hello things you'll need toointegrate with hello Microsoft identity platform.</span></span>

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a><span data-ttu-id="58882-129">Dodaj projekt tooyour biblioteki hello przy użyciu programu CocoaPods</span><span class="sxs-lookup"><span data-stu-id="58882-129">Add hello library tooyour project by using CocoaPods</span></span>
<span data-ttu-id="58882-130">CocoaPods to menedżer zależności dla projektów Xcode.</span><span class="sxs-lookup"><span data-stu-id="58882-130">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="58882-131">Poprzednie kroki instalacji hello zarządza automatycznie.</span><span class="sxs-lookup"><span data-stu-id="58882-131">It manages hello previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="58882-132">Dodaj następujące toothis podfile hello:</span><span class="sxs-lookup"><span data-stu-id="58882-132">Add hello following toothis podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="58882-133">Podfile hello obciążenia przy użyciu programu CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="58882-133">Load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="58882-134">Spowoduje to utworzenie nowego obszaru roboczego Xcode, który zostanie załadowany.</span><span class="sxs-lookup"><span data-stu-id="58882-134">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a><span data-ttu-id="58882-135">Eksploruj hello strukturę hello projektu</span><span class="sxs-lookup"><span data-stu-id="58882-135">Explore hello structure of hello project</span></span>
<span data-ttu-id="58882-136">następujące struktury Hello jest skonfigurowane dla naszych projektu w szkielet hello:</span><span class="sxs-lookup"><span data-stu-id="58882-136">hello following structure is set up for our project in hello skeleton:</span></span>

* <span data-ttu-id="58882-137">Widok wzorca wyszukiwania nazwy UPN</span><span class="sxs-lookup"><span data-stu-id="58882-137">A Master View with a UPN Search</span></span>
* <span data-ttu-id="58882-138">Widok szczegółów hello danych o hello wybranego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="58882-138">A Detail View for hello data about hello selected user</span></span>
* <span data-ttu-id="58882-139">Gdy użytkownik może zalogować się toohello aplikacji tooquery hello wykresu widoku logowania</span><span class="sxs-lookup"><span data-stu-id="58882-139">A Login View where a user can sign in toohello app tooquery hello graph</span></span>

<span data-ttu-id="58882-140">Firma Microsoft będzie Przenieś pliki toovarious hello szkielet tooadd uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="58882-140">We will move toovarious files in hello skeleton tooadd authentication.</span></span> <span data-ttu-id="58882-141">Inne części kodu hello, na przykład kodu visual hello, nie odnoszą się tooidentity, ale są udostępniane dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="58882-141">Other parts of hello code, such as hello visual code, do not pertain tooidentity but are provided for you.</span></span>

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a><span data-ttu-id="58882-142">Konfigurowanie hello settings.plst pliku w bibliotece hello</span><span class="sxs-lookup"><span data-stu-id="58882-142">Set up hello settings.plst file in hello library</span></span>
* <span data-ttu-id="58882-143">W projekcie szybkiego startu hello Otwórz hello `settings.plist` pliku.</span><span class="sxs-lookup"><span data-stu-id="58882-143">In hello QuickStart project, open hello `settings.plist` file.</span></span> <span data-ttu-id="58882-144">Zastąp wartości hello elementów hello hello sekcji tooreflect hello wartości, używane w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="58882-144">Replace hello values of hello elements in hello section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="58882-145">Kod będzie odwoływać tych wartości, przy każdym użyciu hello biblioteki uwierzytelniania usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="58882-145">Your code will reference these values whenever it uses hello Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="58882-146">Witaj `clientId` jest hello identyfikator klienta aplikacji, który został skopiowany z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="58882-146">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="58882-147">Witaj `redirectUri` jest adres URL przekierowania hello tego portalu hello podane.</span><span class="sxs-lookup"><span data-stu-id="58882-147">hello `redirectUri` is hello redirect URL that hello portal provided.</span></span>

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="58882-148">Konfigurowanie biblioteki NXOAuth2Client hello w Twojej LoginViewController</span><span class="sxs-lookup"><span data-stu-id="58882-148">Set up hello NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="58882-149">Biblioteka NXOAuth2Client Hello wymaga niektórych tooget wartości ustawienia.</span><span class="sxs-lookup"><span data-stu-id="58882-149">hello NXOAuth2Client library requires some values tooget set up.</span></span> <span data-ttu-id="58882-150">Po wykonaniu tego zadania można użyć hello nabytych przez niego tokenu toocall hello interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="58882-150">After you complete that task, you can use hello acquired token toocall hello Graph API.</span></span> <span data-ttu-id="58882-151">Ponieważ `LoginView` zostanie wywołana w dowolnym momencie potrzebujemy tooauthenticate, warto tooput wartości konfiguracji w pliku toothat.</span><span class="sxs-lookup"><span data-stu-id="58882-151">Because `LoginView` will be called any time we need tooauthenticate, it makes sense tooput configuration values in toothat file.</span></span>

* <span data-ttu-id="58882-152">Dodajmy toohello niektóre wartości `LoginViewController.m` pliku tooset hello kontekst uwierzytelniania i autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="58882-152">Let's add some values toohello  `LoginViewController.m` file tooset hello context for authentication and authorization.</span></span> <span data-ttu-id="58882-153">Szczegółowe informacje o wartości hello wykonaj hello kodu.</span><span class="sxs-lookup"><span data-stu-id="58882-153">Details about hello values follow hello code.</span></span>
  
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

<span data-ttu-id="58882-154">Oto szczegóły dotyczące hello kodu.</span><span class="sxs-lookup"><span data-stu-id="58882-154">Let's look at details about hello code.</span></span>

<span data-ttu-id="58882-155">pierwszy ciąg Hello jest przeznaczony dla `scopes`.</span><span class="sxs-lookup"><span data-stu-id="58882-155">hello first string is for `scopes`.</span></span>  <span data-ttu-id="58882-156">Witaj `User.Read` wartość umożliwia tooread hello podstawowy profil hello zalogowany użytkownik.</span><span class="sxs-lookup"><span data-stu-id="58882-156">hello `User.Read` value allows you tooread hello basic profile of hello signed in user.</span></span>

<span data-ttu-id="58882-157">Dowiedz się więcej o wszystkie dostępne zakresy hello na [zakresy uprawnień Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="58882-157">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="58882-158">Aby uzyskać `authURL`, `loginURL`, `bhh`, i `tokenURL`, należy użyć wartości hello podane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="58882-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use hello values provided previously.</span></span> <span data-ttu-id="58882-159">Użycie typu open source hello bibliotek tożsamości usługi Microsoft Azure, możemy rozwiń tych danych można za pomocą naszych punktu końcowego metadanych.</span><span class="sxs-lookup"><span data-stu-id="58882-159">If you use hello open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="58882-160">Firma Microsoft wykonane hello Praca wyodrębniania te wartości dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="58882-160">We've done hello hard work of extracting these values for you.</span></span>

<span data-ttu-id="58882-161">Witaj `keychain` wartość jest hello kontenera, w którym hello NXOAuth2Client biblioteki użyje toocreate toostore łańcucha kluczy tokenów.</span><span class="sxs-lookup"><span data-stu-id="58882-161">hello `keychain` value is hello container that hello NXOAuth2Client library will use toocreate a keychain toostore your tokens.</span></span> <span data-ttu-id="58882-162">Jeśli chcesz tooget rejestracji jednokrotnej (SSO) w wielu aplikacjach, można określić hello tego samego łańcucha kluczy w każdej aplikacji i żądania hello stosowania tego łańcucha kluczy w Twoje uprawnienia Xcode.</span><span class="sxs-lookup"><span data-stu-id="58882-162">If you'd like tooget single sign-on (SSO) across numerous apps, you can specify hello same keychain in each of your applications and request hello use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="58882-163">Wyjaśnienie jest zawarte w hello dokumentacji firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="58882-163">This is explained in hello Apple documentation.</span></span>

<span data-ttu-id="58882-164">Hello reszty te wartości są wymagane toouse hello biblioteki i utworzenie miejsc do toocarry wartości toohello kontekstu.</span><span class="sxs-lookup"><span data-stu-id="58882-164">hello rest of these values are required toouse hello library and create places for you toocarry values toohello context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="58882-165">Tworzenie pamięci podręcznej adres URL</span><span class="sxs-lookup"><span data-stu-id="58882-165">Create a URL cache</span></span>
<span data-ttu-id="58882-166">Wewnątrz `(void)viewDidLoad()`, który zawsze jest wywoływana po załadowaniu widoku hello, hello następujący kod primes pamięci podręcznej naszych do użytku.</span><span class="sxs-lookup"><span data-stu-id="58882-166">Inside `(void)viewDidLoad()`, which is always called after hello view is loaded, hello following code primes a cache for our use.</span></span>

<span data-ttu-id="58882-167">Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="58882-167">Add hello following code:</span></span>

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

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="58882-168">Tworzenie widoku sieci Web dla logowania</span><span class="sxs-lookup"><span data-stu-id="58882-168">Create a WebView for sign-in</span></span>
<span data-ttu-id="58882-169">Widok sieci Web można Monituj użytkownika o hello na dodatkowych czynników, takich jak wiadomość SMS (jeśli jest skonfigurowane) lub zwraca błąd wiadomości toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="58882-169">A WebView can prompt hello user for additional factors like SMS text message (if configured) or return error messages toohello user.</span></span> <span data-ttu-id="58882-170">W tym miejscu należy skonfigurować hello widoku sieci Web, a następnie kontynuować hello zapisu kodu toohandle hello zwrotne, które nastąpi w hello widoku sieci Web z hello tożsamości usługi.</span><span class="sxs-lookup"><span data-stu-id="58882-170">Here you'll set up hello WebView and then later write hello code toohandle hello callbacks that will happen in hello WebView from hello identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a><span data-ttu-id="58882-171">Zastąpienie hello WebView metody toohandle uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="58882-171">Override hello WebView methods toohandle authentication</span></span>
<span data-ttu-id="58882-172">Witaj tootell widoku sieci Web, co się dzieje, gdy użytkownik będzie potrzebował toosign w jak wspomniano wcześniej, można wkleić hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="58882-172">tootell hello WebView what happens when a user needs toosign in as discussed previously, you can paste hello following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

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

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a><span data-ttu-id="58882-173">Pisanie kodu toohandle hello wynik hello OAuth2 żądania</span><span class="sxs-lookup"><span data-stu-id="58882-173">Write code toohandle hello result of hello OAuth2 request</span></span>
<span data-ttu-id="58882-174">Witaj następujący kod będzie obsługiwać redirectURL hello, które zwraca hello widoku sieci Web.</span><span class="sxs-lookup"><span data-stu-id="58882-174">hello following code will handle hello redirectURL that returns from hello WebView.</span></span> <span data-ttu-id="58882-175">Jeśli uwierzytelnianie nie powiodło się, kod hello ponowi próbę.</span><span class="sxs-lookup"><span data-stu-id="58882-175">If authentication wasn't successful, hello code will try again.</span></span> <span data-ttu-id="58882-176">W tym samym czasie biblioteki hello zapewni hello błędu, który można wyświetlić w konsoli hello lub obsługi asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="58882-176">Meanwhile, hello library will provide hello error that you can see in hello console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a><span data-ttu-id="58882-177">Konfigurowanie hello kontekstu OAuth (nazywane konta magazynu)</span><span class="sxs-lookup"><span data-stu-id="58882-177">Set up hello OAuth Context (called account store)</span></span>
<span data-ttu-id="58882-178">W tym miejscu możesz wywołać `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` hello udostępnionego konta magazynu dla każdej usługi, które mają tooaccess stanie toobe aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="58882-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on hello shared account store for each service that you want hello application toobe able tooaccess.</span></span> <span data-ttu-id="58882-179">Typ konta Hello jest ciągiem, który służy jako identyfikator dla niektórych usług.</span><span class="sxs-lookup"><span data-stu-id="58882-179">hello account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="58882-180">Ponieważ uzyskujesz dostęp do interfejsu API programu Graph hello hello kod odnosi się tooit jako `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="58882-180">Because you are accessing hello Graph API, hello code refers tooit as `"myGraphService"`.</span></span> <span data-ttu-id="58882-181">Możesz skonfigurować obserwatora, który informuje użytkownika, gdy dowolne zmiany z tokenem hello.</span><span class="sxs-lookup"><span data-stu-id="58882-181">You then set up an observer that will tell you when anything changes with hello token.</span></span> <span data-ttu-id="58882-182">Po uzyskaniu tokenu hello powrócić hello użytkownika wstecz toohello `masterView`.</span><span class="sxs-lookup"><span data-stu-id="58882-182">After you get hello token, you return hello user back toohello `masterView`.</span></span>

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

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a><span data-ttu-id="58882-183">Określanie hello toosearch widok wzorca i wyświetlanie użytkownikom hello hello interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="58882-183">Set up hello Master View toosearch and display hello users from hello Graph API</span></span>
<span data-ttu-id="58882-184">Aplikacji Master-widok-kontroler (MVC), który wyświetla hello zwróciła dane w siatce hello wykracza poza zakres tego przewodnika hello i wiele online samouczki wyjaśniają sposób toobuild jeden.</span><span class="sxs-lookup"><span data-stu-id="58882-184">A Master-View-Controller (MVC) app that displays hello returned data in hello grid is beyond hello scope of this walkthrough, and many online tutorials explain how toobuild one.</span></span> <span data-ttu-id="58882-185">Ten kod jest w pliku szkielet hello.</span><span class="sxs-lookup"><span data-stu-id="58882-185">All this code is in hello skeleton file.</span></span> <span data-ttu-id="58882-186">Należy jednak toodeal z kilku czynności w aplikacji MVC:</span><span class="sxs-lookup"><span data-stu-id="58882-186">However, you do need toodeal with a few things in this MVC application:</span></span>

* <span data-ttu-id="58882-187">ODCIĘTA, gdy użytkownik wpisze coś w polu wyszukiwania hello</span><span class="sxs-lookup"><span data-stu-id="58882-187">Intercept when a user types something in hello search field</span></span>
* <span data-ttu-id="58882-188">Udostępniać obiekt danych wstecz toohello MasterView, co umożliwia wyświetlanie wyników hello w siatce hello</span><span class="sxs-lookup"><span data-stu-id="58882-188">Provide an object of data back toohello MasterView so it can display hello results in hello grid</span></span>

<span data-ttu-id="58882-189">Robimy tych poniżej.</span><span class="sxs-lookup"><span data-stu-id="58882-189">We'll do those below.</span></span>

### <a name="add-a-check-toosee-if-youre-logged-in"></a><span data-ttu-id="58882-190">Dodaj toosee wyboru, jeśli jest zalogowany</span><span class="sxs-lookup"><span data-stu-id="58882-190">Add a check toosee if you're logged in</span></span>
<span data-ttu-id="58882-191">Aplikacja Hello pojawia się tylko hello użytkownik nie jest zalogowany, jeśli istnieje już token w pamięci podręcznej hello jest toocheck inteligentne.</span><span class="sxs-lookup"><span data-stu-id="58882-191">hello application does little if hello user is not signed in, so it's smart toocheck if there is already a token in hello cache.</span></span> <span data-ttu-id="58882-192">Jeśli nie, nastąpi przekierowanie toohello LoginView dla toosign użytkownika hello w.</span><span class="sxs-lookup"><span data-stu-id="58882-192">If not, you redirect toohello LoginView for hello user toosign in.</span></span> <span data-ttu-id="58882-193">Jeśli możesz odwołać hello najlepsze sposób toodo akcje po załadowaniu widoku jest toouse hello `viewDidLoad()` metoda zapewniająca firmy Apple, NAS.</span><span class="sxs-lookup"><span data-stu-id="58882-193">If you recall, hello best way toodo actions when a view loads is toouse hello `viewDidLoad()` method that Apple provides us.</span></span>

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

### <a name="update-hello-table-view-when-data-is-received"></a><span data-ttu-id="58882-194">Aktualizacja hello widoku tabeli po odebraniu danych</span><span class="sxs-lookup"><span data-stu-id="58882-194">Update hello Table View when data is received</span></span>
<span data-ttu-id="58882-195">Gdy hello interfejsu API programu Graph zwraca dane, należy toodisplay hello danych.</span><span class="sxs-lookup"><span data-stu-id="58882-195">When hello Graph API returns data, you need toodisplay hello data.</span></span> <span data-ttu-id="58882-196">Dla uproszczenia Oto wszystkich hello kodu tooupdate hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="58882-196">For simplicity, here is all hello code tooupdate hello table.</span></span> <span data-ttu-id="58882-197">W kodzie umożliwiającego MVC można wkleić tylko hello właściwych wartości.</span><span class="sxs-lookup"><span data-stu-id="58882-197">You can just paste hello right values in your MVC boilerplate code.</span></span>

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


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a><span data-ttu-id="58882-198">Podaj hello toocall sposób interfejsu API programu Graph, gdy użytkownik wpisze w polu wyszukiwania hello</span><span class="sxs-lookup"><span data-stu-id="58882-198">Provide a way toocall hello Graph API when someone types in hello search field</span></span>
<span data-ttu-id="58882-199">Gdy użytkownik wpisze wyszukiwania w polu hello, należy tooshove który za pośrednictwem toohello interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="58882-199">When a user types a search in hello box, you need tooshove that over toohello Graph API.</span></span> <span data-ttu-id="58882-200">Witaj `GraphAPICaller` klasy, która będzie kompilowana w hello następującego kodu, oddziela funkcji wyszukiwania hello hello prezentacji.</span><span class="sxs-lookup"><span data-stu-id="58882-200">hello `GraphAPICaller` class, which you will build in hello following code, separates hello lookup functionality from hello presentation.</span></span> <span data-ttu-id="58882-201">Na razie Napiszmy kod hello źródła żadnych wyszukiwania znaków toohello interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="58882-201">For now, let's write hello code that feeds any search characters toohello Graph API.</span></span> <span data-ttu-id="58882-202">Firma Microsoft w tym celu udostępnia metodę o nazwie `lookupInGraph`, który przyjmuje ciąg hello chcemy toosearch dla.</span><span class="sxs-lookup"><span data-stu-id="58882-202">We do this by providing a method called `lookupInGraph`, which takes hello string that we want toosearch for.</span></span>

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

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a><span data-ttu-id="58882-203">Zapis pomocnika hello tooaccess klasy interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="58882-203">Write a Helper class tooaccess hello Graph API</span></span>
<span data-ttu-id="58882-204">Jest to core hello naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="58882-204">This is hello core of our application.</span></span> <span data-ttu-id="58882-205">Natomiast hello rest został Wstawianie kodu we wzorcu MVC domyślnego powitania od firmy Apple, w tym miejscu pisania kodu tooquery hello wykresu jako użytkownika hello typów, a następnie zwrócić te dane.</span><span class="sxs-lookup"><span data-stu-id="58882-205">Whereas hello rest was inserting code in hello default MVC pattern from Apple, here you write code tooquery hello graph as hello user types and then return that data.</span></span> <span data-ttu-id="58882-206">Oto kod hello i następuje szczegółowy opis.</span><span class="sxs-lookup"><span data-stu-id="58882-206">Here's hello code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="58882-207">Utwórz nowy plik nagłówka Objective C</span><span class="sxs-lookup"><span data-stu-id="58882-207">Create a new Objective C header file</span></span>
<span data-ttu-id="58882-208">Nazwa pliku hello `GraphAPICaller.h`i Dodaj hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="58882-208">Name hello file `GraphAPICaller.h`, and add hello following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="58882-209">Miejscu zobaczysz, że określona metoda przyjmuje ciągiem i zwraca completionBlock.</span><span class="sxs-lookup"><span data-stu-id="58882-209">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="58882-210">Ta completionBlock jako użytkownik może mieć odgadnąć, spowoduje zaktualizowanie tabeli hello podając obiektu wypełnione danych w czasie rzeczywistym jako hello wyszukiwanie użytkowników.</span><span class="sxs-lookup"><span data-stu-id="58882-210">This completionBlock, as you may have guessed, will update hello table by providing an object with populated data in real time as hello user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="58882-211">Utwórz nowy plik języka Objective C</span><span class="sxs-lookup"><span data-stu-id="58882-211">Create a new Objective C file</span></span>
<span data-ttu-id="58882-212">Nazwa pliku hello `GraphAPICaller.m`i dodaj następujące metody hello.</span><span class="sxs-lookup"><span data-stu-id="58882-212">Name hello file `GraphAPICaller.m`, and add hello following method.</span></span>

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
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
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

<span data-ttu-id="58882-213">Przejdźmy za pomocą tej metody szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="58882-213">Let's go through this method in detail.</span></span>

<span data-ttu-id="58882-214">podstawowe Hello tego kodu jest hello `NXOAuth2Request`, metodę, która przyjmuje parametry hello, który zdefiniowano w pliku settings.plist hello.</span><span class="sxs-lookup"><span data-stu-id="58882-214">hello core of this code is in hello `NXOAuth2Request`, method which takes hello parameters that you've already defined in hello settings.plist file.</span></span>

<span data-ttu-id="58882-215">Witaj pierwszym krokiem jest tooconstruct hello prawo wywołania interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="58882-215">hello first step is tooconstruct hello right Graph API call.</span></span> <span data-ttu-id="58882-216">Ponieważ wywoływania `/users`, możesz określić, że dołączając zasobu interfejsu API programu Graph toohello wraz z hello wersji.</span><span class="sxs-lookup"><span data-stu-id="58882-216">Because you are calling `/users`, you specify that by appending it toohello Graph API resource along with hello version.</span></span> <span data-ttu-id="58882-217">Dobrym tooput znaczeniu je w pliku ustawień zewnętrznych, ponieważ te można zmienić w miarę rozwoju środowisko hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="58882-217">It makes sense tooput these in an external settings file because these can change as hello API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="58882-218">Następnie należy parametry toospecify będzie również zawierał toohello wywołania interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="58882-218">Next, you need toospecify parameters that you will also provide toohello Graph API call.</span></span> <span data-ttu-id="58882-219">Jest *bardzo ważne* nie umieszczenie parametrów hello w punkcie końcowym zasobów hello ponieważ która zostaje wyczyszczona dla wszystkich znaków zgodnych-URI w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="58882-219">It is *very important* that you do not put hello parameters in hello resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="58882-220">W parametrach hello należy podać wszystkie kod zapytania.</span><span class="sxs-lookup"><span data-stu-id="58882-220">All query code must be provided in hello parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="58882-221">Można zauważyć wymaga `convertParamsToDictionary` metodę, która jeszcze nie zostać jeszcze zapisane.</span><span class="sxs-lookup"><span data-stu-id="58882-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="58882-222">Umożliwia to teraz zrobić na końcu pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="58882-222">Let's do so now at hello end of hello file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="58882-223">Następnie można użyć hello `NXOAuth2Request` metody tooget dane z powrotem z hello interfejsu API w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="58882-223">Next, let's use hello `NXOAuth2Request` method tooget data back from hello API in JSON format.</span></span>

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
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="58882-224">Na koniec Przyjrzyjmy się jak zwrócić hello danych toohello MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="58882-224">Finally, let's look at how you return hello data toohello MasterViewController.</span></span> <span data-ttu-id="58882-225">dane Hello zwraca serializowane i musi toobe deserializacji i załadowany w obiekcie tego hello MainViewController, jaką może wykorzystać.</span><span class="sxs-lookup"><span data-stu-id="58882-225">hello data returns as serialized and needs toobe deserialized and loaded in an object that hello MainViewController can consume.</span></span> <span data-ttu-id="58882-226">W tym celu ma szkielet hello `User.m/h` pliku, który tworzy obiekt użytkownika.</span><span class="sxs-lookup"><span data-stu-id="58882-226">For this purpose, hello skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="58882-227">Należy wypełnić tego obiektu użytkownika o informacje z hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="58882-227">You populate that User object with information from hello graph.</span></span>

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
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


## <a name="run-hello-sample"></a><span data-ttu-id="58882-228">Uruchom hello próbki</span><span class="sxs-lookup"><span data-stu-id="58882-228">Run hello sample</span></span>
<span data-ttu-id="58882-229">Jeśli już używana szkielet hello lub po oraz wskazówki hello teraz należy uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="58882-229">If you've used hello skeleton or followed along with hello walkthrough your application should now run.</span></span> <span data-ttu-id="58882-230">Uruchom hello symulator i kliknij przycisk **Zaloguj** toouse hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="58882-230">Start hello simulator and click **Sign in** toouse hello application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="58882-231">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="58882-231">Get security updates for our product</span></span>
<span data-ttu-id="58882-232">Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez odwiedzenie hello [Witryna TechCenter poświęcona zabezpieczeniom](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.</span><span class="sxs-lookup"><span data-stu-id="58882-232">We encourage you tooget notifications of when security incidents occur by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

