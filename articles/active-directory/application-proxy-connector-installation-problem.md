---
title: "Instalowanie aaaProblem hello łącznika Agent serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot problemów może hello po zainstalowaniu łącznika Agent serwera Proxy aplikacji"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a>Problem podczas instalowania hello łącznika Agent serwera Proxy aplikacji

Łącznik serwera Proxy aplikacji usługi Microsoft AAD jest składnik domeny wewnętrznej, który używa połączenia wychodzące tooestablish hello łączności z domeny wewnętrznej toohello hello chmury dostępnego punktu końcowego.

## <a name="general-problem-areas-with-connector-installation"></a>Ogólne obszarów problemów z instalacją łącznika

W przypadku niepowodzenia instalacji hello łącznika hello głównego przyczyną jest zazwyczaj jedną z następujących obszarów hello:

1.  **Łączność** — toocomplete udanej instalacji hello nowy łącznik potrzeb tooregister i ustanowienia zaufania przyszłych właściwości. Jest to realizowane łącząc toohello usługi w chmurze serwera Proxy aplikacji usługi AAD.

2.  **Tworzenie relacji zaufania** — nowy łącznik hello tworzy samopodpisany certyfikat i rejestruje toohello usługi w chmurze.

3.  **Uwierzytelnianie Witaj, Administratorze** — podczas instalacji, hello użytkownik musi podać poświadczenia administratora toocomplete hello łącznika instalacji.

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a>Sprawdź łączność toohello serwera Proxy aplikacji w chmurze usługi i strony Login firmy Microsoft

**Cel:** sprawdzić, czy maszyna łącznika hello łączy punktu końcowego rejestracji serwera Proxy aplikacji usługi AAD toohello, a także strony logowania firmy Microsoft.

1.  Otwórz przeglądarkę i przejdź toohello, następujące strony sieci web: <https://aadap-portcheck.connectorporttest.msappproxy.net> , sprawdź tego tooCentral łączności hello USA i działają centrów danych wschodnie stany USA z portami 9090 i 9091.

2.  Jeśli żadnego z tych portów zakończy się niepowodzeniem (nie ma zielonym znacznikiem wyboru), sprawdź, że hello zapory lub serwera proxy wewnętrznej bazy danych ma \*. msappproxy.net z portami 9090 i 9091 poprawnie zdefiniowany.

3.  Otwórz w przeglądarce (osobnej karcie) i przejdź toohello następujące strony sieci web: <https://login.microsoftonline.com>, upewnij się, że możesz zalogować się toothat strony.

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>Sprawdź, czy składniki maszyny i wewnętrznej bazy danych obsługuje dla certyfikatu relacji zaufania serwera Proxy aplikacji

**Cel:** Sprawdź, czy hello łącznika maszyny, wewnętrznej bazy danych serwera proxy i zapory można obsługiwać certyfikatu hello utworzonego przez łącznik powitania dla przyszłych zaufania.

>[!NOTE]
>Łącznik Hello próbuje toocreate cert SHA512, która jest obsługiwana przez TLS1.2. Jeśli maszyna hello lub hello zaporę wewnętrznej bazy danych i serwera proxy nie obsługuje TLS1.2 hello instalacja się nie powieść.
>
>

**problem hello tooresolve:**

1.  Sprawdź komputer hello obsługuje TLS1.2 — wersje wszystkich okien po 2012 R2 powinny obsługiwać protokół TLS 1.2. W przypadku komputera łącznika z wersji 2012 R2 lub wcześniej, upewnij się, że hello następujące KB/s są zainstalowane na komputerze hello: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  Skontaktuj się z administratorem sieci i tooverify że hello wewnętrznej bazy danych z serwera proxy i zapory nie blokują SHA512 dla ruchu wychodzącego.

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a>Sprawdź, czy administratora jest używane tooinstall hello łącznika

**Cel:** Sprawdź, że hello użytkownika, który próbuje tooinstall hello łącznika jest administratorem z prawidłowymi poświadczeniami. Obecnie użytkownik hello musi być administratorem globalnym dla hello toosucceed instalacji.

**tooverify hello poświadczenia są prawidłowe:**

Połącz za<https://login.microsoftonline.com> i użyj hello tych samych poświadczeń. Upewnij się, że hello użytkownik zaloguje się ponownie. Sprawdź hello roli użytkownika, przechodząc zbyt**usługi Azure Active Directory**  - &gt; **użytkowników i grup**  - &gt; **wszyscy użytkownicy**. 

Wybierz konto użytkownika, następnie "Directory Role" w menu wynikowy hello. Sprawdź, czy ta rola wybranego hello jest "Administrator globalny". Jeśli tooaccess żadnego hello strony wraz z tych kroków, nie jesteś administratorem globalnym.

## <a name="next-steps"></a>Następne kroki
[Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md)
