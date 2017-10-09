---
title: "aaaYou nie można pobrać istnieje w tym miejscu na powitania portalu Azure na urządzeniu z systemem Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, gdy nie można w tym miejscu, w którymś z get i co można sprawdzić tooavoid uruchomione w tym oknie dialogowym."
services: active-directory
keywords: "dostęp warunkowy oparty na urządzeniach, rejestracja urządzenia, włączanie rejestracji urządzenia, rejestracja urządzenia i MDM"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a>Nie można dostać się tam z tego miejsca na urządzeniu z systemem Windows

Na przykład podczas próby uzyskania dostępu do intranetu usługi SharePoint Online w organizacji możesz zostać wyświetlona strona z informacją o tym, że *nie można dostać się tam z tego miejsca*. Widzisz tę stronę, ponieważ administrator skonfigurował zasady dostępu warunkowego, uniemożliwiający organizacji tooyour dostępu do zasobów w niektórych warunkach. Gdy może być konieczne toocontact pracy działu pomocy technicznej lub tooget Twojego administratora, można rozwiązać ten problem, istnieje kilka rzeczy, które można wypróbować samodzielnie, najpierw.

Jeśli używasz **Windows** urządzenia, należy sprawdzić następujące hello:

- Czy używasz obsługiwanej przeglądarki?

- Czy używasz obsługiwanej wersji systemu Windows na urządzeniu?

- Czy urządzenie jest zgodne?






## <a name="supported-browser"></a>Obsługiwana przeglądarka

Jeśli administrator skonfigurował zasady dostępu warunkowego, dostęp do zasobów organizacji można uzyskiwać tylko za pomocą obsługiwanej przeglądarki. Na urządzeniu z systemem Windows są obsługiwane tylko przeglądarki **Internet Explorer** i **Edge**.

Można łatwo zidentyfikować, czy nie może uzyskać dostęp do zasobu powodu nieobsługiwanej przeglądarki tooan analizując sekcja szczegóły hello strony błędu hello:

![Komunikat „Nie można dostać się tam z tego miejsca” dotyczący nieobsługiwanych przeglądarek](./media/active-directory-conditional-access-device-remediation/02.png "Scenariusz")

Korygowanie tylko Hello jest toouse przeglądarki obsługującej hello aplikacji dla danej platformy urządzenia. Pełna lista obsługiwanych przeglądarek jest dostępna na stronie [obsługiwanych przeglądarek](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).  


## <a name="supported-versions-of-windows"></a>Obsługiwane wersje systemu Windows

Hello muszą być spełnione następujące warunki dotyczące systemu operacyjnego Windows hello na urządzeniu: 

- Jeśli używasz systemu operacyjnego z pulpitu systemu Windows na urządzeniu, musi toobe systemu Windows 7 lub nowszy.
- Jeśli system operacyjny Windows server są uruchomione na urządzeniu, musi on toobe systemu Windows Server 2008 R2 lub nowszym. 


## <a name="compliant-device"></a>Zgodne urządzenie

Administrator może skonfigurować zasady dostępu warunkowego, który umożliwia organizacji tooyour dostępu do zasobów tylko ze zgodnych urządzeń. toobe zgodne urządzenie musi być albo tooyour dołączonego do lokalnej usługi Active Directory lub przyłączony tooyour usługi Azure Active Directory.

Można łatwo zidentyfikować, czy nie masz dostępu do zasobów powodu tooa urządzenia, które nie jest zgodne przez wyszukiwanie w sekcji szczegółów hello strony błędu hello:
 
![Komunikaty „Nie można dostać się tam z tego miejsca” dotyczące niezarejestrowanych urządzeń](./media/active-directory-conditional-access-device-remediation/01.png "Scenariusz")


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a>Jest tooan Twojego urządzenia przyłączone do lokalnej usługi Active Directory?

**Jeśli Twoje urządzenie jest dołączane tooan lokalnej usługi Active Directory w organizacji:**

1. Upewnij się, że logowania tooWindows przy użyciu swojego konta służbowego (konta usługi Active Directory).
2. Połącz tooyour sieci firmowej za pośrednictwem wirtualnej sieci prywatnej (VPN) lub funkcji DirectAccess.
3. Po połączeniu, naciśnij klawisze logo systemu Windows hello + hello L toolock klucza sesji systemu Windows.
4. Odblokuj sesję systemu Windows, wprowadzając poświadczenia konta służbowego.
5. Poczekaj chwilę, a następnie spróbuj ponownie w odpowiedzi na tooaccess hello aplikacji lub usługi.
6. Jeśli widzisz hello sam kliknij hello **więcej szczegółów** połączyć, a następnie skontaktuj się z administratorem ze szczegółami hello.


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a>Jest tooan Twojego urządzenia, które nie są przyłączone lokalnej usługi Active Directory?

