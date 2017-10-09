---
title: "aaaAzure AD w wersji 2 dla systemu Android wprowadzenie — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Jak uzyskać token dostępu i wywołania interfejsu API programu Microsoft Graph lub interfejsów API, które wymagają tokenów dostępu z punktu końcowego w wersji 2 usługi Azure Active Directory aplikacji systemu Android"
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
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a>Wywołanie interfejsu API Graph usługi Microsoft hello z aplikacji systemu Android

W tym przewodniku pokazano, jak natywnych aplikacji systemu Android mogą pobrać token dostępu i wywołania interfejsu API programu Graph firmy Microsoft lub innych interfejsów API, które wymagają tokenów dostępu z punktu końcowego w wersji 2 usługi Azure Active Directory.

Na końcu hello tego przewodnika, aplikacji będzie można toocall stanie interfejs API chronionych przy użyciu konta osobiste (w tym outlook.com, live.com i inne), a także pracy i kont służbowych z firmy lub organizacji, która ma usługę Azure Active Directory.  

### <a name="how-this-sample-works"></a>Jak działa w tym przykładzie
![Jak działa w tym przykładzie](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

Przykładowe Hello utworzone przez ten przewodnik jest oparty na scenariusz, w przypadku aplikacji systemu Android używane tooquery interfejsu API sieci Web, który akceptuje tokeny od usługi Azure Active Directory v2 punktu końcowego — w takim przypadku interfejsu API programu Microsoft Graph. W tym scenariuszu token jest dodawana tooHTTP żądań za pośrednictwem hello nagłówek autoryzacji. Token nabycia i odnawiania jest obsługiwany przez hello biblioteki uwierzytelniania firmy Microsoft (MSAL).

### <a name="pre-requisites"></a>Wymagania wstępne
* Ten przewodnik instalacji koncentruje się na Android Studio, ale dopuszczalne jest również inne środowiska programowania aplikacji dla systemu Android. 
* Zestaw SDK systemu android 21 lub nowszy jest wymagany (zalecane 25 zestawu SDK).
* Google Chrome lub przeglądarki sieci web przy użyciu karty niestandardowy jest wymagany dla tej wersji programu Microsoft biblioteki uwierzytelniania (MSAL) dla systemu Android.

> Uwaga: Google Chrome nie jest uwzględniony w Visual Studio Emulator for Android. Zalecamy tootest ten kod na emulatorze z interfejsu API 25 lub obraz z interfejsu API 21 lub nowszego z Google Chrome zainstalował.


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a>Jak toohandle token tooaccess nabycia chronionego interfejsu API sieci Web

Po uwierzytelniania użytkownika hello hello Przykładowa aplikacja odbiera token, który może być używane tooquery interfejsu API programu Microsoft Graph i interfejsu API sieci Web zabezpieczonych przez usługi Microsoft Azure Active Directory w wersji 2.

Interfejsy API, takich jak Microsoft Graph wymagają tooallow tokenu dostępu podczas uzyskiwania dostępu do określonych zasobów — na przykład tooread profilu użytkownika, dostęp do kalendarza użytkownika lub Wyślij wiadomość e-mail. Aplikacja może wysłać żądanie tokenu dostępu przy użyciu MSAL tooaccess tych zasobów za pośrednictwem interfejsu API zakresów. Ten token dostępu jest dodany toohello nagłówek autoryzacji HTTP dla każdego wywołania wykonane w stosunku hello chroniony zasób. 

MSAL zarządza buforowanie i odświeżanie tokenów dostępu, więc nie trzeba aplikacji.

### <a name="libraries"></a>Biblioteki

W tym przewodniku używa hello następujące biblioteki:

|Biblioteka|Opis|
|---|---|
|[COM.microsoft.Identity.Client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|Biblioteka uwierzytelniania firmy Microsoft (MSAL)|
