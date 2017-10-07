---
title: "aaaAdd użytkowników z innych katalogów lub firm partnerskich w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak użytkownicy tooadd lub zmienić informacje o użytkowniku w usłudze Azure Active Directory, w tym gości i użytkowników zewnętrznych."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 564a04ec-53c1-470b-9ab9-f3db57da0a89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 92099e5792365c307b0f3d4f2dff5dd8424aeab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a>Dodawanie użytkowników z innych katalogów lub firm partnerskich w usłudze Azure Active Directory

W tym artykule opisano sposób tooadd użytkowników z innych katalogów w usłudze Azure Active Directory lub dodawania użytkowników z firm partnerskich. Aby uzyskać informacje dotyczące dodawania nowych użytkowników w organizacji i dodawanie użytkowników, którzy mają konta Microsoft, zobacz [Dodaj nowe tooAzure użytkowników usługi Active Directory](active-directory-create-users.md). 

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. Jak Centrum gości współpracy tooadd B2B w usłudze Azure AD Witaj, Administratorze dla [co to jest współpraca B2B usługi Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)

Dodano użytkownicy nie mają uprawnień administratora domyślnie, ale można przypisać toothem role w dowolnym momencie.

## <a name="add-a-user"></a>Dodawanie użytkownika
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz usługę **Active Directory**, a następnie otwórz swój katalog.
3. Wybierz hello **użytkowników** , a następnie na pasku poleceń hello, wybierz **Dodaj użytkownika**.
4. Na powitania **Poinformuj nas o tym użytkowniku** w obszarze **typ użytkownika**, wybierz opcję:

   * **Użytkownik w innym katalogu usługi Azure AD** — dodaje katalogu tooyour konta użytkownika, które pochodzi z innego katalogu usługi Azure AD. Możesz wybrać użytkownika w innym katalogu tylko wtedy, gdy również jesteś członkiem tego katalogu.
   * **Użytkownicy w firmach partnerskich** -tooinvite i autoryzowania partnera firmy użytkownicy tooyour katalogu (zobacz [współpracy usługi Azure Active Directory B2B](active-directory-b2b-what-is-azure-ad-b2b.md)). Będziesz potrzebować zbyt[przekazanie pliku CSV zawierającego adresy e-mail](active-directory-b2b-references-csv-file-format.md).
5. Na użytkownika hello **profilu** Podaj imię i nazwisko, nazwę przyjazną użytkownikowi i rolę użytkownika z hello **ról** listy. Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md). Określ, czy za**Włączanie uwierzytelniania wieloskładnikowego** hello użytkownika.
6. Na powitania **Uzyskaj hasło tymczasowe** wybierz pozycję **Utwórz**.

> [!IMPORTANT]
> Jeśli Twoja organizacja korzysta z więcej niż jedną domenę, musisz wiedzieć o hello następujące problemy podczas dodawania konta użytkownika:
>
> * tooadd kont użytkowników z hello tego samego główna nazwa użytkownika (UPN) między domenami, **pierwszy** dodać, na przykład geoffgrisso@contoso.onmicrosoft.com, **następuje** geoffgrisso@contoso.com.
> * **Nie** dodawaj adresu geoffgrisso@contoso.com przed dodaniem adresu geoffgrisso@contoso.onmicrosoft.com.
>

Jeśli zmienisz informacje dla użytkownika, którego tożsamość jest zsynchronizowana z lokalnej usługi Active Directory, nie można zmienić informacje o użytkowniku hello w hello klasycznego portalu Azure. toochange hello informacje o użytkowniku, użyj narzędzi zarządzania lokalnej usługi Active Directory.

## <a name="add-external-users"></a>Dodawanie użytkowników zewnętrznych
Możesz również dodać użytkowników z innej toowhich katalogu usługi Azure AD, której należysz, lub z firm partnerskich poprzez przekazanie pliku CSV. tooadd użytkownika zewnętrznego, dla **typ użytkownika**, określ **użytkownik w innym katalogu usługi Microsoft Azure AD** lub **użytkownicy w firmach partnerskich**.

