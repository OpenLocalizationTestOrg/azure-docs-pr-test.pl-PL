---
title: "Przykłady kodu w usłudze Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Indeks usługi Azure Active Directory, przykłady kodu, uporządkowane według scenariusza."
services: active-directory
documentationcenter: dev-center-name
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: mbaldwin
ms.custom: aaddev
ms.openlocfilehash: 921ce08766cc6e29a6db2c4f38d216e6de11730f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-code-samples"></a>Przykłady kodu usługi Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Można użyć programu Microsoft Azure Active Directory (Azure AD) tooadd uwierzytelniania i autoryzacji tooyour aplikacji sieci web i interfejsów API sieci web. W tej sekcji łączy toosamples możesz które pokazują, jak jest wykonywane i wstawki kodu, których można użyć w aplikacji. Na stronie przykładowy kod hello, można znaleźć szczegółowe odczytu-mnie tematy ułatwiające wymagania, instalacji i konfiguracji. I kod hello komentarze toohelp zrozumieć hello sekcje krytyczne.

toounderstand hello podstawowy scenariusz dla każdego typu przykładowe Zobacz scenariusze uwierzytelniania dla usługi Azure AD.

Współtworzenia tooour przykłady z witryny GitHub: [Microsoft Azure Active Directory przykłady i dokumentacja](https://github.com/Azure-Samples?page=3&query=active-directory).

## <a name="web-browser-tooweb-application"></a>TooWeb przeglądarki sieci Web aplikacji
Pokaż te przykłady sposobu toowrite aplikacji sieci web, który kieruje hello toosign przeglądarki użytkownika w tooAzure AD.

| Język/Platform | Przykład | Opis |
| --- | --- | --- |
| C# / .NET |[Aplikacja sieci Web OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Użyj protokołu OpenID Connect (ASP.Net OpenID Connect OWIN oprogramowanie pośredniczące) użytkownikom tooauthenticate dzierżawa usługi Azure AD. |
| C# / .NET |[Aplikacja sieci Web wielodostępnej OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Wielodostępne .NET MVC aplikacji sieci web używającej protokołu OpenID Connect (ASP.Net OpenID Connect OWIN oprogramowanie pośredniczące) tooauthenticate użytkowników z wieloma dzierżawcami usługi Azure AD. |
| C# / .NET |[Aplikacja sieci Web WSFederation-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation) |Za pomocą protokołu WS-Federation (oprogramowanie pośredniczące OWIN WS-Federation ASP.Net) tooauthenticate użytkowników z dzierżawy usługi Azure AD. |

## <a name="single-page-application-spa"></a>Jednostronicowej aplikacji JEDNOSTRONICOWEJ
W tym przykładzie pokazano, jak toowrite aplikacji jednej strony chronione z usługą Azure AD.  

| Język/Platform | Przykład | Opis |
| --- | --- | --- |
| JavaScript, C# / .NET |[SinglePageApp DotNet](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) |Używana biblioteka ADAL dla aplikacji jednej strony JavaScript i Azure AD toosecure AngularJS na podstawie realizowana za pomocą programu ASP.NET web API zaplecza. |

## <a name="native-application-tooweb-api"></a>Natywny tooWeb aplikacji interfejsu API
Te przykłady pokazują, jak toobuild natywnego klienta aplikacji, które wywołania interfejsów API sieci web, które są zabezpieczone przez usługę Azure AD. Używają [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) i [OAuth 2.0 w usłudze Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Język/Platform | Przykład | Opis |
| --- | --- | --- |
| Javascript |[NativeClient-MultiTarget-Cordova](https://github.com/Azure-Samples/active-directory-cordova-multitarget) |Użyj hello ADAL wtyczki dla oprogramowania Apache Cordova toobuild aplikacji oprogramowania Apache Cordova, który wywołuje interfejs API sieci web i używa usługi Azure AD do uwierzytelniania. |
| C# / .NET |[NativeClient DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) |Aplikacji programu .NET WPF, która wywołuje interfejs API sieci web, która jest chroniona za pomocą usługi Azure AD. |
| C# / .NET |[NativeClient WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Aplikacji Sklepu Windows, która wywołuje interfejs API sieci web, który jest zabezpieczony z usługą Azure AD. |
| C# / .NET |[NativeClient-WebAPI wielodostępnej WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-webapi-multitenant-windows-store) |Wywoływanie składnika web API, który jest zabezpieczony z usługą Azure AD wielodostępne aplikację ze Sklepu Windows. |
| C# / .NET |[WebAPI-OnBehalfOf-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof) |Aplikacja native client aplikacją, która wymaga składnika web API, który pobiera token tooact imieniu hello pierwotnego użytkownika, a następnie używa hello tokenu toocall innego interfejsu API sieci web. |
| C# / .NET |[NativeClient WindowsPhone8.1](https://github.com/Azure-Samples/active-directory-dotnet-windowsphone-8.1) |Aplikacją ze Sklepu Windows dla Windows Phone 8.1, która wywołuje interfejs API sieci web, która jest chroniona przez usługę Azure AD. |
| ObjC |[NativeClient iOS](https://github.com/Azure-Samples/active-directory-ios) |Aplikacja systemu iOS, która wywołuje interfejs API sieci web, która wymaga usługi Azure AD do uwierzytelniania. |
| C# / .NET |[WebAPI-ManuallyValidateJwt-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation) |Aplikacja klientami, która zawiera logikę tooprocess tokenu JWT w składniku web API, zamiast używać oprogramowania pośredniczącego OWIN. |
| C# / Xamarin |[NativeClient-Xamarin-Android](https://github.com/Azure-Samples/active-directory-xamarin-android) |Xamarin, powiązanie toohello macierzystego usługi Azure AD Authentication Library (ADAL) dla hello biblioteki systemu Android. |
| C# / Xamarin |[NativeClient Xamarin systemu iOS](https://github.com/Azure-Samples/active-directory-xamarin-ios) |Xamarin powiązania toohello macierzystego usługi Azure AD Authentication Library (ADAL) dla systemu iOS. |
| C# / Xamarin |[NativeClient-MultiTarget-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-multitarget) |Projekt Xamarin, który jest przeznaczony dla platformy pięć i wywołuje interfejs API sieci web, która jest chroniona przez usługę Azure AD. |
| C# / .NET |[NativeClient bezobsługowe DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-headless) |Aplikacji natywnej, który przeprowadza uwierzytelnianie nieinteraktywne i wywołuje interfejs API sieci web, która jest chroniona przez usługę Azure AD. |

## <a name="web-application-tooweb-api"></a>TooWeb aplikacji sieci Web interfejsu API
Te przykłady kodu, jak używać Pokaż [OAuth 2.0 w usłudze Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) toobuild aplikacji sieci web, które wywołują interfejsów API sieci web, które są zabezpieczone przez usługę Azure AD.

| Język/Platform | Przykład | Opis |
| --- | --- | --- |
| C# / .NET |[Aplikacja sieci Web WebAPI-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-openidconnect) |Wywoływanie interfejsu API sieci web z uprawnieniami hello zalogowanego użytkownika. |
| C# / .NET |[Aplikacja sieci Web WebAPI-OAuth2-AppIdentity-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) |Wywołanie interfejsu API sieci web z aplikacji hello uprawnienia. |
| C# / .NET |[Aplikacja sieci Web WebAPI-OAuth2-tożsamości użytkownika Dotnet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity) |Dodaj autoryzacji z [OAuth 2.0 w usłudze Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooan istniejącą aplikację sieci web, może wywołać interfejs API sieci web. |
| JavaScript |[WebAPI Nodejs](https://github.com/Azure-Samples/active-directory-node-webapi) |Konfigurowanie usługi interfejsu API REST, który jest zintegrowany z usługą Azure AD dla interfejsu API ochrony. Zawiera serwer Node.js interfejs API sieci Web. |
| C# / .NET |[Aplikacja sieci Web WebAPI wielodostępnej OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-multitenant-openidconnect) |Wielodostępne MVC sieci web aplikacji, która używa protokołu OpenID Connect (ASP.Net OpenID Connect OWIN oprogramowanie pośredniczące) użytkownikom tooauthenticate dzierżawa usługi Azure AD. Używa hello tooinvoke kod autoryzacji interfejsu API programu Graph. |

## <a name="server-or-daemon-application-tooweb-api"></a>Serwer lub aplikacja demon tooWeb interfejsu API
Pokaż te przykłady kodu, jak toobuild demon lub serwera aplikacji który pobiera zasoby z interfejsu API sieci web przy użyciu [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) i [OAuth 2.0 w usłudze Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Język/Platform | Przykład | Opis |
| --- | --- | --- |
| C# / .NET |[Demon DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon) |Aplikacja konsolowa wywołuje interfejs API sieci web. poświadczenie klienta Hello jest hasłem. |
| C# / .NET |[Demon CertificateCredential-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) |Aplikacja konsolowa, która wywołuje interfejs API sieci web. poświadczenie klienta Hello jest certyfikat. |

## <a name="calling-azure-ad-graph-api"></a>Wywołanie interfejsu API programu Graph usługi Azure AD
Te przykładowe kodu pokazują, jak toobuild aplikacje, które wywołują hello Azure AD Graph API tooread i zapisuj dane katalogu.

| Język/Platform | Przykład | Opis |
| --- | --- | --- |
| Java |[Aplikacja sieci Web GraphAPI-Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web) |Aplikacji sieci web, która używa tooaccess interfejsu API programu Graph hello danych katalogu usługi Azure AD. |
| PHP |[Aplikacja sieci Web GraphAPI-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-web) |Aplikacji sieci web, która używa tooaccess interfejsu API programu Graph hello danych katalogu usługi Azure AD. |
| C# / .NET |[Aplikacja sieci Web GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Aplikacji sieci web, która używa tooaccess interfejsu API programu Graph hello danych katalogu usługi Azure AD. |
| C# / .NET |[ConsoleApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-console) |Ta aplikacja konsoli Pokazuje typowe odczytu i zapisu wywołania toohello interfejsu API programu Graph i przypisania licencji użytkownika tooexecute i zaktualizować łącza i miniatury zdjęcia użytkownika. |
| C# / .NET |[ConsoleApp-GraphAPI-DiffQuery-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-diffquery) |Aplikacja konsolowa, która używa zapytania różnicowej hello w tooget interfejsu API programu Graph hello okresowych zmian obiektów toouser w dzierżawie usługi Azure AD. |
| C# / .NET |[Aplikacja sieci Web GraphAPI-DirectoryExtensions-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-directoryextensions-web) |Aplikacji MVC używa interfejsu API programu Graph zapytania toogenerate schemat organizacyjny proste firmy. |
| PHP |[Aplikacja sieci Web GraphAPI-DirectoryExtensions-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-directoryextensions-web) |Aplikacja PHP, która wywołuje tooregister interfejsu API programu Graph hello rozszerzenie i następnie odczytu, aktualizacji i usuwania wartości w atrybucie rozszerzenia hello. |

## <a name="authorization"></a>Autoryzacja
Pokaż przykłady te kodu jak toouse Azure AD w celu autoryzacji.

| Język/Platform | Przykład | Opis |
| --- | --- | --- |
| C# / .NET |[Aplikacja sieci Web GroupClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-groupclaims) |Wykonaj kontroli dostępu opartej na rolach (RBAC) przy użyciu usługi Azure Active Directory oświadczenia grupy w aplikacji, która jest zintegrowany z usługą Azure AD. |
| C# / .NET |[Aplikacja sieci Web RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) |Wykonaj kontroli dostępu opartej na rolach (RBAC) przy użyciu ról aplikacji usługi Azure Active Directory w aplikacji, która jest zintegrowany z usługą Azure AD. |

## <a name="legacy-walkthroughs"></a>Wskazówki dotyczące starszej wersji
Te wskazówki używać technologii nieco starsze, ale nadal mogą być przydatne.

| Język/Platform | Przykład | Opis |
| --- | --- | --- |
| C# / .NET |[Autoryzacji opartej na rolach i na podstawie listy ACL w aplikacji Microsoft Azure AD](http://go.microsoft.com/fwlink/?LinkId=331694) |Wykonaj autoryzacji opartej na rolach (RBAC) i autoryzacji na podstawie listy ACL w aplikacji, która jest zintegrowany z usługą Azure AD. |
| C# / .NET |[AAL — usługa tooREST aplikacji Sklepu Windows — uwierzytelnianie](http://go.microsoft.com/fwlink/?LinkId=330605) |Użyj [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) (dawniej AAL) dla aplikacji Sklepu Windows tooa możliwości uwierzytelniania Sklepu Windows w wersji Beta tooadd użytkownika. |
| C# / .NET |[Uwierzytelnianie ADAL — usługa tooREST aplikacji natywnej — przy użyciu usługi AAD za pomocą okna dialogowego przeglądarki](http://go.microsoft.com/fwlink/?LinkId=259814) |Użyj [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) tooadd użytkownika uwierzytelniania możliwości tooa WPF klienta. |
| C# / .NET |[Uwierzytelnianie ADAL — usługa tooREST aplikacji natywnej — ACS za pomocą okna dialogowego przeglądarki](http://code.msdn.microsoft.com/AAL-Native-App-to-REST-de57f2cc) |Użyj [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) i [2.0 usługi kontroli dostępu (ACS)](http://msdn.microsoft.com/library/azure/hh147631.aspx) tooadd użytkownika uwierzytelniania możliwości tooa WPF klienta. |
| C# / .NET |[Biblioteka ADAL - tooServer serwera uwierzytelniania](http://go.microsoft.com/fwlink/?LinkId=259816) |Użyj [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md) toosecure wywołania usługi z serwera tooan proces po stronie usługi MVC4 sieci Web interfejsu API REST. |
| C# / .NET |[Dodawanie tooYour logowania aplikacji sieci Web przy użyciu usługi Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Skonfiguruj .NET aplikacji tooperform sieci web rejestracji jednokrotnej względem katalogu usługi Azure AD w organizacji. |
| C# / .NET |[Tworzenie aplikacji sieci Web z wieloma dzierżawcami za pomocą usługi Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Użyj usługi Azure AD tooadd toohello rejestracji jednokrotnej i możliwości dostępu do katalogu jeden toowork aplikacji .NET przez wiele organizacji. |
| JAVA |[Java przykładową aplikację Azure AD Graph API](http://go.microsoft.com/fwlink/?LinkId=263969) |Użyj hello interfejsu API programu Graph tooaccess katalogu danych z usługi Azure AD. |
| PHP |[PHP przykładową aplikację Azure AD Graph API](http://code.msdn.microsoft.com/PHP-Sample-App-For-Windows-228c6ddb) |Użyj hello interfejsu API programu Graph tooaccess katalogu danych z usługi Azure AD. |
| C# / .NET |[Przykładowa aplikacja dla usługi Azure AD Graph API](http://go.microsoft.com/fwlink/?LinkID=262648) |Użyj hello interfejsu API programu Graph tooaccess katalogu danych z usługi Azure AD. |
| C# / .NET |[Przykładowa aplikacja dla usługi Azure AD Graph różnicowej zapytania](http://go.microsoft.com/fwlink/?LinkId=275398) |Użyj zapytania różnicowej hello w obiektach tooget interfejsu API programu Graph hello toouser okresowych zmian w dzierżawie usługi Azure AD. |
| C# / .NET |[Przykładowa aplikacja dla integracji aplikacji w chmurze wielodostępne dla usługi Azure AD](http://go.microsoft.com/fwlink/?LinkId=275397) |Integracja aplikacji wielodostępnych do usługi Azure AD. |
| C# / .NET |[Zabezpieczanie aplikacji Sklepu Windows i usługi sieci Web REST przy użyciu usługi Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Utwórz zasób prosty interfejs API sieci web i aplikacji Sklepu Windows za pomocą usługi Azure AD i hello [Azure AD Authentication Library (ADAL)](active-directory-authentication-libraries.md). |
| C# / .NET |[Przy użyciu hello tooQuery interfejsu API programu Graph usługi Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Skonfiguruj program Microsoft .NET hello toouse aplikacji interfejsu API usługi Azure AD Graph tooaccess danych z katalogu dzierżawy usługi Azure AD. |

## <a name="see-also"></a>Zobacz też
##### <a name="other-resources"></a>Inne zasoby
[Przewodnik dewelopera usługi Azure Active Directory](active-directory-developers-guide.md)

[Azure AD Graph API koncepcyjne i odwołania](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Biblioteka pomocnik interfejsu API Graph usługi Azure AD](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
