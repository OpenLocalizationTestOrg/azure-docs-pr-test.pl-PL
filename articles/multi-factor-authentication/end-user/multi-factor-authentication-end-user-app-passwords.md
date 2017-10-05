---
title: "Jak używać hasła aplikacji w usłudze Azure MFA? | Microsoft Docs"
description: "Ta strona może pomóc użytkownikom w zrozumieniu hasła aplikacji są i jakie są używane dla z uwzględnieniem usługi Azure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: fe8fb3b6e249fbe6bc0f8e55c4267f09cfcfcff5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>Co to są hasła aplikacji w usłudze Azure Multi-Factor Authentication?
Niektóre aplikacje korzystające z przeglądarki, takie jak klienta natywnego poczty e-mail firmy Apple, który używa programu Exchange Active Sync aktualnie nie obsługują uwierzytelniania wieloskładnikowego. Uwierzytelnianie wieloskładnikowe jest włączone dla użytkownika. Oznacza to, że jeśli użytkownik został włączony dla usługi Multi-Factor authentication i próbuje korzystać z aplikacji korzystających z przeglądarki, będą mogli w tym celu. Hasła aplikacji umożliwia to możliwe.

Po utworzeniu haseł aplikacji, możesz użyć tego zamiast oryginalnemu hasłu z tych aplikacji korzystających z przeglądarki. Jest to spowodowane podczas rejestrowania na potrzeby weryfikacji dwuetapowej jest informacją o Microsoft nie pozwala każdy Zaloguj się przy użyciu hasła, jeśli nie mogą również wykonywać drugi weryfikacji. Apple klienta natywnego poczty e-mail na telefonie nie można zalogować się jako użytkownik, ponieważ nie można żądać na potrzeby weryfikacji dwuetapowej. Rozwiązanie tego problemu jest do tworzenia bardziej bezpieczne hasło aplikacji, które nie są używane bieżące, ale tylko dla tych aplikacji, które nie obsługują weryfikacji dwuetapowej. Użyj hasła aplikacji, dzięki czemu aplikacje mogą obejść usługę Multi-Factor authentication i kontynuować pracę.

> [!NOTE]
> Klienci Office 2013 (w tym programu Outlook) obsługują nowe protokoły uwierzytelniania i może być używany z weryfikacji dwuetapowej.  Oznacza to, że po włączeniu hasła aplikacji nie są wymagane do użytku z klientami pakietu Office 2013.  Aby uzyskać więcej informacji, zobacz [pakietu Office 2013 nowoczesnego uwierzytelniania anonsowania publicznej wersji](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).


## <a name="how-to-use-app-passwords"></a>Jak używać hasła aplikacji
Poniżej przedstawiono niektóre warto zapamiętać dotyczące stosowania haseł aplikacji.

* Nie twórz haseł aplikacji. Zamiast tego są one automatycznie generowane. Ponieważ trzeba wprowadzić hasło aplikacji raz na aplikacji, jest bezpieczniejsze użyj bardziej złożonych, automatycznie wygenerowanego hasła zamiast wprowadzania, który może zapamiętać.
* Obecnie istnieje limit 40 haseł na użytkownika. Jeśli próbujesz utworzyć po osiągnięciu limitu, pojawi się monit o usunięcie istniejących haseł aplikacji przed utworzeniem nowego.
* Należy użyć jednego hasła aplikacji na urządzenie, nie na aplikację. Na przykład można utworzyć hasło aplikacji dla komputera przenośnego i korzystać z dla wszystkich aplikacji na tym komputerze. Następnie utwórz drugi hasło aplikacji dla wszystkich aplikacji na pulpicie. 
* Hasło aplikacji są podane po raz pierwszy należy zarejestrować na potrzeby weryfikacji dwuetapowej.  Jeśli potrzebujesz dodatkowych z nich, można je utworzyć.



## <a name="creating-and-deleting-app-passwords"></a>Tworzenie i usuwanie haseł aplikacji
Podczas początkowej logowanie podano hasło aplikacji, które można użyć.  Ponadto można również tworzyć i Usuń hasła aplikacji w późniejszym czasie na.  Jak to zrobić, zależy od tego, jak używasz usługi Multi-Factor authentication. Odpowiedz na następujące pytania, aby określić, gdzie należy przejść do zarządzania hasłami aplikacji: 

1. Używasz weryfikacji dwuetapowej dla swojego osobistego konta Microsoft? Jeśli tak, należy zapoznać się [haseł aplikacji i weryfikacji dwuetapowej](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) artykułu, aby uzyskać pomoc. Jeśli nie, nadal dwa pytanie.

2. OK, aby używać weryfikację dwuetapową dla konta firmowego lub szkolnego. Używać go do logowania do aplikacji usługi Office 365? Jeśli tak, należy zapoznać się [utworzyć hasło aplikacji dla usługi Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) Aby uzyskać pomoc. Jeśli nie, nadal pytanie trzech. 

