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
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a><span data-ttu-id="d10e4-103">Użyj hello biblioteki uwierzytelniania firmy Microsoft (MSAL) toosign w hello użytkownika</span><span class="sxs-lookup"><span data-stu-id="d10e4-103">Use hello Microsoft Authentication Library (MSAL) toosign-in hello user</span></span>

1.  <span data-ttu-id="d10e4-104">Utwórz plik o nazwie `app.js`.</span><span class="sxs-lookup"><span data-stu-id="d10e4-104">Create a file named `app.js`.</span></span> <span data-ttu-id="d10e4-105">Jeśli używasz programu Visual Studio, wybierz hello projektu (folder główny projekt), kliknij prawym przyciskiem myszy i wybierz: `Add`  >  `New Item`  >  `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="d10e4-105">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="d10e4-106">Dodaj hello następującego kodu tooyour `app.js` pliku:</span><span class="sxs-lookup"><span data-stu-id="d10e4-106">Add hello following code tooyour `app.js` file:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="d10e4-107">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="d10e4-107">More Information</span></span>

<span data-ttu-id="d10e4-108">Po kliknięciu hello *"Wywołaj Microsoft interfejsu API programu Graph"* przycisk powitania po raz pierwszy, `callGraphApi` wywołania metody `loginRedirect` toosign w hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d10e4-108">After a user clicks hello *‘Call Microsoft Graph API’* button for hello first time, `callGraphApi` method calls `loginRedirect` toosign in hello user.</span></span> <span data-ttu-id="d10e4-109">Ta metoda powoduje przekierowanie hello użytkownika toohello *punktu końcowego programu Microsoft Azure Active Directory v2* tooprompt i sprawdzanie poprawności poświadczeń użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d10e4-109">This method results in redirecting hello user toohello *Microsoft Azure Active Directory v2 endpoint* tooprompt and validate hello user's credentials.</span></span> <span data-ttu-id="d10e4-110">Wyniku pomyślnego logowania, użytkownik hello jest przekierowane toohello wstecz oryginalnego *index.html* strony i token odebraniu przetworzonych przez `msal.js` i hello informacji zawartych w tokenie hello są buforowane.</span><span class="sxs-lookup"><span data-stu-id="d10e4-110">As a result of a successful sign-in, hello user is redirected back toohello original *index.html* page, and a token is received, processed by `msal.js` and hello information contained in hello token is cached.</span></span> <span data-ttu-id="d10e4-111">Token ten jest nazywany hello *token Identyfikatora* i zawiera podstawowe informacje o użytkowniku hello, takie jak nazwa wyświetlana użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d10e4-111">This token is known as hello *ID token* and contains basic information about hello user, such as hello user display name.</span></span> <span data-ttu-id="d10e4-112">Jeśli planujesz toouse wszystkie dane wprowadzone przez ten token do celów należy się upewnić, czy token został zweryfikowany przez użytkownika tooguarantee serwera wewnętrznej bazy danych, która hello tokenu toomake został wystawiony tooa prawidłowego użytkownika dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d10e4-112">If you plan toouse any data provided by this token for any purposes, you need toomake sure this token is validated by your backend server tooguarantee that hello token was issued tooa valid user for your application.</span></span>

<span data-ttu-id="d10e4-113">Hello SPA wygenerowane przez ten przewodnik nie oznacza, że użycie bezpośrednio hello identyfikator tokenu — zamiast tego wywołuje `acquireTokenSilent` i/lub `acquireTokenRedirect` tooacquire *token dostępu* używane hello tooquery interfejsu API programu Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d10e4-113">hello SPA generated by this guide does not make use directly of hello ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` tooacquire an *access token* used tooquery hello Microsoft Graph API.</span></span> <span data-ttu-id="d10e4-114">Przykładowe, która weryfikuje token Identyfikatora hello, należy przyjrzeć [to](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 próbki") przykładowej aplikacji w usłudze GitHub — Witaj w przykładzie użyto Interfejs API sieci Web platformy ASP.NET dla tokenu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="d10e4-114">If you need a sample that validates hello ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – hello sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="d10e4-115">Pobieranie tokenu użytkownika interakcyjnego</span><span class="sxs-lookup"><span data-stu-id="d10e4-115">Getting a user token interactively</span></span>

<span data-ttu-id="d10e4-116">Po hello początkowego logowania, nie ma hello Poproś użytkowników tooreauthenticate za każdym razem, gdy muszą toorequest tooaccess token zasobu — tak *acquireTokenSilent* powinien być używany przez większość hello czasu tooacquire tokenów.</span><span class="sxs-lookup"><span data-stu-id="d10e4-116">After hello initial sign-in, you do not want hello ask users tooreauthenticate every time they need toorequest a token tooaccess a resource – so *acquireTokenSilent* should be used most of hello time tooacquire tokens.</span></span> <span data-ttu-id="d10e4-117">Istnieje jednak sytuacji należy tooforce użytkownicy korzystają z usługi Azure Active Directory punktu końcowego v2 — Oto kilka przykładów:</span><span class="sxs-lookup"><span data-stu-id="d10e4-117">There are situations however that you need tooforce users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="d10e4-118">Użytkownicy mogą potrzebować tooreenter poświadczeń ponieważ hello hasło wygasło</span><span class="sxs-lookup"><span data-stu-id="d10e4-118">Users may need tooreenter their credentials because hello password has expired</span></span>
-   <span data-ttu-id="d10e4-119">Żąda dostępu tooa zasób, który hello tooconsent potrzeb użytkownika do aplikacji</span><span class="sxs-lookup"><span data-stu-id="d10e4-119">Your application is requesting access tooa resource that hello user needs tooconsent to</span></span>
-   <span data-ttu-id="d10e4-120">Uwierzytelnianie dwuskładnikowe jest wymagana</span><span class="sxs-lookup"><span data-stu-id="d10e4-120">Two factor authentication is required</span></span>

<span data-ttu-id="d10e4-121">Wywoływanie hello *acquireTokenRedirect(scope)* powoduje przekierowanie do punktu końcowego toohello v2 usługi Azure Active Directory użytkowników (lub *acquireTokenPopup(scope)* wynik w oknie podręcznym) których użytkownicy muszą toointeract z przez albo potwierdzenie poświadczeń, podając toohello zgody hello wymaganych zasobów lub kończenie uwierzytelniania dwuskładnikowego hello.</span><span class="sxs-lookup"><span data-stu-id="d10e4-121">Calling hello *acquireTokenRedirect(scope)* result in redirecting users toohello Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need toointeract with by either confirming their credentials, giving hello consent toohello required resource, or completing hello two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="d10e4-122">Pobieranie tokenu użytkownika dyskretnej</span><span class="sxs-lookup"><span data-stu-id="d10e4-122">Getting a user token silently</span></span>
<span data-ttu-id="d10e4-123">Witaj ` acquireTokenSilent` obsługiwała przejęć tokenu i wznowienie bez interakcji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d10e4-123">hello ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="d10e4-124">Po `loginRedirect` (lub `loginPopup`) jest wykonywana na powitania po raz pierwszy, `acquireTokenSilent` hello metody najczęściej używanych tooobtain tokenów używanych tooaccess chronionych zasobów w kolejnych wywołaniach — jako toorequest wywołania lub odnowić tokeny są wprowadzane w trybie dyskretnym.</span><span class="sxs-lookup"><span data-stu-id="d10e4-124">After `loginRedirect` (or `loginPopup`) is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="d10e4-125">`acquireTokenSilent`może zakończyć się niepowodzeniem w niektórych przypadkach — na przykład użytkownik hello hasło wygasło.</span><span class="sxs-lookup"><span data-stu-id="d10e4-125">`acquireTokenSilent` may fail in some cases – for example, hello user's password has expired.</span></span> <span data-ttu-id="d10e4-126">Aplikacja może obsłużyć tego wyjątku na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="d10e4-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="d10e4-127">Nawiązywanie połączeń za`acquireTokenRedirect` od razu, co powoduje monitowanie hello toosign użytkownika w.</span><span class="sxs-lookup"><span data-stu-id="d10e4-127">Make a call too`acquireTokenRedirect` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="d10e4-128">Ten wzorzec jest często używana w aplikacji online w przypadku, gdy brak nieuwierzytelnione zawartości w toohello dostępne dla użytkowników aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d10e4-128">This pattern is commonly used in online applications where there is no unauthenticated content in hello application available toohello user.</span></span> <span data-ttu-id="d10e4-129">Przykładowe Hello wygenerowane za pomocą tego Instalatora z przewodnikiem używa tego wzorca.</span><span class="sxs-lookup"><span data-stu-id="d10e4-129">hello sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="d10e4-130">Aplikacje można również ustawić oznaczenia wizualne użytkownik toohello interakcyjne logowanie jest wymagany, dlatego hello użytkownik może wybrać toosign odpowiednich momentach hello w lub ponowić aplikacji hello `acquireTokenSilent` w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="d10e4-130">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="d10e4-131">Jest ona powszechnie stosowana, gdy hello użytkownik może użyć innych funkcji aplikacji hello bez są zakłócone — na przykład Brak dostępnej zawartości nieuwierzytelnione w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d10e4-131">This is commonly used when hello user can use other functionality of hello application without being disrupted - for example, there is unauthenticated content available in hello application.</span></span> <span data-ttu-id="d10e4-132">W takim przypadku hello użytkownika można zdecydować, kiedy mają toosign tooaccess hello chronionych zasobów w programie lub toorefresh hello przestarzałe informacje.</span><span class="sxs-lookup"><span data-stu-id="d10e4-132">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="d10e4-133">Wywołanie interfejsu API programu Microsoft Graph hello przy użyciu tokenu hello, który został uzyskany</span><span class="sxs-lookup"><span data-stu-id="d10e4-133">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="d10e4-134">Dodaj hello następującego kodu tooyour `app.js` pliku:</span><span class="sxs-lookup"><span data-stu-id="d10e4-134">Add hello following code tooyour `app.js` file:</span></span>

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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="d10e4-135">Więcej informacji na temat nawiązywania połączenia przed chronionego interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="d10e4-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="d10e4-136">W przykładowej aplikacji hello utworzone przez tego przewodnika, hello `callWebApiWithToken()` metoda jest używana toomake HTTP `GET` żądania dotyczącego zasobu chronionego wymagającego wywołującego zawartości toohello token, a następnie wróć hello.</span><span class="sxs-lookup"><span data-stu-id="d10e4-136">In hello sample application created by this guide, hello `callWebApiWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="d10e4-137">Ta metoda dodaje token hello nabyte w hello *nagłówek autoryzacji HTTP*.</span><span class="sxs-lookup"><span data-stu-id="d10e4-137">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="d10e4-138">Utworzone przez tego przewodnika hello przykładowej aplikacji hello zasób jest hello interfejsu API programu Microsoft Graph *mnie* punktu końcowego — Wyświetla informacje o profilu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d10e4-138">For hello sample application created by this guide, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="d10e4-139">Dodaj metody toosign limit hello użytkownika</span><span class="sxs-lookup"><span data-stu-id="d10e4-139">Add a method toosign out hello user</span></span>

<span data-ttu-id="d10e4-140">Dodaj hello następującego kodu tooyour `app.js` pliku:</span><span class="sxs-lookup"><span data-stu-id="d10e4-140">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