Jeśli urządzenie nie jest dołączony tooan lokalnej usługi Active Directory i systemem Windows 10, dostępne są dwie opcje:

* Uruchom funkcję Azure AD Join
* Dodaj pracy lub szkołą tooWindows konta

Aby uzyskać informacje o różnicach między tymi dwoma opcjami, zobacz [Korzystanie z urządzeń z systemem Windows 10 w miejscu pracy](active-directory-azureadjoin-windows10-devices.md).  
Możliwe są następujące sytuacje:

- Należy tooyour organizacji, należy uruchomić Azure AD Join.
- Jest osobiste urządzenie lub z systemem Windows phone, należy dodać pracy lub szkołą tooWindows konta 



#### <a name="azure-ad-join-on-windows-10"></a>Funkcja Azure AD Join w systemie Windows 10

Hello toojoin kroki tooAzure Twojego urządzenia AD są również powiązane hello wersji systemu Windows 10 są na nim uruchomione. toodetermine hello wersji systemu operacyjnego Windows 10, uruchom hello **winver** polecenia: 

![Wersja systemu Windows](./media/active-directory-conditional-access-device-remediation/03.png )


**Rocznicowa aktualizacja systemu Windows 10 (wersja 1607):**

1. Otwórz hello **ustawienia** aplikacji.
2. Kliknij pozycję **Konta** > **Dostęp w pracy lub szkole**.
3. Kliknij przycisk **Połącz**.
4. Kliknij przycisk **Dołącz to urządzenie tooAzure AD**.
5. Organizacja tooyour uwierzytelniania, zapewniają uwierzytelnianie wieloskładnikowe, jeśli zostanie wyświetlony monit, a następnie wykonaj kroki hello, które są wyświetlane.
6. Wyloguj się, a następnie zaloguj się przy użyciu swojego konta służbowego.
7. Spróbuj ponownie tooaccess hello aplikacji.

**Windows 10 — aktualizacja z listopada 2015 (wersja 1511):**

1. Otwórz hello **ustawienia** aplikacji.
2. Kliknij pozycję **System** > **Informacje**.
3. Kliknij pozycję **Przyłącz do usługi Azure AD**.
4. Organizacja tooyour uwierzytelniania, zapewniają uwierzytelnianie wieloskładnikowe, jeśli zostanie wyświetlony monit, a następnie wykonaj kroki hello, które są wyświetlane.
5. Wyloguj się, a następnie zaloguj się przy użyciu swojego konta służbowego (Twojego konta usługi Azure AD).
6. Spróbuj ponownie tooaccess hello aplikacji.


#### <a name="workplace-join-on-windows-81"></a>Przyłączanie w miejscu pracy w systemie Windows 8.1

Jeśli urządzenie nie jest przyłączony do domeny i systemem Windows 8.1, toodo dołączanie do i zarejestrować się w programie Microsoft Intune, hello następujące kroki:

1. Otwórz okno **Ustawienia komputera**.
2. Kliknij pozycję **Sieć** > **Miejsce pracy**.
3. Kliknij pozycję **Dołącz**.
4. Organizacja tooyour uwierzytelniania, zapewniają uwierzytelnianie wieloskładnikowe, jeśli zostanie wyświetlony monit, a następnie wykonaj kroki hello, które są wyświetlane.
5. Kliknij pozycję **Włącz**.
6. Spróbuj ponownie tooaccess hello aplikacji.



#### <a name="add-your-work-or-school-account-toowindows"></a>Dodaj pracy lub szkołą tooWindows konta 


**Rocznicowa aktualizacja systemu Windows 10 (wersja 1607):**

1. Otwórz hello **ustawienia** aplikacji.
2. Kliknij pozycję **Konta** > **Dostęp w pracy lub szkole**.
3. Kliknij przycisk **Połącz**.
4. Organizacja tooyour uwierzytelniania, zapewniają uwierzytelnianie wieloskładnikowe, jeśli zostanie wyświetlony monit, a następnie wykonaj kroki hello, które są wyświetlane.
5. Spróbuj ponownie tooaccess hello aplikacji.


**Windows 10 — aktualizacja z listopada 2015 (wersja 1511):**

1. Otwórz hello **ustawienia** aplikacji.
2. Kliknij pozycję **Konta** > **Twoje konta**.
3. Kliknij pozycję **Dodaj konto służbowe**.
4. Organizacja tooyour uwierzytelniania, zapewniają uwierzytelnianie wieloskładnikowe, jeśli zostanie wyświetlony monit, a następnie wykonaj kroki hello, które są wyświetlane.
5. Spróbuj ponownie tooaccess hello aplikacji.





## <a name="next-steps"></a>Następne kroki
[Dostęp warunkowy do usługi Azure Active Directory](active-directory-conditional-access.md)

