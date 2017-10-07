---
title: "aaaManage hello członków grupy w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooadd lub usuwanie użytkowników i urządzeń z grupy w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a>Zarządzanie członkostwami grup użytkowników w dzierżawie usługi Azure Active Directory
W tym artykule opisano, jak toomanage hello członków grupy w usłudze Azure Active Directory (Azure AD).

## <a name="how-do-i-find-hello-members-and-manage-them"></a>Jak znaleźć członków hello i zarządzać nimi?
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. Na powitania **użytkowników i grup** bloku, wybierz opcję **wszystkich grup**.

   ![Otwieranie hello grup bloku](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. Na powitania **użytkowników i grup — wszystkie grupy** bloku, wybierz grupę.
5. Na powitania **grupy - *groupname***  bloku, wybierz opcję **członków**.

   ![Otwieranie hello członków bloku](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. tooadd grupy toohello elementy członkowskie, na powitania **grupy - członków** bloku, wybierz opcję **Dodaj członków**.

   ![Dodaj polecenie elementy członkowskie](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. Na powitania **członków** bloku, wybierz jedną lub więcej użytkowników lub urządzeń grupy toohello tooadd i wybierz hello **wybierz** przycisk u dołu hello hello bloku tooadd ich toohello grupy. Witaj **użytkownika** filtry pole hello wyświetlania, w oparciu o dopasowanie wpisu z tooany część nazwy użytkownika lub urządzenia. Nie symbole wieloznaczne są akceptowane w tym polu.
8. tooremove członków z grupy hello na powitania **grupy - członków** bloku, wybierz element członkowski.
9. Na powitania ***membername*** bloku, wybierz hello **Usuń** polecenie i Potwierdź wybór hello w wierszu.

   ![Usuń elementy członkowskie, polecenie](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. Po zakończeniu zmiana członków grupy hello, wybierz **zapisać**.

## <a name="additional-information"></a>Dodatkowe informacje
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zobacz istniejących grup](active-directory-groups-view-azure-portal.md)
* [Utwórz nową grupę i dodawanie członków](active-directory-groups-create-azure-portal.md)
* [Zarządzanie ustawieniami grupy](active-directory-groups-settings-azure-portal.md)
* [Zarządzanie członkostwami grup](active-directory-groups-membership-azure-portal.md)
* [Dynamiczne reguły dla użytkowników w grupie zarządzania](active-directory-groups-dynamic-membership-azure-portal.md)