3. Używasz weryfikacji dwuetapowej platformie Microsoft Azure? Jeśli tak, w dalszym ciągu [zarządzać hasłami aplikacji w portalu Azure](#manage-app-passwords-in-the-Azure-portal) sekcji tego artykułu. Jeśli nie, nadal cztery pytanie.

4. Nie masz pewności, gdy używasz weryfikację dwuetapową? Nadal [Zarządzanie hasłami aplikacji przy użyciu portalu MyApps](#manage-app-passwords-with-the-myapps-portal) sekcji tego artykułu. 


## <a name="manage-app-passwords-in-the-azure-portal"></a>Zarządzanie hasłami aplikacji w portalu Azure
Jeśli używasz weryfikacji dwuetapowej z platformy Azure, chcesz utworzyć hasła aplikacji za pośrednictwem portalu Azure.

### <a name="to-create-app-passwords-in-the-azure-portal"></a>Aby utworzyć hasła aplikacji w portalu Azure
1. Zaloguj się do klasycznego portalu Azure.
2. U góry kliknij prawym przyciskiem myszy nazwę użytkownika, a następnie wybierz dodatkowa weryfikacja zabezpieczeń.
3. Na stronie biurowego u góry wybierz haseł aplikacji
4. Kliknij przycisk **Utwórz**.
5. Wprowadź nazwę hasła aplikacji, a następnie kliknij przycisk **dalej**
6. Kopiuj hasło aplikacji do Schowka i wklej go do aplikacji.
   
   ![Chmura](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="to-delete-app-passwords-in-the-azure-portal"></a>Aby usunąć hasła aplikacji w portalu Azure
1. Zaloguj się do klasycznego portalu Azure.
2. U góry kliknij prawym przyciskiem myszy nazwę użytkownika, a następnie wybierz dodatkowa weryfikacja zabezpieczeń.
3. W górnej części strony obok dodatkowej weryfikacji zabezpieczeń, wybierz **hasła aplikacji.**
4. Obok hasło aplikacji do usunięcia, wybierz **usunąć**.
5. Potwierdź decyzję, klikając **tak**.
6. Po usunięciu hasła aplikacji, możesz kliknąć **zamknąć**.


## <a name="manage-app-passwords-with-the-myapps-portal"></a>Zarządzanie hasłami aplikacji przy użyciu portalu MyApps.
Jeśli nie masz pewności, jak używać usługi Multi-Factor authentication, następnie zawsze możesz utworzyć i usunąć hasła aplikacji za pośrednictwem portalu myapps.

### <a name="to-create-an-app-password-using-the-myapps-portal"></a>Aby utworzyć hasło aplikacji przy użyciu portalu Myapps
1. Zaloguj się do [https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Kliknij nazwę górnym rogu i wybierz **profilu**.
3. Wybierz **dodatkowej weryfikacji zabezpieczeń**.
   ![Wybierz opcję dodatkowa weryfikacja zabezpieczeń — zrzut ekranu](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Wybierz **hasła aplikacji**.
   ![Wybierz hasła aplikacji — zrzut ekranu](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Kliknij przycisk **Utwórz**.
6. Wprowadź nazwę hasła aplikacji, a następnie kliknij przycisk **dalej**.
7. Kopiuj hasło aplikacji do Schowka i wklej go do aplikacji.
   ![Utwórz hasło aplikacji](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="to-delete-an-app-password-using-the-myapps-portal"></a>Aby usunąć hasła aplikacji przy użyciu portalu Myapps
1. Zaloguj się do [https://myapps.microsoft.com](https://myapps.microsoft.com)
2. U góry wybierz profil.
3. Wybierz **dodatkowej weryfikacji zabezpieczeń**.

   ![Wybierz opcję dodatkowa weryfikacja zabezpieczeń — zrzut ekranu](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Wybierz **hasła aplikacji**.

   ![Wybierz hasła aplikacji — zrzut ekranu](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Obok hasło aplikacji do usunięcia, kliknij przycisk **usunąć**.

   ![Usuń hasło aplikacji](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. Upewnij się, czy chcesz usunąć to hasło, klikając **tak**.
7. Po usunięciu hasła aplikacji, możesz kliknąć **zamknąć**.

## <a name="next-steps"></a>Następne kroki

- [Zarządzanie ustawieniami weryfikacji dwuetapowej](multi-factor-authentication-end-user-manage-settings.md)

- Wypróbuj [aplikacji Microsoft Authenticator](microsoft-authenticator-app-how-to.md) można zweryfikować użytkownika logowania z powiadomieniami aplikacji, nie odbiera teksty lub wywołań. 
