---
title: "aaaAzure AD v2 JS SPA z przewodnikiem instalacji — konfigurowanie | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a><span data-ttu-id="a062b-103">Rejestrowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="a062b-103">Register your application</span></span>

<span data-ttu-id="a062b-104">Istnieje wiele sposobów toocreate aplikacji, wybierz jeden z nich:</span><span class="sxs-lookup"><span data-stu-id="a062b-104">There are multiple ways toocreate an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="a062b-105">Opcja 1: Rejestrowanie aplikacji (tryb Express)</span><span class="sxs-lookup"><span data-stu-id="a062b-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="a062b-106">Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="a062b-106">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="a062b-107">Zarejestrować aplikację za pośrednictwem hello [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="a062b-107">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="a062b-108">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="a062b-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="a062b-109">Upewnij się, że opcja powitania *instrukcje konfiguracji* zaznaczono</span><span class="sxs-lookup"><span data-stu-id="a062b-109">Make sure hello option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="a062b-110">Wykonaj identyfikator aplikacji hello hello instrukcje tooobtain i wklej go w kodzie</span><span class="sxs-lookup"><span data-stu-id="a062b-110">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="a062b-111">Opcja 2: Rejestrowanie aplikacji (Tryb zaawansowany)</span><span class="sxs-lookup"><span data-stu-id="a062b-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="a062b-112">Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister aplikacji</span><span class="sxs-lookup"><span data-stu-id="a062b-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="a062b-113">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="a062b-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="a062b-114">Upewnij się, że opcja powitania *instrukcje konfiguracji* nie jest zaznaczone</span><span class="sxs-lookup"><span data-stu-id="a062b-114">Make sure hello option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="a062b-115">Kliknij przycisk `Add Platform`, a następnie wybierz pozycję`Web`</span><span class="sxs-lookup"><span data-stu-id="a062b-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="a062b-116">Dodaj hello `Redirect URL` odnoszą się adres URL aplikacji toohello oparte na serwerze sieci web.</span><span class="sxs-lookup"><span data-stu-id="a062b-116">Add hello `Redirect URL` that correspond toohello application's URL based on your web server.</span></span> <span data-ttu-id="a062b-117">Zobacz hello sekcjach poniżej, aby uzyskać instrukcje na temat tooset / uzyskać adres URL przekierowania hello w Visual Studio i języka Python.</span><span class="sxs-lookup"><span data-stu-id="a062b-117">See hello sections below for instructions on how tooset/ obtain hello redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="a062b-118">Kliknij przycisk *Zapisz*</span><span class="sxs-lookup"><span data-stu-id="a062b-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="a062b-119">Visual Studio instrukcje pobrania adres URL przekierowania</span><span class="sxs-lookup"><span data-stu-id="a062b-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="a062b-120">Wykonaj adres URL przekierowania tooobtain instrukcje hello:</span><span class="sxs-lookup"><span data-stu-id="a062b-120">Follow hello instructions tooobtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="a062b-121">W *Eksploratora rozwiązań*, wybierz projekt hello i przyjrzyj się hello `Properties` okna (Jeśli nie widzisz okna właściwości, naciśnij klawisz `F4`)</span><span class="sxs-lookup"><span data-stu-id="a062b-121">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="a062b-122">Skopiuj wartość hello z `URL` toohello Schowka:</span><span class="sxs-lookup"><span data-stu-id="a062b-122">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="a062b-123">![Właściwości projektu](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="a062b-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="a062b-124">Przełącz wstecz toohello *portalu rejestracji aplikacji* i wkleić wartość hello jako `Redirect URL` i kliknij przycisk "Zapisz"</span><span class="sxs-lookup"><span data-stu-id="a062b-124">Switch back toohello *Application Registration Portal* and paste hello value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="a062b-125">Adres URL przekierowania ustawienie dla języka Python</span><span class="sxs-lookup"><span data-stu-id="a062b-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="a062b-126">Dla języka Python możesz ustawić hello port serwera sieci web przy użyciu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a062b-126">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="a062b-127">Ten przewodnik instalacji używa hello portu 8080 dla odwołania, ale możesz wolnego toouse innych dostępnych portów.</span><span class="sxs-lookup"><span data-stu-id="a062b-127">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="a062b-128">W każdym przypadku wykonaj instrukcje hello poniżej tooset się adres URL przekierowania w informacji o rejestracji aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="a062b-128">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> - <span data-ttu-id="a062b-129">Przełącz wstecz toohello *portalu rejestracji aplikacji* i ustaw `http://localhost:8080/` jako `Redirect URL`, lub użyj `http://localhost:[port]/` używania niestandardowego portu TCP (gdzie *[port]* jest hello niestandardowy port TCP Liczba) i kliknij przycisk "Zapisz"</span><span class="sxs-lookup"><span data-stu-id="a062b-129">Switch back toohello *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="a062b-130">Skonfiguruj SPA skrypt JavaScript</span><span class="sxs-lookup"><span data-stu-id="a062b-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="a062b-131">Utwórz plik o nazwie `msalconfig.js` zawierający informacje o rejestracji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a062b-131">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="a062b-132">Jeśli używasz programu Visual Studio, wybierz hello projektu (folder główny projekt), kliknij prawym przyciskiem myszy i wybierz: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="a062b-132">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="a062b-133">Nadaj jej nazwę`msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="a062b-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="a062b-134">Dodaj hello następującego kodu tooyour `msalconfig.js` pliku:</span><span class="sxs-lookup"><span data-stu-id="a062b-134">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="a062b-135">Zastąp <code>Enter_the_Application_Id_here</code> z hello został zarejestrowany identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="a062b-135">Replace <code>Enter_the_Application_Id_here</code> with hello Application Id you just registered</span></span>
</li>
</ol>
