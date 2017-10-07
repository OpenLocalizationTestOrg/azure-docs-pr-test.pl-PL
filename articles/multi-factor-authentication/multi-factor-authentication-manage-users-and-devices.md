---
title: "aaaAdmins zarządzania użytkownikami i urządzeniami — usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toochange ustawienia użytkownika, takie jak wymuszanie toodo użytkowników hello hello dowód proces ponownie."
documentationcenter: 
services: multi-factor-authentication
author: kgremban
manager: femila
ms.assetid: aac3b922-7cc1-428c-9044-273579aa7b5a
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8c35435e4f6504014d9a4f6f1b837639c3b53481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-user-settings-with-azure-multi-factor-authentication-in-hello-cloud"></a>Zarządzaj ustawieniami użytkowników z usługi Azure Multi-Factor Authentication w chmurze hello
Jako administrator można zarządzać hello następujące ustawienia użytkowników i urządzeń:

* Ponownie wymagają metod kontaktu tooprovide użytkowników
* Usuń hasła aplikacji
* Uwierzytelniania MFA można wymagać wszystkie zaufane urządzenia 

## <a name="require-users-tooprovide-contact-methods-again"></a>Ponownie wymagają metod kontaktu tooprovide użytkowników
Ustawienie to wymusza procesu rejestracji hello toocomplete użytkownika hello ponownie. Aplikacje korzystające z przeglądarki nadal toowork, jeśli użytkownik hello ma haseł aplikacji dla nich.  Możesz usunąć hasła aplikacji hello użytkowników również wybierając **Usuń wszystkie istniejące hasła aplikacji wygenerowane przez użytkowników hello wybrane**.

### <a name="how-toorequire-users-tooprovide-contact-methods-again"></a>Jak tooprovide użytkowników toorequire metody kontaktu ponownie
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Po lewej stronie powitania, wybierz **usługi Azure Active Directory** > **użytkowników i grup** > **wszyscy użytkownicy**.
3. Wybierz **uwierzytelnianie wieloskładnikowe**. zostanie otwarta strona uwierzytelniania wieloskładnikowego Hello. 
4. Sprawdź hello pole dalej toohello lub użytkowników, że chcesz toomanage. Listy opcji szybkiego kroku są wyświetlane na powitania prawo. 
5. Wybierz **Zarządzanie ustawieniami użytkownika**.
6. Sprawdź pola hello **Wymagaj od wybranych użytkowników tooprovide ponownie metod kontaktu**.
   ![Podania metod kontaktu](./media/multi-factor-authentication-manage-users-and-devices/reproofup.png)
7. Kliknij pozycję **Zapisz**.
8. Kliknij przycisk **zamknąć**.

## <a name="delete-users-existing-app-passwords"></a>Usuwanie użytkowników istniejących haseł aplikacji
To ustawienie powoduje usunięcie wszystkich haseł aplikacji hello utworzone przez użytkownika. Aplikacje korzystające z przeglądarki, które zostały skojarzone z tymi hasłami aplikacji Zatrzymaj działa do momentu utworzenia nowego hasła aplikacji.

### <a name="how-toodelete-users-existing-app-passwords"></a>Jak użytkownicy toodelete istniejących haseł aplikacji
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Po lewej stronie powitania, wybierz **usługi Azure Active Directory** > **użytkowników i grup** > **wszyscy użytkownicy**.
3. Wybierz **uwierzytelnianie wieloskładnikowe**. zostanie otwarta strona uwierzytelniania wieloskładnikowego Hello. 
6. Sprawdź hello pole dalej toohello lub użytkowników, że chcesz toomanage. Listy opcji szybkiego kroku są wyświetlane na powitania prawo. 
7. Wybierz **Zarządzanie ustawieniami użytkownika**.
8. Sprawdź pola hello **Usuń wszystkie istniejące hasła aplikacji wygenerowane przez użytkowników hello wybrane**.
   ![Usuń hasła aplikacji](./media/multi-factor-authentication-manage-users-and-devices/deleteapppasswords.png)
9. Kliknij pozycję **Zapisz**.
10. Kliknij przycisk **zamknąć**.

## <a name="restore-mfa-on-all-remembered-devices-for-a-user"></a>Przywróć uwierzytelnianie wieloskładnikowe na wszystkich zapamiętanych urządzeniach użytkownika
Jedną z funkcji można skonfigurować hello Azure Multi-Factor Authentication jest przyznawanie użytkownikom urządzeń toomark opcji hello jako zaufany. Aby uzyskać więcej informacji, zobacz [ustawienia skonfigurować uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-whats-next.md#remember-multi-factor-authentication-for-devices-that-users-trust).

Użytkownicy mogą zrezygnować z weryfikacji dwuetapowej, można skonfigurować liczbę dni na swoich urządzeniach regularne. Jeśli konto jest zagrożone lub zaufanego urządzenia zostaną utracone, należy toobe tooremove stanie hello zaufanego stanu i wymaga weryfikacji dwuetapowej ponownie.

Witaj **przywracania uwierzytelnianie wieloskładnikowe na wszystkich zapamiętanych urządzeniach** ustawienie oznacza użytkownika hello hello weryfikacji dwuetapowej kwestionowanych tooperform następnym razem zalogują, niezależnie od tego, czy zdecydowano toomark ich urządzenie jako zaufany. 

### <a name="how-toorestore-mfa-on-all-suspended-devices-for-a-user"></a>Jak toorestore uwierzytelnianie wieloskładnikowe na wszystkich urządzeniach wstrzymane dla użytkownika
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Po lewej stronie powitania, wybierz **usługi Azure Active Directory** > **użytkowników i grup** > **wszyscy użytkownicy**.
3. Wybierz **uwierzytelnianie wieloskładnikowe**. zostanie otwarta strona uwierzytelniania wieloskładnikowego Hello. 
6. Sprawdź hello pole dalej toohello lub użytkowników, że chcesz toomanage. Listy opcji szybkiego kroku są wyświetlane na powitania prawo. 
7. Wybierz **Zarządzanie ustawieniami użytkownika**.
8. Sprawdź pola hello **przywracania uwierzytelnianie wieloskładnikowe na wszystkich zapamiętanych urządzeniach**
   ![Usuń hasła aplikacji](./media/multi-factor-authentication-manage-users-and-devices/rememberdevices.png)
9. Kliknij pozycję **Zapisz**.
10. Kliknij przycisk **zamknąć**.

## <a name="next-steps"></a>Następne kroki

- Uzyskaj więcej informacji o tym, jak za[ustawienia skonfigurować uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-whats-next.md)

- Jeśli użytkownicy będą potrzebować pomocy, wskazywały je na powitania [Podręcznik użytkownika na potrzeby weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user.md)
