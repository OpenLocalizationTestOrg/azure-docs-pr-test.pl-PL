---
title: "Dokumentacja techniczna usługi Azure Active Directory dostępu warunkowego | Dokumentacja firmy Microsoft"
description: "Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza określonych warunków, można wybrać podczas uwierzytelniania użytkownika i przed zezwoleniem na dostęp do aplikacji. Gdy te warunki są spełnione, użytkownik jest uwierzytelniony i zezwolenie na dostęp do aplikacji."
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
ms.openlocfilehash: ca16a5399f94fd1ab267e0798cade3fd83f75b13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Dokumentacja techniczna usługi Azure Active Directory dostępu warunkowego

## <a name="services-enabled-with-conditional-access"></a>Włączone przy użyciu dostępu warunkowego usługi

Zasady dostępu warunkowego są obsługiwane w wielu różnych typów aplikacji usługi Azure AD. Ta lista zawiera:


* Zarejestrowanych aplikacji przy użyciu serwera Proxy aplikacji Azure
* Usługa Azure RemoteApp
* Rozwinięte wiersz działalności biznesowej i aplikacje wielodostępne w zarejestrowany z usługą Azure AD
* Dynamics CRM
* Aplikacji federacyjnych w galerii aplikacji usługi Azure AD
* Yammer pakietu Microsoft Office 365
* Microsoft Office 365 usługi Exchange Online
* Microsoft Office 365 SharePoint Online (w tym usługi OneDrive dla firm)
* Microsoft Power BI 
* Hasło logowania jednokrotnego aplikacje z galerii aplikacji Azure AD
* Visual Studio Team Services
* Microsoft Teams









## <a name="enable-access-rules"></a>Włącz zasady dostępu
Każda reguła może być włączona lub wyłączona na poszczególnych zasad aplikacji. Jeśli zasady są **ON** one będzie włączony i egzekwowane dla użytkowników uzyskujących dostęp do aplikacji. Gdy są one **OFF** nie będzie używany i nie ma wpływu na środowisko logowania użytkowników.

## <a name="applying-rules-to-specific-users"></a>Stosowania zasad do określonych użytkowników
Zasady można zastosować do określonych zestawów użytkowników oparte na grupę zabezpieczeń, ustawiając **Zastosuj do**. **Zastosuj do** może być ustawiony na **wszyscy użytkownicy** lub **grup**. Jeśli wartość **wszyscy użytkownicy** zasady zostaną zastosowane do każdego użytkownika z dostępu do aplikacji. **Grup** opcja umożliwia zabezpieczeń i grup dystrybucyjnych, należy wybrać tylko zostaną wymuszone zasady dla tych grup.

W przypadku wdrażania reguły, jest często stosowanym rozwiązaniem najpierw zastosować go ograniczony zestaw użytkowników, które są członkami grup pilotażowego. Po wykonaniu tych czynności reguły mogą dotyczyć **wszyscy użytkownicy**. To spowoduje, że reguły mają być egzekwowane dla wszystkich użytkowników w organizacji.

Wybierz grupy może również zostać wykluczony z zasad przy użyciu opcji **z wyjątkiem** opcji. Wszystkich członków tych grup będą zwolnione, nawet jeśli znajdują się w grupie uwzględnione.

## <a name="at-work-networks"></a>Sieci "w miejscu pracy"
Zasady dostępu warunkowego, korzystających z sieci "w miejscu pracy" zależą od zaufanych zakresów adresów IP, które zostały skonfigurowane w usłudze Azure AD, lub użyj oświadczenia "wewnątrz corpnet" z usług AD FS. Do tych reguł należą:

* Wymagaj uwierzytelniania wieloskładnikowego podczas nie podczas pracy
* Blokowanie dostępu, gdy nie w pracy

Określenie opcji sieci "w miejscu pracy"

1. Konfigurowanie zaufanych zakresy adresów IP w [strony konfiguracji uwierzytelniania wieloskładnikowego](../multi-factor-authentication/multi-factor-authentication-whats-next.md). Zasady dostępu warunkowego użyje skonfigurowanych zakresów we wszystkich żądań uwierzytelnienia i wydawania tokenów do oceny zasad. 
2. Skonfiguruj używanie wewnątrz oświadczeń corpnet tej opcji można użyć z katalogami federacyjnego, przy użyciu usług AD FS. Aby dowiedzieć się więcej na temat wewnętrznej corpnet oświadczeń, zobacz [adresów IP Tusted](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="rules-based-on-application-sensitivity"></a>Reguły oparte na czułości aplikacji
Reguły są konfigurowane dla poszczególnych aplikacji, dzięki czemu usługi wysokiej wartości być zabezpieczone bez wpływu na dostęp do innych usług. Można skonfigurować zasady dostępu warunkowego na **Konfiguruj** aplikacji. 

Zasady dostępne:

* **Wymagaj uwierzytelniania wieloskładnikowego**
  
  * Wszyscy użytkownicy, których dotyczą te zasady do będzie wymagane do uwierzytelniania za pośrednictwem usługi Multi-Factor authentication co najmniej raz.
* **Wymagaj uwierzytelniania wieloskładnikowego podczas nie podczas pracy**
  
  * Jeśli ta zasada jest stosowana, wszyscy użytkownicy będzie musiał wykonano uwierzytelnianie wieloskładnikowe w co najmniej raz, jeśli dostępu do usługi z lokalizacji zdalnej wolnych. Jeśli zostały przeniesione z pracy do zdalnej lokalizacji muszą przeprowadzać uwierzytelnianie wieloskładnikowe podczas uzyskiwania dostępu do usługi.
* **Blokowanie dostępu, gdy nie w pracy** 
  
  * Gdy użytkownik przeniesie z pracy do zdalnej lokalizacji, będą blokowani Jeśli zastosowano zasady "Blokowanie dostępu, gdy nie w pracy" do nich.  Ponownie zezwoleniem dostępu, gdy w miejscu pracy.

## <a name="related-topics"></a>Powiązane tematy
* [Zabezpieczanie dostępu do usługi Office 365 i innych aplikacji podłączone do usługi Azure Active Directory](active-directory-conditional-access.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)

