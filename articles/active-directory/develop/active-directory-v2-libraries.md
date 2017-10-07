---
title: "biblioteki uwierzytelniania v2.0 usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Zgodny klient biblioteki i bibliotek oprogramowania pośredniczącego serwera i powiązane biblioteki, źródła i łączy próbek, dla punktu końcowego v2.0 usługi Azure Active Directory hello."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 19cec615-e51f-4141-9f8c-aaf38ff9f746
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7affdaac3a087b951d54d96fa68edde2a065172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-authentication-libraries"></a>Biblioteki uwierzytelniania v2.0 w usłudze Azure Active Directory
punktu końcowego v2.0 usługi Azure Active Directory (Azure AD) Hello obsługuje hello standardowych OAuth 2.0 i OpenID Connect 1.0. Można użyć różnych bibliotek firmy Microsoft i innych organizacjach z punktem końcowym v2.0 hello.

Podczas tworzenia aplikacji, która używa punktu końcowego v2.0 hello, zalecane jest użycie bibliotek, które są zapisywane przez ekspertów domeny protokołu, Obserwujący metodologii Security Development Lifecycle (SDL), są tak samo, jak [hello co następuje Microsoft] [Microsoft-SDL]. Jeśli zdecydujesz się kodu toohand obsługę protokołów hello, firma Microsoft zaleca wykonaj metodologii SDL i zwrócić szczególną uwagę zagadnienia dotyczące zabezpieczeń toohello w specyfikacji standardów powitania dla każdego protokołu.

## <a name="types-of-libraries"></a>Rodzaje bibliotek
Usługi Azure AD 2.0 współpracuje z dwóch typów biblioteki:

* **Bibliotek klienckich**. Natywny klienci i serwery używają tokenów dostępu tooget biblioteki klienta, wywoływania zasobów, takich jak Microsoft Graph.
* **Biblioteki oprogramowania pośredniczącego serwera**. Aplikacje sieci Web korzystać bibliotek oprogramowania pośredniczącego serwera dla logowania użytkownika. Interfejsów API sieci Web używaj tokenów toovalidate biblioteki oprogramowania pośredniczącego serwera, które są wysyłane przez klientów natywnych lub przez inne serwery.

## <a name="library-support"></a>Obsługa biblioteki
Można wybrać żadnej biblioteki zgodny ze standardami, korzystając z punktu końcowego v2.0 hello, dlatego jest ważne tooknow gdzie toogo pomocy technicznej. Problemy i żądania funkcji w kodzie biblioteki skontaktuj się z właścicielem biblioteki hello. Problemy i żądania funkcji w implementacji protokołu po stronie usługi hello kontakt z firmą Microsoft.

Biblioteki są dostępne w dwóch kategorii pomocy technicznej:

* **Obsługiwane przez firmę Microsoft**. Firma Microsoft oferuje poprawki dla bibliotek i wykonaniu SDL termin starannością na tych bibliotek.
* **Zgodne**. Microsoft przetestowała te biblioteki w podstawowe scenariusze i potwierdza, że działają z punktem końcowym v2.0 hello. Firma Microsoft zapewnia poprawki dotyczące biblioteki i nie przeprowadził Przegląd te biblioteki. Problemy i żądania funkcji powinny być projekt open source ukierunkowanej toohello biblioteki.

Listę bibliotek, które współpracują z punktem końcowym v2.0 hello na ten temat można znaleźć w kolejnych sekcjach hello w tym artykule.


## <a name="microsoft-supported-client-libraries"></a>Biblioteki klienta obsługiwane przez firmę Microsoft

