---
title: "aaaHow toogive dostępu tooPrivileged Identity Management - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd toousers ról z hello rozszerzenia usługi Azure Active Directory Privileged Identity Management, którymi zarządzają usługi PIM."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a>Nadanie toomanage dostępu do usługi Azure AD Privileged Identity Management
dostęp tooPIM Hello administrator globalny, który automatycznie włącza Azure AD Privileged Identity Management (PIM) dla organizacji oraz uzyskać przypisań ról. Nikt pobiera zapisu domyślnie, łącznie z innych administratorów globalnych. Inne globalne Administratorzy, administratorów zabezpieczeń i czytników zabezpieczeń mają dostęp tylko do odczytu tooAzure AD PIM. toogive tooPIM dostępu, hello pierwszego użytkownika można przypisywać innym użytkownikom toohello **administrator ról uprzywilejowanych** roli. Ten przydział musi być wykonywane za pomocą programu PIM się i nie można zmienić za pomocą programu PowerShell lub innych portalach.

> [!NOTE]
> Zarządzanie programem Azure AD PIM wymaga usługi Azure MFA. Ponieważ konta Microsoft nie można zarejestrować dla usługi Azure MFA, użytkownik, który zaloguje się za pomocą konta Microsoft nie może uzyskać dostępu usługi Azure AD PIM.
> 
> 

Upewnij się, zawsze istnieją co najmniej dwóch użytkowników należących do roli administrator ról uprzywilejowanych w przypadku, gdy jeden użytkownik jest zablokowany lub ich konto zostało usunięte.

## <a name="give-another-user-access-toomanage-pim"></a>Nadaj innego toomanage dostępu użytkownika PIM
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/) i wybierz hello **Azure AD Privileged Identity Management** aplikacji hello pulpitu nawigacyjnego.
2. Wybierz **Zarządzanie ról uprzywilejowanych** > **administrator ról uprzywilejowanych** > **Dodaj**.
   
    ![Dodawanie ról uprzywilejowanych administratorów — zrzut ekranu][1]
3. W bloku użytkowników zarządzanych Dodaj hello krok 1 została już ukończona. Zaznacz krok 2, **Wybierz użytkowników** i wyszukiwania dla użytkownika hello ma tooadd.
   
    ![Wybierz użytkowników — zrzut ekranu][2]
4. Wybierz użytkownika hello z hello wyniki wyszukiwania, a następnie kliknij przycisk **gotowe**.
5. Kliknij przycisk **OK** toosave wybór. Hello użytkownika, który wybrano będzie wyświetlana na liście hello ról uprzywilejowanych administratorów.
   
   * Gdy przypisujesz nowy toosomeone roli one są automatycznie konfigurowane jako rola hello tooactivate kwalifikujących się. Jeśli chcesz, aby toomake ich stałe w roli powitania kliknij użytkownika hello na liście hello. Wybierz **upewnij uprawnienie** hello użytkownika informacje menu.
6. Wyślij łącze użytkownika hello zbyt[wprowadzenie do korzystania z usługi Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).

## <a name="remove-another-users-access-rights-for-managing-pim"></a>Usuwanie praw dostępu przez innego użytkownika do zarządzania usługi PIM
Zawsze przed usunięciem ktoś z hello administratorem ról uprzywilejowanych, upewnij się, nadal będą przypisanych tooit dwóch użytkowników.

1. Na pulpicie nawigacyjnym usługi PIM hello, kliknij na powitania roli **administrator ról uprzywilejowanych**.  zostanie wyświetlona lista Hello użytkowników obecnie w tej roli.
2. Polecenie hello użytkownika na liście użytkowników hello.
3. Polecenie **Usuń**.  Otrzymasz komunikat potwierdzenia.
4. Kliknij przycisk **tak** tooremove hello użytkownika z roli hello.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
