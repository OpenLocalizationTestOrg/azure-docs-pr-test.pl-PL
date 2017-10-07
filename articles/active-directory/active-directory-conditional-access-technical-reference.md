---
title: "informacje techniczne dotyczące dostępu warunkowego usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza hello określonych warunków, można wybrać podczas uwierzytelniania użytkownika hello i przed zezwoleniem na dostęp toohello aplikacji. Gdy te warunki są spełnione, użytkownik hello uwierzytelniony i dozwolone dostępu toohello aplikacji."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Dokumentacja techniczna usługi Azure Active Directory dostępu warunkowego

## <a name="services-enabled-with-conditional-access"></a>Włączone przy użyciu dostępu warunkowego usługi

Zasady dostępu warunkowego są obsługiwane w wielu różnych typów aplikacji usługi Azure AD. Ta lista zawiera:


* Aplikacje zarejestrowane na powitania serwera Proxy aplikacji Azure
* Usługa Azure RemoteApp
* Rozwinięte wiersz działalności biznesowej i aplikacje wielodostępne w zarejestrowany z usługą Azure AD
* Dynamics CRM
* Aplikacji federacyjnych z galerii aplikacji hello Azure AD
* Yammer pakietu Microsoft Office 365
* Microsoft Office 365 usługi Exchange Online
* Microsoft Office 365 SharePoint Online (w tym usługi OneDrive dla firm)
* Microsoft Power BI 
* Hasło logowania jednokrotnego aplikacje z galerii aplikacji hello Azure AD
* Visual Studio Team Services
* Microsoft Teams









## <a name="enable-access-rules"></a>Włącz zasady dostępu
Każda reguła może być włączona lub wyłączona na poszczególnych zasad aplikacji. Jeśli zasady są **ON** one będzie włączony i egzekwowane dla użytkowników uzyskujących dostęp do aplikacji hello. Gdy są one **OFF** nie będą używane i zostanie nie wpływ hello logowania środowisko.

## <a name="applying-rules-toospecific-users"></a>Stosowanie reguły toospecific użytkowników
Zasady mogą być zastosowane toospecific zbiorów użytkowników oparte na grupę zabezpieczeń, ustawiając **Zastosuj do**. **Zastosuj do** można ustawić także**wszyscy użytkownicy** lub **grup**. Gdy ustawiona zbyt**wszyscy użytkownicy** hello zasady będą stosowane tooany użytkownika z aplikacją toohello dostępu. Witaj **grup** opcja umożliwia zabezpieczeń i toobe grup dystrybucji zaznaczone, reguły będą wymuszane tylko dla tych grup.

W przypadku wdrażania reguły, jest często toofirst zastosowania określonych użytkowników, które są członkami grup pilotażowego. Gdy reguła pełną hello może zostać zastosowana za**wszyscy użytkownicy**. Spowoduje to reguła hello toobe wymuszone dla wszystkich użytkowników w organizacji hello.

Wybierz grupy może również zostać wykluczony z zasad przy użyciu hello **z wyjątkiem** opcji. Wszystkich członków tych grup będą zwolnione, nawet jeśli znajdują się w grupie uwzględnione.

## <a name="at-work-networks"></a>Sieci "w miejscu pracy"
Zasady dostępu warunkowego, korzystających z sieci "w miejscu pracy" zależą od zaufanych zakresów adresów IP, które zostały skonfigurowane w usłudze Azure AD, lub użycie hello "w sieci corpnet" oświadczeń z usług AD FS. Do tych reguł należą:

* Wymagaj uwierzytelniania wieloskładnikowego podczas nie podczas pracy
* Blokowanie dostępu, gdy nie w pracy

Określenie opcji sieci "w miejscu pracy"

1. Konfigurowanie zaufanych zakresów adresów IP w hello [strony konfiguracji uwierzytelniania wieloskładnikowego](../multi-factor-authentication/multi-factor-authentication-whats-next.md). Zasady dostępu warunkowego użyje zakresy hello skonfigurowane w każdej uwierzytelniania żądania i tokenu tooevaluate reguły wystawiania. 
2. Skonfiguruj używanie hello wewnątrz corpnet oświadczenia, ta opcja może być używany z katalogami federacyjnego, przy użyciu usług AD FS. toolearn więcej informacji na temat hello wewnątrz corpnet oświadczeń, zobacz [adresów IP Tusted](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="rules-based-on-application-sensitivity"></a>Reguły oparte na czułości aplikacji
Reguły są konfigurowane dla poszczególnych aplikacji, umożliwiając toobe usługi wysokiej wartości hello zabezpieczone bez wpływu na usługi tooother dostępu. Można skonfigurować zasady dostępu warunkowego na powitania **Konfiguruj** kartę aplikacji hello. 

Zasady dostępne:

* **Wymagaj uwierzytelniania wieloskładnikowego**
  
  * Wszyscy użytkownicy czy te zasady są stosowane toowill być wymagane tooauthenticate za pośrednictwem usługi Multi-Factor authentication co najmniej raz.
* **Wymagaj uwierzytelniania wieloskładnikowego podczas nie podczas pracy**
  
  * Jeśli ta zasada jest stosowana, wszyscy użytkownicy będzie wymagane toohave wykonać uwierzytelnianie wieloskładnikowe co najmniej raz, jeśli dostępu do usługi hello z lokalizacji zdalnej bez pracy. Jeśli przechodzą z miejsca pracy tooremote, zostaną one tooperform wymagane uwierzytelnianie wieloskładnikowe podczas uzyskiwania dostępu do usługi hello.
* **Blokowanie dostępu, gdy nie w pracy** 
  
  * Gdy użytkownik przeniesie z lokalizacji zdalnej tooa pracy, będą blokowani Jeśli hello "Blokowanie dostępu, gdy nie w pracy" zasady są stosowane toothem.  Ponownie zezwoleniem dostępu, gdy w miejscu pracy.

## <a name="related-topics"></a>Powiązane tematy
* [Zabezpieczanie dostępu tooOffice 365 i innych aplikacji połączone tooAzure usługi Active Directory](active-directory-conditional-access.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)

