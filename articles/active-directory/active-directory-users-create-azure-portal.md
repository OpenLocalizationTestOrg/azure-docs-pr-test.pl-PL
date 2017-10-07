---
title: "Nowy aaaAdd tooAzure użytkowników usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooadd nowych użytkowników lub zmienić informacje o użytkowniku w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: c4a156ea31b81202bb0d0ac224afbfc3f1785532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-tooazure-active-directory"></a>Dodaj nowy tooAzure użytkowników usługi Active Directory
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](active-directory-users-create-azure-portal.md)
> * [Klasyczna witryna Azure Portal](active-directory-create-users.md)
>
>

W tym artykule opisano, jak tooadd nowych użytkowników w organizacji w hello Azure Active Directory (Azure AD). 

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.

   ![Otwieranie użytkowników i grup](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. Na powitania **użytkowników i grup** bloku, wybierz opcję **wszyscy użytkownicy**, a następnie wybierz **Dodaj**.

   ![Polecenie Dodaj hello](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. Wprowadź szczegóły użytkownika hello, takich jak **nazwa** i **nazwy użytkownika**. części nazwy domeny Hello hello nazwa użytkownika musi być nazwa domeny "foo.onmicrosoft.com" nazwy domeny początkowej domyślne hello lub nazwę domeny zweryfikowane, niefederacyjnych, takie jak "contoso.com".
5. Kopiowania lub w inny sposób hello Uwaga wygenerowane hasło użytkownika, dzięki czemu możesz podać go toohello użytkownika po zakończeniu tego procesu.
6. Opcjonalnie można otwierać i podanie informacji hello w hello **profilu** bloku, hello **grup** bloku lub hello **roli katalogu** bloku hello użytkownika. Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md).
7. Na powitania **użytkownika** bloku, wybierz opcję **Utwórz**.
8. Bezpiecznie należy rozpowszechnić hello wygenerowane hasło toohello nowego użytkownika, tak aby hello użytkownicy mogą się logować.

### <a name="next-steps"></a>Następne kroki
* [Dodaj użytkownika zewnętrznego](active-directory-users-create-external-azure-portal.md)
* [Resetuj hasło użytkownika w hello nowego portalu Azure](active-directory-users-reset-password-azure-portal.md)
* [Zmień informacje dotyczące pracy użytkownika](active-directory-users-work-info-azure-portal.md)
* [Zarządzanie profilami użytkowników](active-directory-users-profile-azure-portal.md)
* [Usunięcie użytkownika w usługi Azure AD](active-directory-users-delete-user-azure-portal.md)
* [Przypisz rolę użytkownika tooa w usługi Azure AD](active-directory-users-assign-role-azure-portal.md)
