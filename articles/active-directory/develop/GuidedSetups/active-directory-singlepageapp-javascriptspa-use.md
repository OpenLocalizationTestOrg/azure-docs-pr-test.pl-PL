---
title: "aaaAzure AD v2 JS SPA instrukcje konfiguracji - Użyj | Dokumentacja firmy Microsoft"
description: "Jak aplikacje JavaScript SPA można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 4f7f824ed787d998dc4aea3dc21c95d7dfe70ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a>Użyj hello biblioteki uwierzytelniania firmy Microsoft (MSAL) toosign w hello użytkownika

1.  Utwórz plik o nazwie `app.js`. Jeśli używasz programu Visual Studio, wybierz hello projektu (folder główny projekt), kliknij prawym przyciskiem myszy i wybierz: `Add`  >  `New Item`  >  `JavaScript File`:
2.  Dodaj hello następującego kodu tooyour `app.js` pliku:

```javascript
// Graph API endpoint tooshow user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used tooobtain hello access token tooread user profile
var graphAPIScopes = ["https://graph.microsoft.com/user.read"];

// Initialize application
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});

//Previous version of msal uses redirect url via a property
if (userAgentApplication.redirectUri) {
    userAgentApplication.redirectUri = msalconfig.redirectUri;
}

window.onload = function () {
    // If page is refreshed, continue toodisplay user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call hello Microsoft Graph API and display hello results on hello page. Sign hello user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user toosign in via loginRedirect.
        // This will redirect user toohello Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // hello call toologinRedirect above frontloads hello consent tooquery Graph API during hello sign-in.
        // If you want toouse dynamic consent, just remove hello graphAPIScopes from loginRedirect call.
        // As such, user will be prompted toogive consent when requested access tooa resource that 
        // he/she hasn't consented before. In hello case of this application - 
        // hello first time hello Graph API call tooobtain user's profile is executed.
    } else {
        // If user is already signed in, display hello user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API tooshow hello user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order toocall hello Graph API, an access token needs toobe acquired.
        // Try tooacquire hello token used tooquery Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After hello access token is acquired, call hello Web API, sending hello acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If hello acquireTokenSilent() method fails, then acquire hello token interactively via acquireTokenRedirect().
                // In this case, hello browser will redirect user back toohello Azure Active Directory v2 Endpoint so hello user 
                // can reenter hello current username/ password and/ or give consent toonew permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get hello token silently, hello Graph API call results will be made and results will be displayed in hello page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() tooshow results.
 * @param {string} errorDesc - If error occur, hello error message
 * @param {object} token - hello token received from login
 * @param {object} error - hello error string
 * @param {string} tokenType - hello token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in hello page
 * @param {string} endpoint - hello endpoint used for hello error message
 * @param {string} error - Error string
 * @param {string} errorDesc - Error description
 */
function showError(endpoint, error, errorDesc) {
    var formattedError = JSON.stringify(error, null, 4);
    if (formattedError.length < 3) {
        formattedError = error;
    }
    document.getElementById("errorMessage").innerHTML = "An error has occurred:<br/>Endpoint: " + endpoint + "<br/>Error: " + formattedError + "<br/>" + errorDesc;
    console.error(error);
}

```

<!--start-collapse-->
### <a name="more-information"></a>Więcej informacji

Po kliknięciu hello *"Wywołaj Microsoft interfejsu API programu Graph"* przycisk powitania po raz pierwszy, `callGraphApi` wywołania metody `loginRedirect` toosign w hello użytkownika. Ta metoda powoduje przekierowanie hello użytkownika toohello *punktu końcowego programu Microsoft Azure Active Directory v2* tooprompt i sprawdzanie poprawności poświadczeń użytkownika hello. Wyniku pomyślnego logowania, użytkownik hello jest przekierowane toohello wstecz oryginalnego *index.html* strony i token odebraniu przetworzonych przez `msal.js` i hello informacji zawartych w tokenie hello są buforowane. Token ten jest nazywany hello *token Identyfikatora* i zawiera podstawowe informacje o użytkowniku hello, takie jak nazwa wyświetlana użytkownika hello. Jeśli planujesz toouse wszystkie dane wprowadzone przez ten token do celów należy się upewnić, czy token został zweryfikowany przez użytkownika tooguarantee serwera wewnętrznej bazy danych, która hello tokenu toomake został wystawiony tooa prawidłowego użytkownika dla aplikacji.

