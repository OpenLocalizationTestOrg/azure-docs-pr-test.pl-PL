### <span data-ttu-id="58248-101"><a name="server-auth"></a>Instrukcje: uwierzytelnianie za pomocą dostawcy (przepływ serwera)</span><span class="sxs-lookup"><span data-stu-id="58248-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="58248-102">Aby usługa Mobile Apps zarządzała procesem uwierzytelniania w aplikacji, musisz zarejestrować swoją aplikację u dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="58248-102">To have Mobile Apps manage the authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="58248-103">Następnie w usłudze Azure App Service musisz skonfigurować identyfikator aplikacji oraz wpis tajny udostępniony przez dostawcę.</span><span class="sxs-lookup"><span data-stu-id="58248-103">Then in your Azure App Service, you need to configure the application ID and secret provided by your provider.</span></span>
<span data-ttu-id="58248-104">Aby uzyskać więcej informacji, zapoznaj się z samouczkiem [Dodawanie uwierzytelniania do aplikacji](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="58248-104">For more information, see the tutorial [Add authentication to your app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="58248-105">Po zarejestrowaniu dostawcy tożsamości wywołaj metodę `.login()` z nazwą dostawcy.</span><span class="sxs-lookup"><span data-stu-id="58248-105">Once you have registered your identity provider, call the `.login()` method with the name of your provider.</span></span> <span data-ttu-id="58248-106">Na przykład aby zalogować się za pomocą konta usługi Facebook, użyj następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="58248-106">For example, to login with Facebook use the following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="58248-107">Prawidłowe wartości dla dostawcy to „aad”, „facebook”, „google”, „microsoftaccount” oraz „twitter”.</span><span class="sxs-lookup"><span data-stu-id="58248-107">The valid values for the provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="58248-108">Obecnie uwierzytelnianie za pomocą konta Google nie działa za pośrednictwem przepływu serwera.</span><span class="sxs-lookup"><span data-stu-id="58248-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="58248-109">Aby uwierzytelnić się za pomocą konta Google, musisz użyć [metody przepływu klienta](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="58248-109">To authenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="58248-110">W tym przypadku usługa Azure App Service zarządza przepływem uwierzytelniania OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="58248-110">In this case, Azure App Service manages the OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="58248-111">Wyświetla stronę logowania wybranego dostawcy i generuje token uwierzytelniania usługi App Service po pomyślnym zalogowaniu się u danego dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="58248-111">It displays the login page of the selected provider and generates an App Service authentication token after successful login with the identity provider.</span></span> <span data-ttu-id="58248-112">Po zakończeniu swojego działania funkcja logowania zwraca obiekt JSON, który udostępnia zarówno identyfikator użytkownika, jak i token uwierzytelniania usługi App Service, odpowiednio w polach userId oraz authenticationToken.</span><span class="sxs-lookup"><span data-stu-id="58248-112">The login function, when complete, returns a JSON object that exposes both the user ID and App Service authentication token in the userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="58248-113">Ten token można zapisać w pamięci podręcznej i ponownie go używać, dopóki nie wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="58248-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="58248-114"><a name="client-auth"></a>Instrukcje: uwierzytelnianie za pomocą dostawcy (przepływ klienta)</span><span class="sxs-lookup"><span data-stu-id="58248-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="58248-115">Aplikacja może również niezależnie skontaktować się z dostawcą tożsamości, a następnie udostępnić zwrócony token usłudze App Service na potrzeby uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="58248-115">Your app can also independently contact the identity provider and then provide the returned token to your App Service for authentication.</span></span> <span data-ttu-id="58248-116">Ten przepływ klienta pozwala zapewnić środowisko logowania jednokrotnego dla użytkowników bądź pobrać dodatkowe dane użytkownika od dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="58248-116">This client flow enables you to provide a single sign-in experience for users or to retrieve additional user data from the identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="58248-117">Podstawowy przykład uwierzytelniania przy użyciu sieci społecznościowych</span><span class="sxs-lookup"><span data-stu-id="58248-117">Social Authentication basic example</span></span>

<span data-ttu-id="58248-118">W tym przykładzie na potrzeby uwierzytelniania użyto zestawu SDK klienta usługi Facebook:</span><span class="sxs-lookup"><span data-stu-id="58248-118">This example uses Facebook client SDK for authentication:</span></span>

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
<span data-ttu-id="58248-119">W tym przykładzie założono, że token udostępniony przez zestaw SDK danego dostawcy jest przechowywany w zmiennej token.</span><span class="sxs-lookup"><span data-stu-id="58248-119">This example assumes that the token provided by the respective provider SDK is stored in the token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="58248-120">Przykład użycia konta Microsoft</span><span class="sxs-lookup"><span data-stu-id="58248-120">Microsoft Account example</span></span>

<span data-ttu-id="58248-121">W poniższym przykładzie użyto zestawu Live SDK, który obsługuje logowanie jednokrotne dla aplikacji ze Sklepu Windows przy użyciu konta Microsoft:</span><span class="sxs-lookup"><span data-stu-id="58248-121">The following example uses the Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

<span data-ttu-id="58248-122">W tym przykładzie token zostaje pobrany z usługi Live Connect i dostarczony do usługi App Service przez wywołanie funkcji logowania.</span><span class="sxs-lookup"><span data-stu-id="58248-122">This example gets a token from Live Connect, which is supplied to your App Service by calling the login function.</span></span>

###<span data-ttu-id="58248-123"><a name="auth-getinfo"></a>Instrukcje: pozyskiwanie informacji o uwierzytelnionym użytkowniku</span><span class="sxs-lookup"><span data-stu-id="58248-123"><a name="auth-getinfo"></a>How to: Obtain information about the authenticated user</span></span>

<span data-ttu-id="58248-124">Dane uwierzytelniania można pobrać z punktu końcowego `/.auth/me` przy użyciu wywołania HTTP z dowolną biblioteką AJAX.</span><span class="sxs-lookup"><span data-stu-id="58248-124">The authentication information can be retrieved from the `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="58248-125">Pamiętaj, aby dla nagłówka `X-ZUMO-AUTH` ustawić swój token uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="58248-125">Ensure you set the `X-ZUMO-AUTH` header to your authentication token.</span></span>  <span data-ttu-id="58248-126">Token uwierzytelniania jest przechowywany w elemencie `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="58248-126">The authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="58248-127">Na przykład aby użyć interfejsu API Fetch:</span><span class="sxs-lookup"><span data-stu-id="58248-127">For example, to use the fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // The user object contains the claims for the authenticated user
    });
```

<span data-ttu-id="58248-128">Interfejs Fetch jest dostępny jako [pakiet npm](https://www.npmjs.com/package/whatwg-fetch). Ponadto można go pobrać w przeglądarce z witryny [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="58248-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="58248-129">Do pobrania informacji można również użyć biblioteki jQuery lub innego interfejsu API AJAX.</span><span class="sxs-lookup"><span data-stu-id="58248-129">You could also use jQuery or another AJAX API to fetch the information.</span></span>  <span data-ttu-id="58248-130">Dane są odbierane w postaci obiektu JSON.</span><span class="sxs-lookup"><span data-stu-id="58248-130">Data is received as a JSON object.</span></span>
