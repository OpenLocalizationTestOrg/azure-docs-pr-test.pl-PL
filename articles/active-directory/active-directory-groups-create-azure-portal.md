---
title: "aaaCreate grupę dla użytkowników w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toocreate grupy w usłudze Azure Active Directory i dodawanie członków grupy toohello"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>Utwórz grupy i Dodaj elementy członkowskie w usłudze Azure Active Directory
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](active-directory-groups-create-azure-portal.md)
> * [Klasyczna witryna Azure Portal](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

W tym artykule opisano sposób toocreate i wypełnić nową grupę w usłudze Azure Active Directory. Użyj zadań zarządzania tooperform grupy, takich jak przypisywanie licencji lub uprawnienia tooa liczby użytkowników lub urządzeń naraz.

## <a name="how-do-i-create-a-group"></a>Jak utworzyć grupę?
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.

   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. Na powitania **użytkowników i grup** bloku, wybierz opcję **wszystkich grup**.

   ![Otwieranie hello grup bloku](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. Na powitania **użytkowników i grup — wszystkie grupy** bloku, wybierz hello **Dodaj** polecenia.

   ![Polecenie Dodaj hello](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. Na powitania **grupy** bloku, Dodaj nazwę i opis grupy hello.
6. tooselect członków tooadd toohello grupy wybierz **przypisane** w hello **Typ członkostwa** , a następnie wybierz **członków**. Aby uzyskać więcej informacji o sposobie toomanage hello członkostwa w grupie dynamicznie, zobacz [przy użyciu atrybutów toocreate zaawansowane zasady członkostwa w grupie](active-directory-groups-dynamic-membership-azure-portal.md).

   ![Wybieranie elementów członkowskich tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. Na powitania **członków** bloku, wybierz jedną lub więcej użytkowników lub urządzeń grupy toohello tooadd i wybierz hello **wybierz** przycisk u dołu hello hello bloku tooadd ich toohello grupy. Witaj **użytkownika** filtry pole hello wyświetlania, w oparciu o dopasowanie wpisu z tooany część nazwy użytkownika lub urządzenia. Nie symbole wieloznaczne są akceptowane w tym polu.
8. Po zakończeniu dodawania elementów członkowskich toohello grupy, wybierz **Utwórz** na powitania **grupy** bloku.    

   ![Tworzenie grupy potwierdzenia](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zobacz istniejących grup](active-directory-groups-view-azure-portal.md)
* [Zarządzanie ustawieniami grupy](active-directory-groups-settings-azure-portal.md)
* [Elementy członkowskie grupy zarządzania](active-directory-groups-members-azure-portal.md)
* [Zarządzanie członkostwami grup](active-directory-groups-membership-azure-portal.md)
* [Dynamiczne reguły dla użytkowników w grupie zarządzania](active-directory-groups-dynamic-membership-azure-portal.md)
