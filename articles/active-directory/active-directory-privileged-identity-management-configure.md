---
title: "Konfigurowanie usługi Azure AD Privileged Identity Management | Dokumentacja firmy Microsoft"
description: "Temat, który objaśnia, co to jest Azure AD Privileged Identity Management i sposobu użycia usługi PIM, aby zwiększyć bezpieczeństwo chmury."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: eb7059368cb80be7dd625f9dc6ad2aab1bad709a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>Co to jest Azure AD Privileged Identity Management?
Aplikacja Azure Active Directory (AD) Privileged Identity Management umożliwia kontrolę i monitorowanie dostępu, a także zarządzanie nim w ramach danej organizacji. Dotyczy to również dostępu do zasobów usługi Azure AD i innych usług online firmy Microsoft, takich jak Office 365 lub Microsoft Intune.  

> [!NOTE]
> Zarządzanie tożsamościami uprzywilejowanymi jest dostępne w całej organizacji, gdy licencji Administratorzy w Twojej organizacji z usługi Azure Active Directory w wersji Premium P2. Aby uzyskać więcej informacji, zobacz [Wersje usługi Azure Active Directory](active-directory-editions.md).

Organizacje chcesz ograniczyć liczbę użytkowników, którzy mają dostęp do informacji o lub zasobów, ponieważ, która ogranicza ryzyko złośliwemu użytkownikowi uzyskiwanie dostępu. Użytkownicy nadal muszą mieć jednak do wykonania uprzywilejowanych operacji w aplikacji Azure, Office 365 lub SaaS. Organizacje nadaj uprzywilejowanego dostępu użytkowników w usłudze Azure AD bez monitorowania, co robią tych użytkowników, używając swoich uprawnień administratora. Azure AD Privileged Identity Management pomaga rozwiązywać to ryzyko.  

Azure AD Privileged Identity Management pomaga:  

* Zobacz użytkowników, którzy są administratorami usługi Azure AD
* Włącz na żądanie "just in time" dostęp administracyjny do usługi Online firmy Microsoft, takich jak Office 365 i Intune
* Uzyskaj raporty dotyczące historii dostępu administratora i zmian w przypisaniach administratora
* Uzyskiwanie alertów dotyczących dostępu do ról uprzywilejowanych
* Wymagaj zatwierdzenia aktywacji (wersja zapoznawcza)

Azure AD Privileged Identity Management, można zarządzać wbudowanych ról organizacyjnych usługi Azure AD, w tym (między innymi):  

* Administrator globalny
* Administrator rozliczeń
* Administrator usługi  
* Administrator użytkowników
* Administrator haseł

## <a name="just-in-time-administrator-access"></a>Tylko w czasie dostępu administratora
W przeszłości można przypisać użytkownika do roli administratora za pośrednictwem klasycznego portalu Azure lub programu Windows PowerShell. W związku z tym staje się **administrator trwały**, zawsze aktywny w przypisanej roli. Azure AD Privileged Identity Management pojęcia związane z **kwalifikujących się administrator**. Kwalifikujące się Administratorzy powinni mieć użytkowników, które wymagają uprzywilejowanego dostępu teraz, a następnie, ale nie każdego dnia. Rola jest nieaktywny, dopóki użytkownik będzie potrzebował dostępu, a następnie zakończyć proces aktywacji i stają się aktywne administratora dla wstępnie określoną ilość czasu.

## <a name="enable-privileged-identity-management-for-your-directory"></a>Włącz zarządzanie tożsamościami uprzywilejowanymi dla katalogu
Możesz rozpocząć korzystanie z usługi Azure AD Privileged Identity Management w [portalu Azure](https://portal.azure.com/).

> [!NOTE]
> Musi być administratorem globalnym, za pomocą konta organizacyjnego (na przykład @yourdomain.com), nie jest konto Microsoft (na przykład @outlook.com), aby włączyć usługi Azure AD Privileged Identity Management dla katalogu.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/) jako administrator globalny katalogu.
2. Jeśli organizacja dysponuje więcej niż jednym katalogiem, wybierz swoją nazwę użytkownika w prawym górnym rogu witryny Azure Portal. Wybierz katalog, w którym będziesz używać usługi Azure AD Privileged Identity Management.
3. Wybierz polecenie **Więcej usług** i użyj pola tekstowego filtru, aby wyszukać **Azure AD Privileged Identity Management**.
4. Zaznacz opcję **Przypnij do pulpitu nawigacyjnego**, a następnie kliknij pozycję **Utwórz**. Nastąpi otwarcie aplikacji Privileged Identity Management.

Jeśli jesteś pierwszą osobą, która będzie używać aplikacji Azure AD Privileged Identity Management w danym katalogu [kreator zabezpieczeń](active-directory-privileged-identity-management-security-wizard.md) przeprowadzi Cię przez początkowy etap przypisania. Po wykonaniu tej automatycznie staje się pierwszym **administrator zabezpieczeń** i **administrator ról uprzywilejowanych** katalogu.

