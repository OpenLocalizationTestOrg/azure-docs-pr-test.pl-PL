---
title: "aaaAzure AD v2 Windows Desktop wprowadzenie — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Jak aplikacje .NET pulpitu systemu Windows (XAML) można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a>Wywołanie interfejsu API Graph usługi Microsoft hello z aplikacji pulpitu systemu Windows

W tym przewodniku pokazano, jak natywnych aplikacji .NET pulpitu systemu Windows (XAML) można uzyskać token dostępu i wywołania interfejsu API programu Graph firmy Microsoft lub innych interfejsów API, które wymagają tokenów dostępu z punktu końcowego w wersji 2 usługi Azure Active Directory.

Na końcu hello tego przewodnika, aplikacji będzie można toocall stanie interfejs API chronionych przy użyciu konta osobiste (w tym outlook.com, live.com i inne), a także pracy i kont służbowych z firmy lub organizacji, która ma usługę Azure Active Directory.  

> W tym przewodniku wymaga programu Visual Studio 2015 Update 3 lub Visual Studio 2017 r.  Nie masz? [Bezpłatnie pobrać Visual Studio 2017 r.](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a>Jak działa w tym przewodniku

![Jak działa w tym przewodniku](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

Witaj przykładowej aplikacji utworzonych przez ten przewodnik umożliwia tooquery Windows Desktop aplikacji interfejsu API programu Microsoft Graph lub interfejsu API sieci Web, który akceptuje tokeny od punktu końcowego w wersji 2 usługi Azure Active Directory. W tym scenariuszu token jest dodawana tooHTTP żądań za pośrednictwem hello nagłówek autoryzacji. Token nabycia i odnawiania jest obsługiwany przez hello biblioteki uwierzytelniania firmy Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Obsługa tokenów nabycia do uzyskiwania dostępu do chronionego interfejsów API sieci Web

Po uwierzytelniania użytkownika hello hello Przykładowa aplikacja odbiera token, który może być używane tooquery interfejsu API programu Microsoft Graph i interfejsu API sieci Web zabezpieczonych przez usługi Microsoft Azure Active Directory w wersji 2.

Interfejsy API, takich jak Microsoft Graph wymagają tooallow tokenu dostępu podczas uzyskiwania dostępu do określonych zasobów — na przykład tooread profilu użytkownika, dostęp do kalendarza użytkownika lub Wyślij wiadomość e-mail. Aplikacja może wysłać żądanie tokenu dostępu przy użyciu MSAL tooaccess tych zasobów za pośrednictwem interfejsu API zakresów. Ten token dostępu jest dodany toohello nagłówek autoryzacji HTTP dla każdego wywołania wykonane w stosunku hello chroniony zasób. 

MSAL zarządza buforowanie i odświeżanie tokenów dostępu, więc nie trzeba aplikacji.


### <a name="nuget-packages"></a>Pakiety NuGet

W tym przewodniku używa powitania po pakietów NuGet:

|Biblioteka|Opis|
|---|---|
|[Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client)|Biblioteka uwierzytelniania firmy Microsoft (MSAL)|

