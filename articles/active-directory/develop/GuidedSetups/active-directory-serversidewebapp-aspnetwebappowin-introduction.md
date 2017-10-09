---
title: "aaaAzure AD v2 ASP.NET Web Server wprowadzenie — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Implementowanie logowania firmy Microsoft dla rozwiązania ASP.NET z aplikacji opartych na przeglądarce sieci web tradycyjnych przy użyciu standardowego protokołu OpenID Connect"
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a>Dodaj logowanie do aplikacji sieci web ASP.NET tooan firmy Microsoft

W tym przewodniku pokazano, jak tooimplement logowania z firmą Microsoft za pomocą rozwiązania ASP.NET MVC z tradycyjnego aplikacji sieci web opartej na przeglądarce przy użyciu protokołu OpenID Connect. 

Na końcu hello tego przewodnika aplikacja zostanie logowania może tooaccept ins osobiste konta (w tym outlook.com, live.com i inne), a także pracować i służbowych z firmy lub organizacji, która ma być zintegrowane z usługą Azure Active Directory. 

> W tym przewodniku wymaga programu Visual Studio 2015 Update 3 lub Visual Studio 2017 r.  Nie masz?  [Bezpłatnie pobrać Visual Studio 2017 r.](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>Jak działa w tym przewodniku

![Jak działa w tym przewodniku](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

W tym przewodniku opiera się na scenariuszu hello których przeglądarką uzyskuje dostęp do witryny sieci web ASP.NET, żądanie tooauthenticate użytkownika, klikając przycisk logowania. W tym scenariuszu większość strony sieci web hello hello pracy toorender występuje na powitania po stronie serwera.

## <a name="libraries"></a>Biblioteki

W tym przewodniku używa hello następujące biblioteki:

|Biblioteka|Opis|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|Oprogramowanie pośredniczące, umożliwiający OpenIdConnect toouse aplikacji uwierzytelniania|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|Oprogramowanie pośredniczące, umożliwiającą sesję użytkownika toomaintain dla aplikacji przy użyciu plików cookie|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|Umożliwia aplikacji OWIN toorun w usługach IIS za pomocą potoku żądania ASP.NET hello|

