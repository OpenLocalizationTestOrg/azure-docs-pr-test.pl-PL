---
title: "przydziały dostępu do zasobów platformy Azure aaaView | Dokumentacja firmy Microsoft"
description: "Wyświetl i zarządzaj nimi wszystkie hello przypisania opartej na rolach kontroli dostępu dla dowolnego użytkownika lub grupę w hello portalu Azure"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a>Wyświetl przypisania dostępu dla użytkowników i grup w hello portalu Azure
> [!div class="op_single_selector"]
> * [Zarządzanie dostępem użytkowników lub grup](role-based-access-control-manage-assignments.md)
> * [Zarządzanie dostępem do zasobów](role-based-access-control-configure.md)

Kontrola dostępu oparta na rolach (RBAC) w hello Azure Active Directory (Azure AD), można zarządzać access tooyour Azure zasobów. 

Dostęp z RBAC przypisaną jest szczegółowych, ponieważ można ograniczyć uprawnienia hello na dwa sposoby:

* **Zakres:** przypisania roli RBAC są zakresami tooa określonej subskrypcji, grupy zasobów lub zasobów. Podana pojedynczego zasobu tooa dostępu przez użytkownika nie może uzyskać dostępu żadnych innych zasobów w hello tej samej subskrypcji.
* **Rola:** zakresu hello przypisania hello jest zawężony dostępu nawet dalsze przez przypisanie roli. Role można wysokiego poziomu, takich jak właściciela lub określonych, takich jak czytnik maszyny wirtualnej.

Role można przypisać tylko z wewnątrz hello subskrypcji, grupy zasobów lub zasobu, który jest zakresem hello hello przypisania. Jednak można wyświetlić wszystkie przypisania dostępu powitania dla danego użytkownika lub grupy w jednym miejscu. Użytkownik może zawierać maksymalnie too2000 przypisania roli w każdej subskrypcji. 

Uzyskaj więcej informacji o tym, jak za[Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](role-based-access-control-configure.md).

## <a name="view-access-assignments"></a>Wyświetl dostępu przypisania
toolook się hello przypisań dostępu dla jednego użytkownika lub grupę, uruchom w usłudze Azure Active Directory w hello [portalu Azure](http://portal.azure.com).

1. Wybierz **usługi Azure Active Directory**. Jeśli ta opcja nie jest widoczna na liście nawigacji, wybierz **więcej usług** , a następnie przewiń w dół toofind **usługi Azure Active Directory**.
2. Wybierz **użytkowników i grup**, a następnie albo **wszyscy użytkownicy** lub **wszystkich grup**. Na przykład możemy skupić się na poszczególnych użytkowników.
    ![Zarządzaj użytkownikami i grupami w usłudze Azure Active Directory — zrzut ekranu](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)
3. Wyszukiwanie hello użytkownika według nazwy lub nazwy użytkownika.
4. Wybierz **zasobów Azure** na powitania użytkownika bloku. Są wyświetlane wszystkie hello przypisania dostępu dla tego użytkownika.

### <a name="read-permissions-tooview-assignments"></a>Przydziały tooview uprawnienia do odczytu
Ta strona zawiera tylko przypisania dostępu hello czy masz uprawnienie tooread. Na przykład mieć dostęp do odczytu toosubscription A i przejdź toocheck bloku zasobów Azure toohello przypisania użytkownika. Można wyświetlać swoje przydziały dostępu dla subskrypcji A, ale nie widzi ona również ma dostęp do przypisania na subskrypcji B.

## <a name="delete-access-assignments"></a>Usuwanie przypisania dostępu
Z tego bloku można usunąć przypisania dostępu, które zostały przypisane bezpośrednio tooa użytkownika lub grupy. Jeśli przypisanie dostępu hello została odziedziczona z grupy nadrzędnej, wymaga toogo toohello zasobów lub subskrypcji i zarządzanie hello przypisania.

1. Z listy hello wszystkie hello przypisania dostępu dla użytkownika lub grupy wybierz hello, co ma toodelete.
2. Wybierz **Usuń** , a następnie **tak** tooconfirm.
    ![Usuń przypisanie dostępu — zrzut ekranu](./media/role-based-access-control-manage-assignments/delete_assignment.png)

## <a name="next-steps"></a>Następne kroki

* Rozpoczynanie pracy z kontroli dostępu opartej na rolach zbyt[Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](role-based-access-control-configure.md)
* Zobacz hello [wbudowane role RBAC](role-based-access-built-in-roles.md)

