---
title: "aaaAzure AD v2 JS SPA instrukcje konfiguracji — Instalator | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 19e15c6c8db8bea2975f30e7505af79ccad17e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-web-server-or-project"></a>Konfigurowanie serwera sieci web lub projektu

> Preferowane ten przykładowy projekt toodownload zamiast niego? 
> - [Pobierz hello projektu Visual Studio](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> lub
> - [Pobierz pliki projektu hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) serwera sieci web z lokalnych, takich jak Python
>
> A następnie przejdź toohello [kroku konfiguracji](#create-an-application-express) przykładowy kod hello tooconfigure przed jej wykonanie.

## <a name="prerequisites"></a>Wymagania wstępne
Serwer sieci web lokalnych, takich jak [Python http.server](https://www.python.org/downloads/), [serwera http](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), lub integracji usług IIS Express z [programu Visual Studio 2017](https://www.visualstudio.com/downloads/) jest wymagane toorun ten przewodnik instalacji. 

Instrukcje w tym przewodniku są oparte na Visual Studio 2017 r i Python, ale możesz wolnego toouse inne środowisko projektowe lub serwera sieci Web.

## <a name="create-your-project"></a>Tworzenie projektu 

> ### <a name="option-1-visual-studio"></a>Opcja 1: Visual Studio 
> Jeśli używasz programu Visual Studio i tworzenia nowego projektu, wykonaj kroki hello poniżej toocreate nowe rozwiązanie Visual Studio:
> 1.    W programie Visual Studio:`File` > `New` > `Project`
> 2.    W obszarze `Visual C#\Web`, wybierz pozycję`ASP.NET Web Application (.NET Framework)`
> 3.    Nazwa aplikacji, a następnie kliknij przycisk *OK*
> 4.    W obszarze `New ASP.NET Web Application`, wybierz pozycję`Empty`

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a>Opcja 2: Python / inne serwery w sieci web
> Upewnij się, że zainstalowano [Python](https://www.python.org/downloads/), należy wykonać poniższy krok hello:
> - Tworzenie toohost folderu aplikacji.


## <a name="create-your-single-page-applications-ui"></a>Tworzenie aplikacji jednej strony interfejsu użytkownika
1.  Utwórz *index.html* Twojego SPA JavaScript w pliku. Jeśli używasz programu Visual Studio, wybierz hello projektu (folder główny projekt), kliknij prawym przyciskiem myszy i wybierz: `Add`  >  `New Item`  >  `HTML page` i nadaj mu nazwę index.html
2.  Dodaj następujące strony kodowej tooyour hello:
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling hello page -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <title>JavaScript SPA Guided Setup</title>
</head>
<body style="margin: 40px">
    <button id="callGraphButton" type="button" class="btn btn-primary" onclick="callGraphApi()">Call Microsoft Graph API</button>
    <div id="errorMessage" class="text-danger"></div>
    <div class="hidden">
        <h3>Graph API Call Response</h3>
        <pre class="well" id="graphResponse"></pre>
    </div>
    <div class="hidden">
        <h3>Access Token</h3>
        <pre class="well" id="accessToken"></pre>
    </div>
    <div class="hidden">
        <h3>ID Token Claims</h3>
        <pre class="well" id="userInfo"></pre>
    </div>
    <button id="signOutButton" type="button" class="btn btn-primary hidden" onclick="signOut()">Sign out</button>

    <!-- This app uses cdn tooreference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- hello 'bluebird' and 'fetch' references below are required if you need toorun this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
