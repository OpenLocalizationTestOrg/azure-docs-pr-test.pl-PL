---
title: "aaaHow tooactivate lub dezaktywować rolę | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooactivate role uprzywilejowane tożsamości z aplikacji Azure Privileged Identity Management hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8c68ad69e4b006263bbb8a1cfc7ed3dba974e1db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooactivate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a>Jak tooactivate lub dezaktywować role w programie Azure AD Privileged Identity Management
Azure Active Directory (AD) Privileged Identity Management upraszcza sposób przedsiębiorstw Zarządzanie tooresources uprzywilejowanego dostępu w usłudze Azure AD i innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune.  

Jeśli użytkownik wprowadzono uprawnia do skorzystania z rolą administracyjną, oznacza to, że można aktywować tej roli, gdy będziesz potrzebować tooperform uprzywilejowany akcje. Na przykład jeśli zarządzasz czasami funkcje usługi Office 365, organizacji ról uprzywilejowanych administratorów może nie mieć można stałe administratora globalnego, ponieważ ta rola ma wpływ na inne usługi, za. Zamiast tego należy podjąć ich możesz kwalifikuje się do usługi Azure AD ról, takich jak Exchange Online Administrator. Tooactivate można zażądać tej roli, gdy potrzebne są uprawnienia jego, a następnie będziesz mieć administratorowi kontrolowanie ustalonej okresu.

W tym artykule jest dla administratorów, którzy potrzebują tooactivate ich roli w usłudze Azure AD Privileged Identity Management (PIM). Przeprowadza użytkownika przez hello kroki tooactivate rolę w przypadku potrzebne uprawnienia hello i dezaktywować rolę hello, gdy wszystko będzie gotowe. Ponadto administratorzy ról uprzywilejowanych mogą wymagać zatwierdzenia tooactivate roli (wersja zapoznawcza). Dowiedz się więcej o [przepływów pracy PIM](./privileged-identity-management/azure-ad-pim-approval-workflow.md) tutaj.

## <a name="add-hello-privileged-identity-management-application"></a>Dodawanie aplikacji Privileged Identity Management hello
Używanie hello Azure AD Privileged Identity Management aplikacji w hello [portalu Azure](https://portal.azure.com/) toorequest uaktywnienia roli, nawet jeśli chcesz zacząć toooperate w innym portalu lub programu PowerShell. Jeśli nie masz aplikacji usługi Azure AD Privileged Identity Management hello portalu Azure, wykonaj te tooget kroki pracy.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Wybierz swoją nazwę użytkownika w hello prawym górnym rogu hello portalu Azure i wybierz hello katalogu, której będzie można działać.
3. Wybierz **więcej usług** i użyj hello filtru pole tekstowe toosearch dla **Azure AD Privileged Identity Management**.
4. Sprawdź **toodashboard numeru Pin** , a następnie kliknij przycisk **Utwórz**. Otwiera Hello aplikacji Privileged Identity Management.

## <a name="activate-a-role"></a>Aktywować rolę
Jeśli potrzebujesz tootake roli można żądania aktywacji, wybierając hello **Moje ról** opcji nawigacji w hello Azure AD Privileged Identity Management aplikacji lewej formantu kolumny nawigacji.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/) i wybierz hello Azure AD Privileged Identity Management kafelka.
2. Wybierz **Moje ról**. Lista przypisane role kwalifikujących się są wyświetlane w hello grupowanie u góry hello hello strony.
3. Wybierz tooactivate roli.
4. Wybierz **aktywować**. Witaj **żądania aktywacji roli** zostanie wyświetlony blok.
5. Niektóre role wymagają uwierzytelniania wieloskładnikowego (MFA), zanim będzie można aktywować hello roli. Masz tylko tooauthenticate raz na sesji.
   
    ![Sprawdź za pomocą usługi MFA przed Aktywacja roli — zrzut ekranu][2]
6. Wprowadź przyczynę hello żądanie aktywacji hello w polu tekstowym hello.  Niektóre role wymagają toosupply numer biletu problemy.
7. Kliknij przycisk **OK**.  Jeśli rola hello nie wymaga zatwierdzenia, jest już aktywna i roli hello jest widoczna na liście hello aktywnych ról (bezpośrednio pod hello listę przypisań ról kwalifikujących się). Jeśli hello [rola wymaga zatwierdzenia](./privileged-identity-management/azure-ad-pim-approval-workflow.md) tooactivate, wyskakujące powiadomienie krótko będą wyświetlane w hello prawym górnym rogu przeglądarki informujące o tym, Żądanie hello oczekuje na zatwierdzenie.

    ![Żądania oczekujące powiadomienia — zrzut ekranu][3]

## <a name="deactivate-a-role"></a>Dezaktywować rolę
Po uaktywnieniu roli automatycznie dezaktywuje to, gdy zostanie osiągnięty limit czasu (kwalifikujących się czas trwania).

Po ukończeniu zadań administracyjnych wcześniej, można również dezaktywować rolę ręcznie w hello aplikacji Azure AD Privileged Identity Management.  Wybierz **Moje ról**, wybierz rolę hello gotowe korzystanie z hello **przypisania roli Active** grupowania i wybierz **Dezaktywuj**.  

## <a name="cancel-a-pending-request"></a>Anulowanie oczekującego żądania
W przypadku hello nie wymagają aktywacji roli, która wymaga zatwierdzenia, możesz anulować w dowolnym momencie oczekującego żądania. Po prostu zaznacz hello **Moje ról** opcji nawigacji w hello Azure AD Privileged Identity Management aplikacji lewej formantu kolumny nawigacji.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/) i wybierz hello Azure AD Privileged Identity Management kafelka.
2. Wybierz **Moje ról**. Lista przypisane role kwalifikujących się są wyświetlane w hello grupowanie u góry hello hello strony.
3. Wybierz rolę.
4. Wybierz hello **aktywacji oczekuje na zatwierdzenie** transparent hello roli aktywacji szczegóły blok.
5. Wybierz **anulować** u góry hello hello **oczekują na zatwierdzenie** bloku.

   ![Anulowanie oczekującego żądania zrzut ekranu][4]

## <a name="next-steps"></a>Następne kroki
Jeśli chcesz dowiedzieć się więcej o usłudze Azure AD Privileged Identity Management, hello poniższe linki mają więcej informacji.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
