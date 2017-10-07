---
title: "toouse aaaHow haseł aplikacji w usłudze Azure MFA? | Microsoft Docs"
description: "Ta strona będzie pomaganie użytkownikom w zrozumieniu hasła aplikacji są i jakie są używane dla z uwzględnieniem tooAzure MFA."
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
ms.openlocfilehash: bf2c11edc0ca81f2950eff0f7a3a24c8a5b34623
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>Co to są hasła aplikacji w usłudze Azure Multi-Factor Authentication?
Niektóre aplikacje korzystające z przeglądarki, takie jak hello klienta natywnego poczty e-mail firmy Apple, który używa programu Exchange Active Sync aktualnie nie obsługują uwierzytelniania wieloskładnikowego. Uwierzytelnianie wieloskładnikowe jest włączone dla użytkownika. Oznacza to, że jeśli użytkownik został włączony dla usługi Multi-Factor authentication i prób toouse aplikacji niekorzystających z przeglądarki, będą one toodo tak. Hasła aplikacji umożliwia to toooccur.

Po utworzeniu haseł aplikacji, możesz użyć tego zamiast oryginalnemu hasłu z tych aplikacji korzystających z przeglądarki. Jest to spowodowane podczas rejestrowania na potrzeby weryfikacji dwuetapowej, możesz jest informuje Microsoft nie toolet zarejestrować każdy użytkownik się przy użyciu hasła, jeśli nie mogą również wykonywać hello drugi weryfikacji. powitania klienta natywnego poczty e-mail firmy Apple na telefonie nie można zalogować się jako użytkownik, ponieważ nie można żądać na potrzeby weryfikacji dwuetapowej. Witaj rozwiązanie tego problemu jest toocreate bardziej bezpieczne hasło aplikacji, które nie są używane bieżące, ale tylko dla tych aplikacji, które nie obsługują weryfikacji dwuetapowej. Użyj hasła aplikacji hello, dzięki czemu aplikacje mogą obejść usługę Multi-Factor authentication i kontynuować toowork.

> [!NOTE]
> Klienci Office 2013 (w tym programu Outlook) obsługują nowe protokoły uwierzytelniania i może być używany z weryfikacji dwuetapowej.  Oznacza to, że po włączeniu hasła aplikacji nie są wymagane do użytku z klientami pakietu Office 2013.  Aby uzyskać więcej informacji, zobacz [pakietu Office 2013 nowoczesnego uwierzytelniania anonsowania publicznej wersji](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).


## <a name="how-toouse-app-passwords"></a>Jak toouse haseł aplikacji
Witaj poniżej przedstawiono niektóre tooremember zagadnienia dotyczące haseł aplikacji toouse.

* Nie twórz haseł aplikacji. Zamiast tego są one automatycznie generowane. Ponieważ masz tylko hasła aplikacji hello tooenter raz na aplikacji, jest bezpieczniejsze toouse bardziej złożonych, automatycznie wygenerowanego hasła, niż jeden do zapamiętania.
* Obecnie istnieje limit 40 haseł na użytkownika. Jeśli toocreate jeden po osiągnięciu limitu hello, będzie toodelete zostanie wyświetlony monit o jeden z istniejących haseł aplikacji przed utworzeniem nowego.
* Należy użyć jednego hasła aplikacji na urządzenie, nie na aplikację. Na przykład można utworzyć hasło aplikacji dla komputera przenośnego i korzystać z dla wszystkich aplikacji na tym komputerze. Następnie utwórz drugi toouse hasło aplikacji dla wszystkich aplikacji na pulpicie. 
* Jeden hello hasła aplikacji są podane w pierwszym można zarejestrować na potrzeby weryfikacji dwuetapowej.  Jeśli potrzebujesz dodatkowych z nich, można je utworzyć.



## <a name="creating-and-deleting-app-passwords"></a>Tworzenie i usuwanie haseł aplikacji
Podczas początkowej logowanie podano hasło aplikacji, które można użyć.  Ponadto można również tworzyć i Usuń hasła aplikacji w późniejszym czasie na.  Jak to zrobić, zależy od tego, jak używasz usługi Multi-Factor authentication. Hello odpowiedzi następujące pytania dotyczące toodetermine, w której powinien przejść toomanage hasła aplikacji: 

1. Używasz weryfikacji dwuetapowej dla swojego osobistego konta Microsoft? Jeśli tak, należy zapoznać się toohello [haseł aplikacji i weryfikacji dwuetapowej](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) artykułu, aby uzyskać pomoc. Jeśli nie, nadal tooquestion dwa.

