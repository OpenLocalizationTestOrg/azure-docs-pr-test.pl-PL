---
title: "grupy hello aaaManage grupy należy tooin usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Grupy mogą zawierać inne grupy w usłudze Azure Active Directory. Oto jak toomanage tych członkostwa."
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
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Zarządzanie grupami toowhich, do której należy grupa w dzierżawie usługi Azure Active Directory
Grupy mogą zawierać inne grupy w usłudze Azure Active Directory. Oto jak toomanage tych członkostwa.

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a>Jak znaleźć Moja grupa jest członkiem grupy hello?
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. Na powitania **użytkowników i grup** bloku, wybierz opcję **wszystkich grup**.

   ![Otwieranie hello grup bloku](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. Na powitania **użytkowników i grup — wszystkie grupy** bloku, wybierz grupę.
5. Na powitania **grupy - *groupname***  bloku, wybierz opcję **członkostw**.

   ![Otwieranie hello grupy członkostwa w bloku](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. tooadd grupy jako członka innej grupy, na powitania **Group - członkostw** bloku, wybierz hello **Dodaj** polecenia.
7. Wybierz grupę z hello **Wybieranie grupy** bloku, a następnie wybierz opcję hello **wybierz** przycisk u dołu hello hello bloku. Można dodać grupy tooonly jednej grupy naraz. Witaj **użytkownika** filtry pole hello wyświetlania, w oparciu o dopasowanie wpisu z tooany część nazwy użytkownika lub urządzenia. Nie symbole wieloznaczne są akceptowane w tym polu.

   ![Dodaj członkostwa w grupie](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. tooremove grupy jako członka innej grupy, na powitania **Group - członkostw** bloku, wybierz grupę.
9. Na powitania ***groupname*** bloku, wybierz hello **Usuń** polecenie i Potwierdź wybór hello w wierszu.

   ![Usuń polecenie członkostwa](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Po zakończeniu zmiany członkostwa w grupach dla Twojej grupy zaznacz **zapisać**.

## <a name="additional-information"></a>Dodatkowe informacje
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zobacz istniejących grup](active-directory-groups-view-azure-portal.md)
* [Utwórz nową grupę i dodawanie członków](active-directory-groups-create-azure-portal.md)
* [Zarządzanie ustawieniami grupy](active-directory-groups-settings-azure-portal.md)
* [Elementy członkowskie grupy zarządzania](active-directory-groups-members-azure-portal.md)
* [Dynamiczne reguły dla użytkowników w grupie zarządzania](active-directory-groups-dynamic-membership-azure-portal.md)