Użytkownicy obu typów pochodzą z innego katalogu i są dodawani jako **użytkownicy zewnętrzni**. Użytkownicy zewnętrzni mogą współpracować z innymi użytkownikami w katalogu bez żadnych wymagań tooadd nowych kont i poświadczeń. Użytkownicy zewnętrzni są uwierzytelniani z katalogu macierzystego podczas rejestracji, a uwierzytelnianie działa w przypadku innych toowhich katalogi, które zostały dodane.

## <a name="external-user-management-and-limitations"></a>Zarządzanie użytkownikami zewnętrznymi i ograniczenia
Podczas dodawania użytkownika z innego katalogu tooyour katalogu, ten użytkownik jest użytkownika zewnętrznego w Twoim katalogu. Witaj, nazwa wyświetlana i nazwa użytkownika są kopiowane z katalogu macierzystego i używane do hello użytkownika zewnętrznego w Twoim katalogu. Następnie właściwości hello konta użytkownika zewnętrznego są całkowicie niezależne. Jeśli właściwość zmian toohello użytkownika w katalogu macierzystego, zmiany te nie są przenoszone toohello konta użytkownika zewnętrznego w Twoim katalogu.

jedyne połączenie dwóch kont hello Hello jest ten użytkownik hello zawsze jest uwierzytelniany względem swojego katalogu macierzystego lub za pomocą swojego konta Microsoft. Dlatego nie zobacz opcję tooreset hello hasła lub Włącz uwierzytelnianie wieloskładnikowe dla użytkowników zewnętrznych. Zasady uwierzytelniania hello hello katalogu macierzystego lub konta Microsoft jest obecnie hello tylko jeden, której wartość jest szacowana po zalogowaniu użytkownika hello.

> [!NOTE]
> Wciąż możesz zablokować użytkownika zewnętrznego hello w katalogu hello, która blokuje dostęp do katalogu tooyour.
>
>

Jeśli użytkownik zostanie usunięty z katalogu macierzystego lub anuluje swoje konta Microsoft, użytkownik zewnętrzny hello nadal istnieje w katalogu. Jednak hello użytkownika w katalogu nie dostępu do zasobów, ponieważ nie będzie mógł uwierzytelnić przy użyciu katalogu macierzystego ani konta Microsoft.

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a>Usługi obsługujące obecnie dostęp dla użytkowników zewnętrznych usługi Azure AD
* **Klasyczny portal Azure**: umożliwia użytkownikowi zewnętrznemu, który jest administratorem wielu katalogów toomanage każdego z nich.
* **Usługi SharePoint Online**: Jeśli udostępnianie zewnętrzne jest włączone, umożliwia tooaccess użytkowników zewnętrznych zasobów usługi SharePoint Online autoryzacji.
* **Dynamics CRM**: Jeśli hello użytkownik ma licencję za pomocą programu PowerShell, umożliwia użytkownikowi zewnętrznemu tooaccess autoryzowanych zasobów programu Dynamics CRM.
* **Dynamics AX**: Jeśli hello użytkownik ma licencję za pomocą programu PowerShell, umożliwia użytkownikowi zewnętrznemu tooaccess autoryzowanych zasobów programu Dynamics AX. Witaj ograniczenia dotyczące [użytkowników zewnętrznych usługi Azure AD](#known-limitations-of-azure-ad-external-users) użytkowników o tooexternal programu Dynamics AX również zastosować.

## <a name="next-steps"></a>Następne kroki
* [Dodaj nowy tooAzure użytkowników usługi Active Directory](active-directory-create-users.md)
* [Administrowanie usługą Azure AD](active-directory-administer.md)
* [Zarządzanie hasłami w usłudze Azure AD](active-directory-manage-passwords.md)
* [Zarządzanie grupami w usłudze Azure AD](active-directory-manage-groups.md)
