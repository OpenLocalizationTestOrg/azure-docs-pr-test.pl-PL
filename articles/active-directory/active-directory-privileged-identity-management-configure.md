---
title: aaaConfigure Azure AD Privileged Identity Management | Dokumentacja firmy Microsoft
description: "Temat, który wyjaśnia Azure AD Privileged Identity Management i w jaki sposób toouse PIM tooimprove zabezpieczeń chmury."
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
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>Co to jest Azure AD Privileged Identity Management?
Aplikacja Azure Active Directory (AD) Privileged Identity Management umożliwia kontrolę i monitorowanie dostępu, a także zarządzanie nim w ramach danej organizacji. Obejmuje to tooresources dostępu w usłudze Azure AD i innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune.  

> [!NOTE]
> Zarządzanie tożsamościami uprzywilejowanymi jest tooyour dostępne w całej organizacji, gdy licencji administratorami hello Premium P2 Edition usługi Azure Active Directory. Aby uzyskać więcej informacji, zobacz [Wersje usługi Azure Active Directory](active-directory-editions.md).

Organizacje mają toominimize hello liczbę użytkowników, którzy mają dostęp do informacji toosecure lub zasobów, ponieważ, która ogranicza ryzyko hello złośliwemu użytkownikowi uzyskiwanie dostępu. Użytkownicy nadal muszą mieć jednak toocarry uprzywilejowanych operacji w aplikacji Azure, Office 365 lub SaaS. Organizacje nadaj uprzywilejowanego dostępu użytkowników w usłudze Azure AD bez monitorowania, co robią tych użytkowników, używając swoich uprawnień administratora. Azure AD Privileged Identity Management pomaga tooresolve to ryzyko.  

Azure AD Privileged Identity Management pomaga:  

* Zobacz użytkowników, którzy są administratorami usługi Azure AD
* Włącz na żądanie "just in time" tooMicrosoft dostępu administracyjnego usług Online, takich jak Office 365 i Intune
* Uzyskaj raporty dotyczące historii dostępu administratora i zmian w przypisaniach administratora
* Uzyskiwanie alertów dotyczących ról uprzywilejowanych tooa dostępu
* Wymagaj zatwierdzenia tooactivate (wersja zapoznawcza)

Azure AD Privileged Identity Management, można zarządzać ról organizacyjnych hello wbudowane usługi Azure AD, w tym (między innymi):  

* Administrator globalny
* Administrator rozliczeń
* Administrator usługi  
* Administrator użytkowników
* Administrator haseł

## <a name="just-in-time-administrator-access"></a>Tylko w czasie dostępu administratora
W przeszłości można przypisać rolę administratora tooan użytkownika za pośrednictwem hello klasycznego portalu Azure lub programu Windows PowerShell. W związku z tym staje się **administrator trwały**, zawsze aktywny w roli hello przypisane. Azure AD Privileged Identity Management wprowadzono pojęcie hello **kwalifikujących się administrator**. Kwalifikujące się Administratorzy powinni mieć użytkowników, które wymagają uprzywilejowanego dostępu teraz, a następnie, ale nie każdego dnia. Rola Hello jest nieaktywny, dopóki hello użytkownik będzie potrzebował dostępu, a następnie zakończyć proces aktywacji i stają się aktywne administratora dla wstępnie określoną ilość czasu.

## <a name="enable-privileged-identity-management-for-your-directory"></a>Włącz zarządzanie tożsamościami uprzywilejowanymi dla katalogu
Możesz rozpocząć korzystanie z usługi Azure AD Privileged Identity Management w hello [portalu Azure](https://portal.azure.com/).

> [!NOTE]
> Musi być administratorem globalnym, za pomocą konta organizacyjnego (na przykład @yourdomain.com), nie jest konto Microsoft (na przykład @outlook.com), tooenable Azure AD Privileged Identity Management dla katalogu.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/) jako administrator globalny katalogu.
2. Jeśli Twoja organizacja ma więcej niż jeden katalog, w hello prawym górnym rogu hello portalu Azure wybierz nazwy użytkownika. Wybierz katalog hello, w którym będziesz używać usługi Azure AD Privileged Identity Management.
3. Wybierz **więcej usług** i użyj hello filtru pole tekstowe toosearch dla **Azure AD Privileged Identity Management**.
4. Sprawdź **toodashboard numeru Pin** , a następnie kliknij przycisk **Utwórz**. Otwiera Hello aplikacji Privileged Identity Management.

Jeśli jest hello toouse pierwszą osobą Azure AD Privileged Identity Management w katalogu, następnie hello [Kreator zabezpieczeń](active-directory-privileged-identity-management-security-wizard.md) przeprowadzi Cię przez kolejne hello początkowy etap przypisania. Po wykonaniu tej automatycznie staje się hello najpierw **administrator zabezpieczeń** i **administrator ról uprzywilejowanych** hello katalogu.

