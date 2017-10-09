---
title: "iOS v2 aaaAzure AD Getting Started - Użyj | Dokumentacja firmy Microsoft"
description: "Jak aplikacje systemu iOS (Swift) można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 22e67850e2e0b14b6d68815d8f23e18ce2e878ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="6b653-103">Użyj hello biblioteki uwierzytelniania firmy Microsoft (MSAL) tooget token dla hello interfejsu API programu Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="6b653-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="6b653-104">Otwórz `ViewController.swift` i Zastąp kod hello:</span><span class="sxs-lookup"><span data-stu-id="6b653-104">Open `ViewController.swift` and replace hello code with:</span></span>

```swift
import UIKit
import MSAL

class ViewController: UIViewController, UITextFieldDelegate, URLSessionDelegate {
    
    let kClientID = "Your_Application_Id_Here"
    let kAuthority = "https://login.microsoftonline.com/common/v2.0"

    let kGraphURI = "https://graph.microsoft.com/v1.0/me/"
    let kScopes: [String] = ["https://graph.microsoft.com/user.read"]
    
    var accessToken = String()
    var applicationContext = MSALPublicClientApplication.init()

    @IBOutlet weak var loggingText: UITextView!
    @IBOutlet weak var signoutButton: UIButton!

     // This button will invoke hello call toohello Microsoft Graph API. It uses the
     // built in Swift libraries toocreate a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check toosee if we have a current logged in user. If we don't, then we need toosign someone in.
            // We throw an interactionRequired so that we trigger hello interactive signin.
            
            if  try self.applicationContext.users().isEmpty {
                throw NSError.init(domain: "MSALErrorDomain", code: MSALErrorCode.interactionRequired.rawValue, userInfo: nil)
            } else {
            
            // Acquire a token for an existing user silently
            
            try self.applicationContext.acquireTokenSilent(forScopes: self.kScopes, user: applicationContext.users().first) { (result, error) in
    
                    if error == nil {
                        self.accessToken = (result?.accessToken)!
                        self.loggingText.text = "Refreshing token silently)"
                        self.loggingText.text = "Refreshed Access token is \(self.accessToken)"
                        
                        self.signoutButton.isEnabled = true;
                        self.getContentWithToken()
    
                    } else {
                        self.loggingText.text = "Could not acquire token silently: \(error ?? "No error information" as! Error)"
    
                    }
                }
            }
        }  catch let error as NSError {
            
            // interactionRequired means we need tooask hello user toosign-in. This usually happens
            // when hello user's Refresh Token is expired or if hello user has changed their password
            // among other possible reasons.
            
            if error.code == MSALErrorCode.interactionRequired.rawValue {
                
                self.applicationContext.acquireToken(forScopes: self.kScopes) { (result, error) in
                        if error == nil {
                            self.accessToken = (result?.accessToken)!
                            self.loggingText.text = "Access token is \(self.accessToken)"
                            self.signoutButton.isEnabled = true;
                            self.getContentWithToken()
                            
                        } else  {
                            self.loggingText.text = "Could not acquire token: \(error ?? "No error information" as! Error)"
                        }
                }
                
            }
            
        } catch {
            
            // This is hello catch all error.
            
            self.loggingText.text = "Unable tooacquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable toocreate Application Context. Error: \(error)"
        }
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        
        if self.accessToken.isEmpty {
            signoutButton.isEnabled = false; 
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="6b653-105">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="6b653-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="6b653-106">Pobieranie tokenu użytkownika interakcyjnego</span><span class="sxs-lookup"><span data-stu-id="6b653-106">Getting a user token interactively</span></span>
<span data-ttu-id="6b653-107">Wywołania hello `acquireToken` toosign użytkownika w hello metody powoduje monitowanie okna przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="6b653-107">Calling hello `acquireToken` method results in a browser window prompting hello user toosign in.</span></span> <span data-ttu-id="6b653-108">Aplikacje zwykle wymagają toosign użytkownika, w interaktywnie hello muszą tooaccess po raz pierwszy chronionego zasobu lub tooacquire dyskretnej operacji tokenu nie powiedzie się, (np. hasło użytkownika hello ważność).</span><span class="sxs-lookup"><span data-stu-id="6b653-108">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="6b653-109">Pobieranie tokenu użytkownika dyskretnej</span><span class="sxs-lookup"><span data-stu-id="6b653-109">Getting a user token silently</span></span>
<span data-ttu-id="6b653-110">Witaj `acquireTokenSilent` obsługiwała przejęć tokenu i wznowienie bez interakcji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6b653-110">hello `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="6b653-111">Po `acquireToken` jest wykonywana na powitania po raz pierwszy, `acquireTokenSilent` hello metody najczęściej używanych tooobtain tokenów używanych tooaccess chronionych zasobów w kolejnych wywołaniach — jako toorequest wywołania lub odnowić tokeny są wprowadzane w trybie dyskretnym.</span><span class="sxs-lookup"><span data-stu-id="6b653-111">After `acquireToken` is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>

