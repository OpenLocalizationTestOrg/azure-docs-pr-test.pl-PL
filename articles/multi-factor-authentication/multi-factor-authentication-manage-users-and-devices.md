---
title: "Administratorzy zarządzania użytkownikami i urządzeniami — usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Opisuje sposób zmiany ustawień użytkownika, takie jak wymuszanie użytkownikom ponownie wykonaj proces o potwierdzenie."
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
ms.openlocfilehash: e9b8504d4a59cf0fae69a4e975d6f834028066d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-user-settings-with-azure-multi-factor-authentication-in-the-cloud"></a>Zarządzaj ustawieniami użytkowników z usługi Azure Multi-Factor Authentication w chmurze
Jako administrator możesz zarządzać następującymi ustawieniami użytkowników i urządzeń:

* Wymaganie od użytkowników ponownego podania metod kontaktu
* Usuń hasła aplikacji
* Uwierzytelniania MFA można wymagać wszystkie zaufane urządzenia 

## <a name="require-users-to-provide-contact-methods-again"></a>Wymaganie od użytkowników ponownego podania metod kontaktu
Ustawienie to wymusza użytkownika, aby zakończyć proces rejestracji ponownie. Aplikacje korzystające z przeglądarki w dalszym ciągu działać, jeśli użytkownik ma haseł aplikacji dla nich.  Możesz usunąć hasła aplikacji użytkownicy również wybierając **Usuń wszystkie istniejące hasła aplikacji wygenerowane przez wybranych użytkowników**.

### <a name="how-to-require-users-to-provide-contact-methods-again"></a>Sposób wymagać od użytkowników ponownego podania metod kontaktu
1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
2. Po lewej stronie, wybierz **usługi Azure Active Directory** > **użytkowników i grup** > **wszyscy użytkownicy**.
3. Wybierz **uwierzytelnianie wieloskładnikowe**. Zostanie otwarta strona uwierzytelniania wieloskładnikowego. 
4. Zaznacz pole obok użytkownika lub użytkowników, których chcesz zarządzać. Listy opcji szybkiego kroku są wyświetlane po prawej stronie. 
5. Wybierz **Zarządzanie ustawieniami użytkownika**.
6. Pole wyboru dla **Wymagaj od wybranych użytkowników ponownego podania metod kontaktu**.
   ![Podania metod kontaktu](./media/multi-factor-authentication-manage-users-and-devices/reproofup.png)
7. Kliknij pozycję **Zapisz**.
8. Kliknij przycisk **zamknąć**.

## <a name="delete-users-existing-app-passwords"></a>Usuwanie użytkowników istniejących haseł aplikacji
To ustawienie powoduje usunięcie wszystkich haseł aplikacji utworzonych przez użytkownika. Aplikacje korzystające z przeglądarki, które zostały skojarzone z tymi hasłami aplikacji Zatrzymaj działa do momentu utworzenia nowego hasła aplikacji.

### <a name="how-to-delete-users-existing-app-passwords"></a>Jak usunąć użytkowników z istniejących haseł aplikacji
1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
2. Po lewej stronie, wybierz **usługi Azure Active Directory** > **użytkowników i grup** > **wszyscy użytkownicy**.
3. Wybierz **uwierzytelnianie wieloskładnikowe**. Zostanie otwarta strona uwierzytelniania wieloskładnikowego. 
6. Zaznacz pole obok użytkownika lub użytkowników, których chcesz zarządzać. Listy opcji szybkiego kroku są wyświetlane po prawej stronie. 
7. Wybierz **Zarządzanie ustawieniami użytkownika**.
8. Pole wyboru dla **Usuń wszystkie istniejące hasła aplikacji wygenerowane przez wybranych użytkowników**.
   ![Usuń hasła aplikacji](./media/multi-factor-authentication-manage-users-and-devices/deleteapppasswords.png)
9. Kliknij pozycję **Zapisz**.
10. Kliknij przycisk **zamknąć**.

## <a name="restore-mfa-on-all-remembered-devices-for-a-user"></a>Przywróć uwierzytelnianie wieloskładnikowe na wszystkich zapamiętanych urządzeniach użytkownika
Jedną z funkcji można skonfigurować uwierzytelnianie wieloskładnikowe Azure jest nadanie użytkownikom opcję, aby oznaczyć urządzeń jako zaufany. Aby uzyskać więcej informacji, zobacz [ustawienia skonfigurować uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-whats-next.md#remember-multi-factor-authentication-for-devices-that-users-trust).

Użytkownicy mogą zrezygnować z weryfikacji dwuetapowej, można skonfigurować liczbę dni na swoich urządzeniach regularne. Jeśli złamania zabezpieczeń konta lub zaufanego urządzenia zostaną utracone, należy mieć możliwość usunięcia zaufanego stanu i wymaga weryfikacji dwuetapowej ponownie.

**Przywracania uwierzytelnianie wieloskładnikowe na wszystkich zapamiętanych urządzeniach** ustawienie oznacza, że użytkownik będzie wezwał do przeprowadzenia weryfikacji dwuetapowej przy następnym zalogowaniu, niezależnie od tego, czy wybrana do oznaczania ich urządzenia jako zaufany. 

### <a name="how-to-restore-mfa-on-all-suspended-devices-for-a-user"></a>Jak przywrócić uwierzytelnianie wieloskładnikowe na wszystkich urządzeniach wstrzymane dla użytkownika
1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
2. Po lewej stronie, wybierz **usługi Azure Active Directory** > **użytkowników i grup** > **wszyscy użytkownicy**.
3. Wybierz **uwierzytelnianie wieloskładnikowe**. Zostanie otwarta strona uwierzytelniania wieloskładnikowego. 
6. Zaznacz pole obok użytkownika lub użytkowników, których chcesz zarządzać. Listy opcji szybkiego kroku są wyświetlane po prawej stronie. 
7. Wybierz **Zarządzanie ustawieniami użytkownika**.
8. Pole wyboru dla **przywracania uwierzytelnianie wieloskładnikowe na wszystkich zapamiętanych urządzeniach**
   ![Usuń hasła aplikacji](./media/multi-factor-authentication-manage-users-and-devices/rememberdevices.png)
9. Kliknij pozycję **Zapisz**.
10. Kliknij przycisk **zamknąć**.

## <a name="next-steps"></a>Następne kroki

- Uzyskaj więcej informacji o sposobie [ustawienia skonfigurować uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-whats-next.md)

- Jeśli użytkownicy będą potrzebować pomocy, wskazać im kierunku [Podręcznik użytkownika na potrzeby weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user.md)
