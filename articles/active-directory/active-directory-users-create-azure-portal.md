---
title: "Dodawanie nowych użytkowników do usługi Azure Active Directory | Microsoft Docs"
description: "Wyjaśnia, jak dodać nowych użytkowników lub zmienić informacje o użytkowniku w usłudze Azure Active Directory."
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
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a>Dodawanie nowych użytkowników do usługi Azure Active Directory
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](active-directory-users-create-azure-portal.md)
> * [Klasyczna witryna Azure Portal](active-directory-create-users.md)
>
>

W tym artykule opisano sposób dodawania nowych użytkowników w organizacji w usłudze Azure Active Directory (Azure AD). 

1. Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.
2. Wybierz **więcej usług**, wprowadź **użytkowników i grup** w polu tekstowym, a następnie wybierz **Enter**.

   ![Otwieranie użytkowników i grup](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. Na **użytkowników i grup** bloku, wybierz opcję **wszyscy użytkownicy**, a następnie wybierz **Dodaj**.

   ![Dodaj polecenie](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. Wprowadź szczegóły użytkownika, takich jak **nazwa** i **nazwy użytkownika**. Część nazwy domeny nazwa użytkownika musi być domyślna początkowej nazwy domeny "foo.onmicrosoft.com" nazwa domeny lub nazwę domeny zweryfikowane, niefederacyjnych, takie jak "contoso.com".
5. Skopiuj lub w przeciwnym razie należy pamiętać wygenerowane hasło, dzięki czemu można udostępnić go użytkownikowi po zakończeniu tego procesu.
6. Opcjonalnie można otwierać i Wypełnij informacje w **profilu** bloku **grup** bloku lub **roli katalogu** bloku dla użytkownika. Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md).
7. Na **użytkownika** bloku, wybierz opcję **Utwórz**.
8. Bezpiecznie dystrybucji wygenerowane hasło dla nowego użytkownika, dzięki czemu użytkownicy mogą się logować.

### <a name="next-steps"></a>Następne kroki
* [Dodaj użytkownika zewnętrznego](active-directory-users-create-external-azure-portal.md)
* [Resetuj hasło użytkownika w portalu Azure](active-directory-users-reset-password-azure-portal.md)
* [Zmień informacje dotyczące pracy użytkownika](active-directory-users-work-info-azure-portal.md)
* [Zarządzanie profilami użytkowników](active-directory-users-profile-azure-portal.md)
* [Usunięcie użytkownika w usługi Azure AD](active-directory-users-delete-user-azure-portal.md)
* [Przypisanie użytkownika do roli w usługi Azure AD](active-directory-users-assign-role-azure-portal.md)
