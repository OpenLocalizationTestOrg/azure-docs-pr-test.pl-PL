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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Użyj hello biblioteki uwierzytelniania firmy Microsoft (MSAL) tooget token dla hello interfejsu API programu Microsoft Graph

Otwórz `ViewController.swift` i Zastąp kod hello:

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
### <a name="more-information"></a>Więcej informacji
#### <a name="getting-a-user-token-interactively"></a>Pobieranie tokenu użytkownika interakcyjnego
Wywołania hello `acquireToken` toosign użytkownika w hello metody powoduje monitowanie okna przeglądarki. Aplikacje zwykle wymagają toosign użytkownika, w interaktywnie hello muszą tooaccess po raz pierwszy chronionego zasobu lub tooacquire dyskretnej operacji tokenu nie powiedzie się, (np. hasło użytkownika hello ważność).

#### <a name="getting-a-user-token-silently"></a>Pobieranie tokenu użytkownika dyskretnej
Witaj `acquireTokenSilent` obsługiwała przejęć tokenu i wznowienie bez interakcji użytkownika. Po `acquireToken` jest wykonywana na powitania po raz pierwszy, `acquireTokenSilent` hello metody najczęściej używanych tooobtain tokenów używanych tooaccess chronionych zasobów w kolejnych wywołaniach — jako toorequest wywołania lub odnowić tokeny są wprowadzane w trybie dyskretnym.

Po pewnym czasie `acquireTokenSilent` zakończy się niepowodzeniem — np. użytkownika hello zalogował lub została zmieniona hasła na innym urządzeniu. Gdy MSAL wykryje, że hello problem można rozwiązać, gdyż akcję interaktywne, jego generowane `MSALErrorCode.interactionRequired` wyjątku. Aplikacja może obsłużyć tego wyjątku na dwa sposoby:

1.  Nawiązywanie połączeń z `acquireToken` od razu, co powoduje monitowanie hello toosign użytkownika w. Ten wzorzec jest zazwyczaj używany w aplikacji online w przypadku, gdy nie żadnej zawartości w trybie offline w aplikacji hello dostępnej dla użytkownika hello. Witaj przykładowej aplikacji wygenerowane przez tę konfigurację z przewodnikiem używa tego wzorca: Zobacz go w akcji hello wykonania aplikacji hello po raz pierwszy. Ponieważ żaden użytkownik nigdy używana aplikacja hello `applicationContext.users().first` będzie zawierać wartości null, a ` MSALErrorCode.interactionRequired ` zostanie wygenerowany wyjątek. Witaj kodu w przykładowym hello, a następnie uchwytów hello wyjątku przez wywołanie metody `acquireToken` co powoduje monitowanie hello toosign użytkownika w.

2.  Aplikacje można również ustawić oznaczenia wizualne użytkownik toohello interakcyjne logowanie jest wymagany, dlatego hello użytkownik może wybrać toosign odpowiednich momentach hello w lub ponowić aplikacji hello `acquireTokenSilent` w późniejszym czasie. Służy to zwykle gdy hello użytkownik może użyć innych funkcji aplikacji hello bez są zakłócone — na przykład Brak dostępnej zawartości w trybie offline w aplikacji hello. W takim przypadku hello użytkownika można określić, gdy mają toosign w tooaccess hello chroniony zasób, lub toorefresh hello przestarzałe informacje lub aplikacji można określić tooretry `acquireTokenSilent` przywrócenie sieci po są tymczasowo niedostępne.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Wywołanie interfejsu API programu Microsoft Graph hello przy użyciu tokenu hello, który został uzyskany

Dodaj nową metodę hello poniżej zbyt`ViewController.swift`. Ta metoda jest używana toomake `GET` żądania dotyczącego przy użyciu interfejsu API Graph usługi Microsoft hello *nagłówek autoryzacji HTTP*:

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
### <a name="making-a-rest-call-against-a-protected-api"></a>Wywołania chronionego interfejsu API REST

W tej przykładowej aplikacji hello `getContentWithToken()` metoda jest używana toomake HTTP `GET` żądania dotyczącego zasobu chronionego wymagającego wywołującego zawartości toohello token, a następnie wróć hello. Ta metoda dodaje token hello nabyte w hello *nagłówek autoryzacji HTTP*. Dla tego przykładu zasób hello jest hello interfejsu API programu Microsoft Graph *mnie* punktu końcowego — Wyświetla informacje o profilu użytkownika hello.
<!--end-collapse-->

## <a name="set-up-sign-out"></a>Konfigurowanie wylogowania

Dodaj hello następujące metody zbyt`ViewController.swift` toosign limit hello użytkownika:

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
### <a name="more-info-on-sign-out"></a>Więcej informacji dotyczących wylogowania

Witaj `signoutButton` metoda usuwa hello użytkownika z hello pamięci podręcznej użytkownika MSAL — to skutecznie poinformuje MSAL tooforget hello bieżącego użytkownika dzięki tooacquire przyszłych żądania tokenu tylko powiedzie się, jeśli jest on toobe interakcyjne.

Mimo że aplikacji hello w tym przykładzie obsługuje pojedynczego użytkownika, MSAL obsługuje scenariusze, w których może być podpisana wiele kont na powitania jednocześnie — przykładem jest aplikacja poczty e-mail których użytkownik ma wiele kont.
<!--end-collapse-->

## <a name="register-hello-callback"></a>Zarejestruj hello wywołania zwrotnego

Po hello użytkownik jest uwierzytelniany, przeglądarki hello przekierowuje hello użytkownika wstecz toohello aplikacji. Wykonaj kroki hello poniżej tooregister to wywołanie zwrotne:

1.  Otwórz `AppDelegate.swift` i zaimportować MSAL:

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Dodaj następujące metody tooyour hello <code>AppDelegate</code> klasy toohandle wywołania zwrotne:
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

