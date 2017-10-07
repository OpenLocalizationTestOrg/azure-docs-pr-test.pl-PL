---
title: "Nowy aaaAdd tooAzure użytkowników usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooadd nowych użytkowników lub zmienić informacje o użytkowniku w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a>Dodawanie nowych użytkowników lub użytkownicy z Microsoft tooAzure kont usługi Active Directory
Dodaj użytkowników toopopulate katalogu. W tym artykule opisano sposób tooadd nowych użytkowników w organizacji, jak i tooadd użytkowników, którzy mają konta Microsoft. Aby uzyskać więcej informacji na temat dodawania użytkowników z innych katalogów w usłudze Azure Active Directory lub dodawania użytkowników z firm partnerskich, zobacz [Dodawanie użytkowników z innych katalogów lub firm partnerskich w usłudze Azure Active Directory](active-directory-create-users-external.md). Dodano użytkownicy nie mają uprawnień administratora domyślnie, ale można przypisać toothem role w dowolnym momencie.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. Dla tooadd użytkownika w Centrum administracyjnym hello Azure AD, zobacz temat [Dodaj nowe tooAzure użytkowników usługi Active Directory](active-directory-users-create-azure-portal.md).

## <a name="add-a-user"></a>Dodawanie użytkownika
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **usługi Active Directory**, a następnie wybierz nazwę hello katalogu organizacji.
3. Wybierz hello **użytkowników** , a następnie na pasku poleceń hello, wybierz **Dodaj użytkownika**.
4. Na powitania **Poinformuj nas o tym użytkowniku** w obszarze **typ użytkownika**, wybierz opcję:

   * **Nowy użytkownik w organizacji** — dodaje nowe konto użytkownika w katalogu.
   * **Użytkownik z istniejącym kontem Microsoft** — dodaje istniejące Microsoft konsumenta konta tooyour katalog (na przykład konto programu Outlook)
5. W zależności od **typu użytkownika** wprowadź nazwę użytkownika (dla nowego użytkownika) lub adres e-mail (dla użytkownika z kontem Microsoft).
6. Na użytkownika hello **profilu** Podaj imię i nazwisko, nazwę przyjazną użytkownikowi i rolę użytkownika z hello **ról** listy. Aby uzyskać więcej informacji dotyczących ról użytkowników i administratorów, zobacz [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md). Określ, czy za**Włączanie uwierzytelniania wieloskładnikowego** hello użytkownika.
7. Na powitania **Uzyskaj hasło tymczasowe** wybierz pozycję **Utwórz**.

> [!IMPORTANT]
> Jeśli Twoja organizacja korzysta z więcej niż jedną domenę, musisz wiedzieć o hello następujące problemy podczas dodawania konta użytkownika:
>
> * tooadd kont użytkowników z hello tego samego główna nazwa użytkownika (UPN) między domenami, **pierwszy** dodać, na przykład geoffgrisso@contoso.onmicrosoft.com, **następuje** geoffgrisso@contoso.com.
> * **Nie** dodawaj adresu geoffgrisso@contoso.com przed dodaniem adresu geoffgrisso@contoso.onmicrosoft.com. To zamówienie jest ważne i może być skomplikowane tooundo.
>
>

## <a name="change-user-information"></a>Zmiana informacji o użytkowniku
Możesz zmienić dowolny atrybut użytkownika, z wyjątkiem identyfikatora obiektu hello.

1. Otwórz katalog.
2. Wybierz hello **użytkowników** kartę i hello następnie wybierz nazwę wyświetlaną użytkownika ma toochange hello.
3. Wprowadź zmiany, a następnie kliknij przycisk **Zapisz**.

Jeśli użytkownik hello, który chcesz zmienić jest synchronizowane z lokalnej usługi Active Directory, nie można zmienić informacje o użytkowniku hello za pomocą tej procedury. toochange hello użytkownika, użyj narzędzi zarządzania lokalnej usługi Active Directory.

## <a name="guest-user-management-and-limitations"></a>Zarządzanie użytkownikami typu Gość i ograniczenia
Konta gościa korzystają użytkownicy z innych katalogów, którzy byli dokumentów programu SharePoint tooaccess katalogu zaproszonych tooyour, aplikacji lub innych zasobów platformy Azure. Konto gościa w katalogu ma jego podstawowy atrybut UserType ustawiona zbyt "Gość." Normalnych użytkowników (w szczególności członków katalogu) ma atrybut UserType hello "Członek".

Goście mają ograniczony zestaw praw w katalogu hello. Te prawa ograniczają możliwość hello gości toodiscover informacji o innych użytkowników w katalogu hello. Jednak gościa nadal interakcji użytkowników z hello użytkownikami i grupami skojarzonymi z zasobami hello, nad którymi pracuje. Goście mogą:

* Wyświetlać innych użytkowników i grup skojarzonych z toowhich subskrypcji platformy Azure, w których są przydzielone
* Zobacz hello członkami toowhich grup, do których należą
* Wyszukiwać innych użytkowników w katalogu hello, jeśli znają hello pełny adres e-mail użytkownika, powitalne
* Zobaczyć tylko ograniczony zestaw atrybutów użytkowników hello, ich wyszukiwanie — ograniczone toodisplay nazwa, adres e-mail, główna nazwa użytkownika (UPN) i miniatury zdjęcia
* Pobierz listę zweryfikowanych domen w katalogu hello
* Tooapplications zgody, przyznania im hello takie same prawa dostępu, jakie mają członkowie w katalogu

## <a name="set-guest-user-access-policies"></a>Ustawianie zasad dostępu dla gościa
Witaj **Konfiguruj** karta katalogu zawiera opcje toocontrol dostępu dla gości. Te opcje mogą zostać zmienione wyłącznie za pośrednictwem klasycznego portalu Azure przez globalnego administratora katalogu. Obecnie nie ma metody robienia tego przez interfejs API lub program PowerShell.

tooopen hello **Konfiguruj** karcie hello Azure klasycznym portalu, wybierz **usługi Active Directory**, a następnie wybierz nazwę hello hello katalogu.

![Karta Konfigurowanie w usłudze Azure Active Directory][1]

Następnie można edytować hello opcje toocontrol dostępu dla gości.

![Opcje kontroli dostępu dla gości][2]

## <a name="whats-next"></a>Co dalej
* [Dodawanie użytkowników z innych katalogów lub firm partnerskich w usłudze Azure Active Directory](active-directory-create-users-external.md)
* [Administrowanie usługą Azure AD](active-directory-administer.md)
* [Zarządzanie hasłami w usłudze Azure AD](active-directory-manage-passwords.md)
* [Zarządzanie grupami w usłudze Azure AD](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
