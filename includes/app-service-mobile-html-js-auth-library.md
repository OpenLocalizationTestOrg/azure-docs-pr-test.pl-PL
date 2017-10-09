### <span data-ttu-id="7e05a-101"><a name="server-auth"></a>Instrukcje: uwierzytelnianie za pomocą dostawcy (przepływ serwera)</span><span class="sxs-lookup"><span data-stu-id="7e05a-101"><a name="server-auth"></a>How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="7e05a-102">Aplikacje mobilne toohave zarządzać hello proces uwierzytelniania w aplikacji, musisz zarejestrować aplikację w usłudze dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="7e05a-102">toohave Mobile Apps manage hello authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="7e05a-103">W usłudze Azure App Service, wymagana będzie identyfikator aplikacji hello tooconfigure i klucz tajny dostarczonej przez dostawcę.</span><span class="sxs-lookup"><span data-stu-id="7e05a-103">Then in your Azure App Service, you need tooconfigure hello application ID and secret provided by your provider.</span></span>
<span data-ttu-id="7e05a-104">Aby uzyskać więcej informacji, zobacz samouczek hello [aplikacji tooyour authentication Dodaj](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="7e05a-104">For more information, see hello tutorial [Add authentication tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="7e05a-105">Po zarejestrowaniu dostawcy tożsamości, wywołaj hello `.login()` metodę o nazwie hello dostawcy.</span><span class="sxs-lookup"><span data-stu-id="7e05a-105">Once you have registered your identity provider, call hello `.login()` method with hello name of your provider.</span></span> <span data-ttu-id="7e05a-106">Na przykład toologin z usługą Facebook użyć hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="7e05a-106">For example, toologin with Facebook use hello following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="7e05a-107">Prawidłowe wartości dostawcy hello Hello to "aad", "facebook", "google", "microsoftaccount" i "twitter".</span><span class="sxs-lookup"><span data-stu-id="7e05a-107">hello valid values for hello provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="7e05a-108">Obecnie uwierzytelnianie za pomocą konta Google nie działa za pośrednictwem przepływu serwera.</span><span class="sxs-lookup"><span data-stu-id="7e05a-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="7e05a-109">tooauthenticate z serwisem Google, należy użyć [metody przepływu klienta](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="7e05a-109">tooauthenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="7e05a-110">W takim przypadku usługa aplikacji Azure zarządza przepływ uwierzytelniania hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="7e05a-110">In this case, Azure App Service manages hello OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="7e05a-111">Zostanie wyświetlona strona logowania hello hello wybranego dostawcy, a generuje token uwierzytelniania usługi aplikacji po pomyślnego logowania przy hello dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="7e05a-111">It displays hello login page of hello selected provider and generates an App Service authentication token after successful login with hello identity provider.</span></span> <span data-ttu-id="7e05a-112">funkcja logowania Hello, po zakończeniu zwraca obiekt JSON, który ujawnia zarówno hello identyfikator użytkownika, jak i usłudze aplikacji token uwierzytelniania w polach Nazwa użytkownika i authenticationToken hello, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="7e05a-112">hello login function, when complete, returns a JSON object that exposes both hello user ID and App Service authentication token in hello userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="7e05a-113">Ten token można zapisać w pamięci podręcznej i ponownie go używać, dopóki nie wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="7e05a-113">This token can be cached and reused until it expires.</span></span>

###<span data-ttu-id="7e05a-114"><a name="client-auth"></a>Instrukcje: uwierzytelnianie za pomocą dostawcy (przepływ klienta)</span><span class="sxs-lookup"><span data-stu-id="7e05a-114"><a name="client-auth"></a>How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="7e05a-115">Aplikację można również niezależnie skontaktuj się z dostawcą tożsamości hello, a następnie podaj hello zwrócił token tooyour usługi aplikacji — dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="7e05a-115">Your app can also independently contact hello identity provider and then provide hello returned token tooyour App Service for authentication.</span></span> <span data-ttu-id="7e05a-116">Ten przepływ klienta umożliwia tooprovide pojedynczego logowania dla użytkowników lub tooretrieve użytkownika dodatkowe dane z hello dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="7e05a-116">This client flow enables you tooprovide a single sign-in experience for users or tooretrieve additional user data from hello identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="7e05a-117">Podstawowy przykład uwierzytelniania przy użyciu sieci społecznościowych</span><span class="sxs-lookup"><span data-stu-id="7e05a-117">Social Authentication basic example</span></span>

<span data-ttu-id="7e05a-118">W tym przykładzie na potrzeby uwierzytelniania użyto zestawu SDK klienta usługi Facebook:</span><span class="sxs-lookup"><span data-stu-id="7e05a-118">This example uses Facebook client SDK for authentication:</span></span>

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
<span data-ttu-id="7e05a-119">W tym przykładzie założono hello token dostarczony przez dostawcę odpowiednich hello zestawu SDK jest przechowywana w zmiennej tokenu hello.</span><span class="sxs-lookup"><span data-stu-id="7e05a-119">This example assumes that hello token provided by hello respective provider SDK is stored in hello token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="7e05a-120">Przykład użycia konta Microsoft</span><span class="sxs-lookup"><span data-stu-id="7e05a-120">Microsoft Account example</span></span>

<span data-ttu-id="7e05a-121">Witaj przykładzie użyto następujących hello zestaw Live SDK, który obsługuje single-sign-on dla aplikacji ze Sklepu Windows przy użyciu Account Microsoft:</span><span class="sxs-lookup"><span data-stu-id="7e05a-121">hello following example uses hello Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

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

<span data-ttu-id="7e05a-122">W tym przykładzie pobiera token z Live Connect, który jest przez wywołanie funkcji logowania hello dostarczony tooyour usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7e05a-122">This example gets a token from Live Connect, which is supplied tooyour App Service by calling hello login function.</span></span>

###<span data-ttu-id="7e05a-123"><a name="auth-getinfo"></a>Porady: uzyskiwanie informacji na temat hello uwierzytelniony użytkownik</span><span class="sxs-lookup"><span data-stu-id="7e05a-123"><a name="auth-getinfo"></a>How to: Obtain information about hello authenticated user</span></span>

<span data-ttu-id="7e05a-124">informacje o uwierzytelnianiu Hello można pobrać z hello `/.auth/me` Wywołaj punktu końcowego za pomocą protokołu HTTP z dowolnej bibliotece technologii AJAX.</span><span class="sxs-lookup"><span data-stu-id="7e05a-124">hello authentication information can be retrieved from hello `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="7e05a-125">Upewnij się, ustaw hello `X-ZUMO-AUTH` token uwierzytelniania tooyour nagłówka.</span><span class="sxs-lookup"><span data-stu-id="7e05a-125">Ensure you set hello `X-ZUMO-AUTH` header tooyour authentication token.</span></span>  <span data-ttu-id="7e05a-126">Witaj token uwierzytelniania są przechowywane w `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="7e05a-126">hello authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="7e05a-127">Na przykład toouse hello pobranie interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="7e05a-127">For example, toouse hello fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

<span data-ttu-id="7e05a-128">Interfejs Fetch jest dostępny jako [pakiet npm](https://www.npmjs.com/package/whatwg-fetch). Ponadto można go pobrać w przeglądarce z witryny [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="7e05a-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="7e05a-129">Można także użyć jQuery lub innego interfejsu API technologii AJAX toofetch hello informacji.</span><span class="sxs-lookup"><span data-stu-id="7e05a-129">You could also use jQuery or another AJAX API toofetch hello information.</span></span>  <span data-ttu-id="7e05a-130">Dane są odbierane w postaci obiektu JSON.</span><span class="sxs-lookup"><span data-stu-id="7e05a-130">Data is received as a JSON object.</span></span>