<span data-ttu-id="6b653-112">Po pewnym czasie `acquireTokenSilent` zakończy się niepowodzeniem — np. użytkownika hello zalogował lub została zmieniona hasła na innym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="6b653-112">Eventually, `acquireTokenSilent` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="6b653-113">Gdy MSAL wykryje, że hello problem można rozwiązać, gdyż akcję interaktywne, jego generowane `MSALErrorCode.interactionRequired` wyjątku.</span><span class="sxs-lookup"><span data-stu-id="6b653-113">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="6b653-114">Aplikacja może obsłużyć tego wyjątku na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="6b653-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="6b653-115">Nawiązywanie połączeń z `acquireToken` od razu, co powoduje monitowanie hello toosign użytkownika w.</span><span class="sxs-lookup"><span data-stu-id="6b653-115">Make a call against `acquireToken` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="6b653-116">Ten wzorzec jest zazwyczaj używany w aplikacji online w przypadku, gdy nie żadnej zawartości w trybie offline w aplikacji hello dostępnej dla użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="6b653-116">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="6b653-117">Witaj przykładowej aplikacji wygenerowane przez tę konfigurację z przewodnikiem używa tego wzorca: Zobacz go w akcji hello wykonania aplikacji hello po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="6b653-117">hello sample application generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello application.</span></span> <span data-ttu-id="6b653-118">Ponieważ żaden użytkownik nigdy używana aplikacja hello `applicationContext.users().first` będzie zawierać wartości null, a ` MSALErrorCode.interactionRequired ` zostanie wygenerowany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="6b653-118">Because no user ever used hello application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="6b653-119">Witaj kodu w przykładowym hello, a następnie uchwytów hello wyjątku przez wywołanie metody `acquireToken` co powoduje monitowanie hello toosign użytkownika w.</span><span class="sxs-lookup"><span data-stu-id="6b653-119">hello code in hello sample then handles hello exception by calling `acquireToken` resulting in prompting hello user toosign in.</span></span>

2.  <span data-ttu-id="6b653-120">Aplikacje można również ustawić oznaczenia wizualne użytkownik toohello interakcyjne logowanie jest wymagany, dlatego hello użytkownik może wybrać toosign odpowiednich momentach hello w lub ponowić aplikacji hello `acquireTokenSilent` w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="6b653-120">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="6b653-121">Służy to zwykle gdy hello użytkownik może użyć innych funkcji aplikacji hello bez są zakłócone — na przykład Brak dostępnej zawartości w trybie offline w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6b653-121">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="6b653-122">W takim przypadku hello użytkownika można określić, gdy mają toosign w tooaccess hello chroniony zasób, lub toorefresh hello przestarzałe informacje lub aplikacji można określić tooretry `acquireTokenSilent` przywrócenie sieci po są tymczasowo niedostępne.</span><span class="sxs-lookup"><span data-stu-id="6b653-122">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="6b653-123">Wywołanie interfejsu API programu Microsoft Graph hello przy użyciu tokenu hello, który został uzyskany</span><span class="sxs-lookup"><span data-stu-id="6b653-123">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="6b653-124">Dodaj nową metodę hello poniżej zbyt`ViewController.swift`.</span><span class="sxs-lookup"><span data-stu-id="6b653-124">Add hello new method below too`ViewController.swift`.</span></span> <span data-ttu-id="6b653-125">Ta metoda jest używana toomake `GET` żądania dotyczącego przy użyciu interfejsu API Graph usługi Microsoft hello *nagłówek autoryzacji HTTP*:</span><span class="sxs-lookup"><span data-stu-id="6b653-125">This method is used toomake a `GET` request against hello Microsoft Graph API using an *HTTP Authorization header*:</span></span>

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify hello Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set hello Authorization header for hello request. We use Bearer tokens, so we specify Bearer + hello token we got from hello result
    request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")
    let urlSession = URLSession(configuration: sessionConfig, delegate: self, delegateQueue: OperationQueue.main)
    
    urlSession.dataTask(with: request) { data, response, error in
        let result = try? JSONSerialization.jsonObject(with: data!, options: [])
                    if result != nil {
                
                self.loggingText.text = result.debugDescription
            }
        }.resume()
}
```

<!--start-collapse-->
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="6b653-126">Wywołania chronionego interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="6b653-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="6b653-127">W tej przykładowej aplikacji hello `getContentWithToken()` metoda jest używana toomake HTTP `GET` żądania dotyczącego zasobu chronionego wymagającego wywołującego zawartości toohello token, a następnie wróć hello.</span><span class="sxs-lookup"><span data-stu-id="6b653-127">In this sample application, hello `getContentWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="6b653-128">Ta metoda dodaje token hello nabyte w hello *nagłówek autoryzacji HTTP*.</span><span class="sxs-lookup"><span data-stu-id="6b653-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="6b653-129">Dla tego przykładu zasób hello jest hello interfejsu API programu Microsoft Graph *mnie* punktu końcowego — Wyświetla informacje o profilu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="6b653-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="6b653-130">Konfigurowanie wylogowania</span><span class="sxs-lookup"><span data-stu-id="6b653-130">Set up sign-out</span></span>