Tylko administrator ról uprzywilejowanych może zarządzanie dostępem dla innych administratorów. Możesz [umożliwić toomanage możliwości hello innych użytkowników w PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="privileged-identity-management-admin-dashboard"></a>Uprzywilejowane pulpitu nawigacyjnego administratora zarządzania tożsamościami
Azure AD Privileged Identity Manager udostępnia pulpit nawigacyjny administratora, zapewniająca ważne informacje, takie jak:

* Alerty, które wskazać możliwości tooimprove zabezpieczeń
* Witaj liczbę użytkowników, którzy są przypisane do ról uprzywilejowanych tooeach  
* Liczba Hello Administratorzy kwalifikujących się i stałe
* Wykres aktywacji ról uprzywilejowanych w katalogu

![Pulpit nawigacyjny PIM — zrzut ekranu][2]

## <a name="privileged-role-management"></a>Zarządzanie ról uprzywilejowanych
Z usługi Azure AD Privileged Identity Management można zarządzać Administratorzy hello przez dodanie lub usunięcie roli tooeach stałych lub kwalifikujących się Administratorzy.

![Administratorzy dodawania i usuwania PIM — zrzut ekranu][3]

## <a name="configure-hello-role-activation-settings"></a>Skonfiguruj ustawienia aktywacji hello roli
Przy użyciu hello [ustawienia roli](active-directory-privileged-identity-management-how-to-change-default-settings.md) można skonfigurować właściwości aktywacji kwalifikujących się roli hello w tym:

* czas trwania Hello okres aktywacji hello roli
* powiadomienie dotyczące uaktywnienia roli Hello
* informacje o Hello użytkownika muszą tooprovide w procesie aktywacji w rolach hello
* Numer biletu lub zdarzenia usługi
* [Wymagania w zakresie przepływu pracy zatwierdzenia - Preview](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![Zrzut ekranu — Aktywacja administratora — ustawienia usługi PIM][4]

Należy zwrócić uwagę w obrazie hello hello przycisków dla **uwierzytelnianie wieloskładnikowe** są wyłączone. Dla niektórych, wysoko uprzywilejowane ról, wymagamy MFA podwyższonym ochrony.

## <a name="role-activation"></a>Uaktywnienie roli
zbyt[aktywować rolę](active-directory-privileged-identity-management-how-to-activate-role.md), administrator uprawnionych żądań czasu wiązaniem "Aktywacja" hello roli. Witaj aktywacji można żądać przy użyciu hello **Uaktywnij rolę Moje** opcji w usłudze Azure AD Privileged Identity Management.

Administrator, który chce tooactivate roli musi tooinitialize Azure AD Privileged Identity Management w hello portalu Azure.

Aktywacja roli jest można dostosowywać. W ustawieniach usługi PIM hello można określić długości hello hello aktywacji i jakie informacje Witaj, Administratorze potrzebuje tooprovide tooactivate hello roli.

![Aktywacja roli PIM administratora żądania — zrzut ekranu][5]

## <a name="review-role-activity"></a>Czynność przeglądu roli
Istnieją dwa sposoby tootrack sposób umożliwiania pracownikom i Administratorzy korzystają z uprzywilejowany ról. Pierwsza opcja Hello jest przy użyciu [Historia inspekcji ról katalogu](active-directory-privileged-identity-management-how-to-use-audit-log.md). Historia inspekcji Hello dzienniki śledzenia zmian w przypisań ról uprzywilejowanych i historię aktywacji roli.

![Historia aktywacji PIM — zrzut ekranu][6]

Witaj drugą opcją jest tooset się regularne [dostępu przeglądami](active-directory-privileged-identity-management-how-to-start-security-review.md). Te przeglądami dostępu mogą być wykonywane przez i przypisane recenzenta (takie jak Menedżer zespołu) lub pracowników hello można przejrzeć samodzielnie. Jest to hello najlepsze toomonitor sposób który nadal wymaga dostępu i który już nie występuje.

## <a name="azure-ad-pim-at-subscription-expiration"></a>Azure AD PIM na wygaśnięcia subskrypcji
Wcześniejsze tooreaching ogólne dostępności usługi Azure AD PIM był w wersji zapoznawczej i nie było żadnych licencji sprawdza toopreview dzierżawy usługi Azure AD PIM.  Teraz, Azure AD PIM osiągnęła ogólnej dostępności, licencje próbne lub płatne musi być przypisany toohello Administratorzy hello toocontinue dzierżawcy przy użyciu usługi PIM.  Jeśli Twoja organizacja nie zakupić Azure AD Premium P2 lub wersja próbna wygaśnie, przede wszystkim wszystkie funkcje usługi Azure AD PIM hello nie będą dostępne w dzierżawie.  Więcej w hello [wymagań dotyczących subskrypcji usługi Azure AD PIM](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
