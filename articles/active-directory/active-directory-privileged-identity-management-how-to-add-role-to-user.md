---
title: "aaaHow tooadd lub usunąć rolę użytkownika | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd ról tooprivileged tożsamości z hello aplikacji usługi Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: f84639757dd76061ea12ed6ea7ec9e62ad942109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a>Azure AD Privileged Identity Management: Jak tooadd lub usunąć rolę użytkownika
Z usługi Azure Active Directory (AD), administrator globalny (lub administrator firmy) można aktualizować której użytkownicy są **trwale** przypisane tooroles w usłudze Azure AD. Jest to zrobić za pomocą poleceń cmdlet programu PowerShell, takie jak `Add-MsolRoleMember` i `Remove-MsolRoleMember`. Można też używać hello klasycznego portalu Azure, zgodnie z opisem w [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles.md).

Witaj aplikacji Azure AD Privileged Identity Management administratorom ról uprzywilejowanych przypisań ról stałe toomake, jak również. Ponadto administratorzy ról uprzywilejowanych ułatwia użytkownikom **kwalifikujących się** dla ról administratora. Administrator kwalifikujących się aktywować rolę hello podczas potrzebują, a następnie ich uprawnienia wygasają po ich wszystko gotowe.

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a>Zarządzanie rolami PIM w hello portalu Azure
W organizacji można przypisywać użytkowników toodifferent role administracyjne w usłudze Azure AD, Office 365 i innych usług firmy Microsoft i aplikacji.  Więcej informacji na temat hello dostępnych ról można znaleźć w folderze [role w programie Azure AD PIM](active-directory-privileged-identity-management-roles.md).

tooadd lub Usuń użytkownika z rolą przy użyciu Privileged Identity Management, wyświetlić pulpit nawigacyjny PIM hello. A następnie kliknij przycisk hello **użytkownicy o rolach administratora** przycisk lub wybierz określoną rolę (na przykład Administrator globalny) z tabeli ról hello.

> [!NOTE]
> Jeśli nie włączono jeszcze usługi PIM w hello portalu Azure, przejdź zbyt[wprowadzenie do usługi Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) szczegółowe informacje.

Jeśli chcesz toogive innego tooPIM dostępu użytkownika samego hello ról, które wymaga PIM toohave użytkownika hello są opisane dalej w [jak toogive dostępu tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="add-a-user-tooa-role"></a>Dodaj rolę tooa użytkownika
1. W hello [portalu Azure](https://portal.azure.com/), wybierz pozycję hello **Azure AD Privileged Identity Management** kafelka na pulpicie nawigacyjnym hello.
2. Wybierz **Zarządzanie ról uprzywilejowanych**.
3. W hello **Podsumowanie ról** tabeli, wybierz hello roli ma toomanage.
4. W bloku roli hello, wybierz **Dodaj**.
5. Kliknij przycisk **Wybierz użytkowników** i Wyszukaj użytkownika hello na powitania **Wybierz użytkowników** bloku.  
6. Wybierz z listy wyników wyszukiwania hello hello użytkownika, a następnie kliknij przycisk **gotowe**.
7. Kliknij przycisk **OK** toosave wybór. Hello użytkownika, który wybrano będą wyświetlane na liście hello jako kwalifikujący się do roli hello.

> [!NOTE]
> Nowi użytkownicy z rolą tylko kwalifikują się do roli hello domyślnie. Rola hello toomake stałe, kliknij przycisk użytkownika hello na liście hello. informacje o użytkowniku Hello będą wyświetlane w nowym bloku. Wybierz **Sprawdź uprawnienie** hello użytkownika informacje menu.  
> Jeśli użytkownik nie można zarejestrować usługi Azure Multi-Factor Authentication (MFA) lub korzystanie z konta Microsoft (zazwyczaj @outlook.com), należy toomake ich stałe w ich ról. Administratorzy kwalifikujących się monit tooregister dla usługi MFA podczas aktywacji.

Teraz, hello jest uprawniona do roli użytkownika, daj znać, aby aktywować go zgodnie z instrukcjami toohello [jak tooactivate lub dezaktywować rolę](active-directory-privileged-identity-management-how-to-activate-role.md).

## <a name="remove-a-user-from-a-role"></a>Usuwa użytkownika z roli
Możesz usunąć użytkowników z przypisania ról kwalifikujących się, ale upewnij się, że zawsze jest co najmniej jednego użytkownika, który jest stały administratora globalnego.

Wykonaj te kroki tooremove określonego użytkownika z roli:

1. Przejdź roli toohello liście roli powitania po wybraniu roli na pulpicie nawigacyjnym usługi Azure AD PIM hello lub klikając hello **użytkownicy o rolach administratora** przycisku.
2. Polecenie hello użytkownika na liście użytkowników hello.
3. Kliknij przycisk **Usuń**. Komunikat poproś tooconfirm.
4. Kliknij przycisk **tak** tooremove hello roli użytkownika hello.

Jeśli nie masz pewności, którzy użytkownicy nadal muszą ich przypisania ról, a następnie możesz [rozpocząć Przegląd dostępu dla roli hello](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

