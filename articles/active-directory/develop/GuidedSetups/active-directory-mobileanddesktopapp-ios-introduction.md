---
title: "iOS v2 aaaAzure AD Getting Started — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Jak aplikacje systemu iOS (Swift) można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a>Wywołanie interfejsu API Graph usługi Microsoft hello z aplikacji systemu iOS

W tym przewodniku pokazano, jak aplikacji natywnej dla systemu iOS (Swift) można Uzyskaj token dostępu i wywołać hello interfejsu API programu Graph firmy Microsoft lub innych interfejsów API, które wymagają tokenów dostępu z punktu końcowego w wersji 2 usługi Azure Active Directory.

Na końcu hello tego przewodnika, aplikacji będzie można toocall stanie interfejs API chronionych przy użyciu konta osobiste (w tym outlook.com, live.com i inne), a także pracy i kont służbowych z firmy lub organizacji, która ma usługę Azure Active Directory.

> ### <a name="pre-requisites"></a>Wymagania wstępne
> - XCode 8.x jest wymagane dla tego przewodnika. Możesz pobrać XCode [w tym miejscu](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "adresu URL pobierania w środowisku XCode").
> - [Carthage](https://github.com/Carthage/Carthage) dla pakietu administracyjnego

### <a name="how-this-guide-works"></a>Jak działa w tym przewodniku

![Jak działa w tym przewodniku](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

Witaj przykładowej aplikacji utworzonych przez ten przewodnik umożliwia hello tooquery aplikacji systemu iOS interfejsu API programu Microsoft Graph lub interfejsu API sieci Web, który akceptuje tokeny od punktu końcowego w wersji 2 usługi Azure Active Directory. W tym scenariuszu token jest dodawana tooHTTP żądań za pośrednictwem hello nagłówek autoryzacji. Token nabycia i odnawiania jest obsługiwany przez hello biblioteki uwierzytelniania firmy Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Obsługa tokenów nabycia do uzyskiwania dostępu do chronionego interfejsów API sieci Web

Po uwierzytelniania użytkownika hello hello Przykładowa aplikacja odbiera token, który może być używane tooquery hello interfejsu API programu Microsoft Graph lub interfejsu API sieci Web zabezpieczonych przez usługi Microsoft Azure Active Directory w wersji 2.

Interfejsy API, takich jak Microsoft Graph wymagają tooallow tokenu dostępu podczas uzyskiwania dostępu do określonych zasobów — na przykład tooread profilu użytkownika, dostęp do kalendarza użytkownika lub Wyślij wiadomość e-mail. Aplikacja może wysłać żądanie tokenu dostępu przy użyciu MSAL za pośrednictwem interfejsu API zakresów. Ten token dostępu jest dodany toohello nagłówek autoryzacji HTTP dla każdego wywołania wykonane w stosunku hello chroniony zasób.

MSAL zarządza buforowanie i odświeżanie tokenów dostępu, więc nie trzeba aplikacji.


### <a name="nuget-packages"></a>Pakiety NuGet

W tym przewodniku używa powitania po pakietów NuGet:

|Biblioteka|Opis|
|---|---|
|[MSAL.framework](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|Podgląd biblioteki uwierzytelniania firmy Microsoft dla systemu iOS|

