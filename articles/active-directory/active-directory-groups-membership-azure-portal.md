---
title: "Zarządzanie grupami w usłudze Azure Active Directory należy grupy | Dokumentacja firmy Microsoft"
description: "Grupy mogą zawierać inne grupy w usłudze Azure Active Directory. Oto jak zarządzać tymi członkostwa."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Zarządzania do grupy, które grupy należy w dzierżawie usługi Azure Active Directory
Grupy mogą zawierać inne grupy w usłudze Azure Active Directory. Oto jak zarządzać tymi członkostwa.

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a>Jak znaleźć Moja grupa jest członkiem grupy?
1. Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.
2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. Na **użytkowników i grup** bloku, wybierz opcję **wszystkich grup**.

   ![Otwieranie bloku grupy](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. Na **użytkowników i grup — wszystkie grupy** bloku, wybierz grupę.
5. Na **grupy - *groupname***  bloku, wybierz opcję **członkostw**.

   ![Otwieranie bloku członkostwa grupy](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. Aby dodać grupy jako członka innej grupy, na **Group - członkostw** bloku, wybierz opcję **Dodaj** polecenia.
7. Wybierz grupę z **Wybieranie grupy** bloku, a następnie wybierz **wybierz** przycisk w dolnej części bloku. Grupy można dodać tylko do jednej grupy naraz. **Użytkownika** okno filtry wyświetlania na podstawie zgodności wpis do dowolnej części nazwy użytkownika lub urządzenia. Nie symbole wieloznaczne są akceptowane w tym polu.

   ![Dodaj członkostwa w grupie](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. Aby usunąć grupy jako członka innej grupy, na **Group - członkostw** bloku, wybierz grupę.
9. Na ***groupname*** bloku, wybierz opcję **Usuń** polecenie i Potwierdź wybór w wierszu.

   ![Usuń polecenie członkostwa](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Po zakończeniu zmiany członkostwa w grupach dla Twojej grupy zaznacz **zapisać**.

## <a name="additional-information"></a>Dodatkowe informacje
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zobacz istniejących grup](active-directory-groups-view-azure-portal.md)
* [Utwórz nową grupę i dodawanie członków](active-directory-groups-create-azure-portal.md)
* [Zarządzanie ustawieniami grupy](active-directory-groups-settings-azure-portal.md)
* [Elementy członkowskie grupy zarządzania](active-directory-groups-members-azure-portal.md)
* [Dynamiczne reguły dla użytkowników w grupie zarządzania](active-directory-groups-dynamic-membership-azure-portal.md)
