# <a name="add-sign-in-with-microsoft-to-an-aspnet-web-app"></a>Dodaj logowanie z firmy Microsoft do aplikacji sieci web platformy ASP.NET

W tym przewodniku pokazano, jak do implementowania logowania z firmą Microsoft za pomocą rozwiązania ASP.NET MVC z tradycyjnego aplikacji sieci web opartej na przeglądarce przy użyciu protokołu OpenID Connect. 

Na końcu tego przewodnika aplikacja będzie można zaakceptować znak ins osobiste konta (w tym outlook.com, live.com i inne), a także pracy i służbowych z firmy lub organizacji, która ma być zintegrowane z usługą Azure Active Directory. 

> W tym przewodniku wymaga programu Visual Studio 2015 Update 3 lub Visual Studio 2017 r.  Nie masz?  [Bezpłatnie pobrać Visual Studio 2017 r.](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>Jak działa w tym przewodniku

![Jak działa w tym przewodniku](media/active-directory-develop-guidedsetup-aspnetwebapp-intro/aspnetbrowsergeneral.png)

W tym przewodniku opiera się na scenariusz, w których przeglądarką uzyskuje dostęp do witryny sieci web ASP.NET, żądanie użytkownika do uwierzytelniania za pośrednictwem przycisku Zaloguj. W tym scenariuszu większość pracy do renderowania strony sieci web występuje po stronie serwera.

## <a name="libraries"></a>Biblioteki

W tym przewodniku korzysta z bibliotek następujące:

|Biblioteka|Opis|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|Oprogramowanie pośredniczące, które włącza aplikację na potrzeby uwierzytelniania OpenIdConnect|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|Oprogramowanie pośredniczące, który umożliwia aplikacjom obsługę plików cookie sesji użytkownika|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|Umożliwia aplikacji OWIN do uruchomienia na serwerze IIS za pomocą potoku żądania programu ASP.NET|

