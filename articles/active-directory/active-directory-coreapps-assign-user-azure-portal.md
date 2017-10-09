---
title: "aaaAssign użytkownika lub grupę tooan przedsiębiorstwa aplikacji w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooselect tooassign aplikacji organizacji użytkownika lub grupę tooit w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a>Przypisywanie użytkownikowi lub grupie tooan przedsiębiorstwa aplikacji w usłudze Azure Active Directory
Jest łatwy tooassign użytkownika lub grupy tooyour przedsiębiorstwa aplikacji w usłudze Azure Active Directory (Azure AD). Musi mieć hello odpowiednie uprawnienia toomanage hello przedsiębiorstwa aplikacji, a musi być administratorem globalnym katalogu hello.

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a>Jak przypisać aplikację przedsiębiorstwa tooan dostępu użytkownika?
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź w polu tekstowym hello Azure Active Directory, a następnie wybierz **Enter**.
3. Na powitania **usługi Azure Active Directory - *directoryname***  bloku (to znaczy bloku hello Azure AD dla katalogu hello są używane do zarządzania), wybierz **aplikacje dla przedsiębiorstw**.

    ![Otwieranie aplikacji przedsiębiorstwa](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. Na powitania **aplikacje dla przedsiębiorstw** bloku, wybierz opcję **wszystkie aplikacje**. Zobaczysz listę aplikacji hello, którymi można zarządzać.
5. Na powitania **aplikacje przedsiębiorstwa — wszystkie aplikacje** bloku, wybierz aplikację.
6. Na powitania ***appname*** bloku (to znaczy hello bloku o nazwie hello hello wybranej aplikacji w tytule hello) wybierz **użytkownicy i grupy**.

    ![Wybieranie hello wszystkie polecenia aplikacji](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. Na powitania ***appname*** **— przypisanie do grupy & użytkownika** bloku, wybierz hello **Dodaj** polecenia.
8. Na powitania **Dodaj przydziału** bloku, wybierz opcję **użytkowników i grup**.

    ![Przypisywanie użytkownikowi lub grupie aplikacji toohello](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. Na powitania **użytkowników i grup** bloku, wybierz jeden lub więcej użytkowników lub grup z hello listy, a następnie wybierz hello **wybierz** przycisk u dołu hello hello bloku.
10. Na powitania **Dodaj przydziału** bloku, wybierz opcję **roli**. Następnie na powitania **wybierz rolę** bloku, wybierz toohello tooapply roli wybrane użytkowników lub grup, a następnie wybierz hello **OK** przycisk u dołu hello hello bloku.
11. Na powitania **Dodaj przydziału** bloku, wybierz hello **przypisać** przycisk u dołu hello hello bloku. Witaj przypisać użytkowników lub grupy będą mieli uprawnienia hello zdefiniowane przez hello wybranej roli dla tej aplikacji przedsiębiorstwa.

## <a name="next-steps"></a>Następne kroki
* [Wyświetl wszystkie moje grupy](active-directory-groups-view-azure-portal.md)
* [Usuń przypisanie użytkownika lub grupy z aplikacjami](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Wyłącz logowania użytkowników dla aplikacji przedsiębiorstwa](active-directory-coreapps-disable-app-azure-portal.md)
* [Zmiana nazwy hello lub logo aplikacji przedsiębiorstwa](active-directory-coreapps-change-app-logo-user-azure-portal.md)
