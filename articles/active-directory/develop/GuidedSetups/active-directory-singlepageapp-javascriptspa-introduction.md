---
title: "aaaAzure AD v2 JS SPA instrukcje konfiguracji — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Jak aplikacje JavaScript SPA można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Wywołanie interfejsu API Graph usługi Microsoft hello z JavaScript jednej strony aplikacji JEDNOSTRONICOWEJ

W tym przewodniku pokazano, jak JavaScript jednej strony aplikacji JEDNOSTRONICOWEJ mógł zalogować się w osobistym, pracy i kont służbowych uzyskać token dostępu i wywołania interfejsu API Graph usługi Microsoft hello lub innych interfejsów API, które wymagają tokenów dostępu z hello punktu końcowego w wersji 2 usługi Azure Active Directory.

### <a name="how-this-guide-works"></a>Jak działa w tym przewodniku

![Jak działa hello przykładowej aplikacji wygenerowane przez ten przewodnik](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Więcej informacji

Witaj przykładowej aplikacji utworzonych przez ten przewodnik umożliwia hello tooquery JavaScript SPA interfejsu API programu Microsoft Graph lub interfejsu API sieci Web, który akceptuje tokeny od punktu końcowego w wersji 2 usługi Azure Active Directory. W tym scenariuszu po użytkownika logowania, token dostępu jest tooHTTP żądanego i dodać żądań za pośrednictwem hello nagłówek autoryzacji. Token nabycia i odnawiania są obsługiwane przez hello biblioteki uwierzytelniania firmy Microsoft (MSAL).

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Biblioteki

W tym przewodniku używa hello następujące biblioteki:

|Biblioteka|Opis|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Biblioteka uwierzytelniania firmy Microsoft dla podglądu JavaScript|

> [!NOTE]
> *msal.js* hello cele *punktu końcowego w wersji 2 usługi Azure Active Directory* — który umożliwia toosign konta osobiste, szkolnego i pracy w i uzyskać tokeny. Witaj *punktu końcowego w wersji 2 usługi Azure Active Directory* ma [pewne ograniczenia](..\active-directory-v2-limitations.md). Jeśli interesuje Cię tylko na kontach służbowych, jak i szkoły, użyj *adal.js* i hello *punktu końcowego V1*. toounderstand różnice między punktami końcowymi v1 i v2 hello odczytu hello [porównania v1 v2](..\active-directory-v2-compare.md).

<!--end-collapse-->
