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
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Dodawanie aplikacji hello rejestracji informacji tooyour aplikacji

W tym kroku należy adres URL przekierowania hello tooconfigure informacji rejestracyjnych aplikacji, a następnie dodaj hello identyfikator aplikacji tooyour JavaScript SPA aplikacji.

### <a name="configure-redirect-url"></a>Skonfiguruj adres URL przekierowania

Skonfiguruj hello `Redirect URL` pola powyżej z adresem URL hello strony index.html oparte na serwerze sieci web, a następnie kliknij przycisk *aktualizacji*.


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Visual Studio instrukcje pobrania adres URL przekierowania
> tooobtain adres URL przekierowania, wykonaj poniższe instrukcje hello:
> 1.    W *Eksploratora rozwiązań*, wybierz projekt hello i przyjrzyj się hello `Properties` okna (Jeśli nie widzisz okna właściwości, naciśnij klawisz `F4`)
> 2.    Skopiuj wartość hello z `URL` toohello Schowka:<br/> ![Właściwości projektu](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Wklej wartość hello jako `Redirect URL` na powitania początku tej strony, następnie kliknij przycisk`Update`

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Adres URL przekierowania ustawienie dla języka Python
> Dla języka Python możesz ustawić hello port serwera sieci web przy użyciu wiersza polecenia. Ten przewodnik instalacji używa hello portu 8080 dla odwołania, ale możesz wolnego toouse innych dostępnych portów. W każdym przypadku wykonaj instrukcje hello poniżej tooset się adres URL przekierowania w informacji o rejestracji aplikacji hello:<br/>
> Ustaw `http://localhost:8080/` jako `Redirect URL` na początku tej strony hello, lub użyj `http://localhost:[port]/` używania niestandardowego portu TCP (gdzie *[port]* hello niestandardowy numer portu TCP), a następnie kliknij przycisk "Aktualizuj"

### <a name="configure-your-javascript-spa-application"></a>Konfigurowanie aplikacji JEDNOSTRONICOWEJ JavaScript

1.  Utwórz plik o nazwie `msalconfig.js` zawierający informacje o rejestracji aplikacji hello. Jeśli używasz programu Visual Studio, wybierz hello projektu (folder główny projekt), kliknij prawym przyciskiem myszy i wybierz: `Add`  >  `New Item`  >  `JavaScript File`. Nadaj jej nazwę`msalconfig.js`
2.  Dodaj hello następującego kodu tooyour `msalconfig.js` pliku:

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
