---
title: "Problem podczas instalowania agenta łącznika serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Jak rozwiązywać problemy, które może sprostać podczas instalowania agenta łącznika serwera Proxy aplikacji"
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
ms.openlocfilehash: 91b3f6f3c8339647f568a509e9efd8e1fffb13dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-proxy-agent-connector"></a>Problem podczas instalowania agenta łącznika serwera Proxy aplikacji

Łącznik serwera Proxy aplikacji usługi Microsoft AAD jest składnik domeny wewnętrznej, który używa połączenia wychodzące do nawiązywania łączności z dostępnego punktu końcowego chmury do domeny wewnętrznej.

## <a name="general-problem-areas-with-connector-installation"></a>Ogólne obszarów problemów z instalacją łącznika

Podczas instalacji łącznika nie powiedzie się, przyczynę zwykle jest jednym z następujących obszarów:

1.  **Łączność** — w celu ukończenia instalacja przebiegła pomyślnie, nowych potrzeb łącznika do rejestracji i ustanowienia zaufania przyszłych właściwości. Jest to realizowane przez nawiązanie połączenia usługi w chmurze serwera Proxy aplikacji usługi AAD.

2.  **Tworzenie relacji zaufania** — nowy łącznik tworzy samopodpisany certyfikat i rejestruje do usługi w chmurze.

3.  **Uwierzytelnianie Admin** — podczas instalacji, użytkownik musi podać poświadczenia administratora, aby ukończyć instalację łącznika.

## <a name="verify-connectivity-to-the-cloud-application-proxy-service-and-microsoft-login-page"></a>Sprawdź łączność z usługi serwera Proxy aplikacji w chmurze i strony Login firmy Microsoft

**Cel:** upewnij się, że maszyna łącznika można łączyć do punktu końcowego rejestracji serwera Proxy aplikacji usługi AAD, jak również strony logowania firmy Microsoft.

1.  Otwórz przeglądarkę i przejdź do następnej strony sieci web: <https://aadap-portcheck.connectorporttest.msappproxy.net> i sprawdź, czy łączność środkowe stany USA i wschodnie stany USA centrów danych z portami 9090 i 9091 działa.

2.  Jeśli żadnego z tych portów zakończy się niepowodzeniem (nie ma zielonym znacznikiem wyboru), sprawdź, czy zapora lub zaplecza serwer proxy ma \*. msappproxy.net z portami 9090 i 9091 poprawnie zdefiniowany.

3.  Otwórz w przeglądarce (osobnej karcie) i przejdź do następnej strony sieci web: <https://login.microsoftonline.com>, upewnij się, że możesz zalogować się do tej strony.

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>Sprawdź, czy składniki maszyny i wewnętrznej bazy danych obsługuje dla certyfikatu relacji zaufania serwera Proxy aplikacji

**Cel:** Sprawdź, czy łącznik maszyny, wewnętrznej bazy danych serwera proxy i zapory można obsługiwać certyfikat utworzony przez łącznik dla przyszłych zaufania.

>[!NOTE]
>Łącznik próbuje utworzyć certyfikatu SHA512, która jest obsługiwana przez TLS1.2. Jeśli komputer lub zaporę wewnętrznej bazy danych i serwera proxy nie obsługuje TLS1.2, instalacja się nie powieść.
>
>

**Aby rozwiązać ten problem:**

1.  Sprawdź komputer obsługuje TLS1.2 — wersje wszystkich okien po 2012 R2 powinny obsługiwać protokół TLS 1.2. W przypadku komputera łącznika z wersji 2012 R2 lub wcześniej, upewnij się, czy na komputerze są zainstalowane następujące KB/s: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  Skontaktuj się z administratorem sieci i poproś o Sprawdź, czy wewnętrznej bazy danych serwera proxy i zapory nie blokują SHA512 dla ruchu wychodzącego.

## <a name="verify-admin-is-used-to-install-the-connector"></a>Sprawdź, czy administrator służy do instalowania łącznika

**Cel:** Sprawdź, czy administrator z prawidłowymi poświadczeniami użytkownika, który próbuje zainstalować łącznik. Obecnie użytkownik musi być administratorem globalnym dla instalacji powiodło się.

**Aby sprawdzić, czy poświadczenia są prawidłowe:**

Połączyć się z <https://login.microsoftonline.com> i użyć tych samych poświadczeń. Upewnij się, że użytkownik zaloguje się ponownie. Rola użytkownika można sprawdzić, przechodząc do **usługi Azure Active Directory**  - &gt; **użytkowników i grup**  - &gt; **wszyscy użytkownicy**. 

Wybierz konto użytkownika, następnie "Directory Role" w menu wynikowy. Sprawdź, czy wybraną rolę "Administrator globalny". Jeśli nie można uzyskać dostępu do żadnych stron wzdłuż następujące kroki, nie jesteś administratorem globalnym.

## <a name="next-steps"></a>Następne kroki
[Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md)
