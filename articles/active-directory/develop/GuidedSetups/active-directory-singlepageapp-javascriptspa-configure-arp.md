---
title: "aaaAzure AD v2 JS SPA instrukcje konfiguracji — Konfigurowanie (ARP) | Dokumentacja firmy Microsoft"
description: "Jak aplikacje JavaScript SPA można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy usługi Azure Active Directory w wersji 2 (ARP)"
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
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="956f8-103">Dodawanie aplikacji hello rejestracji informacji tooyour aplikacji</span><span class="sxs-lookup"><span data-stu-id="956f8-103">Add hello application’s registration information tooyour App</span></span>

<span data-ttu-id="956f8-104">W tym kroku należy adres URL przekierowania hello tooconfigure informacji rejestracyjnych aplikacji, a następnie dodaj hello identyfikator aplikacji tooyour JavaScript SPA aplikacji.</span><span class="sxs-lookup"><span data-stu-id="956f8-104">In this step, you need tooconfigure hello Redirect URL of your application registration information and then add hello Application Id tooyour JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="956f8-105">Skonfiguruj adres URL przekierowania</span><span class="sxs-lookup"><span data-stu-id="956f8-105">Configure redirect URL</span></span>

<span data-ttu-id="956f8-106">Skonfiguruj hello `Redirect URL` pola powyżej z adresem URL hello strony index.html oparte na serwerze sieci web, a następnie kliknij przycisk *aktualizacji*.</span><span class="sxs-lookup"><span data-stu-id="956f8-106">Configure hello `Redirect URL` field above with hello URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="956f8-107">Visual Studio instrukcje pobrania adres URL przekierowania</span><span class="sxs-lookup"><span data-stu-id="956f8-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="956f8-108">tooobtain adres URL przekierowania, wykonaj poniższe instrukcje hello:</span><span class="sxs-lookup"><span data-stu-id="956f8-108">tooobtain your redirect URL, follow hello instructions below:</span></span>
> 1.    <span data-ttu-id="956f8-109">W *Eksploratora rozwiązań*, wybierz projekt hello i przyjrzyj się hello `Properties` okna (Jeśli nie widzisz okna właściwości, naciśnij klawisz `F4`)</span><span class="sxs-lookup"><span data-stu-id="956f8-109">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="956f8-110">Skopiuj wartość hello z `URL` toohello Schowka:</span><span class="sxs-lookup"><span data-stu-id="956f8-110">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="956f8-111">![Właściwości projektu](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="956f8-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="956f8-112">Wklej wartość hello jako `Redirect URL` na powitania początku tej strony, następnie kliknij przycisk`Update`</span><span class="sxs-lookup"><span data-stu-id="956f8-112">Paste hello value as a `Redirect URL` on hello top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="956f8-113">Adres URL przekierowania ustawienie dla języka Python</span><span class="sxs-lookup"><span data-stu-id="956f8-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="956f8-114">Dla języka Python możesz ustawić hello port serwera sieci web przy użyciu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="956f8-114">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="956f8-115">Ten przewodnik instalacji używa hello portu 8080 dla odwołania, ale możesz wolnego toouse innych dostępnych portów.</span><span class="sxs-lookup"><span data-stu-id="956f8-115">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="956f8-116">W każdym przypadku wykonaj instrukcje hello poniżej tooset się adres URL przekierowania w informacji o rejestracji aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="956f8-116">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> <span data-ttu-id="956f8-117">Ustaw `http://localhost:8080/` jako `Redirect URL` na początku tej strony hello, lub użyj `http://localhost:[port]/` używania niestandardowego portu TCP (gdzie *[port]* hello niestandardowy numer portu TCP), a następnie kliknij przycisk "Aktualizuj"</span><span class="sxs-lookup"><span data-stu-id="956f8-117">Set `http://localhost:8080/` as a `Redirect URL` on hello top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="956f8-118">Konfigurowanie aplikacji JEDNOSTRONICOWEJ JavaScript</span><span class="sxs-lookup"><span data-stu-id="956f8-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="956f8-119">Utwórz plik o nazwie `msalconfig.js` zawierający informacje o rejestracji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="956f8-119">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="956f8-120">Jeśli używasz programu Visual Studio, wybierz hello projektu (folder główny projekt), kliknij prawym przyciskiem myszy i wybierz: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="956f8-120">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="956f8-121">Nadaj jej nazwę`msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="956f8-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="956f8-122">Dodaj hello następującego kodu tooyour `msalconfig.js` pliku:</span><span class="sxs-lookup"><span data-stu-id="956f8-122">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
