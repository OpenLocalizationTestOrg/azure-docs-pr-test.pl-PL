---
title: "Usługi Azure AD w wersji 2 JS SPA instrukcje konfiguracji — Instalator | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: fc9f88cc8d23abcfa8ea30e346192732b422ffa2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
## <a name="setting-up-your-web-server-or-project"></a><span data-ttu-id="7a185-103">Konfigurowanie serwera sieci web lub projektu</span><span class="sxs-lookup"><span data-stu-id="7a185-103">Setting up your web server or project</span></span>

> <span data-ttu-id="7a185-104">Preferowane jest zamiast tego Pobierz ten przykładowy projekt?</span><span class="sxs-lookup"><span data-stu-id="7a185-104">Prefer to download this sample's project instead?</span></span> 
> - [<span data-ttu-id="7a185-105">Pobieranie projektu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a185-105">Download the Visual Studio project</span></span>](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> <span data-ttu-id="7a185-106">lub</span><span class="sxs-lookup"><span data-stu-id="7a185-106">or</span></span>
> - <span data-ttu-id="7a185-107">[Pobierz pliki projektu](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) serwera sieci web z lokalnych, takich jak Python</span><span class="sxs-lookup"><span data-stu-id="7a185-107">[Download the project files](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) for a local web server, such as Python</span></span>
>
> <span data-ttu-id="7a185-108">A następnie przejdź do [kroku konfiguracji](#create-an-application-express) skonfigurowaniu przykładowy kod przed jej wykonanie.</span><span class="sxs-lookup"><span data-stu-id="7a185-108">And then  skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a185-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7a185-109">Prerequisites</span></span>
<span data-ttu-id="7a185-110">Serwer sieci web lokalnych, takich jak [Python http.server](https://www.python.org/downloads/), [serwera http](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), lub integracji usług IIS Express z [programu Visual Studio 2017](https://www.visualstudio.com/downloads/) jest wymagana do uruchamiania Instalatora z przewodnikiem.</span><span class="sxs-lookup"><span data-stu-id="7a185-110">A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required to run this guided setup.</span></span> 

<span data-ttu-id="7a185-111">Instrukcje w tym przewodniku są oparte na Visual Studio 2017 r i Python, ale możesz użyć dowolnego środowiska programowania lub serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7a185-111">Instructions in this guide are based on both Python and Visual Studio 2017, but feel free to use any other development environment or Web Server.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="7a185-112">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="7a185-112">Create your project</span></span> 

> ### <a name="option-1-visual-studio"></a><span data-ttu-id="7a185-113">Opcja 1: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a185-113">Option 1: Visual Studio</span></span> 
> <span data-ttu-id="7a185-114">Jeśli używasz programu Visual Studio i tworzenia nowego projektu, wykonaj poniższe kroki, aby utworzyć nowe rozwiązanie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="7a185-114">If you are using Visual Studio and are creating a new project, follow the steps below to create a new Visual Studio solution:</span></span>
> 1.    <span data-ttu-id="7a185-115">W programie Visual Studio:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="7a185-115">In Visual Studio:  `File` > `New` > `Project`</span></span>
> 2.    <span data-ttu-id="7a185-116">W obszarze `Visual C#\Web`, wybierz pozycję`ASP.NET Web Application (.NET Framework)`</span><span class="sxs-lookup"><span data-stu-id="7a185-116">Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`</span></span>
> 3.    <span data-ttu-id="7a185-117">Nazwa aplikacji, a następnie kliknij przycisk *OK*</span><span class="sxs-lookup"><span data-stu-id="7a185-117">Name your application and click *OK*</span></span>
> 4.    <span data-ttu-id="7a185-118">W obszarze `New ASP.NET Web Application`, wybierz pozycję`Empty`</span><span class="sxs-lookup"><span data-stu-id="7a185-118">Under `New ASP.NET Web Application`, select `Empty`</span></span>

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a><span data-ttu-id="7a185-119">Opcja 2: Python / inne serwery w sieci web</span><span class="sxs-lookup"><span data-stu-id="7a185-119">Option 2: Python/ other web servers</span></span>
> <span data-ttu-id="7a185-120">Upewnij się, że zainstalowano [Python](https://www.python.org/downloads/), wykonaj kroki opisane poniżej:</span><span class="sxs-lookup"><span data-stu-id="7a185-120">Make sure you have installed [Python](https://www.python.org/downloads/), then follow the step below:</span></span>
> - <span data-ttu-id="7a185-121">Utwórz folder na potrzeby hostowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a185-121">Create a folder to host your application.</span></span>


## <a name="create-your-single-page-applications-ui"></a><span data-ttu-id="7a185-122">Tworzenie aplikacji jednej strony interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="7a185-122">Create your single page application’s UI</span></span>
1.  <span data-ttu-id="7a185-123">Utwórz *index.html* Twojego SPA JavaScript w pliku.</span><span class="sxs-lookup"><span data-stu-id="7a185-123">Create an *index.html* file for your JavaScript SPA.</span></span> <span data-ttu-id="7a185-124">Jeśli używasz programu Visual Studio, wybierz projekt (folder główny projekt), kliknij prawym przyciskiem myszy i wybierz: `Add`  >  `New Item`  >  `HTML page` i nadaj mu nazwę index.html</span><span class="sxs-lookup"><span data-stu-id="7a185-124">If you are using Visual Studio, select the project (project root folder), right click and select: `Add` > `New Item` > `HTML page` and name it index.html</span></span>
2.  <span data-ttu-id="7a185-125">Dodaj następujący kod do strony:</span><span class="sxs-lookup"><span data-stu-id="7a185-125">Add the following code to your page:</span></span>
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling the page -->
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

    <!-- This app uses cdn to reference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- The 'bluebird' and 'fetch' references below are required if you need to run this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