Tylko administrator ról uprzywilejowanych może zarządzanie dostępem dla innych administratorów. Możesz [przekazać innym użytkownikom możliwość zarządzania w PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="privileged-identity-management-admin-dashboard"></a>Uprzywilejowane pulpitu nawigacyjnego administratora zarządzania tożsamościami
Azure AD Privileged Identity Manager udostępnia pulpit nawigacyjny administratora, zapewniająca ważne informacje, takie jak:

* Alerty, które wskazać możliwości zwiększające bezpieczeństwo
* Liczba użytkowników przypisanych do poszczególnych ról uprzywilejowanych  
* Liczba administratorów kwalifikujących się i stałe
* Wykres aktywacji ról uprzywilejowanych w katalogu

![Pulpit nawigacyjny PIM — zrzut ekranu][2]

## <a name="privileged-role-management"></a>Zarządzanie ról uprzywilejowanych
Z usługi Azure AD Privileged Identity Management można zarządzać administratorów, przez dodawanie lub usuwanie administratorów trwałych lub kwalifikujących się do każdej roli.

![Administratorzy dodawania i usuwania PIM — zrzut ekranu][3]

## <a name="configure-the-role-activation-settings"></a>Skonfiguruj ustawienia aktywacji roli
Przy użyciu [ustawienia roli](active-directory-privileged-identity-management-how-to-change-default-settings.md) można skonfigurować właściwości aktywacji kwalifikujących się roli, w tym:

* Okres aktywacji roli
* Powiadomienie dotyczące uaktywnienia roli
* Informacje, które użytkownik musi podać w procesie aktywacji w roli
* Numer biletu lub zdarzenia usługi
* [Wymagania w zakresie przepływu pracy zatwierdzenia - Preview](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![Zrzut ekranu — Aktywacja administratora — ustawienia usługi PIM][4]

Należy pamiętać, że w obrazie przyciski **uwierzytelnianie wieloskładnikowe** są wyłączone. Dla niektórych, wysoko uprzywilejowane ról, wymagamy MFA podwyższonym ochrony.

## <a name="role-activation"></a>Uaktywnienie roli
Aby [aktywować rolę](active-directory-privileged-identity-management-how-to-activate-role.md), administrator uprawnionych żądań czasu wiązaniem "Aktywacja" dla roli. Aktywacja może zażądać przy użyciu **Uaktywnij rolę Mój** opcji w usłudze Azure AD Privileged Identity Management.

Administrator, który chce aktywować rolę musi zainicjować usługi Azure AD Privileged Identity Management w portalu Azure.

Aktywacja roli jest można dostosowywać. W ustawieniach usługi PIM można określić długości aktywacji i informacje, administrator musi podać aktywowania roli.

![Aktywacja roli PIM administratora żądania — zrzut ekranu][5]

## <a name="review-role-activity"></a>Czynność przeglądu roli
Istnieją dwa sposoby śledzić pracowników i Administratorzy korzystania z ról uprzywilejowanych. Pierwsza opcja używa [Historia inspekcji ról katalogu](active-directory-privileged-identity-management-how-to-use-audit-log.md). Historia inspekcji dzienniki śledzenia zmian w przypisań ról uprzywilejowanych i historię aktywacji roli.

![Historia aktywacji PIM — zrzut ekranu][6]

Drugą opcją jest skonfigurowanie regular [dostępu przeglądami](active-directory-privileged-identity-management-how-to-start-security-review.md). Te przeglądami dostępu mogą być wykonywane przez i przypisane recenzenta (takie jak Menedżer zespołu) lub pracowników można przejrzeć samodzielnie. Jest to najlepszy sposób, aby monitorować kto nadal wymaga dostępu i który już nie występuje.

## <a name="azure-ad-pim-at-subscription-expiration"></a>Azure AD PIM na wygaśnięcia subskrypcji
Przed osiągnięciem ogólnej dostępności usługi Azure AD PIM był w wersji zapoznawczej i nie istnieją żadne testy licencji dla dzierżawy usługi Azure AD PIM podglądu.  Teraz, Azure AD PIM osiągnęła ogólnej dostępności, licencje próbne lub płatne musi zostać przypisane do administratorów dzierżawy nadal używać aplikacji PIM.  Jeśli Twoja organizacja nie zakupić Azure AD Premium P2 lub wersja próbna wygaśnie, przede wszystkim wszystkie funkcje usługi Azure AD PIM nie będą dostępne w dzierżawie.  Możesz przeczytać więcej informacji, zobacz [wymagań dotyczących subskrypcji usługi Azure AD PIM](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