Hello SPA wygenerowane przez ten przewodnik nie oznacza, że użycie bezpośrednio hello identyfikator tokenu — zamiast tego wywołuje `acquireTokenSilent` i/lub `acquireTokenRedirect` tooacquire *token dostępu* używane hello tooquery interfejsu API programu Microsoft Graph. Przykładowe, która weryfikuje token Identyfikatora hello, należy przyjrzeć [to](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 próbki") przykładowej aplikacji w usłudze GitHub — Witaj w przykładzie użyto Interfejs API sieci Web platformy ASP.NET dla tokenu weryfikacji.

#### <a name="getting-a-user-token-interactively"></a>Pobieranie tokenu użytkownika interakcyjnego

Po hello początkowego logowania, nie ma hello Poproś użytkowników tooreauthenticate za każdym razem, gdy muszą toorequest tooaccess token zasobu — tak *acquireTokenSilent* powinien być używany przez większość hello czasu tooacquire tokenów. Istnieje jednak sytuacji należy tooforce użytkownicy korzystają z usługi Azure Active Directory punktu końcowego v2 — Oto kilka przykładów:
-   Użytkownicy mogą potrzebować tooreenter poświadczeń ponieważ hello hasło wygasło
-   Żąda dostępu tooa zasób, który hello tooconsent potrzeb użytkownika do aplikacji
-   Uwierzytelnianie dwuskładnikowe jest wymagana

Wywoływanie hello *acquireTokenRedirect(scope)* powoduje przekierowanie do punktu końcowego toohello v2 usługi Azure Active Directory użytkowników (lub *acquireTokenPopup(scope)* wynik w oknie podręcznym) których użytkownicy muszą toointeract z przez albo potwierdzenie poświadczeń, podając toohello zgody hello wymaganych zasobów lub kończenie uwierzytelniania dwuskładnikowego hello.

#### <a name="getting-a-user-token-silently"></a>Pobieranie tokenu użytkownika dyskretnej
Witaj ` acquireTokenSilent` obsługiwała przejęć tokenu i wznowienie bez interakcji użytkownika. Po `loginRedirect` (lub `loginPopup`) jest wykonywana na powitania po raz pierwszy, `acquireTokenSilent` hello metody najczęściej używanych tooobtain tokenów używanych tooaccess chronionych zasobów w kolejnych wywołaniach — jako toorequest wywołania lub odnowić tokeny są wprowadzane w trybie dyskretnym.
`acquireTokenSilent`może zakończyć się niepowodzeniem w niektórych przypadkach — na przykład użytkownik hello hasło wygasło. Aplikacja może obsłużyć tego wyjątku na dwa sposoby:

1.  Nawiązywanie połączeń za`acquireTokenRedirect` od razu, co powoduje monitowanie hello toosign użytkownika w. Ten wzorzec jest często używana w aplikacji online w przypadku, gdy brak nieuwierzytelnione zawartości w toohello dostępne dla użytkowników aplikacji hello. Przykładowe Hello wygenerowane za pomocą tego Instalatora z przewodnikiem używa tego wzorca.

2. Aplikacje można również ustawić oznaczenia wizualne użytkownik toohello interakcyjne logowanie jest wymagany, dlatego hello użytkownik może wybrać toosign odpowiednich momentach hello w lub ponowić aplikacji hello `acquireTokenSilent` w późniejszym czasie. Jest ona powszechnie stosowana, gdy hello użytkownik może użyć innych funkcji aplikacji hello bez są zakłócone — na przykład Brak dostępnej zawartości nieuwierzytelnione w aplikacji hello. W takim przypadku hello użytkownika można zdecydować, kiedy mają toosign tooaccess hello chronionych zasobów w programie lub toorefresh hello przestarzałe informacje.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Wywołanie interfejsu API programu Microsoft Graph hello przy użyciu tokenu hello, który został uzyskany

Dodaj hello następującego kodu tooyour `app.js` pliku:

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used toodisplay hello results
 * @param {object} showTokenElement = HTML element used toodisplay hello RAW access token
 */
function callWebApiWithToken(endpoint, token, responseElement, showTokenElement) {
    var headers = new Headers();
    var bearer = "Bearer " + token;
    headers.append("Authorization", bearer);
    var options = {
        method: "GET",
        headers: headers
    };

    fetch(endpoint, options)
        .then(function (response) {
            var contentType = response.headers.get("content-type");
            if (response.status === 200 && contentType && contentType.indexOf("application/json") !== -1) {
                response.json()
                    .then(function (data) {
                        // Display response in hello page
                        console.log(data);
                        responseElement.innerHTML = JSON.stringify(data, null, 4);
                        if (showTokenElement) {
                            showTokenElement.parentElement.classList.remove("hidden");
                            showTokenElement.innerHTML = token;
                        }
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            } else {
                response.json()
                    .then(function (data) {
                        // Display response as error in hello page
                        showError(endpoint, data);
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            }
        })
        .catch(function (error) {
            showError(endpoint, error);
        });
}
```
<!--start-collapse-->

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Więcej informacji na temat nawiązywania połączenia przed chronionego interfejsu API REST

W przykładowej aplikacji hello utworzone przez tego przewodnika, hello `callWebApiWithToken()` metoda jest używana toomake HTTP `GET` żądania dotyczącego zasobu chronionego wymagającego wywołującego zawartości toohello token, a następnie wróć hello. Ta metoda dodaje token hello nabyte w hello *nagłówek autoryzacji HTTP*. Utworzone przez tego przewodnika hello przykładowej aplikacji hello zasób jest hello interfejsu API programu Microsoft Graph *mnie* punktu końcowego — Wyświetla informacje o profilu użytkownika hello.

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Dodaj metody toosign limit hello użytkownika

Dodaj hello następującego kodu tooyour `app.js` pliku:

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
