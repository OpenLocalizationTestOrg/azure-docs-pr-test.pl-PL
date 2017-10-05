---
title: "Zabezpieczanie uprzywilejowanego dostępu w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "Temat opisujący podejścia do zabezpieczania uprzywilejowanego dostępu na platformie Azure, Azure Active Directory i usług Microsoft Online Services."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: acd1c11cecfa37f607fe5d82a76a40647093f43f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a>Zabezpieczanie uprzywilejowanego dostępu w usłudze Azure AD
Zabezpieczanie uprzywilejowanego dostępu jest krytyczne pierwszy krok w celu ochrony zasobów biznesowych w organizacji modern. Uprzywilejowane konta są kontami, które Administruj i Zarządzaj systemów informatycznych. Osoby atakujące przez docelowe te konta do uzyskiwania dostępu do danych organizacji i systemów. Aby zabezpieczyć uprzywilejowanego dostępu, można odizolować kont i systemów ryzyka narażenia na złośliwy użytkownik.

Coraz więcej użytkowników uzyskać uprzywilejowany dostęp za pomocą usługi w chmurze. Może to obejmować Administratorzy globalni dla usługi Office 365, Administratorzy subskrypcji platformy Azure i użytkowników, którzy mają dostęp administracyjny na maszynach wirtualnych lub w aplikacji SaaS.

Firma Microsoft zaleca wykonanie tego planu [zabezpieczanie uprzywilejowanego dostępu](https://technet.microsoft.com/library/mt631194.aspx).

Dla klientów korzystających z usługi Azure Active Directory, usługi Office 365 lub innych usług firmy Microsoft i aplikacji czy konta użytkowników są zarządzane i uwierzytelniony przez usługę Active Directory lub w usłudze Azure Active Directory stosuje się te zasady. Poniższe sekcje zawierają więcej informacji na temat funkcji usługi Azure AD do obsługi zabezpieczanie uprzywilejowanego dostępu.

## <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication
Aby zwiększyć bezpieczeństwo administratora uwierzytelniania, należy włączyć weryfikację dwuetapową przed udzieleniem im uprawnienia. Weryfikacja dwuetapowa jest metodę sprawdzania, kto, które są wymagane jest użycie więcej niż tylko nazwę użytkownika i hasło. Zapewnia drugą warstwę zabezpieczeń do logowania użytkowników i transakcji.

Usługa Azure Multi-Factor Authentication (MFA) jest rozwiązania weryfikacji dwuetapowej firmy Microsoft, które ułatwia zabezpieczenie dostępu do danych i aplikacji, spełniając użytkownika popytu na prosty proces logowania. Zapewnia silne uwierzytelnianie za pośrednictwem szereg opcji weryfikacji łatwy w tym:

- połączenia telefoniczne
- Wiadomości SMS
- powiadomienia z aplikacji mobilnej
- kodów weryfikacyjnych aplikacji mobilnej
- Tokeny OATH innej firmy

Omówienie działania usługi Azure Multi-Factor Authentication można znaleźć w poniższym klipie wideo:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

Aby uzyskać więcej informacji, zobacz [MFA dla usługi Office 365 i uwierzytelniania Wieloskładnikowego na platformie Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).

## <a name="time-bound-privileges"></a>Uprawnienia powiązane z czasu
W niektórych organizacjach może się okazać mają zbyt wielu użytkownikom wysoko uprzywilejowane ról. Użytkownik mogły zostać dodane do roli dla danego działania, takie jak zalogowania się do usługi, ale nie był używany często później tych uprawnień.

Aby zmniejszyć czas ekspozycji uprawnień i zwiększyć Twojej wgląd w ich użycia, ograniczyć użytkownikom na pobieranie tylko na swoje uprawnienia "just in time" (JIT), których potrzebują do wykonania zadania. W przypadku usługi Azure Active Directory i usług Online firmy Microsoft, można użyć [Azure AD Privileged Identity zarządzania (PIM)](http://aka.ms/AzurePIM).

![Pulpit nawigacyjny usługi PIM][2]

## <a name="attack-detection"></a>Wykrywanie ataków
[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) udostępnia skonsolidowany wgląd w zdarzenia o podwyższonym ryzyku i potencjalnych luk w zabezpieczeniach wpływających na tożsamości organizacji. Oparte na zdarzenia o podwyższonym ryzyku, Identity Protection oblicza poziom ryzyka użytkownika, dla każdego użytkownika, dzięki któremu można konfigurować zasady ryzyka, aby automatycznie chronić tożsamości organizacji. Te zasady, oraz innych mechanizmów kontroli dostępu warunkowego zapewniane przez usługę Azure Active Directory i EMS, można automatycznie zablokować użytkownika lub udostępniania sugestii, obejmujące resetowanie haseł i wymuszania uwierzytelnianie wieloskładnikowe.

![Usługa Azure AD Identity Protection][3]

## <a name="conditional-access"></a>Dostęp warunkowy
Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza określonych warunków, można wybrać podczas uwierzytelniania użytkownika, przed zezwoleniem na dostęp do aplikacji. Gdy te warunki są spełnione, użytkownik jest uwierzytelniony i zezwolenie na dostęp do aplikacji.

![Ustawienie zasad dostępu warunkowego za pomocą usługi MFA][4]

## <a name="related-articles"></a>Pokrewne artykuły:
* Włącz [uwierzytelnianie wieloskładnikowe platformy Azure](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Włącz [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)
* Włącz [Azure AD Identity Protection](../active-directory-identityprotection.md)
* Włącz [kontroli dostępu warunkowego](../active-directory-conditional-access.md)

Aby uzyskać więcej informacji na tworzeniu planu pełną zabezpieczeń, zobacz sekcję "obowiązki klienta i plan" [Microsoft Cloud Security dla architektów Enterprise](http://aka.ms/securecustomer) dokumentu. Aby uzyskać więcej informacji na angażowaniu usług firmy Microsoft z dowolnego z tych tematów, skontaktuj się z przedstawicielem firmy Microsoft lub odwiedź nasze [strony rozwiązania bezpieczeństwa](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
