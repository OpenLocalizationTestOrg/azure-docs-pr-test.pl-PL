---
title: "Nowy aaaAdd tooAzure użytkowników usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooadd nowych użytkowników w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a>Szybki Start: Dodawanie nowych tooAzure użytkowników usługi Active Directory
W tym artykule opisano, jak tooadd nowych użytkowników w organizacji w hello Azure Active Directory (Azure AD) jeden za pomocą portalu Azure hello lub synchronizowanie użytkownika systemu Windows Server AD lokalnego konta danych. 

## <a name="add-cloud-based-users"></a>Dodaj użytkowników w chmurze
1. Zaloguj się toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **usługi Azure Active Directory** , a następnie **użytkowników i grup**.
3. Na powitania **użytkowników i grup** bloku, wybierz opcję **wszyscy użytkownicy**, a następnie wybierz **nowego użytkownika**.
   ![Polecenie Dodaj hello](./media/add-users-azure-active-directory/add-user.png)
4. Wprowadź szczegóły użytkownika hello, takich jak **nazwa** i **nazwy użytkownika**. Witaj nazwy użytkownika hello część nazwy domeny muszą zostać hello początkowej domyślnej domeny nazwa "[nazwa domeny].onmicrosoft.com" lub zweryfikowane, niefederacyjnych [niestandardowej nazwy domeny](add-custom-domain.md) takich jak "contoso.com".
5. Kopiowania lub w inny sposób hello Uwaga wygenerowane hasło użytkownika, dzięki czemu możesz podać go toohello użytkownika po zakończeniu tego procesu.
6. Opcjonalnie można otwierać i podanie informacji hello w hello **profilu** bloku, hello **grup** bloku lub hello **roli katalogu** bloku hello użytkownika. Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md).
7. Na powitania **użytkownika** bloku, wybierz opcję **Utwórz**.
8. Bezpiecznie należy rozpowszechnić hello wygenerowane hasło toohello nowego użytkownika, tak aby hello użytkownicy mogą się logować.

> [!TIP]
> Możesz także zsynchronizować dane konto użytkownika z lokalnego systemu Windows Server AD. Firmy Microsoft tożsamościach span lokalnych i chmurze możliwości tworzenia tożsamością jednego użytkownika do uwierzytelniania i autoryzacji zasobów tooall, bez względu na lokalizację. Nazywamy to tożsamość hybrydowa. [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) mogą być używane toointegrate katalogów lokalnych z usługą Azure Active Directory dla scenariuszy hybrydowych tożsamości. Dzięki temu tooprovide wspólną tożsamością dla użytkowników dla usługi Office 365, Azure i aplikacji SaaS zintegrowanych z usługą Azure AD. 

## <a name="delete-users-from-azure-ad"></a>Usuwanie użytkowników z usługi Azure AD
1. Zaloguj się toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **użytkowników i grup**.
3. Na powitania **użytkowników i grup** bloku, wybierz hello toodelete użytkownika z listy hello. 
4. W bloku hello hello wybranego użytkownika, wybierz **omówienie**, a następnie na pasku poleceń hello, wybierz **usunąć**.
   ![Polecenie Dodaj hello](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>Dowiedz się więcej 
* [Dodaj użytkownika zewnętrznego](active-directory-users-create-external-azure-portal.md)

* [Przypisz rolę użytkownika tooa w usługi Azure AD](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>Następne kroki
W tym szybkiego startu, kiedy znasz już jak tooadd nowych użytkowników tooAzure AD — wersja Premium. 

Możesz użyć hello poniższych łączy toocreate nowego użytkownika w usłudze Azure AD z hello portalu Azure.

> [!div class="nextstepaction"]
> [Dodaj użytkowników tooAzure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
