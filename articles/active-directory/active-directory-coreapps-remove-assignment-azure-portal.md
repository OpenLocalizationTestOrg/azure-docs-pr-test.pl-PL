---
title: "aaaRemove użytkownika lub grupę przypisania z aplikacji przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooremove hello dostępu przypisania użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a>Usuń przypisanie użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory
Jest łatwy tooremove użytkownika lub grupę z przypisaniem tooone dostępu do aplikacji w sieci przedsiębiorstwa w usłudze Azure Active Directory (Azure AD). Musi mieć hello odpowiednie uprawnienia toomanage hello przedsiębiorstwa aplikacji, a musi być administratorem globalnym katalogu hello.

## <a name="how-do-i-remove-a-user-or-group-assignment"></a>Jak usunąć użytkownika lub przypisanie do grupy
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w hello pola tekstowego, a następnie wybierz **Enter**.
3. Na powitania **usługi Azure Active Directory - *directoryname***  bloku (to znaczy bloku hello Azure AD dla katalogu hello są używane do zarządzania), wybierz **aplikacje dla przedsiębiorstw**.

    ![Otwieranie aplikacji przedsiębiorstwa](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. Na powitania **aplikacje dla przedsiębiorstw** bloku, wybierz opcję **wszystkie aplikacje**. Zobaczysz listę aplikacji hello, którymi można zarządzać.
5. Na powitania **aplikacje przedsiębiorstwa — wszystkie aplikacje** bloku, wybierz aplikację.
6. Na powitania ***appname*** bloku (to znaczy hello bloku o nazwie hello hello wybranej aplikacji w tytule hello) wybierz **użytkownicy i grupy**.

    ![Wybieranie użytkowników lub grup](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. Na powitania ***appname*** **— przypisanie do grupy & użytkownika** bloku, wybierz jedną więcej użytkowników lub grup, a następnie wybierz hello **Usuń** polecenia. Potwierdź decyzję hello w wierszu.

    ![Polecenie Usuń hello](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a>Następne kroki
* [Wyświetl wszystkie moje grupy](active-directory-groups-view-azure-portal.md)
* [Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](active-directory-coreapps-assign-user-azure-portal.md)
* [Wyłącz logowania użytkowników dla aplikacji przedsiębiorstwa](active-directory-coreapps-disable-app-azure-portal.md)
* [Zmiana nazwy hello lub logo aplikacji przedsiębiorstwa](active-directory-coreapps-change-app-logo-user-azure-portal.md)