> [!IMPORTANT]
> biblioteki Podgląd MSAL Hello są odpowiednie do użycia w środowisku produkcyjnym. Firma Microsoft udostępnia hello tego samego poziomu obsługi produkcji te biblioteki, tak jak skorzystać z bibliotek produkcji bieżącego (ADAL). Hello w wersji zapoznawczej firma Microsoft może wprowadzać zmiany toohello MSAL API format wewnętrznej pamięci podręcznej i innych mechanizmów te biblioteki bez powiadomienia, które będzie wymagane tootake oraz poprawki błędów lub ulepszenia funkcji. Może to mieć wpływ na aplikację. Na przykład format pamięci podręcznej toohello zmiany mogą mieć wpływ na użytkowników, np. wymaganie ich toosign w ponownie. Interfejs API może wymagać możesz tooupdate kodu. Podając hello wersji ogólnodostępnej firma Microsoft będzie wymagać wersji ogólnodostępnej toohello tooupdate w ciągu sześciu miesięcy, jako aplikacje napisane przy użyciu podglądu wersji biblioteki mogą przestać działać.

| Platforma | Biblioteka | Do pobrania | Kod źródłowy | Przykład | Dokumentacja
| --- | --- | --- | --- | --- | --- |
| Klient .NET, Sklep Windows, platformy uniwersalnej systemu Windows, Xamarin iOS i Android | MSAL .NET (wersja zapoznawcza) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Aplikacja klasyczna](guidedsetups/active-directory-mobileanddesktopapp-windowsdesktop-intro.md) |  |
| JavaScript | MSAL.js (wersja zapoznawcza) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Jednej strony aplikacji](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2) |  |
| systemy iOS, system macOS | MSAL (wersja zapoznawcza) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [Aplikacja systemu iOS](https://github.com/Azure-Samples/active-directory-msal-ios-swift) |  |
| Android | MSAL (wersja zapoznawcza) | [Witaj centralnym repozytorium](https://repo1.maven.org/maven2/com/microsoft/identity/client/msal/) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Aplikacji systemu android](guidedsetups/active-directory-mobileanddesktopapp-android-intro.md) | [JavaDocs](http://javadoc.io/doc/com.microsoft.identity.client/msal) |

## <a name="microsoft-supported-server-middleware-libraries"></a>Biblioteki oprogramowania pośredniczącego serwera obsługiwane przez firmę Microsoft

| Platforma | Biblioteka | Do pobrania | Kod źródłowy | Przykład | Dokumentacja
| --- | --- | --- | --- | --- | --- |
| .NET 4.x | OWIN OpenID Connect oprogramowania pośredniczącego |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[Witrynie CodePlex](http://katanaproject.codeplex.com) |[Aplikacji MVC](guidedsetups/active-directory-serversidewebapp-aspnetwebappowin-intro.md) | |
| .NET 4.x | Oprogramowanie pośredniczące elementu nośnego OAuth OWIN do AzureAD |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[Witrynie CodePlex](http://katanaproject.codeplex.com) |  | |
| .NET 4.x | Program obsługi tokenów JWT dla platformy .NET 4.5 | [NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/4.0.4.403061554) | [GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET Core | Oprogramowanie pośredniczące ASP.NET OpenID Connect |[Microsoft.AspNetCore.Authentication.OpenIdConnect (NuGet)][ServerLib-NetCore-Owin-Oidc-Lib] |[Zabezpieczenia programu ASP.NET (GitHub)][ServerLib-NetCore-Owin-Oidc-Repo] |[Aplikacji MVC](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2) |
| .NET Core | Oprogramowanie pośredniczące elementu nośnego OAuth ASP.NET |[Microsoft.AspNetCore.Authentication.OAuth (NuGet)][ServerLib-NetCore-Owin-Oauth-Lib] |[Zabezpieczenia programu ASP.NET (GitHub)][ServerLib-NetCore-Owin-Oauth-Repo] |  |
| .NET Core | Program obsługi tokenów JWT dla platformy .NET Core  |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| Node.js |Azure AD usługi Passport. |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Aplikacja sieci Web](active-directory-v2-devquickstarts-node-web.md)| |

## <a name="compatible-client-libraries"></a>Zgodny klient biblioteki
| Platforma | Nazwa biblioteki | Wersja przetestowany | Kod źródłowy | Przykład |
|:---:|:---:|:---:|:---:|:---:|
| Android |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib/wiki) |0.2.1 |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib) |[Przykładowej aplikacji natywnej](active-directory-v2-devquickstarts-android.md) |
| iOS |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |1.2.8 |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |[Przykładowej aplikacji natywnej](active-directory-v2-devquickstarts-ios.md) |
| JavaScript |[Hello.js](https://adodson.com/hello.js/) |1.13.5 |[Hello.js](https://github.com/MrSwitch/hello.js) |[SPA](https://github.com/Azure-Samples/active-directory-javascript-graphapi-web-v2) |

## <a name="compatible-server-middleware-libraries"></a>Biblioteki oprogramowania pośredniczącego serwera
| Platforma | Nazwa biblioteki | Wersja przetestowany | Kod źródłowy | Przykład |
|:---:|:---:|:---:|:---:|:---:|
| Java | [Scribejava Sekretarz Java](https://github.com/scribejava/scribejava) | [Wersja 3.2.0](https://github.com/scribejava/scribejava/releases/tag/scribejava-3.2.0) | [ScribeJava](https://github.com/scribejava/scribejava/archive/scribejava-3.2.0.zip) | |
| PHP | [powitania klienta oauth2 Ligi PHP](https://github.com/thephpleague/oauth2-client) | [Wersja 1.4.2](https://github.com/thephpleague/oauth2-client/releases/tag/1.4.2) | [Klient protokołu oauth2](https://github.com/thephpleague/oauth2-client/archive/1.4.2.zip) | |
| Platformy Python Flask |[Flask OAuthlib](https://github.com/lepture/flask-oauthlib) |0.9.3 |[Flask OAuthlib](https://github.com/lepture/flask-oauthlib) |[Aplikacja sieci Web](https://github.com/Azure-Samples/active-directory-python-flask-graphapi-web-v2) |
| Ruby |[OmniAuth](https://github.com/omniauth/omniauth/wiki) |omniauth:1.3.1</br>omniauth-oauth2:1.4.0 |[OmniAuth](https://github.com/omniauth/omniauth)</br>[OmniAuth OAuth2](https://github.com/intridea/omniauth-oauth2) |  |

## <a name="related-content"></a>Zawartość pokrewna
Aby uzyskać więcej informacji na temat punktu końcowego v2.0 hello Azure AD, zobacz hello [usługi Azure AD app model v2.0 omówienie][AAD-App-Model-V2-Overview].

<!--Image references-->

<!--Reference style links -->
[AAD-App-Model-V2-Overview]: ../active-directory-appmodel-v2-overview.md
[ClientLib-NET-Lib]: http://www.nuget.org/packages/Microsoft.Identity.Client
[ClientLib-NET-Repo]: https://github.com/AzureAD/microsoft-authentication-library-for-dotnet
[ClientLib-NET-Sample]: active-directory-v2-devquickstarts-wpf.md
[ClientLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ClientLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad
[ClientLib-Node-Sample]:/
[ClientLib-Iosmac-Lib]:/
[ClientLib-Iosmac-Repo]:/
[ClientLib-Iosmac-Sample]:/
[ClientLib-Android-Lib]:/
[ClientLib-Android-Repo]:/
[ClientLib-Android-Sample]:/
[ClientLib-Js-Lib]:/
[ClientLib-Js-Repo]:/
[ClientLib-Js-Sample]:/

[Microsoft-SDL]: http://www.microsoft.com/sdl/default.aspx
[ServerLib-Net4-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/
[ServerLib-Net4-Owin-Oidc-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oidc-Sample]: active-directory-v2-devquickstarts-dotnet-web.md
[ServerLib-Net4-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OAuth/
[ServerLib-Net4-Owin-Oauth-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oauth-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-dotnet-api/
[ServerLib-Net-Jwt-Lib]: https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt
[ServerLib-Net-Jwt-Repo]: https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet
[ServerLib-Net-Jwt-Sample]:/
[ServerLib-NetCore-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect/
[ServerLib-NetCore-Owin-Oidc-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oidc-Sample]: https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2
[ServerLib-NetCore-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OAuth/
[ServerLib-NetCore-Owin-Oauth-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oauth-Sample]:/
[ServerLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ServerLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad/
[ServerLib-Node-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-node-web/