2. OK, aby używać weryfikację dwuetapową dla konta firmowego lub szkolnego. Używasz go toosign w aplikacjach tooOffice 365? Jeśli tak, należy zapoznać się zbyt[utworzyć hasło aplikacji dla usługi Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) Aby uzyskać pomoc. Jeśli nie, nadal tooquestion trzech. 

3. Używasz weryfikacji dwuetapowej platformie Microsoft Azure? Jeśli tak, kontynuuj toohello [zarządzać hasłami aplikacji w portalu Azure hello](#manage-app-passwords-in-the-Azure-portal) sekcji tego artykułu. Jeśli nie, nadal tooquestion czterech.

4. Nie masz pewności, gdy używasz weryfikację dwuetapową? Kontynuować toohello [Zarządzanie hasłami aplikacji z portalu MyApps hello](#manage-app-passwords-with-the-myapps-portal) sekcji tego artykułu. 


## <a name="manage-app-passwords-in-hello-azure-portal"></a>Zarządzanie hasłami aplikacji w portalu Azure hello
Korzystając z platformy Azure, weryfikację dwuetapową, ma toocreate hasła aplikacji za pomocą hello portalu Azure.

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a>hasła aplikacji toocreate w hello portalu Azure
1. Zaloguj się toohello klasycznego portalu Azure.
2. U góry hello kliknij prawym przyciskiem myszy nazwę użytkownika, a następnie wybierz dodatkowa weryfikacja zabezpieczeń.
3. Na stronie biurowego hello u góry hello zaznacz haseł aplikacji
4. Kliknij przycisk **Utwórz**.
5. Wprowadź nazwę hasła aplikacji hello, a następnie kliknij przycisk **dalej**
6. Skopiuj Schowka toohello hasła aplikacji hello i wklej go do aplikacji.
   
   ![Chmura](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a>hasła aplikacji toodelete w hello portalu Azure
1. Zaloguj się toohello klasycznego portalu Azure.
2. U góry hello kliknij prawym przyciskiem myszy nazwę użytkownika, a następnie wybierz dodatkowa weryfikacja zabezpieczeń.
3. U góry hello, dalej tooadditional weryfikacji zabezpieczeń, wybierz **hasła aplikacji.**
4. Dalej hasła aplikacji toohello ma toodelete, wybierz opcję **usunąć**.
5. Potwierdź usunięcie hello klikając **tak**.
6. Po usunięciu hasła aplikacji hello, możesz kliknąć **zamknąć**.


## <a name="manage-app-passwords-with-hello-myapps-portal"></a>Zarządzanie hasłami aplikacji hello MyApps Portal.
Jeśli nie masz pewności, jak używać usługi Multi-Factor authentication, następnie zawsze możesz utworzyć i usunąć hasła aplikacji za pośrednictwem portalu myapps hello.

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a>hasła aplikacji przy użyciu toocreate hello Myapps portalu
1. Zaloguj się za[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Kliknij swoją nazwę na powitania górnym rogu i wybierz polecenie **profilu**.
3. Wybierz **dodatkowej weryfikacji zabezpieczeń**.
   ![Wybierz opcję dodatkowa weryfikacja zabezpieczeń — zrzut ekranu](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Wybierz **hasła aplikacji**.
   ![Wybierz hasła aplikacji — zrzut ekranu](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Kliknij przycisk **Utwórz**.
6. Wprowadź nazwę hasła aplikacji hello, a następnie kliknij przycisk **dalej**.
7. Skopiuj Schowka toohello hasła aplikacji hello i wklej go do aplikacji.
   ![Utwórz hasło aplikacji](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a>hasła aplikacji przy użyciu toodelete hello Myapps portalu
1. Zaloguj się za[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. U góry hello wybierz profil.
3. Wybierz **dodatkowej weryfikacji zabezpieczeń**.

   ![Wybierz opcję dodatkowa weryfikacja zabezpieczeń — zrzut ekranu](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Wybierz **hasła aplikacji**.

   ![Wybierz hasła aplikacji — zrzut ekranu](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Kliknij przycisk Dalej hasła aplikacji toohello ma toodelete, **usunąć**.

   ![Usuń hasło aplikacji](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. Upewnij się, że chcesz toodelete to hasło, klikając **tak**.
7. Po usunięciu hasła aplikacji hello, możesz kliknąć **zamknąć**.

## <a name="next-steps"></a>Następne kroki

- [Zarządzanie ustawieniami weryfikacji dwuetapowej](multi-factor-authentication-end-user-manage-settings.md)

- Wypróbuj hello [aplikacji Microsoft Authenticator](microsoft-authenticator-app-how-to.md) tooverify Twojego logowania z powiadomieniami aplikacji, nie odbiera teksty lub wywołań. 
