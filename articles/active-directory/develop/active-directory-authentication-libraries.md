---
title: "aaaAzure bibliotek uwierzytelniania usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Hello Azure AD Authentication Library (ADAL) klienta aplikacji umożliwia deweloperom stosowanie tooeasily uwierzytelniania użytkowników toocloud lub lokalnej usługi Active Directory (AD) i uzyskać tokeny dostępu dla zabezpieczanie interfejsu API."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: mbaldwin
ms.assetid: 2e4fc79a-0285-40be-8c77-65edee408a22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 20fae18807ef03463ab1bc218e5f3548b5bd5717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-authentication-libraries"></a>Biblioteki uwierzytelniania usługi Azure Active Directory
Hello interfejsów Azure Active Directory Authentication Library (ADAL) umożliwia klienta aplikacji deweloperzy tooeasily uwierzytelniania użytkowników toocloud lub lokalnej usługi Active Directory (AD) i uzyskanie tokenów dostępu do zabezpieczania wywołań interfejsu API. Biblioteka ADAL ułatwia uwierzytelniania dla deweloperów przy użyciu funkcji takich jak:
 - Obsługa dla wywołań metod asynchronicznych
 - można skonfigurować pamięć podręczną tokenów czy magazyny tokenów dostępu i tokenów odświeżania
 - automatyczne odświeżanie tokenu po wygaśnięciu tokenu dostępu i token odświeżania jest dostępny
 - itp.
 
Dzięki obsłudze większość hello złożoności, ADAL ułatwia deweloperom fokus na logice biznesowej i łatwo zabezpieczenia zasobów, bez konieczności eksperta w zabezpieczeń.

Biblioteka ADAL jest dostępna na różnych platformach.

### <a name="client-libraries"></a>Biblioteki klienckie

