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
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Dodawanie aplikacji dla systemu iOS tooan logowania przy użyciu biblioteki innych firm z interfejsu API programu Graph przy użyciu punktu końcowego v2.0 hello
korzysta z platformą tożsamości Microsoft Hello Otwórz standardy, takie jak OAuth2 i OpenID Connect. Deweloperzy mogą używać dowolnej bibliotece mają toointegrate z naszych usług. Deweloperzy toohelp używać platformy z innych bibliotek, możemy napisanych kilka wskazówki, takich jak ta toodemonstrate jeden sposób platformą tożsamości Microsoft tooconnect toohello tooconfigure bibliotek innych firm. Większość bibliotek, które implementują [specyfikację RFC6749 OAuth2 hello](https://tools.ietf.org/html/rfc6749) mogą łączyć się z platformą tożsamości Microsoft toohello.

Aplikacja hello, która tworzy tego przewodnika użytkownicy mogą zarejestrować się w organizacji tootheir i następnie wyszukiwania dla innych użytkowników w organizacji przy użyciu hello interfejsu API programu Graph.

Jeśli nowy tooOAuth2 lub OpenID Connect znacznie to przykładowa konfiguracja może nie mieć tooyou znaczeniu. Zalecamy przeczytanie [protokołów v2.0 - przepływu kodu autoryzacji OAuth 2.0](active-directory-v2-protocols-oauth-code.md) w tle.

> [!NOTE]
> Funkcje platformy, które mają wyrażenia w hello OAuth2 lub standardy OpenID Connect, takie jak dostęp warunkowy i zarządzanie zasadami usługi Intune, wymagają możesz toouse naszych Otwórz źródło bibliotek tożsamości usługi Microsoft Azure.
> 
> 

punktu końcowego v2.0 Hello nie obsługuje wszystkich scenariuszy Azure Active Directory i funkcji.

> [!NOTE]
> toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-code-from-github"></a>Pobierz kod z usługi GitHub
Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).  toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) lub klonowania hello szkielet:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

