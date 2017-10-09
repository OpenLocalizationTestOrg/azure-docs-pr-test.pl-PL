---
title: "aaaHow Azure subskrypcje są kojarzone z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Logowanie tooMicrosoft Azure i powiązane zagadnienia, takie jak hello relacja między subskrypcją platformy Azure i usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bc4773c2-bc4a-4d21-9264-2267065f0aea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4f831cfb972efec57083fcaa63adb43fde7b2faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-subscriptions-are-associated-with-azure-active-directory"></a>Jak subskrypcje platformy Azure są kojarzone z usługą Azure Active Directory
Ten artykuł zawiera informacje na temat hello relacja między subskrypcją platformy Azure i usługi Azure Active Directory (Azure AD), jak i tooadd istniejący katalog usługi Azure AD tooyour subskrypcji.

## <a name="your-azure-subscriptions-relationship-tooazure-ad"></a>TooAzure relacji subskrypcji platformy Azure AD
Twoja subskrypcja platformy Azure ma relację zaufania z usługą Azure AD, co oznacza, że ufa hello katalogu tooauthenticate użytkowników, usług i urządzeń. Wiele subskrypcji może ufać hello tym samym katalogu, ale każda subskrypcja ufać tylko jednemu katalogowi. 

Witaj relacji zaufania, która ma subskrypcję z katalogiem różni się od relacji hello, która składa się z innymi zasobami na platformie Azure (witrynami sieci Web, baz danych i tak dalej). Jeśli subskrypcja wygaśnie, dostęp toohello inne zasoby skojarzone z subskrypcją hello również nie będzie możliwy. Jednak pozostanie katalog usługi Azure AD na platformie Azure i można skojarzyć z nim inną subskrypcję i zarządzać nimi hello katalogu przy użyciu hello nową subskrypcję.

![diagram przedstawiający sposób skojarzenia subskrypcji](./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png)

Wszyscy użytkownicy mają jeden katalog macierzysty, który ich uwierzytelnia, ale mogą również być gośćmi w innych katalogach. W usłudze Azure AD zobacz temat hello katalogów, których konto użytkownika jest członek lub Gość.

## <a name="azure-ad-and-cloud-service-subscriptions"></a>Usługa Azure AD i subskrypcje usług w chmurze
Usługa Azure AD zapewnia hello core katalogami i tożsamościami, możliwości zarządzania bazuje większość usług w chmurze firmy Microsoft, w tym:

* Azure
* Usługa Microsoft Office 365
* Usługa Microsoft Dynamics CRM Online
* Microsoft Intune

Po utworzeniu konta dla każdego z tych usług w chmurze firmy Microsoft możesz uzyskać hello bezpłatnej usługi Azure AD. Jeśli chcesz tooadd katalogu usługi Azure AD tooan dodatkowych subskrypcji platformy Azure, muszą być podpisane za pomocą konta Microsoft. Jeśli Zaloguj tooAzure z pracą lub konta służbowego, nie można dodać istniejącego katalogu tooan subskrypcji platformy Azure, ponieważ nie można uwierzytelnić konta firmowego lub szkolnego bezpośrednio przez platformę Azure. 

## <a name="tooadd-an-existing-subscription-tooyour-azure-ad-directory"></a>tooadd istniejący katalog usługi Azure AD tooyour subskrypcji
Musisz zalogować się przy użyciu konta, które istnieje w obu hello bieżącego katalogu, z którym hello jest skojarzona subskrypcja i w katalogu hello tooadd jej. 

1. Zaloguj się toohello [Centrum konta platformy Azure](https://account.windowsazure.com/Home/Index) przy użyciu konta administratora konta subskrypcji hello jest hello którego własność chcesz tootransfer.
2. Upewnij się, tym hello użytkownika, który ma się, że właściciel subskrypcji hello toobe znajduje się w katalogu hello docelowe.
3. Kliknij pozycję **Przenieś subskrypcję**.
4. Określ adresata hello. Adresat Hello automatycznie otrzymuje wiadomość e-mail z łączem akceptacji.
5. Hello odbiorca kliknie hello link i jest zgodna z instrukcji hello, łącznie z wprowadzania ich informacje dotyczące płatności. Podczas odbiorcy hello zakończy się powodzeniem, jest przenoszona hello subskrypcji. 
6. Witaj domyślny katalog hello subskrypcji zostanie zmieniona toohello katalog jest ten użytkownik hello.


## <a name="suggestions-toomanage-both-a-subscription-and-a-directory"></a>Sugestie toomanage zarówno subskrypcji, jak i katalogów
Hello role administracyjne dla subskrypcji platformy Azure umożliwia zarządzanie zasobami powiązanymi toohello subskrypcji platformy Azure. W tej sekcji opisano różnice hello Administratorzy subskrypcji platformy Azure i Administratorzy katalogu usługi Azure AD. Role administracyjne i innych sugestii dotyczących korzystania z ich subskrypcją są opisane w artykule toomanage [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles.md).

Domyślnie mają przypisaną rolę administratora usługi hello, podczas tworzenia konta. Jeśli inne muszą toosign w, a dostęp do usług za pomocą hello tej samej subskrypcji, możesz dodać je jako współadministratorów. 

Usługa Azure AD ma inny zestaw ról administracyjnych toomanage hello katalogu i funkcjami dotyczącymi tożsamości. Na przykład hello administratora globalnego katalogu można dodać użytkowników i grup toohello katalogu lub wymusić stosowanie uwierzytelniania wieloskładnikowego dla użytkowników. Użytkownik, który tworzy katalog przypisano rolę administratora globalnego toohello i może on przypisać role administracyjne tooother użytkowników. Role administracyjne usługi Azure AD są również używane przez inne usługi, takie jak Microsoft Intune i Office 365. 

Administratorzy subskrypcji platformy Azure i administratorzy katalogu usługi Azure AD to dwie oddzielne role. 
* Administratorzy subskrypcji platformy Azure mogą zarządzać zasobami na platformie Azure i użyć usługi Azure AD w hello portalu Azure (ponieważ hello portalu Azure, sam jest zasobem platformy Azure). 
* Administratorzy katalogu mogą zarządzać właściwościami tylko w katalogu usługi Azure AD hello.

Osoba może pełnić obie te role, lecz nie jest to wymagane. Administrator globalny katalogu nie musi być administratorem usługi ani współadministratorem subskrypcji platformy Azure lub odwrotnie. Nie jest administratorem subskrypcji hello, hello użytkownik mógł zalogować się w portalu Azure toohello, ale nie mogą zarządzać katalogami powitania dla tej subskrypcji w portalu hello. Ten użytkownik może jednak zarządzać katalogów przy użyciu innych narzędzi, takich jak Azure AD PowerShell lub hello Centrum administracyjne usługi Office 365.

## <a name="next-steps"></a>Następne kroki
* więcej informacji o toolearn, toochange Administratorzy subskrypcji platformy Azure, zobacz temat [przeniesienia własności tooanother konta subskrypcji platformy Azure](../billing/billing-subscription-transfer.md)
* Zobacz toolearn więcej informacji na temat sposobu jest kontrolowany dostęp do zasobów na platformie Microsoft Azure [opis dostęp do zasobów na platformie Azure](active-directory-understanding-resource-access.md)
* Aby uzyskać więcej informacji na temat ról tooassign w usłudze Azure AD, zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)

<!--Image references-->
[1]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_PassThruAuth.png
[2]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_OrgAccountSubscription.png
[3]: ./media/active-directory-how-subscriptions-associated-directory/WAAD_SignInDisambiguation.PNG
