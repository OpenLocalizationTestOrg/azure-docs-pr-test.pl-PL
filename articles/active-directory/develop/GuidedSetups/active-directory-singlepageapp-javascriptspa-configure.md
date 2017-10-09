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
## <a name="register-your-application"></a>Rejestrowanie aplikacji

Istnieje wiele sposobów toocreate aplikacji, wybierz jeden z nich:

### <a name="option-1-register-your-application-express-mode"></a>Opcja 1: Rejestrowanie aplikacji (tryb Express)
Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:

1.  Zarejestrować aplikację za pośrednictwem hello [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)
2.  Wprowadź nazwę aplikacji i poczty e-mail
3.  Upewnij się, że opcja powitania *instrukcje konfiguracji* zaznaczono
4.  Wykonaj identyfikator aplikacji hello hello instrukcje tooobtain i wklej go w kodzie

### <a name="option-2-register-your-application-advanced-mode"></a>Opcja 2: Rejestrowanie aplikacji (Tryb zaawansowany)

1. Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister aplikacji
2. Wprowadź nazwę aplikacji i poczty e-mail 
3. Upewnij się, że opcja powitania *instrukcje konfiguracji* nie jest zaznaczone
4.  Kliknij przycisk `Add Platform`, a następnie wybierz pozycję`Web`
5. Dodaj hello `Redirect URL` odnoszą się adres URL aplikacji toohello oparte na serwerze sieci web. Zobacz hello sekcjach poniżej, aby uzyskać instrukcje na temat tooset / uzyskać adres URL przekierowania hello w Visual Studio i języka Python.
6. Kliknij przycisk *Zapisz*

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Visual Studio instrukcje pobrania adres URL przekierowania
> Wykonaj adres URL przekierowania tooobtain instrukcje hello:
> 1.    W *Eksploratora rozwiązań*, wybierz projekt hello i przyjrzyj się hello `Properties` okna (Jeśli nie widzisz okna właściwości, naciśnij klawisz `F4`)
> 2.    Skopiuj wartość hello z `URL` toohello Schowka:<br/> ![Właściwości projektu](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Przełącz wstecz toohello *portalu rejestracji aplikacji* i wkleić wartość hello jako `Redirect URL` i kliknij przycisk "Zapisz"

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Adres URL przekierowania ustawienie dla języka Python
> Dla języka Python możesz ustawić hello port serwera sieci web przy użyciu wiersza polecenia. Ten przewodnik instalacji używa hello portu 8080 dla odwołania, ale możesz wolnego toouse innych dostępnych portów. W każdym przypadku wykonaj instrukcje hello poniżej tooset się adres URL przekierowania w informacji o rejestracji aplikacji hello:<br/>
> - Przełącz wstecz toohello *portalu rejestracji aplikacji* i ustaw `http://localhost:8080/` jako `Redirect URL`, lub użyj `http://localhost:[port]/` używania niestandardowego portu TCP (gdzie *[port]* jest hello niestandardowy port TCP Liczba) i kliknij przycisk "Zapisz"


#### <a name="configure-your-javascript-spa"></a>Skonfiguruj SPA skrypt JavaScript

1.  Utwórz plik o nazwie `msalconfig.js` zawierający informacje o rejestracji aplikacji hello. Jeśli używasz programu Visual Studio, wybierz hello projektu (folder główny projekt), kliknij prawym przyciskiem myszy i wybierz: `Add`  >  `New Item`  >  `JavaScript File`. Nadaj jej nazwę`msalconfig.js`
2.  Dodaj hello następującego kodu tooyour `msalconfig.js` pliku:

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
Zastąp <code>Enter_the_Application_Id_here</code> z hello został zarejestrowany identyfikator aplikacji
</li>
</ol>