Możesz także po prostu pobrać przykładowy hello i od razu rozpocząć:

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a>Rejestracja aplikacji
Utwórz nową aplikację na powitania [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj hello szczegółowe kroki opisane w temacie [jak tooregister aplikacji z punktem końcowym v2.0 hello](active-directory-v2-app-registration.md).  Upewnij się, że:

* Kopiuj hello **identyfikator aplikacji** wynika to z przypisaną tooyour aplikacji należy ją szybko.
* Dodaj hello **Mobile** platformy aplikacji.
* Kopiuj hello **identyfikator URI przekierowania** hello portalu. Należy użyć wartości domyślnej hello `urn:ietf:wg:oauth:2.0:oob`.

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a>Pobierz hello innych firm NXOAuth2 biblioteki i tworzenie obszaru roboczego
W ramach tego przewodnika skorzystasz hello OAuth2Client z serwisu GitHub, czyli OAuth2 biblioteki dla systemu Mac OS X i iOS (Cocoa i Cocoa touch). Ta biblioteka jest oparta na projekt 10 hello specyfikację OAuth2. Ona profilu natywnych aplikacji hello implementuje i obsługuje hello punktu końcowego autoryzacji użytkownika hello. Są to wszystko, co hello należy toointegrate z platformą tożsamości Microsoft hello.

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a>Dodaj projekt tooyour biblioteki hello przy użyciu programu CocoaPods
CocoaPods to menedżer zależności dla projektów Xcode. Poprzednie kroki instalacji hello zarządza automatycznie.

```
$ vi Podfile
```
1. Dodaj następujące toothis podfile hello:
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. Podfile hello obciążenia przy użyciu programu CocoaPods. Spowoduje to utworzenie nowego obszaru roboczego Xcode, który zostanie załadowany.
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a>Eksploruj hello strukturę hello projektu
następujące struktury Hello jest skonfigurowane dla naszych projektu w szkielet hello:

* Widok wzorca wyszukiwania nazwy UPN
* Widok szczegółów hello danych o hello wybranego użytkownika.
* Gdy użytkownik może zalogować się toohello aplikacji tooquery hello wykresu widoku logowania

Firma Microsoft będzie Przenieś pliki toovarious hello szkielet tooadd uwierzytelnienia. Inne części kodu hello, na przykład kodu visual hello, nie odnoszą się tooidentity, ale są udostępniane dla Ciebie.

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a>Konfigurowanie hello settings.plst pliku w bibliotece hello
* W projekcie szybkiego startu hello Otwórz hello `settings.plist` pliku. Zastąp wartości hello elementów hello hello sekcji tooreflect hello wartości, używane w hello portalu Azure. Kod będzie odwoływać tych wartości, przy każdym użyciu hello biblioteki uwierzytelniania usługi Active Directory.
  * Witaj `clientId` jest hello identyfikator klienta aplikacji, który został skopiowany z portalu hello.
  * Witaj `redirectUri` jest adres URL przekierowania hello tego portalu hello podane.

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a>Konfigurowanie biblioteki NXOAuth2Client hello w Twojej LoginViewController
Biblioteka NXOAuth2Client Hello wymaga niektórych tooget wartości ustawienia. Po wykonaniu tego zadania można użyć hello nabytych przez niego tokenu toocall hello interfejsu API programu Graph. Ponieważ `LoginView` zostanie wywołana w dowolnym momencie potrzebujemy tooauthenticate, warto tooput wartości konfiguracji w pliku toothat.

* Dodajmy toohello niektóre wartości `LoginViewController.m` pliku tooset hello kontekst uwierzytelniania i autoryzacji. Szczegółowe informacje o wartości hello wykonaj hello kodu.
  
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

Oto szczegóły dotyczące hello kodu.

pierwszy ciąg Hello jest przeznaczony dla `scopes`.  Witaj `User.Read` wartość umożliwia tooread hello podstawowy profil hello zalogowany użytkownik.

Dowiedz się więcej o wszystkie dostępne zakresy hello na [zakresy uprawnień Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Aby uzyskać `authURL`, `loginURL`, `bhh`, i `tokenURL`, należy użyć wartości hello podane wcześniej. Użycie typu open source hello bibliotek tożsamości usługi Microsoft Azure, możemy rozwiń tych danych można za pomocą naszych punktu końcowego metadanych. Firma Microsoft wykonane hello Praca wyodrębniania te wartości dla Ciebie.

Witaj `keychain` wartość jest hello kontenera, w którym hello NXOAuth2Client biblioteki użyje toocreate toostore łańcucha kluczy tokenów. Jeśli chcesz tooget rejestracji jednokrotnej (SSO) w wielu aplikacjach, można określić hello tego samego łańcucha kluczy w każdej aplikacji i żądania hello stosowania tego łańcucha kluczy w Twoje uprawnienia Xcode. Wyjaśnienie jest zawarte w hello dokumentacji firmy Apple.

Hello reszty te wartości są wymagane toouse hello biblioteki i utworzenie miejsc do toocarry wartości toohello kontekstu.

### <a name="create-a-url-cache"></a>Tworzenie pamięci podręcznej adres URL
Wewnątrz `(void)viewDidLoad()`, który zawsze jest wywoływana po załadowaniu widoku hello, hello następujący kod primes pamięci podręcznej naszych do użytku.

Dodaj hello następującego kodu:

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

### <a name="create-a-webview-for-sign-in"></a>Tworzenie widoku sieci Web dla logowania
Widok sieci Web można Monituj użytkownika o hello na dodatkowych czynników, takich jak wiadomość SMS (jeśli jest skonfigurowane) lub zwraca błąd wiadomości toohello użytkownika. W tym miejscu należy skonfigurować hello widoku sieci Web, a następnie kontynuować hello zapisu kodu toohandle hello zwrotne, które nastąpi w hello widoku sieci Web z hello tożsamości usługi.

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

### <a name="override-hello-webview-methods-toohandle-authentication"></a>Zastąpienie hello WebView metody toohandle uwierzytelniania
Witaj tootell widoku sieci Web, co się dzieje, gdy użytkownik będzie potrzebował toosign w jak wspomniano wcześniej, można wkleić hello następującego kodu.

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

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a>Pisanie kodu toohandle hello wynik hello OAuth2 żądania
Witaj następujący kod będzie obsługiwać redirectURL hello, które zwraca hello widoku sieci Web. Jeśli uwierzytelnianie nie powiodło się, kod hello ponowi próbę. W tym samym czasie biblioteki hello zapewni hello błędu, który można wyświetlić w konsoli hello lub obsługi asynchronicznie.

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

### <a name="set-up-hello-oauth-context-called-account-store"></a>Konfigurowanie hello kontekstu OAuth (nazywane konta magazynu)
W tym miejscu możesz wywołać `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` hello udostępnionego konta magazynu dla każdej usługi, które mają tooaccess stanie toobe aplikacji hello. Typ konta Hello jest ciągiem, który służy jako identyfikator dla niektórych usług. Ponieważ uzyskujesz dostęp do interfejsu API programu Graph hello hello kod odnosi się tooit jako `"myGraphService"`. Możesz skonfigurować obserwatora, który informuje użytkownika, gdy dowolne zmiany z tokenem hello. Po uzyskaniu tokenu hello powrócić hello użytkownika wstecz toohello `masterView`.

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

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a>Określanie hello toosearch widok wzorca i wyświetlanie użytkownikom hello hello interfejsu API programu Graph
Aplikacji Master-widok-kontroler (MVC), który wyświetla hello zwróciła dane w siatce hello wykracza poza zakres tego przewodnika hello i wiele online samouczki wyjaśniają sposób toobuild jeden. Ten kod jest w pliku szkielet hello. Należy jednak toodeal z kilku czynności w aplikacji MVC:

* ODCIĘTA, gdy użytkownik wpisze coś w polu wyszukiwania hello
* Udostępniać obiekt danych wstecz toohello MasterView, co umożliwia wyświetlanie wyników hello w siatce hello

Robimy tych poniżej.

### <a name="add-a-check-toosee-if-youre-logged-in"></a>Dodaj toosee wyboru, jeśli jest zalogowany
Aplikacja Hello pojawia się tylko hello użytkownik nie jest zalogowany, jeśli istnieje już token w pamięci podręcznej hello jest toocheck inteligentne. Jeśli nie, nastąpi przekierowanie toohello LoginView dla toosign użytkownika hello w. Jeśli możesz odwołać hello najlepsze sposób toodo akcje po załadowaniu widoku jest toouse hello `viewDidLoad()` metoda zapewniająca firmy Apple, NAS.

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

### <a name="update-hello-table-view-when-data-is-received"></a>Aktualizacja hello widoku tabeli po odebraniu danych
Gdy hello interfejsu API programu Graph zwraca dane, należy toodisplay hello danych. Dla uproszczenia Oto wszystkich hello kodu tooupdate hello tabeli. W kodzie umożliwiającego MVC można wkleić tylko hello właściwych wartości.

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

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a>Podaj hello toocall sposób interfejsu API programu Graph, gdy użytkownik wpisze w polu wyszukiwania hello
Gdy użytkownik wpisze wyszukiwania w polu hello, należy tooshove który za pośrednictwem toohello interfejsu API programu Graph. Witaj `GraphAPICaller` klasy, która będzie kompilowana w hello następującego kodu, oddziela funkcji wyszukiwania hello hello prezentacji. Na razie Napiszmy kod hello źródła żadnych wyszukiwania znaków toohello interfejsu API programu Graph. Firma Microsoft w tym celu udostępnia metodę o nazwie `lookupInGraph`, który przyjmuje ciąg hello chcemy toosearch dla.

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

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a>Zapis pomocnika hello tooaccess klasy interfejsu API programu Graph
Jest to core hello naszej aplikacji. Natomiast hello rest został Wstawianie kodu we wzorcu MVC domyślnego powitania od firmy Apple, w tym miejscu pisania kodu tooquery hello wykresu jako użytkownika hello typów, a następnie zwrócić te dane. Oto kod hello i następuje szczegółowy opis.

### <a name="create-a-new-objective-c-header-file"></a>Utwórz nowy plik nagłówka Objective C
Nazwa pliku hello `GraphAPICaller.h`i Dodaj hello następującego kodu.

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

Miejscu zobaczysz, że określona metoda przyjmuje ciągiem i zwraca completionBlock. Ta completionBlock jako użytkownik może mieć odgadnąć, spowoduje zaktualizowanie tabeli hello podając obiektu wypełnione danych w czasie rzeczywistym jako hello wyszukiwanie użytkowników.

### <a name="create-a-new-objective-c-file"></a>Utwórz nowy plik języka Objective C
Nazwa pliku hello `GraphAPICaller.m`i dodaj następujące metody hello.

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

Przejdźmy za pomocą tej metody szczegółowo.

podstawowe Hello tego kodu jest hello `NXOAuth2Request`, metodę, która przyjmuje parametry hello, który zdefiniowano w pliku settings.plist hello.

Witaj pierwszym krokiem jest tooconstruct hello prawo wywołania interfejsu API programu Graph. Ponieważ wywoływania `/users`, możesz określić, że dołączając zasobu interfejsu API programu Graph toohello wraz z hello wersji. Dobrym tooput znaczeniu je w pliku ustawień zewnętrznych, ponieważ te można zmienić w miarę rozwoju środowisko hello interfejsu API.

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

Następnie należy parametry toospecify będzie również zawierał toohello wywołania interfejsu API programu Graph. Jest *bardzo ważne* nie umieszczenie parametrów hello w punkcie końcowym zasobów hello ponieważ która zostaje wyczyszczona dla wszystkich znaków zgodnych-URI w czasie wykonywania. W parametrach hello należy podać wszystkie kod zapytania.

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

Można zauważyć wymaga `convertParamsToDictionary` metodę, która jeszcze nie zostać jeszcze zapisane. Umożliwia to teraz zrobić na końcu pliku hello hello:

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
Następnie można użyć hello `NXOAuth2Request` metody tooget dane z powrotem z hello interfejsu API w formacie JSON.

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

Na koniec Przyjrzyjmy się jak zwrócić hello danych toohello MasterViewController. dane Hello zwraca serializowane i musi toobe deserializacji i załadowany w obiekcie tego hello MainViewController, jaką może wykorzystać. W tym celu ma szkielet hello `User.m/h` pliku, który tworzy obiekt użytkownika. Należy wypełnić tego obiektu użytkownika o informacje z hello wykresu.

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


## <a name="run-hello-sample"></a>Uruchom hello próbki
Jeśli już używana szkielet hello lub po oraz wskazówki hello teraz należy uruchomić aplikację. Uruchom hello symulator i kliknij przycisk **Zaloguj** toouse hello aplikacji.

## <a name="get-security-updates-for-our-product"></a>Pobierz aktualizacje zabezpieczeń naszych produktów
Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez odwiedzenie hello [Witryna TechCenter poświęcona zabezpieczeniom](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.

