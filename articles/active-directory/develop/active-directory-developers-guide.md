---
title: "aaaAzure usługi Active Directory dla deweloperów | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie logowania się na konta służbowe Microsoft przy użyciu usługi Azure Active Directory."
services: active-directory
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5c872c89-ef04-4f4c-98de-bc0c7460c7c2
ms.service: active-directory
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4dbbea6c1e0b8a70c0c36ddd1caec5658130a003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-for-developers"></a>Usługa Azure Active Directory dla deweloperów
Azure Active Directory jest usługa tożsamości chmury, która umożliwia deweloperom toosecurely logowania każdy użytkownik z konta służbowego kopii przez firmę Microsoft.  w tym miejscu dokumentacji Hello pokazuje, jak tooadd usługi Azure AD obsługuje tooyour aplikacji przy użyciu branżowych standardowych protokołów uwierzytelniania, OAuth i OpenID Connect.

| | |
| --- | --- |
|[Podstawowe informacje o uwierzytelnianiu](active-directory-authentication-scenarios.md) | Wprowadzenie tooauthentication z usługą Azure AD |
|[Typy aplikacji](active-directory-authentication-scenarios.md#application-types-and-scenarios) | Omówienie scenariuszy uwierzytelniania hello obsługiwane przez usługę Azure AD |                                
                                                                              
## <a name="get-started"></a>Rozpoczęcie pracy
Te konfiguracje z przewodnikiem przeprowadzenie za pomocą naszych toosign biblioteki uwierzytelniania w usłudze Azure Active Directory użytkowników.

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![Aplikacje mobilne i klasyczne](./media/active-directory-developers-guide/NativeApp_Icon.png)<br />Aplikacje mobilne i klasyczne</center> | [Omówienie](active-directory-authentication-scenarios.md#native-application-to-web-api)<br /><br />[iOS](active-directory-devquickstarts-ios.md)<br /><br />[Android](active-directory-devquickstarts-android.md) | [.NET](active-directory-devquickstarts-dotnet.md)<br /><br />[Windows](active-directory-devquickstarts-windowsstore.md)<br /><br />[Xamarin](active-directory-devquickstarts-xamarin.md) | [Cordova](active-directory-devquickstarts-cordova.md)<br /><br />[OAuth 2.0](active-directory-protocols-oauth-code.md) |
| <center>![Aplikacje sieci Web](./media/active-directory-developers-guide/Web_app.png)<br />Aplikacje sieci Web</center> | [Omówienie](active-directory-authentication-scenarios.md#web-browser-to-web-application)<br /><br />[ASP.NET](active-directory-devquickstarts-webapp-dotnet.md)<br /><br />[Java](active-directory-devquickstarts-webapp-java.md) | [NodeJS](active-directory-devquickstarts-openidconnect-nodejs.md)<br /><br />[OpenID Connect 1.0](active-directory-protocols-openid-connect-code.md) |  |
| <center>![Aplikacje jednostronicowe](./media/active-directory-developers-guide/SPA.png)<br />Aplikacje jednostronicowe</center> | [Omówienie](active-directory-authentication-scenarios.md#single-page-application-spa)<br /><br />[AngularJS](active-directory-devquickstarts-angular.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) |  |  |
| <center>![Interfejsy API sieci Web](./media/active-directory-developers-guide/Web_API.png)<br />Interfejsy API sieci Web</center> | [Omówienie](active-directory-authentication-scenarios.md#web-application-to-web-api)<br /><br />[ASP.NET](active-directory-devquickstarts-webapi-dotnet.md)<br /><br />[NodeJS](active-directory-devquickstarts-webapi-nodejs.md) | &nbsp; |
| <center>![Usługa-usługa](./media/active-directory-developers-guide/Service_App.png)<br />Usługa-usługa</center> | [Omówienie](active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)<br /><br />[.NET](active-directory-code-samples.md#server-or-daemon-application-to-web-api)<br /><br />[Poświadczenia klienta OAuth 2.0](active-directory-protocols-oauth-service-to-service.md) |  |

## <a name="guides"></a>Przewodniki
Te artykuły poinformuj o tym, jak tooperform typowe zadania z usługą Azure Active Directory.

|                                                                           |  |
|---------------------------------------------------------------------------| --- |
|[Rejestrowanie aplikacji](active-directory-integrating-applications.md)           | Jak tooregister aplikacji w usłudze Azure AD |
|[Aplikacje z wieloma dzierżawami](active-directory-devhowto-multi-tenant-overview.md)    | Jak konta służbowego toosign w udostępnianych przez firmę Microsoft |
|[OAuth i OpenID Connect](active-directory-protocols-openid-connect-code.md)| W jaki sposób użytkownicy toosign i wywołania interfejsów API sieci web przy użyciu protokołów naszych nowoczesnego uwierzytelniania |
|[Więcej przewodników...](active-directory-developers-guide-index.md#guides)        |     |

## <a name="reference"></a>Dokumentacja
Te artykuły zawierają szczegółowe informacje o interfejsach API, komunikatach protokołów i terminach używanych w usłudze Azure Active Directory.

|                                                                                   | |
| ----------------------------------------------------------------------------------| --- |
| [Biblioteki uwierzytelniania (ADAL)](active-directory-authentication-libraries.md)   | Omówienie biblioteki hello & zestawów SDK dostarczane przez usługę Azure AD |
| [Przykłady kodu](active-directory-code-samples.md)                                  | Lista wszystkich przykładów kodu usługi Azure AD |
| [Słownik](active-directory-dev-glossary.md)                                      | Terminologia i definicje słów używanych w tej dokumentacji |
| [Więcej materiałów referencyjnych...](active-directory-developers-guide-index.md#reference)|     |

## <a name="help--support"></a>Pomoc i obsługa techniczna
Są to hello najlepsze miejsca tooget pomoc dotyczącą tworzenia w usłudze Azure Active Directory.

|  |  
|---|
|[Tagi `azure-active-directory` i `adal` w witrynie Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)      |
|[Opinia o usłudze Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)|
| [Wypróbuj usługę Microsoft Dev Chat (bezpłatnie przez ograniczony czas)](http://aka.ms/devchat) |

<br />

> [!NOTE]
> Jeśli potrzebujesz toosign w osobistego konta Microsoft, może być tooconsider przy użyciu hello [punktu końcowego v2.0 usługi Azure AD](active-directory-appmodel-v2-overview.md).  punktu końcowego v2.0 Hello Azure AD jest ujednolicenie hello osobistego konta Microsoft i konta służbowego firmy Microsoft (z usługi Azure AD) w systemie pojedynczego uwierzytelniania.