<span data-ttu-id="6b653-131">Dodaj hello następujące metody zbyt`ViewController.swift` toosign limit hello użytkownika:</span><span class="sxs-lookup"><span data-stu-id="6b653-131">Add hello following method too`ViewController.swift` toosign out hello user:</span></span>

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from hello cache for this application for hello provided user
        // first parameter:   hello user tooremove from hello cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="6b653-132">Więcej informacji dotyczących wylogowania</span><span class="sxs-lookup"><span data-stu-id="6b653-132">More info on sign-out</span></span>

<span data-ttu-id="6b653-133">Witaj `signoutButton` metoda usuwa hello użytkownika z hello pamięci podręcznej użytkownika MSAL — to skutecznie poinformuje MSAL tooforget hello bieżącego użytkownika dzięki tooacquire przyszłych żądania tokenu tylko powiedzie się, jeśli jest on toobe interakcyjne.</span><span class="sxs-lookup"><span data-stu-id="6b653-133">hello `signoutButton` method removes hello user from hello MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>

<span data-ttu-id="6b653-134">Mimo że aplikacji hello w tym przykładzie obsługuje pojedynczego użytkownika, MSAL obsługuje scenariusze, w których może być podpisana wiele kont na powitania jednocześnie — przykładem jest aplikacja poczty e-mail których użytkownik ma wiele kont.</span><span class="sxs-lookup"><span data-stu-id="6b653-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-hello-callback"></a><span data-ttu-id="6b653-135">Zarejestruj hello wywołania zwrotnego</span><span class="sxs-lookup"><span data-stu-id="6b653-135">Register hello callback</span></span>

<span data-ttu-id="6b653-136">Po hello użytkownik jest uwierzytelniany, przeglądarki hello przekierowuje hello użytkownika wstecz toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6b653-136">Once hello user authenticates, hello browser redirects hello user back toohello application.</span></span> <span data-ttu-id="6b653-137">Wykonaj kroki hello poniżej tooregister to wywołanie zwrotne:</span><span class="sxs-lookup"><span data-stu-id="6b653-137">Follow hello steps below tooregister this callback:</span></span>

1.  <span data-ttu-id="6b653-138">Otwórz `AppDelegate.swift` i zaimportować MSAL:</span><span class="sxs-lookup"><span data-stu-id="6b653-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="6b653-139">Dodaj następujące metody tooyour hello <code>AppDelegate</code> klasy toohandle wywołania zwrotne:</span><span class="sxs-lookup"><span data-stu-id="6b653-139">Add hello following method tooyour <code>AppDelegate</code> class toohandle callbacks:</span></span>
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if hello URL matches hello redirect URI for a pending AppAuth
// authorization request and if so, will look for hello code in hello response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