| Platforma | Biblioteka | Do pobrania | Kod źródłowy | Przykład | Dokumentacja
| --- | --- | --- | --- | --- | --- |
| Klient .NET, Sklep Windows, platformy uniwersalnej systemu Windows, Xamarin iOS i Android |MSAL dla platformy .NET (wersja zapoznawcza) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client/1.1.0-preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Aplikacja klasyczna](~/articles/active-directory/develop/guidedsetups/active-directory-windesktop.md) |[Dokumentacja](https://docs.microsoft.com/dotnet/api/?view=identityclient-1.1.0-preview) | 
| JavaScript |MSAL dla języka JavaScript (wersja zapoznawcza) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Jednej strony aplikacji](~/articles/active-directory/develop/GuidedSetups/active-directory-javascriptspa.md) | [Dokumentacja](https://htmlpreview.github.io/?https://raw.githubusercontent.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/docs/classes/_useragentapplication_.msal.useragentapplication.html) | 
| iOS |MSAL dla systemu iOS (wersja zapoznawcza) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [Aplikacja systemu iOS](~/articles/active-directory/develop/GuidedSetups/active-directory-ios.md) | [Dokumentacja](https://azuread.github.io/docs/objc/) |
| Android |MSAL dla systemu Android (wersja zapoznawcza) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Aplikacji systemu android](~/articles/active-directory/develop/GuidedSetups/active-directory-android.md) | [Dokumentacja](http://javadoc.io/doc/com.microsoft.identity.client/msal/0.1.1) |
| Klient .NET, Sklep Windows, platformy uniwersalnej systemu Windows, Xamarin iOS i Android |ADAL .NET w wersji 3 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet) | [Aplikacja klasyczna](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-dotnet) |[Dokumentacja](https://docs.microsoft.com/dotnet/api/?view=identitymodelclientsad-3.13.9) | 
| .NET klienta, Sklep Windows, Windows Phone 8.1 |ADAL .NET w wersji 2 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/2.28.4) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/releases/tag/v2.28.4) | [Aplikacja klasyczna](https://github.com/AzureADQuickStarts/NativeClient-DotNet/releases/tag/v2.X) | | 
| JavaScript |ADAL.js |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[Jednej strony aplikacji](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) | |
| systemy iOS, system macOS |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc/releases) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc) |[Aplikacja systemu iOS](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-ios) | [Dokumentacja](https://cocoapods.org/pods/ADAL)|
| Android |ADAL |[Witaj centralnym repozytorium](http://search.maven.org/remotecontent?filepath=com/microsoft/aad/adal/) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android) |[Aplikacji systemu android](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-android) | [JavaDocs](http://javadoc.io/doc/com.microsoft.aad/adal/)|
| Node.js |ADAL |[npm](https://www.npmjs.com/package/adal-node) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) | | |
| Java |ADAL4J |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[Aplikacje sieci Web w języku Java](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-java) | |
| Python |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) | | |
### <a name="server-libraries"></a>Serwer biblioteki 

| Platforma | Biblioteka | Do pobrania | Kod źródłowy | Przykład | Dokumentacja
| --- | --- | --- | --- | --- | --- |
| .NET |OWIN dla AzureAD|[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[Witrynie CodePlex](http://katanaproject.codeplex.com) |[Aplikacji MVC](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-dotnet) | |
| .NET |OWIN dla OpenIDConnect |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[Witrynie CodePlex](http://katanaproject.codeplex.com) |[Aplikacja sieci Web](https://github.com/AzureADSamples/WebApp-OpenIDConnect-DotNet) | |
| Node.js |Azure AD usługi Passport. |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Interfejs API sieci Web](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapi-nodejs)| |
| .NET |OWIN dla protokołu WS-Federation |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) |[Witrynie CodePlex](http://katanaproject.codeplex.com) |[Aplikacja sieci Web MVC](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) | |
| .NET |Rozszerzenia protokołu tożsamości dla platformy .NET 4.5 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Protocol.Extensions) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET |Program obsługi tokenów JWT dla platformy .NET 4.5 |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |



## <a name="scenarios"></a>Scenariusze

Poniżej przedstawiono trzy typowe scenariusze, w których ADAL może służyć do uwierzytelniania klienta, który uzyskuje dostęp do zasobu zdalnego:  

### <a name="authenticating-users-of-a-native-client-application-running-on-a-device"></a>Uwierzytelnianie użytkowników aplikację native client, uruchamianie na urządzeniu 

W tym scenariuszu projektant ma WPF aplikacji klienckiej, wymagającym tooaccess zasób zdalny zabezpieczone przez usługę Azure AD, takie jak interfejsu API sieci web. ADAM ma subskrypcji platformy Azure, wie jak tooinvoke hello podrzędne interfejsu API sieci web i zna hello Azure AD dzierżawy, który hello używa interfejsu API sieci web. W związku z tym on można uwierzytelnianie ADAL toofacilitate z usługą Azure AD przez pełni delegowanie tooADAL obsługi uwierzytelniania hello albo przez jawną obsługę poświadczeń użytkownika. Biblioteka ADAL umożliwia łatwe tooauthenticate hello użytkownika, Uzyskaj token dostępu i token odświeżania z usługi Azure AD, a następnie użyć dostępu hello tokenu toomake toohello żądań sieci web interfejsu API.

Aby uzyskać przykładowy kod, który demonstruje ten scenariusz przy użyciu uwierzytelniania tooAzure AD, zobacz [tooWeb natywnych aplikacji WPF klienta interfejsu API](https://github.com/azureadsamples/nativeclient-dotnet).

### <a name="authenticating-a-confidential-client-application-running-on-a-web-server"></a>Uwierzytelniania aplikacji klienckiej poufne uruchomiony na serwerze sieci web

W tym scenariuszu projektant ma aplikacji uruchomionej na serwerze, który wymaga tooaccess zasób zdalny zabezpieczone przez usługę Azure AD, takie jak interfejsu API sieci web. On ma subskrypcji platformy Azure, wie jak tooinvoke hello podrzędne usługi i wie, że używa hello Azure AD dzierżawy hello interfejsu API sieci web. W związku z tym on użyć uwierzytelniania ADAL toofacilitate z usługą Azure AD przez jawną obsługę aplikacji hello poświadczenia. Biblioteka ADAL umożliwia łatwe tooretrieve token z usługi Azure AD przy użyciu poświadczeń klienta aplikacji hello, a następnie użyj tego tokenu toomake żądań toohello interfejsu API sieci web. ADAL również dojść Zarządzanie okresem istnienia hello hello tokenu dostępu, buforowanie ich i odnawianie go odpowiednio do potrzeb. Aby uzyskać przykładowy kod, który demonstruje tego scenariusza, zobacz [tooWeb aplikacji konsoli demon interfejsu API](https://github.com/AzureADSamples/Daemon-DotNet).

### <a name="authenticating-a-confidential-client-application-running-on-a-server-on-behalf-of-a-user"></a>Uwierzytelniania aplikacji klienckiej poufne uruchomiony na serwerze, w imieniu użytkownika 

W tym scenariuszu projektant ma aplikacji uruchomionej na serwerze, który wymaga tooaccess zasób zdalny zabezpieczone przez usługę Azure AD, takie jak interfejsu API sieci web. Żądanie hello musi również toobe wprowadzone w imieniu użytkownika usługi Azure AD. On ma subskrypcji platformy Azure, wie jak tooinvoke hello podrzędne interfejsu API sieci web i wie, że używa hello usługi hello dzierżawy usługi Azure AD. Witaj użytkownik jest uwierzytelniony toohello aplikacji sieci web, aplikacji hello może pobrać kod autoryzacji dla użytkownika hello z usługi Azure AD. Witaj aplikacji sieci web może następnie używać ADAL tooobtain token dostępu i token odświeżania w imieniu użytkownika za pomocą hello kodu i klienta poświadczenia autoryzacji skojarzoną z aplikacją hello z usługi Azure AD. Po hello aplikacji sieci web znajduje się w posiadaniu hello tokenu dostępu, do momentu wygaśnięcia tokenu hello może wywołać interfejs API sieci web hello. Po wygaśnięciu tokenu hello hello aplikacji sieci web można użyć ADAL tooget nowy token dostępu przy użyciu tokenu odświeżania hello, która wcześniej została odebrana. Aby uzyskać przykładowy kod, który demonstruje tego scenariusza, zobacz [tooWeb tooWeb interfejsu API klienta natywnego interfejsu API](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof).

## <a name="see-also"></a>Zobacz też

- [Witaj przewodnik dewelopera usługi Azure Active Directory](active-directory-developers-guide.md)
- [Scenariusze uwierzytelniania dla usługi Azure Active directory](active-directory-authentication-scenarios.md)
- [Przykłady kodu w usłudze Azure Active Directory](active-directory-code-samples.md)
