---
title: "aaaSetting usługę Azure Active Directory dla zarządzania dostępem do aplikacji Sklep internetowy | Dokumentacja firmy Microsoft"
description: "Samoobsługowe zarządzanie grupami umożliwia użytkownikom toocreate i zarządzanie nimi grup zabezpieczeń lub grup usługi Office 365 w usłudze Azure Active Directory i grupy zabezpieczeń toorequest możliwość oferty użytkownicy hello lub członkostwa w grupach usługi Office 365"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 904d5c70-c34a-46c4-a9a7-d1efecf4821c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 2a73f4ed2532d41143fe5abe2fef1322d971a5c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-active-directory-for-self-service-group-management"></a>Konfigurowanie usługi Azure Active Directory do samoobsługowego zarządzania grupami
Samoobsługowe zarządzanie grupami umożliwia użytkownikom toocreate i zarządzaj nimi grup zabezpieczeń lub grup usługi Office 365 w usłudze Azure Active Directory (Azure AD). Użytkownicy mogą również żądać grupy zabezpieczeń lub członkostwa w grupach usługi Office 365, a następnie hello właściciela grupy hello można zatwierdzać lub odrzucać członkostwa. W ten sposób codziennych kontrolę nad członkostwa w grupie może być delegowane toopeople, znającym kontekst biznesowy tego członkostwa hello. Funkcje samoobsługowego zarządzania grupami są dostępne wyłącznie w przypadku grup zabezpieczeń i grup Office 365, natomiast nie są dostępne w przypadku list dystrybucyjnych lub grup zabezpieczeń z włączoną obsługą poczty.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.

Samoobsługowe zarządzanie grupami aktualnie obejmuje dwa podstawowe scenariusze: delegowane zarządzanie grupami i samoobsługowe zarządzanie grupami.

* **Delegowane Zarządzanie grupami** przykładem jest administratorem, który zarządza aplikacji SaaS tooa dostępu, które używają hello firmy. Zarządzanie prawami dostępu jest coraz większym obciążeniem, więc administrator zwraca hello firm właściciela toocreate nowej grupy. Hello administrator przydziela dostęp do nowej grupy toohello aplikacji hello i dodaje wszystkie osoby już dostęp do aplikacji toohello toohello grupy. następnie Hello właściciel firmy może dodawać kolejnych użytkowników, a ci użytkownicy są automatycznie aprowizowanego toohello aplikacji. Właściciel firmy Hello nie wymaga toowait hello dostępu toomanage administratora dla użytkowników. Jeśli hello administrator przyznał hello samego menedżera tooa uprawnień w inną grupą biznesową, a następnie tej osoby mogą również zarządzać dostępem własnych użytkowników. Właściciel firmy hello ani Menedżera hello można wyświetlać lub zarządzanie przez użytkowników. Witaj administrator nadal może wyświetlać wszystkich użytkowników, którzy mają dostęp do aplikacji toohello i blokować prawa dostępu w razie potrzeby.
* **Samoobsługowe zarządzanie grupami** Przykładem tego scenariusza jest dwóch użytkowników mających niezależnie skonfigurowane witryny usługi SharePoint Online. Chcą toogive każdego zespoły innych witryn tootheir dostępu. tooaccomplish, mogą utworzyć jedną grupę w usłudze Azure AD, a w usłudze SharePoint Online każdego z nich wybierze tej grupy tooprovide dostępu tootheir lokacji. Gdy ktoś chce uzyskać dostęp, wprowadzi żądanie w hello Panel dostępu, a po zatwierdzeniu otrzymują dostęp do witryn usługi SharePoint Online tooboth automatycznie. Jeden z nich zdecyduje później, wszystkie osoby, które uzyskuje dostęp do witryny hello powinny również uzyskać dostęp do tooa określonej aplikacji SaaS. administrator Hello hello aplikacji SaaS można dodać prawa dostępu do witryny usługi SharePoint Online toohello aplikacji hello. Następnie wszelkie żądania zatwierdzenia zapewnia dostęp toohello dwóch witryn usługi SharePoint Online, a także toothis aplikacji SaaS.

## <a name="making-a-group-available-for-end-user-self-service"></a>Włączanie samoobsługi użytkowników końcowych w grupie
1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), otwórz katalog usługi Azure AD.
2. Na powitania **Konfiguruj** ustaw **delegowane Zarządzanie grupami** tooEnabled.
3. Ustaw **użytkownicy mogą tworzyć grupy zabezpieczeń** lub **użytkownicy mogą tworzyć grupy Office** tooEnabled.

Gdy **użytkownicy mogą tworzyć grupy zabezpieczeń** jest włączone, wszyscy użytkownicy w katalogu mogą toocreate nowe grupy zabezpieczeń i dodać członków grupy toothese. Te nowe grupy będą również wyświetlane w hello Panel dostępu dla wszystkich innych użytkowników. Jeśli hello ustawienie zasad grupy hello pozwala na to, innych użytkowników można utworzyć żądania toojoin tych grup. Jeśli opcja **Użytkownicy mogą tworzyć grupy zabezpieczeń** jest wyłączona, użytkownicy nie mogą tworzyć grup ani zmieniać istniejących grup, których są właścicielami. Jednak nadal mogą Zarządzanie członkostwami hello tych grup i zatwierdzać żądania od innych użytkowników toojoin ich grup.

Można również użyć **użytkowników, którzy mogą używać samoobsługi dla grup zabezpieczeń** tooachieve bardziej szczegółowo kontroli dostępu na zarządzanie grupami samoobsługi dla użytkowników. Gdy **użytkownicy mogą tworzyć grupy** jest włączone, wszyscy użytkownicy w katalogu mogą toocreate nowe grupy i Dodaj członków grupy toothese. Przez ustawienie również **użytkowników, którzy mogą używać samoobsługi dla grup zabezpieczeń** tooSome, jest ograniczenie grupy zarządzania tooonly ograniczyć grupę użytkowników. Gdy ta opcja jest ustawiona tooSome, należy dodać użytkowników toohello grupy SSGMSecurityGroupsUsers zanim można tworzyć nowe grupy i Dodaj toothem elementy członkowskie. Przez ustawienie **użytkowników, którzy mogą używać samoobsługi dla grup zabezpieczeń** tooAll, umożliwia wszystkim użytkownikom w katalogu toocreate nowych grup.

Można również użyć hello **grupy, które mogą używać samoobsługi dla grup zabezpieczeń** polu toospecify niestandardową nazwę grupy, której członkowie mogą używać samoobsługi.

## <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Co to jest usługa Azure Active Directory?](active-directory-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
