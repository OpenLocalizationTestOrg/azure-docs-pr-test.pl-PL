---
title: "Subskrypcje Zarządzanie tożsamościami aaaPrivileged - Azure | Dokumentacja firmy Microsoft"
description: "Wyjaśniono hello subskrypcji i wymagania dotyczące zarządzania i przy użyciu usługi Azure AD Privileged Identity Management w dzierżawie licencjonowania"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 2639d13c250a582fdcf0b277c9bab37fdfcabcb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a>Wymagania subskrypcji w usłudze Azure Active Directory Privileged Identity Management

Azure AD Privileged Identity Management jest dostępny jako część hello Premium P2 edition usługi Azure AD. Aby uzyskać więcej informacji na temat hello innych funkcji P2 i jak porównuje tooPremium P1, zobacz [wersje usługi Azure Active Directory](../active-directory-editions.md).

>[!NOTE]
Gdy w wersji zapoznawczej usługi Azure Active Directory (Azure AD) Privileged Identity Management, nie było nie są sprawdzane licencji usługi hello tootry dzierżawy.  Teraz, Azure AD Privileged Identity Management została osiągnięta ogólnej dostępności, subskrypcji próbnej lub płatnej musi być dostępna hello toocontinue dzierżawcy przy użyciu Privileged Identity Management po grudnia 2016 r.
  

## <a name="confirm-your-trial-or-paid-subscription"></a>Potwierdzenie Twojej wersji próbnej lub płatnej subskrypcji

Jeśli nie masz pewności, czy Twoja organizacja ma okres próbny lub zakupić subskrypcję, można sprawdzić czy za pomocą poleceń hello objęte Azure Active Directory modułu dla Windows PowerShell V1 jest subskrypcji w dzierżawie. 
1. Otwórz okno programu PowerShell.
2. Wprowadź `Connect-MsolService` tooauthenticate jako użytkownik w dzierżawie.
3. Wprowadź `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.

To polecenie pobiera listę subskrypcji hello w dzierżawie. Jeśli są zwracane żadne wiersze, konieczne będzie wersji próbnej tooobtain Azure AD Premium P2, zakupu subskrypcji usługi Azure AD Premium P2 lub EMS E5 toouse subskrypcji usługi Azure AD Privileged Identity Management.  tooget wersji próbnej i rozpocząć korzystanie z usługi Azure AD Privileged Identity Management, przeczytaj [wprowadzenie do usługi Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

Jeśli to polecenie zwraca wiersz, w które SkuPartNumber jest "AAD_PREMIUM_P2" lub "EMSPREMIUM" i IsTrial ma "wartość prawda", oznacza to, że wersji próbnej platformy Azure AD Premium P2 znajduje się w dzierżawie powitalnych.  Jeśli hello stan subskrypcji nie jest włączona, a nie masz zakupu subskrypcji usługi Azure AD Premium P2 lub EMS E5, następnie należy zakupić subskrypcję usługi Azure AD Premium P2 lub toocontinue subskrypcji E5 pakietu EMS przy użyciu usługi Azure AD Privileged Identity Management.

Jest dostępna za pośrednictwem usługi Azure AD Premium P2 [Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), hello [programu licencjonowania zbiorowego Open](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx)i hello [dostawców rozwiązań w chmurze programu](https://partner.microsoft.com/en-US/cloud-solution-provider). Subskrybenci platformy Azure i usługi Office 365 można również kupić Azure AD Premium P2 w trybie online.  Więcej informacji na temat cen usługi Azure AD Premium i jak tooorder w trybie online można znaleźć pod [Azure Active Directory cennik](https://azure.microsoft.com/en-us/pricing/details/active-directory/).

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a>Nie jest dostępna w dzierżawie usługi Azure AD Privileged Identity Management

Azure AD Privileged Identity Management nie będą już dostępne w Twojej dzierżawie jeśli:
- Organizacji została przy użyciu usługi Azure AD Privileged Identity Management w wersji zapoznawczej i nie zakupu subskrypcji usługi Azure AD Premium P2 lub EMS E5 subskrypcji.
- Twoja organizacja nie usługi Azure AD Premium P2 lub E5 EMS wersji próbnej, która wygasła.
- Twoja organizacja ma zakupiono subskrypcję, która wygasła.

Po wygaśnięciu subskrypcji Azure AD Premium P2 lub subskrypcji EMS E5 lub jako organizacja, która była za pomocą usługi Azure AD Privileged Identity Management w wersji zapoznawczej nie uzyskał P2 Azure AD Premium lub pakietu EMS E5 subskrypcji:

- Rola stałych przypisań tooAzure AD role pozostaną nienaruszone.
- Hello rozszerzenie Azure AD Privileged Identity Management w hello portalu Azure, a także polecenia cmdlet interfejsu API programu Graph hello i interfejsów środowiska PowerShell usługi Azure AD Privileged Identity Management, nie jest już dostępne dla użytkowników, role uprzywilejowane tooactivate, zarządzanie uprzywilejowany dostęp, lub wykonaj dostępu Przegląd ról uprzywilejowanych.
- Przypisania ról kwalifikujące się usługi Azure AD ról zostanie usunięta, użytkownicy nie będą już mogli tooactivate uprzywilejowany ról.
- Zakończy wszystkie przeglądy trwającą dostępu ról usługi Azure AD i będzie można usunąć ustawień konfiguracji usługi Azure AD Privileged Identity Management.
- Azure AD Privileged Identity Management nie będzie wysyłać wiadomości e-mail na zmiany przypisania roli.

## <a name="next-steps"></a>Następne kroki

- [Wprowadzenie do usługi Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)
- [Role w usłudze Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-roles.md)
