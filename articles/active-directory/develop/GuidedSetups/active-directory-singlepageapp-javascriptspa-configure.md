---
title: "Usługi Azure AD w wersji 2 JS SPA instrukcje konfiguracji — Konfigurowanie | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: adff529bfdc40006666cc643d49a302d7f1d09ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
## <a name="register-your-application"></a><span data-ttu-id="df478-103">Rejestrowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="df478-103">Register your application</span></span>

<span data-ttu-id="df478-104">Istnieje wiele sposobów, aby utworzyć aplikację, wybierz jeden z nich:</span><span class="sxs-lookup"><span data-stu-id="df478-104">There are multiple ways to create an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="df478-105">Opcja 1: Rejestrowanie aplikacji (tryb Express)</span><span class="sxs-lookup"><span data-stu-id="df478-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="df478-106">Teraz musisz zarejestrować aplikację w *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="df478-106">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="df478-107">Zarejestrować aplikację za pośrednictwem [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="df478-107">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="df478-108">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="df478-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="df478-109">Upewnij się, opcja *instrukcje konfiguracji* zaznaczono</span><span class="sxs-lookup"><span data-stu-id="df478-109">Make sure the option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="df478-110">Postępuj zgodnie z instrukcjami, aby uzyskać identyfikator aplikacji i wklej go w kodzie</span><span class="sxs-lookup"><span data-stu-id="df478-110">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="df478-111">Opcja 2: Rejestrowanie aplikacji (Tryb zaawansowany)</span><span class="sxs-lookup"><span data-stu-id="df478-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="df478-112">Przejdź do [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/portal/register-app) do rejestrowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="df478-112">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="df478-113">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="df478-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="df478-114">Upewnij się, opcja *instrukcje konfiguracji* nie jest zaznaczone</span><span class="sxs-lookup"><span data-stu-id="df478-114">Make sure the option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="df478-115">Kliknij przycisk `Add Platform`, a następnie wybierz pozycję`Web`</span><span class="sxs-lookup"><span data-stu-id="df478-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="df478-116">Dodaj `Redirect URL` odpowiada adres URL aplikacji, oparty na serwerze sieci web.</span><span class="sxs-lookup"><span data-stu-id="df478-116">Add the `Redirect URL` that correspond to the application's URL based on your web server.</span></span> <span data-ttu-id="df478-117">Znajduje się w sekcjach poniżej instrukcje na temat set / uzyskać adres URL przekierowania w Visual Studio i języka Python.</span><span class="sxs-lookup"><span data-stu-id="df478-117">See the sections below for instructions on how to set/ obtain the redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="df478-118">Kliknij przycisk *Zapisz*</span><span class="sxs-lookup"><span data-stu-id="df478-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="df478-119">Visual Studio instrukcje pobrania adres URL przekierowania</span><span class="sxs-lookup"><span data-stu-id="df478-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="df478-120">Postępuj zgodnie z instrukcjami, aby uzyskać adres URL przekierowania:</span><span class="sxs-lookup"><span data-stu-id="df478-120">Follow the instructions to obtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="df478-121">W *Eksploratora rozwiązań*, wybierz projekt i przyjrzyj się `Properties` okna (Jeśli nie widzisz okna właściwości, naciśnij klawisz `F4`)</span><span class="sxs-lookup"><span data-stu-id="df478-121">In *Solution Explorer*, select the project and look at the `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="df478-122">Skopiuj wartości z `URL` do Schowka:</span><span class="sxs-lookup"><span data-stu-id="df478-122">Copy the value from `URL` to the clipboard:</span></span><br/> <span data-ttu-id="df478-123">![Właściwości projektu](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="df478-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="df478-124">Przywraca *portalu rejestracji aplikacji* i wkleić wartość jako `Redirect URL` i kliknij przycisk "Zapisz"</span><span class="sxs-lookup"><span data-stu-id="df478-124">Switch back to the *Application Registration Portal* and paste the value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="df478-125">Adres URL przekierowania ustawienie dla języka Python</span><span class="sxs-lookup"><span data-stu-id="df478-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="df478-126">Dla języka Python można ustawić sieci web port serwera przy użyciu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="df478-126">For Python, you can set the web server port via command line.</span></span> <span data-ttu-id="df478-127">Ten przewodnik instalacji korzysta z portu 8080 dla odwołania, ale działanie może używać innych dostępnych portów.</span><span class="sxs-lookup"><span data-stu-id="df478-127">This guided setup uses the port 8080 for reference but feel free to use any other port available.</span></span> <span data-ttu-id="df478-128">W każdym przypadku postępuj zgodnie z instrukcjami poniżej, aby zdefiniować adres URL przekierowania w aplikacji informacje rejestracyjne:</span><span class="sxs-lookup"><span data-stu-id="df478-128">In any case, follow the instructions below to set up a redirect URL in the application registration information:</span></span><br/>
> - <span data-ttu-id="df478-129">Przywraca *portalu rejestracji aplikacji* i ustaw `http://localhost:8080/` jako `Redirect URL`, lub użyj `http://localhost:[port]/` używania niestandardowego portu TCP (gdzie *[port]* jest niestandardowy port TCP Liczba) i kliknij przycisk "Zapisz"</span><span class="sxs-lookup"><span data-stu-id="df478-129">Switch back to the *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is the custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="df478-130">Skonfiguruj SPA skrypt JavaScript</span><span class="sxs-lookup"><span data-stu-id="df478-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="df478-131">Utwórz plik o nazwie `msalconfig.js` zawierający informacje o rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="df478-131">Create a file named `msalconfig.js` containing the application registration information.</span></span> <span data-ttu-id="df478-132">Jeśli używasz programu Visual Studio, wybierz projekt (folder główny projekt), kliknij prawym przyciskiem myszy i wybierz: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="df478-132">If you are using Visual Studio, select the project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="df478-133">Nadaj jej nazwę`msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="df478-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="df478-134">Dodaj następujący kod do Twojej `msalconfig.js` pliku:</span><span class="sxs-lookup"><span data-stu-id="df478-134">Add the following code to your `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="df478-135">Zastąp <code>Enter_the_Application_Id_here</code> wraz z identyfikatorem aplikacji został zarejestrowany</span><span class="sxs-lookup"><span data-stu-id="df478-135">Replace <code>Enter_the_Application_Id_here</code> with the Application Id you just registered</span></span>
</li>
</ol>
