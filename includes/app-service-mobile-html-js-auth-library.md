### <a name="server-auth"></a>Instrukcje: uwierzytelnianie za pomocą dostawcy (przepływ serwera)
Aplikacje mobilne toohave zarządzać hello proces uwierzytelniania w aplikacji, musisz zarejestrować aplikację w usłudze dostawcy tożsamości. W usłudze Azure App Service, wymagana będzie identyfikator aplikacji hello tooconfigure i klucz tajny dostarczonej przez dostawcę.
Aby uzyskać więcej informacji, zobacz samouczek hello [aplikacji tooyour authentication Dodaj](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).

Po zarejestrowaniu dostawcy tożsamości, wywołaj hello `.login()` metodę o nazwie hello dostawcy. Na przykład toologin z usługą Facebook użyć hello następującego kodu:

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

Prawidłowe wartości dostawcy hello Hello to "aad", "facebook", "google", "microsoftaccount" i "twitter".

> [!NOTE]
> Obecnie uwierzytelnianie za pomocą konta Google nie działa za pośrednictwem przepływu serwera.  tooauthenticate z serwisem Google, należy użyć [metody przepływu klienta](#client-auth).

W takim przypadku usługa aplikacji Azure zarządza przepływ uwierzytelniania hello OAuth 2.0.  Zostanie wyświetlona strona logowania hello hello wybranego dostawcy, a generuje token uwierzytelniania usługi aplikacji po pomyślnego logowania przy hello dostawcy tożsamości. funkcja logowania Hello, po zakończeniu zwraca obiekt JSON, który ujawnia zarówno hello identyfikator użytkownika, jak i usłudze aplikacji token uwierzytelniania w polach Nazwa użytkownika i authenticationToken hello, odpowiednio. Ten token można zapisać w pamięci podręcznej i ponownie go używać, dopóki nie wygaśnie.

###<a name="client-auth"></a>Instrukcje: uwierzytelnianie za pomocą dostawcy (przepływ klienta)

Aplikację można również niezależnie skontaktuj się z dostawcą tożsamości hello, a następnie podaj hello zwrócił token tooyour usługi aplikacji — dla uwierzytelniania. Ten przepływ klienta umożliwia tooprovide pojedynczego logowania dla użytkowników lub tooretrieve użytkownika dodatkowe dane z hello dostawcy tożsamości.

#### <a name="social-authentication-basic-example"></a>Podstawowy przykład uwierzytelniania przy użyciu sieci społecznościowych

W tym przykładzie na potrzeby uwierzytelniania użyto zestawu SDK klienta usługi Facebook:

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
W tym przykładzie założono hello token dostarczony przez dostawcę odpowiednich hello zestawu SDK jest przechowywana w zmiennej tokenu hello.

#### <a name="microsoft-account-example"></a>Przykład użycia konta Microsoft

Witaj przykładzie użyto następujących hello zestaw Live SDK, który obsługuje single-sign-on dla aplikacji ze Sklepu Windows przy użyciu Account Microsoft:

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

W tym przykładzie pobiera token z Live Connect, który jest przez wywołanie funkcji logowania hello dostarczony tooyour usługi aplikacji.

###<a name="auth-getinfo"></a>Porady: uzyskiwanie informacji na temat hello uwierzytelniony użytkownik

informacje o uwierzytelnianiu Hello można pobrać z hello `/.auth/me` Wywołaj punktu końcowego za pomocą protokołu HTTP z dowolnej bibliotece technologii AJAX.  Upewnij się, ustaw hello `X-ZUMO-AUTH` token uwierzytelniania tooyour nagłówka.  Witaj token uwierzytelniania są przechowywane w `client.currentUser.mobileServiceAuthenticationToken`.  Na przykład toouse hello pobranie interfejsu API:

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

Interfejs Fetch jest dostępny jako [pakiet npm](https://www.npmjs.com/package/whatwg-fetch). Ponadto można go pobrać w przeglądarce z witryny [CDNJS](https://cdnjs.com/libraries/fetch). Można także użyć jQuery lub innego interfejsu API technologii AJAX toofetch hello informacji.  Dane są odbierane w postaci obiektu JSON.
