---
title: "aaaDevelop aplikacji dla usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Przeznaczone dla specjalistów IT hello, w tym artykule przedstawiono wskazówki dotyczące integracji aplikacji Azure z usługą Active Directory."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a>Tworzenie aplikacji biznesowych z usługi Azure Active Directory
Ten przewodnik zawiera omówienie programu biznesowych (LoB) aplikacji dla .hello Azure Active Directory (AD), przeznaczone odbiorców jest Administratorzy globalni usługi Active Directory/Office 365.

## <a name="overview"></a>Omówienie
Tworzenie aplikacji zintegrowanych z usługą Azure AD pozwala użytkownikom w Twojej organizacji logowanie jednokrotne z usługą Office 365. Posiadanie aplikacji hello Azure AD pozwala kontrolować hello zasad uwierzytelniania dla aplikacji hello. więcej informacji na temat dostępu warunkowego i jak wyświetlić tooprotect aplikacji przy użyciu uwierzytelniania wieloskładnikowego (MFA) toolearn [Konfigurowanie reguł dostępu](active-directory-conditional-access-azuread-connected-apps.md).

Zarejestruj toouse Twojej aplikacji usługi Azure Active Directory. Rejestrowanie aplikacji hello oznacza, że deweloperów można użytkownicy tooauthenticate usługi Azure AD i żądania dostępu toouser zasoby, takie jak wiadomości e-mail, kalendarza i dokumenty.

Każdy członek katalogu (nie gości) można zarejestrować aplikacji, nazywanego *tworzenia obiektu aplikacji*.

Rejestrowanie aplikacji umożliwia skonfigurowanie następujących hello toodo dowolnego użytkownika:

* Uzyskać tożsamości dla swoich aplikacji, która rozpoznaje usługi Azure AD
* Jeden lub więcej klucze tajne/kluczy, które hello aplikacji można skorzystaj tooauthenticate samego tooAD
* Aplikacja hello marki w hello portalu Azure z niestandardowej nazwy, logo, itp.
* Zastosuj aplikacji tootheir funkcje autoryzacji usługi Azure AD, w tym:

  * Kontrola dostępu oparta na rolach (RBAC)
  * Usługa Azure Active Directory jako serwera autoryzacji oAuth (interfejs API udostępnianych przez aplikacji hello bezpieczna)
* Zadeklaruj wymaganych uprawnień niezbędnych do toofunction aplikacji hello zgodnie z oczekiwaniami, w tym:

      - Uprawnienia aplikacji (tylko administratorzy globalni). Na przykład: rola członkostwa w innej usłudze Azure AD aplikacji lub roli członkostwa względną tooan Azure zasobu, grupy zasobów, lub subskrypcji
      - Delegowane uprawnienia (każdy użytkownik). Na przykład: usługi Azure AD, logowania i odczytu profilu

> [!NOTE]
> Domyślnie każdy członek można zarejestrować aplikacji. toolearn toorestrict uprawnienia do rejestrowania aplikacji toospecific członków, zobacz temat [sposób dodawania aplikacji tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).
>
>

Oto należy, administrator globalny hello, muszą toodo toohelp deweloperzy tworzą ich stosowania gotowa do produkcji:

* Konfigurowanie reguł dostępu (zasady dostępu/MFA)
* Konfigurowanie przypisanie użytkownika toorequire aplikacji hello i przypisywać użytkowników
* Pomiń hello domyślne środowisko zgody użytkownika

## <a name="configure-access-rules"></a>Skonfiguruj reguły dostępu
Konfigurowanie aplikacji SaaS tooyour reguł dostępu dla poszczególnych aplikacji. Można na przykład wymagać uwierzytelniania MFA lub Zezwalaj toousers dostępu tylko w sieciach zaufanych. Szczegóły Hello tego są dostępne w dokumencie hello [Konfigurowanie reguł dostępu](active-directory-conditional-access-azuread-connected-apps.md).

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a>Konfigurowanie przypisanie użytkownika toorequire aplikacji hello i przypisywać użytkowników
Domyślnie użytkownicy mogą uzyskiwać dostęp do aplikacji bez przypisywane. Jednak aplikacja hello przedstawia role lub ma tooappear aplikacji hello na panelu dostępu użytkownika, należy włączyć przypisanie użytkownika.

[Requiring user assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) (Wymaganie przypisania użytkownika)

Jeśli jesteś subskrybentem Azure AD Premium lub Enterprise Mobility Suite (EMS), zdecydowanie zaleca się korzystanie z grup. Przypisywanie grup aplikacji toohello umożliwia toodelegate trwającą dostępu administracyjnego toohello właściciela grupy hello. Można utworzyć grupy hello lub poprosić stronę odpowiedzialny hello w grupie hello toocreate organizacji przy użyciu funkcji z grupy zarządzania.

[Przypisywanie użytkowników tooan aplikacji](active-directory-applications-guiding-developers-assigning-users.md)  
[Przypisywanie grup aplikacji tooan](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a>Pomiń zgody użytkownika
Domyślnie każdy użytkownik przechodzi przez toosign środowisko zgody w. środowisko zgody Hello, prosząc użytkowników toogrant uprawnienia aplikacji tooan może być niejasna dla użytkowników, którzy nie zna podejmowanie tych decyzji.

Dla aplikacji, którym ufasz można uprościć czynności użytkownika hello przez aplikację toohello zgodę imieniu swojej organizacji.

Aby uzyskać więcej informacji o zgodę użytkownika i zgody hello uruchomienia na platformie Azure, zobacz [integracji aplikacji z usługą Azure Active Directory](active-directory-integrating-applications.md).

## <a name="related-articles"></a>Pokrewne artykuły
* [Włączanie aplikacji lokalnych tooon bezpieczny dostęp zdalny za pomocą serwera Proxy aplikacji usługi Azure AD](active-directory-application-proxy-get-started.md)
* [Podgląd warunkowego dostępu na platformie Azure dla aplikacji SaaS](active-directory-conditional-access-azuread-connected-apps.md)
* [Zarządzanie tooapps dostępu w usłudze Azure AD](active-directory-managing-access-to-apps.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
